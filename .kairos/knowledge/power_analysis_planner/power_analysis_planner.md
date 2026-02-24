---
name: power_analysis_planner
description: Plan sample size and power analysis for study design
tags: [statistics, P0, sample-size, power]
promoted_from: L2/afd_foundation_001/draft_power_analysis_planner
evolution_criterion: Improves rigor — ensures adequate statistical power before experiments
---
# Power Analysis Planner

## Purpose
Calculate minimum sample size and statistical power before experiments begin.

## Workflow
1. Define primary endpoint and expected effect size
2. Set significance level (alpha, typically 0.05) and desired power (1-beta, typically 0.80)
3. Consider study design (one/two-sided, paired/unpaired, multiple groups)
4. Calculate minimum sample size using appropriate method
5. Assess feasibility (budget, available samples, time)
6. Output: sample size recommendation with power curve and assumptions

## Tools
- R: `pwr` package, `samplesize` package
- Python: `statsmodels.stats.power`
- Standalone: G*Power

## Common Effect Sizes (Cohen's conventions)
| Size | d | r | f | w |
|------|-----|-----|-----|-----|
| Small | 0.2 | 0.1 | 0.1 | 0.1 |
| Medium | 0.5 | 0.3 | 0.25 | 0.3 |
| Large | 0.8 | 0.5 | 0.4 | 0.5 |
