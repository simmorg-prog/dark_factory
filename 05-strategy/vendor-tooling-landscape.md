# Vendor & Tooling Landscape

*E5-06 · Wave 7 — Strategy · Audience: Technology Leaders, Architects, Procurement*

> See also: [Investment & Roadmap Planning Guide](./investment-roadmap.md) · [Maturity Assessment Framework](./maturity-assessment-framework.md) · [Specification Corpus Architecture](../02-artefacts/specification-corpus.md) · [Environment Map Reference Design](../02-artefacts/environment-map.md)

---

## Overview

This document maps the tooling categories relevant to each stage of the AI Operational Maturity Framework. It is a structural guide, not a vendor comparison. Tool categories are described by what they need to do — not by which vendor does it best at any given moment, since the market is evolving faster than any static document can track.

Three principles govern how technology decisions should be made within this framework:

> **The Practice Premium Principle:** Technology commoditises. Durable advantage lies in practice discipline, not tool selection. The correct tool decision is: minimum technology investment that enables current-stage practice, with no purchase of Stage N+1 infrastructure before Stage N practice is established.

> **The Lowest Solid Layer Rule:** Technology scores above the Effective Practice Stage are Maturity Debt. Infrastructure cannot compensate for absent practice — it amplifies whatever practices exist. Buying Stage 4 tooling at Stage 2 practice produces Stage 2 outcomes at Stage 4 cost.

> **The Vendor-Independence Principle:** The specification corpus, intent manifest, and audit trail are strategic organisational assets. They must be maintained in formats that survive vendor transitions. Lock-in on these assets is a governance risk, not just a commercial risk.

---

## How to Read This Document

Each section covers one stage's tooling category. For each category, the document describes:

- **What the tooling must do** — the functional requirement from the framework's perspective
- **What to look for** — selection criteria that are independent of specific vendor choices
- **What to avoid** — specific failure patterns in tool selection for that stage
- **Build vs. buy considerations** — when building is appropriate and when it is not

Tool selections should be made in this order: understand the functional requirement from the framework, assess candidate tools against that requirement, select the minimum viable option for current practice maturity, then upgrade as practice matures.

---

## Stage 1 — Prompt Engineering Tooling

### Category: Model Access

**What it must do:** Provide reliable, governed access to one or more large language models with sufficient capability for the organisation's primary use cases.

**What to look for:**
- Latency and reliability SLAs appropriate to production use
- Data handling terms that are compliant with the organisation's regulatory requirements (particularly for regulated industries)
- Cost models that are predictable at the organisation's usage scale
- API stability — model version pinning or deprecation notice policies
- Support for the context window sizes the organisation's workflows require

**What to avoid:**
- Selecting a model on benchmark performance alone without testing against actual workflows
- Contracts that grant the vendor training rights over the organisation's data without explicit review
- Over-investment in custom model infrastructure before standard APIs have been thoroughly validated

**Build vs. buy:** Buy. Model training and hosting is not a competitive differentiator for organisations in knowledge work domains. The frontier model providers have infrastructure advantages that are not replicable. The organisation's advantage lies in how it uses the model, not in which model it built.

---

### Category: Prompt Storage and Governance

**What it must do:** Provide a shared, version-controlled repository for prompts that can be accessed by the whole team, reviewed before production use, and updated with change history.

**What to look for:**
- Version control with diff-visible history (so prompt changes are reviewable)
- Access controls that distinguish read vs. write permissions
- Tagging and search for prompt discovery
- Integration with the workflow tooling where prompts are used
- Export formats that are vendor-neutral

**What to avoid:**
- Personal note-taking tools that cannot be shared or governed (Notion personal pages, local files, browser bookmarks — these are Stage 1 Anti-Pattern AP-01)
- Platforms that store prompts only in proprietary formats without export
- Enterprise prompt management platforms deployed before a prompt governance practice exists — the platform becomes an expensive filing cabinet

**Build vs. buy:** Lightweight: a version-controlled repository (git) with structured metadata is sufficient for Stage 1. Enterprise prompt management platforms are appropriate only when the team has outgrown version control for prompt management.

