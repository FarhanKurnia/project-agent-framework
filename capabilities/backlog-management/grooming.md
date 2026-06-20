# Step 5 — Grooming (recurring)

> Part of [Backlog Management](README.md). Run **recurringly** (e.g., each sprint or after each major meeting), not just once.

## Purpose

Keep the backlog **accurate over time**: split items that turned out large, close items that were delivered or dropped, re-evaluate stale priorities/estimates, and reconcile against new requirements. A backlog that isn't groomed rots into noise.

## Inputs

- `memory/backlog.md` — current state.
- `memory/requirements.md` and `memory/decisions.md` — recent changes (new requirements, superseded decisions).
- Recent `outputs/*` (MOMs) — what was actually delivered/decided lately.

## Procedure

1. **Close delivered work.** For each `BKL-###` whose `delivers:` feature/requirement is now met (or whose action completed), set `status: done` with a `resolution` note and date. Verify against sources — do not assume.
2. **Drop stale items.** Items whose `derived_from` requirement was `rejected`/`superseded` → set `status: dropped` with the reason (cite the superseding `DEC-###`).
3. **Split oversized items.** Items still `size: L/XL` (or consistently slipping) → split into smaller `BKL-###` children, all `derived_from` the same origin; supersede the parent by linking.
4. **Re-estimate changed items.** If new Knowledge arrived (e.g., `Q-###` answered), update `size`/`confidence` and resolve the linked question.
5. **Re-prioritize on signal.** A new `DEC-###` or scope change → adjust `priority` and record a new prioritization decision if material.
6. **Reconcile new requirements.** Run Backlog Generation (step 1) for any `REQ-###` newly promoted to `accepted` since last grooming.
7. **Report churn**: items closed, dropped, split, re-estimated, and newly added — so the change is auditable.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/backlog.md` | Status transitions, splits, re-estimates, additions. |
| `memory/open-questions.md` | Resolved questions closed; new ones raised. |

## Rules

- **Verify before closing.** "Done" requires evidence (a delivered feature / completed action), not assumption.
- **Never delete.** `done`/`dropped` items stay for history.
- **Splits preserve provenance.** Child items inherit `derived_from` and cite the parent.
- **Churn is reported.** A grooming run with zero changes is also a valid, reportable outcome.
- **Reconcile-first** still applies: do not recreate items for already-covered work.

## Example

After the next standup, `ACT-002` (Identity design draft) completes and `Q-003` (Okta protocol) is answered "OIDC". Grooming then:
- `BKL-001` `confidence: medium → high`; update `size` if the design clarified scope.
- Close `Q-003` (`status: answered`, `answer: "OIDC"`).
- If `BKL-001` is now clearly two efforts (OIDC login + SCIM provisioning), split into `BKL-001` (login) and `BKL-005` (provisioning), both `derived_from: [REQ-001]`.
