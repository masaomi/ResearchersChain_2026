---
name: ngs_pipeline_designer
description: Design NGS analysis pipelines tailored to experimental goals
tags: [analysis, P1, ngs, pipeline, bioinformatics]
domain: genomics
source: {type: systematic, evidence_level: systematic}
---
# NGS Pipeline Designer

## Purpose
Design appropriate NGS analysis pipelines based on data type, organism, and research question.

## Pipeline Selection by Data Type

| Data Type | Standard Pipeline | Key Tools |
|-----------|------------------|-----------|
| RNA-seq (bulk) | QC → Trim → Align → Quantify → DE → Enrichment | FastQC, fastp, STAR, featureCounts, DESeq2 |
| RNA-seq (single-cell) | QC → Demux → Align → Count → Cluster → Annotation | CellRanger/STARsolo, Seurat/Scanpy |
| ChIP-seq | QC → Trim → Align → Peak call → Annotation → Motif | BWA/Bowtie2, MACS2, HOMER |
| ATAC-seq | QC → Trim → Align → Peak call → Footprinting | BWA, MACS2, HINT-ATAC |
| WGS/WES | QC → Trim → Align → Mark duplicates → Call variants → Annotate | BWA-MEM2, GATK, VEP/ANNOVAR |
| Metagenomics | QC → Host removal → Classify → Assemble → Annotate | Kraken2, MetaSPAdes, Prokka |

## Design Principles
- Start with established community pipelines (nf-core, Snakemake workflows)
- Pin all tool versions
- Use containerized environments (Docker/Singularity)
- Include QC checkpoints between major steps
- Log all parameters and intermediate file checksums

## Decision Points
- Reference genome version (always document which build)
- Aligner choice depends on data type and speed requirements
- Quantification: alignment-based vs pseudo-alignment (Salmon/Kallisto)
- DE analysis: DESeq2 vs edgeR vs limma-voom (all valid, be consistent)
