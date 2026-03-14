---
name: uniprot_functional_annotation
description: Query and interpret UniProt protein entries for functional annotation, ID mapping, and cross-database integration
tags: [analysis, P1, database-access, proteomics, protein, uniprot, bioinformatics]
domain: genomics
source:
  type: literature
  reference: "https://github.com/K-Dense-AI/claude-scientific-skills (uniprot-database skill); https://www.uniprot.org/help/api"
  evidence_level: systematic
---
# UniProt Functional Annotation

## Purpose
Guide protein functional annotation queries via UniProt REST API. Covers search strategies, ID mapping between databases, data quality assessment (Swiss-Prot vs. TrEMBL), and integration with genomics workflows.

## When to Use UniProt

| Task | UniProt Approach | Alternative |
|------|-----------------|-------------|
| Gene function annotation (from RNA-seq DE list) | Batch search by gene name + organism | gget info (simpler, less detail) |
| Protein domain architecture | Search + retrieve `ft_domain` fields | InterPro (more comprehensive) |
| GO term retrieval | Search + `go_*` fields | QuickGO, AmiGO |
| ID mapping (Ensembl -> UniProt -> PDB) | ID Mapping API | gget info (partial) |
| Protein-protein interactions | Cross-ref to STRING | STRING API directly |
| Sequence retrieval (protein) | FASTA endpoint | gget seq -t |

## Data Quality: Swiss-Prot vs. TrEMBL

This distinction is critical for research reliability:

| | Swiss-Prot (reviewed) | TrEMBL (unreviewed) |
|-|----------------------|---------------------|
| Curation | Manual expert review | Automated annotation |
| Size | ~570K entries | ~250M entries |
| Reliability | High (cite directly) | Variable (verify claims) |
| Filter | `reviewed:true` | `reviewed:false` |
| Use in papers | Safe to cite | Flag as computational prediction |

**Rule**: Always prefer Swiss-Prot entries. When only TrEMBL is available, note this limitation in your methods.

## Search Strategy by Research Context

### After Differential Expression Analysis
```
# Map DE gene list to protein functions
Query: gene:{GENE_NAME} AND organism_id:9606 AND reviewed:true
Fields: accession,gene_names,protein_name,go_p,go_f,go_c,cc_function
Format: tsv
```

### Protein Domain Investigation
```
# Find all human kinases with specific domain
Query: annotation:(type:domain AND name:"Protein kinase") AND organism_id:9606 AND reviewed:true
Fields: accession,gene_names,ft_domain,length,cc_catalytic_activity
```

### Cross-Species Comparison
```
# Find orthologs across model organisms
Query: gene:BRCA1 AND (organism_id:9606 OR organism_id:10090 OR organism_id:7955)
Fields: accession,gene_names,organism_name,sequence,length
```

## ID Mapping Workflow

### Common Mappings for Genomics

| From | To | Use Case |
|------|-----|----------|
| Ensembl Gene ID | UniProtKB | RNA-seq gene list -> protein function |
| UniProtKB | PDB | Protein -> 3D structure |
| UniProtKB | KEGG | Protein -> pathway context |
| Gene Name | UniProtKB | Literature search -> protein data |
| RefSeq Protein | UniProtKB | NCBI annotation -> UniProt |

### API Pattern
```python
import requests

# Submit mapping job
response = requests.post(
    "https://rest.uniprot.org/idmapping/run",
    data={"from": "Ensembl", "to": "UniProtKB", "ids": "ENSG00000012048,ENSG00000141510"}
)
job_id = response.json()["jobId"]

# Poll for results
results = requests.get(f"https://rest.uniprot.org/idmapping/results/{job_id}")
```

### Batch Limits
- Max 100,000 IDs per job
- Results stored for 7 days
- For larger sets: split into chunks, implement retry logic

## Key Fields for Genomics Research

| Field | API Name | Contains |
|-------|----------|----------|
| Function | `cc_function` | Protein function description |
| GO Biological Process | `go_p` | Biological process terms |
| GO Molecular Function | `go_f` | Molecular function terms |
| GO Cellular Component | `go_c` | Subcellular localization |
| Domains | `ft_domain` | Domain annotations |
| Subcellular location | `cc_subcellular_location` | Where protein localizes |
| Tissue specificity | `cc_tissue_specificity` | Expression patterns |
| Disease | `cc_disease` | Disease associations |
| Interaction | `cc_interaction` | Known binding partners |

## Result Interpretation Guidelines

### Annotation Confidence
- **Experimental evidence codes** (ECO:0000269): Directly cite
- **Inferred by similarity** (ECO:0000250): Note as "predicted by homology"
- **Electronic annotation** (ECO:0000501): Treat as hypothesis, not fact

### Common Pitfalls
- Gene name ambiguity: always include organism filter
- Isoform handling: canonical vs. alternative sequences differ
- Obsolete accessions: check entry status, follow redirect
- GO term propagation: child terms are more specific, parent terms may be misleading

## Integration with ResearchersChain Skills
- Feeds into `ngs_pipeline_designer` (functional enrichment step)
- ID mapping results validated by `provenance_chain_builder` (track mapping versions)
- Cross-referenced with `gget_genomics_query_guide` (gget info provides UniProt cross-refs)
- Protein claims checked by `claim_evidence_separator` (evidence code awareness)
- Reproducibility: pin UniProt release version (see `seed_and_version_enforcer`)