# Stage 1 Deep Dive — Prompt Engineering

*E2-01 · Wave 5 — Stages · Audience: All*

> See also: [Stage Transition Playbooks](./stage-transition-playbooks.md) · [Maturity Curve Overview](../00-foundations/maturity-curve.md) · [Cumulative Stack](../00-foundations/cumulative-stack.md)

---

## Overview

Stage 1 is where every organisation starts. It is also the stage most frequently underestimated — treated as a temporary phase to pass through quickly on the way to more sophisticated automation, rather than as a foundational practice that determines the quality of everything above it.

The core activity at Stage 1 is prompt engineering: the craft of eliciting high-quality, reliable outputs from a language model through the design of inputs. This sounds simple. In practice it requires precision, systematic thinking, and organisational habits that most teams do not build until they are forced to by the failures that poorly-engineered prompts produce at scale.

Stage 1 has a ceiling. A single expert with a well-tuned prompt library can achieve impressive results. That expertise cannot be transferred, audited, or maintained without the person who holds it. Stage 1 organisations are highly person-dependent. The transition to Stage 2 — and every stage beyond — begins by making the implicit explicit.

---

## What Stage 1 Looks Like

### The human role

At Stage 1, the human is the entire system. They write prompts, evaluate outputs, edit results, and assemble the final product. The model is a tool the human wields, not an agent the human governs. Every decision about quality, scope, and approach rests with the individual.

**What the human does:**
- Writes and iterates prompts to elicit useful model outputs
- Manually evaluates, edits, and curates model-generated content
- Assembles code, documents, and decisions from raw model outputs
- Holds all task context in their head — nothing is externalised
- Builds personal techniques that are not documented or shared

**The risk:** All knowledge and capability is person-dependent. Non-transferable, non-auditable, non-repeatable.

### The agent role

There is no persistent agent at Stage 1. The model is stateless between interactions. It has no memory, no tools, and no continuity across sessions. Every interaction begins from scratch.

---

## The Craft of Prompt Engineering

Prompt engineering is a genuine discipline. The difference between a well-engineered prompt and a carelessly written one is the difference between a reliable, high-quality output and an inconsistent, expensive, difficult-to-audit one.

### The structure of an effective prompt

Effective prompts have a consistent anatomy. Each element serves a function:

| Element | Purpose | What its absence produces |
|---|---|---|
| Role assignment | Establishes the model's operating persona and expertise domain | Generic outputs; model hedges; no specialised vocabulary |
| Explicit scope | States what the task covers AND what it does not | Outputs that drift into adjacent territory; boundary violations |
| Context | Provides the information the model needs that it cannot infer | Outputs based on assumptions; hallucinated specifics |
| Format specification | Defines the expected output structure | Inconsistent formats; outputs that require manual reformatting |
| Constraints | States what the output must not include or do | Outputs with excluded content; constraint violations |
| Examples | Shows the model what good looks like | Outputs that are technically correct but stylistically wrong |
| Evaluation criteria | Tells the model how to assess its own output | No self-correction; lower quality outputs |

Not every prompt requires all elements. The test is: what would the model have to assume to fill in the missing element, and is that assumption reliable?

### Prompt patterns for software engineering

At Stage 1, software engineering teams commonly use prompts for: code generation, test writing, documentation, code review, architecture advice, and debugging assistance.

**Code generation prompts** must specify: the language and version, the framework and version, the function signature or interface contract, what the function must NOT do (edge cases, error handling scope), and the output format (code only, code with comments, code with tests).

**Review prompts** must specify: what kind of review (correctness, security, performance, style), what standards apply, what to report (issues only, or issues and suggestions), the severity classification expected, and what context the reviewer should assume about the codebase.

**Test prompts** must specify: the test framework, the test style (unit, integration, property-based), what to test (happy path, error cases, edge cases), what the function is supposed to do, and what should not be tested (out of scope).

### Prompt patterns for knowledge work

In non-engineering domains, Stage 1 prompt engineering applies equally. The same principles hold; the vocabulary changes.

**Finance:** Prompts for financial analysis must specify the accounting standard in effect, the jurisdiction, the time period, what material thresholds apply, what to exclude from scope, and what format the output should take (narrative, table, calculated figures).

**Legal:** Prompts for legal review must specify the governing law, the contract type and context, which party's interests are being considered, what issues to flag versus what to approve, and whether the output should be advisory language or a markup of the source document.

**HR:** Prompts for policy application must specify the jurisdiction, the relevant policy version, the specific scenario being assessed, and what the output should be (a determination, a recommendation, a risk flag, or a set of options with implications).

The common requirement across all domains: the model must not have to assume what standard, jurisdiction, or context applies. State it explicitly.

---

## The Specification Discipline at Stage 1

Stage 1 is where the specification discipline — or the absence of it — is established. This matters enormously for what becomes possible at Stage 4 and beyond.

