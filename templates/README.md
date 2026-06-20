# Templates

Templates are the **schema** of the framework. Each template defines the canonical shape of one document type, so that every project — and every LLM agent — produces and consumes consistently structured Markdown.

## How to use templates

- **Copy, don't link.** When bootstrapping a project (see the **Project Onboarding** step of Meeting Intelligence), copy the relevant templates *into* the project's directories and fill them with real content.
- **Templates are read-only in normal use.** They evolve only when the framework's conventions change. Do not edit a template as a side effect of a project task.
- **Fill the placeholders.** Anything in `<angle brackets>` is a placeholder. YAML frontmatter fields marked `# TODO` are required and must be completed.

## Layout

```
templates/
├── source/      # Shapes for raw input documents
│   ├── fsd.md               # Functional Specification Document
│   ├── brd.md               # Business Requirements Document
│   ├── sop.md               # Standard Operating Procedure
│   └── meeting-notes.md     # Meeting notes / transcript (input to Meeting Intelligence)
├── knowledge/   # Shapes for curated knowledge
│   ├── project-overview.md
│   ├── actors.md
│   ├── modules.md
│   ├── features.md
│   ├── business-rules.md
│   ├── glossary.md
│   └── scope.md
├── memory/      # Shapes for living memory items (with frontmatter contract)
│   ├── requirements.md      # REQ-###
│   ├── decisions.md         # DEC-###
│   ├── action-items.md      # ACT-###
│   ├── open-questions.md    # Q-###
│   ├── risks.md             # RSK-###
│   ├── backlog.md           # BKL-###
│   └── assumptions.md       # ASM-###
└── outputs/     # Shapes for generated artifacts
    ├── mom.md                       # Minutes of Meeting
    ├── requirements-traceability.md # trace matrix (Requirements Management)
    ├── requirements-coverage.md     # coverage matrix (Requirements Management)
    ├── requirements-drift.md        # drift findings (Requirements Management)
    ├── sprint.md                    # sprint lifecycle artifact (Sprint Planning)
    ├── status-report.md             # weekly/biweekly status (Reporting)
    ├── decision-log.md              # decision history + supersession (Reporting)
    ├── risk-report.md               # risk register by exposure (Reporting)
    ├── open-questions-report.md     # question aging + blockers (Reporting)
    └── portfolio-report.md          # cross-project roll-up (Reporting, repo-root reports/)
```

## Structure of every template

Each template uses the **dual structure** that makes the framework readable by humans *and* operable by agents:

1. **YAML frontmatter** — machine-relevant metadata (IDs, status, dates, provenance, links).
2. **Markdown body** — human-relevant content, organized into stable sections.

Memory templates additionally define a **per-item frontmatter block** so each requirement/decision/etc. is self-describing and individually linkable.

## The frontmatter contract (recap)

| Layer | Provenance (`source:`) | Status lifecycle | Notes |
|-------|------------------------|------------------|-------|
| Source | n/a (is itself a source) | n/a | Immutable, append-only |
| Knowledge | link to Source where extracted | changelog per doc | Slow-changing |
| Memory | **required** for every item | `proposed → accepted → superseded/rejected/closed` | Never delete |
| Outputs | derived; regenerable | overwritable | Cites the capability run |

See [`AGENTS.md`](../AGENTS.md) §3–§5 for the full ID and editing conventions.

## Adding a new template

1. Add the file under the right `templates/<category>/` directory.
2. If it introduces a new ID prefix or memory type, document it in [`AGENTS.md`](../AGENTS.md) §3.
3. Reference it from the relevant capability's `README.md`.
4. Note it in [`docs/roadmap.md`](../docs/roadmap.md) if it belongs to a future phase.
