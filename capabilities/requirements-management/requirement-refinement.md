# Step 1 — Requirement Refinement

> Part of [Requirements Management](README.md). Run after Meeting Intelligence produces new `proposed` requirements.

## Purpose

Turn raw, under-specified requirements into **well-formed** ones: a precise statement, testable acceptance criteria, a justified priority, a stated rationale, and explicit assumptions. Clear, complete requirements are promoted from `proposed` → `accepted`.

## Inputs

- `memory/requirements.md` — especially `status: proposed` items.
- `knowledge/*` — to ground the statement in modules/features/actors.
- `memory/decisions.md` — rationale often comes from a decision (`DEC-###`).
- `memory/assumptions.md` — to capture what a requirement rests on.
- `memory/open-questions.md` — for genuinely missing information.

## Procedure

For each `proposed` (or under-specified `accepted`) requirement:

1. **Statement** — rewrite as a single, precise, verifiable sentence. Prefer the *"The system shall…"* form for functional requirements; *"The system shall exhibit…"* for non-functional. Remove ambiguity ("fast", "user-friendly") by binding it to a measurable target or a `Q-###`.
2. **Acceptance criteria** — list 2–5 testable conditions under `acceptance:`. "How would we prove this is met?" If you cannot write one, the requirement is not yet clear — raise a `Q-###`.
3. **Type** — set `type:` `functional | non-functional | constraint` (formalized in step 2).
4. **Priority** — set/confirm `priority:` using the originating decision or scope phase; if unstated, raise `Q-###` rather than guessing.
5. **Rationale** — link the decision that drives it (`relates_to: [DEC-###]`); add a one-line `rationale` note. If no decision exists, record the inferred reason as an **assumption** (`ASM-###`), not as fact.
6. **Assumptions** — for anything the requirement *takes for granted* (an integration exists, a policy holds, a threshold applies), create an `ASM-###` in `memory/assumptions.md` and link it via `assumptions: [ASM-###]`. Mark genuinely unknown items as `Q-###` instead.
7. **Trace** — ensure `feature: [FEAT-###]` is set (step 3 formalizes; flag missing links here).
8. **Promote** — once statement + acceptance + type + priority + rationale + trace are all present and nothing is `Q-###`-blocked, set `status: accepted`. Otherwise leave `proposed` and list the blockers.
9. **Bump `updated`** on every modified requirement.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/requirements.md` | Refined requirements; some promoted to `accepted`. |
| `memory/assumptions.md` | New `ASM-###` for inferred rationale/resting assumptions. |
| `memory/open-questions.md` | New `Q-###` for genuinely missing info blocking acceptance. |

## Rules

- **No fabrication.** Infer only where the source/decision clearly implies it; otherwise `ASM-###` (flagged) or `Q-###` (asked).
- **Acceptance is mandatory for `accepted`.** A requirement cannot be promoted without testable criteria.
- **Assumptions are explicit, not hidden.** A silent assumption is a latent defect — surface it as `ASM-###`.
- **Provenance preserved.** `source:` stays; refinement adds detail, not new unsourced claims.
- **Conservative promotion.** When in doubt, keep `proposed` and raise a question.

## Example

Raw (from Meeting Intelligence): `REQ-001` *"SSO via Okta must be live by July."* — `status: proposed`, no acceptance, no rationale.

Refined → promote to `accepted`:

```markdown
### REQ-001 — Employee portal SSO via Okta

---
id: REQ-001
title: Employee portal SSO via Okta
statement: The employee portal shall authenticate users via corporate SSO backed by Okta, with SSO operational by 2026-07-31 to enable pilot onboarding.
type: functional
status: accepted
priority: high
phase: 1
feature: [FEAT-001]
assumptions: [ASM-001]
source: [SRC-MTG-2026-06-15]
owners: [ACTOR-002]
acceptance:
  - Employees sign in with corporate credentials; no separate portal password exists.
  - Okta issues the assertion consumed by the Identity module (MOD-002).
  - SSO is operational in a pilot environment by 2026-07-31.
rationale: Drives the July pilot; corporate SSO standard (BR-001) + decision DEC-001.
tags: [auth, sso]
created: 2026-06-15
updated: 2026-06-16
supersedes: []
superseded_by: []
relates_to: [DEC-001, BR-001, ACT-001, ACT-002]
---
```

New assumption created:

```markdown
### ASM-001 — Okta licensing is sufficient for all portal users

---
id: ASM-001
title: Okta licensing is sufficient for all portal users
statement: The confirmed Okta license count (ACT-001) will cover all portal users including pilot.
status: open
impacts: [REQ-001]
source: [SRC-MTG-2026-06-15]
created: 2026-06-16
updated: 2026-06-16
validated_by:
---
```
