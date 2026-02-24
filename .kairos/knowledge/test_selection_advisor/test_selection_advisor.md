---
name: test_selection_advisor
description: Advise appropriate statistical test based on data distribution and study design
tags: [statistics, P0, testing, rigor]
promoted_from: L2/afd_foundation_001/draft_test_selection_advisor
evolution_criterion: Improves rigor — prevents misuse of parametric tests on non-normal data
---
# Test Selection Advisor

## Purpose
Recommend the appropriate statistical test based on data characteristics and study design.

## Workflow
1. Assess data distribution (normality via Shapiro-Wilk, homoscedasticity via Levene's)
2. Identify study design (paired/unpaired, number of groups, repeated measures)
3. Recommend appropriate test:
   - 2 groups, normal: t-test (paired/unpaired)
   - 2 groups, non-normal: Wilcoxon signed-rank / Mann-Whitney U
   - 3+ groups, normal: ANOVA (one-way/two-way/repeated measures)
   - 3+ groups, non-normal: Kruskal-Wallis
   - Categorical: Chi-squared / Fisher's exact
   - Correlation: Pearson (normal) / Spearman (non-normal)
4. Suggest multiple testing correction if applicable (FDR, Bonferroni)
5. Output: test recommendation with assumptions checklist

## Assumptions Checklist
- [ ] Independence of observations
- [ ] Normality (if parametric)
- [ ] Homogeneity of variance (if parametric)
- [ ] Sample size adequacy
- [ ] Appropriate measurement scale
