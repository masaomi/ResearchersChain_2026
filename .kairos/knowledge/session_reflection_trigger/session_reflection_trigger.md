---
name: session_reflection_trigger
description: "End-of-session reflection: extract reusable patterns and propose L1 knowledge registration"
version: 1.0
layer: L1
tags: [meta-skill, reflection, knowledge-extraction, session-end, P1]
category: assistance
domain: general
priority: P1
source:
  type: conversation
  reference: "ResearchersChain session 2026-02-25 — first research session revealed zero L1 registration triggers"
  evidence_level: empirical
---

# Session Reflection Trigger

When a research session ends (or at a natural breakpoint), review the session
for reusable patterns worth preserving as L1 knowledge.

## When to Trigger

- User signals session end ("done", "let's wrap up", task completion)
- A major deliverable is completed (report, analysis, submission)
- User explicitly requests reflection

## Reflection Procedure

### Step 1: Pattern Scan

Review the session and identify candidates in these categories:

| Category | What to look for | Example |
|----------|-----------------|---------|
| Error patterns | Recurring mistakes, LLM hallucinations, common pitfalls | Species name fabrication in scientific text |
| Methodology | Novel analysis approaches, workflow sequences | Nonlinearity detection via prediction comparison |
| Workflow | Effective task ordering, review procedures | Critical bug → Methodology → Figures → Text |
| Domain knowledge | Field-specific insights confirmed by data | Gene expression normalization edge cases |
| Tool usage | Effective tool combinations, parameter choices | Pipeline parameter sets that worked well |

### Step 2: Evolution Criteria Check

For each candidate, verify at least one criterion is met:

1. Improves reproducibility
2. Accelerates discovery
3. Reduces cognitive load without sacrificing rigor
4. Upholds research ethics

**Discard** candidates that fail all four criteria.

### Step 3: Propose to User

Present candidates as a brief list:

```
## Session Reflection — L1 Knowledge Candidates

1. **[category] Topic name**
   - Pattern: (what was observed)
   - Criterion: (which evolution criterion it satisfies)
   - Reuse value: (when this would help in future sessions)

Register these as L1 knowledge? (all / select / skip)
```

### Step 4: Registration (if approved)

For approved candidates:
1. Use `skill_generator` draft_research_skill format
2. Save to L2 via `context_save` first
3. If evidence_level is empirical (validated in this session), propose direct L1 via `knowledge_update`
4. Record source as `{type: conversation, reference: session_id, evidence_level: empirical}`

## Important Constraints

- **Never auto-register** — always propose and wait for user approval
- **Quality over quantity** — 1-3 high-value patterns per session is ideal
- **No duplicates** — check existing L1 skills via `knowledge_list` before proposing
- **Session focus first** — this reflection happens AFTER the research task is complete, never during
