# Specification Quality Standard

*E1-07 · Foundations · Wave 1 · Audience: Specification Authors, Reviewers, Governance Teams*

> The eight-dimension quality standard for all specifications produced within the AI Operational Maturity Framework — intent manifests, specification corpus entries, requirements documents, and acceptance criteria at every stage.  
> See also: [Specification Discipline](./specification-discipline.md) · [Glossary](./glossary.md) · [Specification Examples](../02-artefacts/specification-examples.md)

---

## Purpose

The purpose of a quality standard is to make quality measurable, not aspirational. A specification that "seems clear" or "reads well" or "reflects intent" is not necessarily a quality specification. Quality is measurable — against observable criteria, by reviewers other than the author.

This document defines eight dimensions along which every specification in this framework can be assessed. A specification that meets all eight is ready to be enforced by agents. One that fails any single dimension is a future defect waiting to be discovered at the worst possible moment — at scale, under time pressure, in a consequential workflow.

The standard applies to every specification-level artefact in this framework:
- Stage 1 acceptance criteria and prompt scope statements
- Stage 2 context schemas and freshness SLAs
- Stage 3 intent manifest clauses
- Stage 4 specification corpus entries
- Stage 5 harness playbook conditions and anomaly thresholds
- Stage 6 environment contracts and legibility standards

The dimensions are not a checklist to satisfy before filing and forgetting. They are the test of whether a specification is fit for the purpose it will be put to: machine-enforced, autonomously applied decisions at the volume and speed of the Dark Factory.

---

## The Atomic Specification Principle

> **The Atomic Specification Principle**
>
> A specification unit that cannot be independently verified cannot be reliably enforced. Every clause in an intent manifest and every entry in a specification corpus must express exactly one obligation, directed at exactly one named actor, verifiable by exactly one test. Conjunctions ("and", "or") in a specification clause are a signal to split, not a drafting style. The same primitive — the uniquely identifiable atomic spec unit — enables RFC 8174 precision, BDD executable tests, OSCAL audit objectives, and SMT conflict detection simultaneously. You cannot have any of them without it.

This principle is the foundation on which the eight dimensions rest. Dimensions 1 through 3 are corollaries of it. Dimensions 4 through 8 are conditions for it to hold under operational stress.

---

## The Eight Quality Dimensions

---

### Dimension 1 — RFC 8174 Normative Precision

**Definition:** Obligation keywords (MUST, SHALL, SHOULD, MAY, MUST NOT, SHOULD NOT, SHALL NOT) carry normative force only when presented in ALL CAPS and only when the document contains the RFC 8174 boilerplate declaration. Without the boilerplate, capitalised keywords are typographic emphasis, not contractual obligations.

**What failure looks like:**
- The RFC 8174 boilerplate declaration is absent from the document header
- Obligation keywords appear in mixed case ("must", "should") and are treated as normative
- SHOULD is used without a rationale explaining why the obligation is advisory rather than absolute
- Obligation keywords are applied to entities that cannot conform (e.g., "data MUST be accurate" — data cannot conform to anything)
- Keywords are used decoratively ("SHOULD be considered") rather than normatively

**What ideal looks like:**
- The RFC 8174 boilerplate declaration appears verbatim in the document header
- Every keyword is bound to a named conformance role — a named actor who must or must not do something
- Every SHOULD is accompanied by an explicit rationale explaining why the deviation is permitted and under what conditions
- Keywords are reserved for genuine obligation points where compliance matters

**The RFC 8174 boilerplate (verbatim — copy this into every normative document):**
```
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in
BCP 14 [RFC 2119] [RFC 8174] when, and only when, they appear in all
capitals, as shown here.
```

**Test:** Remove the boilerplate declaration from the document. Does the remaining text still read correctly without the capitalisation carrying special meaning? If yes — if the document makes the same sense without the boilerplate — the keywords are decorative, not normative. The document fails Dimension 1.

