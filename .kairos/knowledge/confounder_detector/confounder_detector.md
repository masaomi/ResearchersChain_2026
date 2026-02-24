---
name: confounder_detector
description: Identify and address confounding variables in study design and analysis
tags: [analysis, P1, confounding, causal-inference, study-design]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Confounder Detector

## Purpose
Identify variables that may confound the relationship between exposure and outcome.

## What is a Confounder?
A variable that:
1. Is associated with the exposure
2. Is associated with the outcome
3. Is NOT on the causal pathway between exposure and outcome

## Detection Strategies

### At Design Stage
- List all known potential confounders from domain knowledge
- Use DAGs (Directed Acyclic Graphs) to map causal assumptions
- Design to eliminate: randomization, matching, restriction

### At Analysis Stage
- Compare distributions of covariates across groups
- Check if adjusting for a variable changes the effect estimate (>10% change rule)
- Stratified analysis to assess effect modification vs confounding

## Handling Methods

| Method | Stage | Notes |
|--------|-------|-------|
| Randomization | Design | Gold standard — balances known and unknown confounders |
| Matching | Design | Case-control studies; can reduce power |
| Restriction | Design | Limits generalizability |
| Stratification | Analysis | Limited by sample size per stratum |
| Multivariable regression | Analysis | Most common; requires correct model specification |
| Propensity score | Analysis | For observational causal inference |
| Instrumental variables | Analysis | When unmeasured confounding suspected |

## Common Confounders by Field
- **Genomics**: Ancestry/population structure, sex, age, batch
- **Clinical**: Age, sex, BMI, comorbidities, medications
- **ML**: Data collection site, time period, sensor calibration
