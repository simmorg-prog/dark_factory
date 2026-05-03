# Worked Example: Feature Delivery at Each Stage

*E6-01 · Wave 6 — Examples · Audience: All*

> See also: [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md) · [Dark Factory Definition](../00-foundations/dark-factory.md) · [Specification Discipline](../00-foundations/specification-discipline.md)

---

## Overview

This worked example traces a single feature — Multi-Factor Authentication (MFA) — through all six stages of the AI Operational Maturity Framework. The feature is identical at every stage. What changes is how it is delivered, who does the work, how the work is governed, and — critically — the quality of the specifications that define it.

The specification quality progression is the most important thread in this example. The same requirement is written six times — once at each stage's quality standard. The difference between the Stage 1 version and the Stage 4 version is not stylistic. It is the difference between an intention and a machine-enforceable law. Understanding that progression — and why it matters — is the central purpose of this document.

The scenario: a financial services company is adding MFA to its customer authentication system. The feature must comply with PCI DSS requirements and internal security policy. At each stage of maturity, the work looks different, the human role is different, and the specification quality is different.

---

## Stage 1 — Prompt Engineering

### How the work gets done

A senior engineer handles the MFA implementation. They use a language model to assist with specific tasks: generating boilerplate code, writing test cases, reviewing their implementation for obvious errors. Each interaction is a fresh prompt; the engineer assembles context manually and evaluates outputs personally.

The process is personal and person-dependent. The engineer's prompt craft, security knowledge, and judgement drive quality. If a different engineer handles the next similar feature, the approach — and therefore the output quality — will differ.

**What the engineer does:**
- Writes prompts to generate TOTP library integration code
- Manually reviews all generated code against their mental model of the security requirements
- Writes tests by hand; uses the model to fill gaps
- Documents the implementation informally in the PR description

**Timeline:** Several days of iteration. The engineer is productive. The output is good. It is not repeatable by someone who did not do it.

### The specification at Stage 1

The acceptance criterion for the MFA feature at Stage 1:

> *"Users should be able to log in with MFA."*

This is the Stage 1 standard. It is a sentence, not a specification. Let us examine what it fails to define:

- Which users? All users, some users, new users only?
- Which MFA methods? TOTP, SMS OTP, hardware key?
- Under what conditions is MFA required vs. optional?
- What happens if MFA fails — lockout, fallback, alert?
- What does "log in" include — web only, API, mobile?
- What does "should" mean — mandatory or advisory?

A developer reading this criterion makes their own decisions about every open question. Two developers will make different decisions. An AI model asked to implement this specification will also make its own decisions — and will not flag that it has done so.

**The Stage 1 specification problem:** It expresses intent without obligation. It is aspirational rather than testable. It cannot be automatically verified. It produces inconsistent outcomes across different implementers.

---

## Stage 2 — Context Engineering

### How the work gets done

A context-aware agent assists with the MFA implementation. The engineer designs the workflow; the agent executes bounded tasks within it. The agent has access to the existing codebase, the security architecture documentation, the authentication service specifications, and the organisation's coding standards — all injected via a structured context pipeline.

The engineer's role shifts from writing code to reviewing agent outputs and making architectural decisions. The agent produces implementations; the engineer validates them against quality and security requirements.

**What changes from Stage 1:**
- The agent has structured access to relevant context — it does not rely on the engineer to include the right background in each prompt
- The same workflow produces consistent outputs regardless of which engineer runs it
- The engineer's time is spent on review and judgement rather than implementation

**What does not change:**
- The engineer reviews every agent output before it proceeds
- The specification of what MFA should do is still not precise enough for automated verification

### The specification at Stage 2

The acceptance criterion at Stage 2:

> *"The authentication service SHOULD support TOTP-based MFA for all users."*

Progress: an RFC 2119 keyword has appeared. But several problems remain.

**Missing RFC 8174 boilerplate.** Without the boilerplate declaration, SHOULD carries only its ordinary English meaning — a recommendation, not a normative requirement. A model enforcing this specification cannot distinguish normative SHOULDs from ordinary shoulds.