---

### Dimension 2 — Single Responsibility (Atomicity)

**Definition:** Each specification unit expresses exactly one obligation. It cannot be split into independent parts without losing meaning. It cannot be verified without depending on another unit. One verb of obligation, one named subject, one testable condition.

**What failure looks like:**
- Conjunctions ("and", "or") joining multiple obligations in one clause: "The agent MUST validate the applicant's income AND check their credit history"
- Multiple RFC 2119 keywords in one clause (a reliable signal that multiple obligations are present)
- Purpose, rationale, or context embedded in the obligation sentence rather than in a separate field
- Scope qualifiers that make the clause context-dependent without stating the context explicitly
- Parenthetical additions that carry independent obligation force

**What ideal looks like:**
- One RFC 2119 keyword per clause
- One named actor (conformance role)
- One condition — the specific situation the obligation governs
- Rationale in a separate field (`reasoning`, `why`), not in the obligation text
- INCOSE requirements quality metrics R18 through R23 met: singular, complete, unambiguous, verifiable, consistent, unmodified

**Test:** Can you write a single automated test that passes or fails this clause, without also testing any other clause? If the test requires evaluating two different conditions, the clause has two obligations — split it. If the test requires knowledge from another clause to set up, the clause has undeclared dependencies — make them explicit.

---

### Dimension 3 — Testability

**Definition:** Each specification unit admits exactly one verification method and requires at least two test cases: one positive (a case that MUST pass) and one negative (a case that MUST fail). The test cases are co-located with the specification unit, not stored elsewhere.

**What failure looks like:**
- The obligation uses imprecise language that requires human judgement to evaluate: "appropriate", "reasonable", "as needed", "in a timely manner", "sufficient"
- No test cases are defined — the specification states what MUST happen but not what constitutes passing
- Test cases exist but are stored separately from the specification, creating a synchronisation risk
- Evaluation requires simultaneously testing multiple specification clauses to determine compliance
- The test for the clause would pass even if the clause is violated in edge cases

**What ideal looks like:**
- Binary pass/fail evaluation against observable, measurable evidence — no room for interpretation
- At least one positive test case: "given [input], the agent produces [output] — PASS"
- At least one negative test case: "given [input], the agent does not produce [output] — PASS" (or equivalently, "given [prohibited input], the agent rejects it — PASS")
- At least one edge case test: the boundary condition where the specification's scope is at its limit
- Test cases co-located in the specification artefact itself (in the YAML `test-cases` block, the Gherkin feature file, or equivalent)
- A junior engineer can write a passing automated test from the specification alone, without asking for clarification

**Test:** Show the clause to an engineer who had no involvement in writing it. Ask them to write a passing test. If they need to ask a clarifying question, the clause is under-specified. If they write a test that the author considers incorrect, the clause is ambiguous. Either outcome fails Dimension 3.

---

### Dimension 4 — Completeness

**Definition:** The specification covers its stated scope without leaving gaps that require human interpretation to fill. All terms used in the specification are defined. All conditions and exceptions are stated. The boundary of the specification — what it covers and what it does not — is explicit.

**What failure looks like:**
- Terms used in the obligation are not defined in the document or by reference to a named glossary
- Conditions that depend on context not specified in the specification (e.g., "when applicable", "where required")
- Scope limitations not stated — the specification appears to cover more than it does
- Novel situations that fall within the apparent scope are not addressed, leaving agents to infer
- Derived data and proxy risks not addressed for specifications involving personal data

**What ideal looks like:**
- All terms used in obligation clauses are defined in a `definitions` block or by reference to the framework Glossary
- Scope is stated explicitly: "This specification governs [specific situation]" and "This specification does not govern [adjacent situation]"
- A `known-gaps` field documents situations within the apparent scope that are intentionally not covered, with handling instructions (escalate, defer, default action)
- For any specification involving personal data processing: derived data risks and proxy discrimination risks are explicitly addressed (or the specification explicitly states they are out of scope with a rationale)

