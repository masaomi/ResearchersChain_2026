---
name: draft_multiple_testing_controller
description: Apply and justify multiple testing correction methods
category: statistics
priority: P0
evolution_criterion: Improves rigor — controls false discovery rate in high-dimensional genomics data
---
# Multiple Testing Controller (Draft)
## Workflow
1. Count number of simultaneous tests being performed
2. Assess dependency structure among tests (independent vs correlated)
3. Recommend correction method (Bonferroni, Holm, BH/FDR, Storey q-value)
4. Apply correction and report adjusted p-values
5. Flag results that change significance after correction
6. Output: adjusted p-values, method justification, significance changes
