# Stage 4 Deep Dive — Specification Engineering

*E2-04 · Wave 5 — Stages · Audience: All*

> See also: [Stage Transition Playbooks](./stage-transition-playbooks.md) · [Stage 3 Deep Dive](./stage-3-intent-engineering.md) · [Stage 5 Deep Dive](./stage-5-harness-engineering.md) · [Dark Factory Definition](../00-foundations/dark-factory.md) · [Specification Corpus](../02-artefacts/specification-corpus.md)

---

## Overview

Stage 4 is the Dark Factory threshold. It is where human oversight of individual agent decisions ends, and where the specification corpus — not human review — becomes the mechanism of governance.

This transition is the most consequential in the framework. Before Stage 4, humans are in the operational loop. At Stage 4 and beyond, agents own the workflow. Humans set requirements, maintain the specification corpus, respond to escalations, and govern the system's behaviour. They do not review individual outputs.

The enabling mechanism is the specification corpus: a machine-readable, versioned, conflict-checked body of rules that tells agents precisely how to behave in every anticipated situation within their operational scope. When the corpus covers a situation, agents act without escalation. When it does not, they escalate.

Stage 4 demands five specification practices as prerequisites for safe operation. These are not optional enhancements that improve quality. They are the minimum standard required to operate autonomous agents without creating systemic risk. Each is addressed in turn below.

---

## What Stage 4 Looks Like

### The human role

At Stage 4, the human has completed the transition from operational participant to governance actor. They are no longer in the loop for routine decisions. Their work is the governance work — the meta-work that makes autonomous operation possible and safe.

**What the human does:**
- Authors and maintains the specification corpus — the primary governance artefact of the Dark Factory
- Governs corpus changes — reviewing, approving, and deploying specification updates
- Responds to escalation packages — receiving structured packages from agents and making the decisions the corpus cannot make
- Monitors system behaviour at the portfolio level — escalation rates, output quality trends, corpus coverage metrics
- Extends the corpus from escalation patterns — closed escalations become specification improvements

**What agents own:**
- All routine workflow decisions covered by the specification corpus
- Escalation detection and packaging — agents identify when they have reached the specification boundary and prepare the escalation artefact
- Audit logging — every decision is logged with the corpus clause that governed it

**What stays with humans:**
- Novel situations — decisions the corpus does not cover
- Specification authorship — the corpus expresses human intent; agents cannot write their own governance rules
- Systemic interventions — when the corpus itself needs structural change, not just content update

### The agent role

At Stage 4, agents are autonomous workflow operators. They execute the full workflow — design, implementation, test, review, deployment in software engineering; end-to-end process execution in knowledge work — within the bounds of the specification corpus.

The key capability is self-regulation: an agent that encounters a situation outside the corpus does not hallucinate a plausible response. It recognises the gap, prepares an escalation package, and routes it to the appropriate human. The specification corpus determines the boundary; the agent's self-regulatory behaviour determines what happens at the boundary.

---

## The Five Specification Disciplines

### Discipline 1: RFC 8174 Normative Precision

RFC 8174 is not optional at Stage 4. It is what makes human audit of machine-enforced specifications possible.

At Stage 4, agents enforce the specification corpus at scale and at speed. A human reviewing a corpus update or an escalation cannot evaluate its quality by reading prose — they need to know precisely what the specification requires. RFC 8174 obligation keywords provide this: MUST creates an absolute requirement; SHOULD creates a strong default with defined exception conditions; MAY creates a permitted option.

The boilerplate declaration that makes these keywords normative must appear in every specification corpus document:

> The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all capitals, as shown here.

Without this declaration, the keywords carry only their ordinary English meaning. A corpus clause that says agents "must" do something — without the boilerplate — cannot be machine-enforced with confidence; it is a request, not a requirement.

At Stage 3, using RFC 8174 semantics in the intent manifest prepares the ground. At Stage 4, it is the standard. Every corpus entry must have a named conformance role, a single RFC 8174 keyword, and an explicit condition. Entries that use multiple keywords, ambiguous scope, or informal language are specification defects.

