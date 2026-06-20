# Step 2 — Meeting Analysis

> Part of [Meeting Intelligence](README.md). Run **per meeting**, before MOM generation and extraction.

## Purpose

Read a raw transcript/notes file and produce a **structured understanding** of the meeting that the downstream steps (MOM, extractions) all consume. This step does **not** write any project files; it produces an in-session analysis.

## Inputs

- The target meeting file: `projects/<project>/source/meetings/YYYY-MM-DD-<slug>.md`.
- The project's current `knowledge/*` (to disambiguate "the portal", "Alice", etc.).
- The project's current `memory/*` (to recognize items that already exist).

## Procedure

1. **Parse metadata** from the source frontmatter: `meeting_id`, `title`, `date`, `attendees`, `type`, `objective`.
2. **Reconcile attendees** to `knowledge/actors.md`:
   - Map each attendee name to an existing `ACTOR-###` where possible.
   - Flag unrecognized attendees as candidates for new actors (do not create yet — note for Knowledge update).
3. **Segment the discussion** into topics, aligned to the agenda where one exists.
4. **For each topic**, capture:
   - A concise summary (what was discussed).
   - Candidate **decisions** (statements of choice, with who decided).
   - Candidate **action items** (commitments, with owner + due if stated).
   - Candidate **requirements** (statements of "the system shall…").
   - Candidate **open questions** (unresolved or ambiguous points).
   - Candidate **risks** (only if explicitly raised).
5. **Disambiguate** using Knowledge: resolve pronouns and shorthand ("it", "the portal", "that module") to concrete `MOD-###`/`FEAT-###`/`ACTOR-###`. Where disambiguation is impossible, tag as an open question.
6. **Hold the analysis in session** as structured notes keyed by topic, each with the five candidate buckets above. This is the input to steps 3–7.

## Outputs

- **In-session structured analysis** (not a file). Consumed by:
  - Step 3 (MOM Generation) — for the discussion summary and attendee list.
  - Steps 4–7 (Extraction) — for their respective candidate buckets.

## Rules

- **Do not write memory yet.** This step only structures; extraction steps do the writing (with reconciliation).
- **Do not invent.** Candidates must trace to specific passages. Note the rough location (topic/section) for provenance.
- **Ambiguity → question.** Anything you cannot confidently classify becomes a candidate open question, not a forced requirement/decision.
- **Stay faithful.** Summaries must not introduce content absent from the transcript.

## Example

Transcript excerpt: *"We'll go with Okta for SSO — Finance needs it live by July. Alice, can you confirm the IdP licenses by next Friday? Not sure yet if contractors get portal access."*

Analysis output (in-session):
- Topic: Identity/SSO
  - Decision candidate: Adopt Okta as the SSO/IdP provider.
  - Action candidate: Alice to confirm IdP licenses — due next Friday.
  - Requirement candidate: SSO via Okta must be live by July.
  - Open-question candidate: Do contractors get portal access?
  - Disambiguation: "portal" → `MOD-### Employee Portal` (from Knowledge); "Alice" → `ACTOR-###`.

This analysis then feeds step 3 (MOM) and steps 4–7 (extraction, with reconciliation).
