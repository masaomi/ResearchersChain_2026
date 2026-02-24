---
name: draft_effect_size_interpreter
description: Interpret and report effect sizes alongside p-values
category: statistics
priority: P0
evolution_criterion: Improves rigor — p-values alone are insufficient; effect sizes convey practical significance
---
# Effect Size Interpreter (Draft)
## Workflow
1. Identify test type and compute appropriate effect size (Cohen's d, eta-squared, odds ratio, log2FC, etc.)
2. Provide conventional benchmarks (small/medium/large)
3. Compute confidence intervals for effect size
4. Contextualize: is the effect biologically/clinically meaningful?
5. Output: effect size with CI, benchmark comparison, and interpretation note