A prompt is a specification. It describes what the model should do. The discipline of writing it precisely — with explicit scope, explicit constraints, explicit criteria — is the same discipline that, applied at scale to agent governance, produces a specification corpus that the Dark Factory can enforce.

> **The Specification Debt Principle**  
> Ambiguity authored at Stage 1 does not disappear at Stage 4 — it becomes policy. Every poorly-authored prompt or requirement is a specification defect that compounds as it travels up the stack.

The concrete habit that Stage 1 demands is the use of RFC 2119 semantics in acceptance criteria and prompt constraints. When a prompt says "the output MUST include a summary section," that MUST is normative — it is a testable requirement. When it says "the output should be concise," that is aspirational — it cannot be tested or enforced.

The investment in precision at Stage 1 is negligible. The cost of retrofitting it at Stage 4 is significant.

---

## Organisational Patterns at Stage 1

### The prompt library

The single most important Stage 1 artefact is the prompt library — a shared, versioned collection of prompt patterns that works for the team's specific domain and workflows. Without it:

- Knowledge accumulates with individuals
- Different team members produce inconsistent outputs for the same task
- When a person leaves, their prompt craft leaves with them
- There is no baseline to improve from

A minimal prompt library requires: a naming convention for prompt types, a version field, a description of what the prompt is for, the prompt text itself, and at least one example of a good output it produces.

### Review and governance

At Stage 1, prompts used in consequential workflows require review before use in production. "Consequential" means: code deployed to production, documents sent to customers, decisions affecting individuals. The review does not need to be elaborate — a second person assessing whether the prompt does what it claims and does not do what it should not — but it must exist.

Organisations that skip prompt review at Stage 1 discover at Stage 3 or Stage 4 that their intent manifests and specification corpora are built on untested, idiosyncratic prompt foundations. The refactoring cost is high.

### Version control

Prompts change. The model that produces good outputs from a prompt today may produce different outputs from the same prompt after a model update. Without version control, the cause of output quality shifts is opaque. With version control, changes are traceable and regressions are diagnosable.

---

## Failure Modes at Stage 1

**Prompt sprawl.** Every individual has their own prompt techniques, none documented, none shared. The team uses AI but cannot characterise what it is doing or replicate what works. Outcome: inconsistent outputs across the team, no organisational learning. Fix: mandatory prompt library contribution for any prompt used more than once in production.

**Context inflation.** The prompt includes everything that might be relevant "just in case" — the entire codebase, all documentation, all prior decisions. The model's output quality does not improve; context window costs increase; the prompt is unrepeatable without the same sprawling context assembly. Fix: context schemas that define precisely what is needed at each step (Stage 2's contribution, but the discipline starts here).

**Over-reliance on iteration.** The prompt is not specified carefully; the human iterates interactively until they get a good output. The output is good but the process is not repeatable — someone else asking the same question gets a different output because they do not know the iteration path. Fix: document the final prompt that produces the good output, not just the output.

**No constraints.** The prompt specifies what to do but not what not to do. The model includes content that was not wanted, makes assumptions that were not authorised, or produces outputs with no defined scope limit. Fix: every prompt includes an explicit "must not include" or "out of scope" element.

---

## Stage 1 in Enterprise Knowledge Work

The Stage 1 pattern looks similar across all knowledge work domains, with one important difference: the stakes of poor prompt engineering are often higher in non-engineering contexts.

A poorly-prompted code review produces suboptimal code. A poorly-prompted contract review may miss a liability. A poorly-prompted HR policy application may produce an unlawful determination. A poorly-prompted financial analysis may produce materially incorrect figures.

This means the specification discipline requirement — explicit scope, explicit constraints, explicit criteria — is *more* important in knowledge work domains, not less. And the review requirement for prompts used in consequential workflows applies equally, with domain-appropriate reviewers.

The prompt library in a legal team looks different from one in an engineering team, but the governance requirements are the same: shared, versioned, reviewed, owned.

---

## Stage 1 Readiness Assessment

Before transitioning to Stage 2, the following should be true:

| Indicator | What it demonstrates |
|---|---|
| A prompt library exists as a shared team asset | Knowledge is externalised and transferable |
| Prompts are versioned | Changes are traceable; regressions are diagnosable |
| A review process exists for production prompts | Quality governance is operational |
| Prompts include explicit scope boundaries | The discipline of precision is established |
| At least one person can improve prompts others wrote | The craft is transferable, not personal |
| The team can identify which prompts produce inconsistent outputs | Self-awareness of quality gaps exists |

---

*Continue to: [Stage 2 Deep Dive — Context Engineering](./stage-2-context-engineering.md)*  
*Back to: [Stage Transition Playbooks](./stage-transition-playbooks.md) · [Glossary](../00-foundations/glossary.md)*
