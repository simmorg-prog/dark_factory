# Worked Example: Finance Month-End Close at Each Stage

*E6-06 · Wave 6 — Examples · Audience: Business Leaders, Finance*

> See also: [Enterprise Knowledge Work Map](../05-strategy/enterprise-knowledge-work-map.md) · [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md) · [Dark Factory Definition](../00-foundations/dark-factory.md)

---

## Overview

Month-end close is one of the most process-intensive activities in enterprise finance: a time-bounded, high-stakes sequence of reconciliations, adjustments, validations, and reporting activities that must be completed accurately and within a regulatory timeframe.

It is also an ideal worked example for the AI Operational Maturity Framework in knowledge work. Month-end close is structured (defined activities, defined sequence), repeatable (same process every period), consequential (material misstatement carries regulatory and reputational exposure), and time-pressured (the close window is fixed). These properties make it a natural candidate for progressive automation — and they make the governance stakes at each stage clear.

This worked example traces month-end close through all six maturity stages. The process is the same at every stage. What changes is how the work is done, who does it, and how it is governed.

---

## The Process

Month-end close for a mid-sized finance function includes:

1. **Sub-ledger closing** — close all transaction sources (AP, AR, payroll, expenses, fixed assets) and ensure no late entries are processed after the cutoff
2. **Intercompany reconciliation** — match and eliminate intercompany transactions between entities
3. **Account reconciliation** — reconcile all balance sheet accounts to supporting schedules
4. **Journal entries** — post recurring accruals, prepayments, and manual adjustments
5. **Variance analysis** — review actuals against budget and prior period; investigate material variances
6. **Financial statement preparation** — produce the draft P&L, balance sheet, and cash flow statement
7. **Management review** — controller review of draft financials, issue resolution, sign-off
8. **Reporting** — distribute management accounts, prepare regulatory submissions where required

---

## Stage 1 — Prompt Engineering

### How the work gets done

Finance analysts use language models to assist with specific, bounded tasks within the close process: drafting variance analysis commentary, suggesting journal entry narratives, checking reconciliation formats. Each interaction is manual and person-driven.

The model is a writing and calculation assistant. The analyst provides the numbers, the context, and the judgement; the model helps express findings clearly or check arithmetic. No structured integration exists between the AI tooling and financial systems.

**Typical Stage 1 activities:**
- Controller asks the model to draft commentary for a significant revenue variance; reviews and edits manually
- AP analyst uses the model to format a reconciliation output; pastes into the schedule
- FP&A uses the model to generate first-draft management commentary; edits against actuals

**The close timeline:** Same duration as the pre-AI close. Productivity gains are individual and uneven. Knowledge of what prompts work well sits with individuals who have experimented, not with the function.

**Key risk:** Close quality depends on individual prompt skill. There is no team prompt library, no shared quality standard, no governance of how AI is used in the close process.

---

## Stage 2 — Context Engineering

### How the work gets done

Context-aware agents assist with high-volume, structured close tasks. The finance data environment — chart of accounts, trial balance, budget files, prior-period comparatives, reconciliation templates — is structured and fed into agent context pipelines.

Agents can perform account reconciliations against structured schedules, identify unexplained variances above defined thresholds, draft journal entry proposals for recurring items, and produce first-draft variance commentary by comparing actuals to budget.

Human finance staff review all agent outputs. The controller reviews the complete close package before sign-off. No output proceeds without human review.

**What agents handle at Stage 2:**
- High-volume account reconciliations (bank reconciliations, intercompany matching)
- First-pass variance analysis for accounts within defined materiality thresholds
- Recurring journal entry drafts (monthly accruals, prepayments)
- Draft management commentary based on actuals-vs-budget comparisons

**What humans handle:**
- Review of all agent outputs
- Non-recurring journal entries requiring judgement
- Material variance investigation and resolution
- Controller sign-off
- Regulatory submission preparation

**The close timeline:** Measurably shorter. The high-volume reconciliation work that previously occupied junior staff for days is completed in hours. Human review time increases proportionally, but total close time decreases.

**Key risk:** Context rot — if the chart of accounts, budget files, or policy documentation is not kept current in the context pipeline, agents produce outputs based on stale data. Finance context has daily freshness requirements that differ from most knowledge work domains.

---

## Stage 3 — Intent Engineering

