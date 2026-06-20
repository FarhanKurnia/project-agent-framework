# project-agent-framework

> A reusable, **markdown-native** AI Project Management Framework.
> Not a project-specific assistant — a *framework* that can be applied across many projects and domains.

`project-agent-framework` (PAF) turns a pile of project documents into **structured, queryable, evolving project knowledge** that any LLM coding agent can read and update. It is deliberately built **without code, databases, or APIs**: the file system *is* the database, and structured Markdown *is* the contract between humans and AI.

It is designed to be operated by any modern agent — **Claude Code, Gemini CLI, GitHub Copilot Chat**, or any other tool that can read and write files.

---

## The core idea

Every project is understood through four layers that flow into one another:

```
 Source ──▶ Knowledge ──▶ Memory ──▶ Capabilities
   │            │             │             │
   │            │             │             └─ AI workflows that read & write the above
   │            │             └─ Living info that evolves: requirements, decisions, action items…
   │            └─ Structured knowledge extracted from sources: actors, modules, features…
   └─ Raw documents: FSD, BRD, SOP, meeting notes
```

| Layer | What it is | Examples |
|-------|------------|----------|
| **Source** | Raw project documents as-authored | FSD, BRD, SOP, meeting notes, transcripts |
| **Knowledge** | Structured, stable facts extracted from sources | Project Overview, Actors, Modules, Features, Business Rules, Glossary, Scope |
| **Memory** | Living information that evolves over time | Requirements, Decisions, Action Items, Open Questions, Risks, Backlog |
| **Capabilities** | AI workflows that operate on the layers above | Meeting Intelligence, Requirements Management, Backlog Management, Sprint Planning, Reporting |

- **Source** is *immutable* — a record of what was said or written.
- **Knowledge** is *curated* — the distilled, agreed picture of the project.
- **Memory** is *mutable* — it changes every time a meeting happens or a decision is made.
- **Capabilities** are *procedures* — repeatable AI workflows that move information between the layers.

See [`docs/concepts.md`](docs/concepts.md) for the full model.

---

## Why this exists

Project knowledge lives scattered across chat threads, inboxes, slide decks, and heads. By the time it is needed it is half-remembered and contradictory. PAF gives an LLM agent a **predictable, structured place** to:

- **Ingest** a meeting transcript and produce a Minutes of Meeting (MOM).
- **Extract** requirements, decisions, action items, and open questions from that meeting.
- **Reconcile** new information against what is already known.
- **Answer** project questions from a single source of truth.

Because it is just Markdown, the same knowledge base is readable by humans *and* operable by any agent — no lock-in.

---

## Design principles

1. **Markdown-first.** Structured Markdown (with YAML frontmatter) is the single interface. No proprietary formats, no schemas that require a compiler.
2. **Filesystem-as-database.** Projects are directories; isolation is directory separation. No database, no vector store, no API.
3. **Agent-agnostic.** Any tool that can read/write files can operate the framework. Cross-tool conventions are documented in [`AGENTS.md`](AGENTS.md).
4. **Provenance over memory.** Every living item traces back to a Source. Nothing exists in Memory without a citation.
5. **Extensible by design.** New capabilities, knowledge types, and projects are added by *creating files*, not by changing code.
6. **Templates are schemas.** The shape of every document type is defined once in `templates/` and reused across projects.

---

## Repository structure

```
project-agent-framework/
├── README.md                      # You are here
├── AGENTS.md                      # Operating conventions for any LLM agent
├── docs/
│   ├── concepts.md                # The Source → Knowledge → Memory → Capabilities model
│   ├── architecture.md            # Layered architecture, multi-project isolation, agent integration
│   └── roadmap.md                 # Phased capability roadmap
├── templates/                     # Reusable document templates (the "schema")
│   ├── source/                    #   FSD, BRD, SOP, meeting-notes
│   ├── knowledge/                 #   overview, actors, modules, features, business-rules, glossary, scope
│   ├── memory/                    #   requirements, decisions, action-items, open-questions, risks, backlog
│   └── outputs/                   #   MOM, reports
├── capabilities/                  # AI workflow definitions
│   ├── meeting-intelligence/      #   FSD-first onboarding, analysis, MOM, extraction
│   ├── requirements-management/   #   refinement, categorization, traceability, drift, coverage
│   ├── backlog-management/        #   generation, prioritization, estimation, dependencies, grooming
│   └── sprint-planning/           #   capacity, proposal, commitment, review
├── projects/                      # Where real project instances live (one dir per project)
│   └── README.md                  #   multi-project conventions
└── sample-project/                # A fully-populated fictional reference project
    ├── project.md
    ├── source/
    ├── knowledge/
    ├── memory/
    └── outputs/
```

---

## Quick start

### 1. Create a new project

A project is just a directory under `projects/` that mirrors the layer structure:

```
projects/<your-project>/
├── project.md          # Project manifest (name, domain, status, contacts)
├── source/             # Drop raw documents here
├── knowledge/          # Structured knowledge (agent fills this)
├── memory/             # Living memory (agent updates this)
└── outputs/            # Generated artifacts (MOMs, reports, plans)
```

Copy `templates/` into the new project as a starting point, then edit. The `sample-project/` directory shows a completed example.

### 2. Point an agent at it

Open this repository in **Claude Code**, **Gemini CLI**, or **Copilot**, and ask, for example:

> *"Read `AGENTS.md`. Then process the meeting transcript in `projects/hris/source/meetings/2026-06-15-standup.md` using the Meeting Intelligence capability, generate a MOM, and extract any new requirements, decisions, and action items into memory."*

The agent follows the conventions in [`AGENTS.md`](AGENTS.md) and the workflow in [`capabilities/meeting-intelligence/`](capabilities/meeting-intelligence/).

### 3. Iterate

Memory evolves. The next meeting's analysis reconciles against existing memory rather than duplicating it. Open questions get closed. Decisions supersede earlier ones. The framework stays coherent because every change is a tracked Markdown edit.

---

## Current status

| Capability | Status |
|------------|--------|
| **Meeting Intelligence** | 🟦 Specified (FSD-first onboarding → analysis → MOM → extraction) |
| **Requirements Management** | 🟦 Specified (refinement → categorization → traceability → drift → coverage) |
| **Backlog Management** | 🟦 Specified (generation → prioritization → estimation → dependencies → grooming) |
| **Sprint Planning** | 🟦 Specified (capacity → proposal → commitment → review) |
| Reporting | ⬜ Planned |

Only the **Meeting Intelligence** capability is specified in this initial release. See [`docs/roadmap.md`](docs/roadmap.md).

---

## What this is *not*

- ❌ Not an application — there is no runtime, no server, no CLI binary.
- ❌ Not a database — no SQL, no vector store.
- ❌ Not an API — nothing to call over HTTP.
- ❌ Not a single-project tool — it is a *framework* for many projects.

It is a **convention and a set of templates and workflow specifications** that make LLM agents effective project managers.

---

## Documentation

- **[docs/concepts.md](docs/concepts.md)** — the four-layer mental model in depth.
- **[docs/architecture.md](docs/architecture.md)** — how the layers, projects, and agents fit together.
- **[docs/roadmap.md](docs/roadmap.md)** — what is built now and what comes next.
- **[AGENTS.md](AGENTS.md)** — how any LLM agent should read and write this framework.

## License

Structure and documentation only. Adopt and adapt freely within your organization.
