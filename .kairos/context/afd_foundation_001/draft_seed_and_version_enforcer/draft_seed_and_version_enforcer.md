---
name: draft_seed_and_version_enforcer
description: Enforce recording of random seeds and software versions in all analyses
category: reproducibility
priority: P0
evolution_criterion: Improves reproducibility — missing seeds and versions are the #1 cause of irreproducible results
---
# Seed and Version Enforcer (Draft)
## Rules
1. Every script/notebook MUST set and record a random seed at the top
2. Every analysis MUST record software versions used (R sessionInfo, Python sys.version, tool --version)
3. Every pipeline MUST pin dependency versions (renv.lock, requirements.txt, conda env export)
4. Warn if any stochastic operation lacks a fixed seed
5. Output: compliance checklist with pass/fail per item