### How the work gets done

Intent-aware agents handle a broader scope of close activities. The intent manifest encodes the financial governance principles that guide agent decisions: materiality thresholds, accounting policy choices, variance investigation triggers, journal entry authorisation rules, and inter-period comparison standards.

Agents can now make policy-consistent decisions within the encoded intent — for example, applying the correct accounting treatment for a transaction type based on encoded policy rather than requesting human guidance. When a transaction falls outside the manifest's coverage, agents escalate with a structured query.

**The intent manifest for month-end close covers:**

| Intent area | Example encoded guidance |
|---|---|
| Materiality | Variances exceeding £50,000 or 5% of budget (whichever is lower) MUST be investigated before sign-off |
| Accounting policy | Revenue recognition follows IFRS 15 five-step model; specific product line treatments are documented in Annex A |
| Journal entry authority | Recurring journals: agent may post within defined parameters. Non-recurring: controller pre-approval required |
| Intercompany | Mismatches exceeding £1,000 must be escalated with a structured query before elimination |
| Comparative period | Prior period restatements require CFO notification regardless of amount |

**What agents handle at Stage 3:**
- Everything from Stage 2, plus guided policy application
- Automatic application of accounting treatment based on encoded policy
- Escalation of exceptions with structured queries rather than ad hoc emails

**What humans handle:**
- Review of high-materiality items
- Non-recurring journals
- Escalation responses
- Controller and CFO sign-off

**The close timeline:** Further compressed. The bulk of the close is agent-driven. Human time is concentrated on high-value review and exception handling.

**Key governance requirement:** The intent manifest must be updated when accounting policies change or when regulatory requirements are amended. The finance team must own the manifest content; the technology team owns the format and infrastructure. This shared ownership must be explicit.

---

## Stage 4 — Specification Engineering

### How the work gets done

Autonomous agents own the month-end close workflow. The specification corpus contains the rules governing every routine decision class in the close process: account treatment rules, reconciliation standards, journal authorisation limits, variance thresholds, intercompany elimination procedures.

The controller's role is not to review individual close outputs — it is to govern the specification corpus and respond to escalations. When the corpus covers a situation, agents act and the action is logged to the audit trail. When the corpus does not cover a situation, an escalation package arrives.

**The close timeline:** The close runs continuously from day 1 of the period. Sub-ledger cutoffs, reconciliations, and journal processing happen in real time throughout the month, not as a month-end crunch. The "close" is largely complete by the last business day, with sign-off the primary human activity.

**Key artefacts at Stage 4:**

*Specification Corpus — Month-End Close Domain:* Machine-readable rules covering account reconciliation standards, journal authorisation matrix, materiality thresholds by account type, IFRS treatment classifications, intercompany elimination rules, and variance investigation triggers. Every rule traceable to the intent manifest and to the regulatory or policy basis.

*Audit trail:* Every transaction processed, every reconciliation completed, every journal posted — logged with the corpus entry ID and version that governed the decision. SOX-compliant evidence package generated automatically.

*Escalation packages:* Structured documents containing: the specific situation requiring human decision, the relevant corpus gap, the options available (with accounting implications of each), the urgency classification, and the regulatory deadline if applicable.

**What the controller does at Stage 4:**
- Maintains the specification corpus — proposing and approving changes within the governance process
- Responds to escalation packages — making the decisions the corpus cannot make
- Reviews close metrics — escalation rate, corpus gap patterns, audit trail completeness
- Signs off the financial statements — the close is a governance act, not an operational one

**Key risk at Stage 4:** Specification corpus quality. A corpus with ambiguous entries produces inconsistent agent decisions. A corpus with coverage gaps produces high escalation rates. A corpus with undetected conflicts produces non-deterministic behaviour at decision boundaries. The quality gate for corpus entry admission must be maintained under the time pressure of a real close cycle.

---

## Stage 5 — Harness Engineering

### How the work gets done

The harness governs the close process continuously. It monitors: journal posting rates, reconciliation completion rates, escalation patterns, corpus coverage for the period's actual transaction mix, and audit trail completeness.

The harness detects anomalies before they affect close quality or timeline:

