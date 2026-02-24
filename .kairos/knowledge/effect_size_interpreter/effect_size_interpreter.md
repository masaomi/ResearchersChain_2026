---
name: effect_size_interpreter
description: Interpret and report effect sizes alongside p-values
tags: [statistics, P0, effect-size, reporting]
promoted_from: L2/afd_foundation_001/draft_effect_size_interpreter
evolution_criterion: Improves rigor — p-values alone are insufficient; effect sizes convey practical significance
---
# Effect Size Interpreter

## Purpose
Always report effect sizes with confidence intervals alongside p-values.

## Workflow
1. Identify test type and compute appropriate effect size
2. Provide conventional benchmarks (small/medium/large)
3. Compute confidence intervals for effect size
4. Contextualize: is the effect biologically/clinically meaningful?
5. Output: effect size with CI, benchmark comparison, interpretation

## Effect Size by Test Type
| Test | Effect Size | Formula |
|------|------------|---------|
| t-test | Cohen's d | (M1-M2)/SD_pooled |
| ANOVA | Eta-squared (η²) | SS_effect/SS_total |
| Correlation | r / R² | Direct |
| Chi-squared | Cramér's V | sqrt(χ²/(n*min(r-1,c-1))) |
| RNA-seq DE | log2 fold change | log2(condition/control) |
| Odds ratio | OR | (a*d)/(b*c) |

## Key Principle
Statistical significance ≠ practical significance. A large sample can make trivial effects significant.
