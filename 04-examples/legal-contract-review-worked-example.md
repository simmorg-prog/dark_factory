# Worked Example: Legal Contract Review at Each Stage

*E6-07 · Wave 6 — Examples · Audience: Business Leaders, Legal*

> See also: [Enterprise Knowledge Work Map](../05-strategy/enterprise-knowledge-work-map.md) · [Stage Transition Playbooks](../03-stages/stage-transition-playbooks.md) · [Specification Quality Standard](../00-foundations/specification-quality-standard.md)

---

## Overview

Contract review is among the most knowledge-intensive activities in enterprise operations. A lawyer reviewing a commercial contract exercises domain expertise accumulated over years — understanding precedent, jurisdiction, clause interplay, negotiating norms, and organisational risk appetite. It is exactly the kind of work that historically resisted automation.

That resistance is eroding. Not because AI has become a lawyer, but because the maturity framework makes it possible to encode the principles that govern contract review precisely enough for agents to apply them consistently and safely.

This worked example traces commercial contract review through all six maturity stages. The contracts reviewed are the same type at every stage: inbound vendor agreements for SaaS services. What changes is who reviews them, what governance exists, and how consistently the organisation's legal positions are applied.

---

## The Review Process

A standard commercial SaaS contract review covers:

1. **Liability and indemnification** — uncapped liability, mutual vs. one-sided indemnities, consequential damages exclusions
2. **Data processing and privacy** — data processing agreement requirements, subprocessor obligations, UK/EU GDPR alignment
3. **Intellectual property** — ownership of customer data, work product, AI-generated outputs, licence scope
4. **Service levels and remedies** — SLA commitments, credit mechanisms, termination triggers
5. **Term and termination** — lock-in periods, auto-renewal traps, termination-for-convenience rights
6. **Governing law and dispute resolution** — jurisdiction, applicable law, arbitration vs. litigation

---

## Stage 1 — Prompt Engineering

### How the work gets done

A lawyer or contract manager reviews each contract manually, using a language model for specific assistance: drafting a redline comment, suggesting alternative clause language, checking whether a formulation is standard market practice.

The model assists with discrete tasks. It does not review the contract in a principled, consistent way — that is the lawyer's job. The lawyer's judgement, experience, and interpretation of the organisation's risk appetite govern the review.

**Typical Stage 1 activities:**
- Lawyer pastes a liability clause into a prompt and asks whether it is favourable to the buyer
- Contract manager asks the model to draft redline language for a termination-for-convenience clause
- Lawyer uses the model to check whether a data processing addendum meets GDPR minimum requirements

**The review timeline:** Same as pre-AI. Individual productivity may be marginally better. Consistency across reviewers and over time is no better than before.

**Key risk:** The organisation's legal positions are in lawyers' heads, not in a shared system. Different lawyers apply different standards. No governance exists over how AI is used in the review process. What constitutes an acceptable liability cap depends on who is doing the review that day.

---

## Stage 2 — Context Engineering

### How the work gets done

Context-aware agents assist with structured review tasks. The organisation's standard contract positions — the playbook — are structured and fed into agent context pipelines, along with the previous contracts executed with the counterparty, the organisation's risk register for this vendor category, and the relevant jurisdiction's legal framework.

Agents can perform first-pass review against structured checklists: identifying clauses that deviate from standard positions, flagging missing provisions, and producing a structured issues list for lawyer review. The lawyer reviews the agent's output rather than the raw contract.

**What agents handle at Stage 2:**
- Clause-by-clause comparison against the standard positions playbook
- Identification of clauses that are absent from the contract but required by the playbook
- Flagging of liability caps, limitation of liability exclusions, and indemnification scope
- Draft redline language for identified issues, based on playbook standard positions

**What humans handle:**
- Review of the agent's issues list
- Assessment of whether each flagged issue is material in context
- Negotiation strategy — which positions to hold, which to concede
- Final sign-off on execution

**The review timeline:** Faster for standard contracts. The initial issues identification, which previously took a lawyer several hours, takes the agent minutes. Lawyer time is concentrated on the issues list rather than the raw contract.

