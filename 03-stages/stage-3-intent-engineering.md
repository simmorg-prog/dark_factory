# Stage 3 Deep Dive — Intent Engineering

*E2-03 · Wave 5 — Stages · Audience: All*

> See also: [Stage Transition Playbooks](./stage-transition-playbooks.md) · [Stage 2 Deep Dive](./stage-2-context-engineering.md) · [Stage 4 Deep Dive](./stage-4-specification-engineering.md) · [Intent Manifest — Reference Design](../02-artefacts/intent-manifest.md)

---

## Overview

Stage 3 introduces a capability that Stages 1 and 2 do not possess: the ability for agents to ask not just "what should I do?" but "should I do it this way, given what the organisation values?"

Context engineering (Stage 2) equips agents with information. Intent engineering equips agents with direction — a principled understanding of what the organisation optimises for, what it will not compromise on, and how to resolve conflicts between competing legitimate objectives.

The enabling artefact is the intent manifest: a structured, versioned, machine-readable document that encodes organisational strategy, risk appetite, ethical constraints, and conflict resolution rules. Agents reference it at decision points where the task instruction alone does not determine the right action.

Stage 3 is where the human skill requirement changes most sharply. Earlier stages required technical skills — prompt craft, information architecture, retrieval system design. Stage 3 requires the ability to articulate organisational intent with enough precision that it can be encoded and applied consistently by agents. This is a governance and strategy skill, not an engineering one. It requires domain authority, not just technical competence.

---

## What Stage 3 Looks Like

### The human role

At Stage 3, the human is the intent author. The primary product of their expertise is no longer code or reviewed documents — it is the encoded statement of what the organisation is trying to achieve and how it wants to achieve it.

**What the human does:**
- Authors and maintains the intent manifest — defining priorities, constraints, and conflict resolution rules
- Governs the intent authoring process — who may write intent clauses, under what review, with what authority
- Detects and resolves intent drift — monitors whether agent decisions align with encoded intent
- Updates intent when strategy or policy changes — ensuring the manifest remains a current expression of organisational will
- Handles escalations where intent is insufficient to resolve the situation — and learns from those escalations to extend the manifest

**What transfers to agents:**
- Conflict resolution between competing valid objectives — agents apply manifest rules rather than escalating every ambiguous case
- Strategic consistency across independently-operating agents — all agents working from the same intent source

**What stays with humans:**
- Intent authorship — the manifest must express human strategic will; agents cannot define their own intent
- Novel situation resolution — escalations that the manifest does not cover require human judgment and become the source of manifest extensions

### The agent role

At Stage 3, agents are intent-aware workers. They continue to use the context infrastructure of Stage 2. They now additionally reference the intent manifest at decision points where multiple valid approaches exist or where a task instruction conflicts with an organisational constraint.

The significance of this cannot be overstated. Without encoded intent, multiple agents completing the same task may make different choices between competing considerations — and both choices may be defensible. With encoded intent, the choice is principled and consistent. An audit of agent decisions at Stage 3 should be able to trace each decision to the intent clause that governed it.

---

## The Intent Manifest

### What it is

The intent manifest is not a prompt. It is a policy document — a structured statement of what the organisation values, in what priority order, and what it will not compromise on regardless of context.

It has three functions:

**Direction.** It tells agents what to optimise for when instructions are silent on priority. If speed and thoroughness conflict, which wins? If customer satisfaction and regulatory compliance conflict, which wins? The manifest makes these choices explicit rather than leaving them to agent inference.

**Adjudication.** It provides rules for resolving conflicts between legitimate objectives. A conflict resolution rule in the manifest produces the same outcome every time; an agent resolving the conflict by inference produces a different outcome depending on its current context, temperature, and the specific framing of the task.

**Governance.** It creates an auditable record of what the organisation encoded as its intent. When an agent decision is challenged, the manifest is the reference point. "This is what we told agents to prioritise" is a defensible position; "agents made the best choice available" is not.

### What it contains

A well-structured intent manifest contains:

