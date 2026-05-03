# The Stage 3→4 Transition in Detail

*E6-04 · Wave 6 — Examples · Audience: All*

> See also: [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md) · [Stage 3 Deep Dive](../03-stages/stage-3-intent-engineering.md) · [Stage 4 Deep Dive](../03-stages/stage-4-specification-engineering.md) · [Dark Factory Definition](../00-foundations/dark-factory.md)

---

## Overview

The Stage 3→4 transition is the most consequential in the framework. Every other transition adds capability or sophistication. This one changes the fundamental human-agent relationship.

Before Stage 4, humans are in the operational loop. They may delegate heavily. They may use sophisticated context pipelines and intent manifests. But they review, approve, or at minimum have visibility of individual agent decisions. The human is present in the work.

After Stage 4, agents own the workflow. Humans govern the system — they define requirements, maintain the corpus, respond to escalations. But they are not in the operational loop of routine work. The work runs without them.

This is the Dark Factory threshold. It is the most organisationally significant change in the framework — not just technically, but culturally. It requires humans to genuinely trust a system they have built to govern itself. For many organisations, this is harder than any of the technical prerequisites.

This document explores the transition in detail: what it requires, what it looks like in practice, the failure modes most likely to occur, and what the 90 days after crossing the threshold typically look like.

---

## Why This Transition Is Different

Every transition from Stage 1 to Stage 3 is additive. The organisation builds new capabilities — context pipelines, intent manifests, retrieval systems — while retaining the same basic governance posture: humans review agent outputs before they have consequence.

The 3→4 transition is not additive. It is a governance posture change. The review step is removed from the operational workflow. For organisations that have been operating review-gated workflows since Stage 1, removing that gate requires genuine organisational trust — not just technical confidence.

This has implications for how the transition is managed:

**Technical readiness is necessary but not sufficient.** All five preconditions can be met and the transition can still fail — because the humans who are supposed to trust the system to operate without their review have not genuinely developed that trust. Trust is built by evidence, not by specification. The transition process must include a trust-building phase.

**The political dimension is real.** In many organisations, the humans whose review step is being removed have built professional identity around being the final check. Removing that role requires careful change management, not just technical deployment. Organisations that treat this as a pure engineering problem discover the organisational resistance during deployment, which is the worst time to discover it.

**The failure modes are different.** At earlier stages, failure produces bad outputs that humans catch in review. At Stage 4, there is no review gate. Failures propagate further before detection. This is why the harness precondition is non-negotiable — it is the substitute safety mechanism for the removed human review.

---

## The Five Preconditions — In Practice

The five Dark Factory preconditions are stated in the Stage Transition Playbooks. This section describes what each one looks like when it is genuinely met versus when it is nominally met.

### Precondition 1: Context quality is consistently measurable and meets a defined threshold

**Nominally met:** A monitoring dashboard exists. It shows retrieval metrics. The team checks it occasionally.

**Genuinely met:** Retrieval quality has been measured continuously for at least 90 days. A defined threshold exists — a specific number, not "good enough." The system has exceeded that threshold for at least 90 consecutive days. When it has dropped below threshold (as it will have, at some point), the team has detected it through monitoring, diagnosed the cause, and resolved it. The team has experience with context degradation. They know what it looks like and how to fix it.

The distinction matters because context quality at Stage 4 must be self-governing. If the team has only ever seen green dashboards, they have not proven that the governance process works — only that it has not been needed.

### Precondition 2: Organisational intent is encoded in a maintained intent manifest

**Nominally met:** An intent manifest exists. It was published six months ago. It has not been updated since.

**Genuinely met:** The intent manifest has been updated in response to at least one strategy or policy change. When that change happened, the update process worked: the relevant authority identified the change, the manifest was revised within the defined SLA, the agents received the updated manifest before the change became effective. The team can point to a specific agent decision that was governed differently before and after an intent update.

An intent manifest that has never been updated has never proven that the maintenance process works. It is a document, not a practice.

### Precondition 3: Specification corpus covers at least 80% of anticipated workflow decisions

**Nominally met:** The team has a sense that most situations are covered. They have not measured it.

**Genuinely met:** Coverage has been measured against a defined decision taxonomy for the target workflow. The taxonomy was derived from operational observation — the actual decisions the workflow requires — not from a theoretical list. Coverage is 80% or above. The 20% gap is documented in a known-gaps register with escalation triggers for each uncovered class. The team knows, specifically, what situations will produce escalations.

The 80% threshold is a floor. Autonomous operation with lower coverage will produce unsustainable escalation rates. But the more important number is the gap register: do you know what the 20% is? If you don't, you don't know what your agents will escalate, which means you don't know whether your escalation process can handle the volume.

### Precondition 4: A harness exists that can monitor agent behaviour and surface anomalies

