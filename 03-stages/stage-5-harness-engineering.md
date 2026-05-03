# Stage 5 Deep Dive — Harness Engineering

*E2-05 · Wave 5 — Stages · Audience: All*

> See also: [Stage Transition Playbooks](./stage-transition-playbooks.md) · [Stage 4 Deep Dive](./stage-4-specification-engineering.md) · [Stage 6 Deep Dive](./stage-6-environment-engineering.md) · [Escalation Package Standard](../02-artefacts/escalation-package-standard.md)

---

## Overview

Stage 4 creates autonomous operation. Stage 5 makes it sustainable.

At Stage 4, agents own the workflow within the specification corpus. A harness exists — it logs decisions, monitors behaviour, and surfaces anomalies. But at Stage 4, the harness is relatively simple: telemetry flows, alerts fire, humans investigate. The harness is an observer.

At Stage 5, the harness becomes a governor. It continuously monitors context quality, behavioural patterns, and output consistency against defined baselines. When it detects anomalies, it does not just alert — it classifies the anomaly, assesses severity against defined parameters, and applies self-healing playbooks where the situation falls within defined scope. It escalates only when it cannot resolve the issue autonomously.

The shift is significant. A Stage 4 Dark Factory requires human attention to maintain. A Stage 5 Dark Factory monitors itself. Human attention is reserved for anomaly patterns the harness cannot resolve — genuinely novel problems or systemic issues requiring architectural intervention.

Harness engineering is the discipline of building systems that can govern themselves. It requires deep understanding of how agents fail, how those failures manifest in observable signals, and how to design interventions that address root causes rather than symptoms.

---

## What Stage 5 Looks Like

### The human role

At Stage 5, the human's operational role narrows further. They are no longer in the monitoring loop for routine anomalies. The harness handles those. Humans govern the harness — they review its performance, adjust its parameters, approve its playbooks, and respond when it escalates.

**What the human does:**
- Reviews harness performance on a defined cadence — are detection rates within target, are playbooks firing correctly, are there recurring patterns that warrant architectural attention?
- Approves and maintains self-healing playbooks — what the harness may do autonomously must be explicitly authorised
- Responds to harness escalations — the genuinely novel or systemic anomalies the harness cannot resolve
- Governs baseline evolution — as agent behaviour and corpus change, baselines must be updated
- Investigates anomaly patterns — when the same type of anomaly recurs, a systemic response is required

**What transfers to the harness:**
- Routine anomaly detection and classification
- Self-healing interventions within defined playbook scope
- Context quality monitoring and degradation response

**What stays with humans:**
- Playbook authorship and approval
- Baseline definition and revision
- Systemic interventions — when the system design itself needs changing
- Escalations that exceed playbook scope

### The agent role

At Stage 5, agents operate within a self-governing system. They continue to execute the workflow as at Stage 4. They generate the telemetry the harness requires — decision logs with corpus references, confidence scores, context hit rates. The quality of harness governance depends on the quality of agent telemetry. An agent that does not emit informative telemetry cannot be effectively governed.

---

## The Harness Architecture

### What the harness monitors

A Stage 5 harness monitors three distinct layers:

**Behavioural layer** — what agents are doing. Decision frequency, decision distribution across corpus clauses, escalation rate and pattern, confidence score distribution, output quality signals.

**Context layer** — what agents are seeing. Retrieval hit rate, relevance scores, freshness of retrieved content, context fill rate against schema requirements, context window utilisation.

**System layer** — how the infrastructure is performing. Latency, throughput, error rates, model availability, pipeline health.

Most Stage 4 harnesses monitor the system layer well — these are standard infrastructure metrics. The behavioural and context layers are more difficult to instrument and are where Stage 5 adds the most value. A harness that monitors system health but not behavioural health provides false assurance: the infrastructure is green while agent decision quality degrades silently.

### Behavioural baselines

A baseline defines what "normal" looks like for each agent over each metric dimension. Anomaly detection compares current behaviour against the baseline; deviations beyond defined thresholds trigger classification and response.

Baselines must be:

**Specific.** A single baseline across all agents is not useful — different agents have different normal patterns. Baseline per agent, per workflow type, and if necessary per operational period (e.g., month-end behaviour in finance differs from intramonth behaviour).

**Measured.** Baselines derived from observation over a statistically meaningful period, not estimated. The baseline period must cover the full range of normal operational variation.

