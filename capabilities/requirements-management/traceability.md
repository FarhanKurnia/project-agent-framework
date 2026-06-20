# Step 3 — Traceability

> Part of [Requirements Management](README.md). Run after [Categorization](requirement-categorization.md); refresh **recurringly**.

## Purpose

Establish **bidirectional traceability**: every requirement links to the Knowledge it targets (feature → module → actor) and the Source it came from — and produce a **trace matrix report** so nothing is orphaned or unverifiable.

This is the backbone of requirements governance: it answers *"where did this come from, and what does it build?"* for every `REQ-###`.

## Inputs

- `memory/requirements.md`
- `knowledge/features.md`, `knowledge/modules.md`, `knowledge/actors.md`
- `source/*` (the cited sources)

## Procedure

1. **Verify each requirement's forward links** (`REQ → FEAT → MOD → ACTOR`):
   - `feature: [FEAT-###]` present? If not → `Q-###` ("which feature does REQ-### deliver?").
   - That feature maps to a module/actor in Knowledge? If not → Knowledge gap, flag for the Knowledge track.
2. **Verify backward link (`REQ → Source`)**:
   - `source:` present and the source file exists? If not → `Q-###`.
3. **Build the trace matrix** for the report: one row per requirement with columns `REQ | type | phase | feature | module | actor | source | status`.
4. **Flag trace gaps** explicitly in the report:
   - Untraced requirements (no feature / no source).
   - Features that no requirement targets (forward-coverage gap — handed to Coverage Analysis, step 5).
5. **Write** `outputs/reports/requirements-traceability-<date>.md` from the template.
6. **Resolve simple gaps** by adding links where Knowledge clearly implies them; raise `Q-###` where it does not.

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/reports/requirements-traceability-<date>.md` | The trace matrix + gap list. Regenerable. |
| `memory/requirements.md` | Completed `feature:`/`source:` links. |
| `memory/open-questions.md` | `Q-###` for unresolvable trace gaps. |

## Rules

- **Bidirectional expectation.** Forward (REQ→FEAT) and backward (REQ→Source) must both hold for a fully-traced requirement.
- **No fabrication of links.** Only link where Knowledge/Source supports it; otherwise ask.
- **Report is regenerable.** Re-running overwrites the dated report; gaps shrink over time.
- **Gaps are visible, not hidden.** An untraced requirement stays in the matrix with empty cells + a flag.

## Example

Trace row for `REQ-001`:

| REQ | type | phase | feature | module | actor | source | status |
|-----|------|-------|---------|--------|-------|--------|--------|
| REQ-001 | functional | 1 | FEAT-001 | MOD-002 | ACTOR-S01 (Okta), ACTOR-001 (Employee) | SRC-MTG-2026-06-15 | accepted |

Fully traced. Compare a hypothetical `REQ-009 "Export reports as PDF"` with `feature:` empty → row shows the gap and a linked `Q-###`.
