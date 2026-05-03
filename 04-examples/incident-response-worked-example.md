# Worked Example: Incident Response at Each Stage

*E6-02 · Wave 6 — Examples · Audience: Engineering Teams*

> See also: [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md) · [Stage 5 Deep Dive — Harness Engineering](../03-stages/stage-5-harness-engineering.md) · [Dark Factory Definition](../00-foundations/dark-factory.md)

---

## Overview

Incident response is time-critical, high-stakes, and highly structured — making it an excellent lens for understanding how AI operational maturity changes not just the speed of response, but the nature of the human role in it.

At Stage 1, an incident is discovered by a human and resolved by humans. At Stage 6, most incidents are detected by the harness, diagnosed by agents, and resolved autonomously — with humans governing the system that responds, rather than performing the response.

This worked example traces a specific incident type through all six stages: a production service experiencing elevated error rates due to a database connection pool exhaustion. The incident is the same at every stage. What changes is who detects it, who diagnoses it, who resolves it, and how long it takes.

---

## The Incident

**Scenario:** The payment processing service begins returning 5xx errors to ~8% of requests. Root cause: the database connection pool is exhausted because a recently deployed change increased query complexity, causing connections to hold for longer. The pool is not returning connections fast enough to serve incoming requests.

**Impact:** ~8% of payment transactions are failing. Customer-facing error. Regulatory reporting obligation if sustained beyond 15 minutes (PCI DSS incident notification requirements).

---

## Stage 1 — Prompt Engineering

### How the incident unfolds

A customer support agent files a ticket: "Customers reporting payment failures." A developer investigates — checking error logs, reviewing recent deployments, querying the database. They identify the connection pool exhaustion through manual log analysis.

The developer uses a language model to assist with specific tasks: asking it to explain what connection pool exhaustion means, suggesting common causes, helping draft the incident timeline for the post-mortem.

**Timeline:**
- T+0: Customer complaint received by support
- T+15: Support escalates to on-call engineer
- T+30: On-call engineer begins investigation
- T+60: Root cause identified (manual log analysis)
- T+75: Mitigation deployed (connection pool size increased)
- T+90: Incident resolved, service restored

**Total duration:** ~90 minutes. 8% of payment transactions failed during the window.

**The human role:** Everything. Detection, diagnosis, mitigation, communication.

**The model's role:** Advisory. It helps the engineer think through the problem and draft the post-mortem. It does not detect, diagnose, or respond.

---

## Stage 2 — Context Engineering

### How the incident unfolds

Monitoring agents have access to structured context: service metrics, error rates, deployment history, database metrics. When error rates spike, a monitoring agent assembles a contextual summary — recent deployments, correlated metric changes, similar historical incidents — and surfaces it to the on-call engineer.

The engineer does not start from scratch. They receive a structured situation report within minutes of the error rate rising. The agent has correlated the deployment event with the metric change and surfaced the database connection pool as a candidate root cause.

**Timeline:**
- T+0: Error rate spike detected by monitoring agent
- T+3: Structured situation report surfaced to on-call engineer
- T+15: Engineer reviews report, confirms root cause hypothesis
- T+25: Mitigation deployed
- T+30: Incident resolved

**Total duration:** ~30 minutes. Time-to-detection reduced from 30 minutes to 3.

**The human role:** Decision and mitigation. The engineer assesses the agent's root cause hypothesis, confirms it, and deploys the fix.

**The agent's role:** Detection, correlation, context assembly. Not yet: diagnosis confirmation, autonomous mitigation.

---

## Stage 3 — Intent Engineering

### How the incident unfolds

Intent-aware agents understand the organisation's priorities during incidents: service restoration before root cause analysis, customer communication within defined windows, regulatory notification triggered by defined criteria.

The monitoring agent not only surfaces the situation report but applies the intent manifest to prioritise: given the 8% failure rate on payment transactions, the PCI DSS notification window, and the encoded priority of payment system availability above all other services, the agent escalates this immediately as P1 and begins the customer communication draft.

**Timeline:**
- T+0: Error rate spike detected
- T+2: P1 classification applied by agent based on intent manifest (payment system, >5% failure rate = automatic P1)
- T+3: Situation report surfaced to on-call engineer and incident commander
- T+4: Draft customer status page update and regulatory notification draft prepared by agent
- T+10: Engineer confirms root cause, approves communications
- T+20: Mitigation deployed
- T+25: Incident resolved

**The intent manifest contribution:** The P1 classification, the regulatory notification trigger, and the communication drafts were governed by encoded intent — the engineer did not have to make these triage decisions under pressure. The agent made them consistently and correctly.

---

## Stage 4 — Specification Engineering

### How the incident unfolds

Autonomous agents own the incident response workflow. The specification corpus contains the runbook — the machine-enforceable rules governing detection, classification, diagnosis, mitigation, and communication for every defined incident class.

Database connection pool exhaustion is a defined incident class (INC-CLASS-007). The corpus entry covers: detection criteria, P1 classification trigger, initial mitigation steps (connection pool increase within defined bounds, query timeout adjustment), communication timing, and escalation triggers.

**The corpus entry INC-CLASS-007 governs:**