**Dynamic.** Baselines decay as operational patterns evolve. An agent whose workflow complexity increases over time will have a higher normal escalation rate than its initial baseline. Static baselines produce increasing false positive rates as the system matures. Baselines must be reviewed and updated on a defined cadence — and whenever a significant specification corpus change is deployed.

**Documented.** Every baseline has a defined review date, a defined update process, and a change log. Baselines that exist only in monitoring tool configuration are invisible to governance.

### Self-healing playbooks

A self-healing playbook is an authorised, documented response to a classified anomaly type. The harness applies it autonomously when the anomaly matches the playbook's preconditions.

The structure of a self-healing playbook:

| Element | Content |
|---|---|
| Playbook ID | Unique identifier referenced in harness logs |
| Anomaly class | The specific anomaly type this playbook addresses |
| Preconditions | The exact conditions that must be true before this playbook fires — anything outside these conditions escalates |
| Response actions | The sequence of actions the harness takes — specific and bounded |
| Success criterion | How the harness confirms the anomaly is resolved |
| Escalation trigger | What causes the playbook to stop and escalate |
| Owner | Who reviews and approves this playbook |
| Review date | When this playbook is next assessed for continued appropriateness |

Playbooks must be explicit about their scope. A playbook that fires on "context degradation" without defining what "context degradation" means precisely will fire incorrectly. Playbooks must have explicit preconditions that prevent them from applying to situations they were not designed for.

Common playbook categories in Stage 5:

**Context degradation playbook.** Precondition: retrieval hit rate falls below defined threshold for a specific context schema element. Actions: switch to fallback retrieval source; alert content owner; log degradation event. Escalation trigger: fallback source also degraded; escalate to context infrastructure team.

**Escalation rate spike playbook.** Precondition: escalation rate exceeds defined threshold for a specific decision class over a defined rolling window. Actions: flag corpus gap to specification governance queue; alert corpus owner. Escalation trigger: rate continues to climb after flag; escalate to specification engineering lead.

**Confidence distribution shift playbook.** Precondition: agent confidence score distribution shifts materially from baseline (statistical test defined). Actions: flag to quality review; reduce autonomous operation scope for affected decision class pending investigation. Escalation trigger: shift is sustained over 24 hours; escalate to harness engineering.

**Model behaviour change playbook.** Precondition: output pattern metrics shift materially following a model version update. Actions: flag to specification engineering; compare current outputs against baseline sample; assess whether corpus remains correctly calibrated. Escalation trigger: material miscalibration detected; escalate to specification and model governance.

---

## Context Degradation — The Stage 5 Specific Failure Mode

Context rot (the Stage 2 failure mode) occurs when knowledge base content ages out. Stage 5 introduces a related but distinct failure mode: context degradation under operational pressure.

At scale, context pipelines are stressed in ways that do not appear at Stage 2 volume. Retrieval systems develop hotspots — certain queries fire at high frequency and produce inconsistent results as the index operates under load. Embedding models drift as the corpus grows. Freshness SLAs that were achievable at low volume become difficult to maintain at high volume.

Context degradation at Stage 5 is operational rather than governance-originated. The harness must monitor it as an independent signal from content governance.

**Retrieval quality under load** — baseline retrieval metrics established at low volume may not hold at production volume. The harness monitors retrieval quality continuously, not just average freshness.

**Embedding model drift** — as the corpus grows and embedding models are updated, the semantic space changes. Documents embedded six months ago may rank poorly against current queries not because their content is wrong but because the embedding space has shifted. The harness detects this as an anomalous drop in relevance scores for documents known to be current and relevant.

**Cache invalidation failures** — retrieval caches that are not invalidated correctly return stale results with high confidence. The harness detects this through freshness monitoring; the resolution is cache invalidation, not corpus update.

---

## MTTD and MTTR

Stage 5 introduces operational SLAs for harness performance — specifically Mean Time to Detect (MTTD) and Mean Time to Resolve (MTTR) for harness anomalies.

MTTD measures how quickly the harness identifies that an anomalous condition exists. An MTTD target reflects the organisation's risk tolerance: how much undetected anomalous agent behaviour is acceptable before intervention?

MTTR measures how quickly the anomaly is resolved — either through self-healing playbook execution or through human escalation and intervention. MTTR is bounded by the escalation SLA: the human response time to a harness escalation must be defined and governed.

