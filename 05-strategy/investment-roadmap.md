# Investment & Roadmap Planning Guide

*E5-03 · Wave 7 — Strategy · Audience: Technology Leaders, CFOs, Strategy Teams*

> See also: [Maturity Assessment Framework](./maturity-assessment-framework.md) · [Maturity Assessment Tool](./maturity-assessment-tool.md) · [Vendor & Tooling Landscape](./vendor-tooling-landscape.md) · [The Engineering Team of the Future](./engineering-team-future.md)

---

## Opening Principle

> **The Practice Premium Principle:** Technology commoditises. What does not commoditise is the organisational discipline to use it. At every stage of the AI Operational Maturity Framework, the durable competitive advantage lies not in which tools are deployed but in how consistently and deliberately the practices of that stage are applied.

Most AI investment roadmaps are technology procurement sequences. They are built around decisions about which platforms to license, which APIs to integrate, and which infrastructure to deploy. They treat the technology decision as the primary decision and the practice development as something that will follow naturally.

It will not follow naturally. Practice development is slower than technology procurement, more expensive in organisational terms, and more dependent on human capability development. An organisation that procures Stage 4 infrastructure without developing Stage 4 practices has purchased a more expensive Stage 2 system.

This guide is a practice development roadmap. Technology decisions appear in it — but as the secondary decision, made after the practice requirements are understood, not before.

---

## How to Use This Guide

**Step 1 — Know your Effective Stage.** Use the [Maturity Assessment Tool](./maturity-assessment-tool.md) before making any roadmap decisions. Investment decisions made without a current, honest maturity assessment are investment decisions made in the dark.

**Step 2 — Read the guide for your current Effective Stage.** The investment logic at each stage is different. The guide is not read linearly — it is read from the current position outward.

**Step 3 — Apply the lowest-solid-layer rule.** No investment in Stage N+1 until Stage N is solid. This is not conservatism; it is the logic of cumulative stacks. Stage N+1 technology running on a Stage N−1 practice foundation performs at Stage N−1.

**Step 4 — Sequence practice before technology.** At each stage, the practice development investment precedes the technology investment. The technology enables and accelerates practice; it cannot substitute for it.

---

## The Investment Logic at Each Stage

### Stage 0 → Stage 1: Prompt Engineering

**What solid Stage 1 looks like:** A shared prompt library maintained as a team asset, governed prompts for production workflows, prompt craft transferable across team members, and a data-sharing policy that defines what may be sent to external model APIs.

**The practice to develop first:** Prompt craft and prompt governance. Before licensing any tool, the team must understand what makes a prompt effective and how to maintain prompts as durable assets rather than ephemeral personal notes.

**What not to buy before the practice exists:**
- Enterprise prompt management platforms (without a prompt library practice, the platform stores what would otherwise be personal notes)
- Fine-tuning infrastructure (before the base model is being used effectively)
- RAG pipelines (before the team has mastered prompt formulation for the retrieval results they will receive)

**Technology investment sequence:** Model API access (necessary) → shared workspace for prompt storage (lightweight) → usage monitoring (for cost governance)

**Practice development investment:** Prompt craft training, prompt review process design, acceptable use policy development.

---

### Stage 1 → Stage 2: Context Engineering

**What solid Stage 2 looks like:** Context schemas documented for primary workflows, retrieval quality measured with a defined baseline, named owners for each major content category, context budgets enforced, and a knowledge base maintained as a governed asset.

**The practice to develop first:** Knowledge architecture. Before deploying retrieval infrastructure, the team must understand what information each workflow actually needs — defined in a context schema — and how to maintain it. A retrieval pipeline without a context schema retrieves what is available, not what is required.

**What not to buy before the practice exists:**
- Enterprise vector database (before context schemas exist and retrieval quality is understood)
- Knowledge management platforms (before ownership and freshness governance are designed)
- Semantic search infrastructure (before the team can measure whether it is retrieving the right content)

**Technology investment sequence:** Retrieval pipeline (RAG or structured query, matched to schema requirements) → knowledge base storage → retrieval quality monitoring → freshness alert tooling

