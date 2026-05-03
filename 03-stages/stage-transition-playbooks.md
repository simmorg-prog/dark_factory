# Stage Transition Playbooks

*E2-07 · Wave 5 — Stages · Audience: All*

> See also: [Maturity Curve Overview](../00-foundations/maturity-curve.md) · [Cumulative Stack](../00-foundations/cumulative-stack.md) · [Dark Factory Definition](../00-foundations/dark-factory.md)

---

## Overview

A stage transition is not a software upgrade. You cannot deploy it from a vendor catalogue, complete it in a sprint, or declare it done by updating a status field. Each transition is a shift in how the organisation relates to AI — what it trusts agents to do, what governance structures it operates, and what kinds of work remain with humans.

These playbooks describe the five transitions: Stage 1→2, 2→3, 3→4, 4→5, and 5→6. Each playbook follows the same structure: what changes at the transition, the prerequisites that must be true before it is safe to begin, what to build, the milestones that mark progress, the failure modes most commonly encountered, and the success criteria that confirm the transition is complete.

The 3→4 transition is the most consequential. It is the Dark Factory threshold — the point at which humans move from the operational loop to the governance loop. The other four transitions are significant, but none changes the fundamental human-agent relationship as radically as 3→4. It receives the most detailed treatment here.

---

## How to Use These Playbooks

Each playbook is a sequencing guide, not a project plan. It tells you what must exist before you move and what you are building during the transition. It does not tell you how long it will take — that depends entirely on the organisation's current state, the domain, and the discipline with which the foundational stages were built.

Two rules apply across all transitions:

**The prerequisite rule.** Every prerequisite listed is load-bearing. Organisations that begin a transition before prerequisites are met consistently discover the missing foundation during the transition — at the worst possible time. If a prerequisite is not met, the answer is to meet it, not to redefine it as optional.

**The practice-before-platform rule.** At every transition, there is a temptation to procure a platform and expect it to deliver the transition. It does not. The platform supports the practice. The practice must be developed first. Organisations that deploy Stage 4 specification management tooling before developing specification authorship discipline discover this at significant cost.

---

## Playbook 1 — Stage 1 → Stage 2

### Prompt Engineering to Context Engineering

**What changes at this transition**

At Stage 1, the human carries the context. Every prompt includes whatever background the individual knows, inserted manually, assembled fresh each time. The model's output quality is bounded by the human's ability to include the right information in each interaction.

At Stage 2, context is externalised — architected into retrieval systems, injected systematically at defined workflow steps, and measured for quality. The agent stops relying on the human to assemble its information environment. The human stops being a context courier and becomes a context architect.

The shift is not primarily about the agents. It is about how the organisation treats its own knowledge. Stage 2 requires that knowledge be structured, retrievable, and measured — disciplines that matter independently of AI.

**Prerequisites**

Before starting this transition:

- A prompt library exists as a shared team asset — documented, versioned, and accessible to more than one person
- At least one primary knowledge source (documentation, codebase, policy library) is well-structured and machine-readable
- The team can articulate what information agents need at each step of the target workflow — even if that information is not yet retrievable

**What to build**

| Artefact | Description |
|---|---|
| Context schema | A defined structure for what information gets injected at each workflow step — not a retrieval implementation, a documented requirement |
| Retrieval pipeline | The mechanism that populates the schema — semantic search, keyword retrieval, structured query, or hybrid |
| Knowledge base | The source of truth agents retrieve from — clean, current, structured |
| Context quality metrics | Retrieval hit rate, relevance scores, freshness indicators — the measurement infrastructure |
| Context budget | A defined limit on context window allocation per workflow step — prevents flooding, enforces discipline |

**Transition milestones**

1. Context schema v1.0 documented and approved
2. First agent operating with structured context injection (not prompt-only)
3. Retrieval quality measured with a defined baseline
4. Context freshness process in place — someone owns updating the knowledge base

**Common failure modes**

*Context flooding.* Injecting everything available and relying on the model to identify what is relevant. Outcome: inconsistent results, unpredictable quality, high token costs with no quality improvement. The fix is a context schema that specifies exactly what belongs at each step.

