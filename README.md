# ResearchersChain

An MCP server of AI research assistant for data science and genomics, built on [KairosChain](https://github.com/masaomi/KairosChain).

ResearchersChain is a specialized KairosChain instance that embeds scientific principles, research ethics, and domain knowledge directly into an AI agent's memory layers. It acts as an evolving knowledge companion for researchers — enforcing reproducibility, statistical rigor, and ethical compliance through structured, auditable skills.

## What Is ResearchersChain?

ResearchersChain is **not** a traditional software application. It is a **knowledge architecture** — a layered system of principles, skills, and domain knowledge that shapes how an AI agent assists with research.

When you connect to ResearchersChain via [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (or any MCP-compatible client), the agent automatically:

- Follows a **Researcher Constitution** — core scientific principles injected into every conversation
- Draws on **48 research skills** — statistics, ML, ethics, reproducibility, writing, and more
- Applies **quality guardrails** — statistical test selection, privacy risk checks, reproducibility enforcement
- Records all knowledge evolution on a **blockchain** — every change is traceable and auditable

### How It Differs from a Regular AI Chat

| Regular AI Chat | ResearchersChain |
|----------------|-----------------|
| Stateless — starts fresh each session | Persistent memory across sessions via L0/L1/L2 layers |
| Generic knowledge | 48 domain-specific skills across 12 categories |
| No guardrails | Built-in statistical, ethical, and reproducibility checks |
| No audit trail | Blockchain-recorded knowledge evolution (55+ blocks) |
| Manual prompting | Automatic constitution injection via MCP |

## Architecture

ResearchersChain uses KairosChain's three-layer memory architecture:

```
┌───────────────────────────────────────────────────────┐
│  L0: Constitution (Immutable Principles)              │
│  ┌───────────────────────────────────────────────┐    │
│  │ researcher.md — Scientific principles,        │    │
│  │ research ethics, quality guardrails           │    │
│  │ kairos.rb — 9 meta-skills governing           │    │
│  │ self-modification, safety, and skill evolution │    │
│  └───────────────────────────────────────────────┘    │
│                                                        │
│  L1: Knowledge (Stable, Reusable Skills)              │
│  ┌───────────────────────────────────────────────┐    │
│  │ 48 research skills across 12 categories:      │    │
│  │ statistics, ethics, reproducibility, writing,  │    │
│  │ planning, analysis, philosophy, ML,            │    │
│  │ data engineering, visualization, ...           │    │
│  │ + domain knowledge + skill_generator v2.0      │    │
│  └───────────────────────────────────────────────┘    │
│                                                        │
│  L2: Context (Temporary Experiments)                  │
│  ┌───────────────────────────────────────────────┐    │
│  │ Draft skills under evaluation                  │    │
│  │ Session-specific working memory                │    │
│  └───────────────────────────────────────────────┘    │
│                                                        │
│  Blockchain: Immutable audit trail (55+ blocks)       │
│  ┌───────────────────────────────────────────────┐    │
│  │ Every L0/L1 change recorded with hash,         │    │
│  │ timestamp, and reason                          │    │
│  └───────────────────────────────────────────────┘    │
└───────────────────────────────────────────────────────┘
```

### Layer Details

| Layer | Purpose | Mutability | Blockchain |
|-------|---------|------------|------------|
| **L0** | Scientific principles, safety rules, governance | Human approval required | Full transaction record |
| **L1** | Domain knowledge, research skills | Freely modifiable | Hash reference |
| **L2** | Draft skills, experiments, session context | Freely modifiable | None |

## Available Research Skills (48 skills, 12 categories)

### Statistics (7 skills)

| Skill | Priority | Purpose |
|-------|----------|---------|
| `test_selection_advisor` | P0 | Recommend appropriate statistical tests based on data distribution and study design |
| `power_analysis_planner` | P0 | Calculate minimum sample size and statistical power |
| `effect_size_interpreter` | P0 | Interpret and report effect sizes with confidence intervals |
| `multiple_testing_controller` | P0 | Apply and justify FDR/Bonferroni correction |
| `assumption_checklist_enforcer` | P1 | Verify statistical test assumptions before analysis |
| `bayesian_frequentist_router` | P1 | Guide selection between Bayesian and frequentist approaches |
| `missing_data_strategy_advisor` | P1 | Advise on handling missing data (MCAR/MAR/MNAR) |

### Research Ethics (4 skills)

| Skill | Priority | Purpose |
|-------|----------|---------|
| `privacy_risk_preflight` | P0 | Pre-flight privacy risk assessment for data analysis |
| `consent_scope_checker` | P0 | Verify analyses fall within informed consent boundaries |
| `data_governance_auditor` | P0 | Audit FAIR compliance and data governance |
| `conflict_of_interest_prompter` | P1 | Identify and disclose conflicts of interest |

### Reproducibility (5 skills)

| Skill | Priority | Purpose |
|-------|----------|---------|
| `analysis_environment_recorder` | P0 | Capture complete environment snapshots |
| `seed_and_version_enforcer` | P0 | Enforce random seed and software version recording |
| `provenance_chain_builder` | P0 | Build traceable data lineage from raw data to results |
| `result_regeneration_checker` | P1 | Verify published results can be regenerated |
| `artifact_packager_for_submission` | P1 | Package all artifacts for journal submission |

### Scientific Writing (5 skills)

| Skill | Priority | Purpose |
|-------|----------|---------|
| `hypothesis_to_storyline` | P1 | Build narrative arc from hypothesis to conclusions |
| `abstract_composer_structured` | P1 | Compose structured abstracts (IMRaD format) |
| `methods_reproducibility_writer` | P1 | Write Methods sections enabling full reproduction |
| `response_to_reviewer_mapper` | P1 | Structure point-by-point responses to reviewers |
| `cover_letter_drafter_journal_fit` | P1 | Draft cover letters tailored to target journals |

### Research Planning (5 skills)

| Skill | Priority | Purpose |
|-------|----------|---------|
| `research_question_refiner` | P1 | Refine vague ideas into specific, testable questions |
| `novelty_gap_mapper` | P1 | Identify knowledge gaps and articulate novelty |
| `feasibility_risk_matrix_builder` | P1 | Assess feasibility and risks of proposed projects |
| `milestone_timeline_designer` | P1 | Design realistic milestones and timelines |
| `grant_alignment_checker` | P1 | Check proposal alignment with grant requirements |

### Data Analysis (4 skills)

| Skill | Priority | Domain | Purpose |
|-------|----------|--------|---------|
| `ngs_pipeline_designer` | P1 | Genomics | Design NGS pipelines (RNA-seq, ChIP-seq, WGS, etc.) |
| `qc_failure_diagnoser` | P1 | General | Diagnose causes of quality control failures |
| `batch_effect_triager` | P1 | General | Detect, assess, and correct batch effects |
| `confounder_detector` | P1 | General | Identify and address confounding variables |

### Scientific Philosophy (4 skills)

| Skill | Priority | Purpose |
|-------|----------|---------|
| `claim_evidence_separator` | P1 | Separate claims from evidence, observation from interpretation |
| `falsifiability_checker` | P1 | Check whether hypotheses are testable and falsifiable |
| `assumption_surface_mapper` | P1 | Surface and document implicit assumptions |
| `negative_result_value_extractor` | P1 | Extract scientific value from negative/null results |

### Machine Learning (5 skills)

| Skill | Priority | Purpose |
|-------|----------|---------|
| `model_selection_advisor` | P1 | Guide ML model selection based on problem characteristics |
| `cross_validation_designer` | P1 | Design validation strategies to avoid data leakage |
| `overfitting_detector` | P1 | Detect and mitigate overfitting |
| `feature_importance_interpreter` | P1 | Interpret feature importance responsibly (SHAP, permutation) |
| `ml_reproducibility_checklist` | P1 | Comprehensive checklist for reproducible ML experiments |

### Data Engineering (2 skills)

| Skill | Priority | Purpose |
|-------|----------|---------|
| `data_cleaning_advisor` | P1 | Guide systematic data cleaning strategies |
| `exploratory_data_analysis_guide` | P1 | Systematic EDA workflow |

### Visualization (2 skills)

| Skill | Priority | Purpose |
|-------|----------|---------|
| `visualization_best_practices` | P1 | Principles for effective and honest data visualization |
| `figure_accessibility_checker` | P1 | Check figures for color vision deficiency support |

### Domain Knowledge (4 skills)

| Skill | Purpose |
|-------|---------|
| `genomics_basics` | Central dogma, key technologies, common analysis types |
| `ngs_pipelines` | Standard RNA-seq pipeline patterns and best practices |
| `journal_standards` | Target journals, formatting requirements, submission checklists |
| `data_science_foundations` | ML fundamentals, data workflows, common pitfalls |

### Meta-Skill

| Skill | Version | Purpose |
|-------|---------|---------|
| `skill_generator` | v2.0 | Generate and evaluate new research skills from multiple sources (conversation, deep research, persona assembly, literature, pipeline, cross-chain) |

## Domain Tags

Skills are tagged by their applicable domain:

| Tag | Description | Count |
|-----|-------------|-------|
| `general` | Cross-domain, applicable to any research field | 40 |
| `genomics` | Genomics and bioinformatics specific | 4 |
| `ml` | Machine learning specific | 5 |

## Getting Started

### Prerequisites

- Ruby 3.2+
- [KairosChain](https://github.com/masaomi/KairosChain) gem v2.0.2+
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) or any MCP-compatible client

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/masaomi/ResearchersChain_2026.git
cd ResearchersChain_2026

# 2. Install KairosChain
gem install kairos-chain

# 3. Configure your MCP client
# Create .mcp.json in the project root:
cat > .mcp.json << 'EOF'
{
  "mcpServers": {
    "researchers-chain": {
      "command": "kairos-chain",
      "args": ["--data-dir", "/path/to/ResearchersChain_2026/.kairos"]
    }
  }
}
EOF

# 4. Start Claude Code in the project directory
claude
```

When Claude Code starts, it automatically connects to the ResearchersChain MCP server. The `researcher.md` constitution is injected into the system prompt, and all 48 L1 knowledge skills become available.

### Verify the Connection

Once connected, you can verify the setup:

```
# Check instructions mode
instructions_update(command: "status")
# → current_mode: "researcher"

# List available knowledge
knowledge_list()
# → 48 research skills across 12 categories

# Check blockchain integrity
chain_verify()
# → Blockchain Integrity Verified: OK

# View evolution history
chain_history(limit: 5, format: "formatted")
```

## How to Use

### During Research Conversations

Simply work with the AI as you normally would. The researcher constitution automatically guides the agent's behavior:

- **Planning an experiment?** The agent will suggest power analysis and remind you about sample size justification.
- **Analyzing RNA-seq data?** The agent draws on `ngs_pipelines` knowledge and enforces reproducibility practices.
- **Training an ML model?** The agent references `cross_validation_designer` and `overfitting_detector`.
- **Writing a paper?** The agent uses `hypothesis_to_storyline` and separates observation from interpretation.
- **Handling patient data?** The `privacy_risk_preflight` principles are active in every conversation.
- **Creating figures?** The agent checks `visualization_best_practices` and `figure_accessibility_checker`.

### Querying Knowledge Directly

You can explicitly access any skill:

```
# Read a specific skill
knowledge_get(name: "test_selection_advisor")

# Search for relevant skills
knowledge_list(search: "statistics")
knowledge_list(search: "machine learning")
```

### Evolving the Knowledge Base

ResearchersChain is designed to grow through use. The skill_generator v2.0 supports multiple knowledge sources:

```
Knowledge source recognized
  (conversation, deep research, persona assembly, literature, pipeline, cross-chain)
  ↓
Draft a new skill with source tracking:
  → context_save(name: "draft_new_skill", content: "...", session_id: "session_001")
  ↓
Validate through Persona Assembly:
  → skills_promote(command: "analyze", personas: ["kairos", "pragmatic", "skeptic"])
  ↓
Promote to stable knowledge:
  → skills_promote(command: "promote", from_layer: "L2", to_layer: "L1")
  ↓
Record checkpoint:
  → state_commit(reason: "Promoted new_skill to L1")
```

### Skill Priority System

| Priority | Criteria | Examples |
|----------|----------|---------|
| **P0** | Directly improves reproducibility, statistical validity, or ethical safety | test_selection_advisor, privacy_risk_preflight |
| **P1** | Improves research speed or expands capability | model_selection_advisor, hypothesis_to_storyline |
| **P2** | Labor-saving (only if no quality degradation) | literature_triage_assistant, lab_note_structurer |

### Quality Rubric

Skills are evaluated on a 100-point scale:

| Axis | Points | Description |
|------|--------|-------------|
| Reproducibility | 25 | Are skill usage results reproducible? |
| Statistical validity | 20 | Does it promote correct statistical reasoning? |
| Research ethics safety | 20 | No ethical violations or privacy risks? |
| Utility | 20 | Speed improvement or cognitive load reduction? |
| Non-duplication | 15 | Not duplicating existing skills? |

- **80+ points**: Candidate for stable L1 knowledge
- **60-79 points**: Keep in L2 for further validation
- **Below 60**: Reject
- **Critical ethics/safety violation**: Reject regardless of score

## Project Structure

```
ResearchersChain_2026/
├── .kairos/                    # KairosChain data directory
│   ├── skills/
│   │   ├── kairos.rb           # L0 meta-skills (governance, safety, evolution)
│   │   ├── researcher.md       # L0 Researcher Constitution
│   │   ├── config.yml          # KairosChain configuration
│   │   └── versions/           # L0 evolution snapshots
│   ├── knowledge/              # L1 stable knowledge (48 research skills)
│   ├── context/                # L2 temporary experiments
│   ├── config/                 # Safety and tool metadata
│   └── storage/
│       └── blockchain.json     # Immutable audit trail (55+ blocks)
├── storage/
│   └── snapshots/              # State commit snapshots
└── README.md
```

## Built With Agent-First Driven Development (AFD)

ResearchersChain was built entirely through MCP tool calls. This is an experiment in **Agent-First Driven Development (AFD)**, where the AI agent constructs its own knowledge architecture using only the tools available to it.

### Build History

| Phase | Action | MCP Tool | Result |
|-------|--------|----------|--------|
| 2 | Create researcher constitution + activate mode | `instructions_update` | L0 established |
| 3 | Add skill_generator meta-skill | `knowledge_update` | Core evolution engine |
| 4 | Seed domain knowledge (3 skills) | `knowledge_update` | Foundation knowledge |
| 5 | Draft P0 skills in L2 (10 drafts) | `context_save` | Quality guardrails |
| 6 | Promote P0 skills to L1 (10 skills) | `knowledge_update` | Critical skills live |
| 7 | Blockchain checkpoint | `state_commit` | 18 blocks |
| A | Expand scope to data science | `instructions_update` | Broader domain |
| B | Evolve l0_governance + skill_generator v2.0 | `skills_evolve` + `knowledge_update` | L0 evolution works |
| C | Create 33 P1 skills across 12 categories | `knowledge_update` | Full skill set |
| D | Persona Assembly validation | `skills_promote` | Quality confirmed |
| E | Final checkpoint | `state_commit` | 55 blocks |

The entire build history is recorded on the blockchain and can be replayed via `chain_history()`.

## Researcher Constitution

The following principles are injected into every conversation via `researcher.md`:

1. **Reproducibility** — Every analysis must be reproducible. Record all parameters and environments.
2. **Falsifiability** — Hypotheses must be testable and refutable. State null hypotheses explicitly.
3. **Evidence-based reasoning** — Claims require evidence. Distinguish observation from interpretation.
4. **Intellectual honesty** — Report negative results. Acknowledge limitations. No p-hacking.
5. **Open science** — Default to openness. Share data, code, and methods.

### Quality Guardrails

- **Statistical**: State test assumptions. Report effect sizes and confidence intervals. Apply multiple testing correction.
- **Reproducibility**: Record random seeds, software versions, data versions, pipeline parameters.
- **Output format**: Separate observation, interpretation, limitation, and next action.

### Ethics

- Patient/sample privacy is non-negotiable
- Informed consent must be verified before data use
- FAIR principles guide data management
- GDPR/HIPAA compliance where applicable

## Roadmap

- [x] L0 Researcher Constitution
- [x] L1 Foundation skills — P0 (statistics, ethics, reproducibility)
- [x] Skill generator v2.0 (multi-source, domain tags, evidence levels)
- [x] Blockchain audit trail (55+ blocks)
- [x] Scope expansion: genomics → data science general
- [x] L0 evolution via `skills_evolve` (l0_governance updated)
- [x] Persona Assembly validation (KairosChain bugs fixed)
- [x] P1 skills — 33 skills across 12 categories
- [ ] P2 skills (review, assistance) — deferred to post-operation
- [ ] HestiaChain Meeting Place integration (agent-to-agent communication)
- [ ] AWS EC2 deployment with Streamable HTTP

## Part of the GenomicsChain Ecosystem

ResearchersChain is a component of [GenomicsChain](https://genomicschain.ch), a decentralized platform for secure genomic data analysis and sharing. It serves as the AI research assistant layer, providing:

- Natural language interface for research workflows
- Quality-controlled analysis across data science and genomics
- Auditable knowledge evolution
- Future integration with NFT-based data ownership and DAO governance

## License

MIT License. See [LICENSE](LICENSE) for details.

## Author

Masaomi Hatakeyama

## Acknowledgments

- Built with [KairosChain](https://github.com/masaomi/KairosChain) v2.0.2
- Development plan co-authored by Claude Opus 4.6, Gemini 3.0, Codex GPT 5.3, and Cursor
- Foundation built using Agent-First Driven Development (AFD) methodology
