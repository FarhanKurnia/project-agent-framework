# Concepts

This document defines the mental model behind `project-agent-framework`: the four layers of **Source**, **Knowledge**, **Memory**, and **Capabilities**, how they relate, and the rules that keep them coherent.

If you understand only one document, make it this one.

---

## The four-layer model

A project is understood as a flow of information through four layers. Each layer has a different *volatility*, a different *audience*, and a different *editing discipline*.

```
                        ┌─────────────────────────────────────────────┐
                        │              CAPABILITIES                    │
                        │   AI workflows that read & write             │
                        │   the three layers below                     │
                        └─────────────────────────────────────────────┘
                                    ▲             ▲
                                    │             │
   ┌─────────┐    extract    ┌─────────────┐  reconcile  ┌────────┐
   │ SOURCE  │ ────────────▶ │  KNOWLEDGE  │ ──────────▶ │ MEMORY │
   │ (raw)   │               │ (curated)   │             │(living)│
   └─────────┘               └─────────────┘             └────────┘
   immutable                  slow-changing              fast-changing
```

| Layer | Volatility | Discipline | Authority |
|-------|-----------|------------|-----------|
| **Source** | Append-only | Never edit; cite | "What was said/written" |
| **Knowledge** | Slow | Edit with a reason | "What we know the project to be" |
| **Memory** | Fast | Edit freely, always cite | "What we've decided/asked/committed" |
| **Capabilities** | Specified, stable | Follow the workflow | "How we process information" |

---

## 1. Source

### Definition
**Raw project documents, exactly as authored.** Source is the historical record of what people said, wrote, or decided in some original medium.

### Examples
- **FSD** — Functional Specification Document
- **BRD** — Business Requirements Document
- **SOP** — Standard Operating Procedure
- **Meeting notes / transcripts** — the primary input to Meeting Intelligence
- Emails, slide decks, RFCs, interview notes (anything a human files as a source)

### Where it lives
```
projects/<project>/source/
├── fsd/      # functional specs
├── brd/      # business requirements
├── sop/      # standard operating procedures
└── meetings/ # dated meeting notes/transcripts
```

### Rules
- **Immutable.** Source is never edited after it is filed. If it is wrong, add a *correction* document — do not rewrite history.
- **Append-only.** New meetings, new spec versions, new SOPs are *new files*. Versioning is by filename (`fsd-v1.2.md`).
- **Citable.** Every Source is a potential provenance target for Knowledge and Memory. Meeting files follow `YYYY-MM-DD-<slug>.md` so they can be referenced as `SRC-MTG-2026-06-15`.

### Why it matters
Source is the **evidence layer**. The rule *"no uncited memory"* (see Memory) means every living fact in the framework can be traced back to a Source document. This is what makes the framework trustworthy rather than a pile of plausible-sounding AI text.

---

## 2. Knowledge

### Definition
**Structured, curated, relatively stable facts** that describe what the project *is*. Knowledge is the distilled, agreed-upon picture, extracted from Sources and reconciled over time.

### Examples
- **Project Overview** — purpose, goals, context, in-scope/out-of-scope at a glance
- **Actors** — people, teams, systems, and roles that interact with the product
- **Modules** — the functional building blocks of the solution
- **Features** — capabilities the system provides, mapped to modules and actors
- **Business Rules** — the constraints and policies the system enforces
- **Glossary** — the authoritative definitions of domain terms
- **Scope** — what is in and out of the delivery, by phase

### Where it lives
```
projects/<project>/knowledge/
├── project-overview.md
├── actors.md
├── modules.md
├── features.md
├── business-rules.md
├── glossary.md
└── scope.md
```

### Rules
- **Curated, not generated wholesale.** Knowledge is built incrementally as Sources are processed. It is the *output of agreement*, not the *dump of a transcript*.
- **Edit deliberately.** Each knowledge document carries a short changelog. When you change it, note why (e.g., "Added Module M-04 per DEC-007").
- **Cross-linked.** A Feature points to its Module and Actors. A Business Rule points to the Features it constrains. The glossary is the hub for terms.
- **Stable.** Knowledge changes on the cadence of *weeks* (a new module, a clarified actor), not minutes.

### Why it matters
Knowledge is the **context layer**. When an agent analyzes a new meeting, it reads Knowledge to interpret ambiguous statements ("*the portal*" → which portal? see `actors.md`/`modules.md`). Without Knowledge, every extraction starts from scratch and produces duplicates. With Knowledge, extractions *reconcile* against an existing picture.

---

## 3. Memory

### Definition
**Living project information that evolves continuously.** Memory captures what has been *decided, requested, committed, asked, worried about, or queued*. It changes every time a meeting happens or a decision is made.

### Examples (the six memory types)
- **Requirements** — `REQ-###` — what the system must do, with status and priority
- **Decisions** — `DEC-###` — choices made, with rationale and what they supersede
- **Action Items** — `ACT-###` — commitments, with owner and due date
- **Open Questions** — `Q-###` — unresolved questions, with who must answer
- **Risks** — `RSK-###` — identified risks, with likelihood/impact/mitigation
- **Backlog** — `BKL-###` — work items / stories not yet scheduled

