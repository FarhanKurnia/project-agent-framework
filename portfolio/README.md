# portfolio/

This directory holds **cross-project (portfolio) planning artifacts** — work that intentionally spans multiple projects under [`projects/`](../projects/). It is the planning counterpart to [`reports/`](../reports/): where `reports/` *reads up* from projects (read-only synthesis), `portfolio/` *writes down* to projects (a narrow, sanctioned write-back).

## What lives here

```
portfolio/
├── manifest.md        # portfolio identity: org, cadence, sprint counter, in-scope projects
├── sprints/           # portfolio sprints (PS-NN) — one sprint can span many projects
│   └── sprint-PS-NN-<date>.md
└── profiles/          # build-team profiles (Phase B — not yet active)
```

## Why a portfolio layer

The four-layer model (Source → Knowledge → Memory → Capabilities) is **per-project**. But a single team builds **multiple applications** and plans one sprint that pulls work from several project backlogs at once. The portfolio layer sits **above** the project instances to hold that cross-project planning without breaking per-project isolation.

See [`../docs/architecture.md`](../docs/architecture.md) §4 and [`../docs/concepts.md`](../docs/concepts.md) ("Portfolio layer").

## Conventions

- **Portfolio sprint ID:** `PS-NN` (org-wide, monotonic; counter in `manifest.md`). Distinct from per-project `S-NN`.
- **Qualified backlog refs:** a backlog item from a specific project is always written `<project-slug>:BKL-###` (e.g. `hris:BKL-001`). A bare `BKL-###` is ambiguous across projects and is not allowed here. See [`../AGENTS.md`](../AGENTS.md) §3.
- **The cross-project write-back carve-out:** committing a portfolio sprint may write only `sprint:` and `owner:` back into each referenced project's `memory/backlog.md`. See [`../AGENTS.md`](../AGENTS.md) §7.

## Confidentiality (important)

Real portfolio data — actual sprints and the real build team — is **private** and is **gitignored** (see [`../.gitignore`](../.gitignore)). Only the convention files (`README.md`, `manifest.md`) under `portfolio/` are tracked. The fictional, English [`../sample-portfolio/`](../sample-portfolio/) at the repo root is the tracked, shareable reference.

## Status

- **Phase A — Portfolio sprints:** specified (cross-project sprints, write-back). 🟦
- **Phase B — Team profiles:** specified. `profiles/` holds build-team personas (`PERSON-###`) with skills + capacity, powering skill-based assignment, capability measurement, and effective-sprint planning. See [`profiles/README.md`](profiles/README.md) and [`../capabilities/profile-management/`](../capabilities/profile-management/README.md).