**Key risk:** Playbook currency. If the standard positions document has not been updated following a regulatory change (e.g., a new UK data protection standard, a change in market practice on AI IP ownership), the agent's first-pass review will flag issues against outdated positions. The lawyer must know the playbook's limitations and compensate for them — which partly defeats the benefit.

---

## Stage 3 — Intent Engineering

### How the work gets done

Intent-aware agents review contracts against encoded organisational legal intent. The intent manifest encodes the organisation's legal positions with enough precision that agents can make principled decisions about clause acceptability — not just flag deviations from a template, but assess whether a specific formulation advances or undermines the organisation's interests.

The intent manifest for contract review covers:

| Intent area | Encoded guidance |
|---|---|
| Liability cap | Our standard position: 12 months of fees. We SHOULD NOT accept caps below 6 months. We MUST NOT accept uncapped liability for direct damages |
| Data processing | The vendor MUST execute our standard DPA template or provide a substantially equivalent alternative reviewed by Data Protection. No DPA = no execution |
| IP ownership | We MUST retain ownership of all customer data. We MUST NOT grant vendor rights to use our data to train AI models without explicit opt-in |
| Governing law | We SHOULD insist on English law. We MAY accept New York law for US counterparties with mutual agreement. We MUST NOT accept jurisdictions without mutual enforcement treaty |
| Auto-renewal | We MUST NOT accept auto-renewal with notice periods exceeding 30 days |

Agents apply these rules in context — they are not just checking whether a field matches a template; they are assessing whether the counterparty's language achieves the required legal outcome by a different route.

**What agents handle at Stage 3:**
- Full first-pass review against encoded intent
- Issues list with severity classification (must resolve, should resolve, low risk)
- Proposed redline language that achieves the intent in counterparty's drafting style
- Escalation of situations the intent manifest does not cover

**What lawyers handle:**
- Review of agent issues list — focus on "must resolve" items
- Negotiation strategy
- Novel clause types not covered by the manifest
- Execution sign-off

**The close rate:** Standard vendor contracts are reviewed, redlined, and sent back within hours rather than days.

---

## Stage 4 — Specification Engineering

### How the work gets done

Autonomous agents review and redline standard commercial contracts. The specification corpus contains machine-enforceable rules governing every standard decision class in commercial contract review. Agents produce reviewed, redlined contracts without human involvement for contracts within the corpus scope.

The in-house legal team's role shifts to: corpus governance, escalation response, and strategic legal matters that fall outside the corpus (M&A, litigation, novel contract structures).

**The specification corpus for contract review:**

Each corpus entry covers a specific clause type and decision class. Example:

```yaml
id: LEGAL-SPEC-012
version: "2.1.0"
derived-from: LEGAL-INTENT-LIAB-001
normative-basis:
  keyword: MUST NOT
  conformance-role: "contract-review-agent"

scope:
  contract-type: ["SaaS", "professional-services", "data-processing"]
  clause-type: liability-cap

validation:
  check: >
    liability_cap_amount >= contract_annual_value * 0.5
    AND cap_excludes_gross_negligence == true
    AND cap_excludes_wilful_misconduct == true
  operator: all_true
  expected: true

action-on-violation:
  type: redline
  redline-template: LEGAL-TEMPLATE-LIAB-012
  escalation-trigger: "If counterparty resists standard redline on second exchange, escalate to Legal"

test-cases:
  - id: LEGAL-SPEC-012-T01
    input:
      liability_cap_amount: 120000
      contract_annual_value: 120000
      cap_excludes_gross_negligence: true
      cap_excludes_wilful_misconduct: true
    expected-outcome: pass
  - id: LEGAL-SPEC-012-T02
    input:
      liability_cap_amount: 50000
      contract_annual_value: 120000
      cap_excludes_gross_negligence: false
    expected-outcome: redline-required
```

**What agents own at Stage 4:**
- First-pass review and redline of all standard contracts within corpus scope
- Issues classification and negotiation prioritisation
- Tracking of counterparty responses and escalation when standard redlines are rejected
- Audit trail for every review decision — which corpus entry governed each redline

**What lawyers own:**
- Corpus governance — reviewing and approving corpus entries
- Escalation responses — decisions on non-standard positions
- Novel contracts outside corpus scope
- Matter strategy for complex negotiations

