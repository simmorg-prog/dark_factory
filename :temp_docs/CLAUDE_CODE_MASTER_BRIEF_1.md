# Dark Factory — Master Brief for Claude Code
**Version:** 1.3  
**Date:** May 2026  
**Status:** Authoritative instruction set — execute in order  
**Changes:** v1.1 — Added E5-00. v1.2 — Added E5-08. v1.3 — Added Practice Premium Principle across E5-00, E5-08, E1-04, E5-03.

---

## Overview

This document is the single authoritative brief for Claude Code working on the `dark_factory` repository at `https://github.com/simmorg-prog/dark_factory`.

It consolidates all decisions, standards, corrections, and new work items agreed in the strategy conversation. Read this document in full before writing any file.

---

## 1. Framework Identity

### Name
**AI Operational Maturity Framework**

> ⚠️ The framework was previously referred to as "AI Engineering Maturity." The correct name is **AI Operational Maturity**. This must be reflected everywhere — README, all content files, all diagram titles, all navigation links.

### Scope
The framework covers **two equally important domains**:
1. **Software Engineering Workflow** — the original and primary reference implementation
2. **Enterprise Knowledge Work** — Finance, Legal, HR, Procurement, Sales, Risk & Compliance, Customer Operations, R&D, IT Operations, Supply Chain

Software engineering is where the Dark Factory pattern emerged first. All other knowledge work domains follow the same six-stage maturity curve, 12–36 months behind the software frontier.

### Tagline
> *"A six-stage maturity model for AI-operated workflow — from prompt engineering to environment engineering. Applicable to software delivery and all enterprise knowledge work."*

---

## 2. Delivery Standards — Non-Negotiable

These standards apply to every file produced. Do not deviate.

### Markdown Files
- All content delivered as `.md` files
- GitHub-flavoured Markdown
- Header format on every file:
  ```
  > **[Item ID] · [Epic Name] · Wave [N]**  
  > [One-line description of this document's purpose]  
  > See also: [relative links to related docs]
  ```
- All internal cross-links must use **relative paths** — never absolute GitHub URLs
  - ✅ `../diagrams/glossary-relationships.svg`
  - ✅ `./maturity-curve.md`
  - ❌ `https://github.com/simmorg-prog/dark_factory/blob/main/...`
- Named principles and key terms formatted as blockquotes
- Tables used for reference material, prose for explanatory content

### Diagrams
- Every diagram produced as **both** `.drawio` (editable source) and `.svg` (rendered output)
- Both files committed to `/diagrams/` folder
- Diagrams referenced in Markdown as linked SVGs:
  ```markdown
  ![Diagram Title](../diagrams/filename.svg)
  ```
- Never embed SVG inline in Markdown

### Colour Palette — Use Consistently Across All Diagrams

| Stage / Use | Fill | Text / Accent |
|---|---|---|
| Stage 1 — Prompt Eng. | `#2E75B6` | `#FFFFFF` |
| Stage 2 — Context Eng. | `#70AD47` | `#FFFFFF` |
| Stage 3 — Intent Eng. | `#ED7D31` | `#FFFFFF` |
| Stage 4 — Spec. Eng. | `#2D3748` | `#D4A017` |
| Stage 5 — Harness Eng. | `#1C1C1C` | `#D4A017` |
| Stage 6 — Env. Eng. | `#7030A0` | `#FFFFFF` |
| Dark Factory boundary | `#1C1C1C` dashed line | `#D4A017` label |
| Human Zone | `#E2EFDA` | `#375623` |
| Warning / Risk | `#FDDBD8` | `#C00000` |
| Navy (headers) | `#1F3864` | `#FFFFFF` |

---

## 3. Repository Structure

Ensure this exact structure exists. Create any missing folders.

```
dark_factory/
├── README.md                          ← Master index (see Section 4)
├── BACKLOG.md                         ← Living backlog tracker (see Section 5)
├── diagrams/                          ← All .drawio and .svg files
├── 00-foundations/
│   ├── glossary.md                    ← E1-01 ✅ EXISTS — needs fixes (Section 6)
│   ├── maturity-curve.md              ← E1-02 ✅ EXISTS — needs fixes (Section 6)
│   ├── dark-factory.md                ← E1-05 🔜 NEW
│   ├── reader-guide.md                ← E1-03 🔜 NEW
│   ├── cumulative-stack.md            ← E1-04 🔜 NEW
│   └── specification-discipline.md   ← E1-06 🔜 NEW
├── 01-actors/
├── 02-artefacts/
├── 03-stages/
├── 04-examples/
└── 05-strategy/
    └── enterprise-knowledge-work-map.md  ← E5-07 🔜 NEW
```

---

## 4. README.md — Full Rewrite Required

The existing `readme.md` needs the following changes. Rewrite it completely as `README.md` (uppercase).

### Required content:

**Header block:**
```markdown
# AI Operational Maturity Framework

> A six-stage maturity model for AI-operated workflow — from prompt engineering 
> to environment engineering. Applicable to software delivery and all enterprise 
> knowledge work.
```

**The Six Stages table** — correct content, already present, keep it.

**The Dark Factory callout** — correct, keep it.

**Scope statement** — NEW. Add after the Dark Factory callout:
```markdown
## Scope

This framework applies to two domains:

**Software Engineering** — the reference implementation. The Dark Factory 
pattern emerged first in software delivery and provides the clearest evidence 
base for all six stages.

**Enterprise Knowledge Work** — Finance, Legal, HR, Procurement, Sales & 
Marketing, Risk & Compliance, Customer Operations, R&D, IT Operations, and 
Supply Chain. The same six stages apply. The vocabulary changes. The structure 
does not.

See: [Enterprise Knowledge Work Map](./05-strategy/enterprise-knowledge-work-map.md)
```

**Repository structure** — expand to show ALL six folders with descriptions:
```markdown
## Repository Structure

| Folder | Contents |
|---|---|
| `00-foundations/` | Core concepts: glossary, maturity curve, dark factory, specification discipline |
| `01-actors/` | Human, Agent, and Agent Council design patterns |
| `02-artefacts/` | Specification corpus, escalation packages, requirements templates |
| `03-stages/` | Deep dives and transition playbooks for each stage |
| `04-examples/` | Worked examples across software engineering and knowledge work domains |
| `05-strategy/` | Organisational assessment, governance, investment guidance |
| `diagrams/` | All Draw.io source files and exported SVGs |
```

**Wave status table** — show ALL waves and ALL items with status:

```markdown
## Content Status

### Wave 1 — Foundations
| ID | Title | Status |
|---|---|---|
| E1-01 | [Glossary of Terms](./00-foundations/glossary.md) | ✅ Complete |
| E1-02 | [Maturity Curve — Visual Overview](./00-foundations/maturity-curve.md) | ✅ Complete |
| E1-05 | [The Dark Factory — Extended Definition](./00-foundations/dark-factory.md) | 🔄 In Progress |
| E1-03 | [Reader Guide](./00-foundations/reader-guide.md) | 🔜 Pending |
| E1-04 | [The Cumulative Stack Explained](./00-foundations/cumulative-stack.md) | 🔜 Pending |
| E1-06 | [The Specification Discipline — Three Principles](./00-foundations/specification-discipline.md) | 🔜 Pending |

### Wave 2 — Scope & Strategy
| ID | Title | Status |
|---|---|---|
| E5-00 | [The AI-Native Organisation — Vision Narrative](./05-strategy/vision-ai-native.md) | 🔜 Pending |
| E5-08 | [Wardley Map — AI Operational Maturity](./05-strategy/wardley-map.md) | 🔜 Pending |
| E5-07 | [Enterprise Knowledge Work Map](./05-strategy/enterprise-knowledge-work-map.md) | 🔜 Pending |
| E3-01 | Human Role Transformation | 🔜 Pending |
| E3-06 | Human-Agent Handoff Protocols | 🔜 Pending |
| E3-03 | Agent Council Design | 🔜 Pending |

### Waves 3–7 — Pending
See [BACKLOG.md](./BACKLOG.md) for full item list.
```

