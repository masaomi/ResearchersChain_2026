---
name: cross_validation_designer
description: Design appropriate cross-validation strategies to avoid data leakage
tags: [machine_learning, P1, cross-validation, evaluation, data-leakage]
domain: ml
source: {type: systematic, evidence_level: systematic}
---
# Cross-Validation Designer

## Purpose
Design validation strategies that provide honest performance estimates and prevent data leakage.

## CV Strategy Selection

| Strategy | When to Use | Caution |
|----------|------------|---------|
| k-fold (k=5 or 10) | Standard, i.i.d. data | Not for time series or grouped data |
| Stratified k-fold | Imbalanced classes | Default for classification |
| Leave-one-out (LOO) | Very small datasets | High variance, computationally expensive |
| Group k-fold | Samples from same subject/patient | Prevents same-subject leakage |
| Time series split | Temporal data | Must respect time ordering |
| Nested CV | Model selection + evaluation | Outer loop for evaluation, inner for tuning |
| Repeated CV | Reduce variance of estimate | k-fold repeated n times, average results |

## Data Leakage Prevention
- **Feature engineering**: Fit transformations (scaling, imputation) inside CV folds only
- **Feature selection**: Must be done within each fold, not on full dataset
- **Oversampling (SMOTE)**: Apply only to training fold, never test fold
- **Time**: Never train on future, test on past

## Nested CV for Honest Model Selection
```
Outer loop (k=5): Performance estimation
  └── Inner loop (k=5): Hyperparameter tuning
      └── Train on inner-train, validate on inner-val
  → Select best hyperparameters
  → Evaluate on outer-test
→ Report mean ± std across outer folds
```

## Reporting
- Report mean and standard deviation across folds
- Specify which CV strategy and why
- State what was inside vs outside the CV loop