Both metrics must be measured against defined targets and reviewed at the harness governance cadence. A harness that is technically operational but missing its MTTD target is a harness that provides false assurance — anomalies are occurring but being detected too slowly to prevent harm.

| Metric | Definition | Why it matters |
|---|---|---|
| MTTD | Time from anomaly onset to harness detection | Determines how long anomalous behaviour continues undetected |
| MTTR (automated) | Time from detection to playbook resolution | Determines operational impact of detectable anomalies |
| MTTR (escalated) | Time from escalation to human resolution | Determines impact of anomalies outside playbook scope |
| False positive rate | Proportion of harness alerts that do not indicate genuine anomalies | High false positive rate produces alert fatigue and desensitises operators |
| Playbook hit rate | Proportion of anomalies resolved by playbook vs escalated | Indicates whether playbook coverage is adequate |

---

## Harness Engineering in Enterprise Knowledge Work

In non-engineering knowledge work domains, harness engineering takes different forms but the same principles apply.

**Finance.** The harness for financial workflows monitors for decisions that produce figures outside defined materiality thresholds, for classification decisions that may trigger regulatory reporting obligations, and for patterns in agent behaviour that suggest specification gaps in coverage of regulatory requirements. MTTD targets must align with regulatory reporting deadlines — a harness that detects a material error after a report has been filed is too slow.

**Legal.** The harness monitors for agent actions that may have created legal obligations — contract executions, commitments, waivers — that require human awareness regardless of whether they were within specification. A decision that was corpus-compliant but creates a material legal position must be surfaced to legal review within a defined window.

**HR.** The harness monitors for decision patterns that may indicate proxy discrimination — systematic differences in outcomes across individual characteristics that should not affect the decision. This is a Stage 5 capability that implements at scale the proxy discrimination prevention requirements established in Stage 4 corpus entries. The harness detects the pattern; humans investigate and correct.

**Risk & Compliance.** The harness monitors for gaps in regulatory coverage — situations the corpus does not cover that are emerging from regulatory change. Regulatory intelligence must feed the harness, not just the corpus update process. When new regulatory requirements take effect, the harness should be configured to flag decisions in the affected domain pending corpus update.

---

## Failure Modes at Stage 5

**Alert fatigue.** The harness generates too many alerts. Humans stop paying attention. Alerts become noise. Genuine anomalies are missed because the alert channel is saturated. Fix: alert classification — only alerts requiring human intervention reach humans; everything else is handled autonomously or logged silently.

**Baseline decay.** Agent behaviour and operational patterns evolve but baselines are not updated. Anomaly detection degrades as the baseline drifts from reality. Fix: baseline review cadence as a governance requirement; mandatory baseline update on every significant corpus change.

**Playbook scope creep.** Playbooks are applied to situations outside their designed scope because the preconditions are insufficiently precise. The harness resolves the wrong way. Fix: precise preconditions for every playbook; explicit escalation triggers when conditions are not exactly met.

**Monitoring the wrong signals.** The harness monitors infrastructure metrics (latency, throughput, error rate) but not behavioural metrics (decision distribution, confidence shifts, escalation patterns). Infrastructure is green; agent decision quality degrades invisibly. Fix: behavioural and context monitoring as first-class harness requirements, not afterthoughts.

**Self-healing without oversight.** Self-healing playbooks fire without governance review. Over time, playbook parameters drift. Playbooks that were designed for one set of conditions fire under different conditions and produce unintended effects. Fix: every playbook has a review date and an owner; changes require formal approval.

---

## Stage 5 Readiness Assessment

Before transitioning to Stage 6, the following should be true:

| Indicator | What it demonstrates |
|---|---|
| Harness covers all production agents — telemetry flowing, baselines established | Full monitoring coverage |
| MTTD is within defined target for three consecutive review periods | Detection capability is proven operational |
| At least one autonomous self-healing playbook has fired and resolved an anomaly | Self-governance is proven operational, not theoretical |
| False positive rate is below defined threshold | Alert quality is sufficient to prevent fatigue |
| Baseline review process has been executed at least twice | Governance of baselines is operational, not just designed |
| An environment inventory exists | Stage 6 can begin from a clear picture of where redesign is needed |

---

*Continue to: [Stage 6 Deep Dive — Environment Engineering](./stage-6-environment-engineering.md)*  
*Back to: [Stage 4 Deep Dive — Specification Engineering](./stage-4-specification-engineering.md) · [Stage Transition Playbooks](./stage-transition-playbooks.md)*