### Discipline 2: Atomicity

Atomicity (INCOSE singularity rules R18-R23) is not a style preference at Stage 4. It is what enables automated conflict detection and per-clause audit logging.

An atomic specification unit expresses exactly one obligation, directed at exactly one named actor, verifiable by exactly one test. It cannot be split without losing meaning and cannot be verified without depending on another unit's outcome.

The test is simple: can you write a single test that passes or fails this clause without testing anything else? If you cannot, the clause contains multiple obligations and must be split.

Why does this matter at Stage 4? Two reasons:

**Conflict detection.** Automated tools can only detect conflicts between rules if the rules are atomic. A rule that contains two obligations may conflict with another rule on one obligation but not the other — and automated detection cannot distinguish them. Conflict in a multi-obligation rule requires human analysis; conflict between atomic rules can be detected by an SMT solver.

**Audit logging.** When an agent makes a decision, the audit log must record which specific specification clause governed it. If clauses bundle multiple obligations, the audit trail is ambiguous — the agent complied with the clause, but which of its obligations governed this specific decision? Atomic clauses produce unambiguous audit records.

The practical implication: when reviewing a specification corpus entry for admission, conjunctions are red flags. A clause containing "and" or "or" connecting two obligations must be split into two atomic entries. The split takes a minute; the alternative is a clause that cannot be confidently audited or conflict-checked.

### Discipline 3: Embedded Testability

Embedded testability (BDD/Gherkin, OPA test co-location) is not a testing convenience at Stage 4. It is what closes the specification-to-enforcement gap and prevents specification drift.

Specification drift occurs when the corpus describes an intent that the enforcement mechanism does not implement. Over time, as corpus and enforcement code evolve independently, they diverge. The corpus says one thing; the agent does another. Audits pass because they check the corpus; behaviour fails because it checks the implementation.

The mechanism that prevents this is co-location: specification and test in the same artefact, automated validation in CI. In BDD contexts, a Gherkin scenario is both a specification clause and an executable test. In OPA/Rego contexts, a `_test.rego` file lives alongside the policy file and is run in every CI pipeline. The mechanism that confirms specification accuracy is automation, not trust.

Every corpus entry admitted to Stage 4 production must include:

- At least one positive test case: this input with this state MUST produce this outcome
- At least one negative test case: this input MUST NOT produce this outcome
- At least one edge case: the boundary condition that the clause exists to govern

Test cases co-located with corpus entries run in every deployment pipeline. Any corpus entry that fails its own tests is a broken specification — it is not what it says it is.

### Discipline 4: Proxy Discrimination Prevention

Proxy discrimination prevention is not a legal formality at Stage 4. It is what prevents the Dark Factory from systematically reproducing human discrimination at machine speed.

The Dark Factory operates at scale. A specification that permits discriminatory outcomes in individual human decisions produces the same discriminatory outcome in every agent decision, consistently and invisibly, at the rate the workflow executes. The scale is the difference. What was an occasional human failure becomes a systematic machine policy.

Proxy discrimination is particularly dangerous because it survives naive attempts to prevent it. Removing protected-characteristic fields from agent inputs does not prevent discrimination if substitute features remain that correlate with those characteristics. A model trained without `applicant.race` may locate `applicant.postcode`, `applicant.school`, or `applicant.spending_pattern` as proxies that reproduce the same discriminatory pattern.

Every specification corpus entry for a system that processes personal data or makes decisions affecting individuals must:

- Explicitly prohibit the use of features whose predictive utility derives from their correlation with a protected characteristic
- Require proxy analysis at feature engineering — mutual-information testing against protected characteristics before any feature is admitted to a production model
- Specify subgroup outcome testing — the acceptance criterion for model deployment must include outcome distribution analysis across protected characteristic groups
- Reference the legal basis for any retained feature that correlates with a protected characteristic

This is not a Stage 4 addition. The groundwork must be laid in the intent manifest at Stage 3. By Stage 4, the corpus entry makes it machine-enforceable.

### Discipline 5: Conflict Detection

