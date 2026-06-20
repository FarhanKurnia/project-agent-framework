# Step 4 — Portfolio Sprint Review Prep

> Part of [Portfolio Sprint Planning](README.md). Run at sprint end. Extends [`../sprint-planning/sprint-review-prep.md`](../sprint-planning/sprint-review-prep.md) across projects.

## Purpose

Record the portfolio sprint's outcomes per project, carry-overs, and actual velocity, then transition each project's backlog items accordingly.

## Inputs

- The committed portfolio sprint.
- Each in-scope project's `memory/backlog.md` (current status), recent `outputs/meetings/*`, `memory/risks.md`/`decisions.md`/`open-questions.md`.

## Procedure

1. **Per-project completed vs planned** — for each `<slug>:BKL-###`, record done/partial/carry-over with evidence.
2. **Transition backlogs (carve-out, symmetric to commitment):** in each project's `memory/backlog.md`, set done items `status: done`; carry-overs return to `ready` (clear `sprint:` or note the carry-over) with a reason. (Phase B: refresh `current_load` on `PERSON-###`.)
3. **Record actual velocity** (points/days completed vs budget) for the next capacity model.
4. **Capture emergent items** per project (RSK/DEC/Q).
5. **Close** the sprint artifact (`status: closed`).

## Outputs

| Artifact | Notes |
|----------|-------|
| `portfolio/sprints/sprint-<PS-NN>-<date>.md` | Review section filled; `status: closed`. |
| each `projects/<slug>/memory/backlog.md` | Done items closed; carry-overs returned to `ready`. |
| per-project `memory/*` | New RSK/DEC/Q as they emerged. |

## Rules

- **Evidence-based.** No "done" without proof.
- **Carve-out still narrow.** Review edits only `status`/`sprint`/`updated` on listed BKLs in each project.
- **Velocity is historical, not aspirational.** Use the average of recent portfolio sprints; if volatile, use the lower bound and flag it.

## Example

`PS-01` closes: `employee-portal:BKL-001` done (SSO shipped); `helpdesk:BKL-001` partial (import 80% → carry-over). Actual velocity ~8 ideal-days vs ~10 planned.
