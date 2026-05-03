# Specification Examples — Reference Library

*E4-00 · Artefacts · Wave 4 · Audience: Specification Authors, Reviewers, Governance Teams*

> **E4-00 · Artefacts · Wave 4**  
> Canonical reference examples of high-quality specifications at Intent level (Stage 3) and Specification Corpus level (Stage 4), verified against the eight quality dimensions of the Specification Quality Standard.  
> See also: [Specification Quality Standard](../00-foundations/specification-quality-standard.md) · [Requirements Specification Templates](./requirements-spec-templates.md) · [Specification Corpus Architecture](./specification-corpus.md)

---

## Introduction

This document provides the quality bar — concrete, verified examples that all other specification artefacts in this framework must meet.

Both examples are drawn from the **Meridian Capital** scenario: a financial services firm deploying agents across commercial lending workflows. The governance concern is data use in credit assessment — a high-stakes domain where proxy discrimination is a legal and ethical risk and where the specification must be enforceable both by machines at Stage 4 and auditable by regulators.

The examples show the same governance concern at two maturity levels:

- **Example A** — Intent Level (Stage 3): Five atomic intent manifest clauses governing data use in credit assessment
- **Example B** — Specification Corpus Level (Stage 4): Five atomic YAML corpus entries enforcing those intent clauses

Together they demonstrate the translation chain from organisational intent to machine-enforceable specification.

### The Meridian Capital Scenario

Meridian Capital underwrites commercial loans for small and medium enterprises. They are deploying agents at Stage 4 to handle initial creditworthiness assessment — replacing a workflow previously conducted by human underwriters. The agents must evaluate applicants against a defined set of criteria and either approve, decline, or escalate for human review.

