# Maturity Assessment — Framework Design

*E5-01a · Wave 7 — Strategy · Audience: Technology Leaders, Architects*

> See also: [Maturity Assessment Tool](./maturity-assessment-tool.md) · [Wardley Map](./wardley-map.md) · [Maturity Curve](../00-foundations/maturity-curve.md) · [Cumulative Stack](../00-foundations/cumulative-stack.md)

---

## Overview

A maturity assessment answers a simple question: where are we? The answer should be honest, specific, and actionable — not a number that makes people feel good, but a clear picture of what has genuinely been built and where the foundations are weakest.

Most AI maturity assessments fail at this. They measure what an organisation *has*, not what it *can do*. They produce an average score that hides the lowest solid layer. And they treat technology deployment as evidence of practice maturity — ignoring the gap between having a tool and having the discipline to use it effectively.

This document describes the design of an assessment framework that avoids these failure modes.

---

## Why Standard Maturity Assessments Fail

Three named failure modes explain why most AI maturity assessments produce scores that do not reflect operational reality:

**Failure Mode 1 — Tool inventory masquerading as practice assessment.** The assessment asks "do you have a RAG pipeline?" not "do you have a context schema and are retrieval quality metrics measured?" Having the infrastructure is not the same as having the practice. An organisation that deployed vector search six months ago and has never measured retrieval quality is at Stage 1, not Stage 2. Standard assessments score the infrastructure; this framework scores the practice.

**Failure Mode 2 — Averaging that hides the lowest solid layer.** A Stage 4 score in one dimension and a Stage 1 score in another does not average to Stage 2.5. It means Stage 1 — because the Stage 4 capability is built on a Stage 1 foundation that is not load-bearing. The stack is not the average of its layers; it is the height of its lowest solid layer. Averaging obscures this. This framework does not average.

**Failure Mode 3 — The Practice Premium blind spot.** Technology deployment is visible and purchasable; practice maturity is not. A team that licensed a specification management platform last quarter but has never written an atomic, testable specification clause has Stage 4 technology and Stage 1 practice. Standard assessments, which do not distinguish these, will score them at Stage 4. This framework maintains a two-track score precisely to make this distinction visible.

---

## The Five Assessment Dimensions

The assessment evaluates the organisation across five dimensions. Each dimension captures a different aspect of maturity that cannot be inferred from the others.

### Dimension 1 — Technology

What tools, platforms, and infrastructure are deployed and operational. Technology maturity measures whether the enabling infrastructure exists — not whether it is being used effectively, and not whether the practices that make it valuable have been developed.

Technology without practice is infrastructure waiting to fail. Technology scoring high while practice scores low is the single most common maturity gap in organisations investing heavily in AI tooling.

### Dimension 2 — Practice

How consistently and deliberately the disciplines associated with each stage are applied in day-to-day work. Practice maturity is the harder dimension to assess — because it requires observable evidence, not self-report.

The test for practice maturity: can the assessment team produce an artefact, a process, or a metric that demonstrates the practice is real? "We do context engineering" is not evidence. "Here is the context schema for our primary workflow, here are the retrieval quality metrics for the last 90 days, and here is the person accountable for freshness" — that is evidence.

### Dimension 3 — People

Role evolution, skills development, and human governance capability. People maturity measures whether the organisation has the human capabilities that each stage requires — not just the technical skills, but the governance and domain skills that become increasingly important at higher stages.

At Stage 1, the critical people capability is prompt craft. At Stage 3, it is intent authorship — the ability to articulate organisational intent with enough precision that agents can apply it. At Stage 5, it is harness governance. The skills required change with each stage; the assessment must evaluate stage-appropriate capability, not generic "AI skills."

### Dimension 4 — Governance

Specification quality, intent encoding, oversight mechanisms, and audit capability. Governance maturity measures whether the organisation has the structures in place to be accountable for what its agents do.

