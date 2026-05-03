# Anti-Patterns Library

*E6-03 · Wave 6 — Examples · Audience: All*

> See also: [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md) · [Cumulative Stack](../00-foundations/cumulative-stack.md) · [Specification Discipline](../00-foundations/specification-discipline.md)

---

## Overview

An anti-pattern is a response to a recurring problem that appears reasonable and is commonly applied, but produces worse outcomes than doing nothing. Anti-patterns are particularly dangerous because they are not obviously wrong — they are often the natural, intuitive response to a real challenge.

This library documents the most common anti-patterns in AI operational maturity. They are organised by the stage at which they most frequently occur and by the failure mode they produce. Each entry includes the surface signal, the underlying cause, the failure mode it produces, and the resolution.

---

## Stage 1 Anti-Patterns

### AP-01 — The Personal Prompt Vault

**What it looks like:** Each team member has their own prompt library — notes files, browser bookmarks, personal Notion pages. Prompts that work well are not shared. New team members start from scratch. When someone leaves, their prompt craft leaves with them.

**Why it happens:** Sharing prompts takes effort. There is no forcing function. The benefit (team consistency) is diffuse; the cost (documentation effort) is immediate and personal.

**Failure mode:** The team's AI-assisted productivity is the sum of individual capabilities, not a team capability. It does not compound. It does not survive team turnover. It cannot be audited or improved systematically.

**Resolution:** A shared, version-controlled prompt library as a team norm — contribution required, not optional, for any prompt used more than once in a consequential workflow. The library is the team's asset, not individuals'.

---

### AP-02 — The Everything Prompt

**What it looks like:** Prompts are written with maximum context "just in case" — the entire codebase, all documentation, all relevant history, all possible edge cases. The prompt is hundreds of lines. The model outputs something reasonable. The prompter does not know which context elements contributed and which were noise.

**Why it happens:** Uncertainty about what the model needs, combined with the availability of large context windows. Including more feels safer than including less.

**Failure mode:** Unrepeatable results (context assembly is manual and varies); high token costs with no quality improvement; inability to diagnose quality problems because the causal chain from input to output is opaque.

**Resolution:** Context schemas — define precisely what is needed at each workflow step. Start with the minimum and add only what demonstrably improves output quality. The schema documents the decision.

---

### AP-03 — The One Good Output

**What it looks like:** An engineer iterates with a model until they get a very good output. They use that output. The process that produced it — the iteration path, the prompts, the intermediate refinements — is not recorded. Next time someone needs a similar output, they start over.

**Why it happens:** The goal was the output. Documentation of the process feels like overhead after the goal is achieved.

**Failure mode:** Non-repeatable quality. The expertise required to reproduce the result is locked in the original engineer's head and the specific interaction context. Systematic improvement is impossible because there is no baseline to improve from.

**Resolution:** Record the final prompt that produced the good output, not just the output. The prompt is the repeatable artefact; the output is ephemeral.

---

## Stage 2 Anti-Patterns

### AP-04 — The Retrieval System Without a Schema

**What it looks like:** A RAG pipeline is built. Documents are embedded. The system retrieves "relevant" content in response to queries. There is no documented specification of what "relevant" means for each workflow step, what content should and should not be retrieved, or what quality threshold is acceptable.

**Why it happens:** Retrieval system deployment is treated as a technical problem. The schema — the information architecture requirement — is treated as something that emerges from the system's behaviour rather than something that precedes it.

**Failure mode:** The system retrieves something, but there is no criterion for whether it retrieves the right things. Quality improvements are made by intuition (changing chunk sizes, embedding models, similarity thresholds) rather than by closing gaps against a defined requirement. Improvements are not demonstrably improvements.

**Resolution:** Write the context schema before building the retrieval system. Define what is required at each workflow step, what is excluded, what freshness threshold applies. Build and measure against the schema.

---

### AP-05 — The Stale Knowledge Base

**What it looks like:** The knowledge base was populated with care at implementation. Six months later, it is a mix of current and outdated content, with no indication of which is which. Agents retrieve confidently from both.

**Why it happens:** Knowledge base population is treated as a one-time project. Ongoing maintenance is not owned by anyone. No one is accountable for currency.

**Failure mode:** Context rot. Agents produce outputs that are correct for a world that no longer exists. The failure is invisible until it produces a wrong output — by which point the stale content has been active for months.

**Resolution:** Freshness SLAs with named owners for every content source. Automated freshness monitoring. A knowledge base that has no maintenance process is a knowledge base that will degrade.

---

### AP-06 — The Stage 2 Organisation Pretending to Be Stage 3

**What it looks like:** The team has context pipelines and produces high-quality outputs. The organisation announces it has "AI-native operations." The intent manifest has not been written. Agents make decisions based on task instructions, not on encoded intent.

**Why it happens:** Stage 2 produces impressive results that are visible to stakeholders. Stage 3 requires a governance investment (intent authorship) that is less visible. The temptation is to claim Stage 3 maturity without making the investment.

