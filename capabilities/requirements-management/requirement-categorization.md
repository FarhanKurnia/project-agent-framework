# Step 2 — Requirement Categorization

> Part of [Requirements Management](README.md). Run after [Refinement](requirement-refinement.md).

## Purpose

Classify every requirement by **type**, tag it, and **map it to a scope phase** — so the requirement set can be sliced, queried, and planned against delivery phases.

## Inputs

- `memory/requirements.md` — refined requirements.
- `knowledge/scope.md` — the defined phases and their in-scope features.

## Procedure

1. **Set `type`** on each requirement (if not already from refinement):
   - `functional` — what the system *does* (behavior).
   - `non-functional` — *how well* it behaves (performance, security, usability, availability).
   - `constraint` — a fixed limit or mandate (budget, deadline, regulatory, tech stack).
2. **Set/curate `tags`** — consistent, lowercase labels (`auth`, `reporting`, `compliance`, `mobile`, …). Reuse existing tags; do not mint near-duplicates.
3. **Map `phase`** — assign the scope phase each requirement belongs to (from `knowledge/scope.md`), e.g., `phase: 1`. A requirement that spans phases gets the *earliest* phase where it must be satisfied; note the span in its body.
4. **Flag phase orphans** — a requirement that does not fit any defined phase raises `Q-###` ("which phase does REQ-### belong to?") and is a scope signal (scope may need extending).
5. **Cross-check scope** — every Phase-N in-scope feature should have at least one requirement; missing pairs are surfaced in Coverage Analysis (step 5), not invented here.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/requirements.md` | `type`, `tags`, `phase` populated per item. |
| `memory/open-questions.md` | `Q-###` for phase orphans / ambiguous classification. |

## Rules

- **One type per requirement.** If a statement is both functional and non-functional, split into two `REQ-###`.
- **Phase = earliest satisfaction.** Not "nice to have in." If it's truly out of scope, that's a scope decision (`DEC-###`), not a phase assignment.
- **No fabrication of scope.** If a phase doesn't exist for a requirement, ask (`Q-###`); don't invent a phase.
- **Tag hygiene.** Consolidate synonyms (e.g., `auth` vs `authentication`) into one tag.

## Example

`REQ-001` (SSO via Okta) is functional, tags `[auth, sso]`, and belongs to Phase 1 (it gates the July pilot per `knowledge/scope.md`). Set `type: functional`, `phase: 1`.

A requirement like *"page loads under 2 seconds"* → `type: non-functional`, `phase: 1`, `tags: [performance]`.

A requirement like *"must comply with local data-protection law"* → `type: constraint`, `phase: 1`, `tags: [compliance]` — and likely an `RSK-###` if compliance evidence is uncertain.