**Test:** Identify five scenarios that fall within the stated scope of the specification. Can an agent operating solely against this specification, with no additional knowledge, make the correct decision for all five? Identify the one scenario that the author did not anticipate. What does the specification produce? If the answer is "undefined behaviour", the specification fails Dimension 4.

---

### Dimension 5 — Traceability

**Definition:** Every specification unit can be traced in both directions — upward to the source intent or requirement that created it, and downward to the tests and audit records that verify it. The chain from organisational intent to agent decision must be reconstructible from the specification metadata alone.

**What failure looks like:**
- No stable unique identifier — the clause cannot be referenced from test code, audit logs, or other documents without ambiguity
- No `derived-from` field linking the specification to its source intent manifest clause or regulatory basis
- No `verified-by` field linking to the test IDs that exercise this specification
- Audit logs record what the agent decided but not which specification clause version authorised the decision
- The specification has been updated without a version increment, so historical decisions cannot be mapped to the clause version that governed them

**What ideal looks like:**
- Every specification unit has a stable, unique identifier (e.g., `CRED-DATA-005`) that survives refactoring
- A `derived-from` field names the intent manifest clause ID and the regulatory or policy basis
- A `verified-by` field names the test IDs (Gherkin scenarios, OPA test names, or equivalent) that exercise this unit
- Audit logs capture the specification unit ID and semantic version with every decision governed by that unit
- Given any audit log entry, the corresponding specification version can be retrieved and compared with the current version

**Test:** Given an agent decision from six months ago, identified only by its audit log entry, can you determine exactly which specification clause and which version governed that decision? Can you determine whether that clause has since been amended in a breaking way? If either answer is no, the specification fails Dimension 5.

---

### Dimension 6 — Conflict Freedom

**Definition:** No two specification units in the corpus produce contradictory enforcement decisions for the same input. Where two units could apply, their interaction is explicitly resolved by a precedence rule (rule of construction). Conflict detection is automated — not dependent on manual review of a growing corpus.

**What failure looks like:**
- Two rules that both fire on the same input with different outcomes — one permits, one prohibits
- No rule-of-construction clause in the corpus header defining precedence: lex specialis (specific over general), lex posterior (later over earlier), lex superior (higher authority level)
- No `conflicts-with` field on entries with known scope overlaps
- No automated conflict detection — conflicts discovered in production rather than at admission time
- Lex posterior generalis treated as overriding lex prior specialis — a common error that inverts the correct precedence

**What ideal looks like:**
- A rule-of-construction clause in the corpus header explicitly states: lex specialis prevails over lex generalis; lex posterior prevails for same-specificity conflicts; lex superior prevails when authority levels differ; lex posterior generalis does NOT override lex prior specialis
- A `conflicts-with` field on every entry whose scope could overlap with another, documenting the interaction and how it is resolved
- Automated conflict detection (OPA test suite, Cedar analysis, SMT-based checking) runs on every corpus admission — no new entry is admitted without conflict verification
- Breaking changes in one corpus entry trigger re-evaluation of all entries with overlapping scope

**Test:** For every pair of specification units whose stated scopes could overlap, is the conflict explicitly resolved — either by the rule-of-construction clause, by explicit `conflicts-with` documentation, or by demonstrated non-overlapping scope? A corpus that cannot answer this test question for all pairs fails Dimension 6.

---

### Dimension 7 — Versioning and Change Management

**Definition:** Specifications are versioned with semantic precision. Changes are logged. Breaking changes — changes that would cause a previously-compliant agent to become non-compliant, or a previously non-compliant agent to become compliant — are explicitly flagged and require change governance.

**What failure looks like:**
- Version numbers without semantic meaning (v1, v2, v3 with no definition of what constitutes a major vs. minor change)
- No changelog — changes cannot be understood without reading the diff
- No definition of "breaking change" for this corpus
- Agents not notified of version updates — running against stale specification versions without knowing it
- Semantic-version bumps that classify a breaking change as non-breaking to avoid governance overhead

