---
name: feature_importance_interpreter
description: Interpret and report feature importance from ML models responsibly
tags: [machine_learning, P1, interpretability, feature-importance, SHAP]
domain: ml
source: {type: systematic, evidence_level: systematic}
---
# Feature Importance Interpreter

## Purpose
Correctly interpret, report, and communicate feature importance from ML models.

## Methods Comparison

| Method | Model Type | Pros | Cons |
|--------|-----------|------|------|
| Coefficients | Linear models | Direct interpretation | Only for linear models |
| Gini/MDI importance | Tree-based | Fast, built-in | Biased toward high-cardinality features |
| Permutation importance | Any model | Model-agnostic, unbiased | Slow; correlated features problematic |
| SHAP values | Any model | Theoretically grounded, local + global | Computationally expensive |
| LIME | Any model | Local explanations | Unstable, approximation |
| Partial dependence plots | Any model | Shows effect direction/shape | Assumes feature independence |

## Reporting Guidelines
1. State which importance method was used and why
2. Report importance for top features with confidence/stability measures
3. Use SHAP summary plots for global view, SHAP force plots for individual predictions
4. Acknowledge limitations (correlation between features distorts importance)
5. Never claim causal relationships from feature importance alone

## Common Pitfalls
- Interpreting importance as causation
- Ignoring correlated features (importance is split/shared)
- Comparing importance across different models without normalization
- Reporting MDI importance from random forests without noting cardinality bias
- Drawing biological conclusions from a predictive model without validation

## Recommendation
Use **permutation importance** for a quick, unbiased overview.
Use **SHAP** for detailed, theoretically sound interpretation.
Always validate key features with domain knowledge.
