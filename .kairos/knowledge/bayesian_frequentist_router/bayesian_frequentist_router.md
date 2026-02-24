---
name: bayesian_frequentist_router
description: Guide selection between Bayesian and frequentist approaches
tags: [statistics, P1, bayesian, frequentist, decision]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Bayesian vs Frequentist Router

## Purpose
Help researchers choose the appropriate statistical paradigm for their analysis.

## Decision Guide

| Factor | Favor Frequentist | Favor Bayesian |
|--------|-------------------|----------------|
| Prior knowledge | Weak or controversial | Strong, well-established |
| Sample size | Large | Small (priors help) |
| Audience | Traditional journals | Methods-aware reviewers |
| Goal | Hypothesis testing (reject/fail to reject) | Parameter estimation, prediction |
| Sequential analysis | Fixed sample size | Naturally supports stopping rules |
| Multiple comparisons | Requires explicit correction | Naturally handled via hierarchical models |
| Interpretation needed | "Significant or not" | "Probability of hypothesis given data" |

## When Bayesian is Particularly Useful
- Small sample sizes with informative priors
- Complex hierarchical/multilevel models
- Sequential clinical trials
- Integration of prior studies (meta-analytic priors)
- Direct probability statements about parameters

## When Frequentist is Sufficient
- Large, well-powered studies
- Standard designs (RCT, case-control)
- Regulatory submissions requiring p-values
- Simple comparisons with clear null hypotheses

## Key Principle
The choice is not ideological — it is practical. Report the approach, justify it, and interpret correctly.
