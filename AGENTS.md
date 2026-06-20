# AGENTS.md

> Operating conventions for any LLM coding agent working inside `project-agent-framework`.
> This file is the cross-tool entry point: **Claude Code** (`AGENTS.md`), **Gemini CLI** (`GEMINI.md` → symlink or mirror this), **GitHub Copilot** (`github copilot` extensions), and any future agent all read this same document.

If you are an agent that has been pointed at this repository, **read this file first**. It defines the rules of the road: where things live, what the layers mean, how to edit memory safely, and what you must never do.

---

## 1. The mental model (read this before doing anything)

Every project is four layers. Information flows **left to right** and is enriched at each step.

```
Source ──▶ Knowledge ──▶ Memory ──▶ (consumed by) Capabilities
```

- **Source** = raw docs, as-authored. **Never modify.** Append-only.
- **Knowledge** = stable, curated facts. Edit **deliberately**, with a reason.
- **Memory** = living items (requirements, decisions, action items, …). Edit **freely**, but always cite a Source.
- **Capabilities** = workflows (defined in `capabilities/`) that you execute to move information between layers.

Full definitions: [`docs/concepts.md`](docs/concepts.md).

---

## 2. Where things live

```
projects/<project-slug>/
├── project.md                # Manifest — read this to understand the project
├── source/                   # Raw inputs (immutable)
│   ├── fsd/
│   ├── brd/
│   ├── sop/
│   └── meetings/             # meeting notes / transcripts (input to Meeting Intelligence)
├── knowledge/                # Structured knowledge
├── memory/                   # Living memory
└── outputs/                  # Generated artifacts (MOMs, reports) — overwritable
```

- **You operate on ONE project at a time.** Identify it from the user's request or the file paths involved. Never cross-write between projects.
- **`templates/` is read-only.** It defines document shapes. Copy *from* it into a project; never edit the templates themselves unless asked to evolve the framework.
- **`sample-project/` is read-only reference.** Do not mutate it as a side effect of a real task.
- **`capabilities/`** defines workflows as Markdown specs. Treat each spec as a procedure to follow.

---

## 3. Naming conventions (obey these exactly)

Consistent IDs are how items cross-reference and deduplicate.

### Memory item IDs
| Type | Prefix | Example |
|------|--------|---------|
| Requirement | `REQ` | `REQ-014` |
| Decision | `DEC` | `DEC-007` |
| Action Item | `ACT` | `ACT-023` |
| Open Question | `Q` | `Q-005` |
| Risk | `RSK` | `RSK-002` |
| Backlog item | `BKL` | `BKL-011` |
| Assumption | `ASM` | `ASM-003` |

- IDs are **zero-padded to 3 digits**, **monotonic**, and **never reused**. Superseded items keep their ID and gain `status: superseded`.
- Within a project, each memory file owns its own counter.

### Knowledge entity IDs
| Type | Prefix | Example |
|------|--------|---------|
| Actor | `ACTOR` | `ACTOR-004` |
| Module | `MOD` | `MOD-003` |
| Feature | `FEAT` | `FEAT-012` |
| Business Rule | `BR` | `BR-006` |
| Glossary term | *(by slug)* | `sso`, `mom` |

### Source documents
Named by convention, dated for meetings:
```
source/fsd/fsd-v1.2.md
source/brd/brd-2026-q1.md
source/sop/sop-onboarding.md
source/meetings/YYYY-MM-DD-<slug>.md        # e.g. 2026-06-15-standup.md
```

### Outputs
```
outputs/meetings/YYYY-MM-DD-<slug>-mom.md
outputs/reports/<topic>-<YYYY-MM-DD>.md
```

---

## 4. The frontmatter contract

Every **memory** and **knowledge** document starts with YAML frontmatter. Every **item** in a memory file carries its own frontmatter block. Example memory item:

```markdown
### REQ-014 — Single sign-on for employee portal

---
id: REQ-014
title: Single sign-on for employee portal
status: proposed          # proposed | accepted | superseded | rejected
priority: high            # low | medium | high | critical
source: [SRC-MTG-2026-06-15]   # provenance — REQUIRED
owners: [alice@acme]
tags: [auth, security]
created: 2026-06-15
updated: 2026-06-15
supersedes: []            # IDs this replaces
relates_to: [DEC-003, ACT-023]
---

The employee portal shall support SSO via the corporate identity provider…
```