**Practice development investment:** Context schema workshops per primary workflow, knowledge base ownership design, freshness SLA definition, retrieval quality measurement training.

---

### Stage 2 → Stage 3: Intent Engineering

**What solid Stage 3 looks like:** An intent manifest formally owned, actively maintained, and verifiably influencing agent decisions. Intent clauses written in testable language. An update process that has been exercised following a real strategy change. Intent drift detection operational.

**The practice to develop first:** Intent authorship. This is the hardest Stage 3 capability to develop. Writing an intent manifest clause that is specific enough to govern agent decisions — rather than aspirational enough to feel good — requires a combination of domain expertise, structured writing discipline, and understanding of what agents can and cannot apply. This skill does not emerge from deploying a platform.

**What not to buy before the practice exists:**
- Intent management platforms (without intent authorship capability, the platform stores aspirational prose that agents cannot reliably apply)
- Strategy encoding automation (before humans can write intent clauses manually)
- LLM orchestration frameworks with intent-injection features (before the intent is well-formed enough to inject)

**Technology investment sequence:** Version control for the intent manifest (lightweight — this is a document) → manifest injection tooling → intent audit tooling (agent decision tracing)

**Practice development investment:** Intent authorship training and facilitated workshops, strategy-to-manifest translation exercises, intent audit process design, intent ownership assignment with domain authority sign-off.

**Critical implication:** Intent manifest ownership cannot be delegated entirely to engineering. Stage 3 investment requires commitment from the domain authority — the people who can speak to what the organisation actually intends — not just the technical team.

---

### Stage 3 → Stage 4: Specification Engineering

**What solid Stage 4 looks like:** ≥80% corpus coverage of the target workflow's decisions (measured), all five specification disciplines applied to all corpus entries, automated conflict detection operational, a formal admission process functioning, an immutable audit trail in place, and an escalation system with proven SLA compliance.

**The practice to develop first:** Specification craft. Writing atomic, testable, conflict-free specification clauses using RFC 8174 normative precision is a discipline that requires training and practice. The first specification corpus entry a team writes will not be production-quality. The team needs at least six months of deliberate practice before the corpus is ready for autonomous enforcement.

**What not to buy before the practice exists:**
- Enterprise specification management platforms (without specification craft, the platform stores prose policies that are not machine-enforceable)
- Policy-as-code infrastructure (OPA/Rego, Cedar) before the team can write atomic specification clauses manually
- Automated specification generation (LLM-assisted corpus entry creation before the team can review and validate machine-generated entries against quality standards)
- Corpus governance platforms (without an admission process design, the platform is a storage system with no governance value)

**Technology investment sequence:** Specification quality standards adoption → structured specification templates → version control with conflict detection → policy-as-code infrastructure (OPA/Rego) → audit trail infrastructure → escalation routing system

**Practice development investment:** Specification craft training (the five disciplines), corpus review process design, escalation package standard training, audit trail specification, coverage measurement methodology, corpus admission process design.

**Stage 3 → 4 gating condition:** The organisation should not invest in Stage 4 infrastructure until the intent manifest is solid (Stage 3 P-Score ≥1.5). Specification corpus entries derive their authority from intent manifest clauses. A corpus without a manifest parent is orphaned specification — rules without rationale, which cannot be updated coherently when strategy changes.

---

### Stage 4 → Stage 5: Harness Engineering

**What solid Stage 5 looks like:** A comprehensive harness covering all production agents, behavioural baselines established and maintained, self-healing playbooks deployed and operational (not just designed), MTTD within defined targets for three consecutive review periods, and harness governance independent of the operational teams it monitors.

**The practice to develop first:** Behavioural baseline design. Before deploying monitoring infrastructure, the team must understand what normal looks like for each agent in each context. A harness that monitors without a baseline cannot distinguish anomaly from variation. Baseline design requires operational data — which means the Stage 4 system must operate for a period before Stage 5 harness investment is appropriate.

**What not to buy before the practice exists:**
- Enterprise AIOps or MLOps platforms (without behavioural baselines, the platform alerts on everything or nothing)
- Self-healing automation frameworks (before playbooks are designed, tested, and approved by governance)
- Anomaly detection infrastructure (before the team can define what anomalous looks like for their agents)
- Harness governance tools (before harness independence is structurally established)

