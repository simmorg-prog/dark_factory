# Stage 2 Deep Dive — Context Engineering

*E2-02 · Wave 5 — Stages · Audience: All*

> See also: [Stage Transition Playbooks](./stage-transition-playbooks.md) · [Stage 1 Deep Dive](./stage-1-prompt-engineering.md) · [Stage 3 Deep Dive](./stage-3-intent-engineering.md)

---

## Overview

Stage 2 introduces a fundamental shift in how AI systems are designed. At Stage 1, the human carries the context — each prompt includes whatever background the individual knows, assembled manually, freshly each time. At Stage 2, context becomes infrastructure.

Context engineering is the discipline of designing the information environment agents operate within. It asks: what does the agent need to know at each step of the workflow to produce a reliable, high-quality output? Where does that information live? How is it retrieved? How is its quality measured? How is it kept current?

These are architectural questions, not prompt questions. They require skills in information architecture, retrieval system design, and data governance. They also require organisational decisions: who owns the knowledge the agents rely on, and who is accountable when that knowledge degrades.

Stage 2 is where AI moves from individual tool to team infrastructure. The shift is consequential. Infrastructure requires governance. Infrastructure degrades without maintenance. Infrastructure has dependencies that create fragility if not managed. The organisations that treat Stage 2 as a technical upgrade — better prompts, more context — miss the organisational disciplines that make the upgrade durable.

---

## What Stage 2 Looks Like

### The human role

At Stage 2, the human shifts from context courier to context architect. They stop assembling context manually for each interaction and start designing the systems that assemble context automatically. They still review all agent outputs — autonomous operation is not yet appropriate — but the nature of their oversight changes from "did the agent have the right information?" to "is the information architecture working as designed?"

**What the human does:**
- Engineers context pipelines, retrieval systems, and knowledge base architectures
- Defines what information agents receive at each workflow step — the context schema
- Sets quality standards for agent inputs and outputs
- Reviews and approves agent-generated artefacts
- Maintains the knowledge base and retrieval infrastructure

**What transfers to agents:**
- Information assembly — the retrieval pipeline does what the human previously did manually
- First-pass work in bounded domains — code generation, document drafting, research synthesis

**What stays with humans:**
- Architectural decisions about what context is relevant and why
- Quality gate review of all consequential outputs
- Escalation decisions on outputs that fail quality standards

### The agent role

Agents at Stage 2 are persistent workers in bounded workflows. They have retrieval capabilities — they can query knowledge bases, codebases, documentation, and structured data sources. They still lack memory across sessions and they still operate within tight workflow boundaries. But within those boundaries, they produce consistent, high-quality outputs because the information environment they operate in is designed rather than improvised.

---

## The Architecture of Context

### Context schemas

A context schema is the specification of what information an agent receives at each step of a workflow. It is not an implementation — it is a documented requirement. It answers: what must be present in the agent's context for it to produce a reliable output at this step, and in what form?

Context schemas are the primary design artefact of Stage 2. Before building any retrieval system, the schema should exist. Building retrieval without a schema produces systems that retrieve something without a clear criterion for whether they retrieve the *right* things.

A minimal context schema entry includes:

| Field | Description |
|---|---|
| Workflow step | Which step this schema governs |
| Required content | What the agent must have access to — described by content type, not system name |
| Optional content | What may improve output quality but is not required for acceptable quality |
| Excluded content | What must not appear in the context — proprietary, regulated, or scope-limiting |
| Format requirements | Structure the agent expects to receive |
| Freshness requirement | How recent the information must be to be valid |
| Context budget | Maximum tokens allocated to this schema element |

### Retrieval architectures

The retrieval pipeline implements the context schema. Several architectural patterns are available:

**Keyword retrieval** — the simplest form. Full-text search over a document corpus. Fast, predictable, transparent. Fails when the query language differs from the document language (synonyms, paraphrases) or when relevance requires semantic understanding.

**Semantic search / vector retrieval** — embeds documents and queries in a shared vector space; retrieves by similarity. Handles paraphrase and semantic equivalence. Slower than keyword retrieval; requires embedding maintenance; less transparent (why did this document score highly?). Best for unstructured text corpora.

