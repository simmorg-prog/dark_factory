# AI Governance in the Dark Factory

*E5-05 · Wave 7 — Strategy · Audience: Technology Leaders, Compliance, Risk*

> See also: [Dark Factory Definition](../00-foundations/dark-factory.md) · [Specification Corpus Architecture](../02-artefacts/specification-corpus.md) · [Risk Register](./risk-register.md) · [Human Role Transformation](../01-actors/human-role.md)

---

## Overview

Governance is not a constraint placed on the Dark Factory. It is the mechanism by which the Dark Factory operates.

At Stage 4 and beyond, agents act autonomously on consequential decisions. The only thing standing between those decisions and uncontrolled outcomes is the quality of the governance infrastructure: the specification corpus, the intent manifest, the audit trail, the escalation protocols, the harness. Governance is not adjacent to operations — it is the operating system.

This has practical implications. Organisations that treat AI governance as a compliance exercise — something to document and file, not to operate — will have Dark Factories that appear well-governed and are not. Governance in the Dark Factory must be functional, not formal. It must produce accountable outcomes, not auditable procedures.

This document covers what functional AI governance looks like at each stage, the regulatory landscape that shapes it, and the governance failure modes that most commonly undermine Dark Factory operations.

---

## Governance at Each Stage

### Stage 1 — Prompt Engineering

The governance requirement at Stage 1 is minimal but not absent. The primary governance concerns are:

**Acceptable use.** Not all applications of Stage 1 AI assistance are appropriate. A policy defining what the model may and may not be used for — what data can be shared with external models, what decisions may not be delegated to model outputs even with human review, what record-keeping is required — is the Stage 1 governance baseline.

**Output quality accountability.** When model-assisted outputs are used in consequential contexts, accountability for quality must rest with the human, not with the model. The governance question is: does the human understand that they are responsible for reviewing and approving the output?

**Data sharing scope.** Most Stage 1 deployments involve sending data to external model APIs. The governance requirement is clarity about what categories of data may be shared, with whom, under what terms. This is particularly acute in regulated domains (health, finance, legal) where data sharing has explicit regulatory constraints.

### Stage 2 — Context Engineering

At Stage 2, governance expands to cover the context infrastructure:

**Knowledge base governance.** Who owns the content of the knowledge base? Who is accountable for its accuracy and currency? What is the freshness SLA and how is it enforced? These governance questions determine whether the context infrastructure degrades silently or is actively maintained.

**Retrieval quality governance.** Context pipelines require ongoing monitoring. The governance question is: who owns retrieval quality metrics, what threshold triggers remediation, and what escalation path exists when quality degrades?

**Third-party data governance.** If the context pipeline incorporates third-party data sources (market data, regulatory updates, external knowledge bases), the governance requirement includes: what terms govern use of that data for AI training or inference, what happens when third-party data is incorrect, and who is liable for outputs derived from it?

### Stage 3 — Intent Engineering

At Stage 3, intent governance becomes the primary concern:

**Intent manifest authority.** Who has the authority to define and amend organisational intent? The manifest encodes strategic priorities — its content must be owned by people with strategic authority, not delegated entirely to engineering.

**Intent update governance.** When organisational strategy changes, the manifest must change within a defined SLA. The governance requirement is an update process that: identifies strategy changes as triggers, routes them to manifest owners, and confirms manifest deployment before the strategy change takes effect operationally.

**Intent audit.** Periodic review of whether agent decisions align with the encoded intent. Not just whether the manifest is current — whether agents are applying it correctly and whether the intent clauses are producing the decisions the organisation actually wants.

### Stage 4 — Specification Engineering

At Stage 4, governance is most complex because the stakes are highest:

**Corpus admission governance.** Every specification corpus entry is a rule that agents will enforce autonomously at scale. The admission process is the primary control: quality gate, conflict detection, legal or compliance review for regulated domains, formal approval. An admission process that degrades under time pressure is a governance failure.

**Change governance.** Corpus changes — particularly breaking changes — require notification to all systems operating against the corpus. The change governance process must define: who approves changes, what constitutes a breaking change, how agents are notified, and what the rollback process is if a change produces unexpected outcomes.

