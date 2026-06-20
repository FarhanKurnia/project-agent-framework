# portfolio/profiles/

This directory holds **build-team profiles** — the people who *execute* backlog work across projects (developers, QA, analysts). It is distinct from each project's `knowledge/actors.md`, which models the *system users* of a product.

> **Status: specified (Phase B).** The roster lives in [`team.md`](team.md) as `PERSON-###` items (optional `TEAM-###` squads). It powers skill-based assignment, capability measurement, and effective-sprint planning in [Portfolio Sprint Planning](../../capabilities/portfolio-sprint-planning/skill-assignment.md).

## Shape
- **One file:** `team.md` (the org's build roster), with `PERSON-###` items.
- **ID prefix:** `PERSON-###` (persons), optional `TEAM-###` (squads) — org-wide, distinct from per-project `ACTOR-###`.
- **Per-person fields:** name, role, skills (slug array), level, availability %, current_load, home_project, contact, status, source.
- **Template:** [`templates/portfolio/team.md`](../../templates/portfolio/team.md).
- **Capability:** [`profile-management`](../../capabilities/profile-management/README.md) (onboard / maintain / reconcile load). Command: `/profile`.

## How it feeds sprint planning
- **Capacity:** per-person ceiling (`availability` − `current_load`), not just a team total.
- **Assignment:** owner recommended by skill-overlap (`skills_required` on the BKL vs the person's `skills`).
- **Capability measurement:** a coverage matrix (skills-needed vs skills-available) is rendered in each portfolio sprint; gaps raise `Q-###`.

## Confidentiality
Real team data is **gitignored** (private). The tracked, fictional example lives in [`../../sample-portfolio/profiles/`](../../sample-portfolio/profiles/).