Conflict detection (Cedar/SMT stack) is not an advanced capability at Stage 4. It is what prevents the specification corpus from becoming a source of non-deterministic agent behaviour as it grows.

A specification corpus that starts small will grow. As it grows, the probability of conflicts between rules increases. Two rules that individually make sense may produce opposing instructions for the same input. Without systematic conflict detection, these conflicts are discovered in production — where an agent's non-deterministic behaviour between conflicting rules produces unpredictable outputs.

The conflict detection requirement at Stage 4:

**A rule-of-construction clause in the corpus header** — explicit statement of how conflicts are resolved when detected at runtime: lex specialis (specific rule over general rule), lex posterior (later rule over earlier rule in the same hierarchy), lex superior (higher authority rule over lower). The clause must also state that lex posterior generalis does NOT override lex prior specialis — a commonly assumed rule that is not legally correct.

**Automated conflict detection on every corpus update** — no new entry is admitted to production without running automated conflict analysis against the existing corpus. In machine-readable corpora (OPA/Rego, Cedar policy), this can be performed by SMT solvers. In prose corpora, it requires formal legal review against the rule-of-construction clause.

**A `conflicts-with` field in each entry** — where known interactions exist between rules, they are documented explicitly. This is not a substitute for automated detection; it is supplementary documentation of known complexity.

The consequence of absent conflict detection: as the corpus grows past a few dozen rules, agents encounter situations where two or more rules apply. Without a resolution mechanism, agent behaviour becomes unpredictable at the boundary of conflicting rules. This is the specification debt that accumulates silently as the corpus grows — and it is expensive to remediate once discovered.

---

## The Specification Corpus at Stage 4

The specification corpus is the primary governance artefact of Stage 4. It is the law the Dark Factory enforces. Its quality determines the quality of every agent decision made within it.

### Architecture

The corpus has two layers:

**The intent layer** (from Stage 3) — the manifest clauses that express strategic priorities, constraints, and conflict resolution rules in human-readable form. These are the source of truth that corpus entries are derived from.

**The enforcement layer** — machine-readable corpus entries derived from intent manifest clauses. Each entry traces back to a specific manifest clause and extends it into an enforceable rule with explicit test cases, versioning, and audit logging.

The traceability between layers is non-negotiable. A corpus entry that cannot be traced to an intent manifest clause is an orphan — it has no authorised source. When it produces a questionable outcome, there is no intent basis to audit against.

### Entry structure

A minimal corpus entry contains:

| Field | Requirement |
|---|---|
| Unique ID | Stable across versions; referenced in audit logs |
| Version | Semantic — breaking changes explicitly flagged |
| `derived-from` | Reference to the intent manifest clause this entry implements |
| `normative-basis` | Single RFC 8174 keyword; named conformance role |
| `regulatory-basis` | Applicable legislation, standards, or policies |
| `enforcement` | Mode (pre-action validation, post-action audit); action on violation |
| `validation` | Exactly one check — Single Responsibility enforced |
| `test-cases` | At least one positive, one negative, one edge case |
| `audit` | What to log; retention period |
| `versioning` | Breaking-change flag; changelog |
| `conflicts-with` | Known interactions with other corpus entries |

### The quality gate

Every corpus entry must pass the eight-dimension quality checklist before admission to production. The checklist enforces all five disciplines above. No entry enters production that fails any dimension.

The quality gate is enforced by the specification corpus governance process — not by the engineering team alone. Governance over what enters the corpus is as important as governance over what enters the codebase. An agent operating from a low-quality corpus is an agent operating from bad law. The outputs follow.

---

## Escalation at Stage 4

The escalation mechanism is the safety valve of the Dark Factory. When an agent reaches the boundary of its specification envelope — a situation the corpus does not cover — it must not hallucinate a resolution. It must escalate.

The escalation package is the artefact the agent produces to trigger human involvement. A well-formed escalation package contains:

- The context of the decision that cannot be made
- The specification gap that prevents resolution (referencing the corpus by entry ID)
- The options available to the receiving human, with implications of each
- The urgency classification
- The SLA for human response

