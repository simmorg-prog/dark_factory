# AI Operational Maturity Framework

> A six-stage maturity model for AI-operated workflow — from prompt engineering to environment engineering. Applicable to software delivery and all enterprise knowledge work.

**New to this framework?** Start with the strategic narrative: [The AI-Native Organisation — Vision Narrative](./05-strategy/vision-ai-native.md)

---

## The Six Stages

Each stage subsumes the one before it. You cannot skip stages.

| Stage | Discipline | CMMI Analogue | Entry point |
|---|---|---|---|
| 1 | **Prompt Engineering** | L1 — Initial | A single human, one model, one response |
| 2 | **Context Engineering** | L2 — Managed | Systematic management of what the model sees |
| 3 | **Intent Engineering** | L3 — Defined | Encoding organisational goals into agent infrastructure |
| 4 | **Specification Engineering** | L4 — Quant. Managed | Policy-as-code; entry to the Dark Factory |
| 5 | **Harness Engineering** | L5 — Optimising | The runtime envelope: everything that isn't the model |
| 6 | **Environment Engineering** | L6 — Transcending | Re-architecting the world the agent operates in |

---

## The Dark Factory

> Stages 4–6. Human involvement is exception-based only.

The Dark Factory is the operational mode in which agents own the full workflow — design, implementation, testing, review, deployment. Humans define requirements, set intent boundaries, resolve escalations, and govern the systems agents operate within. They are not in the operational loop of routine work.

See: [The Dark Factory — Extended Definition](./00-foundations/dark-factory.md)

---

## Scope

This framework applies to two domains:

**Software Engineering** — the reference implementation. The Dark Factory pattern emerged first in software delivery and provides the clearest evidence base for all six stages.

**Enterprise Knowledge Work** — Finance, Legal, HR, Procurement, Sales & Marketing, Risk & Compliance, Customer Operations, R&D, IT Operations, and Supply Chain. The same six stages apply. The vocabulary changes. The structure does not.

See: [Enterprise Knowledge Work Map](./05-strategy/enterprise-knowledge-work-map.md)

---

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

---

## Content Status

### Wave 1 — Foundations

| ID | Title | Status |
|---|---|---|
| E1-01 | [Glossary of Terms](./00-foundations/glossary.md) | ✅ Complete |
| E1-02 | [Maturity Curve — Visual Overview](./00-foundations/maturity-curve.md) | ✅ Complete |
| E1-03 | [Reader Guide](./00-foundations/reader-guide.md) | ✅ Complete |
| E1-04 | [The Cumulative Stack Explained](./00-foundations/cumulative-stack.md) | ✅ Complete |
| E1-05 | [The Dark Factory — Extended Definition](./00-foundations/dark-factory.md) | ✅ Complete |
| E1-06 | [The Specification Discipline — Three Principles](./00-foundations/specification-discipline.md) | ✅ Complete |
| E1-07 | [Specification Quality Standard](./00-foundations/specification-quality-standard.md) | ✅ Complete |
| E1-08 | [LANGUAGE.md — Structural Vocabulary](./00-foundations/LANGUAGE.md) | 🔜 To Do |

### Wave 2 — Scope & Strategy

| ID | Title | Status |
|---|---|---|
| E5-00 | [The AI-Native Organisation — Vision Narrative](./05-strategy/vision-ai-native.md) | ✅ Complete |
| E5-08 | [Wardley Map — AI Operational Maturity](./05-strategy/wardley-map.md) | ✅ Complete |
| E5-07 | [Enterprise Knowledge Work Map](./05-strategy/enterprise-knowledge-work-map.md) | ✅ Complete |
| E5-01a | [Maturity Assessment — Framework Design](./05-strategy/maturity-assessment-framework.md) | ✅ Complete |
| E5-01b | [Maturity Assessment — Instrument & Tool](./05-strategy/maturity-assessment-tool.md) | ✅ Complete |
| E3-01 | [The Human Role Transformation](./01-actors/human-role.md) | ✅ Complete |
| E3-06 | [Human-Agent Handoff Protocols](./01-actors/handoff-protocols.md) | ✅ Complete |
| E3-03 | [Agent Council Design — Constitution & Governance](./01-actors/agent-council-design.md) | ✅ Complete |

### Wave 3 — Actors

| ID | Title | Status |
|---|---|---|
| E3-02 | [Agent Taxonomy — Types, Capabilities, Limitations](./01-actors/agent-taxonomy.md) | ✅ Complete |
| E3-04 | [Agent Council Patterns](./01-actors/agent-council-patterns.md) | ✅ Complete |
| E3-05 | [The Meta-Council — Cross-Domain Arbitration](./01-actors/meta-council.md) | ✅ Complete |