```yaml
id: INC-CLASS-007
version: "1.3.0"
derived-from: OPS-INTENT-AVAILABILITY-001

detection:
  trigger: "connection_pool_utilisation > 95% AND error_rate > 3% for > 2 minutes"
  classification: P1

automated-mitigation:
  step-1:
    action: increase-connection-pool-size
    limit: 150-percent-of-current
    condition: "current_pool_size < max_pool_size_limit"
  step-2:
    action: enable-query-timeout
    value: 30-seconds
    condition: "p95_query_duration > 20-seconds"

escalation-trigger:
  condition: "error_rate > 5% AND 15-minutes-elapsed-since-mitigation"
  target: senior-on-call-and-incident-commander

communications:
  customer-status-update:
    trigger: "P1 AND 5-minutes-elapsed"
    template: COMM-TEMPLATE-SERVICE-DEGRADED
  regulatory-notification:
    trigger: "payment-system AND P1 AND 15-minutes-elapsed"
    target: compliance-queue
    template: COMM-TEMPLATE-PCI-NOTIFICATION
```

**Timeline:**
- T+0: Detection trigger fires (connection pool >95%, error rate >3%)
- T+0: P1 classification applied
- T+1: Automated mitigation step 1 begins (connection pool increase)
- T+2: Error rate begins declining
- T+5: Customer status page updated via template
- T+7: Error rate below threshold — incident resolved
- T+7: Post-mortem generation initiated, audit trail complete

**Total duration:** ~7 minutes. No human involvement in the operational response.

**The human role:** The on-call engineer receives a notification at T+0 (P1 alert), reviews the mitigation in progress, and confirms the post-mortem. They did not have to act. The system resolved the incident faster than a human could have diagnosed it.

**The escalation that did not fire:** The corpus entry specified an escalation trigger if the error rate remained above 5% at 15 minutes. It did not fire — the automated mitigation was sufficient. If it had fired, the engineer would have received a structured escalation package with full diagnostic context.

---

## Stage 5 — Harness Engineering

### How the incident unfolds

The harness detected the connection pool exhaustion trend before it became an incident. Continuous behavioural monitoring identified that connection hold times had been increasing incrementally over the 72 hours following the deployment — a pattern that did not trigger the P1 threshold but was a statistically significant deviation from the behavioural baseline.

At T-18 hours (relative to the Stage 4 timeline), the harness surfaced an anomaly report: "Connection hold time trending upward since deployment DPL-2847. Current P95 duration: 18 seconds vs baseline 8 seconds. Projected to exceed mitigation trigger threshold in ~24 hours at current trajectory."

An engineer reviewed the report and increased the connection pool size proactively — before any customer-facing impact.

**Timeline:** No customer-facing incident occurred.

**The key difference:** The harness detected the pre-incident signal. The Stage 4 specification was triggered by the incident itself; the Stage 5 harness prevented it.

**The telemetry that enabled this:** Behavioural baselines for connection hold time were established as part of the Stage 5 harness build-out. Without baselines, the trending increase would have been invisible until the P1 threshold was breached.

---

## Stage 6 — Environment Engineering

### How the incident unfolds

The database environment has been redesigned. Connection pool management is a structurally governed property of the database service contract, not a runtime configuration that can drift.

The environment contract for the database service specifies:
- Maximum connection hold time for each query class (governed by explicit contract, not by timeout configuration)
- Minimum pool size guaranteed by the database service to the consuming application
- Automatic pool adjustment within defined bounds, executed by the database service itself
- API for consuming applications to declare connection usage patterns (enabling proactive pool allocation)

The deployment DPL-2847 that caused the Stage 1–5 incident cannot produce connection pool exhaustion in the Stage 6 environment — the database service contract prevents it structurally. The query complexity increase is absorbed by the service's contractual obligation to maintain adequate connection pool capacity for the declared usage pattern.

**Total duration:** The class of incident no longer occurs.

**The significance:** This is the Stage 6 compounding effect. Every incident class that is eliminated by environment design reduces the ongoing specification, monitoring, and harness overhead for that class — permanently. The cumulative effect, over years of Stage 6 operation, is an operational environment where the error rate for the defined incident class approaches zero, not through continuous vigilance, but through structural prevention.

---

## What This Example Reveals About the Human Role

The incident response worked example makes the human role transformation vivid:

| Stage | Human activity during a connection pool exhaustion incident |
|---|---|
| 1 | Discovers the incident through a customer complaint; diagnoses manually; deploys fix; writes post-mortem |
| 2 | Reviews the agent's situation report; confirms root cause; deploys fix |
| 3 | Receives P1 alert; reviews classification and communications; confirms mitigation |
| 4 | Receives P1 notification; reviews mitigation in progress; confirms post-mortem |
| 5 | Reviews a pre-incident anomaly report; approves proactive mitigation |
| 6 | N/A — the incident class no longer occurs |

This is not automation replacing human expertise. It is human expertise expressed at a different level. The engineer who designed the Stage 4 corpus entry for INC-CLASS-007 applied deep domain knowledge to encode exactly the right mitigation sequence. The engineer who built the Stage 5 harness baselines knew what a "normal" connection hold time looked like because they understood the system. The architect who designed the Stage 6 environment contract understood the failure mode well enough to eliminate it structurally.

The expertise is present at every stage. Where it is applied changes.

---

*Continue to: [Anti-Patterns Library](./anti-patterns.md)*  
*Back to: [Legal Contract Review Worked Example](./legal-contract-review-worked-example.md) · [Stage 5 Deep Dive — Harness Engineering](../03-stages/stage-5-harness-engineering.md)*
