# Step 4 — Requirement Extraction

> Part of [Meeting Intelligence](README.md). Run after [Meeting Analysis](meeting-analysis.md), alongside the other extraction steps.

## Purpose

Convert requirement candidates from the analysis into formal `REQ-###` items in `memory/requirements.md`, **reconciled** against existing requirements so nothing is duplicated.

## Inputs

- The in-session analysis (requirement candidates, with topic/section provenance).
- `memory/requirements.md` (current requirements + `counter`).
- `knowledge/features.md` and `knowledge/modules.md` (to map requirements to features).

## Procedure

1. **Load** existing requirements into a lookup (by title + key nouns).
2. **For each requirement candidate**:
   1. **Search** for an existing requirement expressing the same need (semantic match, not just string match).
   2. If a match exists → **update** it: refine `statement`/`priority`/`acceptance` if the meeting adds detail; bump `updated`; append the meeting to `source`; note the reconciliation. Do **not** create a new ID.
   3. If no match → **create** a new `REQ-###`: increment `counter`, write the per-item frontmatter block (filling `statement`, `type`, `status: proposed`, `priority`, `feature`, `source: [<meeting_id>]`, `acceptance`, `tags`, dates).
3. **Link** each requirement to its feature(s) (`FEAT-###`) where known; if the requirement implies a feature that does not exist yet, flag it (it may need adding to Knowledge, or become an open question).
4. **Record reconciliations** (updated existing vs. created new) for the MOM.
5. **Write** the updated `memory/requirements.md`, placing items under "Open / Accepted" or "Superseded / Rejected".

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/requirements.md` | New and updated `REQ-###` items; counter updated. |
| Reconciliation notes | Fed into the MOM's *Reconciliations* section. |

## Rules

- **Provenance required.** Every new/updated requirement sets `source: [<meeting_id>]`.
- **Reconcile-first.** Duplicates are a defect. When in doubt whether two requirements are the same, prefer updating and note the ambiguity in an open question.
- **Proposed by default.** New requirements enter as `status: proposed` unless the meeting explicitly *accepted* them. Acceptance is a human/sign-off concern; record evidence if so.
- **Acceptance criteria.** A requirement without testable acceptance criteria is draft-quality; note that and, where inferable, propose criteria as a suggestion.
- **Never delete.** Supersede via `status` and `superseded_by`.

## Example

Candidate: *"SSO via Okta must be live by July."*

Reconciliation: no existing `REQ` matches → create `REQ-001`:

```markdown
### REQ-001 — Employee portal SSO via Okta

---
id: REQ-001
title: Employee portal SSO via Okta
statement: The employee portal shall authenticate users via corporate SSO backed by Okta, available by July 2026.
type: functional
status: proposed
priority: high
feature: [FEAT-001]
source: [SRC-MTG-2026-06-15]
owners: [alice]
acceptance: [Users log in with corporate credentials, No separate portal password]
tags: [auth, sso]
created: 2026-06-15
updated: 2026-06-15
supersedes: []
superseded_by: []
relates_to: [DEC-001, ACT-001]
---
```

If a later meeting reaffirms this with a deadline change, **update REQ-001** (bump `updated`, append source) rather than creating `REQ-002`.
