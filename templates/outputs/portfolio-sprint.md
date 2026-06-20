# Output — Portfolio Sprint (Template)

> Generated into `portfolio/sprints/sprint-<PS-NN>-<YYYY-MM-DD>.md`.
> Produced by the [Portfolio Sprint Planning](../../capabilities/portfolio-sprint-planning/README.md) capability. **Lifecycle artifact**: it grows from `proposed` → `committed` → `closed`.
> A portfolio sprint spans **multiple** `projects/<slug>/`. Every backlog reference uses the qualified form `<slug>:BKL-###`.

---
doc_type: output
output_type: portfolio-sprint
sprint_id: <PS-NN>                       # e.g. PS-01 (org-wide; counter in portfolio/manifest.md)
scope_projects: [<project-slug>, ...]    # every project this sprint draws from
contributor_pool: [PERSON-###, ...]      # from portfolio/profiles/team.md
window_start: <YYYY-MM-DD>
window_end: <YYYY-MM-DD>
goal: <one-sentence cross-project outcome>
status: proposed                         # proposed | committed | closed
capacity_budget: <points or ideal-days>
actual_velocity:                         # filled at review
generated_by: portfolio-sprint-planning
generated_at: <YYYY-MM-DD>
---

# Portfolio Sprint <PS-NN> — <Org / theme>

## Sprint Goal
<One sentence: the cross-project outcome this sprint delivers.>

## Capacity
> Pooled across the in-scope projects' contributors (Phase A: free-text roles + time-math; Phase B: `PERSON-###` with a per-person ceiling).

| Contributor (role / project) | Availability | Working days | Notes |
|------------------------------|--------------|--------------|-------|
| <role> @ <slug> | 100% | <n> | |
| <role> @ <slug> | 50% | <n> | part-time |

- **Window:** <start> → <end> (<n> working days)
- **Deductions:** holidays/absences = <n>
- **Focus factor:** <e.g. 25%>
- **Budget:** <points or ideal-days> (estimate if no velocity)
- **Assumptions:** [ASM-###] (per project, where relevant)

## Proposed Scope  *(filled at Sprint Proposal — status: proposed)*
> Refs are **qualified**: `<slug>:BKL-###`. Pull from each in-scope project's `memory/backlog.md` (`ready` items only).

| Ref | Project | Title | Size | Priority | Dependencies | Skills needed | Owner (tentative) |
|-----|---------|-------|------|----------|--------------|---------------|-------------------|
| <slug>:BKL-### | <slug> | <…> | M | high | — | [skill, …] | <PERSON-###> |

### Capability Coverage
> Skills-needed vs skills-available across the proposed set. Gaps raise `Q-###` (item → carry-forward). Produced by [`skill-assignment.md`](../../capabilities/portfolio-sprint-planning/skill-assignment.md).

| Skill needed | Required by | Covered by | Gap? |
|--------------|-------------|------------|------|
| <skill> | <slug>:BKL-### | PERSON-### | ✅ |
| <skill> | <slug>:BKL-### | — | ❌ Q-### |

### Carry-forward candidates (next portfolio sprint)
- <slug>:BKL-### — <why it didn't fit>

### Excluded (with reason)
- <slug>:BKL-### — blocked by <slug>:BKL-### / not ready / low priority

---

## Committed Scope  *(filled at Sprint Commitment — status: committed)*
| Ref | Project | Title | Size | Owner | Dependencies |
|-----|---------|-------|------|-------|--------------|
| <slug>:BKL-### | <slug> | <…> | M | <owner> | — |

**Committed on:** <YYYY-MM-DD>
**Capacity utilization:** <points/days committed / budget>
**Write-back:** for each row, `sprint: <PS-NN>` + `owner:` written to `projects/<slug>/memory/backlog.md` (carve-out, `AGENTS.md` §7).

---

## Review  *(filled at Sprint Review Prep — status: closed)*

### Completed vs Planned
| Ref | Project | Status | Evidence / Note |
|-----|---------|--------|-----------------|
| <slug>:BKL-### | <slug> | done | <…> |

### Carry-overs (to next sprint)
- <slug>:BKL-### — <reason>

### Actual velocity
<points/days completed> (vs <budget> planned)

### Emergent items this sprint
- Risks: RSK-### (@ <slug>) — <…>
- Decisions: DEC-### (@ <slug>) — <…>
- Open questions: Q-### (@ <slug>) — <…>

**Closed on:** <YYYY-MM-DD>

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | agent | Proposed. | Portfolio Sprint Proposal. |
| <YYYY-MM-DD> | agent | Committed. | Human approval. |
| <YYYY-MM-DD> | agent | Closed (review). | Portfolio Sprint Review Prep. |

---
*Produced by Portfolio Sprint Planning. The file evolves through the sprint lifecycle; do not delete — transition status. Backlog items are referenced by qualified `<slug>:BKL-###` and written back via the carve-out in `AGENTS.md` §7.*
