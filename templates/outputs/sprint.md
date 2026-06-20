# Output — Sprint (Template)

> Generated into `projects/<project>/outputs/sprints/sprint-<n>-<YYYY-MM-DD>.md`.
> Produced by the [Sprint Planning](../../capabilities/sprint-planning/README.md) capability. **Lifecycle artifact**: it grows from `proposed` → `committed` → `closed`.

---
doc_type: output
output_type: sprint
project: <project-slug>
sprint_id: <S-NN>                       # e.g. S-01
window_start: <YYYY-MM-DD>
window_end: <YYYY-MM-DD>
goal: <one-sentence sprint outcome>
status: proposed                        # proposed | committed | closed
capacity_budget: <points or ideal-days>
actual_velocity:                        # filled at review
generated_by: sprint-planning
generated_at: <YYYY-MM-DD>
---

# Sprint <S-NN> — <Project Name>

## Sprint Goal
<One sentence: the outcome this sprint delivers. Tie to a phase goal in knowledge/scope.md.>

## Capacity
| Contributor | Availability | Working days | Notes |
|-------------|--------------|--------------|-------|
| <ACTOR-###> | 100% | <n> | |
| <ACTOR-###> | 50% | <n> | part-time |

- **Window:** <start> → <end> (<n> working days)
- **Deductions:** holidays/absences = <n>
- **Focus factor:** <e.g. 25%>
- **Budget:** <points or ideal-days>
- **Assumptions:** [ASM-###]

## Proposed Scope  *(filled at Sprint Proposal — status: proposed)*
| BKL | Title | Size | Priority | Dependencies | Owner (tentative) |
|-----|-------|------|----------|--------------|-------------------|
| BKL-### | <…> | M | high | — | ACTOR-### |

### Carry-forward candidates (next sprint)
- BKL-### — <why it didn't fit>

### Excluded (with reason)
- BKL-### — blocked by BKL-### / not ready / low priority

---

## Committed Scope  *(filled at Sprint Commitment — status: committed)*
| BKL | Title | Size | Owner | Dependencies |
|-----|-------|------|-------|--------------|
| BKL-### | <…> | M | ACTOR-### | — |

**Committed on:** <YYYY-MM-DD>
**Capacity utilization:** <points committed / budget>

---

## Review  *(filled at Sprint Review Prep — status: closed)*

### Completed vs Planned
| BKL | Status | Evidence / Note |
|-----|--------|-----------------|
| BKL-### | done | <delivered feature / completed action> |
| BKL-### | partial | <reason> |

### Carry-overs (to next sprint)
- BKL-### — <reason>

### Actual velocity
<points completed> (vs <budget> planned)

### Emergent items this sprint
- Risks: RSK-### — <…>
- Decisions: DEC-### — <…>
- Open questions: Q-### — <…>

**Closed on:** <YYYY-MM-DD>

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | agent | Proposed. | Sprint Proposal. |
| <YYYY-MM-DD> | agent | Committed. | Human approval. |
| <YYYY-MM-DD> | agent | Closed (review). | Sprint Review Prep. |

---
*Produced by Sprint Planning. The file evolves through the sprint lifecycle; do not delete — transition status.*