**Failure mode:** Agent consistency is an illusion. Different agents completing similar tasks with different task instructions make different choices between competing considerations. The organisation cannot defend those choices as principled decisions — because they were not. When challenged (by a customer, a regulator, an auditor), there is no governance basis for the outcome.

**Resolution:** Honest maturity assessment. The lowest solid layer rule: the organisation is the stage where its practices are genuinely established, not where its technology operates. Context pipelines without intent governance is Stage 2.

---

## Stage 3 Anti-Patterns

### AP-07 — The Aspirational Intent Manifest

**What it looks like:** The intent manifest contains clauses like "act in the best interests of customers," "apply good judgement in ambiguous situations," and "prioritise compliance with all applicable regulations." It is thorough, well-written, and completely unenforced.

**Why it happens:** Intent authorship is hard. Writing testable, actionable intent clauses requires domain authority and precision. Writing aspirational prose is easier and produces a document that looks complete.

**Failure mode:** Agents cannot apply aspirational instructions to specific decisions. They infer what "best interests of customers" means from their training, inconsistently. The manifest provides no governance benefit — it is a document that exists, not a governance mechanism that functions.

**Resolution:** Test every intent clause against five real scenarios before publishing. If the clause does not produce a clear, determinable answer for each scenario, it is aspirational rather than actionable. Rewrite until it produces determinate answers.

---

### AP-08 — The Engineering-Owned Intent Manifest

**What it looks like:** The intent manifest is written, maintained, and understood by the engineering team. Business strategy changes but the manifest is not updated because the people responsible for strategy do not know the manifest exists.

**Why it happens:** Intent manifests emerge from engineering workflows. Engineers are the first to need them and the first to build them. The organisational governance connection — between business strategy and manifest content — is established later, if at all.

**Failure mode:** Intent drift. Agents apply the previous strategy because that is what the manifest encodes. Outputs feel wrong without being technically incorrect. The mismatch between actual intent and encoded intent grows until it produces a consequential error.

**Resolution:** Dual ownership from the outset. The manifest format and infrastructure are engineering responsibilities. The manifest content is a business responsibility. The governance connection must be established before v1.0, not after the first drift event.

---

## Stage 4 Anti-Patterns

### AP-09 — The Prose Specification Corpus

**What it looks like:** The specification corpus is a collection of well-written policy documents. Agents reference them. The documents are reviewed and approved. But they are natural language prose — not machine-readable, not structured, not automatically testable.

**Why it happens:** Writing prose policy documents feels like the right form for governance content. Policy documents are familiar. Machine-readable formats feel like engineering artefacts, not governance ones.

**Failure mode:** The corpus cannot be automatically enforced. Agents interpret the prose and apply it variably. Conflicts between entries cannot be detected automatically. Test cases cannot be co-located. The audit trail records that agents referenced the corpus but cannot verify that they applied it correctly.

**Resolution:** Machine-readable format — OPA/Rego, structured YAML with defined schema, OSCAL — as the canonical representation. The prose version can exist as a human-readable companion, but it is not the enforcement mechanism.

---

### AP-10 — Stage 4 Without a Harness

**What it looks like:** Autonomous operation begins. Agents are acting without human review. There is no harness — or there is a harness that monitors infrastructure metrics (latency, error rates) but not behavioural metrics (decision distribution, escalation patterns, confidence shifts).

**Why it happens:** The harness is often perceived as an engineering nice-to-have rather than a governance necessity. The focus during transition is on corpus completeness and escalation readiness. Harness deployment is deferred.

**Failure mode:** Silent failure. Agents behave anomalously — escalation rate drifts, decision confidence shifts, output quality degrades — with no detection mechanism. The problem is discovered through downstream consequences rather than through monitoring. By the time it is discovered, the anomalous behaviour has been running for weeks.

**Resolution:** Harness as a Stage 4 precondition, not a Stage 5 goal. A minimal harness — behavioural telemetry, anomaly alerts, audit log review — must exist before autonomous operation begins.

---

### AP-11 — The Escalation That Is Never Closed

**What it looks like:** Escalation packages arrive. The receiving human makes a decision. The decision is communicated back to the agent. But the escalation is not converted into a corpus extension. The same gap produces the same escalation next week, and the week after.

**Why it happens:** Corpus extension requires time and governance effort. The escalation response is urgent; the corpus extension is not. It is deferred, then forgotten.

**Failure mode:** The escalation rate does not decline. The corpus does not grow. The improvement loop is broken. The Dark Factory remains dependent on human exception-handling for a class of decisions that should have been incorporated into the corpus months ago.

**Resolution:** Every escalation package has a mandatory close-out step: was this escalation converted into a corpus extension? If no, why not? The governance process must track open escalations against corpus extensions as a ratio — a declining ratio indicates systemic failure of the improvement loop.

---

## Stage 5 Anti-Patterns