| Section | Content |
|---|---|
| Document header | Manifest ID, version, owner, effective date, superseded version |
| Strategic priorities | Ranked list of what the organisation optimises for |
| Hard constraints | Non-negotiable boundaries — what agents must never do regardless of instruction |
| Conflict resolution rules | Explicit rules for each identified class of conflict between priorities |
| Domain-specific guidance | Intent clauses specific to particular workflow domains |
| Escalation triggers | Conditions that must trigger escalation regardless of whether the manifest provides guidance |
| Governance | Who may amend the manifest, review cadence, change process |

### The quality bar for intent clauses

An intent clause that agents cannot apply consistently is not useful. The most common cause of an unusable intent clause is ambiguity — the clause expresses an aspiration rather than a decision rule.

| Problematic | Effective |
|---|---|
| "Act ethically" | "When regulatory compliance and commercial efficiency conflict, compliance takes precedence in all cases" |
| "Prioritise customer value" | "When the lower-cost option provides the stated functional outcome, recommend the lower-cost option unless the customer has explicitly specified a quality preference" |
| "Be cautious with sensitive data" | "Any action that involves processing personal health data MUST be escalated to the Data Ethics function before execution" |
| "Use good judgement" | "When task instructions conflict with this manifest, manifest takes precedence. When two manifest clauses conflict, the clause with the higher priority rank takes precedence" |

The test for an intent clause: can an agent apply it to a specific decision scenario without requesting clarification? If yes, it is actionable. If no, it requires rewriting.

### RFC 2119 semantics in intent manifests

Intent manifests benefit from RFC 2119 obligation keywords for the same reason that specifications do: they remove ambiguity about whether a guideline is mandatory or advisory.

A MUST in an intent manifest creates an absolute obligation. A SHOULD creates a strong default with exceptions possible. A MAY creates a permitted option. These distinctions matter at Stage 3 and are load-bearing at Stage 4, where the specification corpus derived from the manifest is machine-enforced.

Begin using RFC 2119 semantics in intent manifests at Stage 3, even before Stage 4 enforcement is in place. The habit of precision is what produces a manifest that can be translated directly into machine-enforceable specifications.

---

## Intent Authorship as an Organisational Capability

The most underestimated requirement of Stage 3 is the human skill it demands. Intent authorship — writing clear, testable, conflict-free statements of organisational priority — is not a common skill. Most organisations have never needed it in this form.

The skills required:

**Domain authority.** The intent author must understand the domain well enough to know which conflicts matter and what the organisation's genuine priorities are. They cannot be guessing at strategic preferences; they must know them.

**Precision in natural language.** The ability to write a sentence that means exactly one thing — no more, no less — and to detect when a sentence admits multiple interpretations. Legal drafting training is directly applicable here. Technical writing is partially applicable. General writing is not sufficient.

**Systems thinking.** The ability to anticipate second-order effects: if this is the rule, what scenarios does it govern correctly, and what scenarios does it produce bad outcomes for? Intent clauses must be stress-tested against edge cases before they are published.

**Political authority.** Some intent conflicts are political — they represent genuine disagreements about organisational priorities between different stakeholders. Resolving these in the manifest requires authority to make the call, or a process for reaching consensus. Technical staff cannot write intent clauses that resolve political conflicts; the authority must come from the level that owns the conflict.

Where intent authorship capability does not exist, it must be developed. This is a practice development investment, not a tooling investment. A platform for managing intent manifests does not create the ability to write good intent clauses.

---

## Intent Drift

Intent drift occurs when agent decisions diverge from the intent manifest — either because the manifest was not updated when strategy changed, or because agents are not consistently applying it, or because the manifest contains gaps that agents fill with their own inference.

Intent drift is insidious because it is often invisible. Agents produce outputs that are technically correct but strategically wrong. A human reviewing individual outputs may see nothing alarming; the pattern only emerges in aggregate.

Detecting intent drift requires:

**Decision logging with intent references.** Every agent decision at a manifest-governed decision point must be logged with the manifest clause it applied. Without this, drift cannot be detected — there is no record of what intent the agent was applying.

**Pattern analysis.** Periodic review of decision logs to identify clusters of decisions that suggest agents are interpreting intent clauses in ways that were not intended, or that suggest the manifest has gaps.