**Structured query** — retrieves from a schema-defined data source using explicit query logic. Fully deterministic. Requires the source to be structured. Cannot handle natural language queries without a translation layer.

**Hybrid retrieval** — combines keyword and semantic search, often with a reranking step. More robust than either alone. More complex to operate and maintain. Appropriate when corpus diversity requires different retrieval strategies for different content types.

**Graph retrieval** — traverses a knowledge graph to retrieve related entities and their relationships. Powerful for tasks requiring multi-hop reasoning. Highest operational complexity. Appropriate when the domain knowledge is inherently relational.

The right architecture depends on the corpus, the query types, and the acceptable complexity ceiling. The most common mistake is implementing semantic search as a default without establishing that keyword retrieval is insufficient. Start with the simplest architecture that meets the schema requirements.

### Context quality measurement

A retrieval system that returns results is not the same as one that returns *good* results. Without measurement, quality degradation is invisible until it manifests as agent output failure.

Key metrics for context quality:

| Metric | What it measures | Why it matters |
|---|---|---|
| Retrieval hit rate | What proportion of queries return at least one relevant result | Whether the corpus covers the query space |
| Relevance score | How well the top results match the query intent | Whether retrieval is returning what is needed |
| Freshness | What proportion of retrieved documents are within defined recency bounds | Whether the agent is operating on current information |
| Coverage | What proportion of the knowledge base is indexed and retrievable | Whether dark data exists outside the retrieval scope |
| Context fill rate | What proportion of schema requirements are satisfied per workflow execution | Whether the schema is achievable in practice |

Establish baseline measurements before deploying agents into production. Anomalies in these metrics are early warnings of quality degradation that, undetected, produce unexplained agent performance decline.

---

## Context Rot

Context rot is the term for knowledge base degradation over time. It is the Stage 2 failure mode that most consistently surprises organisations — because it is invisible until its effects appear in agent outputs.

Knowledge becomes stale. Documents are updated but the indexed version is not. Systems change but the documentation describing them is not revised. Policies are amended but the corpus reflects the previous version. An agent operating on stale context produces outputs that were correct for a world that no longer exists.

Context rot is not a technical failure. It is a governance failure. The retrieval pipeline is working correctly — it retrieves what is there. What is there is outdated.

Preventing context rot requires:

**Ownership.** Every content source in the knowledge base has an owner — a person or team accountable for keeping it current. Without ownership, currency degrades through neglect.

**Freshness SLAs.** Defined maximum ages for content by type. Policy documents: reviewed quarterly. Code documentation: reviewed on each major release. External regulatory content: reviewed when regulatory changes are published. The SLA is an operational commitment, not a guideline.

**Automated freshness monitoring.** Alerts when content exceeds its defined age. Humans should not have to manually audit freshness.

**Retrieval freshness weighting.** Retrieval systems can be configured to penalise older documents in relevance scoring. This is a mitigation for governance failures, not a substitute for them — but it helps.

---

## Context Window Management

Language models have finite context windows. At Stage 2, where multiple sources are retrieved and injected, context window management becomes a design constraint.

**Context budgets** — allocate the available context window across the schema elements. A schema that requires 80% of the available window for retrieved content leaves little room for the task instruction, the output specification, and the model's working space. Budget allocation is an architectural decision that requires measurement of typical content sizes across schema elements.

**Chunking strategy** — most retrieval systems operate on document chunks rather than full documents. Chunk size affects retrieval quality (too small: loss of coherence; too large: dilution of relevance) and context budget efficiency. Chunking strategy should be validated against schema requirements, not assumed.

**Selective injection** — not all schema elements are equally important for all queries. Dynamic context assembly — injecting based on query relevance rather than schema completeness — reduces context bloat. Requires confidence in the relevance scoring system.

**Progressive injection** — in multi-step workflows, inject context incrementally as it becomes needed rather than front-loading everything at the first step. Reduces total context window pressure across the workflow.

---

