# sample-portfolio/

> ⚠️ **Fictional sample.** A worked example of the [`portfolio/`](../portfolio/) layer and [Portfolio Sprint Planning](../capabilities/portfolio-sprint-planning/README.md). Generic, English, shareable — no real data.

This sample demonstrates a **cross-project sprint** (`PS-01`) that pulls backlog items from two fictional projects and commits them in one time-boxed sprint.

## Contents

```
sample-portfolio/
├── manifest.md                              # portfolio manifest (Acme, biweekly)
├── projects/
│   ├── sample-helpdesk/                     # fictional IT helpdesk
│   │   ├── project.md
│   │   └── memory/backlog.md               # BKL-001 (committed to PS-01), BKL-002 (ready)
│   └── sample-intranet/                     # fictional company intranet
│       ├── project.md
│       └── memory/backlog.md               # BKL-001 (committed to PS-01), BKL-002 (new, excluded)
└── sprints/
    └── sprint-PS-01-2026-07-06.md          # committed cross-project sprint
```

> The two projects here are **intentionally minimal stubs** (manifest + backlog only) so the portfolio concept reads clearly. A real project has the full anatomy (`source/ knowledge/ memory/ outputs/`) — see [`../sample-project/`](../sample-project/).

## How to read it

1. [`manifest.md`](manifest.md) — the portfolio identity and in-scope projects.
2. Each `projects/<slug>/memory/backlog.md` — note `BKL-001` carries `sprint: PS-01`, `status: in-progress` (written by the portfolio commitment carve-out).
3. [`sprints/sprint-PS-01-2026-07-06.md`](sprints/sprint-PS-01-2026-07-06.md) — the committed sprint referencing both projects by `<slug>:BKL-###`, with the write-back noted.

This is the **bidirectional integrity** the portfolio layer guarantees: every committed-scope row ⇔ a backlog entry.
