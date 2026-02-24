---
name: missing_data_strategy_advisor
description: Advise on strategies for handling missing data
tags: [statistics, P1, missing-data, imputation]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Missing Data Strategy Advisor

## Purpose
Guide appropriate handling of missing data based on missingness mechanism and analysis goals.

## Step 1: Identify Missingness Mechanism

| Mechanism | Definition | Example |
|-----------|-----------|---------|
| MCAR | Missing completely at random | Lab sample randomly dropped |
| MAR | Missing at random (conditional on observed) | Older patients more likely to miss follow-up |
| MNAR | Missing not at random | Sickest patients drop out |

## Step 2: Choose Strategy

| Strategy | When to Use | Caution |
|----------|------------|---------|
| Complete case analysis | MCAR, small proportion missing (<5%) | Loses power, biased if not MCAR |
| Mean/median imputation | Quick exploration only | Underestimates variance, never for final analysis |
| Multiple imputation (MI) | MAR, moderate missingness | Gold standard for many analyses |
| Maximum likelihood (ML) | MAR, structural equation models | Efficient, no imputed datasets needed |
| Inverse probability weighting | MAR, causal inference | Sensitive to weight model specification |
| Sensitivity analysis | Always, especially suspected MNAR | Essential to assess robustness |

## Reporting Requirements
- Report proportion and pattern of missing data
- State assumed missingness mechanism with justification
- Describe imputation method and number of imputations
- Compare results with and without imputation (sensitivity)
