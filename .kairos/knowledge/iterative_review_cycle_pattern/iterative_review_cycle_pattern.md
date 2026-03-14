---
title: Iterative Review Cycle Pattern for Complex Research and Development
description: >
  A universal workflow pattern for complex research and development tasks using
  a diverge-converge-diverge structure: multi-perspective planning, single-agent
  implementation, and multi-perspective review — repeated iteratively for complex tasks.
tags:
  - workflow
  - quality-assurance
  - review
  - agent-team
  - persona-assembly
  - research-methodology
  - error-cascade
priority: P1
version: "1.0"
created: "2026-02-25"
---

# Iterative Review Cycle Pattern

## Core Principle

Iterative multi-perspective review is a **universal principle** that applies regardless
of whether the executor is human or AI. For complex tasks (especially research), errors
cascade through reasoning chains and compound at each step — no single pass can reliably
catch all of them.

### Mathematical Basis

```
Total accuracy = p^n  (where p = per-step accuracy, n = number of steps)

p = 0.99, n = 10  →  0.90   (still acceptable)
p = 0.95, n = 50  →  0.08   (unreliable)
```

Research tasks have large `n` and structurally lower `p` at each layer
(hypothesis → implementation → analysis → interpretation).

---

## The Diamond Cycle

```
[PLAN]      Diverge  →  Multi-LLM / Multi-Persona
                ↓
[IMPLEMENT] Converge →  Single LLM / Single Thread
                ↓
[REVIEW]    Diverge  →  Multi-LLM / Multi-Persona
                ↓
         (repeat for complex tasks)
```

### Why Multi for Plan and Review

Different models and personas have **complementary failure modes**. Multi-perspective
review catches errors that a single agent would systematically miss due to training
biases or hallucination patterns.

| Human error            | LLM equivalent                          |
|------------------------|-----------------------------------------|
| Confirmation bias      | Training data distribution bias         |
| Fatigue / oversight    | Hallucination (confident wrong answers) |
| Domain blind spots     | Local optimum in token prediction       |
| Communication drift    | Prompt interpretation variance          |

### Why Single for Implementation

Parallel agents during implementation introduce:

- **Context fragmentation** → inconsistent variable names, design decisions
- **Conflicting outputs** → judgment cost to reconcile which is correct
- **Diffuse accountability** → error tracing becomes difficult

Use a high-capability single model (e.g., Opus) for implementation to maximize
coherence and context retention over long tasks.

---

## Tool Priority for Multi-Perspective Phases

When multiple perspectives are needed (Plan / Review), use in this order:

1. **Multiple LLMs** (different providers/models) — maximum diversity of failure modes
2. **Claude Code agent team (cowork)** — parallel specialized agents within one session
3. **Persona Assembly (researchers-chain)** — available in any KairosChain session
   as fallback when options 1 and 2 are unavailable

### Using Persona Assembly as Fallback

```
mcp__researchers-chain__skills_promote(
  command: "analyze",
  personas: ["kairos", "skeptic", "conservative", "pragmatic"],
  assembly_mode: "discussion"
)
```

Persona Assembly simulates multi-perspective review within a single LLM session
by invoking structured viewpoints (skeptic, conservative, pragmatic, etc.).

---

## Applicability by Task Complexity

| Task duration / complexity | Recommended cycles |
|----------------------------|--------------------|
| Simple (< 1 hour)          | 1 cycle sufficient |
| Moderate (hours)           | 2–3 cycles         |
| Complex (days+)            | 3+ cycles, escalate rigor per cycle |

### Research-Specific Risk: Error Cascade

In scientific research, downstream impact of errors is non-linear:

- Code bug → wrong numbers → statistical conclusion reverses
- Config error → sample contamination → entire interpretation invalid
- Oversight → uncontrolled confounder → false causal attribution

This makes multi-cycle review not just helpful but a **quality control protocol**,
analogous to peer review and reproducibility checks in science.

---

## AI Era Insight

AI agents do **not** eliminate the need for iterative review — they change the **cost**:

- Before AI: each review cycle consumed human time and attention
- With AI: iteration cost drops dramatically → more cycles become practically feasible

The principle is unchanged; the barrier to applying it is lowered.
The right response is to run **more** cycles, not fewer.

---

## Related Skills

- `session_reflection_trigger` — when to reflect and evolve knowledge
- `llm_hallucination_patterns_scientific_writing` — specific LLM failure modes
- `mcp_to_saas_development_workflow` — broader development workflow context
- `persona_definitions` — available personas for Persona Assembly
