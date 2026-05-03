# Maturity Assessment — Instrument & Tool

*E5-01b · Wave 7 — Strategy · Audience: Technology Leaders, Architects*

> See also: [Assessment Framework Design](./maturity-assessment-framework.md) · [Maturity Curve](../00-foundations/maturity-curve.md)

---

## How to Conduct the Assessment

### Who should participate

A valid assessment requires perspectives from multiple functions. Assembling only the AI team produces a biased score — they are motivated to demonstrate maturity and may not be aware of practice gaps in domains they do not operate in.

Recommended participants:
- Technology leadership (CTO or equivalent) — technology decisions and roadmap
- Engineering leads for primary AI-enabled workflows — practice evidence
- Domain function heads for each in-scope knowledge work domain — practice evidence in their domain
- A governance or compliance lead — governance dimension scoring
- An external facilitator (if available) — challenge function for aspirational scoring

### Time required

- **Focused session:** 2–3 hours for a single domain (e.g., Software Engineering only)
- **Multi-domain assessment:** 1–2 weeks for a thorough cross-domain assessment with artefact review

The multi-domain assessment requires pre-work: collection of artefacts (prompt libraries, context schemas, intent manifests, corpus samples, harness dashboards) before the scoring sessions. Assessment sessions that attempt to score without reviewing artefacts produce unreliable results.

### The honest scoring rule

Score what is *consistently true*, not what is *sometimes true*, *aspirationally true*, or *true in a pilot*.

The observable evidence standard: if you cannot point to an artefact, a process with named ownership, or a metric with a defined baseline, score it as not present.

The specific failure pattern to avoid: scoring a practice based on intent rather than evidence. "We plan to implement context schemas this quarter" is not a Stage 2 practice indicator. "Here is the context schema for our primary workflow, here are the retention metrics showing it has been maintained for six months, and here is the person whose role includes maintaining it" is a Stage 2 practice indicator.

---

## The Assessment Questionnaire

Each question scores: **0 — Not present**, **1 — Partial** (exists in some areas, inconsistently, or without governance), **2 — Established** (consistently present, governed, and maintained).

---

### Stage 1 — Prompt Engineering

#### Technology Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| T1.1 | Do team members have access to a language model API or application? | | | |
| T1.2 | Is there tooling for storing and sharing prompts (version control, shared workspace)? | | | |

#### Practice Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| P1.1 | Is a shared prompt library maintained as a team asset (not individual notes)? | | | |
| P1.2 | Is there a review process for prompts used in consequential workflows? | | | |
| P1.3 | Do prompts include explicit scope and constraint boundaries? | | | |
| P1.4 | Can the team produce documentation for its most-used production prompts on request? | | | |

#### People Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| PE1.1 | Do team members understand what makes a prompt effective vs. ineffective? | | | |
| PE1.2 | Is prompt craft transferable — can multiple team members produce equivalent quality? | | | |

#### Governance Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| G1.1 | Is there an acceptable use policy defining what the model may and may not be used for? | | | |
| G1.2 | Is there clarity on what data categories may be shared with external model APIs? | | | |

---

### Stage 2 — Context Engineering

#### Technology Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| T2.1 | Is a retrieval pipeline (RAG, search, structured query) deployed and operational? | | | |
| T2.2 | Is a knowledge base or document store maintained for agent retrieval? | | | |
| T2.3 | Is retrieval quality measurement tooling in place (metrics dashboard)? | | | |

#### Practice Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| P2.1 | Are context schemas documented for primary workflows? | | | |
| P2.2 | Are retrieval quality metrics measured with a defined baseline? | | | |
| P2.3 | Are freshness SLAs defined for each major content category with named owners? | | | |
| P2.4 | Are context budgets (maximum context window allocation) defined and enforced? | | | |

#### People Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| PE2.1 | Do team members understand what context quality means and how to measure it? | | | |
| PE2.2 | Is there a named role accountable for knowledge base maintenance? | | | |

#### Governance Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| G2.1 | Is there governance over what third-party data sources can be used in context pipelines? | | | |
| G2.2 | Is context quality degradation visible and actioned before it affects agent outputs? | | | |

---

### Stage 3 — Intent Engineering

#### Technology Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| T3.1 | Is a system in place for storing and versioning the intent manifest? | | | |
| T3.2 | Is there tooling for agents to reference the intent manifest at decision points? | | | |