*Context rot.* The knowledge base is populated once and never maintained. Agent outputs begin to drift from organisational reality as documents age. The fix is a defined freshness process with ownership — someone is accountable for knowledge base currency.

*Single-source brittleness.* The entire context pipeline depends on one retrieval source. When it fails or degrades, agent quality collapses with no visibility. The fix is redundancy and quality measurement that surfaces degradation before it affects outputs.

*Premature sophistication.* Investing in complex multi-stage retrieval architecture before establishing that basic retrieval works and is needed. The fix is to prove the value of simple retrieval first, then add sophistication in response to demonstrated need.

**Success criteria**

The Stage 1→2 transition is complete when:

- Agent output quality has measurably improved with structured context injection compared to prompt-only baseline
- Context schemas are documented, versioned, and reviewed at least quarterly
- Retrieval quality is measured and reported — anomalies are detected before they affect outputs
- The knowledge base has a defined owner and a maintenance process
- More than one person in the team can build and maintain the context pipeline

---

## Playbook 2 — Stage 2 → Stage 3

### Context Engineering to Intent Engineering

**What changes at this transition**

At Stage 2, agents do what they are asked. They may do it very well — with rich context, high retrieval quality, and consistent outputs. But they have no awareness of whether *how* they do it serves the organisation's actual goals. Two different agents completing the same task may make opposite choices between competing considerations — more speed versus more safety, more completeness versus more privacy — with no consistent principle governing which wins.

At Stage 3, agents stop simply executing and begin asking whether a given action is the right one given what the organisation values. This is made possible by the intent manifest — the encoded record of the organisation's strategic priorities, risk appetite, and non-negotiable constraints.

The shift demands something from humans that earlier stages did not: the capacity to articulate organisational intent with enough precision that agents can apply it. This is harder than it sounds. Many organisations have never formally articulated what they optimise for when objectives conflict. Stage 3 forces them to.

**Prerequisites**

Before starting this transition:

- Context quality is consistently measurable and meeting a defined threshold — not just "working" but demonstrably good
- Leadership has agreed that intent encoding is a governance priority, not an engineering experiment
- At least one senior practitioner with domain authority is prepared to own the intent manifest — not just contribute to it, but be accountable for its accuracy and currency
- The team has experience with at least one incident where inconsistent agent decisions were traced to absent intent guidance — the problem is experiential, not hypothetical

**What to build**

| Artefact | Description |
|---|---|
| Intent manifest v1.0 | The encoded statement of organisational priorities, conflict resolution rules, and hard constraints — the primary Stage 3 artefact |
| Intent authoring process | Who may write and amend intent clauses, under what governance, with what review cycle |
| Intent validation mechanism | How you detect that agent decisions diverge from encoded intent — what signals indicate intent drift |
| Conflict resolution rules | Explicit rules for what happens when two valid intent clauses produce opposing guidance — lex specialis, priority ranking, escalation trigger |

**Transition milestones**

1. Intent manifest v1.0 published — covering the target workflow's primary decision points
2. At least one agent decision demonstrably shaped by encoded intent (traceable to a specific clause)
3. Intent drift detection operational — alerts fire when agent decisions cluster against intent boundaries
4. Intent manifest reviewed and updated following a strategy change — confirming the maintenance process works

**Common failure modes**

*Governance theatre.* The intent manifest is written, approved, and filed. Agents do not reference it. No one checks whether decisions align with it. It becomes a compliance artefact rather than an operational one. The fix is closing the loop — every agent decision must reference the intent clause it was guided by; auditors must check this.

*Aspirational abstraction.* Intent clauses written at the level of "act ethically" or "prioritise customer value" are not actionable by agents. An agent cannot derive a decision from an aspiration. The fix is specific, testable intent — "when delivery speed and data minimisation conflict, default to data minimisation unless the task owner explicitly accepts the trade-off."

*Unresolved conflicts.* The intent manifest contains two clauses that produce opposing guidance for common situations but no resolution rule. Agents either escalate everything or pick arbitrarily. The fix is explicit precedence rules and a conflict resolution process run before v1.0 is published.