**Audit trail governance.** The audit trail is the primary accountability mechanism at Stage 4. Its completeness and integrity must be governed independently of the corpus. If the audit trail can be modified, its value as an accountability instrument is compromised. Audit log immutability (append-only, cryptographic integrity) is a governance requirement, not a technical nicety.

**Escalation governance.** The escalation loop — from agent to human and back to corpus extension — must be a governed process with defined SLAs, ownership, and metrics. Escalations that are not resolved, or resolved without corpus extension, are governance failures.

### Stage 5 — Harness Engineering

At Stage 5, governance extends to the harness itself:

**Harness independence.** The harness should not be governed by the same team that operates the agents it monitors. Independence is the basis of effective oversight — a team that monitors its own work will not detect failures it is motivated not to find.

**Self-healing playbook governance.** Autonomous harness interventions require explicit authorisation. Every playbook must be approved by an authority that understands its scope and its limits. Playbooks that fire outside their authorised scope represent governance failures.

**Performance accountability.** MTTD and MTTR targets must be governed as operational commitments, not technical aspirations. If the harness consistently misses its MTTD target, that is a governance failure requiring escalation and remediation — not just a metric to track.

### Stage 6 — Environment Engineering

At Stage 6, governance extends to the architectural layer:

**Environment Council authority.** The Environment Council must have genuine decision rights, not advisory standing. If it can be overridden by engineering teams who prioritise product roadmaps over legibility standards, it is governance theatre.

**Environment map integrity.** The map is an operational artefact. Its accuracy must be governed with the same rigour as the specification corpus. Stale map entries are not documentation debt — they are incorrect information that agents navigate by.

**Structural change governance.** Environment redesign decisions are architectural decisions with organisation-wide implications. They require governance at the appropriate level — not just engineering sign-off.

---

## The Regulatory Landscape

The regulatory environment for AI governance is evolving rapidly. The most significant frameworks are:

### EU AI Act

The EU AI Act (Regulation 2024/1689) introduces a risk-based regulatory framework. For Dark Factory operations:

**High-risk systems** — AI systems used in employment, credit, critical infrastructure, education, or essential services fall in the high-risk category and require: conformity assessment, CE marking, registration in the EU database, and ongoing post-market monitoring. The specification corpus, audit trail, and harness are directly relevant to compliance obligations for high-risk systems.

**Transparency obligations** — AI systems that interact with natural persons must disclose that they are AI. Dark Factory systems that produce customer-facing outputs must identify AI-generated content where required.

**Prohibited practices** — social scoring, real-time biometric identification in public spaces, and manipulation of vulnerable groups are prohibited. Specification corpus entries in any of these areas must be reviewed for compliance.

**Governance implication:** Organisations deploying Dark Factory operations in regulated domains within the EU must design their governance infrastructure to satisfy AI Act requirements from Stage 4 onward. Retrofitting compliance to a mature Dark Factory is significantly more expensive than building compliance in.

### UK AI Framework

The UK's approach to AI governance is currently principles-based rather than legislation-based, with sector-specific regulation through existing regulators (FCA, ICO, CQC). The five cross-sectoral principles — safety, security and robustness; transparency and explainability; fairness; accountability and governance; contestability and redress — map directly to Dark Factory governance requirements.

**Accountability and governance** is the principle most directly relevant: organisations must be able to demonstrate who is responsible for AI decisions, how those decisions are made, and how affected parties can contest them. The specification corpus governance, audit trail, and escalation protocols are the primary evidence of compliance.

### Sector-specific requirements

| Sector | Key regulatory framework | Dark Factory governance implication |
|---|---|---|
| Financial services | FCA PS22/2, PRA SS1/23, SR 11-7 (US) | Model risk management, explainability, audit trail |
| Healthcare | MDR/IVDR (EU), MHRA (UK) | Clinical risk classification, change management, post-market surveillance |
| Legal services | SRA Code of Conduct | Supervision obligations, conflict checking, client confidentiality |
| HR and employment | Equality Act 2010, UK GDPR, EU AI Act (high-risk) | Proxy discrimination prevention, human oversight of employment decisions |
| Critical infrastructure | NIS2 Directive, UK NCSC guidance | Resilience, incident reporting, supply chain governance |

