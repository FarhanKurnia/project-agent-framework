# Step 3 — Risk Report

> Part of [Reporting](README.md). Run on demand or each period.

## Purpose

Present the current **risk register** ranked by exposure, with mitigation status — so attention goes to the highest-impact, least-mitigated risks first.

## Inputs

- `memory/risks.md` — `RSK-###` with likelihood, impact, mitigation, status.

## Procedure

1. **Score each risk** — exposure = `likelihood × impact` (low/med/high → 1/2/3); sort descending.
2. **Render the register** — per `RSK-###`: description, score, status, mitigation, contingency, owner, due.
3. **Highlight** — high-exposure risks (score ≥ 6) and any `identified`/unmitigated risk.
4. **Mitigation status roll-up** — how many risks are `mitigating` vs `monitoring` vs `closed`/`materialized`.
5. **Gap check** — a known area of uncertainty with no `RSK-###` → raise `Q-###`.

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/reports/risk-report-<YYYY-MM-DD>.md` | Regenerable. |
| `memory/open-questions.md` | `Q-###` for unrecorded uncertainties. |

## Rules

- **Score-based ordering.** Highest exposure first; no burying red risks.
- **Mitigation status visible.** An unmitigated high risk is the headline, not a footnote.
- **Cite IDs.** Each row links to its `RSK-###` and `affects:`.
- **Read-only upstream.** Honest scoring; do not downgrade to look better.

## Example

| RSK | Risk | L×I | Score | Status | Mitigation | Owner |
|-----|------|-----|-------|--------|------------|-------|
| RSK-001 | SSO slips past July | med×high | 6 | identified | Confirm licenses (ACT-001) | ACTOR-002 |