## Stage 2 in Enterprise Knowledge Work

Context engineering in knowledge work domains presents specific challenges that differ from software engineering.

**Regulated content.** Finance, Legal, HR, and Risk & Compliance operate with content that has regulatory constraints on access, retention, and use. Context pipelines must respect information barriers, data residency requirements, and access controls. The schema must explicitly state who may retrieve what, under what conditions.

**Jurisdiction sensitivity.** A legal knowledge base serving a global organisation contains documents that apply in some jurisdictions and not others. Context schemas must include jurisdiction as a retrieval parameter; agents must not apply UK case law to a US contract.

**Document authority hierarchy.** In policy-heavy domains, multiple versions of the same policy may exist — draft, approved, superseded, in-force. Context pipelines must retrieve the authoritative version, not just the most recent file. This requires document governance that pre-exists the retrieval system.

**Professional indemnity.** In Legal and Finance, an agent producing an output based on stale or incorrect content may expose the organisation to liability. Freshness SLAs in these domains are not operational conveniences — they are risk management requirements.

| Domain | Critical schema element | Freshness SLA example | Key governance risk |
|---|---|---|---|
| Software Engineering | Codebase context, test results | Within current sprint | Missing recent changes |
| Finance | Chart of accounts, regulatory rates, policy documents | Daily for rates; quarterly for policy | Stale regulatory content |
| Legal | Case law, contract precedents, regulatory text | Within publication cycle | Jurisdiction mismatch |
| HR | Policy documents, organisational structure, employment law | Quarterly; at legislative update | Outdated policy version |
| Procurement | Approved vendor list, pricing schedules, contract terms | Monthly; at contract renewal | Pricing drift |

---

## Failure Modes at Stage 2

**Context flooding.** Injecting everything available rather than what the schema requires. Result: high token costs, diluted relevance, inconsistent output quality. Fix: enforce context budgets; every schema element must justify its presence.

**Retrieval system substituting for knowledge governance.** The retrieval system is built, but the knowledge base is not maintained. The technical solution cannot compensate for content that is outdated, poorly structured, or incomplete. Fix: knowledge governance — ownership, SLAs, freshness monitoring — as a prerequisite to retrieval system deployment.

**Single-source dependency.** The context pipeline relies on one source. When it fails or degrades, context quality collapses with no fallback. Fix: source diversity and quality monitoring that triggers alerts when a source goes dark.

**No quality baseline.** The system goes live without establishing retrieval quality baselines. Quality degradation over time is invisible — there is nothing to compare current performance against. Fix: measure retrieval quality before deployment and track it continuously.

**Schema absent.** Retrieval is implemented without a documented context schema. The system retrieves *something*, but there is no specification for what it should retrieve. Improvements are made by intuition rather than by closing gaps against a requirement. Fix: write the schema before building the system.

---

## Stage 2 Readiness Assessment

Before transitioning to Stage 3, the following should be true:

| Indicator | What it demonstrates |
|---|---|
| Context schemas are documented and versioned | Information requirements are explicit, not implicit |
| Retrieval quality is measured with a defined baseline | Quality degradation will be detected, not discovered through complaints |
| A freshness process exists with defined SLAs and ownership | Context rot is governed, not managed reactively |
| Context budgets are defined per workflow step | Context window is an architectural constraint, not an afterthought |
| At least one context quality anomaly has been detected and resolved | The detection system is proven operational |
| The team can articulate what strategic priorities govern agent decisions in ambiguous cases | The organisation is ready to encode intent at Stage 3 |

The last indicator is a Stage 3 precondition, not a Stage 2 completion criterion. But organisations that cannot articulate their strategic priorities at Stage 2 completion will struggle to encode them in an intent manifest. The awareness of the gap is the preparation for closing it.

---

*Continue to: [Stage 3 Deep Dive — Intent Engineering](./stage-3-intent-engineering.md)*  
*Back to: [Stage 1 Deep Dive — Prompt Engineering](./stage-1-prompt-engineering.md) · [Stage Transition Playbooks](./stage-transition-playbooks.md)*
