# Architecture

This document describes how `project-agent-framework` is structured: the layered architecture, the multi-project isolation model, the capability model, the agent-integration model, and the extensibility seams. It is oriented to architects and maintainers.

For the conceptual model behind the layers, see [`concepts.md`](concepts.md).

---

## 1. Architectural style

PAF follows a **document-as-database, convention-over-code** style:

- **No application code.** There is no runtime. The framework is a set of *conventions, templates, and workflow specifications* expressed in Markdown.
- **Filesystem-as-database.** Projects are directories; queries are file reads; transactions are file writes; isolation is directory separation.
- **Markdown-as-contract.** Structured Markdown with YAML frontmatter is the typed interface between humans and agents. Templates (`templates/`) are the schemas.
- **Agent-as-runtime.** The "engine" that executes capabilities is whatever LLM agent the user chooses. The framework is agent-agnostic by construction.

```
┌──────────────────────────────────────────────────────────┐
│                    AGENT LAYER                            │   ← Claude Code, Gemini CLI, Copilot…
│   (reads AGENTS.md, executes capabilities, edits files)   │
└──────────────────────────────────────────────────────────┘
                          │  read / write files
                          ▼
┌──────────────────────────────────────────────────────────┐
│                CAPABILITY LAYER                           │
│   capabilities/<name>/  — workflow specifications         │
└──────────────────────────────────────────────────────────┘
                          │  operate on
                          ▼
┌─────────────────────┐  ┌─────────────────┐  ┌────────────┐
│  PROJECT INSTANCE   │  │  PROJECT INST.  │  │  …more…    │
│  (one directory)    │  │                 │  │            │
│  source/knowledge/  │  │  …same shape…   │  │            │
│  memory/outputs/    │  │                 │  │            │
└─────────────────────┘  └─────────────────┘  └────────────┘
          ▲
          │  derived from
┌──────────────────────────────────────────────────────────┐
│                  TEMPLATE LAYER                           │
│   templates/ — the reusable schema for every doc type     │
└──────────────────────────────────────────────────────────┘
```

---

## 2. The layers of the framework itself

Note: these are the *framework's* layers (the repo structure), distinct from the *project's* conceptual layers (Source/Knowledge/Memory/Capabilities).

### Template layer (`templates/`)
The **schema**. Defines the canonical shape of every document type across all projects. Templates are read-only in normal use; they evolve only when the framework's conventions change. See §6.

### Capability layer (`capabilities/`)
The **procedures**. Each capability is a self-contained workflow spec: inputs, steps, outputs, rules. A capability is *how* information moves between a project's Source/Knowledge/Memory. See §5.

### Project instances (`projects/`, `sample-project/`)
The **data**. Each project is an independent directory mirroring the conceptual layer structure. `projects/` holds real projects; `sample-project/` is a populated fictional reference. See §3–§4.

### Agent contract (`AGENTS.md`)
The **operating manual**. The single document every agent reads to learn the rules of the road. See §7.

### Documentation (`docs/`, `README.md`)
The **rationale**. Why the framework is shaped this way, and where it is going.

---

## 3. The project anatomy

Every project — real or sample — has the same anatomy. This uniformity is what makes a single set of templates and capabilities work across all projects and domains.

```
projects/<project-slug>/
├── project.md                # Manifest: identity, domain, status, contacts, changelog
├── source/                   # SOURCE — immutable raw inputs
│   ├── fsd/
│   ├── brd/
│   ├── sop/
│   └── meetings/             # YYYY-MM-DD-<slug>.md
├── knowledge/                # KNOWLEDGE — curated, stable
│   ├── project-overview.md
│   ├── actors.md
│   ├── modules.md
│   ├── features.md
│   ├── business-rules.md
│   ├── glossary.md
│   └── scope.md
├── memory/                   # MEMORY — living, cited
│   ├── requirements.md       # REQ-###
│   ├── decisions.md          # DEC-###
│   ├── action-items.md       # ACT-###
│   ├── open-questions.md     # Q-###
│   ├── risks.md              # RSK-###
│   └── backlog.md            # BKL-###
└── outputs/                  # CAPABILITY OUTPUTS — regenerable
    ├── meetings/             # *-mom.md
    └── reports/              # <topic>-<date>.md
```

### The project manifest (`project.md`)
Every project starts with a manifest declaring its identity. This is what an agent reads first to orient itself. It is also the primary output of **Project Onboarding** (the first step of Meeting Intelligence).

The manifest carries: project name, slug, domain, status, owning team, key contacts (mapped to Actors), creation date, a one-paragraph description, and a changelog.

---

## 4. Multi-project isolation