### Where it lives
```
projects/<project>/memory/
├── requirements.md
├── decisions.md
├── action-items.md
├── open-questions.md
├── risks.md
└── backlog.md
```

### Rules
- **Provenance is mandatory.** Every item cites a Source in its frontmatter (`source: [SRC-MTG-2026-06-15]`). No uncited memory — ever.
- **Reconcile before you add.** Search existing memory for a near-match first. Update rather than duplicate.
- **Never delete — supersede.** Items transition through `status` (`proposed → accepted → superseded/rejected/closed`). IDs are never reused.
- **Highly linked.** A Requirement relates to the Decisions that shaped it and the Action Items that deliver it. These links are the project's decision graph.

### Why it matters
Memory is the **working layer** — the layer humans and agents actually consult day to day ("What did we decide about SSO?", "What's blocking the inventory module?"). Because it is reconciled and cited, it stays coherent as the project ages, instead of fragmenting across chat logs.

---

## 4. Capabilities

### Definition
**Repeatable AI workflows that operate on Source, Knowledge, and Memory.** A capability is a *procedure*: given certain inputs, follow certain steps, produce certain outputs. Capabilities are how information moves *between* the layers.

### Examples (roadmap)
- **Meeting Intelligence** — `source/meetings/*` → `outputs/meetings/*-mom.md` + updates to `memory/*` *(specified now)*
- **Requirements Management** — maintain `memory/requirements.md`, trace to Knowledge, detect drift
- **Backlog Management** — convert requirements/action items into backlog, prioritize, groom
- **Sprint Planning** — propose a sprint from Backlog + capacity + decisions
- **Reporting** — synthesize Knowledge + Memory into stakeholder reports

### Where it lives
```
capabilities/
└── meeting-intelligence/      # one directory per capability
    ├── README.md              # the workflow overview
    ├── project-onboarding.md  # step: bootstrap a project's Knowledge/Memory
    ├── meeting-analysis.md    # step: read a transcript, structure it
    ├── mom-generation.md      # step: write the Minutes of Meeting
    ├── requirement-extraction.md
    ├── decision-extraction.md
    ├── action-item-extraction.md
    └── open-question-extraction.md
```

### Rules
- **Each capability is a spec, not code.** It is written so *any* LLM agent can execute it by following instructions.
- **Idempotent where possible.** Re-running a capability on the same inputs should converge, not duplicate (the reconcile rule in Memory makes this work).
- **Explicit inputs/outputs.** Every step declares what it reads and what it writes, so agents (and humans) can reason about side effects.
- **Layer-aware.** A capability knows which layers it touches. Meeting Intelligence *reads* Source + Knowledge, and *writes* Outputs + Memory (and, during onboarding, Knowledge).

### Why it matters
Capabilities are the **automation layer**. Without them, "use this framework" is vague. With them, "process this meeting" means a precise, repeatable, auditable sequence that any agent can perform and any human can review.

---

## How the layers relate (worked example)

A team holds a kickoff meeting about an HRIS employee portal. Here is how the layers interact:

| Step | Layer touched | What happens |
|------|---------------|--------------|
| 1. Transcript filed | **Source** | `source/meetings/2026-06-15-kickoff.md` is added (immutable). |
| 2. Meeting Intelligence runs | **Capability** | The agent reads the transcript + existing Knowledge (initially sparse). |
| 3. MOM generated | **Output** | `outputs/meetings/2026-06-15-kickoff-mom.md` is written. |
| 4. Requirements extracted | **Memory** | `REQ-014 SSO` is added to `requirements.md`, citing the transcript. |
| 5. Decision extracted | **Memory** | `DEC-007 Use Okta for SSO` is added to `decisions.md`. |
| 6. Action items extracted | **Memory** | `ACT-023 Alice to confirm IdP licenses` is added. |
| 7. Open question raised | **Memory** | `Q-005 Do contractors get portal access?` is added. |
| 8. Knowledge enriched | **Knowledge** | New actor "Corporate IdP" and module "Identity" are added to Knowledge. |
| 9. Next meeting | **Source → Capability → Memory** | The agent *reconciles* against `REQ-014`, `DEC-007`, etc. — it does not re-create them. |

The key property: **step 9 does not duplicate steps 4–6.** That is the entire point of the layered model. Provenance + reconciliation keep the framework coherent over time.

---

## Summary table

| Concept | One-liner | Mutability | Citation |
|---------|-----------|------------|----------|
| **Source** | "What was said." | Immutable, append-only | Is itself the citation |
| **Knowledge** | "What the project is." | Slow, deliberate | Links to Source where extracted |
| **Memory** | "What we decided/asked/committed." | Fast, reconciled | **Must** cite a Source |
| **Capabilities** | "How we process the above." | Stable spec | Declares inputs/outputs |

Next: [`architecture.md`](architecture.md) for how projects, isolation, and agents are structured on top of this model.