### Wave 4 — Artefacts

| ID | Title | Status |
|---|---|---|
| E4-00 | [Specification Examples — Reference Library](./02-artefacts/specification-examples.md) | ✅ Complete |
| E4-01 | [Artefact Catalogue — All Stages](./02-artefacts/artefact-catalogue.md) | ✅ Complete |
| E4-02 | [Requirements Specification Templates](./02-artefacts/requirements-spec-templates.md) | ✅ Complete |
| E4-03 | [Intent Manifest — Reference Design](./02-artefacts/intent-manifest.md) | ✅ Complete |
| E4-04 | [Specification Corpus — Architecture & Governance](./02-artefacts/specification-corpus.md) | ✅ Complete |
| E4-05 | [Escalation Package Standard](./02-artefacts/escalation-package-standard.md) | ✅ Complete |
| E4-06 | [Environment Map — Reference Design](./02-artefacts/environment-map.md) | ✅ Complete |

### Wave 5 — Stage Overviews

| ID | Title | Status |
|---|---|---|
| E2-07 | [Stage Transition Playbooks (1→2, 2→3, 3→4, 4→5, 5→6)](./03-stages/stage-transition-playbooks.md) | ✅ Complete |
| E2-01 | [Stage 1 Deep Dive — Prompt Engineering](./03-stages/stage-1-prompt-engineering.md) | ✅ Complete |
| E2-02 | [Stage 2 Deep Dive — Context Engineering](./03-stages/stage-2-context-engineering.md) | ✅ Complete |
| E2-03 | [Stage 3 Deep Dive — Intent Engineering](./03-stages/stage-3-intent-engineering.md) | ✅ Complete |
| E2-04 | [Stage 4 Deep Dive — Specification Engineering](./03-stages/stage-4-specification-engineering.md) | ✅ Complete |
| E2-05 | [Stage 5 Deep Dive — Harness Engineering](./03-stages/stage-5-harness-engineering.md) | ✅ Complete |
| E2-06 | [Stage 6 Deep Dive — Environment Engineering](./03-stages/stage-6-environment-engineering.md) | ✅ Complete |

### Wave 6 — Worked Examples

| ID | Title | Status |
|---|---|---|
| E6-01 | [Worked Example: Feature Delivery at Each Stage](./04-examples/feature-delivery-worked-example.md) | ✅ Complete |
| E6-02 | [Worked Example: Incident Response at Each Stage](./04-examples/incident-response-worked-example.md) | ✅ Complete |
| E6-03 | [Anti-Patterns Library](./04-examples/anti-patterns.md) | ✅ Complete |
| E6-04 | [The Stage 3→4 Transition in Detail](./04-examples/stage-3-4-transition.md) | ✅ Complete |
| E6-05 | [Dark Factory Operating Model](./04-examples/dark-factory-operating-model.md) | ✅ Complete |
| E6-06 | [Worked Example: Finance Month-End Close at Each Stage](./04-examples/finance-month-end-worked-example.md) | ✅ Complete |
| E6-07 | [Worked Example: Legal Contract Review at Each Stage](./04-examples/legal-contract-review-worked-example.md) | ✅ Complete |

### Wave 7 — Organisational & Strategic

| ID | Title | Status |
|---|---|---|
| E5-01a | [Maturity Assessment — Framework Design](./05-strategy/maturity-assessment-framework.md) | ✅ Complete |
| E5-01b | [Maturity Assessment — Instrument & Tool](./05-strategy/maturity-assessment-tool.md) | ✅ Complete |
| E5-02 | [The Engineering Team of the Future](./05-strategy/engineering-team-future.md) | ✅ Complete |
| E5-03 | [Investment & Roadmap Planning Guide](./05-strategy/investment-roadmap.md) | ✅ Complete |
| E5-04 | [Risk Register — Across All Stages](./05-strategy/risk-register.md) | ✅ Complete |
| E5-05 | [AI Governance in the Dark Factory](./05-strategy/ai-governance.md) | ✅ Complete |
| E5-06 | [Vendor & Tooling Landscape](./05-strategy/vendor-tooling-landscape.md) | ✅ Complete |

### Wave 8 — Maintenance & Vocabulary

| ID | Title | Status |
|---|---|---|
| E1-08 | [LANGUAGE.md — Structural Vocabulary](./00-foundations/LANGUAGE.md) | 🔜 To Do |
| E1-01-FIX | Glossary — 4 missing entries (Atomic Specification Unit, Proxy Discrimination, Conflict Detection, RFC 8174) | ✅ Complete |

---

*This framework is developed iteratively. See [BACKLOG.md](./BACKLOG.md) for the full item list and execution sequence.*
