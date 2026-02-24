---
name: batch_effect_triager
description: Detect, assess, and correct batch effects in data analysis
tags: [analysis, P1, batch-effect, normalization, confounding]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Batch Effect Triager

## Purpose
Identify and handle batch effects that can confound analysis results.

## Detection Methods
1. **Visual**: PCA/MDS colored by batch — do samples cluster by batch?
2. **Statistical**: PVCA (Principal Variance Component Analysis)
3. **Correlation**: Check if batch correlates with variables of interest

## Critical Check: Batch-Condition Confounding
If batch is perfectly confounded with biological condition, **NO correction method can save this**.
Prevention: randomize samples across batches at experimental design stage.

## Correction Methods

| Method | When to Use | Caution |
|--------|------------|---------|
| ComBat (sva) | Known batch variable, moderate effects | Can over-correct if batch ≈ biology |
| limma::removeBatchEffect | Before visualization (PCA, heatmaps) | For visualization only, not for DE testing |
| Include batch as covariate | DE analysis (DESeq2/edgeR design formula) | Preferred for statistical testing |
| Harmony / MNN | Single-cell integration across batches | scRNA-seq specific |
| Quantile normalization | Cross-platform comparisons | Aggressive; can remove real signal |

## Decision Flowchart
```
Batch detected in PCA?
  → No: Proceed (document check)
  → Yes: Is batch confounded with condition?
    → Yes: STOP — redesign experiment or report limitation
    → No: Include batch in model (preferred) or apply correction
```

## Reporting
Always report: batch detection method, correction applied (if any), before/after PCA plots.
