# ResearchersChain

A memory-driven AI research assistant for genomics, built on [KairosChain](https://github.com/masaomi/KairosChain).

ResearchersChain is a specialized KairosChain instance that embeds scientific principles, research ethics, and domain knowledge directly into an AI agent's memory layers. It acts as an evolving knowledge companion for genomics researchers — enforcing reproducibility, statistical rigor, and ethical compliance through structured, auditable skills.

## What Is ResearchersChain?

ResearchersChain is **not** a traditional software application. It is a **knowledge architecture** — a layered system of principles, skills, and domain knowledge that shapes how an AI agent assists with genomics research.

When you connect to ResearchersChain via [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (or any MCP-compatible client), the agent automatically:

- Follows a **Researcher Constitution** — core scientific principles injected into every conversation
- Draws on **domain knowledge** — genomics fundamentals, NGS pipeline patterns, journal standards
- Applies **quality guardrails** — statistical test selection, privacy risk checks, reproducibility enforcement
- Records all knowledge evolution on a **blockchain** — every change is traceable and auditable

### How It Differs from a Regular AI Chat

| Regular AI Chat | ResearchersChain |
|----------------|-----------------|
| Stateless — starts fresh each session | Persistent memory across sessions via L0/L1/L2 layers |
| Generic knowledge | Domain-specific skills for genomics research |
| No guardrails | Built-in statistical, ethical, and reproducibility checks |
| No audit trail | Blockchain-recorded knowledge evolution |
| Manual prompting | Automatic constitution injection via MCP |

## Architecture

ResearchersChain uses KairosChain's three-layer memory architecture:

```
┌─────────────────────────────────────────────────┐
│  L0: Constitution (Immutable Principles)        │
│  ┌─────────────────────────────────────────┐    │
│  │ researcher.md — Scientific principles,  │    │
│  │ research ethics, quality guardrails     │    │
│  │ kairos.rb — 8 meta-skills governing    │    │
│  │ self-modification and safety            │    │
│  └─────────────────────────────────────────┘    │
│                                                  │
│  L1: Knowledge (Stable, Reusable Skills)        │
│  ┌─────────────────────────────────────────┐    │
│  │ Domain: genomics_basics, ngs_pipelines, │    │
│  │         journal_standards               │    │
│  │ Statistics: test_selection_advisor,      │    │
│  │   power_analysis_planner, ...           │    │
│  │ Ethics: privacy_risk_preflight,         │    │
│  │   consent_scope_checker, ...            │    │
│  │ Reproducibility: seed_and_version_      │    │
│  │   enforcer, provenance_chain_builder,...│    │
│  │ Meta: skill_generator v1.0              │    │
│  └─────────────────────────────────────────┘    │
│                                                  │
│  L2: Context (Temporary Experiments)            │
│  ┌─────────────────────────────────────────┐    │
│  │ Draft skills under evaluation           │    │
│  │ Session-specific working memory         │    │
│  └─────────────────────────────────────────┘    │
│                                                  │
│  Blockchain: Immutable audit trail              │
│  ┌─────────────────────────────────────────┐    │
│  │ Every L0/L1 change recorded with hash,  │    │
│  │ timestamp, and reason                   │    │
│  └─────────────────────────────────────────┘    │
└─────────────────────────────────────────────────┘
```

### Layer Details

| Layer | Purpose | Mutability | Blockchain |
|-------|---------|------------|------------|
| **L0** | Scientific principles, safety rules, governance | Human approval required | Full transaction record |
| **L1** | Domain knowledge, research skills | Freely modifiable | Hash reference |
| **L2** | Draft skills, experiments, session context | Freely modifiable | None |

## Available Research Skills

### Statistics (P0 — Critical)

| Skill | Purpose |
|-------|---------|
| `test_selection_advisor` | Recommend appropriate statistical tests based on data distribution and study design |
| `power_analysis_planner` | Calculate minimum sample size and statistical power |
| `effect_size_interpreter` | Interpret and report effect sizes with confidence intervals |
| `multiple_testing_controller` | Apply and justify FDR/Bonferroni correction for genomics data |

### Research Ethics (P0 — Critical)

| Skill | Purpose |
|-------|---------|
| `privacy_risk_preflight` | Pre-flight privacy risk assessment for genomic data |
| `consent_scope_checker` | Verify analyses fall within informed consent boundaries |
| `data_governance_auditor` | Audit FAIR compliance and data governance across the lifecycle |

### Reproducibility (P0 — Critical)

| Skill | Purpose |
|-------|---------|
| `analysis_environment_recorder` | Capture complete environment snapshots (OS, packages, seeds, data versions) |
| `seed_and_version_enforcer` | Enforce random seed and software version recording |
| `provenance_chain_builder` | Build traceable data lineage from raw data to final results |

### Domain Knowledge

| Skill | Purpose |
|-------|---------|
| `genomics_basics` | Central dogma, key technologies, common analysis types |
| `ngs_pipelines` | Standard RNA-seq pipeline patterns and best practices |
| `journal_standards` | Target journals, formatting requirements, submission checklists |

### Meta-Skill

| Skill | Purpose |
|-------|---------|
| `skill_generator` | Generate and evaluate new research skills from conversation patterns |

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

When Claude Code starts, it automatically connects to the ResearchersChain MCP server. The `researcher.md` constitution is injected into the system prompt, and all L1 knowledge skills become available.

### Verify the Connection

Once connected, you can verify the setup by asking Claude Code to run these MCP tools:

```
# Check instructions mode
instructions_update(command: "status")
# → current_mode: "researcher"

# List available knowledge
knowledge_list()
# → 14 ResearchersChain-specific skills

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
- **Writing a paper?** The agent references `journal_standards` and separates observation from interpretation.
- **Handling patient data?** The `privacy_risk_preflight` principles are active in every conversation.

### Querying Knowledge Directly

You can explicitly access any skill:

```
# Read a specific skill
knowledge_get(name: "test_selection_advisor")

# Search for relevant skills
knowledge_list(search: "statistics")
```

### Evolving the Knowledge Base

ResearchersChain is designed to grow through use. The evolution workflow:

```
1. Recognize a pattern in your research conversations
2. Draft a new skill:
   → context_save(name: "draft_new_skill", content: "...", session_id: "session_001")
3. Validate through use (1-2 weeks)
4. Promote to stable knowledge:
   → knowledge_update(command: "create", name: "new_skill", content: "...")
5. Record the checkpoint:
   → state_commit(reason: "Promoted new_skill to L1 after 2 weeks validation")
```

### Skill Priority System

When adding new skills, follow this priority:

| Priority | Criteria | Examples |
|----------|----------|---------|
| **P0** | Directly improves reproducibility, statistical validity, or ethical safety | test_selection_advisor, privacy_risk_preflight |
| **P1** | Improves research speed | ngs_pipeline_designer, hypothesis_to_storyline |
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
│   │   └── config.yml          # KairosChain configuration
│   ├── knowledge/              # L1 stable knowledge (14 ResearchersChain skills)
│   ├── context/                # L2 temporary experiments
│   │   └── afd_foundation_001/ # Initial skill drafts
│   ├── config/                 # Safety and tool metadata
│   └── storage/
│       └── blockchain.json     # Immutable audit trail
├── storage/
│   └── snapshots/              # State commit snapshots
└── README.md
```

## Built With Agent-First Driven Development (AFD)

ResearchersChain was built entirely through MCP tool calls — no files were directly edited (with one exception: enabling evolution in `config.yml`). This is an experiment in **Agent-First Driven Development (AFD)**, where the AI agent constructs its own knowledge architecture using only the tools available to it.

### Build Sequence (Phases 2-7)

| Phase | Action | MCP Tool |
|-------|--------|----------|
| 2 | Create researcher constitution + activate mode | `instructions_update` |
| 3 | Add skill_generator meta-skill | `knowledge_update` |
| 4 | Seed domain knowledge (3 skills) | `knowledge_update` |
| 5 | Draft P0 skills in L2 (10 drafts) | `context_save` |
| 6 | Promote P0 skills to L1 (10 skills) | `knowledge_update` |
| 7 | Blockchain checkpoint + Git commit | `state_commit` |

The entire build history is recorded on the blockchain (18 blocks) and can be replayed via `chain_history()`.

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
- [x] L1 Foundation skills (statistics, ethics, reproducibility)
- [x] Skill generator meta-skill
- [x] Blockchain audit trail
- [ ] Persona Assembly validation of existing skills (pending KairosChain bug fix)
- [ ] P1 skills (writing, planning, analysis, philosophy)
- [ ] P2 skills (review, assistance)
- [ ] HestiaChain Meeting Place integration (agent-to-agent communication)
- [ ] AWS EC2 deployment with Streamable HTTP

## Part of the GenomicsChain Ecosystem

ResearchersChain is a component of [GenomicsChain](https://genomicschain.ch), a decentralized platform for secure genomic data analysis and sharing. It serves as the AI research assistant layer, providing:

- Natural language interface for genomics pipelines
- Quality-controlled research workflows
- Auditable knowledge evolution
- Future integration with NFT-based data ownership and DAO governance

## License

MIT License. See [LICENSE](LICENSE) for details.

## Author

Dr. Masa Hatakeyama — University of Zurich, Functional Genomics Center Zurich

## Acknowledgments

- Built with [KairosChain](https://github.com/masaomi/KairosChain) v2.0.2
- Development plan co-authored by Claude Opus 4.6, Gemini 3.0, Codex GPT 5.3, and Cursor Auto
- Foundation built using Agent-First Driven Development (AFD) methodology