- An unusual journal entry pattern (posting frequency spike, unusual account combinations) triggers a behavioural anomaly alert before the controller would otherwise notice
- A context freshness degradation in the FX rates feed triggers a harness alert before agents process transactions using stale rates
- An escalation rate spike in a specific account class signals a corpus gap that is likely to recur, prompting a pre-emptive corpus extension

**Self-healing playbooks for the close process:**

*Playbook FIN-HNS-001 — FX rate feed degradation:*
Precondition: FX rate freshness exceeds 4 hours for any actively-used currency pair.
Actions: Switch to secondary FX rate source; flag to treasury operations; hold transactions in affected currencies pending confirmation.
Escalation trigger: Secondary source also degraded or unavailable.

*Playbook FIN-HNS-002 — High-volume reconciliation anomaly:*
Precondition: Bank reconciliation completion rate falls below 95% with more than 2 hours remaining before cutoff.
Actions: Surface incomplete reconciliation list to finance team; increase sampling rate for anomaly detection.
Escalation trigger: Completion rate continues to decline; escalate to controller with time-to-deadline alert.

**The MTTD requirement for finance:** Financial data systems have regulatory reporting deadlines. An anomaly that is detected after the reporting deadline cannot be remediated. MTTD targets in finance must account for the close calendar — tighter targets apply in the days before close deadlines.

---

## Stage 6 — Environment Engineering

### How the work gets done

The financial environment has been redesigned for AI legibility. The consequences are structural:

**Machine-readable chart of accounts:** The chart of accounts is a formal machine-readable contract — every account has a stable ID, explicit account type classification, applicable IFRS treatment codes, materiality thresholds, and reconciliation standard reference. Agents navigate the chart of accounts by contract, not by interpretation.

**Transaction classification at source:** Source systems (AP, AR, payroll) emit transactions with explicit IFRS classification metadata attached at origination — agents do not classify transactions retrospectively. The classification is a property of the transaction, not a downstream inference task.

**Intercompany elimination by construction:** Intercompany transactions carry matching identifiers from both entities at origination. The elimination is mechanical — matching by identifier rather than by reconciliation — reducing the reconciliation task from hours of matching to seconds of identifier lookup.

**Regulatory reporting contracts:** The regulatory reporting environment publishes machine-readable templates with explicit field-level taxonomy references. Agents populate regulatory reports by mapping against the taxonomy contract, not by interpreting submission guidance.

**The close at Stage 6:** The month-end close, as a distinct crunch period, largely disappears. Continuous accounting — where every transaction is classified, reconciled, and provisionally reported as it occurs — replaces the periodic close with a continuous process. The period-end activity is validation and sign-off, not processing.

| Close activity | Stage 4 | Stage 6 |
|---|---|---|
| Sub-ledger closing | Day 1 of close window | Continuous — no crunch |
| Account reconciliation | Automated, period-end | Continuous — real-time |
| Journal entry processing | Autonomous within corpus | Continuous — event-driven |
| Variance analysis | Period-end | Continuous — threshold-triggered |
| Financial statement draft | Close window | Available on demand |
| Controller sign-off | End of close window | Ongoing — exception-based |
| SOX evidence package | Generated at close | Available on demand |

---

## The Governance Stakes in Finance

Finance is different from software engineering in one critical way: outputs cannot be rolled back. A line of code that is deployed incorrectly can be reverted. A financial statement that is filed incorrectly triggers a restatement, regulatory scrutiny, and reputational damage. A material misstatement that is missed because the specification corpus was inadequate is not just a technical failure — it is potentially a legal and regulatory one.

This makes the specification corpus quality standard in finance *more* demanding than in software engineering, not less. Every corpus entry that governs a decision affecting reported figures requires:

- Explicit accounting policy reference (IFRS/GAAP standard, article, and interpretation)
- Materiality threshold that defines when the agent decision is within scope and when it must escalate
- A regulatory filing deadline reference if the decision affects a submitted figure
- Dual-ownership on change governance — controller approval and compliance review for any corpus change affecting reported figures

The Dark Factory in finance does not lower governance requirements. It systematises and scales them.

---

*Continue to: [Worked Example: Legal Contract Review at Each Stage](./legal-contract-review-worked-example.md)*  
*Back to: [Feature Delivery Worked Example](./feature-delivery-worked-example.md) · [Enterprise Knowledge Work Map](../05-strategy/enterprise-knowledge-work-map.md)*