**Footer navigation:**
```markdown
---
*This framework is developed iteratively. See [BACKLOG.md](./BACKLOG.md) 
for the full item list and execution sequence.*
```

---

## 5. BACKLOG.md — Create New File

Create `BACKLOG.md` at the repo root. This is the living backlog tracker.

### Required content:

**Header:**
```markdown
# AI Operational Maturity — Backlog

> Living tracker. Updated as each item is completed.  
> **Total items:** 42 | **Done:** 2 | **In Progress:** 0 | **To Do:** 40
```

**Full item table — all 41 items:**

| ID | Title | Epic | Wave | Priority | Effort | Status |
|---|---|---|---|---|---|---|
| E1-01 | Glossary of Terms | Foundations | 1 | P1 | S | ✅ Done |
| E1-02 | Maturity Curve — Visual Overview | Foundations | 1 | P1 | M | ✅ Done |
| E1-05 | The Dark Factory — Extended Definition | Foundations | 1 | P1 | M | 🔜 To Do |
| E1-03 | Reader Guide | Foundations | 1 | P2 | S | 🔜 To Do |
| E1-04 | The Cumulative Stack Explained | Foundations | 1 | P2 | M | 🔜 To Do |
| E1-06 | The Specification Discipline — Three Principles | Foundations | 1 | P1 | S | 🔜 To Do |
| E5-00 | The AI-Native Organisation — Vision Narrative | Strategy | 2 | P1 | M | 🔜 To Do |
| E5-08 | Wardley Map — AI Operational Maturity | Strategy | 2 | P1 | L | 🔜 To Do |
| E5-07 | Enterprise Knowledge Work Map | Strategy | 2 | P1 | L | 🔜 To Do |
| E3-01 | The Human Role Transformation | Actors | 2 | P1 | L | 🔜 To Do |
| E3-06 | Human-Agent Handoff Protocols | Actors | 2 | P1 | M | 🔜 To Do |
| E3-03 | Agent Council Design — Constitution & Governance | Actors | 2 | P1 | L | 🔜 To Do |
| E3-02 | Agent Taxonomy — Types, Capabilities, Limitations | Actors | 3 | P2 | M | 🔜 To Do |
| E3-04 | Agent Council Patterns | Actors | 3 | P2 | L | 🔜 To Do |
| E3-05 | The Meta-Council — Cross-Domain Arbitration | Actors | 3 | P2 | M | 🔜 To Do |
| E4-01 | Artefact Catalogue — All Stages | Artefacts | 4 | P1 | L | 🔜 To Do |
| E4-02 | Requirements Specification Templates | Artefacts | 4 | P1 | M | 🔜 To Do |
| E4-05 | Escalation Package Standard | Artefacts | 4 | P2 | S | 🔜 To Do |
| E4-03 | Intent Manifest — Reference Design | Artefacts | 4 | P2 | M | 🔜 To Do |
| E4-04 | Specification Corpus — Architecture & Governance | Artefacts | 4 | P2 | L | 🔜 To Do |
| E4-06 | Environment Map — Reference Design | Artefacts | 4 | P3 | M | 🔜 To Do |
| E2-07 | Stage Transition Playbooks (1→2, 2→3, 3→4, 4→5, 5→6) | Stages | 5 | P1 | XL | 🔜 To Do |
| E2-01 | Stage 1 Deep Dive — Prompt Engineering | Stages | 5 | P3 | M | 🔜 To Do |
| E2-02 | Stage 2 Deep Dive — Context Engineering | Stages | 5 | P2 | L | 🔜 To Do |
| E2-03 | Stage 3 Deep Dive — Intent Engineering | Stages | 5 | P2 | L | 🔜 To Do |
| E2-04 | Stage 4 Deep Dive — Specification Engineering | Stages | 5 | P2 | L | 🔜 To Do |
| E2-05 | Stage 5 Deep Dive — Harness Engineering | Stages | 5 | P1 | L | 🔜 To Do |
| E2-06 | Stage 6 Deep Dive — Environment Engineering | Stages | 5 | P2 | L | 🔜 To Do |
| E6-01 | Worked Example: Feature Delivery at Each Stage | Examples | 6 | P1 | XL | 🔜 To Do |
| E6-04 | The Stage 3→4 Transition in Detail | Examples | 6 | P1 | L | 🔜 To Do |
| E6-06 | Worked Example: Finance Month-End Close at Each Stage | Examples | 6 | P2 | L | 🔜 To Do |
| E6-07 | Worked Example: Legal Contract Review at Each Stage | Examples | 6 | P2 | L | 🔜 To Do |
| E6-02 | Worked Example: Incident Response at Each Stage | Examples | 6 | P2 | L | 🔜 To Do |
| E6-03 | Anti-Patterns Library | Examples | 6 | P2 | M | 🔜 To Do |
| E6-05 | Dark Factory Operating Model | Examples | 6 | P2 | L | 🔜 To Do |
| E5-01 | Organisational Maturity Assessment | Strategy | 7 | P1 | L | 🔜 To Do |
| E5-05 | AI Governance in the Dark Factory | Strategy | 7 | P1 | L | 🔜 To Do |
| E5-04 | Risk Register — Across All Stages | Strategy | 7 | P1 | M | 🔜 To Do |
| E5-02 | The Engineering Team of the Future | Strategy | 7 | P2 | M | 🔜 To Do |
| E5-03 | Investment & Roadmap Planning Guide | Strategy | 7 | P2 | M | 🔜 To Do |
| E5-06 | Vendor & Tooling Landscape | Strategy | 7 | P3 | M | 🔜 To Do |

**Effort key:**
```markdown
## Effort Key
| Code | Meaning |
|---|---|
| S | Small — ~1 page |
| M | Medium — ~2–3 pages |
| L | Large — ~4–6 pages |
| XL | Extensive — ~7–10 pages |
```

**Wave sequence summary:**
```markdown
## Execution Sequence

| Wave | Focus | Items |
|---|---|---|
| 1 | Foundations | E1-01 ✅ E1-02 ✅ E1-05 E1-03 E1-04 E1-06 |
| 2 | Scope & Strategy | E5-00 E5-08 E5-07 E3-01 E3-06 E3-03 |
| 3 | Actors | E3-02 E3-04 E3-05 |
| 4 | Artefacts | E4-01 E4-02 E4-05 E4-03 E4-04 E4-06 |
| 5 | Stage Overviews | E2-07 E2-01 E2-02 E2-03 E2-04 E2-05 E2-06 |
| 6 | Worked Examples | E6-01 E6-04 E6-06 E6-07 E6-02 E6-03 E6-05 |
| 7 | Organisational & Strategic | E5-01 E5-05 E5-04 E5-02 E5-03 E5-06 |
```

---

## 6. Fixes to Existing Files

### 6.1 — glossary.md (E1-01)

**Location:** `00-foundations/glossary.md`

**Changes required:**
1. Update framework name from "AI Engineering Maturity" to "AI Operational Maturity" wherever it appears
2. Add two new entries to the **Key Concepts** section:

**Entry: Living Specification**
```markdown
### Living Specification
A specification that is co-located with the work it governs, validated 
automatically by continuous integration, and updated iteratively as 
understanding evolves. Contrast with a static specification, which is 
written upfront, frozen after sign-off, and becomes obsolete as the 
system evolves. Living specifications deliver rigour without requiring 
completeness upfront — they mature alongside the system they describe.

The mechanism that makes a specification living is automation, not intent. 
A specification that someone intends to keep updated but is not validated 
by automated tests is a static specification with good intentions.
```

