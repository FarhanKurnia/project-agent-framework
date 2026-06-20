# projects/

This directory holds **real project instances** — one directory per project. The framework supports any number of projects, each fully isolated.

## Convention

```
projects/
├── <project-slug>/          # one directory per project
│   ├── project.md           # manifest (identity, domain, status, contacts)
│   ├── source/              # immutable raw inputs
│   ├── knowledge/           # curated, stable facts
│   ├── memory/              # living, cited items
│   └── outputs/             # regenerable artifacts
├── helpdesk/                # example slugs
├── hris/
├── inventory/
└── crm/
```

## Creating a new project

1. **Choose a slug.** Lowercase, kebab-case, domain-revealing (e.g. `hris`, `inventory`, `customer-portal`).
2. **Copy the template skeleton** into `projects/<slug>/`:
   - `project.md` ← `templates/knowledge/project-overview.md` (adapt as the manifest).
   - `source/`, `knowledge/`, `memory/`, `outputs/` ← copy the respective template files from `templates/`.
3. **Run Project Onboarding** (the first step of [Meeting Intelligence](../capabilities/meeting-intelligence/project-onboarding.md)) on the initial source documents to populate Knowledge and initialize Memory.
4. **Commit.** The project now exists and is ready for per-meeting processing.

> The fully-populated [`../sample-project/`](../sample-project/) is a copy-paste reference for what a finished project looks like.

## Isolation rules (recap)

- **IDs are per-project.** `REQ-001` in `hris` and `REQ-001` in `crm` are unrelated.
- **No cross-project references.** A project's files reference only files within the same project (plus the shared framework docs/templates/capabilities).
- **One project per agent task.** Confine all writes to the target project. See [`../AGENTS.md`](../AGENTS.md) §4 and §7.

## Portfolio layer

A project's backlog item may carry `sprint: PS-NN` and `owner:` written by a **portfolio sprint** — the only sanctioned cross-project write (see [`../portfolio/`](../portfolio/) and [`../AGENTS.md`](../AGENTS.md) §7). A portfolio sprint pulls `<slug>:BKL-###` items from multiple projects into one time-boxed sprint at the repo root.

## Suggested project slugs (examples only)

| Slug | Domain example |
|------|----------------|
| `helpdesk` | IT helpdesk / support ticketing |
| `hris` | Human resources information system |
| `inventory` | Warehouse / stock management |
| `crm` | Customer relationship management |

These are illustrative. Replace with your real projects.

## Shared resources (future)

Organization-wide assets that many projects reference (e.g. a corporate glossary) may live under a reserved `_shared/` directory in a future phase. This is noted in [`../docs/roadmap.md`](../docs/roadmap.md) Phase 6 and will not affect per-project isolation.
