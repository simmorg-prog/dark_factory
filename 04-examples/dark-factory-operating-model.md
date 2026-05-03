# Dark Factory Operating Model

*E6-05 · Wave 6 — Examples · Audience: All*

> See also: [Dark Factory Definition](../00-foundations/dark-factory.md) · [Agent Council Design](../01-actors/agent-council-design.md) · [Escalation Package Standard](../02-artefacts/escalation-package-standard.md) · [Specification Corpus Architecture](../02-artefacts/specification-corpus.md)

---

## Overview

The Dark Factory operating model describes how a Stage 4–6 organisation actually runs: how work enters the system, how agents govern it, how exceptions surface to humans, how the system learns and improves, and how the humans who remain are organised.

This is not a theoretical description. It is a model of operational reality — the rhythms, governance structures, roles, and artefacts that characterise an organisation that has crossed the Dark Factory threshold and is maintaining it.

---

## The Fundamental Structure

The Dark Factory has four operational layers:

**Layer 1 — Inputs.** Requirements and intent enter the system from human sources: strategy, regulatory requirements, customer needs, operational parameters. This is the only layer where the human is in the origination flow. Everything else is governed by what was encoded here.

**Layer 2 — Agent operation.** Agents execute the workflow within the specification corpus and intent manifest. They take actions, make decisions, produce outputs. They do not require human oversight for decisions within their specification envelope.

**Layer 3 — Governance infrastructure.** The harness monitors agent behaviour against baselines. The audit trail records every decision with its corpus reference. The escalation mechanism routes decisions outside the specification envelope to humans.

**Layer 4 — Human governance loop.** Humans maintain the specification corpus, respond to escalations, review harness reports, and evolve the governance infrastructure. They do not participate in the operational flow of routine work.

These layers interact continuously. Layer 2 generates telemetry that Layer 3 monitors. Layer 3 generates escalations that Layer 4 responds to. Layer 4 generates corpus updates that Layer 2 operates against. The system is self-governing within a defined envelope, and self-improving through the escalation loop.

---

## The Daily Operating Rhythm

### What the agents are doing

In a running Dark Factory, agents are continuously executing workflow:

- Processing inputs as they arrive — not batched, not periodic, but event-driven
- Making decisions within the specification corpus without escalation
- Logging every decision to the audit trail
- Generating telemetry for the harness
- Packaging and routing escalations when the corpus boundary is reached

The volume of agent activity in a mature Stage 5 operation is orders of magnitude greater than what a human team of equivalent scope could handle. The speed is also different — agent workflows complete in seconds or minutes rather than hours or days. The scale and speed are what make the governance infrastructure necessary: a system that makes thousands of decisions per hour cannot be governed by individual human review of each decision.

### What the harness is doing

Simultaneously, the harness is:

- Monitoring behavioural baselines across all production agents
- Comparing current telemetry to established normal ranges
- Running self-healing playbooks against classified anomalies
- Tracking escalation rates by decision class
- Monitoring context quality across all retrieval pipelines
- Generating periodic performance reports for human governance review

Most of the harness's work is invisible to humans — it detects anomalies, applies playbooks, resolves them, and logs the activity. Humans see only the anomalies the harness cannot resolve, and the periodic performance reports.

### What the humans are doing

On a typical day in a Dark Factory operation, the human governance team is:

**Responding to escalations.** The volume depends on corpus coverage and system maturity. In a well-established Stage 4 operation, escalations are a small fraction of total decisions — measured in tens or hundreds per day for a system making thousands of decisions. Each escalation package is well-formed: context, gap, options, urgency. The human's job is to make the decision and initiate the corpus extension.

**Reviewing harness reports.** Weekly or daily (depending on stage and risk profile), the team reviews harness performance: MTTD trends, false positive rates, playbook firing patterns, anomaly classifications. Where patterns indicate systemic issues, they initiate investigations.

