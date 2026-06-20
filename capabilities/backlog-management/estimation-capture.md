# Step 3 — Estimation Capture

> Part of [Backlog Management](README.md). Run after [Prioritization](prioritization.md).

## Purpose

Record a **size estimate** and **confidence** for each backlog item, and **surface estimation unknowns as open questions** rather than guessing. Estimates make future Sprint Planning (Phase 4) feasible.

## Inputs

- `memory/backlog.md` — items needing `size` and `confidence`.
- `knowledge/*` — modules/features to gauge complexity.
- `memory/open-questions.md` — to raise estimation unknowns.

## Procedure

1. **For each backlog item**, assign:
   - `size` — t-shirt (`S | M | L | XL`) or numeric points, using the project's chosen scale (state the scale once in the run).
   - `confidence` — `low | medium | high` reflecting how well-understood the work is.
2. **Use Knowledge to size.** Map the item to its module/feature in `knowledge/*`; unfamiliar or undefined modules reduce confidence.
3. **Low confidence → open question.** Whenever `confidence: low`, raise a `Q-###` naming the specific unknown ("What protocols does the IdP expose for BKL-001?") and link it from the item via `relates_to`/note.
4. **Missing size → flag.** An item that cannot yet be sized stays `size: unknown` with a linked `Q-###`; it is **not** sprint-ready.
5. **Write** the updated `memory/backlog.md` and any new `Q-###`.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/backlog.md` | `size` and `confidence` set per item. |
| `memory/open-questions.md` | `Q-###` for each low-confidence / unsizable item. |

## Rules

- **State the scale.** Mixing t-shirt and points is not allowed within one project.
- **Confidence is honest.** `high` requires the relevant Knowledge to be complete; otherwise downgrade and raise a question.
- **Never fabricate precision.** A wild guess recorded as a precise number is worse than `size: unknown`.
- **Sprint-readiness gate.** Only `size`-set, `confidence ≥ medium` items are eligible for future sprint planning.

## Example

`BKL-001` (Okta SSO integration): Identity module design is still a draft (`ACT-002` open) → `size: M`, `confidence: medium`. Raise `Q-003`: "Which Okta APIs/protocols will the integration use?" until the design lands.

```markdown
### Q-003 — Which Okta integration protocol for SSO?

---
id: Q-003
title: Which Okta integration protocol for SSO?
question: Will the Identity module (MOD-002) integrate via SAML, OIDC, or SCIM?
context: Needed to size BKL-001 accurately and to finalize the design (ACT-002).
status: open
priority: medium
needs_answer_from: [ACTOR-002]
blocks: [BKL-001]
source: [SRC-MTG-2026-06-15]
...
---
```
