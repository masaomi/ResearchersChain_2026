---
name: assumption_checklist_enforcer
description: Enforce verification of statistical test assumptions before analysis
tags: [statistics, P1, assumptions, validation]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Assumption Checklist Enforcer

## Purpose
Ensure all statistical test assumptions are explicitly checked and documented before interpreting results.

## Common Assumptions by Test

| Test | Assumptions to Check |
|------|---------------------|
| t-test | Normality, equal variance (if unpaired), independence |
| ANOVA | Normality, homoscedasticity, independence |
| Chi-squared | Expected count >= 5 per cell, independence |
| Pearson correlation | Linearity, bivariate normality, no outliers |
| Linear regression | Linearity, normality of residuals, homoscedasticity, independence, no multicollinearity |
| Wilcoxon/Mann-Whitney | Independence, similar distribution shape (for location shift interpretation) |

## Verification Methods
- **Normality**: Shapiro-Wilk test, Q-Q plot, histogram
- **Homoscedasticity**: Levene's test, residual plots
- **Independence**: Study design review, Durbin-Watson test
- **Multicollinearity**: VIF (Variance Inflation Factor)
- **Outliers**: Cook's distance, leverage plots

## When Assumptions Fail
1. Use non-parametric alternative
2. Apply data transformation (log, Box-Cox)
3. Use robust methods
4. Report violation and interpret cautiously
