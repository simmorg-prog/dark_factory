# AI Engineering Maturity Framework

> A cumulative, six-stage model for engineering AI systems — from ad-hoc prompt use to fully autonomous, agent-operated software delivery.

**New to this framework?** Start with the strategic narrative: [The AI-Native Organisation — A Vision](./05-strategy/vision-ai-native.md)

---

## The Six Disciplines

Each stage subsumes the one before it. You cannot skip stages.

| Stage | Discipline | CMMI Analogue | Entry point |
|---|---|---|---|
| 1 | **Prompt Engineering** | L1 — Initial | A single human, one model, one response |
| 2 | **Context Engineering** | L2 — Managed | Systematic management of what the model sees |
| 3 | **Intent Engineering** | L3 — Defined | Encoding organisational goals into agent infrastructure |
| 4 | **Specification Engineering** | L4 — Quant. Managed | Policy-as-code; entry to the Dark Factory |
| 5 | **Harness Engineering** | L5 — Optimising | The runtime envelope: everything that isn't the model |
| 6 | **Environment Engineering** | L6 — Transcending | Re-architecting the world the agent operates in |

> **The Dark Factory** begins at Stage 4. Humans provide requirements and intent boundaries; agents own the full engineering workflow.

---

## Repository Structure

```
00-foundations/      Core concepts, glossary, maturity curve
01-actors/           Human, Agent, and Agent Council design patterns
02-artefacts/        Specification corpus, escalation packages, requirements templates
03-stages/           Stage deep dives and transition playbooks
04-examples/         Worked examples and anti-patterns
05-strategy/         Organisational and strategic guidance
diagrams/            Draw.io sources and exported SVGs
```

---

## Wave 1 — Foundations

| ID | Title | Status |
|---|---|---|
| E1-01 | [Glossary of Terms](./00-foundations/glossary.md) | ✅ Complete |

---

*This framework is developed iteratively. Wave 1 establishes the foundational vocabulary. Later waves build out actor design, artefact standards, harness patterns, and environment architecture.*
