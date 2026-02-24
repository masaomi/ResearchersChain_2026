---
name: assumption_surface_mapper
description: Surface and document implicit assumptions in research design and analysis
tags: [philosophy, P1, assumptions, transparency, critical-thinking]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Assumption Surface Mapper

## Purpose
Make implicit assumptions explicit so they can be examined, tested, and communicated.

## Assumption Categories

| Category | Examples |
|----------|---------|
| **Statistical** | Data is normally distributed; observations are independent; missing data is MAR |
| **Biological** | Gene expression reflects protein activity; cell lines represent in vivo biology |
| **Methodological** | Reference genome is correct; antibody is specific; model is correctly specified |
| **Causal** | No unmeasured confounders; treatment precedes outcome; no reverse causation |
| **Computational** | Algorithm converges; hyperparameters are adequate; training data is representative |

## Surfacing Process
1. For each major conclusion, ask: "What must be true for this to hold?"
2. List each assumption explicitly
3. Classify: testable vs untestable, strong vs weak
4. For testable assumptions: how would you check?
5. For untestable: acknowledge as limitation

## Documentation Template
```
Assumption: [State the assumption]
Type: [Statistical / Biological / Methodological / Causal / Computational]
Testable: [Yes/No]
If violated: [What happens to conclusions]
Mitigation: [How addressed or acknowledged]
```

## Key Principle
Every analysis rests on assumptions. The quality of science is not determined by having no assumptions, but by knowing and stating what they are.