*Intent as engineering artefact.* The intent manifest is owned, authored, and understood only by the engineering team. Business strategy changes but the manifest is not updated because the people who own strategy do not know the manifest exists. The fix is dual ownership — engineering maintains the manifest format and tooling; business leadership maintains the content.

**Success criteria**

The Stage 2→3 transition is complete when:

- The intent manifest is actively used by agents in production — not aspirationally, demonstrably
- A specific agent decision in the last 30 days can be traced to a specific intent clause
- The intent manifest has been reviewed and updated in response to at least one strategy or policy change
- The team can identify an example where encoded intent prevented a decision that would have been made without it
- Intent drift has been detected at least once — confirming the detection mechanism is operational, not theoretical

---

## Playbook 3 — Stage 3 → Stage 4

### Intent Engineering to Specification Engineering — The Dark Factory Threshold

**What changes at this transition**

Every previous transition has been a change in how agents are equipped. Stage 1→2 gave agents context. Stage 2→3 gave agents intent. The 3→4 transition is different. It is a change in how humans relate to the work.

Before Stage 4, humans are in the operational loop. They may delegate heavily, but they review, approve, and confirm at key decision points. Agents assist. After Stage 4, agents own the workflow. Humans are in the governance loop — they set requirements, maintain the specification corpus, respond to escalations, and review the system's behaviour. But they are not in the operational loop of routine work.

This is the Dark Factory threshold. The manufacturing analogy applies precisely: FANUC's lights-off facilities do not dim the lights and hope production continues. They redesign their systems so that production *requires no human presence*. The 3→4 transition is that redesign for knowledge work.

The enabling artefact is the specification corpus — a machine-readable, versioned, conflict-checked body of rules that tells agents how to behave in every anticipated situation within their operational scope. The corpus is the law the Dark Factory enforces.

**The five preconditions**

This transition has five prerequisites that are qualitatively different from earlier playbooks. They are not milestones on the way to the transition — they are preconditions that must all be true before the transition begins. Beginning the 3→4 transition before all five are met is the most common and most expensive failure mode in this entire framework.

| Precondition | What "met" looks like |
|---|---|
| Context quality | Consistently measurable; meeting a defined threshold for at least 90 days; no unresolved context rot |
| Intent encoding | Intent manifest v1.0 published, maintained, and in active use by production agents |
| Specification coverage | Specification corpus covers ≥80% of anticipated workflow decisions — the 80% figure is a floor, not a target |
| Harness presence | A harness exists that can monitor agent behaviour and surface anomalies — even a minimal harness — before autonomous execution begins |
| Escalation readiness | Escalation protocols are defined, documented, and tested with the humans who will receive escalation packages — they have practised responding, not just been briefed |

**What to build**

| Artefact | Description |
|---|---|
| Specification corpus | The machine-readable body of rules governing agent behaviour — versioned, atomic, conflict-checked, traceable to intent manifest clauses |
| Specification authoring process | How new rules are written, reviewed, and admitted to the corpus — who has write access, what review gate applies, how conflicts are detected before admission |
| Escalation package standard | The defined format for escalation packages — what information is included, how urgency is classified, where packages are routed, what SLA governs human response |
| Audit infrastructure | The mechanism that records which specification clause version governed each agent decision — the audit trail that makes the Dark Factory accountable |
| Harness v1.0 | Behavioural monitoring for all production agents — telemetry, anomaly alerts, context quality tracking |
| Change governance | The process for updating the specification corpus — who approves changes, how breaking changes are flagged, how agents are notified of version updates |

**Transition milestones**

1. Specification corpus v1.0 covering ≥80% of target workflow decisions, conflict-checked, with all five quality dimensions verified
2. Audit infrastructure operational — every agent decision logged with specification version reference
3. Harness operational — behavioural telemetry flowing, anomaly alerts configured
4. First escalation package issued, routed, resolved, and confirmed by the receiving human — the full escalation loop tested end-to-end
5. First workflow segment operating in autonomous mode — no human in the operational loop — for a defined period (minimum 30 days) without requiring unplanned human intervention