**Entry: Specification Discipline**
```markdown
### Specification Discipline
The practice of writing specifications with semantic precision from the 
outset of a project, regardless of maturity stage. The Specification 
Discipline is founded on three principles:

1. **Rigour from the outset, not rigour all at once** — precision at 
   Stage 1 costs almost nothing; retrofitting it at Stage 4 is 
   enormously expensive.
2. **Living specifications, not static documents** — specifications 
   should be emergent, iterative, and continuously refined.
3. **Universal applicability** — specification quality governs 
   deterministic systems (rules engines, OPA) and probabilistic systems 
   (LLM agents) equally. The failure modes differ; the discipline is the same.

See: [The Specification Discipline — Three Principles](./specification-discipline.md)
```

### 6.2 — maturity-curve.md (E1-02)

**Location:** `00-foundations/maturity-curve.md`

**Changes required:**
1. Update framework name to "AI Operational Maturity" throughout
2. Fix all internal links to use relative paths (not absolute GitHub URLs)
3. Add explanatory paragraph under the Actor Involvement section **before** the diagram link:

```markdown
The heat map below shows how the involvement of each actor type changes 
across the six stages. Human involvement is high and continuous in Stages 
1–3, transitioning to exception-based at Stage 4 and above. Agent 
involvement grows from zero at Stage 1 to dominant from Stage 4 onward. 
Agent Council involvement emerges at Stage 2 (informally) and becomes 
the primary governance mechanism of the Dark Factory from Stage 4.
```

4. Add a callout box after the Stage Summary table linking to the Specification Discipline document:

```markdown
> 💡 **Specification Discipline starts at Stage 1, not Stage 4.**  
> The quality of specifications authored at every stage determines what 
> the Dark Factory can enforce. See: 
> [The Specification Discipline — Three Principles](./specification-discipline.md)
```

---

## 7. New Files to Create — Wave 1 Remainder

Execute in this order. Complete each file before starting the next.

---

### 7.1 — E1-05: The Dark Factory — Extended Definition

**File:** `00-foundations/dark-factory.md`  
**Diagrams:**
- `diagrams/dark-factory-boundary.drawio` + `.svg`
- `diagrams/dark-factory-operating-model.drawio` + `.svg`

**dark-factory-boundary diagram:** A before/after split diagram. Left half labelled "Before Stage 4 — Human-in-the-loop." Right half labelled "Stage 4 and beyond — Dark Factory." Left side shows: Requirements → Human Design → Human Implementation → Human Test → Human Review → Human Deploy. Right side shows: Human Requirements → Agent Design → Agent Implementation → Agent Test → Agent Review → Agent Deploy → Human Exception Handling. A bold vertical dashed line separates the two halves, labelled "The Dark Factory Boundary." Left side uses lighter colours. Right side uses dark charcoal/gold palette. Humans marked with 👤, agents marked with 🤖.

**dark-factory-operating-model diagram:** A runtime flow diagram. Top input: "Human — Requirements & Intent Boundaries." Arrow down into a dark-background box labelled "Dark Factory." Inside: Agent Council (left) → Workflow Stages (centre: Design, Implement, Test, Review, Deploy) → Specification Corpus (right). At the bottom of the box: "Specification Gap or Novel Risk detected." Arrow down to: "Escalation Package → Human Decision." Arrow back up into the Dark Factory: "Specification Updated — Workflow Resumes." Use gold arrows for the escalation loop.

**Content structure:**
1. Definition — what the Dark Factory is. The manufacturing analogy (FANUC, lights-off production). What "lights off" means in knowledge work — not darkness, but the absence of humans in the operational loop.
2. Boundary diagram (linked SVG) — the before/after split
3. What changes at the boundary — a comparison table:

| Dimension | Before Stage 4 | Stage 4 and beyond |
|---|---|---|
| Who owns design | Human | Agent Council |
| Who owns implementation | Human | Agent |
| Who owns testing | Human (with agent assist) | Agent |
| Who owns deployment | Human | Agent |
| How humans are involved | Continuously, in every step | Exception-based only |
| What escalation looks like | Ad hoc conversation | Formal escalation package |

4. Operating model diagram (linked SVG)
5. The operating model explained — requirements in, Agent Councils govern, escalation out, human response, workflow resumes. The specification corpus is the law. Escalation is what happens when the law doesn't cover the situation.
6. Five preconditions for entering the Dark Factory — these must all be true before an organisation transitions from Stage 3 to Stage 4:
   - Context quality is consistently measurable and meets a defined threshold
   - Organisational intent is encoded in a maintained intent manifest
   - The specification corpus covers at least 80% of anticipated workflow decisions
   - A harness exists that can monitor agent behaviour and surface anomalies
   - Escalation protocols are defined, tested, and trusted by the humans who will receive them
7. Three primary failure modes and their symptoms:
   - **Specification Gap** — agents halt or produce confident wrong outputs. Symptom: escalation rate spikes, output quality degrades, human override frequency rises.
   - **Intent Drift** — agents comply with specifications but produce strategically wrong outcomes. Symptom: outputs feel wrong without being technically incorrect, human overrides cluster around a specific class of decision.
   - **Harness Failure** — agent behaviour becomes unpredictable or inconsistent. Symptom: non-reproducible outputs, context degradation, agent loops.
8. The human role transformation — what it demands of the humans who remain. Shift from execution to governance. The skills that matter: intent authorship, specification quality, escalation triage, system design.
9. Navigation links

---

### 7.2 — E1-03: Reader Guide

**File:** `00-foundations/reader-guide.md`  
**No diagrams required.**

**Content structure:**
1. Purpose of this guide — how to navigate the framework depending on who you are
2. Four reader profiles with recommended reading paths:

**The CTO / Technology Leader**
- Start: Maturity Curve Overview → Dark Factory Definition → Enterprise Knowledge Work Map
- Then: Stage 3→4 Transition → AI Governance in the Dark Factory → Maturity Assessment
- Skip: Stage 1 and 2 deep dives (unless needed for context)
- Key question answered: *"Where are we, where do we need to get to, and what does it take?"*

**The Engineering Architect**
- Start: Glossary → Maturity Curve → Cumulative Stack
- Then: Stage deep dives in sequence → Harness Engineering → Agent Council Design
- Then: Artefact Catalogue → Specification Corpus → Environment Map
- Key question answered: *"How do I design systems that can operate at Stage 4 and beyond?"*

**The Engineering Manager / Team Lead**
- Start: Glossary → Dark Factory Definition → Human Role Transformation
- Then: Human-Agent Handoff Protocols → Stage Transition Playbooks → Anti-Patterns
- Then: Worked Examples (feature delivery, incident response)
- Key question answered: *"What changes for my team and how do I manage the transition?"*

**The Business Leader (non-engineering)**
- Start: Enterprise Knowledge Work Map → Dark Factory Definition → Maturity Curve
- Then: Worked Examples (Finance, Legal) → Risk Register → AI Governance
- Skip: Stage deep dives, Harness Engineering, Agent Council technical detail
- Key question answered: *"What does this mean for my function and what do I need to govern?"*

3. How the document is structured — a brief explanation of the wave approach and what breadth-first means for completeness
4. How to contribute — links back, suggestions, terminology corrections
5. Navigation links

---

### 7.3 — E1-04: The Cumulative Stack Explained

**File:** `00-foundations/cumulative-stack.md`  
**Diagrams:**
- `diagrams/cumulative-stack.drawio` + `.svg`

**cumulative-stack diagram:** A pyramid or stacked block diagram. Six layers stacked vertically, Stage 1 at the base, Stage 6 at the apex. Each layer labelled with stage number, name, and one-line characteristic. The layers below the Dark Factory boundary are lighter; the layers above are darker. An arrow on the left side pointing upward labelled "Increasing autonomy." An arrow on the right side pointing upward labelled "Increasing specification maturity." A horizontal line at the Stage 3/4 boundary labelled "Dark Factory Threshold." Key callout: "Remove any layer and the layers above it collapse."

