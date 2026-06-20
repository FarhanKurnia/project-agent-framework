# Step 2 — Decision Log Report

> Part of [Reporting](README.md). Run on demand or each period.

## Purpose

Render the project's **decision history** with full rationale and a clear view of what has been **superseded** — so past choices are auditable and the *current* decision set is unambiguous.

## Inputs

- `memory/decisions.md` — active, superseded, and rejected decisions.

## Procedure

1. **Active decisions** (`status: accepted`) — for each `DEC-###`: context, decision, rationale, consequences, scope, `affects:`.
2. **Supersession chains** — render `DEC-A → superseded by → DEC-B`, showing how the choice evolved. Both ends of every chain appear.
3. **Proposed (not yet accepted)** — list pending decisions awaiting sign-off.
4. **Rejected** — list `status: rejected` with the reason, for completeness.
5. **Group** by scope/topic where helpful (e.g., architecture vs process).
6. **Gap check** — if a major choice has no recorded `DEC-###`, raise `Q-###` ("no decision recorded for <topic>").

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/reports/decision-log-<YYYY-MM-DD>.md` | Regenerable. |
| `memory/open-questions.md` | `Q-###` for unrecorded-but-important choices. |

## Rules

- **Rationale is shown, not just the choice.** A decision log without the "why" is useless later.
- **Supersession is explicit.** Never silently drop an old decision; render the chain.
- **Cite IDs.** Every entry links to its `DEC-###` and affected `REQ/FEAT`.
- **Read-only upstream.**

## Example

> **Active**
> - **DEC-001 — Adopt Okta as SSO/IdP** *(accepted)* — Rationale: corporate standard (BR-001), avoids new vendor. Affects: REQ-001, FEAT-001.
>
> **Superseded**
> - ~~**DEC-00x — Use SAML**~~ *(superseded by DEC-001)* — superseded when the team standardized on Okta/OIDC.
