# Step 4 — Drift Detection

> Part of [Requirements Management](README.md). Run **recurringly** (after each meeting / decision batch) to keep the requirement set consistent with reality.

## Purpose

Detect requirements that have **drifted** from the evolving project: conflicts with decisions or newer sources, staleness, duplicates, and orphans. Surface each with a proposed resolution — never silently rewrite.

## Inputs

- `memory/requirements.md`
- `memory/decisions.md` — especially new/`accepted` decisions.
- `source/*` — newer sources than the requirement's `source:`.
- `memory/risks.md`, `memory/assumptions.md` — invalidated assumptions destabilize requirements.

## Procedure

Scan for four drift patterns; for each, record a finding and a proposed action:

1. **Conflict** — a requirement contradicts a `DEC-###` or a newer source.
   - *Action:* propose superseding or re-prioritizing the requirement; raise `Q-###` if the conflict is unresolved; never auto-delete.
2. **Staleness** — a requirement's `source:` has been superseded, or it has not been touched in a long time with no progress.
   - *Action:* flag for re-validation; if obsolete, propose `status: superseded` with `superseded_by` pointing to a replacement (or `rejected` if dropped).
3. **Duplicate** — two `REQ-###` express the same need.
   - *Action:* merge — keep the better-formed one, supersede the other (set `superseded_by` both ways via `supersedes`), and consolidate links/acceptance.
4. **Orphan** — a requirement targets a feature/module that was removed from Knowledge, or rests on an `ASM-###` now `invalidated`.
   - *Action:* flag; propose supersede/reject or re-link; raise `Q-###` if unclear.

5. **Write** `outputs/reports/requirements-drift-<date>.md` listing every finding (pattern, REQ, evidence, proposed action, blocking `Q-###` if any).
6. **Apply only unambiguous resolutions** (e.g., clear duplicate merges) with `status: superseded` + links. **Leave ambiguous cases** as findings + `Q-###` for human decision.

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/reports/requirements-drift-<date>.md` | Findings + proposed actions. |
| `memory/requirements.md` | Applied supersessions / merges (unambiguous only). |
| `memory/open-questions.md` | `Q-###` for ambiguous drift needing a decision. |

## Rules

- **Detect, propose, then (carefully) act.** Most drift needs a human decision; only obvious duplicates are auto-merged.
- **Supersede, never delete.** History is preserved via `superseded_by`.
- **Evidence required.** Every finding cites the conflicting decision/source.
- **Invalidated assumptions trigger review.** If `ASM-###` becomes `invalidated`, every requirement in its `impacts:` is re-examined here.

## Example

Finding: `REQ-001` requires SSO by July, but a new `DEC-005` pushes the pilot to September. → **Conflict**. Proposed action: update `REQ-001.statement` deadline to September (bump `updated`, append `DEC-005` to source) — or, if the July date is a hard stakeholder commitment, raise `Q-###` "July SSO vs September pilot — which holds?" rather than silently changing it.