The framework is explicitly designed to hold **many projects at once**, each fully isolated.

### Isolation by directory
Each project is a self-contained subtree under `projects/`. A project's Source, Knowledge, Memory, and Outputs never reference another project's files. This is enforced by **convention** (in `AGENTS.md`) and by the directory structure itself.

```
projects/
├── helpdesk/       # e.g. an IT helpdesk / support system
│   ├── project.md
│   ├── source/  knowledge/  memory/  outputs/
├── hris/           # e.g. a human resources system
│   ├── project.md
│   ├── source/  knowledge/  memory/  outputs/
├── inventory/      # e.g. a warehouse/inventory system
│   └── …
└── crm/            # e.g. a customer relationship system
    └── …
```

### What isolation guarantees
- **Independent IDs.** `REQ-014` in `hris` and `REQ-014` in `crm` are unrelated. IDs are scoped per-project.
- **Independent memory.** A decision in one project never affects another.
- **Independent lifecycles.** Projects can be at different maturity (one onboarding, one reporting) without interference.
- **Safe parallel agents.** Different agents (or the same agent in separate sessions) can work on different projects concurrently without write conflicts.

### What is shared (the framework)
Across all projects, the *same* templates, *same* capabilities, *same* agent contract, and *same* ID conventions apply. This is the point of a *framework*: uniform machinery, isolated data.

