# Step 1 — Status Report

> Part of [Reporting](README.md). Run weekly or biweekly (per cadence).

## Purpose

Give stakeholders a single-page answer to *"where are we?"* — progress, key decisions, top risks, blockers, and what's next — all cited to the underlying Memory.

## Inputs

- `memory/requirements.md` (status counts), `memory/decisions.md` (recent), `memory/action-items.md` (due/overdue), `memory/open-questions.md` (blocking), `memory/risks.md` (top), `memory/backlog.md` (progress).
- Current `outputs/sprints/*` (in-flight sprint).
- `knowledge/scope.md` (phase progress).

## Procedure

1. **Header** — project, period (start–end), report date, author.
2. **Overall status** — RAG (red/amber/green) + one-sentence summary, justified by the sections below.
3. **Progress** — current sprint items (`BKL-###`) by status; requirement status counts (`accepted/proposed/...`); phase progress vs `knowledge/scope.md`.
4. **Key decisions this period** — list `DEC-###` with one-line rationale.
5. **Top risks** — `RSK-###` ranked by score, with mitigation status.
6. **Blockers** — blocking `Q-###`, unresolved `dependencies:`, stalled `ACT-###`.
7. **Action items** — `ACT-###` due this period / overdue.
8. **Needs attention** — aging or high-priority `Q-###`.
9. **Upcoming** — next sprint preview / milestones.
10. **Gaps noticed** — raise `Q-###` for anything material that Memory doesn't yet capture.

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/reports/status-<YYYY-MM-DD>.md` | Regenerable; overwritten each period. |
| `memory/open-questions.md` | `Q-###` for noticed gaps (optional). |

## Rules

- **Honest RAG.** Red means a real risk to the period's goal; do not soften.
- **Cite IDs throughout.** Every line points to the item it summarizes.
- **Read-only upstream.** No new primary data; only optional flagging `Q-###`.
- **Skimmable.** One page; detail lives behind the cited IDs.

## Example

> **Overall: 🟡 Amber.** SSO integration (BKL-001) on track for S-01; license count (ACT-001) still pending and gates the pilot.
> **Progress:** S-01 — BKL-001 in-progress, BKL-002 pending. Requirements: 1 accepted / 0 proposed. Phase 1: 1 of 3 features have a requirement.
> **Decisions:** DEC-001 adopt Okta.
> **Top risk:** RSK-001 SSO slips past July (med×high).
> **Blockers:** Q-002 contractor access unresolved; ACT-001 overdue-risk (due 2026-06-27).
