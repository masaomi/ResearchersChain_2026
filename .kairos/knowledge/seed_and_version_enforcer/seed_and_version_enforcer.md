---
name: seed_and_version_enforcer
description: Enforce recording of random seeds and software versions in all analyses
tags: [reproducibility, P0, seeds, versions, enforcement]
promoted_from: L2/afd_foundation_001/draft_seed_and_version_enforcer
evolution_criterion: Improves reproducibility — missing seeds and versions are the #1 cause of irreproducible results
---
# Seed and Version Enforcer

## Purpose
Ensure every analysis records random seeds and software versions.

## Rules (Mandatory)
1. Every script/notebook MUST set and record a random seed at the top
2. Every analysis MUST record software versions used
3. Every pipeline MUST pin dependency versions
4. Warn if any stochastic operation lacks a fixed seed

## Implementation Examples

### R
```r
set.seed(42)
sessionInfo()  # Record at end of script
renv::snapshot()  # Pin package versions
```

### Python
```python
import random, numpy as np, torch
SEED = 42
random.seed(SEED)
np.random.seed(SEED)
torch.manual_seed(SEED)
# pip freeze > requirements.txt
```

### Pipeline (Nextflow/Snakemake)
```
# Pin all tool versions in container/conda env
# Record params in config file
# Log all versions at pipeline start
```

## Compliance Checklist
- [ ] Random seed set and recorded
- [ ] Language runtime version recorded
- [ ] Package/library versions pinned
- [ ] Tool versions recorded
- [ ] No uncontrolled stochastic operations
