# Step 3 — MOM Generation

> Part of [Meeting Intelligence](README.md). Run after [Meeting Analysis](meeting-analysis.md).

## Purpose

Produce a human-readable **Minutes of Meeting** from the structured analysis, written to `outputs/meetings/`. The MOM is the shareable artifact; the formal memory items live in `memory/*` and are *linked* from the MOM.

## Inputs

- The in-session analysis from step 2.
- The MOM template: `templates/outputs/mom.md`.
- IDs assigned during steps 4–7 (run those, or reserve IDs, before finalizing cross-links).

## Procedure

1. **Copy** `templates/outputs/mom.md` to `projects/<project>/outputs/meetings/YYYY-MM-DD-<slug>-mom.md`.
2. **Fill the frontmatter**: `project`, `source_meeting` (the `meeting_id`), `generated_by: meeting-intelligence`, `generated_at`, `status: draft`.
3. **Attendees** — list with reconciled `ACTOR-###` and roles.
4. **Objective** — distill the meeting's purpose in one or two sentences.
5. **Discussion Summary** — one concise section per topic (from the analysis). Tight, human-readable.
6. **Decisions / Action Items / Open Questions / New Requirements** — list each with its assigned `DEC/ACT/Q/REQ` ID and a one-line summary. These cross-link to `memory/*`.
7. **Reconciliations** — list items from *this* meeting that matched or updated *existing* memory (proves dedup). Populate from the extraction steps' reconciliation notes.
8. **Next Steps** — any stated follow-ups.
9. Set `status: draft` (a human or later review step may promote to `final`).

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/meetings/YYYY-MM-DD-<slug>-mom.md` | The MOM. Regenerable if the source changes. |

## Rules

- **Link, don't duplicate.** The MOM references `DEC-###`/`REQ-###`/etc. by ID; the full item lives in memory.
- **Concise.** The MOM summarizes; it is not a transcript. Aim for skim-readability.
- **Faithful.** Every summary must be supportable by the source transcript.
- **Reconciliations are required content.** A MOM with no reconciliations on a mature project is a red flag (possible duplication). On a first/early meeting, "none yet" is fine.

## Example

(See `sample-project/outputs/meetings/2026-06-15-kickoff-mom.md` for a complete generated example.)

A snippet of the generated MOM:

```markdown
## Decisions
- **DEC-001** — Adopt Okta as the corporate SSO/IdP for the employee portal.

## Action Items
| ID | Action | Owner | Due |
|----|--------|-------|-----|
| ACT-001 | Confirm IdP licenses | Alice (ACTOR-001) | 2026-06-27 |

## Reconciliations
- (none — first meeting for this project)
```