**Content structure:**
1. Opening — the most important structural principle of the framework: these stages do not replace each other, they stack. Every stage presupposes and subsumes all stages below it.
2. The stack diagram (linked SVG)
3. Why stacking matters — three paragraphs explaining:
   - What each stage adds (not replaces)
   - What breaks if a layer is missing
   - Why organisations that skip stages create technical debt at the architecture level, not just the code level
4. The Specification Debt Principle — named principle, formatted as a blockquote:

> **The Specification Debt Principle**  
> Ambiguity authored at Stage 1 does not disappear at Stage 4 — it becomes policy. Every poorly-authored requirement is a specification defect that compounds as it travels up the stack. At Stage 1 it produces a bad output. At Stage 2 it contaminates a retrieval pipeline. At Stage 3 it encodes a wrong goal. At Stage 4 it becomes law that agents enforce at production speed. The cost of fixing a specification defect multiplies at each stage transition. The cost of authoring it correctly at Stage 1 is negligible.

5. The amplification argument — how the same defect produces increasingly severe outcomes at higher stages. A worked example: an ambiguous requirement at each stage and what it produces.
6. **The Practice Stack — not just a technology stack** — a critical clarifying section. The cumulative stack is not a technology deployment sequence. It is a *practice development sequence*. Each stage represents a set of organisational disciplines that must be genuinely developed, not just technologies that must be deployed. This is why skipping stages fails — not because the technology won't run, but because the *practices* at each stage build the organisational muscle required for the next. Include the Practice Premium Principle as a named blockquote:

> **The Practice Premium Principle**  
> Technology components in the AI stack commoditise on the standard evolution curve — available to all, differentiating to none. The durable competitive advantage lies in the organisational practice disciplines that make those components work. These practices are emergent and tacit. They develop through deliberate learning and accumulation. They cannot be purchased. An organisation that deploys a Stage 4 specification management platform without having developed the specification discipline practices of Stages 1–3 has purchased infrastructure that will amplify its existing weaknesses. The platform does not create the practice. The practice must precede the platform.

7. The maturity assessment implication — organisations should identify their *lowest solid layer*, not their highest attempted layer. An organisation with Stage 4 tooling and Stage 2 context quality is a Stage 2 organisation with expensive technical debt.
8. Navigation links — forward to Specification Discipline, Wardley Map, back to Maturity Curve

---

### 7.4 — E1-06: The Specification Discipline — Three Principles

**File:** `00-foundations/specification-discipline.md`  
**Diagrams:**
- `diagrams/specification-discipline-spectrum.drawio` + `.svg`
- `diagrams/specification-universality.drawio` + `.svg`

**specification-discipline-spectrum diagram:** A horizontal spectrum. Left zone (muted red/amber): "Static Specification" — labelled: Upfront, Frozen, Obsolete, Waterfall. Right zone (green): "Living Specification" — labelled: Incremental, Versioned, Automated, Agile-compatible. A vertical dividing line in the centre labelled "The misconception lives here — both sides require rigour." Below the spectrum: RFC 2119, BDD/Gherkin, and Spec-Driven Development shown as points on the right side. IEEE 830, Big Design Upfront shown on the left.

**specification-universality diagram:** Three equal columns. Column 1: "Deterministic Systems" — icons: Rules Engine, OPA/Rego, BRMS, Decision Table. Column 2: "Probabilistic Systems" — icons: LLM Agent, RAG Pipeline, AI Workflow. Column 3: "Hybrid Systems" — both combined, with an arrow between them. Below each column, what a bad specification produces: Column 1: "Consistent wrong decision — every time, at scale." Column 2: "Variable invisible failure — hard to detect, hard to diagnose." Column 3: "Both failure modes simultaneously." Shared header across all three: "All three execute the specification they are given with fidelity."

**Content structure:**
1. Opening — directly address the objection. State it plainly: *"specification rigour means waterfall."* Then state clearly: this is understandable, historically grounded, and wrong.
2. Where the misconception comes from — the waterfall failure mode, the Agile Manifesto's reaction, how "working software over comprehensive documentation" became misread as "no specification needed." Short and honest — acknowledge the legitimate concern before dismantling it.
3. **Principle 1 — Rigour from the outset, not rigour all at once** — formatted as a named blockquote. The compounding argument. The spectrum diagram (linked SVG). RFC 2119 as the evidence that precision and brevity coexist — a MUST in a user story acceptance criterion is as precise as a MUST in a 500-page document, and costs almost nothing to write.
4. **Principle 2 — Living specifications, not static documents** — formatted as a named blockquote. BDD, Specification by Example, Spec-Driven Development as the agile-native evidence. The four properties of a living specification: co-located with code, validated by CI, updated iteratively, owned by the whole team. The mechanism is automation, not intention.
5. **Principle 3 — Universal applicability: deterministic and probabilistic systems alike** — formatted as a named blockquote. The universality diagram (linked SVG). Rules engines fail with bad specs just as surely as LLM agents — they just fail differently. Deterministic = consistently wrong. Probabilistic = variably and invisibly wrong. Hybrid = both simultaneously. The Dark Factory contains both layers.
6. The practical implication — one tight closing section. What to do tomorrow, regardless of maturity stage: use RFC 2119 semantics on the next requirement you write. Make acceptance criteria explicit and binary. Name what is out of scope. Version your specifications. The corpus grows from there.
7. Navigation links

---

### 7.5 — E5-07: Enterprise Knowledge Work Map

**File:** `05-strategy/enterprise-knowledge-work-map.md`  
**Diagrams:**
- `diagrams/knowledge-work-domains.drawio` + `.svg`
- `diagrams/knowledge-work-maturity-grid.drawio` + `.svg`

**knowledge-work-domains diagram:** A hub-and-spoke or grid layout. Centre: "AI Operational Maturity — Six Stage Framework." Ten domain nodes arranged around it, colour-coded by cluster:
- Back-office (blue-grey): Finance, HR, Procurement
- Front-office (teal): Sales & Marketing, Customer Operations
- Specialist professional (purple): Legal, R&D, Risk & Compliance
- Infrastructure (slate): IT Operations, Supply Chain

**knowledge-work-maturity-grid diagram:** A matrix. Rows = six maturity stages (Stage 1–6). Columns = five domains: Software Engineering, Finance, Legal, HR, Procurement. Each cell: one-line description of what that stage looks like in that domain. Stages 4–6 rows: dark charcoal background, gold text. Stages 1–3 rows: light backgrounds matching stage colours. Dark Factory boundary line between rows 3 and 4, labelled in gold.

**Content structure:**
1. Opening — explicit scope statement. This framework began in software engineering. It applies to every domain where knowledge work is structured, repeatable, and consequential. The historical parallel: industrial revolution mechanised physical work; agentic revolution is mechanising knowledge work.
2. What is knowledge work? — tight definition. Work requiring human judgement, synthesis, and decision-making. Historically resistant to automation because inputs are ambiguous, processes non-deterministic, outputs require contextual judgement. Agentic AI changes the equation.
3. The domain map — introduce domains diagram (linked SVG). One paragraph per domain cluster:
   - **Back-office** — structured, high-volume, heavily regulated, clear acceptance criteria
   - **Front-office** — high-frequency, customer-facing, intent-sensitive
   - **Specialist professional** — high-stakes, knowledge-intensive, historically most resistant
   - **Infrastructure operations** — complex systems, real-time, interdependency-heavy