---

## Governance Architecture

A functional AI governance architecture for the Dark Factory includes five components:

### 1. Policy layer

The policy layer defines what the organisation will and will not do with AI: acceptable use policy, data governance policy, model risk policy, AI ethics principles. This layer governs what can be built and deployed — it is the outermost constraint.

### 2. Specification layer

The specification corpus and intent manifest are the primary governance instruments for agent behaviour. The specification layer translates policy into enforceable rules. Its governance is the admission process, the change process, and the audit trail.

### 3. Operational layer

The harness is the operational governance mechanism — it monitors whether agents behave consistently with their specifications and surfaces deviations. The operational layer provides real-time governance.

### 4. Accountability layer

The audit trail is the accountability layer — the immutable record of what agents did, under which specification version, with what outcome. The accountability layer enables retrospective review, regulatory inquiry, and dispute resolution.

### 5. Human oversight layer

The escalation process and the governance team are the human oversight layer. They handle decisions outside the specification envelope, govern the specification and harness, and respond to regulatory requirements. The human oversight layer cannot be eliminated — it is what makes the other layers accountable.

These five layers are interdependent. Weakening any one degrades the others: a policy layer without a specification layer is aspirational; a specification layer without an audit layer cannot be verified; an audit layer without a human oversight layer cannot be acted upon.

---

## Governance Failure Modes

**The documented but non-functional process.** Governance procedures exist on paper. Admission review is documented but not consistently applied under time pressure. Audit logs are kept but not reviewed. Escalation SLAs are defined but not tracked. The governance is formal, not functional.

**The missing independence.** The harness is operated by the same team that operates the agents. The specification corpus is reviewed by the same engineers who write it. Audit logs are accessible to the teams they audit. Independence is the basis of effective governance — its absence is a structural vulnerability.

**The governance lag.** Regulation changes. Strategy changes. The specification corpus is not updated within the required window. Agents enforce rules that the organisation no longer intends or that are no longer legally valid. The lag between external change and governance update is the exposure.

**The escalation sink.** Escalation packages arrive but are not resolved within SLA. They accumulate in a queue. Humans are overwhelmed, unclear on their authority, or insufficiently briefed to act. The Dark Factory continues to operate against a specification that cannot handle a growing class of situations. The safety valve does not function.

**The compliance substitution.** The organisation treats regulatory compliance documentation as a substitute for operational governance. Policies are filed, conformity assessments are completed, registration is confirmed — but the underlying governance infrastructure (corpus quality, harness independence, audit trail integrity) does not meet the standard the documentation claims. The gap is not visible until a regulatory inquiry or incident makes it so.

---

## What Good AI Governance Looks Like

Functional AI governance in the Dark Factory has five observable properties:

**It produces auditable decisions.** Every agent decision can be traced to a specific specification clause, version, and intent source. The audit trail is complete, accurate, and immutable.

**It surfaces anomalies before harm.** The harness detects behavioural deviations before they produce harmful outputs. Anomalies are not discovered through customer complaints or regulatory inquiries.

**It responds to change.** When strategy, policy, or regulation changes, the governance infrastructure is updated within defined windows. The update process is tested and proven, not theoretical.

**It handles escalations.** Escalation packages are acted on within SLA. The humans who receive them have the authority, information, and training to make decisions. Escalations produce corpus improvements that close the gaps that generated them.

**It is independently verified.** Governance processes are reviewed by parties independent of those they govern. Audit logs are reviewed. Corpus admissions are checked. Harness performance is assessed against targets. The governance claims are verified, not assumed.

---

*Continue to: [Risk Register — Across All Stages](./risk-register.md)*  
*Back to: [Dark Factory Definition](../00-foundations/dark-factory.md) · [Specification Corpus Architecture](../02-artefacts/specification-corpus.md)*
