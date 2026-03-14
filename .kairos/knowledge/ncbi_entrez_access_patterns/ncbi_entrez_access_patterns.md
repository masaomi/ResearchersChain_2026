---
name: ncbi_entrez_access_patterns
description: Programmatic access to NCBI databases (GEO, SRA, Gene, Nucleotide, Protein) via BioPython Entrez for batch data retrieval
tags: [analysis, P1, database-access, ncbi, bioinformatics, biopython, data-retrieval]
domain: genomics
source:
  type: literature
  reference: "https://github.com/K-Dense-AI/claude-scientific-skills (biopython skill); https://biopython.org/wiki/Documentation"
  evidence_level: systematic
---
# NCBI Entrez Access Patterns

## Purpose
Guide programmatic access to NCBI's 38+ databases via BioPython's Entrez module. Covers database selection, query patterns, batch retrieval, and responsible API usage for genomics research.

## When to Use Entrez vs. Alternatives

| Task | BioPython Entrez | gget | Web Browser |
|------|-----------------|------|-------------|
| Batch metadata retrieval (>100 records) | Best | Limited | Impractical |
| SRA/GEO dataset discovery | Best | No | Possible |
| PubMed programmatic search | Best | No | OK for small queries |
| Gene info (single gene) | Overkill | Best | Fine |
| Sequence download (batch) | Best | OK (small sets) | No |
| Cross-database linking | Best (elink) | Partial | Manual |

## Setup (Required for All Queries)
```python
from Bio import Entrez
Entrez.email = "your.email@institution.edu"  # NCBI requirement
Entrez.api_key = "YOUR_KEY"                  # Optional: 10 vs 3 req/s
```
Get API key: https://www.ncbi.nlm.nih.gov/account/settings/

## Database Selection Guide

| Database | db parameter | Contains | Typical Use |
|----------|-------------|----------|-------------|
| PubMed | `pubmed` | Literature citations | Systematic reviews, citation lookup |
| Gene | `gene` | Gene records | Gene info, nomenclature, orthologs |
| Nucleotide | `nucleotide` | DNA/RNA sequences | Sequence retrieval, reference seqs |
| Protein | `protein` | Protein sequences | Protein sequence analysis |
| SRA | `sra` | Sequencing runs | Find raw data for reanalysis |
| GEO DataSets | `gds` | Expression datasets | Find published datasets |
| GEO Profiles | `geoprofiles` | Gene expression profiles | Single-gene expression patterns |
| Taxonomy | `taxonomy` | Organism classification | Species verification |
| Assembly | `assembly` | Genome assemblies | Reference genome selection |
| ClinVar | `clinvar` | Clinical variants | Variant clinical significance |
| dbSNP | `snp` | SNP records | Variant lookup |

## Core API Patterns

### Pattern 1: Search + Fetch (Most Common)
```python
# Search
handle = Entrez.esearch(db="gene", term="BRCA1[Gene Name] AND human[Organism]", retmax=10)
record = Entrez.read(handle)
ids = record["IdList"]

# Fetch full records
handle = Entrez.efetch(db="gene", id=ids, retmode="xml")
records = Entrez.read(handle)
```

### Pattern 2: Large Result Sets (History Server)
```python
# Search with history
handle = Entrez.esearch(db="pubmed", term="single-cell RNA-seq[tiab]",
                        retmax=0, usehistory="y")
result = Entrez.read(handle)
count = int(result["Count"])
webenv = result["WebEnv"]
query_key = result["QueryKey"]

# Fetch in batches of 500
batch_size = 500
for start in range(0, count, batch_size):
    handle = Entrez.efetch(db="pubmed", retstart=start, retmax=batch_size,
                           webenv=webenv, query_key=query_key,
                           rettype="medline", retmode="text")
    data = handle.read()
    # process batch...
```

### Pattern 3: Cross-Database Linking
```python
# Gene -> PubMed (find papers about a gene)
handle = Entrez.elink(dbfrom="gene", db="pubmed", id="672")  # BRCA1
result = Entrez.read(handle)
pubmed_ids = [link["Id"] for link in result[0]["LinkSetDb"][0]["Link"]]

# Gene -> Nucleotide (find sequences for a gene)
handle = Entrez.elink(dbfrom="gene", db="nucleotide", id="672")
```

### Pattern 4: GEO Dataset Discovery
```python
# Find RNA-seq datasets for a condition
handle = Entrez.esearch(db="gds", term="liver cancer[Description] AND gse[Entry Type] AND Homo sapiens[Organism]", retmax=20)
result = Entrez.read(handle)

# Get dataset summaries
handle = Entrez.esummary(db="gds", id=",".join(result["IdList"]))
summaries = Entrez.read(handle)
for s in summaries:
    print(f"GSE{s['Accession']}: {s['title']} ({s['n_samples']} samples)")
```

### Pattern 5: SRA Metadata for Reanalysis
```python
# Find SRA runs for a project
handle = Entrez.esearch(db="sra", term="PRJNA123456[BioProject]", retmax=500)
result = Entrez.read(handle)

# Fetch run metadata (XML)
handle = Entrez.efetch(db="sra", id=result["IdList"], rettype="full", retmode="xml")
```

## Rate Limits and Responsible Usage

| | Without API Key | With API Key |
|-|----------------|--------------|
| Requests/second | 3 | 10 |
| Recommended | Development only | All production use |

### Best Practices
- Always set `Entrez.email` (NCBI will contact you before blocking)
- Use history server (`usehistory="y"`) for queries returning >500 results
- Implement exponential backoff on HTTP 429 errors
- Cache results locally (NCBI data updates weekly, not hourly)
- Run large batch jobs during off-peak hours (US Eastern evening/night)

## Common Query Patterns for Genomics

### RNA-seq Data Discovery
```
"RNA-Seq"[Strategy] AND "Homo sapiens"[Organism] AND "liver"[Text Word] AND 2023:2024[Publication Date]
```

### Finding Reference Sequences
```
BRCA1[Gene Name] AND "Homo sapiens"[Organism] AND RefSeqGene[Filter]
```

### Variant Lookup
```
BRCA1[Gene] AND pathogenic[Clinical Significance]  (db: clinvar)
```

## Result Validation
- Cross-check GEO sample counts against the paper's methods section
- Verify SRA run accessions resolve correctly before downloading
- Confirm taxonomy ID matches expected organism
- For clinical data: verify variant classifications against ClinVar review status

## Integration with ResearchersChain Skills
- GEO/SRA discovery feeds into `ngs_pipeline_designer` (data acquisition step)
- PubMed queries use strategies from `pubmed_literature_retrieval`
- Batch downloads tracked by `provenance_chain_builder` (record accessions + dates)
- Cross-database linking complements `gget_genomics_query_guide` (gget for quick lookups, Entrez for batch)
- API key and email documented via `analysis_environment_recorder`