4. The maturity grid — introduce grid diagram (linked SVG). Two paragraphs: the same six stages apply in every domain; the human role transformation follows the same arc; the Dark Factory boundary represents the same qualitative shift.
5. Why software engineering leads — honest explanation. Fastest adoption, most tooling, clearest evidence. Other domains are 12–36 months behind. This means software engineering lessons are directly applicable as those domains mature.
6. The governance imperative outside engineering — non-engineering domain stakes are higher. Financial decisions, employment decisions, legal commitments, customer-facing actions cannot be rolled back like code. Specification rigour is *more* critical in business operations, not less.
7. Domain-specific risks at the Dark Factory boundary — table:

| Domain | Primary Dark Factory Risk | Regulatory Exposure | Key Escalation Trigger |
|---|---|---|---|
| Finance | Incorrect financial reporting | SOX, IFRS, GAAP | Material variance, audit query |
| Legal | Incorrect legal commitment | Jurisdiction-specific liability | Novel clause, unresolved ambiguity |
| HR | Discriminatory or unlawful decision | Employment law, GDPR | Protected characteristic involved |
| Procurement | Unauthorised commitment | Procurement policy, contract law | Value threshold exceeded |
| Risk & Compliance | Undetected regulatory breach | EU AI Act, sector regulation | Regulatory change, control failure |
| Customer Operations | Incorrect customer commitment | Consumer protection law | Complaint escalation, SLA breach |

8. Navigation links — forward to E6-06 (Finance worked example), E6-07 (Legal worked example), E1-05 (Dark Factory definition), E1-06 (Specification Discipline)

### 7.6 — E5-00: The AI-Native Organisation — Vision Narrative

**File:** `05-strategy/vision-ai-native.md`  
**No diagrams required.** This is a pure narrative document.

**Purpose:** This is the strategic entry point for the entire framework. It is written for a CEO, COO, board member, or senior business leader who needs to understand *why* AI operational maturity matters before engaging with *how*. It should be the first document a non-technical reader encounters, and the document that convinces a technical reader that this framework has strategic weight beyond the engineering domain.

**Tone:** Authoritative, direct, and considered. Not evangelical or hype-driven. This document should read like it was written by a practitioner who has seen both sides of this transition — what it looks like when it works and what it looks like when it fails. It names uncomfortable truths without being alarmist.

**Content:** The full vision narrative text is provided below. Reproduce it exactly, formatted as clean GitHub Markdown. Apply the standard file header.

**File header:**
```markdown
> **E5-00 · Strategy · Wave 2**  
> Vision narrative — why AI operational maturity is the critical capability 
> for organisations that intend to become AI-native.  
> See also: [Maturity Curve Overview](../00-foundations/maturity-curve.md) · 
> [Enterprise Knowledge Work Map](./enterprise-knowledge-work-map.md) · 
> [The Dark Factory](../00-foundations/dark-factory.md)
```

**Full narrative content to reproduce:**

---

# The AI-Native Organisation

## Why This Moment Is Different From Every Previous Technology Wave

Every generation of enterprise technology has promised transformation. Mainframes, ERP systems, the internet, cloud computing — each arrived with the claim that it would fundamentally change how organisations operate. Each did, eventually. But in each case, organisations adapted their existing structures to accommodate the new technology. They automated what they were already doing. They moved existing processes to new platforms. The fundamental unit of work — a task performed by a human, assisted by a tool — remained unchanged.

The agentic revolution breaks that pattern. For the first time in the history of enterprise technology, the question is not *how do we use this tool to do our work better?* It is *how do we redesign our work so that agents can do most of it?*

That is not an incremental question. It is a constitutional one. And organisations that fail to recognise the difference will spend the next decade doing what they have always done — layering new technology onto old operating models — and wondering why the returns never materialise. Only 34% of organisations are truly reimagining the business. The rest are delivering efficiency gains, not transformation.

---

## What AI-Native Actually Means

The term "AI-native" is used loosely. It is worth being precise.

An AI-native organisation is not one that uses a lot of AI tools. Most organisations now use AI tools. Tool adoption is not transformation. An organisation that has given every employee a ChatGPT licence and seen productivity tick up slightly is not AI-native. It is AI-augmented. The distinction matters enormously.

An AI-native organisation is one that has redesigned its operating model around the assumption that agents will perform the majority of structured knowledge work — and that humans will govern, direct, and evolve the systems those agents operate within.

Organisations should take an AI-native approach and redesign work holistically rather than layering AI onto legacy processes. The operative word is *holistically*. Not function by function, pilot by pilot, tool by tool — but as a coherent operating model in which the relationship between human work and agent work is deliberately designed, governed, and continuously improved.

Three things define an AI-native organisation that do not define an AI-augmented one:

**First, agents are participants, not tools.** In an AI-augmented organisation, a human picks up an AI tool to help with a task and puts it down when the task is done. In an AI-native organisation, agents are persistent participants in workflows — they have memory, they use tools, they coordinate with other agents, they operate continuously, and they escalate to humans when they encounter decisions beyond their specification envelope. The agent is not something you use. It is something you govern.

**Second, the specification is the product.** In a traditional organisation, the product of knowledge work is a document, a decision, a piece of software, a financial report. In an AI-native organisation, the most important product is the specification that instructs agents how to produce those outputs. The quality of human thinking is no longer expressed primarily in doing the work. It is expressed in defining the work clearly enough that agents can do it reliably, at scale, and without continuous human oversight. The bottleneck moves from execution speed to the clarity of organisational intent. This is true not just in software — it is true in finance, legal, HR, procurement, and every other knowledge work domain.

**Third, the environment is designed for agents, not adapted for them.** AI-augmented organisations take their existing systems, processes, and data architectures and try to make AI work within them. AI-native organisations redesign their environments — their APIs, data models, process structures, and knowledge bases — to be inherently legible to agents. The AI-native enterprise treats context as critical infrastructure.

---

## The Maturity Journey — Why You Cannot Skip Stages

Becoming AI-native is not a destination you can jump to. It is a progression through six stages of organisational maturity, each of which builds indispensably on the last.

This is the central claim of the AI Operational Maturity Framework — and it is worth stating plainly, because it runs against the instinct of most technology leaders. The instinct is to move fast, deploy boldly, and learn by doing. That instinct is right for many things. For agentic AI, it is a reliable path to expensive failure.

The organisations that skip the foundational stages in favour of pure agentic deployment, treating AI agents as the workflow rather than as a component within it, will see their agentic AI deployments fail. Gartner predicts over 40% of agentic AI projects will be cancelled by the end of 2027. Why do they fail? Not because the technology doesn't work. The technology increasingly works. They fail because the organisational infrastructure required to operate agents reliably — the context architecture, the encoded intent, the specification corpus, the harness, the governance model — was not built before the agents were deployed. You cannot govern what you haven't designed. You cannot enforce what you haven't specified. And you cannot specify what you haven't understood.

The six stages of the framework describe exactly what must be built, in what order, before an organisation can operate reliably at the next level. Each stage is a prerequisite for the next. The stack is load-bearing. Remove a layer and the layers above it collapse.

See: [The Maturity Curve — Visual Overview](../00-foundations/maturity-curve.md) · [The Cumulative Stack Explained](../00-foundations/cumulative-stack.md)

---

## The Dark Factory — The Destination That Redefines Human Work

The Dark Factory is the name for what an organisation looks like when it has progressed through all six stages and agents genuinely own the operational workflow. It borrows from manufacturing — the lights-off production facility where automation runs 24 hours a day without human presence on the floor.

In knowledge work, the Dark Factory does not mean an organisation without humans. It means an organisation where humans are no longer in the operational loop of routine knowledge work. They are in the governance loop. They define requirements, set intent boundaries, maintain the specification corpus, resolve escalations, and architect the environments agents operate in. The work that requires human judgement is the meta-work — designing the systems that do the work.

In practice, a human team of two to five people can already supervise an agent factory of 50 to 100 specialised agents running an end-to-end process such as onboarding a customer, launching a product, or closing the books.

