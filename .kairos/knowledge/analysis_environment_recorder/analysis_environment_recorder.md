---
name: analysis_environment_recorder
description: Record complete analysis environment for reproducibility
tags: [reproducibility, P0, environment, versioning]
promoted_from: L2/afd_foundation_001/draft_analysis_environment_recorder
evolution_criterion: Improves reproducibility — ensures environment can be recreated
---
# Analysis Environment Recorder

## Purpose
Capture a complete snapshot of the analysis environment for reproducibility.

## Captures
1. **OS**: Version, architecture, hardware specs
2. **Language runtimes**: R version, Python version, Java version
3. **Packages**: R sessionInfo(), pip freeze, conda list
4. **Tools**: Aligner version, samtools version, etc.
5. **Random seeds**: All seeds used in stochastic operations
6. **Data versions**: Input file checksums (MD5/SHA256), database versions
7. **Pipeline parameters**: All non-default parameters explicitly recorded

## Output Format
```yaml
environment:
  os: "Ubuntu 22.04 LTS (x86_64)"
  r_version: "4.3.1"
  python_version: "3.11.5"
  packages:
    DESeq2: "1.40.2"
    ggplot2: "3.4.4"
  tools:
    STAR: "2.7.11a"
    samtools: "1.18"
  seeds: [42, 123]
  data:
    input_fastq_md5: "abc123..."
    genome_build: "GRCh38.p14"
  timestamp: "2026-02-24T12:00:00Z"
```

## Best Practices
- Generate automatically at pipeline start
- Store alongside results
- Use containerization (Docker/Singularity) when possible