**Common failure modes**

*Premature autonomy.* Moving agents to autonomous operation before specification coverage reaches the threshold. The immediate symptom is high escalation rate as agents encounter uncovered situations constantly. The downstream symptom is specification debt — uncovered situations become visible only in production, under time pressure, which produces poorly-authored patches that compound the coverage problem.

*Specification as prose.* The specification corpus is written as policy documents rather than machine-readable rules. Agents cannot directly parse and apply natural language policies with the precision required at Stage 4. The fix is structured, machine-readable format — OPA/Rego, YAML with defined schema, OSCAL-compatible structures.

*Absent audit trail.* Agents operate autonomously but there is no record of which specification clause version governed each decision. When an output is challenged, there is no way to determine whether the agent followed the specification, what version it was following, or whether the specification was adequate. The fix is audit logging at the point of enforcement — not a downstream activity.

*Untested escalation.* Escalation protocols exist on paper but the humans who receive escalation packages have never done so. When the first live escalation arrives — typically at an inconvenient time — the response is slow, uncertain, or incorrect. The fix is rehearsal: simulate escalations before autonomous operation begins, with the actual people who will respond.

*Harness absence.* Autonomous operation begins without a functioning harness. The organisation has no visibility of what agents are doing or whether their behaviour is drifting. Problems are discovered through downstream output quality degradation rather than through behavioural monitoring. The fix is the precondition rule: no autonomous operation without a functioning harness.

**Success criteria**

The Stage 3→4 transition is complete when:

- Agents operate autonomously on the target workflow without human review of individual decisions — humans receive only escalation packages
- Escalation rate is within the defined acceptable threshold and trending downward as specification gaps are closed
- Every agent decision in the audit log is traceable to a specific specification clause ID and version
- The specification corpus has received at least one change through the formal change governance process — confirming the process works under operational conditions
- The receiving humans rate escalation packages as actionable — they have what they need to make decisions without requesting additional information in the majority of cases

---

## Playbook 4 — Stage 4 → Stage 5

### Specification Engineering to Harness Engineering

**What changes at this transition**

At Stage 4, the specification corpus is the law and agents operate within it. The harness at Stage 4 may be relatively simple — telemetry, basic anomaly alerts, audit logging. What it cannot do is *respond* to anomalies autonomously. A human is still required to interpret alerts, diagnose issues, and intervene.

At Stage 5, the harness becomes an active governor of the system. It continuously monitors context quality, behavioural patterns, and output consistency against defined baselines. When it detects anomalies, it does not simply alert — it classifies the anomaly, assesses severity, applies self-healing playbooks where the situation falls within defined parameters, and escalates only when it cannot resolve the issue autonomously.

The shift is from a Dark Factory that requires human monitoring to a Dark Factory that monitors itself. Human attention is reserved for anomaly patterns the harness cannot resolve — genuinely novel situations or systemic issues that require architectural intervention.

**Prerequisites**

Before starting this transition:

- The specification corpus is stable — the gap-filling phase of Stage 4 is substantially complete, and new specification additions are incremental rather than structural
- Behavioural baselines have been established for all production agents — what "normal" looks like is defined and measured
- The team understands the failure taxonomy: what kinds of anomalies have occurred, what caused them, what resolution looked like
- A self-healing playbook can be written for at least one common anomaly class — there is a known, tested resolution for at least one type of problem

**What to build**

| Artefact | Description |
|---|---|
| Comprehensive harness | Behavioural telemetry, context quality monitoring, output consistency tracking — covering all production agents and all workflow stages |
| Behavioural baselines | Defined normal ranges for each agent's key metrics — output volume, latency, escalation rate, context hit rate, confidence distribution |
| Self-healing playbooks | Documented, tested responses to classified anomaly types — what the harness does autonomously when each type occurs |
| MTTD / MTTR targets | Defined targets for Mean Time to Detect and Mean Time to Resolve harness anomalies — the SLA the harness operates to |
| Context degradation detection | Automated monitoring of retrieval quality, freshness, and completeness — surfaces context rot before it affects agent outputs |
| Harness governance | Who reviews harness performance, what cadence, what threshold triggers human escalation from the harness itself |

