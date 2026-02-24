---
name: multiple_testing_controller
description: Apply and justify multiple testing correction methods
tags: [statistics, P0, multiple-testing, FDR]
promoted_from: L2/afd_foundation_001/draft_multiple_testing_controller
evolution_criterion: Improves rigor — controls false discovery rate in high-dimensional genomics data
---
# Multiple Testing Controller

## Purpose
Prevent false discoveries in high-dimensional genomics analyses.

## Workflow
1. Count number of simultaneous tests
2. Assess dependency structure (independent vs correlated)
3. Recommend correction method
4. Apply correction and report adjusted p-values
5. Flag results that change significance after correction
6. Output: adjusted p-values, method justification, significance changes

## Method Selection Guide
| Method | Use When | Strictness |
|--------|----------|------------|
| Bonferroni | Few tests, need FWER control | Most strict |
| Holm | Few tests, slightly more power than Bonferroni | Strict |
| BH (FDR) | Many tests (genomics default), tolerate some false positives | Moderate |
| Storey q-value | Large-scale genomics, estimate proportion of true nulls | Moderate |
| Permutation-based | Complex dependency structures | Adaptive |

## Genomics Context
- RNA-seq DE: BH/FDR correction is standard (padj < 0.05)
- GWAS: Genome-wide significance threshold (p < 5e-8)
- Multiple enrichment tests: BH correction recommended