#### Practice Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| P3.1 | Is an intent manifest published and actively used by production agents? | | | |
| P3.2 | Can a specific agent decision be traced to a specific intent manifest clause? | | | |
| P3.3 | Has the intent manifest been updated in response to a strategy or policy change? | | | |
| P3.4 | Is intent drift detection operational — does the team review agent decision patterns against encoded intent? | | | |

#### People Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| PE3.1 | Is there a named owner with domain authority for the intent manifest? | | | |
| PE3.2 | Are intent clauses written in testable, specific language — not aspirational prose? | | | |

#### Governance Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| G3.1 | Is there a defined SLA for updating the intent manifest following a strategy change? | | | |
| G3.2 | Is intent manifest governance shared between engineering and business domain owners? | | | |

---

### Stage 4 — Specification Engineering

#### Technology Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| T4.1 | Is a machine-readable specification corpus deployed (OPA/Rego, structured YAML, OSCAL, or equivalent)? | | | |
| T4.2 | Is automated conflict detection operational on corpus updates? | | | |
| T4.3 | Is an audit trail infrastructure in place, logging corpus entry ID and version with each decision? | | | |
| T4.4 | Is an escalation package system deployed and operational? | | | |

#### Practice Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| P4.1 | Does ≥80% of the target workflow's decisions have corpus coverage (measured)? | | | |
| P4.2 | Are all five specification disciplines applied to all production corpus entries? | | | |
| P4.3 | Is specification gap rate measured and within a defined acceptable threshold? | | | |
| P4.4 | Has at least one escalation been resolved and converted to a corpus extension? | | | |

#### People Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| PE4.1 | Is there a named corpus owner responsible for quality and coverage? | | | |
| PE4.2 | Do the humans who receive escalation packages have training and practiced experience responding to them? | | | |

#### Governance Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| G4.1 | Is there a formal admission process for new corpus entries (quality review, conflict detection, approval)? | | | |
| G4.2 | Is the audit trail immutable and independently reviewable? | | | |
| G4.3 | Is there a change governance process for corpus updates with breaking-change classification? | | | |

---

### Stage 5 — Harness Engineering

#### Technology Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| T5.1 | Is a comprehensive harness deployed covering all production agents (not just infrastructure metrics)? | | | |
| T5.2 | Are behavioural baselines established and maintained for all production agents? | | | |
| T5.3 | Are self-healing playbooks deployed and operational? | | | |

#### Practice Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| P5.1 | Is MTTD measured and within defined target for three consecutive review periods? | | | |
| P5.2 | Has a self-healing playbook fired and resolved an anomaly autonomously? | | | |
| P5.3 | Are behavioural baselines reviewed and updated on a defined cadence? | | | |
| P5.4 | Is harness governance independent of the team that operates the agents it monitors? | | | |

#### People Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| PE5.1 | Is there a named harness operator accountable for performance metrics? | | | |
| PE5.2 | Do playbook owners review and approve their playbooks on a defined cadence? | | | |

#### Governance Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| G5.1 | Are harness performance metrics (MTTD, MTTR, false positive rate) reported to governance on defined cadence? | | | |
| G5.2 | Are self-healing playbooks formally approved before deployment? | | | |

---

### Stage 6 — Environment Engineering

#### Technology Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| T6.1 | Is an environment map published and maintained? | | | |
| T6.2 | Are machine-readable API contracts in place for ≥50% of agent-consumed APIs? | | | |
| T6.3 | Is environment health monitoring operational? | | | |

#### Practice Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| P6.1 | Is an Environment Council constituted with defined mandate and decision rights? | | | |
| P6.2 | Has at least one legacy system been redesigned for AI legibility with documented improvement? | | | |
| P6.3 | Is the environment map reviewed for accuracy on a defined cadence? | | | |
| P6.4 | Is a legacy redesign programme active with prioritised targets and defined timelines? | | | |

#### People Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| PE6.1 | Does the Environment Council include representatives from technology, governance, and business domains? | | | |
| PE6.2 | Are environment architects embedded in the teams making architectural decisions that affect AI legibility? | | | |

#### Governance Dimension

| # | Question | 0 | 1 | 2 |
|---|---|---|---|---|
| G6.1 | Does the Environment Council have blocking authority over system deployments that fail the legibility standard? | | | |
| G6.2 | Is environment health reported to governance on a defined cadence? | | | |

---

## Scoring Rubric

