---
name: draft_test_selection_advisor
description: Advise appropriate statistical test based on data distribution and study design
category: statistics
priority: P0
evolution_criterion: Improves rigor — prevents misuse of parametric tests on non-normal data
---
# Test Selection Advisor (Draft)
## Workflow
1. Assess data distribution (normality, homoscedasticity)
2. Identify study design (paired/unpaired, groups, repeated measures)
3. Recommend appropriate test (t-test, ANOVA, Wilcoxon, Kruskal-Wallis, etc.)
4. Suggest multiple testing correction if applicable (FDR, Bonferroni)
5. Output: test recommendation with assumptions checklist