This is not a future projection. It is a present reality in organisations that have made the journey. The question for every organisation is not whether this will happen to their industry. It is whether they will be operating the Dark Factory or competing against organisations that are.

The competitive implications are significant. When any organisation can have agents process claims, review contracts, or close the books, proprietary data, deep domain knowledge, strength of ecosystem, and intent quality become the differentiating factors. The organisations that will win are not those with the best AI models. They will be those with the clearest organisational intent, the most rigorous specifications, and the most mature governance infrastructure.

See: [The Dark Factory — Extended Definition](../00-foundations/dark-factory.md)

---

## The Specification Discipline — The Capability That Underpins Everything

Every organisation considering this journey will encounter a moment where it discovers that its biggest problem is not the AI. The biggest problem is that it cannot describe what it wants clearly enough for an agent to do it reliably.

This is the specification problem. And it is not new. Rules engines, policy systems, workflow automation, and compliance frameworks have always required precise specification to function correctly. Organisations have always underinvested in this discipline because humans are remarkably good at filling in gaps — at interpreting ambiguous requirements charitably, at using contextual knowledge to produce the right output even when the instructions were incomplete.

Agents cannot do this. An agent executes the specification it is given with fidelity. A deterministic system — a rules engine, a policy engine — executes a bad specification consistently and at scale. A probabilistic system — an LLM agent — executes a bad specification variably and invisibly. A hybrid system, which is what the enterprise actually is, does both simultaneously.

The organisations that will successfully become AI-native are those that treat specification authorship as a core organisational discipline — not a Stage 4 concern, but a Stage 1 habit. The cost of writing a requirement precisely at Stage 1 is negligible. The cost of discovering that every specification in the organisation is too ambiguous for agents to enforce at Stage 4 is enormous.

And critically — this discipline does not require a return to waterfall. The practices of behaviour-driven development, specification by example, and spec-driven development demonstrate that precise, rigorous specifications can be written incrementally, collaboratively, and continuously. The discipline is available. The question is whether organisations choose to adopt it before or after they discover why it matters.

See: [The Specification Discipline — Three Principles](../00-foundations/specification-discipline.md)

---

## The Human Transformation — From Doing to Governing

Becoming AI-native requires a fundamental rethinking of what human work is for. This is uncomfortable. It is also unavoidable.

Research consistently shows that 75% of current knowledge work roles will need reshaping, with new or different skill mixes including more technological literacy and greater emphasis on strategic, contextual, and higher-order cognitive skills. New profiles are emerging: agent orchestrators who design and supervise agent workflows; hybrid managers who lead blended human-agent teams; domain specialists who encode their expertise into agentic systems rather than applying it directly.

The transformation is not about job elimination, though some roles will not survive. It is about role elevation. The humans who remain in an AI-native organisation are doing work that is genuinely hard — defining organisational intent with enough precision that agents can act on it, designing escalation protocols that surface the right decisions at the right time, maintaining the specification corpus as the organisation's goals evolve, architecting the environments that agents navigate.

The engineer who used to write code learns to write specifications clear enough that agents can write the code. The finance controller who used to do the reconciliation learns to govern the agents that do it. The lawyer who used to draft contracts learns to define the intent and specification envelope within which agents draft them. In every domain, the role shift is the same: from execution to governance, from doing the work to designing the systems that do it.

See: [The Human Role Transformation](../01-actors/human-role.md)

---

## The Scope — Every Domain of Knowledge Work

This framework applies to the full enterprise — not just software engineering, not just one function. Finance, Legal, HR, Procurement, Sales, Risk & Compliance, Customer Operations, R&D, and IT Operations all follow the same six-stage maturity curve. The vocabulary changes by domain. The structure does not.

Software engineering is the reference implementation because it is where the Dark Factory pattern emerged first and where the evidence base is clearest. Other domains are typically 12 to 36 months behind the software engineering frontier — which means the lessons from software engineering are directly applicable as those domains mature.

One important difference: the governance stakes outside software engineering are higher. Financial decisions, employment decisions, legal commitments, and customer-facing actions cannot be rolled back the way code can. This makes specification rigour more critical in business operations domains, not less.

See: [Enterprise Knowledge Work Map](./enterprise-knowledge-work-map.md)

---

## Why This Framework Is the Map

Most organisations approaching this journey have a technology strategy. What most organisations do not have is a maturity map — a clear picture of where they are, where they need to get to, and what they must build at each stage of the journey.

The AI Operational Maturity Framework provides that map. It answers four questions that every organisation on this journey needs answered:

**Where are we?** The maturity assessment maps an organisation's current state across technology, process, people, and governance dimensions — identifying the lowest solid layer, the genuine foundation from which progression is possible.

**What must we build next?** The stage deep dives and transition playbooks define exactly what capabilities, artefacts, and governance structures must be in place before the next stage transition is safe to make.

**What could go wrong?** The failure mode catalogue — specification gaps, intent drift, harness failure, environment ossification — gives organisations a risk register grounded in the actual failure patterns of organisations that have attempted this journey.

**What does good look like?** The worked examples show the same process at each stage of maturity across software engineering, finance, and legal domains — making the abstract concrete and giving organisations a reference point for evaluating their own progress.

---

## The Stakes

The organisations that become genuinely AI-native in the next three to five years will not simply be more efficient than their competitors. They will be operating at a fundamentally different speed, scale, and cost structure. They will be able to do in hours what their competitors do in weeks. They will be able to run processes their competitors cannot staff. They will be able to respond to market changes and regulatory shifts with a speed that legacy operating models cannot match.

The organisations that do not make this journey — or that attempt it without the disciplinary foundations this framework describes — will find themselves in an increasingly difficult position. Not immediately. The gap will open slowly, and then very quickly.

The answer, when it becomes clear, will be the same answer it always is. It was not the technology that failed. It was the absence of the organisational maturity to deploy it correctly. That is what this framework is for. Not to describe a destination. To map the journey.

---

## The Practice Premium — Where the Real Value Lives

There is a common misreading of the AI transformation story that must be named directly: becoming AI-native is not a technology procurement exercise.

The organisations that fail will, in many cases, have purchased all the right technology. They will have licensed the best LLMs, deployed the most capable agent platforms, implemented the most sophisticated harness infrastructure. And they will still fail — because they will have confused acquiring technology with developing practice.

> **The Practice Premium Principle**
>
> Technology components in the AI stack are commoditising on the standard evolution curve — available to all, differentiating to none. The durable competitive advantage lies in the organisational practice disciplines that make those technology components work: specification authoring, intent encoding, harness governance, environment design. These practices are emergent and tacit. They develop through deliberate learning, cultural change, and institutional accumulation. They cannot be purchased, licensed, or deployed from a vendor catalogue. Two organisations with identical technology stacks at Stage 4 will produce completely different outcomes because their practice maturity differs. The practice is the advantage, not the platform.

This is not a new phenomenon. It is the same story from every previous technology transition. Two companies adopted ERP systems in the 1990s with identical software. One transformed their operations. The other spent a decade in implementation chaos. The software was identical. The organisational practices around the software were not. The same pattern played out with cloud adoption, with DevOps, with data platforms. The technology became available to everyone. The practices that unlocked the technology's value remained scarce.

The AI transition is following the same curve — but faster, and with higher stakes, because the practice disciplines required are newer, less understood, and more consequential when absent.

What this means practically: the six stages of the AI Operational Maturity Framework are not a technology deployment roadmap. They are a **practice development roadmap**. Technology investment at each stage should be selected to support practice development — not the other way around. The question is never "what tools do we need?" The question is "what practice disciplines do we need to develop, and what tools will support that development?"

