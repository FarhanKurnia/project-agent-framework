# Step 5 — Decision Extraction

> Part of [Meeting Intelligence](README.md). Run after [Meeting Analysis](meeting-analysis.md), alongside the other extraction steps.

## Purpose

Convert decision candidates from the analysis into formal `DEC-###` items in `memory/decisions.md`, capturing the **rationale** and any **supersession** of earlier decisions.

## Inputs

- The in-session analysis (decision candidates).
- `memory/decisions.md` (current decisions + `counter`).
- `memory/requirements.md` and `knowledge/*` (to link `affects:`).

## Procedure

1. **Load** existing decisions into a lookup.
2. **For each decision candidate**:
   1. **Search** for an existing decision on the same topic.
   2. If a match exists and the new one **agrees** → update details (rationale, deciders), append source, bump `updated`. Note reconciliation.
   3. If a match exists and the new one **contradicts/supersedes** → set the old decision `status: superseded`, set its `superseded_by: [<new>]`, and create the new `DEC-###` with `supersedes: [<old>]`. **Both links must be set.**
   4. If no match → **create** a new `DEC-###` (increment `counter`), filling `context`, `decision`, `rationale`, `consequences`, `scope`, `deciders`, `source: [<meeting_id>]`, `affects`, dates.
3. **Link `affects:`** to the requirements/features/actors the decision reshapes.
4. **Cascade** obvious consequences: if a decision supersedes one that drove a `REQ-###`, flag that requirement for re-review (e.g., add an open question or note).
5. **Record reconciliations** for the MOM.
6. **Write** the updated `memory/decisions.md`.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/decisions.md` | New/updated/superseded `DEC-###` items; counter updated. |
| Reconciliation notes | Fed into the MOM. |
| Flagged requirements | Requirements touched by a supersession (for re-review). |

## Rules

- **Rationale is required.** A decision without its "why" is useless later. If the transcript states the choice but not the reason, infer the rationale only if clearly implied; otherwise raise a `Q-###` ("Why was DEC-### chosen?").
- **Supersession is bidirectional.** Always set both `supersedes` (on the new) and `superseded_by` (on the old). A one-sided link breaks the history.
- **Provenance required.** `source: [<meeting_id>]`.
- **Never delete.** Superseded decisions remain visible with their links.
- **Status accuracy.** Only mark `accepted` if the meeting clearly agreed. A single person's suggestion is `proposed`.

## Example

Candidate: *"We'll go with Okta for SSO."* No prior decision on this topic.

Create `DEC-001`:

```markdown
### DEC-001 — Adopt Okta as SSO/IdP

---
id: DEC-001
title: Adopt Okta as SSO/IdP
status: accepted
context: Employee portal needs authentication; corporate standard IdP must be chosen.
decision: Use Okta as the identity provider for SSO.
rationale: Okta is already the corporate standard; avoids new vendor onboarding.
consequences: Licenses required; integration effort in Identity module.
scope: project-wide
source: [SRC-MTG-2026-06-15]
deciders: [ACTOR-002]
affects: [REQ-001, FEAT-001]
tags: [auth, sso]
created: 2026-06-15
updated: 2026-06-15
supersedes: []
superseded_by: []
---
```

If a later meeting switches to Azure AD, create `DEC-005` with `supersedes: [DEC-001]`, and set `DEC-001.status: superseded`, `DEC-001.superseded_by: [DEC-005]`.