**Not atomic.** The clause bundles two distinct obligations: (1) support TOTP-based MFA, and (2) apply it to all users. These are independently verifiable and may have different implementation scopes. An atomic specification expresses exactly one obligation.

**No rationale for SHOULD.** RFC 8174 practice requires that SHOULDs be accompanied by an explicit rationale explaining why deviation is permitted. What circumstances permit an administrator to bypass this recommendation?

**No test cases.** The criterion cannot be automatically verified. There is no definition of what "support" means in a testable sense — does it mean the capability exists, that it is enabled, that it is enforced?

**The Stage 2 specification problem:** Better than Stage 1 — more specific, RFC 2119 vocabulary present — but not yet machine-enforceable, not atomic, and not testable.

---

## Stage 3 — Intent Engineering

### How the work gets done

Intent-aware agents handle the implementation workflow. The engineer has encoded MFA requirements in the intent manifest, giving agents principled guidance for the decisions that the task instruction alone cannot resolve: which MFA methods are acceptable, what compliance standard governs, how to handle edge cases.

The agent no longer infers these decisions from its training data or from contextual signals. It applies the manifest. When the manifest covers the question, the agent acts. When the manifest is silent, the agent escalates.

**What changes from Stage 2:**
- Agent decisions are consistent across sessions and across agents — all reference the same intent source
- The engineer is not consulted for every edge case — the manifest resolves most of them
- The requirement is authored as a formal intent manifest clause with RFC 8174 semantics

### The specification at Stage 3 — Intent Manifest Clause

RFC 8174 boilerplate declaration (appears once at the document header):

> The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all capitals, as shown here.

---

**CRED-AUTH-001 — Multi-Factor Authentication Requirement**

| Field | Value |
|---|---|
| Clause ID | CRED-AUTH-001 |
| Version | 1.0 |
| Conformance role | The authentication service |
| Obligation level | MUST |
| Jurisdiction | UK (PCI DSS v4.0 §8.4, FCA SYSC 13, UK GDPR Art. 32) |
| Temporal scope | All authentication events from 2026-06-01 |

**Obligation:**

The authentication service MUST require successful completion of a second authentication factor for all interactive login events before granting access to customer account data.

**Scope:**
- Applies to: all authentication pathways (web, mobile, API with delegated user context)
- Excluded: machine-to-machine API calls using service account credentials with certificate-based mutual TLS authentication — these are governed by CRED-AUTH-002

**Reasoning:**

PCI DSS v4.0 Requirement 8.4 mandates MFA for all non-console administrative access and all remote access to cardholder data environments. The FCA's SYSC 13 guidance requires appropriate authentication controls for systems processing customer financial data. Single-factor authentication is no longer considered adequate for these contexts given the prevalence of credential compromise. This clause encodes an absolute requirement rather than a recommendation because the regulatory and risk basis does not permit exceptions.

**Escalation trigger:**

The authentication service MUST escalate to the Security Governance function before implementing any authentication event that this clause does not cover.

---

**What changes from Stage 2:**
- The clause is atomic — one obligation, one conformance role
- The RFC 8174 boilerplate makes the MUST normative
- Scope and exclusions are explicit — no open questions
- Reasoning is included — agents and auditors can evaluate whether the clause applies to novel situations
- Escalation behaviour is defined — the agent knows what to do when the manifest is silent

**What the Stage 3 specification still cannot do:** It cannot be directly machine-enforced. An agent reads this clause and applies it as guidance. It cannot be parsed and validated automatically. That capability arrives at Stage 4.

---

## Stage 4 — Specification Engineering

### How the work gets done

Autonomous agents implement the MFA feature without human review of individual decisions. The specification corpus contains the rules governing authentication behaviour. Agents act within those rules; when they reach a decision the corpus does not cover, they escalate.

The engineer no longer reviews each implementation step. They govern the corpus — reviewing additions, maintaining the quality standard, responding to escalations. The implementation proceeds at agent speed: continuous, consistent, auditable.

