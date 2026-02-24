---
name: skill_generator_v2_design_notes
description: Design notes for skill_generator v2.0 — multi-source skill generation architecture
category: meta-skill
priority: P1
evolution_criterion: Accelerates discovery — enables knowledge crystallization from diverse research activities
---
# Skill Generator v2.0 Design Notes

## Motivation

skill_generator v1.0 is limited to "extracting patterns from conversation."
In practice, valuable research skills can emerge from many sources:

1. **Conversation patterns** — recurring workflows recognized during research dialogue
2. **Web Search / Deep Research** — structured knowledge from literature surveys
3. **Persona Assembly discussions** — consensus knowledge from multi-perspective deliberation
4. **Literature review** — methodological best practices extracted from papers
5. **Pipeline execution results** — empirically validated best practices
6. **Meeting Place (cross-Chain)** — externalized knowledge from other KairosChain instances

## Architecture Principle

The skill generation workflow should be **source-agnostic**:

```
Input (diverse sources)
  ↓
[Structuring] Source-specific knowledge extraction
  ↓
[Draft] Unified format skill proposal (source-independent)
  ↓
[Evaluate] Quality rubric (same criteria regardless of source)
  ↓
[Output] L2 save → validation → L1 promotion
```

Key insight: the **quality gate (evaluate) is unified** across all sources.
This guarantees fairness and quality assurance regardless of origin.

## Proposed Changes to draft_research_skill

### New input parameter: source

```yaml
source:
  type: conversation | deep_research | persona_assembly | literature | pipeline | meeting_place
  reference: "URL, session ID, DOI, pipeline run ID, etc."
  evidence_level: anecdotal | systematic | consensus | empirical
```

### Evidence Levels

| Level | Description | Example Source |
|-------|-------------|---------------|
| anecdotal | Single observation, not systematically verified | One-time conversation pattern |
| systematic | Structured search or survey | Deep Research, literature review |
| consensus | Agreement from multiple perspectives | Persona Assembly discussion |
| empirical | Validated through actual execution/experimentation | Pipeline results, benchmarks |

### Rubric Weight Adjustment by Evidence Level

The evaluate step could adjust rubric weights based on evidence_level:
- **empirical/consensus**: Higher initial trust → lower bar for L1 promotion
- **anecdotal**: Requires longer L2 validation period before promotion
- **systematic**: Standard evaluation

## Relationship to v2.0 Plan (from development plan)

The original v2.0 plan (Section 4 of development plan) focuses on:
- Additional inputs: risk_level, required_evidence, examples
- Additional outputs: test_plan (min 3 cases), duplication_report
- Quality gates: duplication check, danger check, evidence check

The multi-source architecture proposed here is **complementary** to those changes.
Both can be integrated together when v2.0 is implemented.

## Prerequisites

- Accumulate 10+ skills through v1.0 usage (per development plan)
- Identify which source types actually produce useful skills in practice
- KairosChain bug fixes: SafeEvolver::DSL_PATH (#1), ContextManager#get (#3)

## Decision Record

- **2026-02-24**: Idea proposed during AFD Phase 2-7 review discussion
- **Status**: Recorded as L2 context for future reference
- **Next action**: Revisit after 10+ skills accumulated through v1.0 workflow