### AP-12 — Alert Fatigue

**What it looks like:** The harness is comprehensive. It monitors everything. It alerts on every anomaly, regardless of severity. The on-call engineer receives 40 alerts per day. They have learned to ignore most of them. A genuine anomaly is lost in the noise.

**Why it happens:** Alert configuration is typically conservative at first — better to over-alert than to under-alert. Alert triage — determining which alerts require human action — requires effort and discipline that is often not prioritised after initial deployment.

**Failure mode:** The harness exists but does not function as a safety mechanism. Genuine anomalies are missed. The organisation has false confidence that it is monitoring its system.

**Resolution:** Alert classification: only alerts requiring human action should reach humans. Everything else is handled autonomously (by self-healing playbook) or logged silently for periodic review. Regularly review alert-to-action ratio: what proportion of received alerts resulted in human action? If the ratio is below 30%, the alert configuration requires triage.

---

### AP-13 — The Baseline That Was Never Updated

**What it looks like:** Behavioural baselines were established when Stage 4 went live. Eighteen months later, the system has evolved — the corpus has grown, operational patterns have shifted, new agent capabilities have been added. The baselines reflect the system as it was at initial deployment.

**Why it happens:** Baseline update requires discipline and deliberate effort. There is no forcing function. The original baselines continue to work, mostly — they just produce increasing numbers of false positives as the system drifts from them.

**Failure mode:** Anomaly detection degrades. False positive rate increases. The team adjusts thresholds upward to reduce noise — which reduces sensitivity to genuine anomalies. Eventually, the harness is technically operational but no longer detecting anomalies reliably.

**Resolution:** Baseline review as a formal governance cadence — at minimum quarterly, and mandatorily on any significant corpus change. The baseline review process must be as formal as the corpus review process.

---

## Cross-Stage Anti-Patterns

### AP-14 — Stage Skipping

**What it looks like:** The organisation deploys a Stage 4 specification management platform, contracts with a harness engineering firm, and declares itself preparing for Stage 4 operations — while still operating with Stage 2 context engineering and no intent manifest.

**Why it happens:** Technology platforms are visible and purchasable. Practice development is slow and unglamorous. Leadership wants to demonstrate AI investment. Vendors sell platforms, not practices.

**Failure mode:** The platform amplifies existing weaknesses rather than compensating for them. Agents operating without adequate context and intent governance produce low-quality outputs that the specification corpus cannot compensate for. The platform is expensive; the results are poor; the conclusion is that the platform failed. The actual failure was the absent foundational practice.

**Resolution:** The Lowest Solid Layer Rule — investment in higher-stage technology must be calibrated to practice maturity at lower stages. The question is not "what platform should we deploy?" but "what practice must we develop, and what tools support that development?"

---

### AP-15 — The Maturity Theatre Assessment

**What it looks like:** The organisation conducts a maturity assessment and scores itself at Stage 4 across all dimensions. The assessment was conducted by the team that built the system, asking the team that uses the system. No external perspective. No artefact review. No observable evidence standard.

**Why it happens:** Maturity assessments are typically self-assessments. There is organisational pressure to demonstrate progress. Assessments that produce lower scores may reflect badly on the team that commissioned them. Aspirational scoring is natural under these conditions.

**Failure mode:** Investment and governance decisions are made on the basis of a maturity level the organisation has not actually achieved. Stage 4 governance assumptions are applied to a Stage 2 operation. When the system encounters the situations that Stage 4 governance was designed to handle, it is not actually Stage 4 — and the failures are attributed to the framework rather than to the assessment.

**Resolution:** The observable evidence standard. Score only what is demonstrably true — where an artefact, a metric, or a measurable outcome can be produced as evidence. "We intend to have X" is not Stage X. "We have X, and here is the evidence" is Stage X.

---

### AP-16 — The Technology Premium Fallacy

**What it looks like:** The organisation invests heavily in the most advanced AI infrastructure — the latest LLM APIs, a sophisticated vector database, a proprietary agent orchestration platform. It believes this investment will produce competitive advantage. Eighteen months later, competitor organisations have deployed equivalent or better technology at commodity prices.

**Why it happens:** Technology is visible, purchasable, and produces immediate results. Practice development is slow, tacit, and produces results that compound over years. The short-term return on technology investment appears to exceed the return on practice investment.

**Failure mode:** The organisation has infrastructure that anyone can now purchase at commodity cost, and practices that are no better than its competitors'. The investment produced no durable advantage.

**Resolution:** The Practice Premium Principle. Technology components in the AI stack commoditise on the standard evolution curve — available to all, differentiating to none. The durable competitive advantage lies in the organisational practice disciplines that make those components work. Invest in technology to support practice development. Invest in practice development to produce durable advantage.

---

*Continue to: [Dark Factory Operating Model](./dark-factory-operating-model.md)*  
*Back to: [Feature Delivery Worked Example](./feature-delivery-worked-example.md) · [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md)*