The receiving human's job is to make the decision the corpus cannot make — and then to initiate the process of extending the corpus so that the same situation does not require escalation in future. Every resolved escalation is a corpus improvement opportunity. An escalation pattern that recurs without producing a corpus extension is a governance failure.

---

## Stage 4 in Enterprise Knowledge Work

The Dark Factory in enterprise knowledge work has higher governance stakes than in software engineering. Financial decisions, legal commitments, employment decisions, and customer-facing actions cannot be rolled back. The specification corpus in these domains is not just a technical artefact — it is a compliance document.

**Finance:** The corpus for financial workflows must cover all decision classes that carry regulatory reporting obligations. Every agent action that affects a reported figure must be traceable to a corpus entry. Corpus changes that affect reported figures require dual authorisation — technical and financial governance.

**Legal:** Legal corpus entries must be reviewed by qualified legal practitioners before admission. The corpus cannot be entirely machine-authored because the legal judgements it encodes require human expertise. Legal technology staff can build the machine structure; legal professionals must approve the normative content.

**HR:** HR corpus entries that govern decisions affecting individuals require equality impact assessment before deployment. Any corpus entry that could be applied differently to individuals on the basis of a protected characteristic must demonstrate that differential application is legally justified or that it is prevented by design.

**Risk & Compliance:** The corpus for compliance workflows must be reviewed when regulations change and updated within the regulatory effective date. This is a binding governance requirement, not an operational preference. The compliance function must own review cycles for compliance-domain corpus entries.

---

## Common Failure Modes at Stage 4

**Premature autonomy.** Autonomous operation begins before the corpus reaches the coverage threshold. Agents frequently encounter uncovered situations, produce high escalation rates, and the team spends more time in exception management than the previous stage required. Fix: the 80% coverage threshold is a floor; do not begin autonomous operation below it.

**Specification corpus as prose.** The corpus is written in natural language policy documents. Agents reference it, but natural language policies cannot be machine-enforced with the precision required. Conflicts are undetectable. Test cases cannot be co-located. Audit trails are ambiguous. Fix: machine-readable format — OPA/Rego, structured YAML with defined schema, or OSCAL — as the canonical representation.

**Orphan entries.** Corpus entries exist without traceable connection to intent manifest clauses. There is no authorised source for what they enforce. When challenged, there is no governance basis. Fix: `derived-from` field as mandatory; no entry admitted without a valid manifest clause reference.

**Untested escalation.** Escalation protocols exist on paper but the humans who receive escalation packages have never done so in practice. When a live escalation arrives, the response is slow and uncertain. Fix: rehearse escalation before autonomous operation begins. Simulate packages; practice response; confirm the loop works.

**Corpus growth without governance.** The corpus grows but the governance process does not scale with it. Changes are admitted informally. Conflict detection is skipped because it is slow. Quality checks are abbreviated under time pressure. The corpus becomes a source of risk rather than a source of governance. Fix: governance scales with corpus size; quality gates are non-negotiable.

---

## Stage 4 Readiness Assessment

Before transitioning to Stage 5, the following should be true:

| Indicator | What it demonstrates |
|---|---|
| Specification corpus covers ≥80% of workflow decisions, measured | Coverage threshold is met, not estimated |
| All five specification disciplines are applied to all production entries | Quality standard is operational across the corpus |
| Every agent decision is logged with corpus entry ID and version | Audit trail is complete and unambiguous |
| Escalation rate is within defined threshold and trending toward stability | Corpus coverage is working; gaps are being systematically closed |
| At least one escalation has been received, resolved, and converted to a corpus extension | The improvement loop is proven operational |
| Behavioural baselines have been established for all production agents | Stage 5 can begin building from a defined baseline |

---

*Continue to: [Stage 5 Deep Dive — Harness Engineering](./stage-5-harness-engineering.md)*  
*Back to: [Stage 3 Deep Dive — Intent Engineering](./stage-3-intent-engineering.md) · [Specification Corpus Architecture](../02-artefacts/specification-corpus.md)*
