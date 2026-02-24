---
name: ngs_pipelines
description: NGS analysis pipeline patterns and best practices
tags: [ngs, pipelines, analysis, bioinformatics]
---
# NGS Pipeline Patterns

## RNA-seq Standard Pipeline
1. Quality control (FastQC / MultiQC)
2. Adapter trimming (Trimmomatic / fastp)
3. Alignment (STAR / HISAT2)
4. Quantification (featureCounts / Salmon)
5. Differential expression (DESeq2 / edgeR)
6. Functional enrichment (clusterProfiler / GSEA)

## Best Practices
- Version-controlled pipeline definitions
- Record all software versions and parameters
- Containerized environments (Docker/Singularity)
- Biological replicates (n >= 3)
