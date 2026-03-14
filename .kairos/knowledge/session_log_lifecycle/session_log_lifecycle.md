---
description: "Manage L2 session logs: save at breakpoints, digest at session end, and leverage accumulated logs for project continuity"
tags:
  - meta-skill
  - session-management
  - L2-lifecycle
  - continuity
  - P1
version: "1.1"
---

# Session Log Lifecycle

L2 context serves as **project working memory** — not just disposable scratch space.
This skill defines when and how to save session logs, how to create session digests,
and how to leverage accumulated L2 logs for cross-session continuity.

## Motivation

Context windows are finite. Valuable work products — analysis results, decisions,
intermediate findings — are lost when a session ends without saving. L2 provides
a low-cost, no-approval-needed place to preserve this work. But without structure,
L2 becomes an unorganized dump. This skill introduces a lightweight lifecycle.

## Project Identifier Convention

Since a single KairosChain instance may serve multiple projects, **all L2 log names
must include a project identifier prefix** to enable filtering without reading content.

### Format

```
{project_id}_{topic}_{log_type}
```

- **project_id**: Short, stable identifier for the project (e.g., `ni_paper`, `kairoschain`, `genomicschain`)
- **topic**: What the log is about
- **log_type**: One of `results`, `decision`, `plan`, `review`, `diagnostic`, `checkpoint`, `snapshot`, `digest`

### Examples

```
ni_paper_noise_normalization_results
ni_paper_session_digest
kairoschain_l2_lifecycle_decision
genomicschain_nft_pipeline_plan
```

### Choosing a project_id

- Use a short, memorable name (1-3 words, snake_case)
- Keep it consistent within a project — do NOT alternate between `ni` and `ni_paper`
- If unsure, ask the user at session start: "Which project are we working on?"
- Once established, reuse the same project_id for all logs in that project

## When to Save to L2 (Breakpoint Triggers)

Save a log to L2 via `context_save` when any of these occur **during** a session:

| Trigger | What to Save | Name Example (`ni_paper` project) |
|---------|-------------|-----------------------------------|
| **Analysis complete** | Results, parameters, interpretation | `ni_paper_degs_analysis_results` |
| **Decision made** | Options considered, rationale, chosen approach | `ni_paper_normalization_method_decision` |
| **Plan formulated** | Steps, dependencies, acceptance criteria | `ni_paper_revision_plan` |
| **Review/critique done** | Findings, severity, recommendations | `ni_paper_methods_section_review` |
| **Error diagnosed** | Root cause, attempted fixes, resolution | `ni_paper_batch_effect_diagnostic` |
| **Context window ~50% used** | Current state summary, what remains to do | `ni_paper_progress_checkpoint` |
| **Before risky operation** | Pre-state snapshot, rollback plan | `ni_paper_pre_reanalysis_snapshot` |

### Log Template

```markdown
---
description: "{Brief description of what this log contains}"
tags:
  - {project_id}
  - {topic}
  - {log-type: results|decision|plan|review|diagnostic|checkpoint}
version: "1.0"
---

# {Title}

## Context
- Project: {project_id}
- Task: {what was being done}
- Date: {YYYY-MM-DD}
- Prior session: {session_id if continuing previous work, or "new"}

## Content
{The actual results, decision, plan, review, etc.}

## Open Questions
{Unresolved issues, if any}

## Next Steps
{What should happen next — critical for session continuity}
```

### Proactive Prompting

At natural breakpoints, proactively suggest saving:

> "This analysis produced significant results. Save to L2 before continuing?
> Suggested: `context_save` as `ni_paper_degs_analysis_results`"

Do NOT wait for the user to ask — **offer** the save. The user can decline.

## Session Digest (End of Session)

When a session ends, create a **digest** that summarizes the entire session.
This is separate from `session_reflection_trigger` (which extracts L1 candidates).

### Digest Naming

```
{project_id}_session_digest
```

