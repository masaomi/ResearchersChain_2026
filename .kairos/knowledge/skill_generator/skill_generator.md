---
name: skill_generator
description: "Meta-skill v2.0: generate and evaluate research skills from multiple sources. Core engine of AFD evolution."
tags: [meta-skill, evolution, skill-generation, quality-rubric, multi-source]
version: "2.0"
domain: general
---
# Skill Generator v2.0

Meta-skill for generating and evaluating research skills from diverse sources.
Core engine of Agent-First Driven Development (AFD) evolution.

**v2.0 change**: Source-agnostic architecture. Skills can emerge from any knowledge source,
not just conversation patterns. Quality gate (evaluate) is unified across all sources.

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
| machine_learning | Model selection, validation, interpretation |
| data_engineering | Data preprocessing, cleaning, EDA |
| visualization | Data visualization, accessibility |

## Domain Tags

| Tag | Description |
|-----|-------------|
| general | Cross-domain, applicable to any field |
| genomics | Genomics, bioinformatics specific |
| ml | Machine learning specific |

## Priority Rules

- **P0**: Directly improves reproducibility/statistical validity/ethical safety → deploy first
- **P1**: Improves research speed or expands capability
- **P2**: Labor-saving (only if no quality degradation)

## Tool 1: draft_research_skill

### Required Inputs
- **topic** (string): Skill topic
- **category** (string): Taxonomy tag from the table above
- **domain** (string): Domain tag — general | genomics | ml
- **justification** (string): Which evolution criterion this satisfies and why

### Source Tracking (v2.0 new)
- **source.type**: conversation | deep_research | persona_assembly | literature | pipeline | meeting_place
- **source.reference**: URL, session ID, DOI, pipeline run ID, etc.
- **source.evidence_level**: anecdotal | systematic | consensus | empirical

### Evidence Levels

| Level | Description | Example Source |
|-------|-------------|---------------|
| anecdotal | Single observation, not systematically verified | One-time conversation pattern |
| systematic | Structured search or survey | Deep Research, literature review |
| consensus | Agreement from multiple perspectives | Persona Assembly discussion |
| empirical | Validated through actual execution/experimentation | Pipeline results, benchmarks |

### Output
```yaml
proposed_skill: <topic>
category: <category>
domain: <domain>
source: {type: <type>, reference: <ref>, evidence_level: <level>}
justification: <justification>
status: drafted
next_step: "Evaluate via evaluate_skill_proposal, then save to L2 via context_save"
```

## Tool 2: evaluate_skill_proposal

### Required Inputs
- **skill_draft** (string): The drafted skill definition to evaluate
- **existing_skills** (string, optional): List of existing skills for duplication check

### Quality Rubric (100 points)

| Axis | Points | Description |
|------|--------|-------------|
| Reproducibility | 25 | Are skill usage results reproducible? |
| Statistical validity | 20 | Does it promote correct statistical reasoning? |
| Research ethics safety | 20 | No ethical violations or privacy risks? |
| Utility | 20 | Contributes to speed improvement or cognitive load reduction? |
| Non-duplication | 15 | Not duplicating existing skills? |

### Rubric Adjustment by Evidence Level
- **empirical/consensus**: Higher initial trust → standard bar for L1 promotion
- **anecdotal**: Requires longer L2 validation period before promotion
- **systematic**: Standard evaluation

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
Knowledge source recognized (conversation, research, assembly, literature, pipeline)
  → draft_research_skill(topic, category, domain, justification, source)
  → evaluate_skill_proposal(skill_draft, existing_skills)
  → context_save() to L2 (Small Batch: 3-5 items)
  → 1-2 weeks of usage validation
  → skills_promote(analyze) with Persona Assembly
  → skills_promote(promote) L2→L1 (rubric score >= 60)
```