**Technology investment sequence:** Operational logging (prerequisite) → behavioural baseline measurement tooling → anomaly detection → alert routing → playbook execution infrastructure → MTTD/MTTR measurement

**Practice development investment:** Baseline design workshops per agent type, anomaly threshold calibration, playbook design and approval process, MTTD governance design, harness independence design (organisational structure), playbook rehearsal exercises.

**Stage 4 → 5 gating condition:** The Dark Factory must have operated at Stage 4 for long enough to establish behavioural baselines before Stage 5 investment makes sense. Deploying harness infrastructure before baselines exist produces harness theatre — monitoring dashboards with no diagnostic value.

---

### Stage 5 → Stage 6: Environment Engineering

**What solid Stage 6 looks like:** An environment map published and maintained, machine-readable API contracts for ≥50% of agent-consumed APIs, an Environment Council constituted with defined mandate and blocking authority, at least one legacy system redesigned for AI legibility with documented improvement, and a legacy redesign programme active with prioritised targets.

**The practice to develop first:** Environment mapping. Before establishing the Environment Council or beginning redesign programmes, the team must understand what the environment currently looks like — all APIs, data sources, legacy systems, and external dependencies that agents interact with. The environment map is the prerequisite for all subsequent Stage 6 work.

**What not to buy before the practice exists:**
- API gateway infrastructure for AI routing (before the environment is mapped and the routing requirements understood)
- Legacy modernisation platforms (before the AI legibility standard is defined and the target systems are assessed against it)
- Service mesh tooling for AI traffic (before the environment map identifies what traffic patterns exist and what they require)

**Technology investment sequence:** Environment mapping tooling → API contract tooling (OpenAPI, AsyncAPI) → environment health monitoring → legacy redesign tooling (matched to specific target systems)

**Practice development investment:** Environment mapping methodology, AI legibility standard definition, Environment Council constitution design, legacy assessment process design, environment review cadence design.

---

## The Master Practice-Technology Table

For each stage, the practice must precede the technology. This table is the planning instrument.

| Stage | Practice to Develop | Practice Indicators (Observable Evidence) | Technology That Supports It | What NOT to Buy Before Practice Exists |
|---|---|---|---|---|
| 1 — Prompt Engineering | Prompt craft and governance | Shared prompt library; governed production prompts; transferable craft | Model API; shared workspace; usage monitoring | Enterprise prompt platforms; fine-tuning infra; RAG pipelines |
| 2 — Context Engineering | Knowledge architecture and retrieval quality | Context schemas per workflow; retrieval metrics with baseline; named freshness owners | RAG pipeline; knowledge base; retrieval quality monitoring | Enterprise vector DB; knowledge management platforms; semantic search |
| 3 — Intent Engineering | Intent authorship and manifest governance | Testable intent clauses; manifest update process exercised; agent decisions traceable to clauses | Version control; manifest injection tooling; decision audit | Intent management platforms; strategy encoding automation; orchestration with intent injection |
| 4 — Specification Engineering | Specification craft and corpus governance | Five disciplines applied; ≥80% coverage; admission process functioning; escalations resolved with corpus extension | Policy-as-code (OPA/Rego); audit trail; escalation routing | Enterprise spec platforms; policy-as-code infra; corpus governance platforms; automated spec generation |
| 5 — Harness Engineering | Behavioural baseline design and harness governance | Baselines established; MTTD on target for 3 periods; playbook fired and resolved anomaly; harness independence in place | Anomaly detection; alert routing; playbook execution; MTTD measurement | Enterprise AIOps; self-healing frameworks; anomaly detection (without baselines) |
| 6 — Environment Engineering | Environment mapping and legibility standard | Map published and maintained; ≥50% API contracts; Council constituted with blocking authority; one legacy redesign completed | Environment mapping tooling; API contract tooling; environment health monitoring | API gateways for AI routing; legacy modernisation platforms; service mesh tooling |

---

## Sizing the Investment

AI operational maturity investment divides into four categories. The ratio between them shifts across stages in a consistent pattern.