### Cross-project concerns (future)
Some legitimate cross-project needs are *out of scope* for the initial release but designed for:
- **A shared glossary** for organization-wide terms (could live at `projects/_shared/glossary.md`).
- **Portfolio reporting** across projects (a future Reporting capability reading each project's manifest).
These are noted in [`roadmap.md`](roadmap.md); they will be added without disturbing per-project isolation.

---

## 5. The capability model

A capability is a **repeatable workflow** over a project's layers. The framework specifies capabilities as Markdown so any agent can execute them.

### Anatomy of a capability
```
capabilities/<capability-slug>/
├── README.md              # Overview: purpose, inputs, outputs, full step list, examples
└── <step-slug>.md         # One file per step (or sub-capability)
```

Each step spec declares:
- **Inputs** — which Source/Knowledge/Memory files it reads.
- **Outputs** — which Output/Knowledge/Memory files it writes, and how (new item vs. update).
- **Rules** — the constraints it must honor (provenance, dedup, ID conventions, guardrails).
- **Examples** — a worked before/after.

### Capability execution contract
For any agent running a capability:
1. Read the capability `README.md` and the step spec(s).
2. Read the declared inputs from the *target project*.
3. Execute steps in order, honoring `AGENTS.md`.
4. Write declared outputs to the target project.
5. Report created/updated/flagged items.

### The capability roadmap
Only **Meeting Intelligence** is specified now. It is itself a *family* of sub-workflows:

```
Meeting Intelligence
├── Project Onboarding        # bootstrap a new project's Knowledge/Memory from first docs
├── Meeting Analysis          # structure a raw transcript
├── MOM Generation            # produce Minutes of Meeting
├── Requirement Extraction    # source → memory/requirements.md
├── Decision Extraction       # source → memory/decisions.md
├── Action Item Extraction    # source → memory/action-items.md
└── Open Question Extraction  # source → memory/open-questions.md
```

See `capabilities/meeting-intelligence/README.md`.

### Extensibility: adding a new capability
To add (say) *Requirements Management*:
1. Create `capabilities/requirements-management/README.md` defining the workflow.
2. Add step specs for each sub-workflow (trace, drift detection, prioritization, …).
3. Add any new *output* templates needed under `templates/outputs/`.
4. Register it in `README.md` and `docs/roadmap.md`.

**No existing capability or project needs to change.** That is the extensibility guarantee.

---

## 6. The template model (the schema)

Templates are the framework's type system. Each template defines the canonical structure for one document type, so projects stay consistent and capabilities can rely on predictable shapes.

### Template categories
```
templates/
├── source/      # FSD, BRD, SOP, meeting-notes     (input shapes)
├── knowledge/   # overview, actors, modules, …      (knowledge shapes)
├── memory/      # requirements, decisions, …        (memory item shapes + frontmatter)
└── outputs/     # MOM, report                        (generated-artifact shapes)
```

### How templates encode structure
- **YAML frontmatter** carries machine-relevant metadata (IDs, status, dates, provenance, links).
- **Markdown sections** carry human-relevant content.
- **Inline guidance** (comments/placeholders) tells the agent what to fill in.

This dual structure (frontmatter for agents, prose for humans) is the reason Markdown-with-frontmatter is the contract rather than JSON or YAML alone: it is fully readable by both.

### Evolving templates
Templates are versioned by the framework, not by projects. When a template changes, projects adopt the new shape on their next capability run (agents migrate frontmatter fields). Breaking changes to conventions are recorded in this repo's history and called out in `roadmap.md`.

---

## 7. Agent integration model

PAF is built to be operated by **any** file-capable LLM agent. Integration is *by convention*, not by SDK.

### The universal entry point: `AGENTS.md`
`AGENTS.md` defines where things live, the ID conventions, the frontmatter contract, the editing disciplines per layer, and the guardrails. **It is the single source of truth for agent behavior.**

### Tool-specific mapping
| Agent | Native entry file | Mapping |
|-------|-------------------|---------|
| Claude Code | `AGENTS.md` (+ `CLAUDE.md`) | Read natively. Optionally add a `CLAUDE.md` that says "follow AGENTS.md". |
| Gemini CLI | `GEMINI.md` | Mirror or symlink `AGENTS.md` → `GEMINI.md`. |
| GitHub Copilot | `.github/copilot-instructions.md` | Mirror the relevant subset, pointing back to `AGENTS.md`. |
| Cursor / Windsurf | `.cursorrules` / `.windsurfrules` | Mirror as needed. |
| Any other | `AGENTS.md` | Read it. It is tool-neutral. |

The design rule: **other entry files reference `AGENTS.md`; they do not diverge.** This guarantees all agents follow identical rules.

### Why agent-agnostic works
Because the framework has:
- **No SDK calls** — agents just read/write files.
- **No hidden state** — everything is on disk.
- **Declared I/O** — capabilities say exactly what they read and write.
- **Tool-neutral specs** — capability steps are prose instructions, not API calls.

An agent's only required capabilities are: read file, write file, search files, and follow Markdown instructions — which every modern coding agent has.

### Operational guidance
- **One project per task.** Agents should resolve the target project from the user's request and confine all writes to it (per §4 isolation and `AGENTS.md` §7).
- **Human-in-the-loop on high-stakes memory.** Decisions, priority changes, and scope changes are flagged for confirmation.
- **Outputs are regenerable; memory is not.** Agents may freely overwrite `outputs/`, but must *reconcile* (not overwrite) `memory/`.

---

## 8. Extensibility seams

PAF is designed to grow along three axes without restructuring.

### Axis 1 — More projects
Add a directory under `projects/`. Nothing else changes. Isolation is automatic.

### Axis 2 — More capabilities
Add a directory under `capabilities/` with a `README.md` and step specs. Register in docs. Existing projects can adopt it immediately. See §5.

### Axis 3 — More knowledge/memory types
Add a template under `templates/knowledge/` or `templates/memory/` and a corresponding file convention in `AGENTS.md`. For example, `memory/assumptions.md` (`ASM-###`) — added in Phase 2 — plugged in without touching the rest.

### Non-axes (intentionally out of scope)
- **Not** code, runtimes, or build tooling.
- **Not** databases or vector stores.
- **Not** HTTP APIs.
These are deliberately excluded to keep the framework portable and agent-agnostic. If a future deployment wants a database or API, it would be built *on top of* this Markdown core (treating the files as the source of truth), never *instead of* it.

---

## 9. Design properties (and how they are achieved)

| Property | How it is achieved |
|----------|--------------------|
| **Portability** | Markdown-only; no proprietary format; filesystem-as-database. |
| **Agent-agnostic** | `AGENTS.md` as universal contract; tool entry files mirror, not diverge. |
| **Multi-project** | Directory isolation; per-project ID scopes; shared templates/capabilities. |
| **Trustworthiness** | Mandatory provenance; immutable Source; never-delete memory. |
| **Coherence over time** | Reconcile-before-add; supersede-not-delete; cross-linking. |
| **Extensibility** | Three independent axes (projects, capabilities, types); templates-as-schema. |
| **Maintainability** | Small, single-purpose Markdown files; explicit I/O per capability; uniform anatomy. |
| **Auditability** | Every memory item cites a Source; every Knowledge change has a changelog; outputs are regenerable. |

---

## 10. Summary

PAF is a **convention framework**, not a software product. Its "architecture" is:

- A **four-layer conceptual model** (Source/Knowledge/Memory/Capabilities) per project.
- A **uniform project anatomy** enabling isolation and reuse.
- A **template layer** acting as the schema.
- A **capability layer** acting as the procedures.
- An **agent contract** (`AGENTS.md`) acting as the universal operating manual.

Together these let any LLM agent act as a disciplined project manager across any number of projects — today via Meeting Intelligence, and tomorrow via the capabilities on the roadmap.
