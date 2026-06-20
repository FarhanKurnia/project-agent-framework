# Step 3 — Portfolio Sprint Commitment

> Part of [Portfolio Sprint Planning](README.md). Run **only after a human approves** the [proposal](portfolio-sprint-proposal.md). This step performs the **write-back carve-out** — the second sanctioned cross-project exception (see [`AGENTS.md`](../../AGENTS.md) §7).

## Purpose

Finalize the portfolio sprint, assign owners, and reflect the commitment back into **each** referenced project's backlog.

## Inputs

- The proposed sprint artifact (`status: proposed`).
- **Human approval** (explicit; may amend scope/owners).
- `knowledge/actors.md` / `portfolio/profiles/team.md` for owner assignment (Phase A: free-text owner; Phase B: `PERSON-###`).

## Procedure

1. **Confirm amendments** from the approval; re-check capacity + dependencies.
2. **Assign owners** — one accountable owner per `<slug>:BKL-###`. Resolve ambiguity by raising `Q-###` in that project's `open-questions.md`.
3. **Finalize the sprint goal.**
4. **Update the sprint artifact:** `status: committed`, committed date, filled committed-scope table.
5. **Write-back (the carve-out):** for each `<slug>:BKL-###` in the committed scope, edit `projects/<slug>/memory/backlog.md` and set **only**:
   - `sprint: <PS-NN>`
   - `owner: <...>`
   - bump `status: in-progress` and `updated`.

   Do **not** touch any other field or file (no `REQ/DEC/ACT/Q/RSK/ASM`, no `knowledge/`, no `source/`).
6. **Verify bidirectional integrity:** every committed-scope row has a matching backlog entry carrying `sprint: <PS-NN>`; no unlisted BKL carries that `PS-NN`. Mismatch → raise `Q-###`.
7. **Report** the committed set, owners, goal, utilization.

## Outputs

| Artifact | Notes |
|----------|-------|
| `portfolio/sprints/sprint-<PS-NN>-<date>.md` | Status → `committed`. |
| each `projects/<slug>/memory/backlog.md` | Listed items → `status: in-progress`, `sprint: <PS-NN>`, `owner:` set. |
| per-project `memory/open-questions.md` | `Q-###` for unresolved ownership/dependency. |

## Rules

- **Human approval is mandatory.** The agent proposes; a human commits.
- **The carve-out is narrow.** Only `sprint:` + `owner:` (+ status/updated) are written to projects. This is the *only* cross-project write a portfolio sprint performs.
- **Bidirectional integrity.** Sprint artifact ⇔ each project's backlog must agree.
- **Single accountable owner per item.** Split shared-ownership items into separate `BKL-###`.
- **Never delete — transition.** A dropped item returns to `ready` (with a note) in its project.

## Example

Human approves. Commit `PS-01`:
- Sprint artifact → `committed`; owners: `employee-portal:BKL-001` → "FE/BE Dev", `helpdesk:BKL-001` → "BE Dev".
- Backlogs: `projects/employee-portal/memory/backlog.md` `BKL-001` → `sprint: PS-01`, `status: in-progress`; `projects/helpdesk/memory/backlog.md` `BKL-001` → `sprint: PS-01`, `status: in-progress`.