**Step 1 — Calculate dimension scores by stage.** For each stage, sum the scores in each dimension (Technology, Practice, People, Governance). The maximum score for each dimension at each stage varies by the number of questions; normalise to a percentage or a 0–2 average.

**Step 2 — Apply T-Score threshold.** For each stage, if the Technology dimension average is ≥1.5, the T-Score threshold is met at that stage.

**Step 3 — Apply P-Score threshold.** For each stage, if the Practice dimension average is ≥1.5, the P-Score threshold is met at that stage. (People and Governance contribute to P-Score alongside Practice dimension questions.)

**Step 4 — Determine Effective Stage.** The Effective Stage is the highest stage where both the T-Score threshold and the P-Score threshold are met.

**Step 5 — Calculate Maturity Debt.** Maturity Debt = (Highest stage with T-Score ≥ threshold) − Effective Stage.

**Step 6 — Produce the Domain Coverage Map.** Repeat Steps 1–5 for each assessed domain. Produce the matrix.

---

## The Output Format

A completed assessment produces:

**Executive Summary (one page)**
- Current Effective Stage per domain
- Maturity Debt summary — where gaps exist and what they mean operationally
- Top three priorities — the actions most likely to advance Effective Stage

**Domain Coverage Map**
The domain-stage matrix showing Effective Stage, T-Score, P-Score, and Maturity Debt for each assessed domain.

**Priority Actions by Domain**
For each domain, the specific practice indicators that are not yet met and the actions required to meet them, sequenced by impact on Effective Stage.

---

## Interpreting Results — Five Common Patterns

### Pattern 1 — The Over-Tooled Organisation

**Profile:** High T-Score, low P-Score across all domains. T-Score 4–5, P-Score 1–2 typical.

**What it means:** The organisation has invested heavily in AI infrastructure without developing the practice disciplines that make the infrastructure work. Specification management platforms, harness tooling, and vector databases are deployed. Prompt libraries are personal. Context schemas do not exist. Intent manifests are aspirational documents. The corpus, where it exists, is prose policy rather than machine-enforceable specification.

**Priority:** Stop buying tools. Begin developing practices. The next investment should be in practice development (training, facilitated workshops, dedicated practice leads) rather than additional technology.

### Pattern 2 — The Engineering Island

**Profile:** Software Engineering at Effective Stage 3–4. All other domains at Effective Stage 1.

**What it means:** Common in technology companies. Engineering has made the journey; the rest of the organisation has not. The risk is significant: the Dark Factory exists in engineering while governance, compliance, finance, and legal operate at Stage 1 — with no shared context, no common intent, and no coordinated governance.

**Priority:** Domain expansion. The engineering team's practices need to be shared with the highest-risk adjacent domains (compliance, legal, HR) before they are extended to lower-risk domains.

### Pattern 3 — The Governance Gap

**Profile:** Technology and practice scores reasonable. Governance dimension consistently scoring 0–1 across stages.

**What it means:** Agents are operating without adequate oversight infrastructure. Audit trails are incomplete. Corpus admission processes are informal. Harness independence is absent. The operational capability is present; the accountability infrastructure is not.

**Priority:** Governance catch-up before any further stage progression. This pattern carries the highest regulatory exposure.

### Pattern 4 — The Solid Foundation

**Profile:** Low Effective Stage but T-Score and P-Score in alignment. Maturity Debt = 0.

**What it means:** This is the healthiest starting position for organisations early in their journey. Stage 1 or 2, but genuinely established — practices are real, governance is appropriate for the stage, the foundation is solid. Progression is predictable and safe.

**Priority:** Planned stage progression. Begin Stage 2 or Stage 3 investment with confidence that the existing foundation will hold.

### Pattern 5 — The Fragile Advanced

**Profile:** High attempted stage (T-Score 4–5), high Maturity Debt (3+ layers), multiple domains.

**What it means:** The most dangerous pattern. Multiple layers of technology deployed without practice foundations. Autonomous operation is running on foundations that are not solid. The system appears functional until it encounters situations where the missing foundations matter — and in a high-throughput Dark Factory, those situations arrive frequently.

**Priority:** Deliberate remediation before further investment. The organisation must develop the practices of the lowest unsolid layer before adding further capability above it.

---

*Back to: [Assessment Framework Design](./maturity-assessment-framework.md) · [Maturity Curve](../00-foundations/maturity-curve.md)*