**What changes from Stage 3:**
- No human in the operational loop for decisions the corpus covers
- Every agent decision logged with the corpus entry ID and version that governed it
- The specification is machine-enforceable — it is not advisory

### The specification at Stage 4 — Specification Corpus Entry

```yaml
id: AUTH-SPEC-001
version: "1.2.0"
breaking-change: false
changelog: "1.2.0 — Added FIDO2/WebAuthn to accepted method list. 1.1.0 — Clarified scope exclusion for mTLS service accounts. 1.0.0 — Initial."

derived-from: CRED-AUTH-001
normative-basis:
  keyword: MUST
  conformance-role: "authentication-service"

regulatory-basis:
  - standard: "PCI DSS v4.0"
    requirement: "8.4.2"
    note: "MFA for all non-console administrative access and remote access to CDE"
  - standard: "FCA SYSC"
    requirement: "13.9"
    note: "Appropriate authentication controls for financial data systems"
  - standard: "UK GDPR"
    article: "32"
    note: "Appropriate technical measures for security of processing"

scope:
  included:
    - "All interactive login events (web, mobile, OAuth delegation flows)"
  excluded:
    - "Machine-to-machine API calls using service-account credentials with mutual TLS — governed by AUTH-SPEC-002"

enforcement:
  mode: pre-action-validation
  action-on-violation: block
  escalation-target: security-governance-queue
  escalation-severity: high

validation:
  check: "second-factor-verified == true AND second-factor-method IN ['TOTP', 'FIDO2', 'WebAuthn']"
  operator: equals
  expected: true

test-cases:
  - id: AUTH-SPEC-001-T01
    description: "Positive — TOTP factor verified"
    input:
      login-event-type: interactive
      second-factor-provided: true
      second-factor-method: TOTP
      second-factor-verified: true
    expected-outcome: access-granted
  - id: AUTH-SPEC-001-T02
    description: "Negative — no second factor presented"
    input:
      login-event-type: interactive
      second-factor-provided: false
    expected-outcome: access-blocked
  - id: AUTH-SPEC-001-T03
    description: "Edge — SMS OTP attempted (not in accepted method list)"
    input:
      login-event-type: interactive
      second-factor-provided: true
      second-factor-method: SMS-OTP
      second-factor-verified: true
    expected-outcome: access-blocked
  - id: AUTH-SPEC-001-T04
    description: "Scope exclusion — mTLS service account, should pass without MFA"
    input:
      login-event-type: machine-to-machine
      credential-type: service-account-mtls
    expected-outcome: access-granted
    note: "Governed by AUTH-SPEC-002, not this entry"

audit:
  log-fields:
    - authentication-event-id
    - user-id
    - second-factor-method
    - second-factor-verified
    - corpus-entry-id
    - corpus-entry-version
    - decision-outcome
    - timestamp
  retention-period: "7 years (PCI DSS v4.0 §12.5.1)"

conflicts-with: []
known-gaps:
  - id: AUTH-SPEC-001-GAP-001
    description: "Behaviour undefined for users with accessibility-related MFA exemptions — escalate all such cases to Security Governance pending AUTH-SPEC-003"
    status: open
    owner: security-governance
```

**What changes from Stage 3:**
- Machine-parseable and machine-enforceable — the validation check is directly executable
- Test cases are co-located — they run in CI on every corpus update; a test failure prevents deployment
- Audit fields are defined — every decision is logged against specific fields with a defined retention period
- Known gaps are explicit — the corpus acknowledges what it does not yet cover and defines escalation behaviour for those cases
- Semantic versioning — breaking changes are flagged; agents can verify they are operating against the current version

---

## Stage 5 — Harness Engineering

### How the work gets done

The harness governs the authentication system continuously. AUTH-SPEC-001 is validated on every deployment via a harness pre-flight check — the deployment cannot proceed if the authentication service does not comply with the corpus entry. During operation, the harness monitors MFA compliance rate, second-factor method distribution, and escalation patterns.