The Data Ethics function has flagged that the previous human underwriting process showed statistically significant outcome disparities across postcodes (a proxy for ethnicity in several of Meridian's operating markets). The specification must address both explicit protected-characteristic exclusions and the proxy risk that removing those fields does not eliminate.

---

## The Translation Chain

```
Organisational Intent
        ↓ [Stage 3] Intent Manifest Clause — reasoned, RFC 8174, atomic
        ↓ [Stage 4] Specification Corpus Entry — machine-enforceable, testable
        ↓ [Stage 5] Harness Enforcement — pre-assessment validation, audit log
        ↓ [Stage 6] Environment Contract — structurally impossible to violate
```

Each level translates the level above it into a more precise, more enforceable form. Intent manifest clauses encode *why* the organisation holds a position and *what* it prohibits — in language domain authorities can author and review. Corpus entries translate that intent into machine-executable rules — precise enough to be evaluated without human interpretation.

The translation chain is the traceability chain. Every corpus entry derives from an intent clause. Every audit log entry references a corpus entry. Regulatory inquiries work backwards up the chain.

---

## Example A — Intent Level (Stage 3)

### The RFC 8174 Boilerplate Declaration

The following declaration appears at the top of the Meridian Capital Intent Manifest and applies to all clauses within it.

```
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in
BCP 14 [RFC 2119] [RFC 8174] when, and only when, they appear in all
capitals, as shown here.
```

---

### CRED-INTENT-004-001 — Protected Characteristics Prohibition

```markdown
**Clause ID:** CRED-INTENT-004-001  
**Version:** 1.0.0  
**Effective date:** 2024-01-01  
**Jurisdiction:** United Kingdom  
**Domain:** Credit Assessment  

A credit assessment agent MUST NOT use the following characteristics 
as inputs to, or features within, any creditworthiness determination: 
age, sex, race, religion or belief, disability, gender reassignment, 
marriage and civil partnership, pregnancy and maternity, or sexual 
orientation as defined by the Equality Act 2010.

**Conformance role:** Credit assessment agent  
**Obligation level:** MUST NOT (absolute prohibition — no deviation permitted)  
**Regulatory basis:** Equality Act 2010 s.4; FCA PRIN 12; Consumer Duty  

**Reasoning:** Direct use of protected characteristics in credit 
decisions is unlawful under UK equality legislation and inconsistent 
with Meridian Capital's obligations under the FCA Consumer Duty. This 
prohibition is absolute — there is no business justification that 
permits deviation. For the treatment of derived features that correlate 
with these characteristics, see CRED-INTENT-004-005.

**Escalation trigger:** Any request to add a feature directly encoding 
a protected characteristic to a credit assessment model MUST be 
escalated to the General Counsel before any technical evaluation 
begins. Escalation package standard: CRED-ESC-001.
```

---

### CRED-INTENT-004-002 — Postcode-as-Primary-Factor Prohibition

```markdown
**Clause ID:** CRED-INTENT-004-002  
**Version:** 1.0.0  
**Effective date:** 2024-01-01  
**Jurisdiction:** United Kingdom  
**Domain:** Credit Assessment  

A credit assessment agent MUST NOT use postcode as the primary 
determinative factor in a creditworthiness decision.

**Conformance role:** Credit assessment agent  
**Obligation level:** MUST NOT (conditional — applies when postcode 
is the primary factor; does not prohibit postcode as one of many 
factors where its weight is demonstrably non-determinative)  
**Regulatory basis:** Equality Act 2010 s.19 (indirect discrimination); 
ICO AI and Data Protection Guidance Annex A  

**Reasoning:** Postcode correlates with ethnicity, income level, and 
other protected characteristics in Meridian Capital's operating 
markets. Using postcode as the primary determinative factor in a 
credit decision produces disparate outcomes for groups with protected 
characteristics, constituting indirect discrimination even where the 
intent is facially neutral. Postcode may be used as one contextual 
factor where its weight is demonstrably non-determinative and where 
postcode-as-proxy risk has been assessed under CRED-INTENT-004-005.

**Escalation trigger:** Where postcode feature importance exceeds 
30% of model decision weight, escalate to the Data Ethics function 
before production deployment. Escalation package standard: CRED-ESC-002.
```

---

### CRED-INTENT-004-003 — Unconsented Social Media Prohibition

```markdown
**Clause ID:** CRED-INTENT-004-003  
**Version:** 1.0.0  
**Effective date:** 2024-01-01  
**Jurisdiction:** United Kingdom  
**Domain:** Credit Assessment  

A credit assessment agent MUST NOT use data sourced from social media 
platforms as input to a creditworthiness determination unless the 
applicant has provided explicit, informed, and freely given consent to 
that specific use of that specific data.

**Conformance role:** Credit assessment agent  
**Obligation level:** MUST NOT (conditional — applies absent verified 
consent; use is permitted only where consent is documented and 
reviewable in the audit trail)  
**Regulatory basis:** UK GDPR Article 6(1)(a) (consent as lawful basis); 
UK GDPR Article 7 (conditions for consent); FCA COBS 2.1  

**Reasoning:** Social media data is typically collected for purposes 
unrelated to credit assessment. Its use for creditworthiness decisions 
without specific consent violates the UK GDPR purpose limitation 
principle. Social media data also presents significant proxy 
discrimination risk — social networks tend to be homophilous, 
meaning an applicant's network and activity may be statistically 
predictive of protected characteristics. Consent does not eliminate 
the proxy risk addressed in CRED-INTENT-004-005; both clauses apply 
concurrently where social media data is used with consent.

**Escalation trigger:** None at clause level — consent is a 
data-capture governance process, not an agent-level escalation trigger.
```

---

### CRED-INTENT-004-004 — Health and Medical Data Prohibition

```markdown
**Clause ID:** CRED-INTENT-004-004  
**Version:** 1.0.0  
**Effective date:** 2024-01-01  
**Jurisdiction:** United Kingdom  
**Domain:** Credit Assessment  

A credit assessment agent MUST NOT use health or medical data as 
input to a creditworthiness determination.

**Conformance role:** Credit assessment agent  
**Obligation level:** MUST NOT (absolute prohibition — no deviation 
permitted, including where the applicant has provided consent)  
**Regulatory basis:** UK GDPR Article 9 (special category data); 
Equality Act 2010 s.6 (disability as protected characteristic); 
FCA PRIN 12  

**Reasoning:** Health and medical data is special-category data under 
UK GDPR, subject to heightened protection. Its use in credit 
assessment is not a legitimate processing purpose under Article 9 and 
would constitute disability discrimination under the Equality Act 2010 
in the majority of applications. This prohibition is absolute — unlike 
social media data, consent does not establish a lawful basis for 
health data use in credit assessment under UK GDPR Article 9.

**Escalation trigger:** Any feature in a proposed credit assessment 
model that derives from medical records, insurance claims, pharmacy 
data, or health-related spending categories MUST be escalated to the 
General Counsel and Data Protection Officer jointly before any 
technical evaluation begins. Escalation package standard: CRED-ESC-001.
```

---

### CRED-INTENT-004-005 — Derived Data and Proxy Discrimination Prohibition

```markdown
**Clause ID:** CRED-INTENT-004-005  
**Version:** 1.0.0  
**Effective date:** 2024-01-01  
**Jurisdiction:** United Kingdom  
**Domain:** Credit Assessment  

A credit assessment agent MUST NOT use any feature, derived feature, 
composite variable, or model representation whose predictive utility 
derives primarily from its correlation with a protected characteristic 
as defined in CRED-INTENT-004-001, regardless of whether that feature 
directly encodes the characteristic.

**Conformance role:** Credit assessment agent  
**Obligation level:** MUST NOT (absolute — same force as 
CRED-INTENT-004-001; no deviation permitted)  
**Regulatory basis:** Equality Act 2010 s.19 (indirect discrimination); 
FCA PRIN 12; ICO AI and Data Protection Guidance Annex A (proxy 
analysis requirement); EU AI Act Article 10(5) (lawful processing 
basis for bias testing data)  
**Temporal scope:** Applies at feature engineering, model training, 
and inference stages  

**Reasoning:** Removing protected-characteristic fields from model 
inputs does not prevent discrimination if substitute features are 
available that correlate with those characteristics. A model trained 
without `applicant.race` may locate `applicant.postcode`, 
`applicant.school`, `applicant.spending_pattern`, or other correlated 
features as proxies that reproduce the same discriminatory pattern. 
This phenomenon — fairness through unawareness — is neither legally 
sufficient nor ethically adequate under UK equality law. The ICO's 
AI and Data Protection Guidance (Annex A) explicitly requires proxy 
analysis at feature engineering. Meridian Capital's own historical 
data shows statistically significant outcome disparities by postcode 
that are consistent with proxy discrimination; this clause responds 
directly to that finding.

**Test:** After removing all fields prohibited under 
CRED-INTENT-004-001 through CRED-INTENT-004-004, apply 
mutual-information testing and adversarial classifier recovery against 
all remaining features. Any feature with statistically significant 
correlation to a protected characteristic (mutual information > 0.05 
or adversarial classifier AUC > 0.65) MUST be either:
(a) removed from the feature set, or
(b) justified by documented less-discriminatory-alternative analysis 
    reviewed and approved by the Data Ethics function.

**Escalation trigger:** Proxy analysis results MUST be reviewed by 
the Data Ethics function before any model or agent reaches production. 
Escalation package standard: CRED-ESC-003.
```

---

## Example B — Specification Corpus Level (Stage 4)

The following YAML entries translate the five intent clauses above into machine-enforceable specification corpus entries. Each entry derives from exactly one intent clause and enforces exactly one prohibition.

---

### CRED-DATA-005 — Proxy Discrimination Prevention (complete entry)

This entry is shown in full as the reference example. It is the most technically complex of the five entries and the one most often absent from credit assessment specifications.

```yaml
id: CRED-DATA-005
title: Proxy Discrimination — Derived Feature Prohibition
version: 1.0.0
breaking-change: false
effective-date: "2024-01-01"

derived-from:
  intent-clause: CRED-INTENT-004-005
  regulatory-basis:
    - "Equality Act 2010 s.19"
    - "FCA PRIN 12"
    - "ICO AI and Data Protection Guidance Annex A"
    - "EU AI Act Article 10(5)"

normative-basis: MUST NOT
conformance-role: credit-assessment-agent
jurisdiction: UK
domain: credit-assessment
temporal-scope: "feature engineering, model training, and inference"

obligation: >
  A credit-assessment-agent MUST NOT use any feature, derived feature,
  composite variable, or model representation whose predictive utility
  derives primarily from its correlation with a protected characteristic
  as defined in CRED-DATA-001, regardless of whether that feature
  directly encodes the characteristic.

definitions:
  protected-characteristic: >
    As defined in CRED-DATA-001: age, sex, race, religion or belief,
    disability, gender reassignment, marriage and civil partnership,
    pregnancy and maternity, or sexual orientation under the Equality
    Act 2010.
  proxy-feature: >
    A feature whose mutual information with a protected characteristic
    exceeds 0.05, or for which an adversarial classifier can predict
    the protected characteristic with AUC > 0.65.
  less-discriminatory-alternative-analysis: >
    Documented assessment showing that no alternative feature set
    achieves comparable predictive performance with lower proxy risk,
    reviewed and approved by the Data Ethics function.

enforcement:
  mode: pre-assessment-validation
  action-on-violation: block-and-escalate
  escalation-target: data-ethics-function
  escalation-package-standard: CRED-ESC-003
  audit-reference: mandatory

validation:
  check: proxy-analysis-clearance
  method: >
    Verify that a proxy analysis report for this model version exists
    in the Data Ethics approval register, is dated no more than 90 days
    before deployment, and records PASS for all features in the
    feature set against the proxy-feature thresholds defined above.
  result: binary-pass-fail

test-cases:
  - id: CRED-DATA-005-T001
    description: "Model with cleared proxy analysis — PASS"
    given: "A credit assessment model with proxy analysis report dated 2024-01-15, all features MI < 0.05, adversarial AUC < 0.65"
    when: "Pre-assessment validation is run"
    then: "Validation passes; model proceeds to assessment workflow"
    expected: PASS

  - id: CRED-DATA-005-T002
    description: "Model with postcode MI > 0.05 and no LDAA — FAIL"
    given: "A credit assessment model where postcode has MI = 0.12 with applicant ethnicity, no less-discriminatory-alternative analysis on record"
    when: "Pre-assessment validation is run"
    then: "Validation fails; model is blocked; escalation package CRED-ESC-003 is generated"
    expected: FAIL

  - id: CRED-DATA-005-T003
    description: "Model with proxy feature but approved LDAA — PASS"
    given: "A credit assessment model where postcode has MI = 0.09 with applicant ethnicity, AND a LDAA exists showing no lower-proxy alternative achieves comparable Gini coefficient, approved by Data Ethics 2024-01-10"
    when: "Pre-assessment validation is run"
    then: "Validation passes; LDAA reference logged in audit trail"
    expected: PASS

  - id: CRED-DATA-005-T004
    description: "Stale proxy analysis (> 90 days) — FAIL"
    given: "A credit assessment model with proxy analysis report dated 2023-09-01 (> 90 days before deployment date 2024-01-15)"
    when: "Pre-assessment validation is run"
    then: "Validation fails; stale-analysis escalation generated"
    expected: FAIL

known-gaps:
  - gap-id: CRED-DATA-005-G001
    description: >
      This entry does not govern proxy risk in embedding representations
      or neural network intermediate layers, where feature importance
      analysis is insufficient to detect protected-characteristic
      encoding. Interpretability tooling (SHAP, LIME) for deep
      architectures is not yet standardised. Handling: escalate any
      deep-learning model to Data Ethics for architecture-level review
      before proxy validation.
    status: open
    owner: data-ethics-function
    resolution-target: "2024-Q3"

conflicts-with:
  - entry-id: CRED-DATA-002
    interaction: >
      CRED-DATA-002 prohibits postcode as the primary determinative
      factor. CRED-DATA-005 prohibits postcode where MI with a
      protected characteristic exceeds threshold. These interact:
      a postcode that passes CRED-DATA-002 (non-primary) may still
      fail CRED-DATA-005 (proxy). Both constraints apply
      independently. Rule of construction: lex specialis —
      CRED-DATA-005 is the more specific prohibition and governs
      where both apply.

audit:
  log-fields:
    - specification-id: CRED-DATA-005
    - specification-version: 1.0.0
    - validation-result: PASS|FAIL
    - proxy-analysis-report-id: "<report-id>"
    - ldaa-reference: "<ldaa-id or null>"
    - timestamp: ISO-8601
    - agent-id: "<agent-id>"
  retention-period: "7 years (FCA record-keeping requirement)"
  log-integrity: append-only

versioning:
  current: 1.0.0
  changelog:
    - version: 1.0.0
      date: "2024-01-01"
      author: data-ethics-function
      approved-by: general-counsel
      notes: "Initial admission. Addresses postcode proxy finding from 2023 underwriting audit."
      breaking-change: false
  deprecation-protocol: "90-day notice; successor entry required before deprecation"
```

---

### CRED-DATA-001 through CRED-DATA-004 (abbreviated)

The following four entries follow the same structure as CRED-DATA-005. Key fields shown; structure is identical.

```yaml
# CRED-DATA-001 — Protected Characteristics Prohibition
id: CRED-DATA-001
title: Protected Characteristics — Direct Use Prohibition
version: 1.0.0
derived-from:
  intent-clause: CRED-INTENT-004-001
  regulatory-basis: ["Equality Act 2010 s.4", "FCA PRIN 12"]
normative-basis: MUST NOT
conformance-role: credit-assessment-agent
obligation: >
  A credit-assessment-agent MUST NOT use age, sex, race, religion or
  belief, disability, gender reassignment, marriage and civil
  partnership, pregnancy and maternity, or sexual orientation as
  inputs to any creditworthiness determination.
enforcement:
  mode: pre-assessment-validation
  action-on-violation: block-and-escalate
  escalation-target: general-counsel
  escalation-package-standard: CRED-ESC-001
validation:
  check: feature-set-exclusion
  method: >
    Verify that no field in the feature set maps to a protected
    characteristic. Field mapping registry maintained by Data
    Engineering; checked against prohibited-fields list version
    matching this entry version.
  result: binary-pass-fail
# ... test-cases, known-gaps, audit, versioning as per CRED-DATA-005
```

```yaml
# CRED-DATA-002 — Postcode-as-Primary-Factor Prohibition
id: CRED-DATA-002
title: Postcode — Primary Determinative Factor Prohibition
version: 1.0.0
derived-from:
  intent-clause: CRED-INTENT-004-002
  regulatory-basis: ["Equality Act 2010 s.19", "ICO AI Guidance Annex A"]
normative-basis: MUST NOT
conformance-role: credit-assessment-agent
obligation: >
  A credit-assessment-agent MUST NOT use postcode as the primary
  determinative factor in a creditworthiness decision.
enforcement:
  mode: post-inference-audit
  action-on-violation: flag-for-review
  escalation-target: data-ethics-function
  escalation-package-standard: CRED-ESC-002
  threshold: "postcode feature importance > 30% of model decision weight"
# ... test-cases, known-gaps, conflicts-with, audit, versioning
```

```yaml
# CRED-DATA-003 — Unconsented Social Media Prohibition
id: CRED-DATA-003
title: Social Media Data — Consent Requirement
version: 1.0.0
derived-from:
  intent-clause: CRED-INTENT-004-003
  regulatory-basis: ["UK GDPR Article 6(1)(a)", "UK GDPR Article 7", "FCA COBS 2.1"]
normative-basis: MUST NOT
conformance-role: credit-assessment-agent
obligation: >
  A credit-assessment-agent MUST NOT use data sourced from social
  media platforms as input to a creditworthiness determination unless
  the audit trail for this assessment records verified consent
  reference ID for the specific applicant and specific data use.
enforcement:
  mode: pre-assessment-validation
  action-on-violation: block-and-escalate
  escalation-target: data-protection-officer
  escalation-package-standard: CRED-ESC-004
# ... test-cases, known-gaps, audit, versioning
```

```yaml
# CRED-DATA-004 — Health and Medical Data Prohibition
id: CRED-DATA-004
title: Health and Medical Data — Absolute Prohibition
version: 1.0.0
derived-from:
  intent-clause: CRED-INTENT-004-004
  regulatory-basis: ["UK GDPR Article 9", "Equality Act 2010 s.6", "FCA PRIN 12"]
normative-basis: MUST NOT
conformance-role: credit-assessment-agent
obligation: >
  A credit-assessment-agent MUST NOT use health or medical data as
  input to a creditworthiness determination.
enforcement:
  mode: pre-assessment-validation
  action-on-violation: block-and-escalate
  escalation-target: general-counsel
  escalation-package-standard: CRED-ESC-001
# ... test-cases, known-gaps, audit, versioning
```

---

## Quality Verification

Both example sets are verified against the eight dimensions of the [Specification Quality Standard](../00-foundations/specification-quality-standard.md).

### Example A — Intent Manifest Clauses (CRED-INTENT-004-001 through 005)

| Dimension | Check | Result |
|---|---|---|
| RFC 8174 | Boilerplate declaration present in manifest header | **PASS** |
| RFC 8174 | All keywords bound to named conformance role ("A credit assessment agent") | **PASS** |
| RFC 8174 | CRED-INTENT-004-002 SHOULD → replaced with MUST NOT + conditional scope | **PASS** |
| Atomicity | Each clause contains exactly one prohibition, no conjunctions | **PASS** |
| Atomicity | Rationale in separate "Reasoning" paragraph, not in obligation sentence | **PASS** |
| Testability | CRED-INTENT-004-005 includes explicit test methodology (MI threshold, adversarial AUC) | **PASS** |
| Testability | Positive and negative conditions derivable from each clause | **PASS** |
| Completeness | All terms defined (protected characteristic, proxy feature, LDAA) | **PASS** |
| Completeness | CRED-INTENT-004-002 scope limit stated (primary factor, not any use) | **PASS** |
| Traceability | Stable clause IDs (CRED-INTENT-004-NNN) assigned | **PASS** |
| Traceability | Regulatory basis named per clause | **PASS** |
| Conflict Freedom | CRED-INTENT-004-001 and 004-005 interaction documented | **PASS** |
| Versioning | Version, effective date present on all clauses | **PASS** |
| Proxy | CRED-INTENT-004-005 dedicated proxy clause; fairness-through-unawareness explicitly rejected | **PASS** |
| Proxy | Lawful processing basis for bias testing data cited (EU AI Act Article 10(5)) | **PASS** |

### Example B — Specification Corpus Entries (CRED-DATA-001 through 005)

| Dimension | Check | Result |
|---|---|---|
| RFC 8174 | `normative-basis: MUST NOT` field on all entries | **PASS** |
| RFC 8174 | `conformance-role: credit-assessment-agent` on all entries | **PASS** |
| Atomicity | Each entry's `obligation` field: one verb, one subject, one condition | **PASS** |
| Atomicity | Rationale in intent clause (via `derived-from`), not embedded in obligation | **PASS** |
| Testability | `validation` block: single `check` per entry, `binary-pass-fail` result | **PASS** |
| Testability | `test-cases` block: positive, negative, and edge case per entry | **PASS** |
| Completeness | `definitions` block on CRED-DATA-005 defines all domain terms | **PASS** |
| Completeness | `known-gaps` block documents embedding architecture gap | **PASS** |
| Traceability | `derived-from.intent-clause` links to manifest clause ID | **PASS** |
| Traceability | `audit.log-fields` includes specification-id, version, agent-id | **PASS** |
| Conflict Freedom | `conflicts-with` block on CRED-DATA-005 documents CRED-DATA-002 interaction | **PASS** |
| Conflict Freedom | Precedence rule stated: lex specialis, CRED-DATA-005 governs | **PASS** |
| Versioning | Semantic version; `breaking-change` boolean; `changelog` with author and approver | **PASS** |
| Versioning | `retention-period` in audit block (7 years, FCA requirement) | **PASS** |
| Proxy | CRED-DATA-005 entry: proxy-analysis-clearance validation, LDAA pathway, stale-analysis test | **PASS** |
| Proxy | Lawful processing basis for special-category data in bias detection stated | **PASS** |

---

## What Changed from the Original Examples

Earlier versions of this framework's specification examples contained a single intent manifest clause and a single corpus entry governing the full set of data-use prohibitions. The table below documents every gap the original examples had and how the corrected examples address it.

| Gap | Where in Original | How Corrected |
|---|---|---|
| Bundled obligations (multiple MUST NOTs in one clause) | Original single intent clause | Split into five atomic clauses (CRED-INTENT-004-001 through -005), one prohibition each |
| No proxy discrimination clause | Original set | CRED-INTENT-004-005 and CRED-DATA-005 added — the most consequential addition |
| "Fairness through unawareness" implicit assumption | Original prohibited explicit fields only | CRED-INTENT-004-005 explicitly rejects this: removing fields does not prevent proxy discrimination |
| No mutual-information or adversarial-AUC thresholds | Original had no quantitative proxy test | CRED-DATA-005 specifies MI > 0.05 and AUC > 0.65 as proxy-feature thresholds |
| No LDAA (less-discriminatory-alternative analysis) pathway | Original had no remediation path for correlated features | CRED-DATA-005 defines the LDAA pathway: correlated features may be retained with documented LDAA |
| Missing `derived-from` field | Original corpus entry | `derived-from.intent-clause` required on all entries |
| Missing `regulatory-basis` per entry | Original had no regulatory references | `derived-from.regulatory-basis` with specific Acts and articles on all entries |
| No `conflicts-with` field | Original had no conflict documentation | CRED-DATA-005 documents interaction with CRED-DATA-002 and states lex specialis resolution |
| No `known-gaps` block | Original had no gap documentation | CRED-DATA-005 documents the embedding architecture gap as an open gap with owner and resolution target |
| `breaking-change` boolean absent | Original had no change classification | `versioning.breaking-change` boolean on all entries |
| Retention period absent from audit block | Original logged decisions without retention policy | `audit.retention-period: "7 years (FCA requirement)"` on all entries |
| No edge case test | Original had one test case per entry | Three test cases per entry: positive, negative, edge (including stale analysis) |
| EU AI Act Article 10(5) not cited | Original had no special-category data processing basis | Cited in CRED-INTENT-004-005 and CRED-DATA-005 as the lawful basis for using special-category data in bias testing |

---

*Continue to: [Specification Corpus Architecture](./specification-corpus.md) · [Requirements Specification Templates](./requirements-spec-templates.md)*  
*Back to: [Specification Quality Standard](../00-foundations/specification-quality-standard.md)*