Governance maturity is frequently the lowest-scoring dimension in organisations with high technology scores. Deploying agents without governance is the most common source of the failures described in the Risk Register.

### Dimension 5 — Domain Coverage

Which knowledge work domains are at which stage. Because the framework applies across all domains, the assessment must capture domain-stage distribution — not a single overall score, but a coverage map showing where each domain sits.

An organisation with Stage 4 software engineering and Stage 1 finance is not a Stage 2.5 organisation. It is two different assessments, each with its own gap profile and risk posture.

---

## The Two-Track Scoring Model

The two-track model is the central design innovation of this assessment. It separates technology readiness from practice maturity — and derives effective stage from the lower of the two.

### T-Score — Technology Readiness

The T-Score measures whether the tools and infrastructure for each stage exist and are operational. Scoring is binary for each stage: the infrastructure is either present and operational or it is not.

A T-Score of 4 means the organisation has deployed the technical infrastructure associated with Stages 1 through 4: prompt tooling, context pipelines, intent management systems, and a specification corpus management platform.

### P-Score — Practice Maturity

The P-Score measures whether the disciplines of each stage are genuinely applied, consistently, by the teams operating the system. Practice maturity requires observable evidence — artefacts, metrics, processes — not self-assessment.

A P-Score of 4 means the organisation has demonstrably developed the practice disciplines of Stages 1 through 4: a shared prompt library with governance, measured context quality, an actively maintained intent manifest, and a specification corpus with a functioning admission process.

### Effective Stage

> **Effective Stage = the highest stage where both T-Score ≥ threshold AND P-Score ≥ threshold**

An organisation with T-Score 4 and P-Score 2 has an Effective Stage of 2. It has purchased infrastructure it does not yet have the practice to use. The platform amplifies whatever practices exist at Stage 2 — and Stage 2 practices are not what Stage 4 infrastructure is designed to govern.

This is the most common and most dangerous configuration. It looks advanced. It costs significantly. It performs at Stage 2.

---

## The Lowest Solid Layer Rule

The assessment output is not an average or a blend. It is the identification of the highest stage at which the foundation is genuinely solid — both technology and practice thresholds met — and the measurement of the gap above that foundation.

**Effective Maturity Stage** — the highest stage where both T-Score and P-Score meet the defined threshold.

**Maturity Debt** — the gap between the highest attempted stage and the Effective Maturity Stage.

| Maturity Debt | Interpretation | Consequence |
|---|---|---|
| 0 layers | T-Score and P-Score in alignment | Healthy — progression is predictable and safe |
| 1 layer | One stage of unmatched technology | Manageable — close the practice gap before investing further |
| 2 layers | Two stages of unmatched technology | Significant risk — Stage 4+ governance assumptions applied to Stage 2 operations |
| 3+ layers | Systemic misalignment | Fragility — investment is accelerating exposure, not reducing it |

The most important insight the assessment produces is not the Effective Stage number. It is the Maturity Debt — the gap that explains why the organisation's AI investment is not producing the expected returns.

---

## The Domain Coverage Map

Because the framework covers all knowledge work domains, the assessment must produce a domain-stage matrix. A single overall score obscures the domain distribution that matters most for risk and governance.

Example assessment output (Domain Coverage Map):

| Domain | Effective Stage | T-Score | P-Score | Maturity Debt |
|---|---|---|---|---|
| Software Engineering | 3 | 4 | 3 | 1 layer |
| Finance | 2 | 2 | 2 | 0 |
| Legal | 1 | 2 | 1 | 1 layer |
| HR | 1 | 1 | 1 | 0 |
| Procurement | 2 | 3 | 2 | 1 layer |

The reading of this map: the organisation is most mature in Software Engineering (Effective Stage 3, but with 1 layer of technology debt). Finance and HR are solid at their effective stages. Legal and Procurement have technology deployments that exceed their practice foundations.

The risk implication: Legal has Stage 2 technology but Stage 1 practice — it is the most exposed domain, particularly given the regulatory stakes of legal AI deployment.

