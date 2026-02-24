---
name: skill_generator
description: "Meta-skill v1.0: generate and evaluate researcher-specific skills from conversation. Core engine of AFD evolution."
tags: [meta-skill, evolution, skill-generation, quality-rubric]
version: "1.0"
---
# Skill Generator v1.0

Meta-skill for generating and evaluating researcher-specific skills.
This is the core engine of AFD (Agent-First Driven Development) evolution.

**Bottleneck awareness** (Gemini insight): skill_generator's quality determines
the quality of the entire system's evolution. Start lightweight, strengthen with experience.

## Evolution Criteria

New skills MUST satisfy at least one:
1. Improves reproducibility
2. Accelerates discovery
3. Reduces cognitive load without sacrificing rigor
4. Upholds research ethics

## Skill Taxonomy Tags

| Tag | Description |
|-----|-------------|
| writing | Paper authoring, submission, rebuttal |
| planning | Research planning, grant applications |
| analysis | Data analysis, bioinformatics |
| statistics | Statistical methods, testing, modeling |
| review | Paper review, peer review |
| ethics | Research ethics, compliance |
| philosophy | Scientific philosophy, reasoning rigor |
| assistance | Literature management, protocols, lab notes |
| reproducibility | Reproducibility, environment recording, automation |

## Priority Rules

- **P0**: Skills that directly improve reproducibility/statistical validity/ethical safety → deploy first
- **P1**: Skills that improve research speed
- **P2**: Labor-saving (only if no quality degradation)

## Tool 1: draft_research_skill

### Purpose
Draft a new research skill based on conversation analysis.

### Required Inputs
- **topic** (string): Skill topic (e.g., research_planning, peer_review)
- **category** (string): Taxonomy tag from the table above
- **justification** (string): Which evolution criterion this satisfies and why

### Output
```yaml
proposed_skill: <topic>
category: <category>
justification: <justification>
status: drafted
next_step: "Evaluate via evaluate_skill_proposal, then save to L2 via context_save"
```

## Tool 2: evaluate_skill_proposal

### Purpose
Self-evaluate a drafted skill against evolution criteria and quality rubric.

### Required Inputs
- **skill_draft** (string): The drafted skill definition to evaluate
- **existing_skills** (string, optional): List of existing skills for duplication check

### Quality Rubric (Codex proposal, 100 points)

| Axis | Points | Description |
|------|--------|-------------|
| Reproducibility | 25 | Are skill usage results reproducible? |
| Statistical validity | 20 | Does it promote correct statistical reasoning? |
| Research ethics safety | 20 | No ethical violations or privacy risks? |
| Utility | 20 | Contributes to speed improvement or cognitive load reduction? |
| Non-duplication | 15 | Not duplicating existing skills? |

### Judgment Criteria
- **80+ points**: L1 candidate → proceed to skills_promote
- **60-79 points**: Keep in L2, continue validation
- **Below 60**: Reject
- **Critical ethics/safety violation**: Reject regardless of score

### Output
```yaml
validation_result: Passed|Failed
score: <0-100>
breakdown: {reproducibility: X, statistics: X, ethics: X, utility: X, non_duplication: X}
recommendation: L1_candidate|L2_keep|reject
next_step: "Submit via skills_promote for Persona Assembly review"
```

## Workflow

```
Conversation pattern recognized
  → draft_research_skill(topic, category, justification)
  → evaluate_skill_proposal(skill_draft, existing_skills)
  → context_save() to L2 (Small Batch: 3-5 items)
  → 1-2 weeks of usage validation
  → skills_promote(analyze) with Persona Assembly
  → skills_promote(promote) L2→L1 (rubric score >= 60)
```

## Future Evolution (v2.0)

After accumulating 10+ skills:
- Add inputs: risk_level, required_evidence, examples
- Add output: test_plan (minimum 3 cases), duplication_report
- Add quality gates: duplication check, danger check, evidence check (automated)
- Quantitative rubric scoring (100-point scale, automated)

## Future Evolution (v3.0)

- Persona Assembly integration (evaluate_skill_proposal auto-invokes assembly)
- Operational KPI tracking: proposal_acceptance_rate, rollback_rate
- Self-improvement: meta-skill rubric weight re-calibration
