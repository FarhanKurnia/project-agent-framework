# Step 3 — Sprint Commitment

> Part of [Sprint Planning](README.md). Run **only after a human approves** the [Sprint Proposal](sprint-proposal.md).

## Purpose

Finalize the sprint: lock scope, assign owners, set the sprint goal, and reflect the commitment back into the backlog. This is the transition from *plan* to *in-flight work*.

## Inputs

- The proposed sprint artifact (`outputs/sprints/sprint-<n>-<date>.md`, status: proposed).
- **Human approval** (explicit) — possibly with amendments (drop/add items, reassign owners).
- `knowledge/actors.md` — to assign owners.

## Procedure

1. **Confirm amendments** — apply any human changes to scope/owners from the approval. Re-check that the amended set still fits capacity and dependencies; if not, flag and ask.
2. **Assign owners** — map each committed `BKL-###` to an accountable `ACTOR-###`. Resolve ambiguities by raising `Q-###` (do not assign an owner who is not available).
3. **Finalize the sprint goal** — confirm or refine it to match the committed set.
4. **Update the sprint artifact**:
   - `status: committed`, set committed date.
   - Fill the committed scope table (BKL, title, owner, size, priority, dependencies).
5. **Reflect into the backlog**: for each committed `BKL-###`, set `status: in-progress`, `sprint: <sprint-id>`, `owner: <ACTOR-###>`, bump `updated`.
6. **Report** the committed set, owners, goal, and capacity utilization.

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/sprints/sprint-<n>-<date>.md` | Status → `committed`; scope + owners + goal finalized. |
| `memory/backlog.md` | Committed items → `status: in-progress`, `sprint:` and `owner:` set. |
| `memory/open-questions.md` | `Q-###` for any unresolved ownership/dependency. |

## Rules

- **Human approval is mandatory.** Never commit without it. The agent proposes; a human commits.
- **Capacity/delivery re-check on amendment.** If the human changes scope, re-verify fit and dependencies before committing.
- **Single accountable owner per item.** Split items with shared ownership into separate `BKL-###`.
- **Bidirectional integrity.** The sprint artifact and the backlog items must agree (same `BKL-###`, same `sprint:` id).
- **Never delete — transition.** A dropped item returns to `ready` (with a note), it is not erased.

## Example

Human approves the proposal. Commit:
- Sprint artifact `sprint-01-2026-07-06.md` → `status: committed`, owners: BKL-001 → ACTOR-002 (Ben), BKL-002 → ACTOR-002 (Ben). Goal confirmed: *"Employees can sign in to the portal via Okta SSO."*
- Backlog: `BKL-001.status: in-progress`, `sprint: S-01`; `BKL-002.status: in-progress`, `sprint: S-01`.