The engineer's operational role has narrowed further. They govern the harness — reviewing its performance metrics, approving its self-healing playbooks, responding to escalations the harness cannot resolve autonomously.

**The harness pre-flight check for AUTH-SPEC-001:**

Before any authentication service deployment reaches production, the harness executes:

1. Load AUTH-SPEC-001 v1.2.0 from the specification corpus
2. Run AUTH-SPEC-001-T01 through T04 against the deployment candidate
3. Verify that the audit logging configuration includes all required fields at the defined retention period
4. Verify that the escalation routing for `security-governance-queue` is operational
5. Block deployment if any check fails; emit a structured failure report referencing the failing test case IDs

**Continuous monitoring:**

| Signal | Baseline | Alert threshold |
|---|---|---|
| MFA compliance rate | 99.97% | < 99.9% for 5 minutes |
| Escalation rate (MFA-related) | 0.01% of login events | > 0.1% for 15 minutes |
| SMS-OTP attempt rate | ~0% | > 0.5% — possible client app using deprecated method |
| Audit log completeness | 100% | < 100% for 1 minute |

**Self-healing playbook AUTH-HNS-004 — MFA compliance rate drop:**

Precondition: MFA compliance rate falls below 99.9% for 5 continuous minutes AND no deployment event in the last 30 minutes.

Actions:
1. Capture a sample of non-compliant login events (last 50)
2. Check for pattern — are they from a specific client version, geography, or user segment?
3. If pattern detected: flag to application engineering with structured anomaly report; increase sampling rate for affected segment
4. If no pattern detected: escalate to security governance as unclassified anomaly

Escalation trigger: compliance rate continues to fall after flagging; escalate immediately.

**What changes from Stage 4:**
- Compliance is not just specified and enforced — it is continuously measured
- Deployment is blocked if compliance cannot be verified — not by human review, by automated pre-flight
- Anomalies are detected proactively — before downstream harm occurs

---

## Stage 6 — Environment Engineering

### How the work gets done

At Stage 6, MFA compliance is not a specification to be enforced or a harness to be monitored. It is a property of the environment. The authentication environment contract makes non-MFA interactive authentication structurally impossible.

The authentication gateway — the single entry point for all interactive login events — is redesigned so that the second-factor verification step is not a validation check but a structural requirement in the authentication flow. The code path for granting access without a verified second factor does not exist. There is no branch to audit, no flag to check, no rule to enforce.

**The authentication environment contract:**

```yaml
contract-id: ENV-AUTH-CONTRACT-001
contract-type: authentication-gateway-interface
version: "2.0.0"

structural-guarantees:
  - id: ENV-AUTH-GUAR-001
    statement: >
      The interactive-login operation has no code path that produces an
      access-token without a verified second-factor-verification field
      in the authentication context. This is a structural guarantee,
      not a runtime check.
    verification: formal-proof
    proof-reference: auth-gateway-formal-proof-v2.0.0.pdf

  - id: ENV-AUTH-GUAR-002
    statement: >
      The accepted-methods registry is the only authoritative source of
      valid second-factor methods. The authentication gateway cannot
      accept a method not present in this registry. Registry updates
      require Environment Council approval.
    verification: static-analysis
    static-analysis-reference: auth-gateway-analysis-v2.0.0-sarif.json

runtime-checks-eliminated:
  - AUTH-SPEC-001
  - note: >
      AUTH-SPEC-001 remains in the specification corpus as the
      authoritative statement of intent. It is no longer enforced
      at runtime because the structural guarantee makes runtime
      enforcement redundant. The corpus entry is retained for
      audit and intent traceability.

corpus-relationship:
  derived-from-intent: CRED-AUTH-001
  supersedes-runtime-enforcement: AUTH-SPEC-001
  audit-note: >
    Agent decisions involving authentication are traceable to this
    environment contract rather than to AUTH-SPEC-001 runtime checks.
    Both references are valid for audit purposes.
```