The practices are emergent. They build on each other. They compound over time. An organisation that has genuinely developed the specification discipline practices of Stages 1–3 arrives at Stage 4 with capabilities its competitors cannot replicate overnight by purchasing the same platform. That is where the durable advantage lives. Not in the tooling. In the learning that the tooling was acquired to enable.

---

## A Note on Urgency

If 2025 was the year enterprises learned to build with AI, 2026 is the year they must learn to operate as AI-native organisations.

The window for building the foundational disciplines — context engineering, intent encoding, specification rigour, harness design — before they are urgently needed is closing. The organisations that build these capabilities now, before the competitive pressure becomes acute, will find the transition manageable. The organisations that wait until Stage 4 is a competitive necessity will find they are trying to retrofit the foundations of a building while the upper floors are already occupied.

Stage 1 is where every organisation starts. It is also where the decisions that determine Stage 4 outcomes are made. The habit of precision, the discipline of specification, the practice of living documentation — these cost almost nothing to build at Stage 1. They cost everything to retrofit at Stage 4.

Start now. Start small. Start with the next requirement you write.

---

*Continue to: [The Maturity Curve — Visual Overview](../00-foundations/maturity-curve.md) · [Enterprise Knowledge Work Map](./enterprise-knowledge-work-map.md) · [Wardley Map — Strategic Positioning](./wardley-map.md)*  
*Back to: [README](../README.md)*

---

**End of E5-00 content.**

---

---

### 7.7 — E5-08: Wardley Map — AI Operational Maturity

**File:** `05-strategy/wardley-map.md`

**Diagrams:**
- `diagrams/wardley-technology-evolution.drawio` + `.svg` — Technology Evolution Map
- `diagrams/wardley-organisational-capability.drawio` + `.svg` — Organisational Capability Map

---

**wardley-technology-evolution diagram:**

A standard Wardley Map layout. Y-axis (vertical): "Visibility to Business Outcome" — top is visible, bottom is invisible/infrastructure. X-axis (horizontal): four evolution phases labelled left to right: **Genesis | Custom-Built | Product | Commodity/Utility**.

Components positioned approximately as follows (top to bottom, left to right reflects evolution):

```
TOP (Visible)
│
│  Business Outcomes (Knowledge Work Delivered)          [anchored top-centre]
│       │
│  AI-Native Operations / Dark Factory                   [custom-built, upper]
│       │
│  Agent Workflows (domain-specific)                     [custom → product]
│       │
│  Agent Orchestration / Harness                         [custom → product]
│       │
│  Specification Corpus                                   [genesis → custom]
│       │
│  Context Pipelines / RAG                               [custom → product]
│       │
│  LLM Foundation Models                                 [product → commodity]
│       │
│  Vector Databases / Embeddings                         [product → commodity]
│       │
│  Cloud / Compute Infrastructure                        [commodity → utility]
│
BOTTOM (Invisible/Infrastructure)
│◄──────────────────────────────────────────────────────────►
Genesis    Custom-Built     Product      Commodity/Utility
```

Draw components as circles. Connect them with dependency lines (solid arrows pointing from dependent to dependency — top components depend on lower ones). Add an **inertia marker** (double vertical bars ∥) on "LLM Foundation Models" to indicate this is where many organisations are over-investing despite rapid commoditisation. Add a **movement arrow** (→) on LLM Foundation Models pointing right to show commoditisation direction. Add a dashed red box around the upper-left quadrant (genesis/custom-built, upper half) labelled "Current competitive advantage zone." Title: "Technology Evolution — AI Operational Maturity." Use the standard dark factory colour palette — dark background for the map itself with gold axis labels.

---

**wardley-organisational-capability diagram:**

Same Wardley Map layout. This map shows *organisational capabilities* rather than technology components.

```
TOP (Visible to Business Value)
│
│  AI-Native Enterprise (Competitive Advantage)          [anchored top-centre]
│       │
│  Environment Engineering capability                    [genesis]
│       │
│  Harness Engineering capability                        [genesis → custom]
│       │
│  Specification Engineering capability                  [genesis → custom]
│       │
│  Intent Engineering capability                         [genesis → custom]
│       │
│  Agent Governance capability                           [genesis → custom]
│       │
│  Context Engineering capability                        [custom → product]
│       │
│  Prompt Engineering capability                         [product → commodity]
│       │
│  AI Tool Access / Licences                             [commodity → utility]
│
BOTTOM (Invisible/Infrastructure)
│◄──────────────────────────────────────────────────────────►
Genesis    Custom-Built     Product      Commodity/Utility
```

Add an **inertia marker** on "Prompt Engineering capability" — this is where most enterprise investment is currently concentrated, despite commoditisation. Add a **movement arrow** on Prompt Engineering pointing right. Add a dashed red box around the upper-left zone (genesis/custom-built, upper half) labelled "Where investment should be flowing." Add a separate dashed amber box around the lower-right zone (product/commodity, lower half) labelled "Where most enterprises are currently investing." Add the six maturity stage labels as an overlay on the left side:

- Stage 1 (Prompt Eng.) — aligns with Prompt Engineering capability row
- Stage 2 (Context Eng.) — aligns with Context Engineering row
- Stage 3 (Intent Eng.) — aligns with Intent Engineering row
- Stage 4 (Spec. Eng.) — aligns with Specification Engineering row
- Stage 5 (Harness Eng.) — aligns with Harness Engineering row
- Stage 6 (Env. Eng.) — aligns with Environment Engineering row

Title: "Organisational Capability Evolution — AI Operational Maturity." This is the most strategically important diagram in the entire framework — the visual proof that most organisations are investing in the wrong layer.

---

**File header:**
```markdown
> **E5-08 · Strategy · Wave 2**  
> Wardley Maps showing technology evolution and organisational capability 
> evolution for AI operational maturity — revealing where competitive 
> advantage is being created and where most enterprises are misallocating investment.  
> See also: [Vision Narrative](./vision-ai-native.md) · 
> [Maturity Curve](../00-foundations/maturity-curve.md) · 
> [Enterprise Knowledge Work Map](./enterprise-knowledge-work-map.md)
```

**Content structure:**

1. **Why Wardley Mapping** — one short paragraph. Wardley Maps make strategic positioning visible by combining value chain (what depends on what) with evolutionary stage (how mature each component is). Unlike most strategy tools, they reveal not just current state but inevitable direction — which is exactly what AI operational maturity strategy requires.

2. **How to read these maps** — a brief primer for readers unfamiliar with Wardley Maps. Three things to know: components higher on the Y-axis are more visible to business outcomes; components further right on the X-axis are more evolved/commoditised; dependency arrows flow downward; components naturally move rightward over time regardless of organisational intent.

3. **Map 1 — Technology Evolution** — introduce the first diagram (linked SVG). Three analytical paragraphs:
   - What the map shows: LLM models and cloud infrastructure are commoditising rapidly. The competitive advantage zone is in the upper-left — agent workflows, orchestration, specification corpus. These are still in genesis or custom-built.
   - The inertia problem: most organisations are over-investing in LLM model selection (product/commodity boundary) while under-investing in the layers above it.
   - The strategic implication: as LLMs commoditise, the value migrates upward. Organisations that have built specification corpus, harness, and agent workflow capabilities will compound that advantage. Those who haven't will find that commodity LLMs give them nothing to differentiate with.

4. **Map 2 — Organisational Capability Evolution** — introduce the second diagram (linked SVG). Three analytical paragraphs:
   - What the map shows: Prompt Engineering is commoditising as a *capability*, not just as a technology. The ability to write a good prompt is being embedded in platforms, templates, and AI assistants. Differentiation here is evaporating.
   - The investment gap: the amber box (where most enterprises are investing) and the red box (where they should be investing) are in entirely different quadrants. This is the strategic misalignment the framework addresses.
   - The maturity framework alignment: the six maturity stages map directly onto this capability evolution chart. Stage 1 = prompt engineering (commodity). Stage 6 = environment engineering (genesis). Progressing through the stages is the act of building capabilities in the right order, moving up and left on this map.

