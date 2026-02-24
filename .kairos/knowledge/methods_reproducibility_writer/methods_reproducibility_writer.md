---
name: methods_reproducibility_writer
description: Write Methods sections that enable full reproduction of the study
tags: [writing, P1, methods, reproducibility]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Methods Reproducibility Writer

## Purpose
Write Methods sections detailed enough for independent reproduction.

## Required Elements

### Computational Analysis
- Software names and exact versions
- Package/library versions
- All non-default parameters
- Random seeds
- Hardware specifications (if relevant to runtime)
- Code availability statement (GitHub + archived DOI via Zenodo)

### Experimental Design
- Sample size and justification (power analysis)
- Randomization procedure
- Blinding strategy
- Inclusion/exclusion criteria
- Controls (positive, negative, vehicle)

### Statistical Analysis
- Tests used and why
- Multiple testing correction method
- Significance threshold
- Software used for statistics
- Effect size measures reported

## Reproducibility Checklist
- [ ] Could another lab replicate this with only the Methods section?
- [ ] Are all software versions specified?
- [ ] Are all parameters (including defaults) documented?
- [ ] Is code available and archived?
- [ ] Is raw data accessible (or reason for restriction stated)?