**What ideal looks like:**
- Semantic versioning where:
  - MAJOR version change = breaking change (previously-compliant agent becomes non-compliant, or previously-prohibited action becomes permitted)
  - MINOR version change = backwards-compatible addition (new obligations for new situations not previously covered)
  - PATCH version change = clarification, editorial correction, no change to compliance outcomes
- A `breaking-change: true/false` boolean field in the version metadata
- A changelog entry for every version increment: what changed, why, who approved
- A deprecation protocol: deprecated clauses are marked, remain enforced during the deprecation window, then retired with notification
- Deployed agents verify they are operating against the current specification version at startup

**Test:** Given specification versions v2.0 and v2.1, can you determine from the document alone — without examining an external changelog or asking the author — whether any agent fully compliant with v2.0 would need to change its behaviour to be compliant with v2.1? If no, the versioning fails Dimension 7.

---

### Dimension 8 — Proxy Discrimination Prevention *(applies to specifications governing personal data processing)*

**Definition:** Specifications for systems that process personal data about individuals explicitly address the risk of proxy discrimination — the use of facially neutral features that correlate with protected characteristics to reproduce discriminatory outcomes even after those characteristics are removed.

This dimension applies whenever the specification governs: credit assessment, employment decisions, insurance underwriting, housing allocation, educational access, healthcare resource allocation, or any other context where protected characteristics (age, sex, race, religion, disability, gender reassignment, marriage and civil partnership, pregnancy and maternity, sexual orientation under the Equality Act 2010; or analogous characteristics in other jurisdictions) could influence outcomes.

**What failure looks like:**
- The specification prohibits explicit protected-characteristic fields but is silent on derived or correlated features — treating "fairness through unawareness" as sufficient protection
- No proxy analysis is required at feature engineering, model training, or inference stages
- No disparate impact testing is specified — the specification does not require measurement of outcome distributions across protected characteristic groups
- No procedure for reviewing features with statistically significant correlation to protected characteristics

**What ideal looks like:**
- Explicit rejection of fairness-through-unawareness as a compliance strategy: the specification acknowledges that removing a protected-characteristic field does not prevent a model from locating a substitute feature
- Mandatory mutual-information testing and adversarial classifier recovery at feature engineering: any feature with statistically significant correlation to a protected characteristic must be either justified by documented less-discriminatory-alternative analysis or removed
- Subgroup outcome testing required before production deployment, with documented acceptable tolerance thresholds for outcome distribution divergence
- Lawful processing basis stated for any special-category data used in bias detection or disparity measurement (EU AI Act Article 10(5); UK GDPR Article 9 — the explicit permission for processing sensitive data for equality monitoring purposes)
- An escalation trigger: proxy analysis results reviewed by a named governance function before any model or agent reaches production

**Test:** Does this specification prevent an agent or model from locating a substitute feature that reproduces discriminatory outcomes after all explicitly prohibited fields are removed? If the specification is silent on this question, it fails Dimension 8.

---

## The Quality Checklist

Use this checklist as a pre-admission gate for any specification corpus entry, or as a review rubric for any intent manifest clause or requirements document.

