# Stage 6 Deep Dive — Environment Engineering

*E2-06 · Wave 5 — Stages · Audience: All*

> See also: [Stage Transition Playbooks](./stage-transition-playbooks.md) · [Stage 5 Deep Dive](./stage-5-harness-engineering.md) · [Environment Map — Reference Design](../02-artefacts/environment-map.md) · [Dark Factory Definition](../00-foundations/dark-factory.md)

---

## Overview

Every stage up to Stage 5 is about equipping agents to operate better within an existing environment. Stage 6 asks a fundamentally different question: what would the environment look like if it were designed for agents from the outset?

The previous five stages are adaptive. They fit agents to the world — designing prompts that work in ambiguous systems, engineering context from poorly structured knowledge bases, encoding intent in the presence of undefined organisational priorities, building specifications that govern behaviour within systems never intended to be governed this way. Each stage adds capability. But the underlying environment — the APIs, data models, process architectures, and knowledge structures — was designed for humans and adapted for agents.

Stage 6 inverts this. It is redesign: deliberately restructuring the environment so that agents can operate within it without the workarounds, adaptations, and integration complexity that accumulate when you fit AI to legacy infrastructure. When an environment is engineered for agents, the constraints that required compensating specification at lower stages become structural impossibilities. The safety is built in, not bolted on.

This is the most ambitious and longest transition in the framework. It requires authority to make architectural decisions across organisational systems, a governance body with the mandate to direct that redesign, and a deliberate programme of work that spans multiple years. But it is also the stage that produces the greatest operational leverage — a Dark Factory operating in an environment designed for it is qualitatively more capable than one operating against legacy infrastructure.

---

## What Stage 6 Looks Like

### The human role

At Stage 6, the human is an environment architect. Their primary contribution is not governing what agents do within the environment — the harness handles that. It is designing the environment itself.

**What the human does:**
- Defines the environment map — the machine-readable model of the operational landscape agents navigate
- Governs the Environment Council — the body that makes architectural decisions about the environment
- Directs the legacy redesign programme — which systems to redesign, in what order, to what standard
- Maintains environment health metrics — ensuring the environment remains current and legible as systems evolve
- Resolves structural escalations — situations where the environment's design prevents agents from doing what the specification requires

**What agents can do in a Stage 6 environment:**
- Navigate the environment by map rather than by ad hoc discovery
- Rely on machine-readable API contracts rather than inferring interface behaviour
- Operate within structurally enforced constraints rather than specification-checked ones
- Access data in formats designed for agent consumption rather than human-oriented formats

**What the Environment Council does:**
- Sets the AI legibility standard for all systems in the environment
- Approves new systems and changes to existing systems against the standard
- Arbitrates when engineering team priorities conflict with environment design requirements
- Reviews and updates the environment map on defined cadence

### The agent role

In a Stage 6 environment, agents navigate by map rather than by inference. The environment map describes what exists, what it exposes, what agents may do within it, and how it interconnects. Agents that were previously required to discover interface behaviour through trial, error, and complex specification now operate from a defined, current, authoritative source.

---

## The Environment Map

The environment map is the primary artefact of Stage 6. It is not documentation — it is the machine-readable model from which agents navigate. Its accuracy is therefore operational, not archival. A stale environment map does not just create compliance risk; it creates agent failures.

### What the map models

**System inventory.** The ground truth of what exists: every system agents interact with, identified by stable ID, with purpose, ownership, and operational status.

**Interface specifications.** Machine-readable contracts for every API agents consume: input schemas, output schemas, error conditions, rate limits, authentication requirements, usage constraints. These are not human-readable documentation — they are formal specifications that can be verified automatically.

**Access permissions.** What agents may do within each system: which operations are permitted, which require escalation, which are prohibited by specification. These permissions are derived from the specification corpus and intent manifest; the environment map makes them spatially explicit.

**Interdependency graph.** How systems connect: what calls what, what depends on what, where cascading failures propagate. Agents navigating complex multi-system workflows need this to understand the blast radius of their actions and to identify escalation paths when a dependency fails.

**Data models.** The structure of data in each system as exposed to agents: field names, types, valid ranges, referential relationships. In a Stage 6 environment, data models are designed for machine legibility — consistent naming, explicit types, no implicit conventions that agents must infer.

**Environment health status.** The current operational state of each system: degraded, operational, scheduled maintenance, recently changed. Agents should not need to discover through failed calls that a system is degraded; the map tells them.

### The AI legibility standard

