# Knowledge — Business Rules (Template)

> Copy into `projects/<project>/knowledge/business-rules.md`.
> **Business rules** are the constraints and policies the system enforces, independent of any one feature.

---
doc_type: knowledge
knowledge_type: business-rules
project: <project-slug>
last_reviewed: <YYYY-MM-DD>
---

# Business Rules — <Project Name>

> Each rule has a `BR-###` ID. Rules constrain features (`FEAT-###`) and often drive requirements (`REQ-###`).
> Categorize: **Policy**, **Constraint**, **Computation**, **Validation**.

## BR-001 — <Rule Name>
- **Category:** <policy | constraint | computation | validation>
- **Statement:** <the rule, stated precisely and testably>
- **Rationale:** <why it exists — link DEC-### if a decision established it>
- **Applies to:** <FEAT-###, MOD-###>
- **Source:** <SRC-…>
- **Exceptions:** <none, or describe>

## BR-002 — <Rule Name>
- … *(copy block per rule)*

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | <name> | Added BR-001. | Onboarding (<SRC-…>). |
