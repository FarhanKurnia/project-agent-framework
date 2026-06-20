# CLAUDE.md

> This file is the Claude Code entry point. **The authoritative agent contract is [`AGENTS.md`](AGENTS.md).** Read it first.

## What this repo is
`project-agent-framework` (PAF) is a **markdown-native AI Project Management framework**. There is no code, database, or API — the filesystem *is* the database. You operate it by reading and writing structured Markdown files.

## The model (four layers, per project)
```
Source ──▶ Knowledge ──▶ Memory ──▶ (operated on by) Capabilities
(raw)      (curated)     (living)
```
- **Source** (`source/`) — immutable raw docs. Never edit.
- **Knowledge** (`knowledge/`) — stable facts. Edit deliberately.
- **Memory** (`memory/`) — living items (`REQ/DEC/ACT/Q/RSK/BKL`). Edit freely, **always cite a source**.
- **Capabilities** (`capabilities/`) — workflows you execute.

## Before you do anything
1. Read [`AGENTS.md`](AGENTS.md) — ID conventions, frontmatter contract, editing disciplines, guardrails.
2. Identify the **one target project** under `projects/` (or `sample-project/`) and confine all writes to it.
3. `templates/` and `sample-project/` are **read-only** during project tasks.

## Capabilities currently specified
- [Meeting Intelligence](capabilities/meeting-intelligence/README.md) — FSD-first onboarding, meeting analysis, MOM, and extraction of requirements/decisions/action-items/open-questions.
- [Backlog Management](capabilities/backlog-management/README.md) — turn accepted requirements into a prioritized, estimated, dependency-linked backlog.

## Docs
- [`docs/concepts.md`](docs/concepts.md) · [`docs/architecture.md`](docs/architecture.md) · [`docs/roadmap.md`](docs/roadmap.md)

**When in doubt:** cite a source, reconcile before adding, raise an open question rather than guessing. Full rules in [`AGENTS.md`](AGENTS.md).