**Maintaining the specification corpus.** As escalations are resolved and patterns identified, the corpus is extended. New corpus entries go through the governance process: authoring, quality review, conflict detection, approval, deployment. In a mature operation, this is a routine flow — not a periodic large effort.

**Governing the intent manifest.** When strategy or policy changes, the manifest is updated. This is less frequent than corpus maintenance but more consequential — manifest changes ripple through to corpus entries that derive from them.

**Evolving the harness.** Baselines are updated. Playbooks are refined based on observed firing patterns. New alert categories are added as new anomaly types are identified. The harness is a living system.

---

## The Escalation Loop in Detail

The escalation loop is the primary mechanism by which the Dark Factory learns and improves. Understanding it in operational detail is essential for anyone responsible for maintaining a Stage 4+ operation.

### Step 1: Escalation trigger

An agent encounters a situation where no corpus entry applies, or where the corpus entry explicitly designates the situation as requiring human decision. The agent:

1. Stops processing the workflow at this decision point
2. Assembles the escalation package: context, gap, options, urgency
3. Routes the package to the appropriate human queue
4. Logs the escalation event to the audit trail with the specific gap reference

The workflow is paused at the decision point. It does not fail — it waits for human input. The SLA governing human response time is defined by the urgency classification in the package.

### Step 2: Human response

The receiving human reviews the escalation package. In a well-designed package, they have everything they need: what happened, what the corpus does not cover, what options are available, and what the implications of each option are.

The human makes a decision. They communicate it back to the agent queue. The workflow resumes from the decision point.

### Step 3: Corpus extension

The escalation is closed. Before it is marked complete, a mandatory question is asked: should this decision be incorporated into the specification corpus so that future occurrences do not require escalation?

In most cases, the answer is yes. The human who made the decision drafts the corpus extension — the new entry that encodes the decision as a rule. The entry goes through the governance process (quality review, conflict detection, approval). Once deployed, future occurrences of the same situation are handled autonomously.

### Step 4: Pattern monitoring

The harness tracks escalation patterns by decision class. When the same class escalates repeatedly:

- If corpus extensions have been made: the extensions are not sufficient — revisit the rule design
- If corpus extensions have not been made: the improvement loop is broken — investigate the governance bottleneck

Escalation rate by decision class is a primary indicator of corpus quality. Declining rates indicate the corpus is learning. Stable high rates indicate governance failure.

---

## How the Dark Factory Is Governed

### The governance team

The human governance team in a Dark Factory operation typically includes:

**The specification corpus owner** — responsible for the quality and completeness of the corpus. Reviews incoming corpus changes, ensures the quality gate is maintained, tracks coverage metrics. In a large operation, this may be a small team rather than one person.

**The intent manifest owner** — responsible for keeping the manifest aligned with organisational strategy and policy. Has the domain authority to make intent decisions and the organisational relationships to detect when strategy changes require manifest updates.

**The harness operator** — responsible for harness performance: baseline maintenance, playbook governance, alert configuration, MTTD/MTTR tracking. In a mature operation, this is a monitoring and governance role rather than an active engineering role.

**Domain escalation responders** — the humans who receive escalation packages for specific decision domains. In a finance Dark Factory, this is the controller function. In a legal Dark Factory, it is the in-house legal team. These people do not need to understand the technical governance infrastructure — they need to understand the domain and be able to make decisions from well-formed escalation packages.

### Governance cadences

A mature Dark Factory operates on defined governance cadences:

| Cadence | Activity |
|---|---|
| Continuous | Escalation response (within defined SLA) |
| Daily | Harness anomaly review (where risk profile requires) |
| Weekly | Harness performance review; escalation pattern review; corpus extension queue review |
| Monthly | Corpus coverage assessment; baseline review (if flagged); intent manifest review |
| Quarterly | Full baseline refresh; governance process audit; harness playbook review |
| At strategy change | Intent manifest update (within defined SLA of change) |
| At regulatory change | Corpus review for affected entries (within regulatory effective date) |