**Transition milestones**

1. Harness covering all production agents — telemetry flowing, baselines established, alerts configured
2. First autonomous harness intervention: harness detects an anomaly, applies a self-healing playbook, resolves the issue without human trigger
3. MTTD measured over 30 days and within defined target
4. Context degradation detected by harness before it affects downstream output quality — confirming detection is proactive, not reactive
5. Harness performance reviewed on defined cadence with findings documented and actioned

**Common failure modes**

*Alert fatigue.* The harness generates too many alerts, humans stop paying attention, alerts become noise. The consequence is a harness that is technically operational but functionally absent — anomalies are missed because alerts are ignored. The fix is alert classification and escalation thresholds — only alerts that require human intervention reach humans; everything below the threshold is either handled autonomously or logged silently.

*Baseline decay.* Agent behaviour evolves over time — as the specification corpus is updated, as context sources change, as task volume shifts. Baselines defined at Stage 4 transition become progressively less accurate. Anomaly detection degrades. The fix is a baseline review cadence — baselines are updated on a defined schedule and whenever a significant specification change is deployed.

*Wrong signals.* The harness monitors the easy metrics — latency, volume, error rate — rather than the meaningful ones — specification coverage, decision confidence distribution, escalation pattern analysis. A harness that is technically healthy but missing the substantive signals provides false assurance. The fix is signal design: what does anomalous *behaviour* look like, not just anomalous *performance*.

*Self-healing without bounds.* Self-healing playbooks are written without defined operating bounds — the harness applies them to situations outside their designed scope. Autonomous resolution creates new problems. The fix is explicit preconditions for each playbook — the harness only applies it when specific conditions are true; everything else escalates.

**Success criteria**

The Stage 4→5 transition is complete when:

- The harness detects anomalies before they affect downstream output quality — not through complaint, through monitoring
- Self-healing playbooks are operational and tested — confirmed to work under real conditions, not just in simulation
- MTTD is within defined target for at least three consecutive review periods
- Human escalation from the harness is triggered by genuinely novel anomalies, not by routine issues the self-healing playbooks should handle
- Harness performance is reviewed on cadence and findings are actioned — confirming the governance loop is operational

---

## Playbook 5 — Stage 5 → Stage 6

### Harness Engineering to Environment Engineering

**What changes at this transition**

All previous transitions have been about equipping agents to operate better within an existing environment. Stage 5 completes that journey: the harness is mature, the specification corpus is comprehensive, agents operate reliably and are actively governed. The Dark Factory is running well.

Stage 6 asks a different question. Not "how do we equip agents for this environment?" but "how do we redesign the environment so that agents can operate within it without the adaptations, workarounds, and integration complexity that accumulate when you adapt AI to legacy infrastructure?"

The transition is from a Dark Factory that operates *despite* its environment to one that operates *because of* its environment. APIs are designed with agent contracts in mind. Data models are structured for machine legibility. Process architectures eliminate the ambiguities that generate avoidable escalations. The environment becomes inherently safe for AI — not by adding guardrails, but by removing the conditions that require them.

This is the longest transition. It involves deliberate redesign of systems that predate AI, with all the political, technical, and organisational complexity that entails. It requires a governance function — the Environment Council — with the mandate and standing to make architectural decisions that affect the whole organisation.

**Prerequisites**

Before starting this transition:

- The harness is mature and self-governing — human attention is not consumed by monitoring tasks that the harness should handle autonomously
- An environment inventory exists — the team knows what systems agents interact with, where the integration friction lives, and what the highest-value redesign targets are
- Leadership has agreed that environment redesign is a first-class investment priority, not an engineering improvement project
- An Environment Council is constituted or a clear path to constituting one exists — environment redesign decisions cannot be made by engineering alone

**What to build**