The AI legibility standard is the specification every system in the environment must meet to be considered Stage 6 compliant. Systems that do not meet the standard require agent workarounds — which reintroduce the complexity that Stage 6 is designed to eliminate.

A minimal AI legibility standard includes:

| Requirement | Rationale |
|---|---|
| Machine-readable API contract (OpenAPI, AsyncAPI, or equivalent) | Agents can verify interface behaviour without inference |
| Explicit error taxonomy with machine-readable codes | Agents can classify errors and apply appropriate responses without ambiguity |
| Idempotent operations where possible | Agents retrying failed operations do not produce duplicate effects |
| Stable unique IDs on all entities | Agents can maintain references across sessions without ambiguity |
| Explicit permissions model | What agents may and may not do is a property of the API, not a convention |
| Semantic versioning with deprecation notice | Agents are notified before interface changes break their assumptions |
| Observability endpoints | The harness can monitor system health without external detection |

Legacy systems that do not meet this standard are candidates for redesign. The redesign programme is the primary delivery vehicle of Stage 6.

---

## The Legacy Redesign Programme

Most organisations entering Stage 6 have environments built for human workers over many years. These environments were not designed with AI legibility in mind — and their lack of legibility has been managed, at lower stages, through increasingly complex specification, context engineering, and harness compensation.

Stage 6 addresses this at source. Instead of continuing to build compensating infrastructure, the environment itself is redesigned.

### Prioritisation

Not all systems require redesign at the same time. Redesign effort should be prioritised by the product of two factors:

**Agent interaction frequency.** Systems that agents interact with most frequently produce the most accumulated friction. Redesigning them produces the most operational benefit.

**Current legibility deficit.** Systems that most significantly fail the AI legibility standard impose the greatest compensating specification burden. Redesigning them removes the most technical debt.

The highest-value redesign targets are systems with both high interaction frequency and significant legibility deficit. Systems with low interaction frequency or acceptable legibility can be deferred.

### Redesign principles

The redesign is not a migration to a new technology. It is a deliberate restructuring to meet the AI legibility standard. Common redesign patterns:

**Interface contract publication.** Systems that expose functional APIs but without formal contracts — the most common situation. The redesign is publishing the contract, not changing the implementation. High value at low cost.

**Data model clarification.** Systems whose data models contain implicit conventions, ambiguous field names, or inconsistent type representations. The redesign is standardising the model, with a migration layer for existing consumers.

**Permission externalisation.** Systems whose permission model is embedded in application logic rather than declared at the interface. The redesign is extracting permissions to an explicit, machine-readable layer. Enables the environment map to represent permissions accurately.

**Error taxonomy standardisation.** Systems that return generic errors or rely on error message text for semantics. The redesign is defining a machine-readable error taxonomy. Enables agents to apply deterministic responses to error conditions.

**Legacy wrapping.** Systems that cannot be structurally redesigned — third-party systems, mainframe applications, or systems with large downstream consumer bases. The approach is a thin wrapper service that presents an AI-legible interface to agents while preserving the existing system. The wrapper is owned by the organisation; its interface contract is maintained to the legibility standard.

---

## The Environment Council

The Environment Council is the governance body that directs Stage 6. It has a unique position in the organisation's governance structure — unlike engineering governance, which owns code and systems, the Environment Council owns the *legibility standard* and the environment map.

### Mandate

The Environment Council's mandate covers:

- Setting and updating the AI legibility standard
- Maintaining the environment map as a current, accurate, and trusted artefact
- Approving new system onboarding against the legibility standard — no new system joins the environment without council approval
- Directing the legacy redesign programme — prioritisation, sequencing, resource allocation
- Arbitrating conflicts between system team priorities and legibility requirements

### Composition

The council requires representatives from: engineering architecture (technical design authority), the specification corpus governance function (alignment between environment and corpus), security (environment changes have security implications), and domain business functions whose systems are in scope (Finance, Legal, HR, etc.).

The council must have executive backing. Environment redesign decisions affect multiple teams and may delay product roadmaps. Without authority that transcends individual engineering teams, redesign priorities will consistently lose to product delivery priorities.

### Decision rights

The Environment Council must have clear decision rights:

- **Blocking authority** — the council can block the production deployment of a new system that does not meet the legibility standard
- **Redesign direction** — the council can direct engineering teams to remediate legibility deficits within defined timescales
- **Map maintenance** — the council approves changes to the environment map and is accountable for its accuracy

Without blocking authority, the standard becomes advisory. Systems that fail the standard will be deployed anyway, documented as exceptions, and never remediated.

---

## Environment Engineering in Enterprise Knowledge Work

