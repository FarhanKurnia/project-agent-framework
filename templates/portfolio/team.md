# Portfolio Profile — Team (Template)

> Copy into `portfolio/profiles/team.md` (the org-wide build-team roster). **Gitignored** — it holds real people data.
> Each person is a `PERSON-###`; optional squads are `TEAM-###`. Distinct from per-project `ACTOR-###` (system *users* of a product) — `PERSON-###` are the people who *build* across projects.

---
doc_type: portfolio-profile
profile_type: team
org: <org name>
last_reviewed: <YYYY-MM-DD>
counter: 0
---

# Team Profiles — <Org>

> One `PERSON-###` per build-team human. Reconcile before add; supersede (`status: alumni`), never delete. Source provenance is required (HR roster / hiring record). Maintain via [Profile Management](../../capabilities/profile-management/README.md).

## Suggested skill vocabulary (free-form kebab slugs — not enforced)
`frontend backend fullstack react vue node python java php laravel mobile qa qa-automation devops dba postgres mysql ux ui ba sa pm`

## Persons

<!-- TEMPLATE FOR A NEW PERSON:
### PERSON-001 — <Display Name>

---
id: PERSON-001
name: <Display Name>
kind: person                      # person | team
role: <e.g. Senior Frontend Engineer>
skills: [react, typescript, css]  # free-form kebab slugs (see vocabulary above)
level: junior | mid | senior | lead
availability: 100                 # % available this cycle
current_load: 0                   # % committed to in-flight portfolio sprints (agent-maintained — see load-reconciliation)
home_project: <slug or null>      # primary project, if any
contact: <handle or email>
status: active                    # active | part-time | unavailable | alumni
source: [SRC-HR-…]               # provenance — REQUIRED (HR roster / hiring record)
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---

- Primary stack: <…>
- Notes: <interests, constraints, timezone>.
-->

## Teams (optional squads)
<!-- TEMPLATE FOR A NEW TEAM:
### TEAM-01 — <squad name>

---
id: TEAM-01
name: <squad name>
kind: team
lead: PERSON-###
members: [PERSON-###]
skills: [react, node]        # union of member skills
availability: 200            # sum of member availability %
source: [SRC-…]
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---
-->

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | <name> | Created file (counter=0). | Profile Management onboarding. |