If multiple projects were worked on in a single session, create one digest per project.

### Digest Template

```markdown
---
description: "Session digest: {one-line summary}"
tags:
  - digest
  - {project_id}
version: "1.0"
---

# Session Digest — {project_id} — {YYYY-MM-DD}

## Objectives
- {What was the goal of this session?}

## Accomplished
- {Key outcomes, with references to detailed logs if saved}

## Key Decisions
- {Important choices made and their rationale}

## Unresolved / Carry-forward
- {Issues, questions, or tasks for the next session}

## L2 Logs Created This Session
- `{project_id}_{log_name_1}`: {brief description}
- `{project_id}_{log_name_2}`: {brief description}
```

### Relationship to session_reflection_trigger

These two skills work together at session end:

```
Session End
  ├── session_log_lifecycle → Create session digest (L2)
  │     "What happened this session?"
  └── session_reflection_trigger → Propose L1 candidates
        "What patterns are reusable across sessions?"
```

Run `session_log_lifecycle` first (preserves facts), then `session_reflection_trigger`
(extracts patterns). The digest itself may serve as input for reflection.

## Session Start: Leveraging Past Logs

When starting a new session, check for relevant prior context:

### Step 1: Identify Project

Determine the project_id from user's request or ask:

> "Which project are we working on? (e.g., `ni_paper`, `kairoschain`)"

### Step 2: Scan Project Digests

```
resource_list(layer: "l2") → filter names matching {project_id}_*digest*
resource_read(uri) → read the most recent matching digest
```

Because the project_id is in the name, filtering is immediate — no need to
read each log's content to determine relevance.

### Step 3: Offer Continuity

If prior work is found, offer to resume:

> "Found digest for `ni_paper` from {date}: {summary}.
> Continue from where you left off, or start fresh?"

### Step 4: Load Relevant Context

If continuing, read the referenced L2 logs (same project_id prefix) to restore context.
This turns L2 into an **external memory** that extends across sessions.

## L2 Hygiene (Optional, User-Initiated)

L2 logs accumulate. This is acceptable — storage is cheap and logs have reference
value. However, if the user wants to clean up:

### Archive Candidates

Logs that are candidates for cleanup:
- Logs from sessions > 30 days old where the digest exists
- `{project_id}_progress_checkpoint` logs (superseded by digest)
- Draft logs that were later superseded by final versions

### Preservation Priority

Never auto-delete. When cleanup is requested, preserve in order:
1. **Session digests** (`*_session_digest`) — always keep
2. **Decision logs** (`*_decision`) — rationale has long-term value
3. **Final results** (`*_results`) — may be referenced later
4. **Plans and reviews** (`*_plan`, `*_review`) — lower priority if digest captures key points
5. **Checkpoints and diagnostics** (`*_checkpoint`, `*_diagnostic`) — safe to remove after digest

### Per-Project Cleanup

Use the project_id prefix to scope cleanup:

> "Clean up old `ni_paper` logs? This will preserve digests and decisions."

Never mix projects in a single cleanup operation.

## Integration with Existing Skills

| Skill | Relationship |
|-------|-------------|
| `session_reflection_trigger` | Complementary: this skill saves facts (L2), that skill extracts patterns (L1) |
| `layer_placement_guide` | This skill operates within L2; promotion to L1 follows that guide |
| `analysis_environment_recorder` | Environment info can be included in result logs |
| `provenance_chain_builder` | L2 logs contribute to provenance documentation |

## Key Principles

1. **Save early, save often** — Context windows are finite; L2 is not
2. **Prefix everything** — Project identifier in every log name, no exceptions
3. **Digest, don't just dump** — Raw logs plus structured digest
4. **Connect sessions** — Digests are the bridge between sessions
5. **Never auto-delete** — Only clean up when user requests
6. **Offer, don't force** — Proactively suggest saves, but respect user's workflow
