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
| E1-05 | [The Dark Factory — Extended Definition](./00-foundations/dark-factory.md) | ✅ Complete |
| E1-03 | [Reader Guide](./00-foundations/reader-guide.md) | ✅ Complete |
| E1-04 | [The Cumulative Stack Explained](./00-foundations/cumulative-stack.md) | ✅ Complete |
| E1-06 | [The Specification Discipline — Three Principles](./00-foundations/specification-discipline.md) | 🔜 Pending |

### Wave 2 — Scope & Strategy

| ID | Title | Status |
|---|---|---|
| E5-00 | [The AI-Native Organisation — Vision Narrative](./05-strategy/vision-ai-native.md) | ✅ Complete |
| E5-08 | [Wardley Map — AI Operational Maturity](./05-strategy/wardley-map.md) | 🔜 Pending |
| E5-07 | [Enterprise Knowledge Work Map](./05-strategy/enterprise-knowledge-work-map.md) | 🔜 Pending |
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
| E4-01 | [Artefact Catalogue — All Stages](./02-artefacts/artefact-catalogue.md) | ✅ Complete |
| E4-02 | [Requirements Specification Templates](./02-artefacts/requirements-spec-templates.md) | ✅ Complete |
| E4-05 | [Escalation Package Standard](./02-artefacts/escalation-package-standard.md) | ✅ Complete |
| E4-03 | [Intent Manifest — Reference Design](./02-artefacts/intent-manifest.md) | ✅ Complete |
| E4-04 | [Specification Corpus — Architecture & Governance](./02-artefacts/specification-corpus.md) | ✅ Complete |
| E4-06 | [Environment Map — Reference Design](./02-artefacts/environment-map.md) | ✅ Complete |

### Waves 5–7 — Pending

See [BACKLOG.md](./BACKLOG.md) for the full item list and execution sequence.

---

*This framework is developed iteratively. See [BACKLOG.md](./BACKLOG.md) for the full item list and execution sequence.*