---

## Stage 2 — Context Engineering Tooling

### Category: Vector Storage and Retrieval

**What it must do:** Store embedded representations of knowledge base content and retrieve relevant content in response to agent queries, with sufficient speed, relevance, and volume capacity for the organisation's workflows.

**What to look for:**
- Retrieval quality metrics (precision, recall, MRR) that can be measured and trended
- Metadata filtering to support context schema requirements (freshness, content category, source)
- Hybrid retrieval (dense + sparse) for domains with specialised terminology
- Scalability to the knowledge base volume required
- Export formats that prevent asset lock-in

**What to avoid:**
- Deploying vector infrastructure before context schemas are defined — retrieval without a schema retrieves what is available, not what is required
- Selecting on index size benchmarks alone without testing on the organisation's actual queries
- Platforms where retrieval quality is opaque (no visibility into why a chunk was retrieved or not)

**Build vs. buy:** Buy for the retrieval infrastructure; build for the schema and quality measurement layer. The schema and measurement tooling should be owned by the organisation, since it encodes the context requirements that are specific to the organisation's workflows.

---

### Category: Knowledge Base Management

**What it must do:** Ingest, organise, version, and maintain the content that feeds the retrieval pipeline, with provenance metadata, freshness tracking, and ownership assignment.

**What to look for:**
- Provenance metadata support (source, ingestion date, last verified date, owner)
- Freshness alerting (configurable thresholds by content category)
- Change propagation (when a document is updated, the index is updated)
- Content owner assignment per category
- Audit log of content changes

**What to avoid:**
- Knowledge management platforms selected for user-experience features (nice UIs) without evaluating their retrieval-quality implications
- Platforms that do not support provenance metadata — without provenance, freshness governance is impossible
- Conflating internal collaboration tooling (wikis, shared drives) with knowledge base infrastructure — they serve different purposes and should not be merged

**Build vs. buy:** This decision depends on existing infrastructure. Organisations with well-governed document management systems can adapt them. Organisations without should consider purpose-built knowledge base platforms or lightweight custom solutions that satisfy the provenance and freshness requirements.

---

### Category: Retrieval Quality Monitoring

**What it must do:** Measure whether the retrieval pipeline is returning content that is relevant to the query, fresh enough to be reliable, and consistent over time.

**What to look for:**
- Retrieval quality metrics dashboards (not just infrastructure metrics)
- Alerting on quality degradation below defined thresholds
- Query-level logging for diagnostic investigation
- Baseline comparison (current quality vs. established baseline)

**What to avoid:**
- Infrastructure monitoring tools repurposed for retrieval quality — infrastructure uptime is not retrieval quality
- Monitoring that measures token counts and latency but not relevance
- Point-in-time quality measurement without trending (single measurements cannot detect degradation)

**Build vs. buy:** Custom measurement layer built against standard metrics (MRR, nDCG, precision@k). This is typically built, since it must be calibrated to the organisation's specific quality thresholds and content categories.

---

## Stage 3 — Intent Engineering Tooling

### Category: Intent Manifest Management

**What it must do:** Store, version, and publish the intent manifest in a format that agents can access, with a change history that allows manifest updates to be reviewed and traced.

**What to look for:**
- Version control with full change history
- RFC 8174 clause structure supported (MUST/SHALL/SHOULD normative precision)
- Metadata fields for clause ID, version, derived-from (for corpus traceability at Stage 4), effective date
- Access controls that distinguish authors (domain authorities) from readers
- Machine-readable export format (YAML or JSON for agent injection)

**What to avoid:**
- Document management systems that treat the manifest as an unstructured document — without structured clause IDs, traceability from corpus entries to manifest clauses is impossible
- Platforms where the manifest format is proprietary — the manifest is a strategic asset that must survive vendor transitions
- Collaborative writing tools without structured metadata support — rich text is insufficient for manifest governance

**Build vs. buy:** Lightweight: a structured YAML or JSON file in version control (git) with a simple web rendering layer is sufficient for most organisations. Purpose-built intent management platforms are appropriate only for very large-scale deployments.