5. **Doctrine alignment** — a table showing how Wardley's universal doctrines apply to the framework:

| Wardley Doctrine | Application to AI Operational Maturity |
|---|---|
| Optimise flow | The Dark Factory is the ultimate expression — remove all friction from requirement to outcome |
| Use appropriate methods | Apply the method appropriate to your current stage; don't impose Stage 5 discipline on a Stage 1 team |
| Move fast where stable | Prompt Engineering is stable and commoditising — adopt best practice and move on |
| Move carefully where volatile | Harness Engineering patterns are still forming — build carefully, contribute to emerging standards |
| Avoid inertia | Success at Stage 2 creates resistance to Stage 3 investment — name it and plan for it |
| Think small teams | The agentic organisation is structurally flatter — agents absorb the coordination overhead that required large teams |

6. **Climatic patterns** — four named patterns relevant to the framework, each in one paragraph:
   - **Everything evolves** — LLM capability will commoditise. Specification corpus tooling will productise. The question is when, and what you build before it does.
   - **Efficiency enables innovation** — commoditised models enable organisational innovation at the Dark Factory layer. The commoditisation of AI is not a threat; it is the precondition for the next wave of competitive advantage.
   - **Capital flows to new value** — investment is already leaving prompt tooling and flowing to harness engineering, context engines, and agent governance. Read this signal and move ahead of the flow.
   - **Inertia increases with success** — organisations successful at Stage 1–2 will resist the Stage 3→4 transition. The Wardley Map makes this resistance legible — and therefore addressable.

7. **Gameplay table** — the strategic moves appropriate to each maturity stage:

| Stage | Wardley Position | Appropriate Gameplay |
|---|---|---|
| Stage 1 — Prompt Eng. | Commodity/Product | **Standardise** — don't differentiate here; adopt best practice fast and move up |
| Stage 2 — Context Eng. | Custom → Product | **Build for scale** — invest in context architecture now before it productises |
| Stage 3 — Intent Eng. | Genesis → Custom | **Pioneer** — there are no playbooks yet; build, document, and share your own |
| Stage 4 — Spec. Eng. | Genesis | **Land grab** — organisations that master specification corpus design now will hold durable advantage |
| Stage 5 — Harness Eng. | Genesis | **Ecosystem play** — contribute to emerging harness standards; help shape commoditisation on your terms |
| Stage 6 — Env. Eng. | Genesis | **Architectural bet** — redesign your environment before competitors redesign theirs |

8. **The two most important insights** — formatted as named blockquotes:

> **The Strategic Misalignment Principle**
>
> The components most organisations are investing in are commoditising. The components that will determine competitive position in three to five years are still in genesis. The gap between where most organisations are investing and where they should be investing is precisely the gap the AI Operational Maturity Framework is designed to close. A Wardley Map makes this misalignment visible in a single diagram. The maturity framework provides the path to correct it.

> **The Practice Premium Principle**
>
> Technology components in the AI stack commoditise on the standard Wardley curve — available to all, differentiating to none. The durable competitive advantage lies in the organisational practice disciplines that make those components work: specification authoring, intent encoding, harness governance, environment design. These practices are emergent and tacit. They develop through deliberate learning and institutional accumulation. They cannot be purchased or licensed. Two organisations with identical technology stacks at Stage 4 will produce different outcomes because their practice maturity differs. The practice is the advantage, not the platform.

**Diagram annotation note for Map 2:** The Organisational Capability Map should visually distinguish between *technology capability* (labelled with a "T" marker, moves right at standard Wardley pace) and *practice capability* (labelled with a "P" marker, moves more slowly due to tacit knowledge and cultural change requirements). Add a legend explaining this distinction. Practice capabilities should have a slower movement arrow (shorter) than technology capabilities to visually represent their stickiness. This distinction is the key insight that separates the framework from technology-centric maturity models.

9. **Navigation links**

---

## 8. Execution Order

Execute all tasks in this exact sequence:

1. ✅ Read this brief completely before writing any file
2. 🔧 Fix `glossary.md` — name update + two new entries
3. 🔧 Fix `maturity-curve.md` — name update + link fixes + two additions
4. 📝 Rewrite `README.md` (uppercase) — full rewrite per Section 4
5. 📝 Create `BACKLOG.md` — per Section 5
6. 📝 Create `00-foundations/dark-factory.md` + 2 diagrams — per Section 7.1
7. 📝 Create `00-foundations/reader-guide.md` — per Section 7.2
8. 📝 Create `00-foundations/cumulative-stack.md` + 1 diagram — per Section 7.3
9. 📝 Create `00-foundations/specification-discipline.md` + 2 diagrams — per Section 7.4
10. 📝 Create `05-strategy/vision-ai-native.md` — per Section 7.6 (no diagrams)
11. 📝 Create `05-strategy/wardley-map.md` + 2 diagrams — per Section 7.7
12. 📝 Create `05-strategy/enterprise-knowledge-work-map.md` + 2 diagrams — per Section 7.5
13. 🔍 Final check — verify all internal links are relative, all diagrams are linked not embedded, framework name is consistent throughout

---

## 9. Quality Checks — Before Committing

Run these checks on every file before committing:

- [ ] Framework name is "AI Operational Maturity Framework" throughout
- [ ] All internal links use relative paths
- [ ] Every `.md` file has the correct header block (ID · Epic · Wave)
- [ ] Every diagram referenced exists as both `.drawio` and `.svg` in `/diagrams/`
- [ ] Diagrams are linked, not embedded inline
- [ ] Colour palette matches the standard in Section 2
- [ ] No absolute GitHub URLs in any file
- [ ] BACKLOG.md status reflects actual state of files
- [ ] The three named principles appear consistently wherever referenced: **Specification Debt Principle**, **Strategic Misalignment Principle**, **Practice Premium Principle**

---

## 10. Authoring Notes — Future Items

These notes apply to backlog items not yet being written but whose content direction has been decided. Store these so the correct framing is applied when those items are executed.

### E5-03 — Investment & Roadmap Planning Guide (Wave 7)

**Critical framing note:** This document must NOT be written as a technology procurement roadmap. The Practice Premium Principle must anchor its opening. The central reframe is:

> The investment question is never "what tools do we need?" The question is "what practice disciplines do we need to develop, and what tools will support that development?"

The document should structure investment planning as a **practice development roadmap** in which:
- Each stage of the maturity framework represents a practice investment, not a technology purchase
- Technology spending at each stage is justified by and calibrated to the practice it enables
- ROI is measured in practice maturity gain, not tool deployment
- The roadmap explicitly names which practices must precede which technology investments

The document should include a table structured as:

| Stage | Practice to Develop | Practice Indicators (how you know it's real) | Technology That Supports It | What to Avoid Buying Before the Practice Exists |
|---|---|---|---|---|

This framing is a genuine differentiator from all other AI investment frameworks in the market, which are universally tool-centric. It is also more defensible with CFOs and boards who are rightly sceptical of technology investment claims.

### E5-00 — Vision Narrative (Wave 2, already specified in Section 7.6)

**Additional note:** The Practice Premium Principle section has been added to the narrative content in Section 7.6. Ensure it appears between "The Stakes" and "A Note on Urgency" sections as specified.

### E5-08 — Wardley Map (Wave 2, already specified in Section 7.7)

**Additional note:** The Organisational Capability Map (second diagram) must visually distinguish between technology capability components (T marker, standard rightward movement) and practice capability components (P marker, slower movement arrow). This distinction is the key visual insight that separates the framework from technology-centric maturity models. See Section 7.7 diagram annotation note for full specification.

---

*End of brief. All questions or clarifications should be raised before execution begins.*
