# portfolio/sprints/

Portfolio sprints (`PS-NN`) — a single time-boxed sprint that pulls backlog items (`BKL-###`) from **multiple** project backlogs. Produced by [Portfolio Sprint Planning](../../capabilities/portfolio-sprint-planning/README.md).

## Convention

- **Filename:** `sprint-PS-NN-<YYYY-MM-DD>.md` (e.g. `sprint-PS-01-2026-07-06.md`), dated by window start.
- **Lifecycle:** `proposed → committed → closed` (same as per-project sprints).
- **Template:** [`../../templates/outputs/portfolio-sprint.md`](../../templates/outputs/portfolio-sprint.md).
- **Qualified refs:** every backlog reference uses `<project-slug>:BKL-###`.

## Rules

- **Propose, then commit.** The proposal is the agent's recommendation; commitment requires **human approval** (see the capability's commitment step + the write-back carve-out in [`../../AGENTS.md`](../../AGENTS.md) §7).
- **Integrity two ways.** Every committed-scope row must have a matching backlog entry (`sprint: PS-NN`) in that project's `memory/backlog.md`, and vice-versa.
- **Respect isolation otherwise.** Commitment writes only `sprint:` and `owner:` back to projects — nothing else.

## Confidentiality
Real sprint artifacts are **gitignored** (private). The tracked, fictional example lives in [`../../sample-portfolio/sprints/`](../../sample-portfolio/sprints/).