**Nominally met:** Infrastructure exists. It logs decisions. Alerts are configured.

**Genuinely met:** The harness has detected at least one anomaly in pre-production testing and surfaced it correctly. The alert routing is tested — alerts reach the right person within the defined SLA. The audit log has been reviewed for a sample of decisions to confirm that corpus entry IDs and versions are being recorded correctly. The team has a response process for harness alerts that has been rehearsed.

A harness that has never fired is a harness that has never been proven. Stage 4 requires the harness to work the first time it is needed under live conditions. That confidence requires evidence from controlled pre-production conditions, not from the absence of problems.

### Precondition 5: Escalation protocols are defined, tested, and trusted

**Nominally met:** Escalation package format is documented. Routing is configured. The receiving team has been briefed.

**Genuinely met:** The receiving humans have received and responded to at least three simulated escalation packages before autonomous operation begins. The simulation included packages with different urgency classifications, different types of specification gaps, and at least one ambiguous situation where the right response was not obvious. The response SLA has been agreed and the receiving team has confirmed it is achievable. After the simulation, the receiving team expressed that they could handle live escalations with confidence.

Escalation is the safety valve of the Dark Factory. If it is not trusted — if the humans who receive escalations do not know what to do with them — the safety valve does not work. There is no substitute for practice.

---

## The Transition Process — What It Looks Like in Practice

The Stage 3→4 transition should not be a single deployment event. It should be a programme with distinct phases.

### Phase 1: Specification coverage assessment (4–8 weeks)

Before the transition begins, conduct a formal specification coverage assessment:

1. Define the decision taxonomy for the target workflow — every decision class the workflow requires agents to make
2. Map existing corpus entries to the taxonomy — which decisions are covered, which are not
3. Calculate coverage percentage
4. Document the gap register — every uncovered decision class, its escalation trigger, its estimated frequency
5. Identify the critical path to 80% — what additional corpus entries are needed

This phase may reveal that the transition cannot begin yet. That is its purpose. Better to discover coverage gaps in a structured assessment than in production.

### Phase 2: Harness and escalation validation (2–4 weeks)

Before autonomous operation, validate the safety mechanisms:

1. Run the harness against a representative sample of decisions from the Stage 3 workflow — confirm telemetry, confirm alert routing, confirm audit log completeness
2. Conduct escalation simulation — three or more simulated escalation packages, with the actual receiving humans responding
3. Review simulation results — identify gaps in escalation package quality, response process, or receiving team confidence
4. Address any gaps found

This phase is not optional. Organisations that skip it cite time pressure; they discover the omission when the first live escalation arrives.

### Phase 3: Parallel operation (2–4 weeks)

Run autonomous operation in parallel with the existing Stage 3 workflow:

1. Agents operate autonomously on the target workflow — they make decisions without human review
2. In parallel, the existing Stage 3 process continues — a human reviews the same decisions
3. Compare outcomes: where do autonomous decisions differ from human decisions?
4. Investigate discrepancies — are they specification gaps? Intent drift? Corpus misalignment?
5. Close gaps before disabling the parallel process

Parallel operation provides the evidence base for trust. At the end of this phase, the team can point to X decisions made autonomously over Y days, with a discrepancy rate of Z%, and a resolution process for every discrepancy. That evidence is what builds organisational confidence in the transition.

### Phase 4: Controlled go-live

Disable the parallel human review process for the target workflow. Autonomous operation is now the only process.

The first 30 days after go-live are the highest-risk period. The harness should be on heightened alert. The escalation receiving team should have reduced response SLAs. Weekly reviews should assess escalation patterns, corpus gap rate, and output quality signals.

After 30 days of stable operation, the transition is complete. The heightened alert status can be relaxed.

---

## The First 90 Days After the Threshold

The 90 days following Stage 4 go-live have a predictable pattern for organisations that have prepared well.

### Days 1–30: The escalation discovery phase

The first wave of escalations arrives. Despite good coverage assessment, some situations were not anticipated. The escalation packages are reviewed. Some are straightforward — a new decision class the corpus did not cover; the resolution adds a corpus entry. Some reveal a gap in the escalation package format — the receiving human needs different information to make the decision. Some reveal intent ambiguity — the manifest was silent on a priority conflict the corpus did not resolve.

Each escalation is a learning event. The measure of a healthy first 30 days is not zero escalations — it is a declining escalation rate and a functional corpus-extension process. If the rate is declining, the system is learning. If the extension process is working, the learning is accumulating.

### Days 31–60: Stabilisation

Escalation rate has typically declined to near-baseline. The corpus has grown to cover the most common gap classes. The harness is providing reliable telemetry. The receiving team has developed confidence — they can triage escalation packages efficiently because they understand the patterns.

