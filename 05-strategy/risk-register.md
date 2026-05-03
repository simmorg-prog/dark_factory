# Risk Register — Across All Stages

*E5-04 · Wave 7 — Strategy · Audience: Technology Leaders, Risk, Compliance*

> See also: [AI Governance in the Dark Factory](./ai-governance.md) · [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md) · [Anti-Patterns Library](../04-examples/anti-patterns.md)

---

## Overview

This risk register documents the primary risks that arise at each stage of the AI Operational Maturity Framework. It is organised by risk category and stage, with likelihood, impact, and mitigations for each.

Two principles govern the structure of this register:

**Stage-specific risks are real.** Each stage introduces risks that did not exist at the previous stage. The register does not attempt to document every possible risk — it documents the risks most likely to materialise at each stage and most likely to be underestimated.

**Risk accumulates with stage.** Higher stages do not replace lower-stage risks — they inherit them. A Stage 4 operation carries all Stage 1 through 3 risks plus its own. Mitigation must be maintained across all active stages, not just the current one.

---

## How to Use This Register

Each risk entry contains:
- **Description** — what the risk is and how it manifests
- **Stage** — when this risk is most relevant
- **Likelihood** — probability of occurrence if unmitigated (H/M/L)
- **Impact** — severity of consequences if it materialises (H/M/L)
- **Leading indicators** — observable signals that the risk is increasing
- **Mitigation** — primary controls that reduce likelihood or impact

This register is a starting point for organisational risk assessment. It should be augmented with domain-specific risks and tailored to the organisation's operating context.

---

## Category 1 — Specification Risks

### SR-01 — Specification Ambiguity

**Description:** Specifications are written in ambiguous natural language that admits multiple valid interpretations. Agents apply different interpretations inconsistently, or apply an interpretation the organisation did not intend.

**Stage:** 1 through 6 (originates at 1, compounds at every stage)
**Likelihood:** H (most common specification failure mode)
**Impact:** Varies — L at Stage 1 (inconsistent outputs), H at Stage 4 (systematic wrong decisions at scale)

**Leading indicators:**
- Multiple agents completing the same task produce different outcomes
- Human reviewers override agent outputs but cannot articulate a precise rule for why
- Escalation packages cite "unclear guidance" as the gap

**Mitigation:**
- RFC 8174 normative precision from Stage 1 onward — obligation keywords carry normative force
- Atomicity (one obligation per specification unit) — prevents bundled ambiguities
- Test cases co-located with specifications — ambiguity becomes visible when a test cannot be written
- Peer review of specification clauses with explicit challenge: "What are the five scenarios this clause governs, and does it produce the right answer for all five?"

---

### SR-02 — Specification Drift

**Description:** The specification corpus diverges from the intent manifest over time. Corpus entries are updated without updating the intent clauses they derive from, or vice versa. Agents enforce rules that no longer reflect organisational intent.

**Stage:** 4 through 6
**Likelihood:** M (requires discipline to prevent; discipline typically degrades under operational pressure)
**Impact:** H (agents enforce wrong intent at scale)

**Leading indicators:**
- Corpus entries with no `derived-from` field, or with broken links to the manifest
- Intent manifest updated following a strategy change but corpus entries not reviewed
- Escalation packages that reveal agents applying rules inconsistent with stated intent

**Mitigation:**
- Bidirectional traceability — every corpus entry links to its manifest source; manifest changes trigger corpus review
- Corpus currency review as part of the intent manifest update process
- Regular traceability audits — verify that the corpus-to-intent linkage is intact

---

### SR-03 — Specification Corpus Conflict

**Description:** Two or more specification corpus entries produce contradictory enforcement decisions for the same input. Agents behave non-deterministically at the conflict boundary — producing different outcomes for the same situation.

