---
name: falsifiability_checker
description: Check whether hypotheses are testable and falsifiable
tags: [philosophy, P1, falsifiability, hypothesis, scientific-method]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Falsifiability Checker

## Purpose
Ensure hypotheses are formulated in a way that allows them to be disproven by evidence.

## Falsifiability Test
A hypothesis is falsifiable if you can specify an observation that would prove it wrong.

| Hypothesis | Falsifiable? | Why |
|-----------|-------------|-----|
| "Drug X reduces tumor size" | Yes | Measurable outcome, clear comparison possible |
| "This gene is important" | No | "Important" is undefined; no clear test |
| "The model will perform well" | No | "Well" is undefined; specify metric and threshold |
| "Random forest achieves AUROC > 0.8 on held-out data" | Yes | Specific, measurable, testable |

## Checklist
- [ ] Is there a clear null hypothesis (H0)?
- [ ] What specific result would reject H0?
- [ ] Is the outcome measurable with available methods?
- [ ] Is the sample size sufficient to detect the expected effect?
- [ ] Are success criteria defined BEFORE data analysis? (pre-registration)

## Common Non-Falsifiable Patterns
- Post-hoc "hypothesis" generated after seeing data (HARKing)
- Vague predictions: "may be associated with", "could play a role"
- Moving goalposts: redefining success criteria after analysis
- Unfalsifiable framework claims disguised as testable hypotheses

## Strengthening Weak Hypotheses
Vague → Specific:
- "Gene X is involved in disease Y" → "Knockout of gene X in mouse model reduces disease Y phenotype by >50% compared to wild-type (p<0.05)"