---

### Category: Agent Decision Tracing

**What it must do:** Record which intent manifest clause influenced which agent decision, enabling the governance loop to verify that decisions reflect encoded intent.

**What to look for:**
- Clause ID and version logged with each decision
- Query interface for "which decisions were influenced by clause X in the last 30 days?"
- Integration with the audit trail infrastructure (at Stage 4, this becomes the full audit log)
- Retention policy aligned with governance requirements

**What to avoid:**
- Natural language decision explanations without structured clause references — explanations cannot be audited; clause IDs can
- Tracing infrastructure that only records what the agent decided, not the specification that authorised the decision

**Build vs. buy:** Custom development is typically required here. Few commercial products provide decision-to-manifest-clause traceability as a primary feature. The logging layer should be built against the organisation's specific manifest structure.

---

## Stage 4 — Specification Engineering Tooling

### Category: Policy-as-Code Infrastructure

**What it must do:** Express specification corpus entries as machine-executable policy, evaluate those policies against inputs, and return a governed decision with an audit reference.

**What to look for:**
- First-class support for the specification disciplines: normative precision, atomicity, testability
- Conflict detection — does the platform detect contradictory rules before admission?
- Traceability — does each evaluation record the corpus entry ID and version that produced the decision?
- Human-readable and machine-executable in the same artefact — the specification must be reviewable by non-engineers
- Open, vendor-neutral format for long-term asset preservation

**Relevant technology categories:**
- **OPA/Rego (Open Policy Agent):** Open-source, widely adopted, strong community. Rego is human-readable for technical reviewers. Works well for admission control and decision enforcement. Does not natively support structured specification metadata; the metadata layer must be built alongside it.
- **Cedar (AWS):** Purpose-built for authorisation decisions; strong formal verification properties. Native support for structured policies with schema validation. Newer ecosystem than OPA.
- **Structured YAML/JSON with validation:** For organisations not yet at the stage of requiring full policy-as-code, structured YAML with JSON Schema validation provides version-controlled, human-readable corpus entries with basic quality gates.
- **OSCAL (NIST):** Appropriate for organisations with regulatory compliance requirements where the specification corpus must satisfy NIST or FedRAMP frameworks.

**What to avoid:**
- Policy platforms that do not support per-decision audit references — without audit references, the audit trail requirement cannot be satisfied
- Specification management platforms with proprietary formats — the corpus is a multi-decade asset
- Platforms that do not support conflict detection — manual conflict management does not scale above ~50 corpus entries

**Build vs. buy:** Policy evaluation engines should be bought (OPA, Cedar) or adopted open-source. The corpus governance layer — admission process, conflict detection orchestration, audit integration — is typically built on top of the evaluation engine.

---

### Category: Audit Trail Infrastructure

**What it must do:** Record an immutable, independently reviewable log of every agent decision, with the corpus entry ID, corpus version, input summary, decision, and timestamp.

**What to look for:**
- Append-only storage (immutability)
- Cryptographic integrity verification (tamper evidence)
- Indexed query access (for regulatory inquiry and pattern analysis)
- Retention policy aligned to regulatory requirements
- Access controls that prevent modification by the teams whose decisions are logged

**What to avoid:**
- Application-layer audit logs that can be modified by the application itself
- Audit infrastructure that records what the agent decided but not which corpus entry authorised it
- Log storage with retention periods shorter than regulatory requirements (varies by domain: financial services typically 7 years; healthcare varies by jurisdiction)

**Build vs. buy:** The storage layer should use existing enterprise audit infrastructure (SIEM, immutable object storage). The schema design — specifically the decision record structure — must be custom designed to satisfy the specification corpus traceability requirement.

---

### Category: Escalation Management

**What it must do:** Route agent escalations to the appropriate human decision-maker, track SLA compliance, record human decisions, and feed resolved escalations back to the corpus extension process.

**What to look for:**
- Structured escalation package format (not free-form tickets)
- SLA tracking with alerts on breach
- Routing rules based on escalation type and decision authority
- Integration with the corpus update process (resolved escalations should produce corpus extension candidates)
- Audit log of all human decisions made via the escalation system