**Stage:** 4 through 6 (emerges as the corpus grows)
**Likelihood:** M (almost certain in corpora larger than ~100 entries without automated detection)
**Impact:** H (non-deterministic agent behaviour undermines the Dark Factory's accountability premise)

**Leading indicators:**
- Growing corpus without automated conflict detection tooling
- Agent decisions that vary for similar inputs in the same session
- Escalation packages that cite contradictory guidance from different corpus entries

**Mitigation:**
- Automated conflict detection on every corpus update — no new entry admitted without conflict check
- Rule-of-construction clause in the corpus header defining precedence (lex specialis, lex posterior)
- `conflicts-with` field in corpus entries documenting known interactions
- Regular corpus health reviews that run full conflict analysis against the complete corpus

---

### SR-04 — Specification Coverage Gap

**Description:** A situation arises in production that the specification corpus does not cover. Agents are forced to escalate — or, worse, proceed with inferred guidance — in situations the organisation did not anticipate.

**Stage:** 4 through 6
**Likelihood:** H (coverage of 100% of situations is unachievable; gaps will exist)
**Impact:** M (healthy escalation behaviour limits impact; absent escalation behaviour increases it)

**Leading indicators:**
- Escalation rate above defined threshold
- Escalations clustering around a specific decision class (structural gap, not one-off)
- New operational context (new product, new regulation, new counterparty type) without corresponding corpus update

**Mitigation:**
- Coverage assessment before Stage 4 go-live — known gaps documented before autonomous operation begins
- Well-defined escalation behaviour for uncovered situations — agents do not proceed with inference
- Gap register governance — open gaps are tracked, owned, and have defined resolution timelines
- Escalation pattern analysis — recurring gap classes become corpus extensions

---

## Category 2 — Context Risks

### CR-01 — Context Rot

**Description:** Knowledge base content becomes stale relative to operational reality. Agents produce outputs based on outdated information — superseded policies, obsolete code, incorrect data models.

**Stage:** 2 through 6
**Likelihood:** H (content degrades without active maintenance; active maintenance requires governance)
**Impact:** H in regulated domains (decisions based on superseded regulatory content), M in engineering (code generated against outdated APIs)

**Leading indicators:**
- Knowledge base last modified date significantly behind current date
- Agent outputs referencing superseded systems, policies, or standards
- No defined owner for major knowledge base content categories
- Freshness monitoring absent or not reviewed

**Mitigation:**
- Named content owners with explicit freshness SLAs
- Automated freshness monitoring with alert thresholds
- Freshness review as part of operational governance cadences
- Provenance metadata on all content (last verified date, verification owner)

---

### CR-02 — Context Flooding

**Description:** Excessive context is injected without discrimination, exceeding the context window's effective capacity or diluting retrieval relevance. Agent output quality degrades as the signal-to-noise ratio in the context window falls.

**Stage:** 2 through 4
**Likelihood:** M (natural tendency when context requirements are not formally specified)
**Impact:** M (degraded output quality, increased token costs, unpredictable behaviour)

**Leading indicators:**
- Context window utilisation consistently above 90%
- Output quality varies significantly between runs with identical task instructions
- No defined context schema — content injected by availability rather than requirement

**Mitigation:**
- Formal context schemas defining exactly what is required at each workflow step
- Context budget enforcement — hard limits on tokens allocated to each schema element
- Quality measurement before and after context changes
- Progressive injection patterns — inject content as needed, not all at once

---

### CR-03 — Context Source Failure

**Description:** A primary context source fails, degrades, or becomes unavailable. Agents operate without the information the context schema requires, producing lower-quality or incorrect outputs.

**Stage:** 2 through 6
**Likelihood:** M (infrastructure failures are routine; resilience design is not always present)
**Impact:** Varies — M in engineering, H in finance or legal where time-sensitive accuracy is critical

**Leading indicators:**
- No fallback sources for critical context elements
- Retrieval error rate increasing
- No harness monitoring for context source availability

**Mitigation:**
- Redundant sources for critical context elements
- Defined fallback behaviour when primary source is unavailable (pause workflow, use fallback, escalate)
- Harness monitoring for context source health
- Regular failover testing

---

## Category 3 — Intent and Governance Risks

### IGR-01 — Intent Manifest Staleness

**Description:** The intent manifest is not updated following a strategy change, regulatory amendment, or policy revision. Agents apply the previous intent, producing outputs that are systematically inconsistent with current organisational will.

**Stage:** 3 through 6
**Likelihood:** M (update process requires active governance; governance degrades under operational pressure)
**Impact:** H (systematic strategic misalignment in all decisions the manifest governs)

**Leading indicators:**
- Strategy change announced but no manifest update triggered
- Agents producing outputs that feel "wrong" to domain experts despite technical correctness
- Time elapsed since last manifest review exceeds defined cadence

**Mitigation:**
- Manifest update SLA linked to strategy change detection
- Regular manifest currency review as part of governance cadence
- Stakeholder channels that surface strategy changes to manifest owners before operational deployment

---

### IGR-02 — Governance Capture

**Description:** The governance process is captured by the operational team it is supposed to govern. The team reviews its own corpus entries, approves its own playbooks, and assesses its own compliance. Independence is absent.

**Stage:** 4 through 6
**Likelihood:** M (structural independence requires deliberate organisational design; it does not emerge naturally)
**Impact:** H (without independence, governance failures are systematically undetected)

**Leading indicators:**
- Same team authors, reviews, and approves corpus entries
- No external audit of governance process
- Governance metrics are self-reported without independent verification

**Mitigation:**
- Structural separation between teams that operate agents and teams that govern them
- Independent audit of corpus admission process (legal, compliance, or external)
- Independent harness review (separate from harness operators)
- Escalation routing that does not return to the team whose decision triggered the escalation

---

### IGR-03 — Escalation SLA Failure

**Description:** Escalation packages are not responded to within defined SLAs. The Dark Factory is operating against specification gaps without timely human resolution. Agents may proceed with inferred guidance or halt entirely.

**Stage:** 4 through 6
**Likelihood:** M (SLA compliance requires sustained operational commitment)
**Impact:** H (unresolved escalations are unresolved governance gaps operating at production speed)

**Leading indicators:**
- Escalation queue depth increasing
- Average escalation age increasing
- Escalation SLA compliance below defined threshold
- Receiving human team expressing that escalation packages are unclear or underdefined

**Mitigation:**
- Escalation SLA as a governed operational commitment with defined consequences for non-compliance
- Escalation package quality standard — packages must include all information needed for decision
- Escalation receiving team training and rehearsal before Stage 4 go-live
- Escalation queue monitoring with alerts on breach of SLA

---

## Category 4 — Operational Risks

### OR-01 — Harness Failure

**Description:** The harness fails to detect an anomaly in agent behaviour. The anomaly propagates, producing harmful outputs, incorrect decisions, or regulatory exposure before detection.

**Stage:** 4 through 6
**Likelihood:** M (harness failure modes include: wrong signals, stale baselines, alert fatigue, configuration drift)
**Impact:** H (undetected anomalies in a high-throughput system cause significant harm)

**Leading indicators:**
- MTTD increasing over time
- False positive rate high (alert fatigue leading to reduced attention)
- Baselines not reviewed following significant corpus or operational changes
- Harness coverage gaps (some agents not monitored)

**Mitigation:**
- MTTD as a primary governance metric with defined targets
- Independent harness review
- Regular baseline review cadence
- Alert triage to prevent fatigue
- Harness coverage audits

---

### OR-02 — Agent Loop

**Description:** An agent enters a loop state — repeatedly attempting a workflow step that is failing, without detecting that it has failed and escalating. Resources are consumed; the workflow makes no progress; the loop may generate harmful side effects.

**Stage:** 4 through 6
**Likelihood:** L (requires specific conditions, but those conditions arise in complex multi-step workflows)
**Impact:** M-H (resource exhaustion, external API abuse, duplicate side effects)

**Leading indicators:**
- Workflow execution time significantly exceeding expected duration
- Repeated identical calls to external systems within a short window
- No maximum iteration count defined in workflow specification

**Mitigation:**
- Maximum iteration counts enforced at the harness level for every workflow step
- Idempotency design for all external API calls
- Loop detection in the harness — pattern of repeated identical actions triggers alert
- Well-defined failure states with escalation triggers

---

### OR-03 — Proxy Discrimination at Scale

**Description:** An agent system applies a specification that is facially neutral but that produces systematically different outcomes for individuals with protected characteristics — due to proxy features that correlate with those characteristics. At Dark Factory scale, the discrimination is systematic and invisible.

**Stage:** 4 through 6 (at all prior stages, human review can catch patterns; at Stage 4+, review is absent)
**Likelihood:** M (common in any model trained on historical data that reflects past discrimination)
**Impact:** H (regulatory, reputational, and human harm)

**Leading indicators:**
- No proxy analysis in the corpus entry development process for personal data systems
- Subgroup outcome testing not included in specification acceptance criteria
- Proxy discrimination not addressed in the intent manifest

**Mitigation:**
- Proxy discrimination prevention as a mandatory quality dimension for all corpus entries involving personal data
- Subgroup outcome testing as a deployment gate
- Harness monitoring for outcome distribution divergence across protected characteristic groups
- Regular fairness audits with external review

---

## Category 5 — Regulatory and Compliance Risks

### RCR-01 — Regulatory Change Lag

**Description:** A regulatory change takes effect but the specification corpus is not updated within the required window. Agents enforce rules that are no longer legally valid. The organisation is in breach of regulation.

**Stage:** 4 through 6
**Likelihood:** M (regulatory change is continuous; corpus update processes may not be calibrated to regulatory timelines)
**Impact:** H (regulatory breach, enforcement action, reputational damage)

**Leading indicators:**
- No regulatory intelligence process feeding corpus update workflows
- Corpus entries with no regulatory basis field — changes in regulation are not connected to specific entries
- Regulatory effective dates not tracked in corpus versioning

**Mitigation:**
- Regulatory intelligence as a formal input to corpus governance
- Corpus entries with explicit regulatory basis fields and review triggers for regulatory changes
- Regulatory update deadlines treated as corpus deployment deadlines
- Legal and compliance review of corpus entries with regulatory dependencies

---

### RCR-02 — Audit Trail Inadequacy

**Description:** In a regulatory inquiry or legal dispute, the audit trail does not contain the information required to demonstrate what decision was made, on what basis, under what specification version. The organisation cannot reconstruct the decision and cannot defend it.

**Stage:** 4 through 6
**Likelihood:** M (audit trail design is commonly under-specified)
**Impact:** H (regulatory sanction, inability to defend legal position, inability to demonstrate compliance)

**Leading indicators:**
- Audit log does not include corpus entry ID and version for each decision
- Audit log retention period shorter than regulatory requirement
- Audit log accessible to operational teams (integrity at risk)
- No defined audit log review process

**Mitigation:**
- Audit trail specification as a governance requirement, not a technical afterthought
- Immutable audit logs with cryptographic integrity
- Retention policy aligned to regulatory requirements by domain
- Regular audit log completeness and integrity checks

---

## Risk Summary Matrix

| Risk | Stage | Likelihood | Impact | Priority |
|---|---|---|---|---|
| SR-01 — Specification Ambiguity | 1–6 | H | H | Critical |
| CR-01 — Context Rot | 2–6 | H | H | Critical |
| IGR-01 — Intent Manifest Staleness | 3–6 | M | H | High |
| SR-03 — Corpus Conflict | 4–6 | M | H | High |
| OR-03 — Proxy Discrimination at Scale | 4–6 | M | H | High |
| RCR-01 — Regulatory Change Lag | 4–6 | M | H | High |
| SR-02 — Specification Drift | 4–6 | M | H | High |
| IGR-02 — Governance Capture | 4–6 | M | H | High |
| IGR-03 — Escalation SLA Failure | 4–6 | M | H | High |
| OR-01 — Harness Failure | 4–6 | M | H | High |
| RCR-02 — Audit Trail Inadequacy | 4–6 | M | H | High |
| SR-04 — Coverage Gap | 4–6 | H | M | High |
| CR-02 — Context Flooding | 2–4 | M | M | Medium |
| CR-03 — Context Source Failure | 2–6 | M | M | Medium |
| OR-02 — Agent Loop | 4–6 | L | H | Medium |

---

*Continue to: [AI Governance in the Dark Factory](./ai-governance.md) · [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md)*  
*Back to: [Dark Factory Definition](../00-foundations/dark-factory.md)*
