---
name: pubmed_literature_retrieval
description: Structured PubMed search strategies using MeSH terms, Boolean operators, and E-utilities API for systematic literature retrieval
tags: [assistance, P1, database-access, literature, pubmed, systematic-review]
domain: general
source:
  type: literature
  reference: "https://github.com/K-Dense-AI/claude-scientific-skills (pubmed-database skill); https://pubmed.ncbi.nlm.nih.gov/help/"
  evidence_level: systematic
---
# PubMed Literature Retrieval

## Purpose
Guide structured literature searches for research planning, systematic reviews, and novelty verification. Complements `novelty_gap_mapper` with operational search strategies.

## When to Search PubMed

| Research Phase | Search Goal | Strategy |
|---------------|-------------|----------|
| Project planning | Landscape scan | Broad MeSH + review filter |
| Hypothesis formation | Gap identification | Specific terms + NOT known results |
| Methods design | Protocol precedents | Method terms + publication type filter |
| Writing introduction | Context building | MeSH hierarchy + date range |
| Reviewer response | Evidence for claims | Precise queries with field tags |

## Query Construction Framework

### Step 1: Decompose Research Question (PICO)
- **P**opulation/Problem: What organism, tissue, disease?
- **I**ntervention/Exposure: What treatment, method, variable?
- **C**omparison: What control or alternative?
- **O**utcome: What measurement or result?

### Step 2: Map to MeSH Terms + Free Text
```
# Example: "Does RNA-seq batch correction affect differential expression in mouse liver?"

MeSH:   RNA-Seq[mh] AND Liver[mh] AND Mice[mh]
Free:   batch effect*[tiab] OR batch correction[tiab]
Combined: (RNA-Seq[mh] AND Liver[mh] AND Mice[mh]) AND (batch effect*[tiab] OR batch correction[tiab])
```

### Step 3: Apply Filters
- Date: `2020:2024[dp]` (scope to recent work)
- Language: `english[la]`
- Type: `systematic review[pt]` or `randomized controlled trial[pt]`
- Availability: `free full text[sb]`

## Essential Field Tags

| Tag | Field | Use When |
|-----|-------|----------|
| `[mh]` | MeSH heading | Controlled vocabulary (preferred for precision) |
| `[majr]` | MeSH major topic | Topic is the paper's main focus |
| `[tiab]` | Title/Abstract | New terms not yet in MeSH |
| `[au]` | Author | Searching specific researcher's work |
| `[1au]` | First author | Primary contributor search |
| `[pt]` | Publication type | Filter by study design |
| `[dp]` | Date published | Time-scope results |
| `[ta]` | Journal title | Field-specific journals |

## Common MeSH Subheadings for Genomics

| Subheading | Use For |
|-----------|---------|
| `/genetics` | Genetic aspects of a disease/condition |
| `/methods` | Methodological papers |
| `/analysis` | Analytical approaches |
| `/drug therapy` | Treatment studies |
| `/epidemiology` | Population-level patterns |

## Search Strategies by Use Case

### Systematic Review Search
```
# Comprehensive: MeSH + free text + exploded terms
(RNA-Seq[mh] OR "RNA sequencing"[tiab] OR transcriptom*[tiab])
AND (single cell[mh] OR "single-cell"[tiab] OR "scRNA-seq"[tiab])
AND (quality control[mh] OR "batch effect"[tiab] OR normalization[tiab])
AND 2020:2024[dp]
```
- Document exact query, date, and result count (see `methods_reproducibility_writer`)
- Use PRISMA flow diagram for screening

### Quick Novelty Check
```
"your specific method or finding"[tiab] AND relevant_organism[mh]
```
- Zero results suggests novelty (but check synonyms)
- Few results: read carefully to differentiate your contribution

### Competitor/Collaborator Scan
```
smith j[au] AND (genomics[mh] OR bioinformatics[mh]) AND 2023:2024[dp]
```

## Programmatic Access (E-utilities)

### When to Use API vs. Web Interface
- **Web**: Exploratory searches, < 50 results, MeSH tree browsing
- **API**: Reproducible searches, batch retrieval, pipeline integration, > 100 results

### Core API Pattern (Python)
```python
from Bio import Entrez
Entrez.email = "your.email@example.com"  # Required
Entrez.api_key = "YOUR_KEY"              # 10 req/s vs 3 req/s

# Search
handle = Entrez.esearch(db="pubmed", term="YOUR_QUERY", retmax=100, usehistory="y")
results = Entrez.read(handle)

# Fetch abstracts
handle = Entrez.efetch(db="pubmed", webenv=results["WebEnv"],
                       query_key=results["QueryKey"], rettype="abstract", retmode="text")
```

### Rate Limits and Best Practices
- Without API key: max 3 requests/second
- With API key: max 10 requests/second (get key at NCBI)
- Use `usehistory="y"` for large result sets
- Cache results locally; don't re-fetch unchanged queries
- Always include `Entrez.email` (NCBI requirement)

## Result Evaluation Checklist
- [ ] Query documented with exact syntax and date
- [ ] Result count recorded
- [ ] MeSH terms verified against MeSH Browser
- [ ] Synonyms and alternative spellings included
- [ ] Publication type filter appropriate for question
- [ ] Results exported in structured format (PMID list or citation manager)

## Integration with ResearchersChain Skills
- Feeds into `novelty_gap_mapper` (gap identification)
- Search strategy documented via `methods_reproducibility_writer`
- Multiple comparisons awareness: `multiple_testing_controller` (for meta-analyses)
- Citation management: pair with reference manager (Zotero/pyzotero)
- Claims from literature validated by `claim_evidence_separator`