---
doc_type: portfolio-manifest
org: <generic org name>            # e.g. "Acme" — no real company in this committed file
cadence: biweekly                  # sprint cadence
sprint_counter: 0                  # monotonic source of PS-NN
contributors_ref: portfolio/profiles/team.md   # Phase B: build-team roster (not yet active)
last_reviewed: <YYYY-MM-DD>
---

# Portfolio Manifest

> The portfolio layer sits **above** the project instances. A portfolio sprint (`PS-NN`) spans multiple `projects/<slug>/`. Read [`../AGENTS.md`](../AGENTS.md) §2 ("where things live") and §7 (the write-back carve-out) before writing here.

## Organization
- **Org:** <generic org name>
- **Cadence:** biweekly (Mon start). The window is recorded per sprint artifact.

## In-scope projects
> Populated at run time from each `projects/<slug>/project.md`. List the slugs a portfolio sprint may draw from.

- `<slug>` — <one-line domain/purpose>

## Sprint counter
- `sprint_counter: 0` — increment when a new `PS-NN` is proposed. This counter is the source of the next `PS-NN` (portfolio sprint IDs are org-wide, never reused).

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | agent | Created manifest. | Portfolio layer (Phase A). |
