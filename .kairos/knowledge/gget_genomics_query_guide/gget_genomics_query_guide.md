---
name: gget_genomics_query_guide
description: Unified access to 20+ genomics databases via gget for gene info, BLAST, enrichment, and structure queries
tags: [analysis, P1, database-access, genomics, bioinformatics, gget]
domain: genomics
source:
  type: literature
  reference: "https://github.com/K-Dense-AI/claude-scientific-skills (gget skill); https://github.com/pachterlab/gget"
  evidence_level: systematic
---
# gget Genomics Query Guide

## Purpose
Provide structured guidance for querying 20+ genomics databases through gget's unified CLI/Python interface. Covers when to use each module, result interpretation, and integration with downstream analysis.

## When to Use gget vs. Alternatives

| Scenario | Use gget | Use BioPython/Entrez | Use BioServices |
|----------|----------|---------------------|-----------------|
| Quick gene lookup | Yes | Overkill | Overkill |
| Batch processing (>1000 queries) | No | Yes | Depends |
| BLAST (interactive) | Yes (`gget blast`) | Yes (more control) | No |
| Multi-database Python pipeline | Possible | Better | Best |
| AlphaFold structure retrieval | Yes (`gget alphafold`) | No | No |
| Enrichment analysis | Yes (`gget enrichr`) | No | Possible |

## Module Decision Tree

### 1. Gene/Transcript Information
- **"What gene is this?"** -> `gget search` (search by name/description across species)
- **"Details on this Ensembl ID?"** -> `gget info` (UniProt, NCBI, PDB cross-references)
- **"Get the sequence"** -> `gget seq` (nucleotide or protein FASTA)
- **"Download reference genome"** -> `gget ref` (Ensembl reference files)

### 2. Sequence Analysis
- **"Where does this sequence match?"** -> `gget blast` (NCBI BLAST) or `gget blat` (UCSC BLAT for genomic coordinates)
- **"Align two sequences"** -> `gget muscle` (multiple sequence alignment via MUSCLE5)

### 3. Functional Analysis
- **"What pathways are enriched?"** -> `gget enrichr` (Enrichr gene set enrichment)
- **"What's the protein structure?"** -> `gget alphafold` (AlphaFold predicted structures)
- **"Find orthologs"** -> `gget info` with cross-species Ensembl IDs

### 4. Expression & Disease
- **"Expression across tissues?"** -> `gget archs4` (ARCHS4 expression data from RNA-seq)
- **"Disease associations?"** -> `gget opentargets` (Open Targets disease-gene links)
- **"Sequence variants?"** -> `gget cosmic` (COSMIC somatic mutations, requires license)

## Common Workflows for Genomics Research

### Workflow A: Gene Characterization (RNA-seq follow-up)
```
1. gget search -s human "gene_name"       # Find Ensembl ID
2. gget info ENSG...                       # Cross-database metadata
3. gget seq -t ENSG...                     # Protein sequence
4. gget alphafold ENSG...                  # Predicted structure
5. gget enrichr --db GO_Biological_Process_2023 GENE1 GENE2 ...  # Pathway context
```

### Workflow B: Variant Investigation
```
1. gget info ENSG... -pdb                  # Gene context + PDB structures
2. gget cosmic --muttype substitution GENE # Known somatic mutations
3. gget blast SEQUENCE                     # Check conservation
4. gget opentargets ENSG...                # Disease relevance
```

### Workflow C: Reference Preparation (before pipeline run)
```
1. gget ref homo_sapiens -w gtf            # Latest Ensembl GTF
2. gget ref homo_sapiens -w dna            # Genome FASTA
3. gget ref --list_species                 # Check available organisms
```

## Key Parameters and Pitfalls

### Species Naming
- Use `homo_sapiens` or shortcut `human`; `mus_musculus` or `mouse`
- Case-insensitive for shortcuts, but Genus_species format for others

### Ensembl Release Pinning
- Default: latest release. For reproducibility, always pin: `gget ref -r 111 human`
- Document the release number in your methods section (see `seed_and_version_enforcer`)

### Rate Limits and Caching
- `gget blast` uses NCBI servers: respect 3 req/s (10 with API key)
- `gget alphafold` downloads PDB files: cache locally for repeated access
- Large batch queries: consider BioPython Entrez for better batch control

### Result Validation
- Always cross-check `gget info` results against the primary source (Ensembl/UniProt web)
- BLAST results: check E-value AND query coverage, not just top hit
- Enrichment results: report adjusted p-values, not raw p-values (see `multiple_testing_controller`)

## Installation
```bash
uv pip install --upgrade gget
```

## Integration with ResearchersChain Skills
- Results feed into `ngs_pipeline_designer` (reference preparation)
- Enrichment results validated by `multiple_testing_controller`
- Reproducibility ensured by `seed_and_version_enforcer` (pin gget + Ensembl versions)
- Privacy considerations for human data: check `privacy_risk_preflight`