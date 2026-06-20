# Step 4 — Sprint Review Prep

> Part of [Sprint Planning](README.md). Run at **sprint end**, before the review/demo.

## Purpose

Prepare an evidence-based account of the sprint: what was completed vs planned, what carried over, and what new risks/decisions/questions emerged — feeding the next Sprint Proposal and Reporting.

## Inputs

- The committed sprint artifact (`outputs/sprints/sprint-<n>-<date>.md`).
- `memory/backlog.md` — current status of the sprint's items.
- Recent `outputs/meetings/*` — standups/decisions during the sprint.
- `memory/risks.md`, `memory/decisions.md`, `memory/open-questions.md` — what emerged.

## Procedure

1. **Compare completed vs planned** — for each committed `BKL-###`, determine its real status (`done` requires evidence: a delivered feature / completed action, not an assumption). Categorize: **done / partial / not-started / dropped**.
2. **Record carry-overs** — items not `done` move to the next sprint's candidate list; note the reason (blocked, underestimated, deprioritized).
3. **Compute actual velocity** — sum of `size` for `done` items; record it for future Capacity Modeling.
4. **Surface emergent items** — new `RSK-###`, `DEC-###`, `Q-###`, or `REQ-###` that arose during the sprint (often captured via Meeting Intelligence on standups).
5. **Close delivered backlog items** — set `status: done` with a `resolution` note + date (verify first, per Grooming rules).
6. **Write the review** into the sprint artifact's *Review* section, set `status: closed` with the close date.
7. **Report** completion rate, carry-overs, actual velocity, and emergent items.

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/sprints/sprint-<n>-<date>.md` | *Review* section filled; `status: closed`. |
| `memory/backlog.md` | Delivered items → `done` (verified); carry-overs noted for next sprint. |
| `memory/risks.md` / `decisions.md` / `open-questions.md` | Emergent items from the sprint. |

## Rules

- **Evidence-based completion.** "Done" requires proof (delivered feature / completed action). No assumptions.
- **Carry-overs are explicit, not silent.** Every non-done item is accounted for with a reason.
- **Actual velocity is recorded.** It feeds the next Capacity Modeling — keep it honest.
- **Never delete — close.** Undone items return to `ready` or roll forward; they are not erased.
- **Emergent items are captured.** A sprint that produced a new risk but no `RSK-###` is under-reported.

## Example

Sprint S-01 review: BKL-001 `done` (Okta integration delivered, OIDC confirmed — closes `Q-003`), BKL-002 `partial` (UI built, blocked on end-to-end testing) → carry-over to S-02. Actual velocity: 3 points (vs 5 planned). New: `RSK-002` "Okta rate limits under load". Sprint artifact `status: closed`; BKL-001 → `done`. Next proposal (S-02) seeds from BKL-002 carry-over.