**The review timeline:** Standard contracts reviewed and redlined within the same business day of receipt. Backlog of pending vendor contracts, previously measured in weeks, eliminated.

**The governance requirement:** Every corpus entry governing a legal position must be reviewed by a qualified lawyer before admission. The legal function cannot be removed from corpus governance — only from the operational review loop.

---

## Stage 5 — Harness Engineering

### How the work gets done

The harness monitors the contract review pipeline. It tracks: review completion rates, escalation patterns by clause type, corpus coverage for the current contract mix, and counterparty acceptance rates on standard redlines.

**Signals that indicate corpus gaps:** A persistent escalation pattern on a specific clause type indicates the corpus does not cover that type adequately. The harness surfaces this pattern proactively — before lawyers discover it through accumulating escalation volume.

**Signals that indicate market evolution:** If counterparty acceptance rates on a standard redline position begin declining (from 85% to 65% over a quarter), this may indicate that market practice has shifted and the organisation's standard position is no longer within normal negotiating range. The harness detects this trend and flags it to the legal team for playbook review.

**MTTD in legal context:** A contract with a 5-business-day counterparty review window requires that harness anomalies be detected within the window. A harness failure that is not detected until day 6 cannot be remediated within the timeline. MTTD targets for legal review pipelines must align with contract execution timelines.

---

## Stage 6 — Environment Engineering

### How the work gets done

The legal environment has been redesigned for machine legibility:

**Machine-readable standard forms:** The organisation's standard contract forms are published in machine-readable structured format — each clause has a stable identifier, a version, and an explicit relationship to the corpus entries that govern it. Counterparties who submit deviations from the standard form are submitting structured deviations, not unstructured text, enabling exact clause-by-clause comparison.

**Counterparty contract analysis by structure:** The contract ingestion pipeline identifies clause types structurally rather than by natural language parsing. A liability limitation clause is identified as such regardless of how it is drafted — by its structural position in the agreement and its relationship to other provisions.

**Precedent management by contract:** The organisation's executed contract database is structured and queryable by clause terms. When a similar counterparty position arises, the agent can retrieve all precedents where similar language was accepted, what the negotiating history was, and what outcome resulted. This is legal knowledge as infrastructure.

**The legal environment at Stage 6:** The contract review process is faster, more consistent, and more legally defensible than at any earlier stage. The standard positions are embedded in the environment — they cannot be overridden without a conscious governance decision. Every review is auditable with full corpus traceability. The legal team's time is spent on genuinely strategic work: novel clause structures, high-stakes negotiations, and evolving the corpus as law and market practice develop.

---

## The Governance Stakes in Legal

Legal is the knowledge work domain where the specification precision requirement is highest. A specification defect in software engineering produces a bug. A specification defect in a legal corpus entry may produce a contractual commitment the organisation did not intend to make.

Consider the difference:

**Ambiguous corpus entry:** "The contract MUST include appropriate data protection provisions."

This cannot be machine-enforced. "Appropriate" is not a testable condition. An agent applying this rule will determine what is appropriate based on its training, not based on the organisation's legal position. Two contracts reviewed against this rule may receive different treatment. The audit trail records compliance with the rule but provides no evidence of what "appropriate" meant.

**Precise corpus entry:** "The contract MUST include a Data Processing Agreement executed against the organisation's standard DPA template (LEGAL-DPA-v3.2) or a Data Processing Agreement reviewed and approved by the Data Protection function (ref: LEGAL-DPA-EQUIV-PROCESS)."

This is testable. An agent can verify whether the DPA is present, which version it uses, and whether the equivalence review process has been completed. The audit trail is legally defensible.

The investment in writing the second version rather than the first is measured in minutes. The cost of a contractual misunderstanding arising from the first version may be measured in months of dispute resolution.

---

*Continue to: [Worked Example: Incident Response at Each Stage](./incident-response-worked-example.md)*  
*Back to: [Finance Month-End Close Worked Example](./finance-month-end-worked-example.md) · [Enterprise Knowledge Work Map](../05-strategy/enterprise-knowledge-work-map.md)*