The environment engineering challenge in non-engineering knowledge work is often more complex than in software engineering — because the "environment" spans not just technical systems but also the data, process, and knowledge structures that agents operate within.

**Finance.** The financial environment for agents includes: ERP systems, accounting platforms, regulatory reporting infrastructure, and the data models that connect them. AI legibility requirements in finance include: explicit account classification schemas, machine-readable chart of accounts, formal data lineage models that agents can query. The redesign programme in finance often requires addressing data quality and data governance deficits that predate AI — data that was acceptable for human reconciliation is too ambiguous for agent operation.

**Legal.** The legal environment includes: contract management systems, legal research platforms, matter management systems, and document repositories. AI legibility in legal requires: machine-readable contract metadata models, explicit matter taxonomies, structured clause libraries. The redesign programme often requires formalising knowledge structures that existed only in the heads of legal practitioners — making tacit knowledge explicit and machine-readable.

**HR.** The HR environment includes: HRIS systems, policy libraries, organisational hierarchies, and workflows for employment decisions. AI legibility requires: explicit organisational unit hierarchies with stable IDs, machine-readable policy version histories, structured decision taxonomies. The redesign programme must address the high sensitivity of HR data and the strict access control requirements that govern it.

---

## Environment Health

An environment map that is accurate at publication degrades as systems change. Environment health is the ongoing measurement of how well the map reflects reality.

**Map accuracy rate** — what proportion of interface specifications in the environment map match the current implementation of those interfaces? Discrepancies are detected through automated contract validation testing against live systems.

**Legibility standard compliance rate** — what proportion of active systems in the environment meet the AI legibility standard? This metric drives the redesign programme — it should trend upward over time.

**Deprecation notice lead time** — when systems change interfaces, how much notice is given before the change takes effect? Short lead times require the harness to compensate; long lead times enable orderly agent adaptation.

**Dark system rate** — what proportion of systems agents interact with are not covered in the environment map? Dark systems produce invisible complexity that accumulates into harness burden.

These metrics are reviewed by the Environment Council at defined cadence. Degradation in any metric triggers an investigation and a remediation plan.

---

## The Maturity of Environment Engineering

Environment engineering is the frontier of the framework. Most organisations have not reached Stage 6. The patterns are still emerging. What is known is less settled than at earlier stages.

This is explicit in the Wardley position: environment engineering capabilities are in genesis. There are no commodity platforms for it. There are no established playbooks. The organisations that develop this capability now are building practices that will compound over years — and that cannot be replicated overnight by competitors who purchase the same technology later.

The Practice Premium is highest here. An organisation that has genuinely redesigned its environment for AI legibility has created something that its competitors cannot acquire. The environment was built by the organisation; it reflects its domain, its data, and its operational architecture. It is structurally unique. The specifications and harnesses at lower stages are potentially replicable; the environment is not.

> **The Environment Engineering Principle**
>
> An environment designed for agents is not a more sophisticated adaptation of an environment designed for humans. It is a different kind of artefact entirely. It encodes legibility as a structural property — the constraints that earlier stages enforced at specification level become impossible to violate at the environment level. The Dark Factory operating in such an environment does not just perform better. It performs differently — with a class of errors that exist at lower stages eliminated by construction, not by governance.

---

## Stage 6 Readiness — Ongoing Assessment

Stage 6 does not have a completion state in the same sense that earlier stages do. The environment is continuously redesigned as systems evolve, new capabilities emerge, and the AI legibility standard itself matures.

The ongoing assessment for Stage 6 is not "are we done?" but "are we progressing at the right rate?"

| Indicator | Target trend |
|---|---|
| Legibility standard compliance rate | Upward — more systems meeting the standard over time |
| Dark system rate | Downward — fewer unmapped systems |
| Map accuracy rate | Stable at high level — active maintenance is working |
| Legacy redesign completions | Progressing on defined schedule |
| Environment Council meeting cadence | Consistent — governance is operational |
| Agent friction reduction | Measurable — new workflows deploy faster and with less specification overhead |

The last indicator is the most important. If the environment redesign programme is working, agents should be easier to deploy over time, not harder. The specification and harness burden for new workflows should decrease as more of the environment meets the legibility standard. If this trend does not appear, the redesign programme is not delivering the expected benefit and the approach should be reviewed.

---

*Back to: [Stage 5 Deep Dive — Harness Engineering](./stage-5-harness-engineering.md) · [Stage Transition Playbooks](./stage-transition-playbooks.md) · [Environment Map — Reference Design](../02-artefacts/environment-map.md)*
