---
name: draft_provenance_chain_builder
description: Build data provenance chain from raw data to final results
category: reproducibility
priority: P0
evolution_criterion: Improves reproducibility — traceable data lineage enables verification and audit
---
# Provenance Chain Builder (Draft)
## Workflow
1. Identify raw data source (GEO accession, internal ID, sequencing run)
2. Record each transformation step (QC, trimming, alignment, quantification, normalization)
3. For each step: input files, output files, tool + version, parameters, timestamp
4. Link steps into a directed acyclic graph (DAG)
5. Verify chain completeness (no missing intermediate steps)
6. Output: provenance chain document (YAML/JSON) with DAG visualization suggestion
