# Step 2b — Skill Assignment & Capability Coverage

> Part of [Portfolio Sprint Planning](README.md). Runs as a sub-step of [Sprint Proposal](portfolio-sprint-proposal.md), using the roster in [`portfolio/profiles/team.md`](../../portfolio/profiles/team.md). This is the **"effective sprint" engine**: recommend owners by skill + residual capacity, measure team capability, and surface gaps.

## Purpose
For each candidate `<slug>:BKL-###` in the proposed set, recommend a `PERSON-###` owner by skill-overlap and available capacity; build a **coverage matrix** (skills-needed vs skills-available); and raise `Q-###` for skill gaps so the proposed sprint is feasible.

## Inputs
- The proposed scope (candidate `<slug>:BKL-###` items) from the proposal.
- Each item's `skills_required:` (optional; if absent, **infer** — see step 1).
- `portfolio/profiles/team.md` (`PERSON-###` with `skills`, `availability`, `current_load`, `level`, `status`).

## Procedure
1. **Resolve `skills_required` per item.**
   - If the BKL has `skills_required:`, use it.
   - Else **infer** from `delivers: [FEAT-###]` → look up the feature's module/tech in that project's `knowledge/features.md` + `modules.md`, and from the BKL `tags`. Mark inferred skills `(inferred)`. If inference is low-confidence, raise `Q-###` in that project's `open-questions.md`.
2. **Candidate filter.** For each item, from the roster keep PERSONs with `status: active` and **residual capacity** `availability − current_load > 0`.
3. **Skill-overlap score.** `overlap = |skills_required ∩ person.skills| / |skills_required|` (fraction of required skills the person has). Recommend the highest-overlap PERSON. Ties → higher `level` (for the hardest required skill), then most residual capacity.
4. **Capability-gap detection.** If **no** active candidate has `overlap ≥ 0.5`, raise a **`Q-###` skill-gap** in that item's project `open-questions.md`: *"No active PERSON covers `[missing-skill]` for `<slug>:BKL-###`."* The item becomes a **carry-forward candidate** (excluded with reason "skill gap — Q-###").
5. **Overload guard.** Tentatively assign; track running residual capacity per PERSON. Never exceed a PERSON's `availability`. If the best-fit PERSON is full, move to the next-best or defer the item.
6. **Build the coverage matrix** (below) and write it into the sprint artifact. Also note team-level capability health (union of skills-available vs union of skills-needed).
7. **Record** recommended `owner: PERSON-###` (tentative) in the proposed-scope *Owner* column and fill the *Skills needed* column.

## Coverage matrix (rendered in the sprint artifact)
```markdown
## Capability Coverage
| Skill needed | Required by | Covered by | Gap? |
|--------------|-------------|------------|------|
| node | helpdesk:BKL-001 | PERSON-004 | ✅ |
| qa | intranet:BKL-002 | PERSON-002 | ✅ |
| mobile | helpdesk:BKL-005 | — | ❌ Q-### |
```

## Outputs
| Artifact | Notes |
|----------|-------|
| `portfolio/sprints/sprint-<PS-NN>-<date>.md` | Owner column = `PERSON-###`; *Skills needed* column; coverage matrix section. |
| per-project `memory/open-questions.md` | `Q-###` for skill gaps / low-confidence inference. |

## Rules
- **Skill match is a gate, not a tie-breaker.** A hard skill gap (no candidate ≥ 0.5) defers the item — it is not forced onto a misfit owner.
- **Respect the per-person ceiling.** Use `availability − current_load`, never exceed it.
- **Inference is flagged.** Inferred `skills_required` are marked `(inferred)`; low-confidence → `Q-###`.
- **Capability is measured, not assumed.** The coverage matrix is the deliverable for "measuring capability."

## Example
Item `helpdesk:BKL-001` needs `[node, sso]`. PERSON-004 (backend) has `[node, postgres, sso]` → overlap 1.0; residual capacity 50%. Recommended owner **PERSON-004**. Item `helpdesk:BKL-005` needs `[mobile]`; no active PERSON has `mobile` → raise `Q-###`, defer to carry-forward. Coverage matrix shows `mobile ❌`.
