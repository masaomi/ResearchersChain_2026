---
name: draft_analysis_environment_recorder
description: Record complete analysis environment for reproducibility
category: reproducibility
priority: P0
evolution_criterion: Improves reproducibility — ensures environment can be recreated
---
# Analysis Environment Recorder (Draft)
## Captures
1. OS version, hardware specs
2. Software versions (R, Python, tools)
3. Package versions (sessionInfo/pip freeze)
4. Random seeds used
5. Data versions and checksums
6. Pipeline parameters
7. Output: structured environment manifest (YAML/JSON)