The governance cadences are as important as the technical infrastructure. An organisation that has deployed the technical Dark Factory but has not established the governance cadences will see degradation over time: baselines drift, corpus gaps accumulate, escalation patterns are not converted to corpus extensions.

---

## The Agent Council in the Dark Factory

The Agent Council is the governance mechanism that coordinates agent behaviour within the Dark Factory. It is not a single agent — it is a governance structure that orchestrates the agents responsible for a workflow.

### What the Agent Council does

In a running Dark Factory, the Agent Council:

- Receives the workflow requirements from the human governance layer
- Assigns workflow stages to specialist agents based on their capability specifications
- Resolves disputes between agents that produce conflicting outputs at a workflow stage
- Manages escalation packaging and routing when any agent reaches the corpus boundary
- Coordinates recovery when a harness anomaly requires workflow intervention
- Maintains audit records that span the full workflow (where individual agent logs cover single decisions)

### The Agent Council and specification conflicts

The most important operational function of the Agent Council is conflict resolution. When two agents within a workflow produce outputs that cannot both be accepted — for example, when a risk assessment agent and a compliance agent both flag a decision but with contradictory implications — the Agent Council applies the conflict resolution rules in the specification corpus and intent manifest to determine which output takes precedence.

This is not a technical operation. It is a governance operation. The corpus must contain the conflict resolution rules — the Agent Council applies them; it does not invent them.

### When the Agent Council escalates

The Agent Council escalates when:

- No conflict resolution rule applies to the identified conflict
- The corpus is silent on a decision class that multiple agents are contesting
- A harness alert indicates anomalous behaviour in a critical workflow stage and the self-healing playbook cannot resolve it
- The escalation SLA is approaching and the receiving human has not responded

These escalations go to the human governance layer. The package includes: the nature of the conflict or gap, the agents involved, the workflow context, and the options available.

---

## Operating Metrics for the Dark Factory

An organisation operating a mature Dark Factory tracks the following metrics as indicators of health:

| Metric | What it measures | Target direction |
|---|---|---|
| Autonomous decision rate | What proportion of workflow decisions are made without escalation | Rising (more coverage) |
| Escalation rate by class | Frequency of escalations for each decision type | Declining per class (corpus improving) |
| Escalation-to-corpus extension ratio | What proportion of resolved escalations produce corpus extensions | Should be >80% |
| Corpus coverage percentage | What proportion of anticipated decisions are covered | Rising |
| Audit trail completeness | What proportion of decisions have full corpus traceability | 100% target |
| MTTD | Mean time to detect harness anomalies | Within defined target |
| MTTR (automated) | Mean time to resolve via self-healing playbook | Within defined target |
| Human response SLA compliance | What proportion of escalations are responded to within defined SLA | >95% target |
| Intent manifest currency | Days since last review relative to defined review cadence | Within cadence |

These metrics are reviewed at the defined governance cadences. Degradation in any metric triggers an investigation. The metrics are not reported to justify the Dark Factory — they are used to govern it.

---

## What the Dark Factory Is Not

**It is not unsupervised.** The harness monitors continuously. Every decision is logged. Escalation packages reach humans when needed. The Dark Factory is actively governed; it is not running without oversight.

**It is not inflexible.** The specification corpus can be updated. The intent manifest can be revised. New agent capabilities can be added. The governance infrastructure is designed to evolve with the organisation.

**It is not elimination of human expertise.** The humans in the governance loop exercise judgement that is genuinely hard — corpus design, escalation resolution, intent authorship, harness governance. The expertise is present; it is applied at a different level.

**It is not the same for all organisations.** A Dark Factory in financial services, with SOX and PCI DSS compliance requirements, looks different from a Dark Factory in a software engineering team. The governance cadences, the corpus quality standards, the escalation routing, and the audit requirements differ. The structure is the same; the content is domain-specific.

---

*Back to: [Anti-Patterns Library](./anti-patterns.md) · [Dark Factory Definition](../00-foundations/dark-factory.md) · [Agent Council Design](../01-actors/agent-council-design.md)*