**Rules:**
- `source` (provenance) is **required** for any new memory item. Cite the meeting, doc, or decision that produced it. No uncited memory.
- `status` drives the lifecycle. When you resolve an open question, set its `status: closed` and add `resolution:` in the body.
- `updated` changes on every edit. `created` never does.
- `relates_to` / `supersedes` keep the graph connected. Use real IDs.

---

## 5. How to edit each layer

### Source — never edit
- Source documents are **append-only and immutable**.
- If a source is wrong, add a correction document; do not rewrite history.
- You *read* source to extract knowledge/memory. You *write* new source only when a human hands you a new raw document to file.

### Knowledge — edit deliberately
- Knowledge changes slowly. When you update it, state *why* in the document's changelog section.
- Prefer to **enrich** (add detail, add a new actor/module) over **rewrite**.
- Keep the glossary authoritative: if you coin or standardize a term, add it once to `knowledge/glossary.md` and link to it elsewhere.

### Memory — edit freely, with discipline
- **Extract → reconcile → write.** Before adding a new item, search existing memory for a near-match. If one exists, *update* it (and bump `updated`) instead of creating a duplicate.
- **Deduplicate aggressively.** Two action items that describe the same task are one action item.
- **Never delete an item.** Set `status: superseded` / `rejected` / `closed`. History matters.
- When a decision supersedes an earlier one, link both via `supersedes` / `superseded_by`.

### Outputs — overwritable
- MOMs and reports are *regenerable*. You may overwrite them when re-running a capability.
- Keep them dated so prior versions remain in git history.

---

## 6. How to run a capability

Capabilities live in `capabilities/<name>/`. Each has a `README.md` describing the workflow and one file per step. To run one:

1. **Read** the capability `README.md` and the relevant step spec(s).
2. **Read** the required inputs (e.g., a meeting transcript under `source/`, plus the project's current `knowledge/` and `memory/`).
3. **Execute** the steps **in order**. Each spec tells you its inputs, outputs, and rules.
4. **Write** outputs to the project's `outputs/`, `knowledge/`, and/or `memory/` per the spec — following §3–§5.
5. **Report** what you created, updated, or flagged for human review.

Currently specified: [`capabilities/meeting-intelligence/`](capabilities/meeting-intelligence/).

---

## 7. Guardrails — what you must NOT do

- ❌ **Do not invent sources.** If something is not in a source document, mark it as an *assumption* or raise it as an *open question* — do not silently add it to memory.
- ❌ **Do not cross projects.** A change for `hris` must never touch `crm`.
- ❌ **Do not edit `templates/` or `sample-project/`** as a side effect of a project task.
- ❌ **Do not delete memory items.** Supersede them.
- ❌ **Do not strip provenance.** `source:` stays attached to its item.
- ❌ **Do not create code, databases, APIs, or config** unless explicitly asked. This framework is Markdown-only by design.
- ❌ **Do not change the ID conventions** in §3 ad hoc. They are the integrity guarantee.

---

## 8. When in doubt

1. Prefer **asking the human** over guessing on ambiguous, high-stakes items (a requirement's priority, a decision's scope).
2. Prefer **raising an open question** (`memory/open-questions.md`) over fabricating an answer.
3. Prefer **linking** (`relates_to`) over duplicating.
4. Prefer **small, cited edits** over large unsourced rewrites.

---

## 9. Tool-specific notes

| Agent | Entry file | Note |
|-------|-----------|------|
| **Claude Code** | `AGENTS.md` (this file) | Auto-loaded into context. Also honors `CLAUDE.md`. |
| **Gemini CLI** | `GEMINI.md` | Mirror or symlink this file to `GEMINI.md` at the repo root. |
| **GitHub Copilot** | `.github/copilot-instructions.md` | Mirror the relevant subset of this file there. |
| **Cursor / others** | `.cursorrules` / `.windsurfrules` | Mirror as needed. |

The **single source of truth is this `AGENTS.md`**. Other entry files should point back to it rather than diverge, so all agents follow identical rules.