This phase often reveals the second-order gaps: situations where the corpus covers the decision but the escalation trigger is set too sensitively (producing escalations for decisions the corpus could have handled) or too loosely (allowing decisions to proceed that should have escalated). Calibration of escalation triggers is a normal part of this phase.

### Days 61–90: Operational maturity

The system is operating predictably. Escalation rate is stable and within the defined threshold. The corpus extension process is routine — new entries are added through the formal governance process without significant engineering effort. The harness telemetry provides a clear picture of system behaviour.

At 90 days, conduct a formal Stage 4 maturity review:

- Escalation rate trend — declining or stable?
- Corpus coverage — has it grown? Are gaps being systematically closed?
- Audit log completeness — is every decision traceable?
- Harness performance — has MTTD been within target?
- Escalation package quality — are receiving humans satisfied with the information they receive?

An organisation that passes this review at 90 days is operating a mature Stage 4 Dark Factory. The foundation for Stage 5 is established.

---

## What Goes Wrong: The Most Common Stage 3→4 Failures

### Failure 1: Premature go-live

The team is under pressure to demonstrate autonomous operation. One or more preconditions is not genuinely met — most commonly, specification coverage has not been measured formally or the harness has not been tested under real conditions. Autonomous operation begins.

The first week produces a manageable escalation rate. The second week reveals that several common decision classes are not covered — the escalation rate spikes. The receiving team is overwhelmed. Decisions are made hastily and without adequate information. Some are wrong. The autonomous operation is suspended.

The organisation has now demonstrated to itself that Stage 4 does not work — when in fact what failed was the pre-transition process. Recovery requires going back to Phase 1 of the transition process, which the team now treats as bureaucratic overhead. The second attempt is harder than the first.

### Failure 2: The corpus that sounds good but doesn't enforce

The specification corpus is written in clear natural language. It is comprehensive. It is reviewed. But it is not machine-enforceable — the entries are prose policies rather than structured specifications with explicit validation logic and test cases.

Agents reference the corpus and interpret it. Two agents may interpret the same clause differently. There is no automated test that fails when an agent makes a corpus-violating decision. The audit log captures decisions but cannot verify them against the corpus automatically.

The failure mode is invisible at first. The system appears to work. Over time, the corpus and actual agent behaviour diverge in subtle ways. When the divergence is eventually discovered — through an escalation that reveals an unexpected pattern — the gap between the corpus and agent behaviour is difficult to characterise because there is no systematic audit mechanism.

The fix is rebuilding the corpus in machine-readable format. This is expensive. The avoidance is building it in machine-readable format from the start.

### Failure 3: The governance that exists on paper

The specification corpus governance process is defined: an approval workflow, a review checklist, a change log requirement. For the first month, it is followed. Then a time-pressured corpus update is made informally. Then another. Within six months, the formal process exists on paper and the informal process is how things actually work.

The consequence is a corpus that lacks traceability, contains undocumented changes, and has no reliable version history. When an agent makes a questionable decision and the governance question is asked — "was this entry properly reviewed?" — the answer is uncertain.

The fix is governance that is technically enforced, not socially enforced. If a corpus entry cannot be admitted without passing automated quality checks, the governance is structural. If it depends on people following a process, the governance is social — and social governance degrades under pressure.

---

## The Cultural Dimension

The most common unacknowledged challenge in the Stage 3→4 transition is cultural, not technical.

The humans whose review step is being removed have been the quality gate for the workflow. They understand the domain. They have caught errors. They have improved outputs through their review. Removing their review step requires them to trust a system — the specification corpus, the harness, the escalation protocol — in a way that feels like reduced responsibility.

For some, it is experienced as professional displacement. Their expertise was expressed through review. That expression is now encoded in the corpus, not exercised in real time.

The organisations that navigate this well reframe the transition explicitly: the human's expertise is not being removed from the system — it is being encoded *into* the system in a more durable and scalable form. The corpus *is* the expression of their expertise. The quality of the corpus is the quality of their judgement, made permanent and scalable.

This reframe is not always sufficient. In some cases, the transition requires genuine organisational change management — clearly defined new roles, explicit acknowledgement of what is changing and why, and visible leadership commitment to the transition being an investment in the humans involved, not a replacement of them.

The organisations that skip the cultural dimension in favour of pure technical execution typically encounter it in the first 30 days after go-live — in the form of an escalation process that does not work because the humans receiving escalations are not genuinely engaged in making it work.

---

*Continue to: [Anti-Patterns Library](./anti-patterns.md) · [Dark Factory Operating Model](./dark-factory-operating-model.md)*  
*Back to: [Feature Delivery Worked Example](./feature-delivery-worked-example.md) · [Stage 4 Deep Dive](../03-stages/stage-4-specification-engineering.md)*
