# Copilot Instructions

> GitHub Copilot entry point for this repository. **The authoritative agent contract is [`AGENTS.md`](../AGENTS.md).** Read it before editing.

## What this repo is
`project-agent-framework` (PAF) is a **markdown-native AI Project Management framework**. There is no code, database, or API — the filesystem *is* the database. Edits are structured Markdown reads and writes.

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
1. Read [`AGENTS.md`](../AGENTS.md) — ID conventions, frontmatter contract, editing disciplines, guardrails.
2. Identify the **one target project** under `projects/` (or `sample-project/`) and confine all writes to it.
3. `templates/` and `sample-project/` are **read-only** during project tasks.

## Capabilities currently specified
- Meeting Intelligence — FSD-first onboarding, meeting analysis, MOM, extraction (`capabilities/meeting-intelligence/`).
- Requirements Management — refine, classify, trace, and govern requirements (`capabilities/requirements-management/`).
- Backlog Management — prioritized, estimated, dependency-linked backlog (`capabilities/backlog-management/`).

**When in doubt:** cite a source, reconcile before adding, raise an open question rather than guessing. Full rules in [`AGENTS.md`](../AGENTS.md).