| Artefact | Description |
|---|---|
| Environment map | The machine-readable model of the operational landscape — what exists, what it exposes, how it interconnects, what agents may and may not do within it |
| Machine-readable API contracts | Formal specifications of all APIs consumed by agents — input schemas, output schemas, error conditions, usage constraints |
| Agent-legible data models | Restructured data models that eliminate ambiguity agents have historically required workarounds to manage |
| Environment health metrics | Ongoing measurement of environment legibility — API contract coverage, schema stability, ambiguity rate, integration failure rate |
| Environment Council | The governance body with mandate to approve environment changes, set legibility standards, and arbitrate between engineering priorities and AI requirements |
| Legacy redesign roadmap | A prioritised programme of deliberate redesign work — which systems to address in what order, with rationale |

**Transition milestones**

1. Environment map v1.0 published — covering all systems agents currently interact with
2. Environment Council constituted with defined mandate and decision rights
3. ≥50% of agent-consumed APIs have machine-readable contracts — the baseline from which improvement is measured
4. First legacy system deliberately redesigned for AI legibility — demonstrating that the redesign process works end-to-end
5. Environment health metrics operational and reviewed on defined cadence

**Common failure modes**

*Boiling the ocean.* Attempting to redesign all legacy systems simultaneously. The effort becomes unmanageable, nothing reaches completion, and the team loses momentum. The fix is ruthless prioritisation — identify the three systems that create the most friction for the highest-value agent workflows, and complete those redesigns before expanding scope.

*Environment map without governance.* The map is created once and immediately begins to drift from reality as systems change. Within six months, it is unreliable. Agents navigating by a stale map make errors that would not occur if the map were current. The fix is the governance precondition: no environment map without an Environment Council to maintain it.

*Redesigning for current agents.* Legacy systems are redesigned to eliminate friction for today's agent workflows. The environment ossifies around today's architecture rather than anticipating future agent capabilities and requirements. The fix is designing for legibility as a property — structured, explicit, unambiguous — rather than for any specific agent or workflow.

*Engineering ownership only.* Environment redesign decisions are made by engineering without governance authority. Teams whose systems are being redesigned resist changes that affect their roadmaps. The redesign programme stalls in negotiation. The fix is the Environment Council with genuine standing — not an advisory body, but a decision-making body with executive backing.

**Success criteria**

The Stage 5→6 transition is complete when:

- New agent workflows can be deployed to the environment without requiring custom integration work for each system they touch — the environment is legible by default
- The environment map is current and trusted — discrepancies are detected and resolved within a defined SLA
- Environment health is measured, reviewed, and actioned on cadence
- The Environment Council is operational and making substantive decisions about the environment's evolution
- At least three legacy systems have been redesigned for AI legibility, with documented improvement in agent performance on workflows that use them

---

## Transition Summary

| Transition | Human role shift | Primary artefact produced | Gating condition |
|---|---|---|---|
| 1 → 2 | Context courier → Context architect | Context schema + retrieval pipeline | Context quality measurable |
| 2 → 3 | Execution reviewer → Intent author | Intent manifest | Intent ownership confirmed |
| 3 → 4 | Operational participant → Governance loop | Specification corpus | All five Dark Factory preconditions met |
| 4 → 5 | Harness monitor → Anomaly triage | Self-healing playbook library | Specification corpus stable |
| 5 → 6 | System navigator → Environment designer | Environment map | Harness self-governing |

The most important column is the last. Each gating condition is the single most important prerequisite for each transition — the one that, if unmet, makes the transition unsafe regardless of how well everything else is prepared.

---

> **The Transition Principle**
>
> A stage transition is not complete when the new artefacts are deployed. It is complete when the human role has genuinely shifted — when the work that required human presence at the previous stage is reliably performed by agents, and the humans have moved to the governance and exception-handling responsibilities of the next stage. Deploying the tooling is the beginning of the transition. The human role shift is the end of it.

---

*Continue to: [Stage 1 Deep Dive — Prompt Engineering](./stage-1-prompt-engineering.md) · [Stage 3→4 Transition in Detail](../04-examples/stage-3-4-transition.md)*  
*Back to: [Maturity Curve Overview](../00-foundations/maturity-curve.md) · [Cumulative Stack](../00-foundations/cumulative-stack.md)*
