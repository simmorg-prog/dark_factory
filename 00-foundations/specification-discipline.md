> **E1-06 · Foundations · Wave 1**  
> The four principles of specification discipline — rigour from the outset, living specifications, universal applicability, and normative language precision.  
> See also: [Cumulative Stack Explained](./cumulative-stack.md) · [Glossary of Terms](./glossary.md) · [Maturity Curve Overview](./maturity-curve.md) · [LANGUAGE.md — Structural Vocabulary](./LANGUAGE.md)

---

# The Specification Discipline — Three Principles

## The Objection Worth Taking Seriously

State it plainly: *"specification rigour means waterfall."*

This objection is understandable. It is historically grounded. It is widely held. And it is wrong.

The organisations that will successfully become AI-native are those that can hold two things at once: agility in how work is planned and executed, and precision in how requirements and policies are expressed. The failure to hold both simultaneously is what produces specification debt — the compounding liability that makes AI systems brittle, unpredictable, and expensive to govern.

Understanding where this objection comes from is the first step to dismantling it.

---

## Where the Misconception Comes From

The waterfall failure mode was real. Large software projects of the 1970s through 2000s produced thousands of pages of requirements documentation that was obsolete before the first line of code was written. The documents were comprehensive. They were also wrong, because the world changed while they were being written.

The Agile Manifesto's response — *"working software over comprehensive documentation"* — was the right reaction to the right problem. But over time it became misread. "Comprehensive documentation" became "documentation." The useful correction became a blanket avoidance of specification precision.

The problem this created was invisible for a long time. Humans are remarkably good at filling in specification gaps. When a developer reads an ambiguous requirement, they apply context, domain knowledge, and charitable interpretation to produce a reasonable implementation. The specification could say "the system should handle errors gracefully" and a skilled developer would produce something sensible.

Agents cannot do this the same way. An agent executes the specification it is given with fidelity. The gap-filling that human practitioners performed invisibly is now a missing input. Every ambiguity the human workforce absorbed becomes a specification defect when the workforce is an agent.

---

## Principle 1 — Rigour from the Outset, Not Rigour All at Once

> **Principle 1: Rigour from the outset, not rigour all at once.**  
> Precision at Stage 1 costs almost nothing. Retrofitting it at Stage 4 is enormously expensive. The discipline is not about writing complete specifications upfront. It is about writing precise specifications at every point where specifications are written, regardless of their scope or completeness.

The compounding argument: a specification defect authored at Stage 1 does not stay at Stage 1. It travels upward through every stage. At Stage 2, an ambiguous requirement becomes a poorly-scoped retrieval query. At Stage 3, it becomes an under-specified intent boundary. At Stage 4, it becomes law that agents enforce at production speed. The cost of the original defect multiplies at every transition.

The evidence that precision and brevity coexist is thirty years old. RFC 2119 — the internet engineering standard for requirement keywords — demonstrates that a single word carries semantic precision equivalent to a page of explanatory prose. A MUST in a user story acceptance criterion carries exactly the same precision as a MUST in a 500-page internet standard. The precision is not a function of the document's length or formality. It is a function of the writer's intent and vocabulary.

[The Specification Discipline Spectrum](../diagrams/specification-discipline-spectrum.svg)

The spectrum above shows the false dichotomy that drives the misconception. Static specifications and living specifications are not distinguished by whether they are rigorous. They are distinguished by when they are written and how they are maintained. Both require precision. One freezes it; the other evolves it.

---

## Principle 2 — Living Specifications, Not Static Documents

> **Principle 2: Living specifications, not static documents.**  
> A living specification is not a specification that someone intends to keep updated. It is a specification that is validated automatically by continuous integration and updated iteratively as the system evolves. The mechanism is automation, not intention.

The Agile community has already built the evidence base for this principle. Behaviour-Driven Development (BDD) demonstrated that acceptance criteria written in structured natural language (Given-When-Then) can be parsed by a test framework and validated automatically on every commit. Specification by Example showed that concrete examples annotated with expected outcomes serve simultaneously as requirements, tests, and documentation. Spec-Driven Development generalised this: the specification is the artefact from which tests are generated, not an artefact that tests verify after the fact.

The four properties of a living specification:

1. **Co-located with the work it governs** — stored in the same repository, versioned with the same tooling, readable in the same review
2. **Validated by CI** — every commit triggers validation; a failing specification is a breaking change
3. **Updated iteratively** — specifications are refined as understanding develops, not frozen at sign-off
4. **Owned by the whole team** — engineers, product owners, and domain experts all contribute and maintain

The mechanism that makes a specification living is automation, not intent. A specification that someone intends to keep updated but is not validated by automated tests is a static specification with good intentions. Good intentions do not survive production.

---

## Principle 3 — Universal Applicability: Deterministic and Probabilistic Systems Alike

> **Principle 3: Universal applicability.**  
> Specification quality governs deterministic systems (rules engines, OPA, policy engines) and probabilistic systems (LLM agents, RAG pipelines) equally. The failure modes differ. The discipline is the same.