---

## Practice Indicators — The Observable Evidence Standard

Practice indicators are the observable evidence of practice maturity at each stage. They are the test for whether a practice is real or claimed. If an indicator cannot be pointed to, the practice is not at the level the indicator describes.

### Stage 1 — Prompt Engineering Practice Indicators

- A prompt library exists as a shared team asset — version-controlled, accessible to the whole team, not personal files
- A governance process exists for prompts used in production workflows — review by a second person before use
- Prompts include explicit scope boundaries: what the prompt is for AND what it must not do
- The team can produce the current version of its most-used prompts for any workflow — they are documented, not tribal

### Stage 2 — Context Engineering Practice Indicators

- Context schemas are documented and versioned for each primary workflow — what information is required at each step, in what format
- Context quality is measured with a defined baseline — retrieval hit rate, relevance scores, freshness metrics
- A freshness process exists with named owners for each content category — someone is accountable for currency
- Agents have defined and enforced context budgets — context window allocation is governed, not unlimited

### Stage 3 — Intent Engineering Practice Indicators

- An intent manifest exists, is formally owned, and is actively maintained — not a document, a practice
- When strategy changes, the intent manifest is updated within a defined SLA — the update process has been exercised
- Teams can trace a specific agent decision to a specific intent manifest clause — the governance loop is closed
- A process exists for detecting intent drift — decision patterns are reviewed against encoded intent

### Stage 4 — Specification Engineering Practice Indicators

- ≥80% of workflow decisions are covered by machine-readable specification — coverage is measured, not estimated
- Specification gap rate is measured — escalations per unit of workflow, tracked over time
- Specifications are versioned with full change history and breaking-change flags
- Every agent decision can be traced to a specific specification clause ID and version in the audit trail

### Stage 5 — Harness Engineering Practice Indicators

- Context quality is continuously monitored with automated alerts — not periodic review, continuous
- MTTD is defined, measured, and within target for three consecutive review periods
- A self-healing playbook has fired and resolved an anomaly autonomously — proven operational, not designed
- Behavioural baselines are maintained and reviewed on a defined cadence following corpus changes

### Stage 6 — Environment Engineering Practice Indicators

- ≥50% of internal APIs consumed by agents have machine-readable contracts — measured, not estimated
- An Environment Council exists with a defined mandate and decision rights, meeting on a defined cadence
- An environment health review cadence exists and is followed — map accuracy is measured
- At least one legacy system has been deliberately redesigned for AI legibility with documented improvement

---

## How to Use This Framework

The assessment framework is a tool for honest self-knowledge, not a scoring exercise for reporting purposes. The following guidance is for the people conducting the assessment.

**Start with artefacts, not interviews.** Interviews produce aspirational answers. Artefacts — prompts libraries, context schemas, intent manifests, corpus entries, audit logs, harness dashboards — are evidence. When an indicator cannot be evidenced by an artefact, score it as not met.

**Score consistently, not charitably.** The purpose of the assessment is to identify gaps, not to validate investment. Charitable scoring produces a higher score and a less useful assessment. The organisation that scores honestly and finds its lowest solid layer is better positioned than the one that scores charitably and builds on a foundation that does not hold.

**Separate T-Score and P-Score in every conversation.** The tendency in assessment conversations is to conflate technology deployment with practice maturity. Make the distinction explicit at every step: "We have this tool" (T-Score question) vs. "We consistently do this practice with evidence" (P-Score question).

**Present results with Maturity Debt, not just Effective Stage.** The Maturity Debt is where the insight lives. An Effective Stage of 3 with 0 debt is a much stronger position than an Effective Stage of 3 with 2 layers of debt.

---

*Continue to: [Maturity Assessment Instrument & Tool](./maturity-assessment-tool.md)*  
*Back to: [Wardley Map](./wardley-map.md) · [Cumulative Stack](../00-foundations/cumulative-stack.md)*
