# Step 4 — Dependency Mapping

> Part of [Backlog Management](README.md). Run after [Estimation Capture](estimation-capture.md).

## Purpose

Link backlog items that **block** each other, so ordering is explicit and the critical path is visible. This is what turns a flat list into a *plan-able* backlog.

## Inputs

- `memory/backlog.md` — all items.
- `memory/requirements.md` — cross-requirement dependencies.
- `knowledge/modules.md` — module dependency map (technical sequencing).

## Procedure

1. **For each pair of items**, ask: "must A be done before B can start?"
   - If yes → set `dependencies: [<blocking IDs>]` on **B** (the blocked item), and ensure **A** notes it blocks B.
2. **Use module dependencies as a guide.** If `MOD-002` must precede `MOD-001` (per `knowledge/modules.md`), the backlog items delivering them inherit that order.
3. **Link requirement dependencies too.** If `REQ-002` depends on `REQ-001`, their backlog items reflect it.
4. **Detect cycles.** If mapping produces a circular dependency, raise a `Q-###` ("BKL-X and BKL-Y are mutually blocking — how to sequence?") — do not invent an order.
5. **Record the critical path** informally: which chain of `dependencies` is longest (highest cumulative size). This informs future prioritization/sprint planning.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/backlog.md` | `dependencies:` populated; blocked items marked. |
| `memory/open-questions.md` | `Q-###` for any cyclic/ambiguous dependency. |

## Rules

- **Direction is explicit.** `dependencies:` on an item lists what **blocks it** (predecessors). Always record in this direction.
- **Bidirectional awareness.** If B depends on A, the agent understands A must be scheduled first; no need to duplicate the link on A, but A's status blocks B's progress.
- **No fabrication.** Only link where a real technical or requirement dependency exists. "Nice to do first" is not a dependency.
- **Cycles are questions, not silent choices.**

## Example

`BKL-001` (SSO integration) must exist before `BKL-004` (portal login UI) can be tested end-to-end. So:

```markdown
### BKL-004 — Employee portal login UI
...
dependencies: [BKL-001]
...
---
```

Critical path note (informal): `BKL-001 → BKL-004` is the gating chain for the July pilot.
