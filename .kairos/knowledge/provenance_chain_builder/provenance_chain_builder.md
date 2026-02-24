---
name: provenance_chain_builder
description: Build data provenance chain from raw data to final results
tags: [reproducibility, P0, provenance, lineage, audit]
promoted_from: L2/afd_foundation_001/draft_provenance_chain_builder
evolution_criterion: Improves reproducibility — traceable data lineage enables verification and audit
---
# Provenance Chain Builder

## Purpose
Build a complete, traceable chain from raw data to published results.

## Workflow
1. Identify raw data source (GEO accession, internal ID, sequencing run)
2. Record each transformation step
3. For each step: input files, output files, tool + version, parameters, timestamp
4. Link steps into a DAG (directed acyclic graph)
5. Verify chain completeness (no missing intermediate steps)
6. Output: provenance document with DAG

## Provenance Record Template
```yaml
provenance:
  raw_data:
    source: "GEO:GSE123456"
    files: ["sample1_R1.fastq.gz", "sample1_R2.fastq.gz"]
    checksums: {md5: "abc123..."}
  steps:
    - name: "Quality trimming"
      tool: "fastp 0.23.4"
      input: ["sample1_R1.fastq.gz"]
      output: ["sample1_R1_trimmed.fastq.gz"]
      params: {quality: 20, length: 36}
      timestamp: "2026-02-24T10:00:00Z"
    - name: "Alignment"
      tool: "STAR 2.7.11a"
      input: ["sample1_R1_trimmed.fastq.gz"]
      output: ["sample1_Aligned.bam"]
      params: {genome: "GRCh38", sjdbOverhang: 100}
      timestamp: "2026-02-24T11:00:00Z"
```

## Completeness Check
- Every output file must have a recorded input
- No gaps between raw data and final results
- All tools and versions documented
- All parameters (including defaults) recorded