| Dimension | Check | Pass / Fail |
|---|---|---|
| RFC 8174 | Document contains the RFC 8174 boilerplate declaration verbatim | |
| RFC 8174 | All obligation keywords (MUST, SHOULD, MAY, etc.) bound to a named conformance role | |
| RFC 8174 | All SHOULDs accompanied by explicit rationale for advisory status | |
| Atomicity | No conjunctions ("and", "or") joining multiple obligations within one clause | |
| Atomicity | Exactly one verb of obligation, one subject, one testable condition per clause | |
| Atomicity | Rationale in a separate field, not embedded in the obligation sentence | |
| Testability | Binary pass/fail evaluation against observable evidence — no room for interpretation | |
| Testability | At least one positive test case co-located with the clause | |
| Testability | At least one negative test case co-located with the clause | |
| Completeness | All terms used in obligation clauses defined in document or by reference | |
| Completeness | Scope explicitly stated, including what is NOT covered | |
| Completeness | Known-gaps documented with handling instructions | |
| Traceability | Stable unique ID assigned that will survive refactoring | |
| Traceability | `derived-from` field names source intent clause and regulatory basis | |
| Traceability | `verified-by` field names test IDs that exercise this clause | |
| Conflict Freedom | Rule-of-construction clause present in corpus header | |
| Conflict Freedom | Automated conflict detection run on this corpus update | |
| Conflict Freedom | `conflicts-with` field present or explicit statement of non-conflict | |
| Versioning | Semantic version with `breaking-change` boolean field | |
| Versioning | Changelog entry present for this version | |
| Proxy *(if personal data)* | Proxy analysis methodology required at feature engineering stage | |
| Proxy *(if personal data)* | Subgroup outcome testing specified with tolerance thresholds | |
| Proxy *(if personal data)* | Lawful processing basis stated for special-category data use | |

---

## How to Use This Standard

### For specification authors

Apply the checklist before submitting any specification unit for review. If any row fails, remediate before submission. Submitting a failing specification for review does not save time — it generates review cycles that would not otherwise occur.

The most common failure patterns and their remediations:

| Failure | Symptom | Remediation |
|---|---|---|
| Missing RFC 8174 boilerplate | Capitalised keywords with no declaration | Add boilerplate to document header; confirm all keywords are bound to named actors |
| Conjunction in obligation | "MUST validate X AND check Y" | Split into two clauses: CLAUSE-001 governs X, CLAUSE-002 governs Y |
| Undefined terms | "The agent MUST apply the standard credit policy" | Define "standard credit policy" in the definitions block or replace with a specific rule |
| No test cases | Clause states what MUST happen but not how compliance is verified | Write the test cases first — if they cannot be written, the clause is not ready |
| Missing `derived-from` | Corpus entry with no link to intent manifest | Identify the intent manifest clause that authorises this rule; if none exists, the entry is unauthorised |
| SHOULD without rationale | "The agent SHOULD consider mitigating factors" | State why this is advisory: under what conditions is non-compliance acceptable? |
| Proxy silence | Specification governing credit assessment with no proxy clause | Add Dimension 8 content; see [Specification Examples](../02-artefacts/specification-examples.md) for CRED-INTENT-004-005 as a template |

### For reviewers

The checklist is the review protocol. A specification review is not a reading for comprehension — it is a systematic check against each dimension. A specification that reads well but fails Dimension 5 (no traceability) is not a quality specification.

Assign each checklist row a pass or fail during review. Fail means: this row must be remediated before admission. Partial is not a valid score — a row either passes or it does not.

### For governance teams

The Quality Checklist is the admission gate for the specification corpus. No corpus entry is admitted without a completed checklist with no fails. The corpus owner is accountable for enforcing this gate.

The checklist is also the audit instrument for periodic corpus health reviews. Run the checklist against every corpus entry on the review cadence defined in the corpus governance process. Entries that have decayed (e.g., a `derived-from` link that now points to a retired intent clause) must be remediated or retired.

The Maturity Debt of an organisation can often be read directly from the checklist results: an organisation operating at Stage 4 technology maturity with Stage 1 practice maturity will have a corpus where the majority of entries fail Dimensions 3 through 8 — testability, completeness, traceability, conflict freedom, versioning, and proxy prevention. That gap is the Maturity Debt.

---

*Continue to: [Specification Examples](../02-artefacts/specification-examples.md) · [Specification Discipline](./specification-discipline.md)*  
*Back to: [Glossary](./glossary.md)*