**Escalation analysis.** A rising escalation rate in a particular decision class is often a signal that the intent manifest is insufficient for that class. Analysing escalation patterns surfaces manifest gaps before drift becomes systemic.

**Strategy alignment review.** When organisational strategy changes, the manifest must be reviewed and updated within a defined SLA. Failure to do this is the most common source of intent drift — agents are applying the previous strategy because that is what the manifest encodes.

---

## Stage 3 in Enterprise Knowledge Work

Intent engineering has significant implications in non-engineering knowledge work domains where agent decisions can have legal, financial, or reputational consequences.

### Finance

A financial services firm's intent manifest must encode: regulatory compliance priorities (which regulations take precedence in conflict), materiality thresholds (what size of variance requires escalation), audit requirements (what must be logged regardless of outcome), and customer relationship priorities (how to balance commercial efficiency with customer service standards).

The manifest must be updated when regulatory requirements change — and the change must be reflected in agent behaviour within the regulatory effective date. This is not an optional governance cadence; it is a legal compliance requirement.

### Legal

Legal intent manifests encode: which party's interests are represented (critical — the same task instruction produces different outputs for different parties), the jurisdiction hierarchy (which law governs when laws conflict), acceptable risk levels by clause type (what level of contract risk requires escalation to counsel), and confidentiality requirements (what information may not be included in agent outputs).

### HR

HR intent manifests must be particularly precise about protected characteristics — any intent clause that could be applied differently to individuals on the basis of a protected characteristic must be reviewed for indirect discrimination. The manifest must explicitly prohibit instructions that would produce discriminatory outcomes even when the task instruction does not mention protected characteristics.

### The governance imperative

In all non-engineering domains, the intent manifest is a compliance and governance document, not just an operational one. It may need to be reviewed by legal, compliance, or data protection functions before deployment. Changes to it may require the same review. This is appropriate — in domains where agent decisions can produce material harm, the intent manifest is a risk management instrument.

---

## Failure Modes at Stage 3

**Governance theatre.** The manifest is written but agents do not consistently reference it. Outputs are generated without applying intent governance. No one audits compliance. Fix: close the loop — every governed decision must reference the manifest clause applied; auditors must verify this.

**Abstract intent.** Clauses express aspirations rather than decision rules. Agents cannot apply them consistently because they do not produce determinate guidance in specific scenarios. Fix: test every clause against five real scenarios before publishing it; if the clause does not produce a clear answer, rewrite it.

**Engineer ownership without business authority.** The manifest is written by the engineering team without input from the business functions that own the strategic priorities. The result is a manifest that reflects technical understanding of what the business values rather than the business's actual values. Fix: intent authorship must involve domain authority holders — the people accountable for the outcomes the manifest governs.

**Manifest as static document.** The manifest is published, referenced in system documentation, and never updated. Strategy changes but the manifest does not. Agents apply obsolete intent. Fix: a defined review cadence and a mandatory update process triggered by strategy or policy changes.

---

## Stage 3 Readiness Assessment

Before transitioning to Stage 4, the following should be true:

| Indicator | What it demonstrates |
|---|---|
| Intent manifest v1.0 is published and actively used | Intent governance is operational, not theoretical |
| At least one agent decision is traceable to a specific manifest clause | The intent loop is closed |
| Intent drift detection is operational | Divergence from manifest will be detected |
| The manifest has been updated following a strategy or policy change | The maintenance process works under real conditions |
| The Dark Factory preconditions have been assessed and gaps identified | The organisation understands what remains before Stage 4 is safe |
| Specification coverage planning has begun | The primary Stage 4 artefact development is underway |

The last two indicators are Stage 4 preconditions, not Stage 3 completion criteria. The assessment and the planning must begin during Stage 3, before the transition is attempted.

---

*Continue to: [Stage 4 Deep Dive — Specification Engineering](./stage-4-specification-engineering.md)*  
*Back to: [Stage 2 Deep Dive — Context Engineering](./stage-2-context-engineering.md) · [Intent Manifest — Reference Design](../02-artefacts/intent-manifest.md)*