[Specification Universality — Three System Types](../diagrams/specification-universality.svg)

The diagram above makes the argument visually. Three columns. One shared header: *all three execute the specification they are given with fidelity.*

**Deterministic systems** — rules engines, OPA/Rego, business rules management systems, decision tables — execute a bad specification consistently. Every time. At scale. The failure is reproducible and auditable, which makes it diagnosable. But it also means the wrong outcome happens with 100% reliability until someone fixes the specification. There is no variance to alert you.

**Probabilistic systems** — LLM agents, RAG pipelines, agentic workflows — execute a bad specification variably. Sometimes the output is fine. Sometimes it is wrong. The variance makes the failure hard to detect — the system appears to work most of the time — and hard to diagnose, because the same input does not produce the same output. The defect is invisible until it matters.

**Hybrid systems** — which is what the enterprise AI stack actually is — combine both failure modes simultaneously. A specification corpus governs deterministic policy enforcement. An LLM agent governs probabilistic task execution. A bad specification produces both consistent wrong decisions and variable invisible failures, running in parallel, interacting with each other.

The governance implication: specification discipline is *more* critical in hybrid systems than in either pure type. The interaction between the two failure modes creates compounding risk that neither deterministic nor probabilistic governance alone can detect.

The Dark Factory contains both layers. Every specification the organisation fails to author with precision is a potential failure point in both layers simultaneously.

---

## Principle 4 — Normative Language Must Be Declared and Calibrated

> **Principle 4: Normative language must be declared and calibrated.**  
> A specification that uses MUST without the RFC 8174 boilerplate is expressing aspiration, not obligation. A SHOULD without a rationale clause is a weak MUST with the information removed. A keyword applied to an unnamed subject has no conformance meaning. The RFC 2119 Precision Principle is the minimum standard for any normative claim in this framework, at any maturity stage.

This principle names the mechanism by which Principles 1–3 are made operational. Precision at Stage 1 (Principle 1) requires a vocabulary for expressing obligation levels. Living specifications (Principle 2) require keywords that are stable enough to be tested automatically. Universal applicability (Principle 3) requires keywords that carry the same meaning for deterministic and probabilistic systems alike.

RFC 2119 and RFC 8174 provide that vocabulary. But vocabulary alone is not enough — the vocabulary must be invoked correctly. A document that uses MUST without the RFC 8174 boilerplate has not invoked the RFC 2119 vocabulary. It has used capital letters. There is no conformance obligation in capital letters alone.

The [RFC 2119 Precision Principle](./LANGUAGE.md) defines six rules that together constitute the minimum standard:

1. **Invocation** — the RFC 8174 boilerplate MUST appear verbatim before any normative content
2. **Named conformance roles** — every keyword MUST be bound to a named actor, not an abstract system or process
3. **Keyword strength calibration** — MUST, SHOULD, and MAY are not interchangeable; each makes a different claim about whether exceptions are permitted
4. **SHOULD rationale** — every SHOULD MUST be accompanied by a rationale clause stating either the exceptional circumstance or the harm being prevented
5. **Lowercase is non-normative** — lowercase must, should, may carry only ordinary English meaning and are never obligations
6. **Scope** — the six rules apply to normative documents; purely descriptive documents are excluded unless they introduce normative requirements

> 💡 **The minimum viable precision standard at Stage 1 is three things:** include the RFC 8174 boilerplate, bind every obligation keyword to a named actor, and accompany every SHOULD with a rationale clause. This costs minutes. Not having it at Stage 4 costs months.

See: [LANGUAGE.md — Normative Language: The RFC 2119 Precision Principle](./LANGUAGE.md) for the full six rules and keyword decision rubric.

---

## The Practical Implication — What to Do Tomorrow

The discipline is available. It does not require a methodology change, a governance restructure, or a new toolchain. It requires a decision to apply precision habitually.

What to do with the next requirement you write:

1. **Use RFC 2119 semantics** — choose MUST, SHOULD, MAY explicitly. Eliminate "should" used as a hedge when you mean MUST.
2. **Make acceptance criteria explicit and binary** — a criterion that cannot be evaluated as pass/fail is not a criterion. It is an aspiration.
3. **Name what is out of scope** — the boundary of a specification is as important as its content. An agent that does not know what it is not responsible for will invent an answer.
4. **Version your specifications** — a specification without a version is a specification without accountability. When an agent fails, you need to know which specification it was operating under.

The corpus grows from there. One precise requirement is the beginning of the discipline. The discipline, developed consistently from Stage 1, is what makes the Dark Factory governable.

---

*See also: [Cumulative Stack Explained](./cumulative-stack.md) · [Glossary of Terms](./glossary.md) · [Maturity Curve Overview](./maturity-curve.md) · [Vision Narrative](../05-strategy/vision-ai-native.md) · [LANGUAGE.md — RFC 2119 Precision Principle](./LANGUAGE.md)*  
*Back to: [README](../README.md)*