**What to avoid:**
- Generic helpdesk ticketing systems not adapted for escalation package requirements — the package must contain all information the human decision-maker needs, in a structured format, before the ticket is created
- Escalation systems that do not track SLA compliance — untracked escalation SLAs will fail without detection

**Build vs. buy:** This is typically built on top of existing workflow or ticketing infrastructure, with customisation to support the escalation package format and corpus extension integration.

---

## Stage 5 — Harness Engineering Tooling

### Category: Behavioural Monitoring

**What it must do:** Monitor agent behaviour against established baselines, detect anomalies in real time, and alert the harness operator before anomalies produce harmful outcomes.

**What to look for:**
- Baseline management — the ability to define, store, and update behavioural baselines per agent
- Anomaly detection against baselines (not just threshold alerts on infrastructure metrics)
- Agent-level monitoring (not just infrastructure-level — CPU, memory, latency are insufficient)
- Alert quality controls (false positive rate management, alert fatigue prevention)
- MTTD measurement capability

**Relevant technology categories:**
- **ML model monitoring platforms** (Evidently AI, WhyLabs, Arize): Designed for production ML models; applicable to agent output monitoring with adaptation. Strong on distribution shift detection.
- **Observability platforms** (Datadog, Grafana, Honeycomb): Strong infrastructure monitoring; require custom instrumentation for agent-level behavioural metrics.
- **Custom harness:** For organisations where the off-the-shelf platforms do not support the behavioural metrics specific to their agents — specification compliance rate, escalation frequency, decision pattern consistency. Custom harnesses are more work but produce metrics that are directly actionable for corpus governance.

**What to avoid:**
- Infrastructure monitoring tools repurposed as behavioural monitors — they cannot detect specification non-compliance or decision pattern drift
- Deploying harness infrastructure before behavioural baselines are established — monitoring without a baseline produces alerts without context
- Platforms where the alert threshold configuration is opaque — if the threshold logic cannot be audited, harness governance cannot be demonstrated

**Build vs. buy:** Hybrid. Infrastructure monitoring should be bought. The behavioural monitoring layer — baseline management, specification compliance monitoring, decision pattern tracking — typically requires custom development on top of the observability infrastructure.

---

### Category: Self-Healing Playbook Infrastructure

**What it must do:** Execute approved autonomous responses to detected anomalies, with full audit logging, scope controls, and human override capability.

**What to look for:**
- Playbook approval workflow — no playbook executes without formal authorisation
- Scope enforcement — playbooks cannot execute actions outside their authorised scope
- Execution audit log — full record of every playbook firing, including trigger, action taken, and outcome
- Human override mechanism — any playbook can be halted by an authorised human
- Rollback support — playbook actions that are reversible should have an associated rollback

**What to avoid:**
- Runbook automation platforms configured to execute without governance review — autonomous remediation without approved playbooks is ungoverned automation, not a harness
- Platforms that do not log playbook execution to the audit trail

**Build vs. buy:** The execution infrastructure can use existing runbook automation or workflow orchestration platforms. The governance layer — approval workflow, scope controls, execution audit — must be custom built and integrated with the audit trail.

---

## Stage 6 — Environment Engineering Tooling

### Category: Environment Mapping and Documentation

**What it must do:** Maintain a machine-readable, versioned map of all APIs, data sources, legacy systems, and external dependencies that agents interact with, with AI legibility scores and API contract links.

**What to look for:**
- Structured data model for environment components (API, data source, legacy system, external service)
- AI legibility assessment fields per component
- API contract linkage (links to OpenAPI, AsyncAPI, or equivalent)
- Change history and review cadence tracking
- Export formats compatible with agent tooling (so agents can access the environment map at runtime)

**What to avoid:**
- Architecture documentation tools not adapted for machine-readable export — PDF architecture diagrams are not an environment map
- Platforms where the map cannot be accessed programmatically by agents