**What changes from Stage 5:**
- MFA compliance cannot fail at runtime because it cannot be violated by construction
- The specification corpus retains AUTH-SPEC-001 as the authoritative statement of intent — but it is no longer the enforcement mechanism
- The harness monitoring of MFA compliance rate becomes a consistency check against the structural guarantee, not a primary safety mechanism
- Future authentication changes are governed by the Environment Council, not just by specification corpus update

**The significance of Stage 6:** The effort required to ensure MFA compliance drops to near zero, permanently. The specification corpus entry still exists. The harness still monitors. But neither is the primary safety mechanism. The environment is. This compounding effect — where each Stage 6 redesign eliminates a class of ongoing specification and monitoring overhead — is why Stage 6 produces increasing returns.

---

## The Specification Quality Progression — Summary

The most important thread across this worked example is not the operational changes — it is the quality of the specification at each stage.

| Stage | Specification | Key quality gap |
|---|---|---|
| 1 | "Users should be able to log in with MFA." | Not normative; not atomic; not testable; open questions on scope, method, conditions |
| 2 | "The authentication service SHOULD support TOTP-based MFA for all users." | No RFC 8174 boilerplate; not atomic (two obligations); no test cases; no rationale for SHOULD |
| 3 | Intent Manifest Clause CRED-AUTH-001 — RFC 8174, atomic, scoped, reasoned | Not machine-enforceable; requires agent interpretation |
| 4 | YAML Corpus Entry AUTH-SPEC-001 — machine-enforceable, atomic, test-co-located, audited | All dimensions met; runtime enforcement required |
| 5 | Harness pre-flight + continuous monitoring against AUTH-SPEC-001 | Compliance verified before deployment and monitored continuously |
| 6 | Environment Contract ENV-AUTH-CONTRACT-001 — structural guarantee | MFA compliance is a property of the environment; runtime enforcement eliminated |

The Stage 1 specification is not wrong because MFA is unimportant. It is wrong because it cannot be verified, cannot be consistently applied by different implementers, and cannot be enforced by agents at Stage 4. Every open question in the Stage 1 specification becomes a decision that someone makes — probably differently each time — or an assumption that the agent fills in with whatever its training suggests.

The cost of writing the Stage 1 specification more precisely is a sentence. The cost of discovering at Stage 4 that the specification corpus is built on ambiguous foundations is a specification corpus rewrite.

> **The Specification Debt Principle**  
> Ambiguity authored at Stage 1 does not disappear at Stage 4 — it becomes policy. Every poorly-authored requirement is a specification defect that compounds as it travels up the stack. At Stage 1 it produces a bad output. At Stage 2 it contaminates a retrieval pipeline. At Stage 3 it encodes a wrong goal. At Stage 4 it becomes law that agents enforce at production speed.

---

## What This Example Reveals

**The human role at each stage:**

| Stage | What the human does in this example |
|---|---|
| 1 | Writes the code (with model assistance); reviews everything personally |
| 2 | Designs the workflow; reviews all agent outputs |
| 3 | Authors the intent manifest; reviews agent decisions against it |
| 4 | Maintains the specification corpus; responds to escalations |
| 5 | Governs the harness; responds to anomalies the harness cannot resolve |
| 6 | Governs the environment architecture; approves structural changes |

**The compounding value of specification quality:**

The Stage 3 intent manifest clause took careful work to write. But it produced:
- A Stage 4 corpus entry that required no new intent authorship — only translation to machine-readable format
- A Stage 5 harness configuration that was derived directly from the corpus entry's test cases
- A Stage 6 environment contract that preserved the same intent in structural form

Good work at Stage 3 compounded forward. The reverse is also true: the ambiguous Stage 1 specification would have compounded backward — producing inconsistent Stage 2 context schemas, incomplete Stage 3 intent clauses, and a Stage 4 corpus entry with known-gaps that should have been prevented.

---

*Continue to: [The Stage 3→4 Transition in Detail](./stage-3-4-transition.md) · [Anti-Patterns Library](./anti-patterns.md)*  
*Back to: [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md) · [Specification Discipline](../00-foundations/specification-discipline.md)*
