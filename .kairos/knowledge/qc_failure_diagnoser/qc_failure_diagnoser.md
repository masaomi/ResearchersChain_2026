---
name: qc_failure_diagnoser
description: Diagnose causes of quality control failures in data analysis
tags: [analysis, P1, qc, troubleshooting, diagnostics]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# QC Failure Diagnoser

## Purpose
Systematically diagnose and resolve quality control failures.

## Common QC Failures and Diagnoses

### Sequencing Data (NGS)
| Symptom | Likely Cause | Action |
|---------|-------------|--------|
| Low quality scores at read ends | Normal degradation | Trim with fastp/Trimmomatic |
| Adapter contamination | Short inserts or over-sequencing | Adapter trimming |
| GC bias | Library prep issue or contamination | Check for contamination, adjust normalization |
| High duplication rate | Low library complexity or over-amplification | Mark/remove duplicates, consider re-sequencing |
| Low mapping rate | Wrong reference, contamination, poor quality | Verify organism, check for contamination |

### General Data
| Symptom | Likely Cause | Action |
|---------|-------------|--------|
| Unexpected distribution shape | Data entry errors, outliers, mixed populations | Inspect raw data, check for subgroups |
| High missingness in specific variables | Systematic collection issue | Investigate cause, apply appropriate imputation |
| Impossible values | Unit errors, coding errors | Validate against expected ranges |
| Batch effects in PCA | Technical variation between runs | Batch correction (ComBat, limma::removeBatchEffect) |

## QC Report Template
1. Summary statistics (before/after filtering)
2. Flagged samples with reasons
3. Decision: include / exclude / re-process
4. Impact on downstream analysis