**Build vs. buy:** The environment map is typically a structured YAML or JSON asset in version control, with tooling built around it for rendering, search, and access. Purpose-built architecture documentation tools can be adapted if they support machine-readable export.

---

### Category: API Contract Management

**What it must do:** Define and maintain machine-readable contracts for APIs consumed by agents, enabling agents to understand what each API provides, how to call it, and what errors to expect.

**What to look for:**
- OpenAPI 3.x or AsyncAPI for synchronous and asynchronous APIs respectively
- Contract validation tooling (verifies that the implementation matches the contract)
- Breaking change detection (alerts when a contract update is breaking for current consumers)
- Contract registry (central, versioned repository of all active contracts)

**What to avoid:**
- API documentation tools that produce human-readable docs but not machine-readable contracts — human-readable docs are insufficient for agent consumption
- Contracts that are not versioned or do not have deprecation policies

**Build vs. buy:** OpenAPI/AsyncAPI are open standards; tooling ecosystem is mature. The contract registry layer typically requires light custom integration with the environment map. Contract validation tooling (Dredd, Schemathesis) is available open-source.

---

## Cross-Stage Infrastructure Considerations

### The Strategic Assets

Three artefacts are strategic organisational assets that must be protected from vendor lock-in regardless of what tooling is chosen:

**The specification corpus.** This is the primary governance instrument for Stage 4+ operations. It must be maintained in a vendor-neutral, version-controlled format. If the corpus is locked in a proprietary platform, it cannot be migrated without reconstruction — and reconstruction from a live corpus is a governance risk, not just an operational cost.

**The intent manifest.** The manifest encodes organisational priorities and strategic intent. It must be in a format the organisation owns and controls. A manifest locked in a platform the organisation does not control is a strategic dependency, not just a technical one.

**The audit trail.** The audit trail is the legal and regulatory accountability record. It must be in a format that can be independently audited, that survives vendor transitions, and that satisfies regulatory retention requirements. Audit trails in proprietary formats are inadequate as accountability instruments.

### Build-Buy-Partner Framework

For each tooling category in the framework, the decision structure is:

| Infrastructure Type | Default Decision | Rationale |
|---|---|---|
| Model API access | Buy | Frontier model infrastructure is not replicable; advantage lies in usage, not build |
| Storage infrastructure (vector, object, audit) | Buy (open standards) | Commodity storage should not be custom-built; buy with vendor-neutral formats |
| Policy evaluation engine | Adopt open-source (OPA, Cedar) | Strong community, vendor-neutral, proven in production |
| Monitoring infrastructure | Buy + extend | Base observability is commodity; behavioural monitoring layer requires custom build |
| Governance layer (admission process, escalation routing, manifest governance) | Build | Organisation-specific; must match the organisation's specific corpus structure and governance design |
| Strategic assets (corpus, manifest, audit trail) | Build/own | These are owned organisational assets; they are not bought from a vendor |

---

## Evaluating Vendors Against the Framework

When evaluating any AI tooling vendor against the needs of this framework, the following questions reveal whether the tool supports framework-compliant operations:

**Specification corpus:** Does the platform support atomic, versioned specification entries with metadata for clause ID, version, derivation, and effective date? Does it provide conflict detection? Does it produce audit references with each evaluation?

**Audit trail:** Is the audit log immutable? Does it record corpus entry ID and version with each decision? What is the retention model and can it satisfy regulatory requirements?

**Intent management:** Does the platform support structured RFC 8174 clause management? Can clauses be queried by agents programmatically?

**Harness:** Does the platform support behavioural baseline management? Can it monitor specification compliance rate, not just infrastructure metrics? Does it support playbook approval governance?

**Data portability:** Can all governed assets (corpus, manifest, audit log) be exported in vendor-neutral formats? What is the migration path if the vendor discontinues the product?

A vendor that cannot answer these questions in the affirmative is not a suitable foundation for Stage 4+ Dark Factory operations — regardless of sales positioning, analyst ratings, or reference customers.

---

*Back to: [Investment & Roadmap Planning Guide](./investment-roadmap.md) · [Specification Corpus Architecture](../02-artefacts/specification-corpus.md)*
