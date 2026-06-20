# Step 1 — Profile Onboarding

> Part of [Profile Management](README.md).

## Purpose
Add a new build-team member as a `PERSON-###` to `portfolio/profiles/team.md`, with provenance.

## Inputs
- An HR/hiring source (roster entry, hiring record) naming the person + role.
- Existing `portfolio/profiles/team.md`.

## Procedure
1. **Reconcile first.** Search `team.md` for an existing PERSON by name/email. If found, run [Maintenance](profile-maintenance.md) instead (do not duplicate).
2. **Assign the next `PERSON-###`** (increment `counter`).
3. **Fill frontmatter:** name, role, skills (kebab slugs), level, availability %, `current_load: 0`, home_project (if known), contact, `status: active`, `source: [<HR record>]`, created/updated (today).
4. **Add the item** under `## Persons`, plus a one-line note (primary stack, constraints).
5. **Bump `counter`** and add a changelog row.
6. **Report** the new `PERSON-###`.

## Rules
- **Provenance required** — cite the HR/hiring source. No uncited persona.
- **Reconcile before add** — never duplicate a person.
- **`skills` are slugs** from the suggested vocabulary (free-form, not enforced).

## Example
Onboard "Ravi" (senior backend, [node, postgres], 100%, home `helpdesk`) from `SRC-HR-2026-06-01`. Reconcile: no match → assign `PERSON-004`, `counter` 3→4.
