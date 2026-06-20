---
description: Profile management — onboard / update / reconcile-load for the build-team roster (PERSON-###)
argument-hint: "add | update | load  [details]"
---

# /profile — Profile Management

Maintain the build-team roster at `portfolio/profiles/team.md` (`PERSON-###`). **Propose before writing** — show the change, ask before saving.

## 1. Resolve subcommand
- `$CMD` = first token of `$ARGUMENTS`: `add` | `update` | `load`. If empty, ask the user.

## 2. Read capability and sources
- Read `capabilities/profile-management/`: the relevant step (`profile-onboarding.md` / `profile-maintenance.md` / `load-reconciliation.md`). Plus `AGENTS.md` and `templates/portfolio/team.md`.
- Read `portfolio/profiles/team.md` (the roster). For `load`, also read `portfolio/sprints/*` at `status: committed`.

## 3. Execute (propose, then write)
- **`add <name> <role> [skills] [avail%] [home:<slug>]`** — reconcile by name/email; assign the next `PERSON-###`; **require a `source:`** (HR/hiring record). Propose the new item; on OK, write it + bump `counter`.
- **`update <PERSON-###> <field=value …>`** — edit skills/level/availability/contact; or a status transition (`part-time` / `unavailable` / `alumni` / `active`). Propose the diff; on OK, write + bump `updated`.
- **`load`** — recompute `current_load` for every PERSON from in-flight committed portfolio sprints; flag any > 100% (raise `Q-###`). Propose; on OK, write back.

## 4. Guardrails
- Follow `AGENTS.md`. Provenance required for any new PERSON. Reconcile before add (no duplicates). Supersede (`alumni`), never delete.
- `PERSON-###` ≠ `ACTOR-###`. `current_load` is derived (set only via `load`), never hand-guessed.
- `portfolio/profiles/team.md` is gitignored/private — do not commit/push.

## 5. Report briefly
- New/updated `PERSON-###`, the change, and (for `load`) per-person `current_load` + any overload flags.