**Category 1 — Technology (platform licenses, infrastructure):** Decreases as a share of total investment as stages advance. Technology commoditises; practice does not. At Stage 1, technology is the dominant cost. At Stage 5, practice development and governance are.

**Category 2 — Practice development (training, workshops, facilitation):** Increases across stages. Writing specification corpus entries requires more training than writing prompts. Designing behavioural baselines requires more expertise than designing context schemas.

**Category 3 — Governance design (process, roles, accountability structures):** Increases sharply from Stage 3 onward. Intent manifest governance, corpus admission governance, harness independence, and environment council design are not technology investments — they are organisational design investments.

**Category 4 — Ongoing operations (harness operation, corpus maintenance, manifest currency):** Grows with each stage and does not decrease. Each stage adds operational commitments on top of the previous ones. A Stage 5 Dark Factory carries all Stage 1–4 operational obligations plus the harness operation commitment. Roadmap planning must account for the ongoing operational cost of each stage — not just the one-time investment to reach it.

### Investment ratios by stage

| Stage | Technology | Practice Development | Governance Design | Ongoing Operations |
|---|---|---|---|---|
| 1 | High | Low | Low | Low |
| 2 | High | Medium | Low | Low |
| 3 | Medium | High | Medium | Medium |
| 4 | Medium | High | High | High |
| 5 | Medium | High | High | High |
| 6 | Medium | High | High | High |

The most common investment error is maintaining a Stage 1 ratio (technology-heavy) at Stage 4+. The result is high technology spend, low practice capability, and a large Maturity Debt.

---

## The Roadmap Planning Process

A practice-first AI investment roadmap is built in five steps:

**Step 1 — Assess current Effective Stage per domain.** Use the maturity assessment. Produce the Domain Coverage Map. Know exactly where each domain sits and what its Maturity Debt is.

**Step 2 — Identify the binding constraint.** For each domain, what is the specific practice gap that is preventing Effective Stage advancement? The practice gap, not the technology gap, drives the roadmap.

**Step 3 — Sequence practice development.** For each domain, sequence the practice development investments that close the binding constraint. These are training programmes, facilitated workshops, process design engagements, and role development plans — not platform licenses.

**Step 4 — Identify the enabling technology.** Once the practice requirements are understood, identify the technology that enables those practices. Size the technology investment to the practice maturity level — do not over-invest in technology infrastructure for practices that do not yet exist.

**Step 5 — Establish the governance cadence.** For each stage reached, define the ongoing governance cadence that maintains practice maturity. Stage 3 requires regular manifest review. Stage 4 requires corpus admission governance. Stage 5 requires harness independence review. These are permanent operational commitments, not one-time investments.

---

## Common Investment Mistakes

**Procuring Stage N+2 technology at Stage N practice.** The most common and most expensive mistake. The technology runs on a practice foundation that cannot support it. The result is high cost, low performance, and eventual abandonment.

**Treating practice development as soft cost.** Training, facilitation, and process design are consistently under-budgeted relative to technology. In a practice-first roadmap, they are the primary investment, not the secondary one.

**Ignoring ongoing operational costs.** A Stage 4 specification corpus requires governance staff, admission review cycles, and corpus maintenance. A Stage 5 harness requires independent operators and ongoing baseline review. These are not one-off costs — they are permanent operational additions. Roadmaps that do not include them will exhaust their budgets before maturity is sustained.

**Measuring return on technology investment, not return on practice investment.** The technology cannot be held accountable for outcomes that depend on practice. If a RAG pipeline is deployed but retrieval quality is not measured, the return on the retrieval pipeline cannot be assessed. Measuring the technology without measuring the practice produces systematically misleading signals.

**Rushing the Stage 3→4 transition.** The transition from intent engineering to specification engineering is the most consequential transition in the framework. The organisations that move too fast lose the practice foundation on which autonomous operation depends. See [The Stage 3→4 Transition in Detail](../04-examples/stage-3-4-transition.md).

---

*Continue to: [Vendor & Tooling Landscape](./vendor-tooling-landscape.md)*  
*Back to: [Maturity Assessment Framework](./maturity-assessment-framework.md) · [The Engineering Team of the Future](./engineering-team-future.md)*
