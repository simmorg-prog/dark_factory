# AI Engineering Maturity
## A Six-Stage Framework for Engineering Workflow

*From Prompt Engineering to Environment Engineering*  
*Actors: Humans · Agents · Agent Councils*  
*Stages 4–6 constitute the Dark Factory — where agents own the workflow*

May 2026

---

## Introduction: The Maturity Stack

This framework describes how engineering workflow evolves as AI capability and organisational maturity increase. Unlike replacement models — where one paradigm supersedes the last — this is a **cumulative stack**: each stage presupposes and subsumes the disciplines below it.

The six stages map onto an extended CMMI model, adapted for the AI era. The critical transition occurs between Stage 3 and Stage 4: the entry into what we call the **Dark Factory** — the operational mode where humans provide requirements and intent, and agents own the full engineering workflow.

---

## The Dark Factory Concept

In manufacturing, the "dark factory" describes a fully automated production floor that operates without human presence — lights-off, machines running. Applied to software engineering, the Dark Factory describes an agentic workflow environment where:

- Humans produce requirements, intent boundaries, and environment specifications
- All design, implementation, testing, review, and deployment is agent-operated
- Agent Councils govern workflow domains and self-organise for each task
- Human involvement is exception-based, not process-based

> **⬛ DARK FACTORY ZONE ⬛**  
> Stages 4–6: Humans produce requirements only. Agents own the workflow.

---

## Three Actor Types

| Actor | Description |
|---|---|
| **Human** | The engineer, architect, product owner, or stakeholder. Role shifts from maker → reviewer → governor → architect across the maturity curve. |
| **Agent** | An AI agent with persistent state, tool access, and task autonomy. Role shifts from oracle → executor → decision-maker → environment navigator across the maturity curve. |
| **Agent Council** | A structured collective of specialist agents that deliberate, coordinate, and govern a domain of the workflow. Composition evolves from informal pipeline → deliberation council → self-constituting governance body → environment steward across the maturity curve. |

---

## Stage 1: Prompt Engineering
*The Craft Era · CMMI Level 1 — Initial*  
*Human-led, ad hoc, artisanal*

### Definition

The foundational discipline of AI-assisted engineering. Engineers craft natural language instructions to elicit useful outputs from a model. All intelligence about task, context, and intent lives in the human's head and is transcribed into a prompt. Outputs are evaluated manually and iteration is manual.

### Engineering Workflow

| Workflow Stage | Description |
|---|---|
| Requirements | Captured in natural language by a human engineer or BA |
| Design | Engineer prompts the model for design options; selects and edits manually |
| Implementation | Engineer uses model to generate code snippets; assembles manually |
| Test | Manual testing; engineer may prompt for test cases but runs them manually |
| Review | Peer review by humans; model consulted ad hoc for feedback |
| Deploy | Manual deployment pipelines; humans control all gates |

### Actors

| Actor | Role in this Stage |
|---|---|
| Human Engineer | Sole driver. Writes prompts, evaluates outputs, edits, decides. The model is a sophisticated autocomplete. |
| Agent | None formally. The LLM is invoked as a stateless oracle — no memory, no tool use, no autonomy. |
| Agent Council | Not present. |

### Key Artefacts

- Prompt scripts (informal, personal, undocumented)
- Model outputs (raw, manually curated)
- Hand-edited code / documents
- Personal prompt libraries (notebooks, text files)
- No structured artefact governance

> **⚠ Stage Risk:** Entirely person-dependent. Knowledge is non-transferable. No repeatability or auditability.

---

## Stage 2: Context Engineering
*The Systems Era · CMMI Level 2 — Managed*  
*Human-designed, agent-assisted, process-aware*

### Definition

Engineering teams move beyond prompt craft to systematically manage what information the model sees at each step. RAG pipelines, retrieval systems, and structured context windows are engineered deliberately. Agents begin to appear as persistent workers within bounded, human-designed workflows.

### Engineering Workflow

| Workflow Stage | Description |
|---|---|
| Requirements | Human-authored, but stored in structured systems (Jira, Confluence) that agents can retrieve from |
| Design | Agent retrieves relevant prior designs, standards docs, and constraints; human makes final design decisions |
| Implementation | Coding agents generate code with injected codebase context; humans review and merge |
| Test | Agents generate and run unit tests; humans review coverage and edge cases |
| Review | Agents perform static analysis and first-pass code review; humans do final approval |
| Deploy | Semi-automated pipelines; humans approve deployment gates |

### Actors

| Actor | Role in this Stage |
|---|---|
| Human Engineer | Designs the context architecture. Decides what information is retrieved and when. Reviews and approves agent outputs. |
| Agent | Executes bounded tasks with engineered context: coding, testing, documentation, search. Operates within a single session or workflow step. |
| Agent Council | Informal — multiple agents may exist in a pipeline but without formal coordination protocols. |

### Key Artefacts

- Context schemas (what gets injected at each workflow step)
- RAG / retrieval pipeline configurations
- Structured requirements documents (machine-readable)
- Agent-generated code with human review records
- Test suites (agent-generated, human-approved)
- Context quality logs (relevance, retrieval hit rates)

> **⚠ Stage Risk:** Context rot, retrieval failure, schema drift. Systems work in dev but degrade in production without sensors.

---

## Stage 3: Intent Engineering
*The Strategy Era · CMMI Level 3 — Defined*  
*Org-goals encoded, agent-directed, human-governed*

### Definition

Organisational goals, values, trade-off hierarchies, and strategic priorities are encoded into agent infrastructure — not just prompts. Agents act with awareness of business intent, not just task instructions. Humans shift from doing to governing: defining intent, reviewing decisions, and resolving conflicts agents cannot arbitrate.

### Engineering Workflow

| Workflow Stage | Description |
|---|---|
| Requirements | Humans define business intent and high-level acceptance criteria. Agents decompose into structured, traceable sub-requirements. |
| Design | Agent Council proposes architecture options scored against encoded intent (cost, speed, risk tolerance). Human approves strategic direction. |
| Implementation | Agents implement autonomously within intent guardrails. Human reviews strategic decisions only. |
| Test | Agents execute full test suites including intent-alignment checks (does this feature serve the stated goal?). |
| Review | Automated review for compliance with encoded intent. Human review reserved for intent conflicts and novel risk. |
| Deploy | Agents manage deployment with intent-aware rollout strategies (e.g. risk tolerance defines canary %). Human approves. |

### Actors

| Actor | Role in this Stage |
|---|---|
| Human Engineer | Intent author and governor. Encodes organisational goals, resolves trade-off conflicts, approves major decisions. Moves from maker to strategist. |
| Agent | Executes within intent constraints. Can decline or escalate actions that conflict with encoded organisational values. |
| Agent Council | Formally constituted. Multiple specialist agents (architecture, security, performance, compliance) deliberate and propose. A coordinator agent synthesises recommendations for human review. |

### Key Artefacts

- Intent manifests (machine-readable org goals and trade-off hierarchies)
- Agent Council deliberation logs
- Intent-annotated design documents
- Automated intent-alignment test reports
- Escalation records (where agents flagged intent conflicts)
- Human decision records (why intent was overridden or confirmed)

> **⚠ Stage Risk:** Intent drift — encoded goals become stale as strategy evolves. Agents optimise for outdated intent without detection.

---

> **⬛ DARK FACTORY ZONE ⬛**  
> Stages 4–6: Humans produce requirements only. Agents own the workflow.

---

## Stage 4: Specification Engineering
*The Governance Era — Dark Factory Begins · CMMI Level 4 — Quantitatively Managed*  
*Policy-as-code, auditable, humans provide requirements only*

### Definition

All corporate policies, compliance frameworks, brand standards, security controls, and operational rules are converted into machine-readable specifications that agents can consume, enforce, and audit against. Humans are now primarily requirements authors. The engineering workflow from design through deployment is agent-operated. This is the entry point of the Dark Factory.

### Engineering Workflow

| Workflow Stage | Description |
|---|---|
| Requirements | 👤 **HUMAN ZONE:** Business stakeholders and architects author requirements in structured natural language. This is the primary human contribution. |
| Design | ⬛ **DARK FACTORY:** Agent Council auto-generates architecture, validated against specification corpus. No human in the loop unless spec conflict is unresolvable. |
| Implementation | ⬛ **DARK FACTORY:** Agents implement, self-review against specs, and iterate autonomously. Human not involved. |
| Test | ⬛ **DARK FACTORY:** Agents run full regression, security, performance, and spec-compliance suites. Results logged for audit. |
| Review | ⬛ **DARK FACTORY:** Specification-compliant output is auto-approved. Violations trigger human escalation with full evidence package. |
| Deploy | ⬛ **DARK FACTORY:** Agents execute deployment within specification-defined risk envelopes. Humans receive summary reports. |

### Actors

| Actor | Role in this Stage |
|---|---|
| Human | Requirements author and specification curator. Reviews escalations. Does not touch design, code, tests, or deployment. |
| Agent | Autonomous executor within specification bounds. Implements, tests, and deploys without human involvement per workflow step. |
| Agent Council | Governs the dark factory. Specialist councils (Architecture Council, Security Council, Compliance Council, Deployment Council) own their workflow domains. A Meta-Council arbitrates cross-domain conflicts. |

### Key Artefacts

- Specification corpus (machine-readable policies, standards, compliance rules)
- Requirements documents (human-authored, structured)
- Auto-generated architecture decision records (ADRs)
- Agent implementation logs with spec-compliance traces
- Automated audit trails (every decision linked to a spec)
- Escalation packages (evidence bundles sent to humans when spec conflict occurs)
- Deployment manifests (auto-generated, spec-validated)

> **⚠ Stage Risk:** Specification completeness gaps — agents comply with specs but specs don't cover novel situations. Brittle governance at the edges.

---

## Stage 5: Harness Engineering
*The Operational Era — Deep Dark Factory · CMMI Level 5 — Optimising*  
*Self-monitoring, adaptive, resilient, humans provide intent only*

### Definition

The agent system becomes a self-monitoring, self-correcting operational environment. The harness — the runtime envelope of tool dispatch, state management, observability, safety enforcement, and failure recovery — is engineered as a first-class system. Humans provide high-level requirements and intent boundaries. The dark factory monitors itself, detects drift, and adapts.

### Engineering Workflow

| Workflow Stage | Description |
|---|---|
| Requirements | 👤 **HUMAN ZONE:** Humans author requirements and define intent boundaries. All else is automated. |
| Design | ⬛ **DARK FACTORY:** Harness selects and assembles agent configurations for the task. Architecture is generated and validated against live telemetry from prior runs. |
| Implementation | ⬛ **DARK FACTORY:** Agents implement in parallel streams. Harness monitors context quality, detects drift, and re-routes or restarts failing agents. |
| Test | ⬛ **DARK FACTORY:** Harness orchestrates continuous testing. Failure signals trigger autonomous root-cause analysis and remediation cycles. |
| Review | ⬛ **DARK FACTORY:** Harness performs behavioural review — comparing outputs against intent, spec, and historical baselines. Anomalies trigger deep audit. |
| Deploy | ⬛ **DARK FACTORY:** Harness manages progressive deployment, monitors signals in real time, and auto-rolls back on drift detection. Human notified, not involved. |

### Actors

| Actor | Role in this Stage |
|---|---|
| Human | Strategic requirements author. Defines intent boundaries and escalation thresholds. Receives exception reports only. |
| Agent | Harness-managed executor. Operates within monitored, constrained environments. Can be paused, re-routed, or replaced by the harness mid-task. |
| Agent Council | Self-constituting. The harness dynamically assembles the right council composition for each task type, drawing from a registry of specialised agents. Councils self-evaluate and report health metrics. |

### Key Artefacts

- Harness configuration (runtime envelope specifications)
- Live telemetry dashboards (context quality, agent health, drift signals)
- Automated root-cause analysis reports
- Self-healing event logs (what failed, what the harness did, outcome)
- Progressive deployment manifests with live rollback records
- Behavioural baselines (what normal looks like, updated continuously)
- Exception reports to humans (pre-packaged, decision-ready)

> **⚠ Stage Risk:** Harness monoculture — over-reliance on harness assumptions that break at the system boundary. Observability gaps in novel failure modes not seen in training data.

---

## Stage 6: Environment Engineering
*The Transcendent Era — The Intelligent Enterprise · CMMI Level 6 — Transcending*  
*AI-native infrastructure, humans design the world agents operate in*

### Definition

The organisation stops adapting agents to work around legacy infrastructure and instead re-architects the environment itself to be inherently legible, navigable, and safe for AI. APIs, codebases, data models, knowledge bases, and organisational processes are redesigned as first-class AI-native environments. Humans are environment architects — designing the world, not the work.

### Engineering Workflow

| Workflow Stage | Description |
|---|---|
| Requirements | 👤 **HUMAN ZONE:** Humans define outcomes and constraints at environment level — what the system must achieve and what it must never do. Implementation is fully delegated. |
| Design | ⬛ **DARK FACTORY:** Agents design solutions natively within an AI-legible architecture. No reverse-engineering of legacy systems. Environment provides clean contracts. |
| Implementation | ⬛ **DARK FACTORY:** Agents implement against well-structured, AI-native APIs and data models. Ambiguity is an environment defect, not a prompt problem. |
| Test | ⬛ **DARK FACTORY:** Environment provides built-in test oracles and formal verification surfaces. Testing is structural, not sample-based. |
| Review | ⬛ **DARK FACTORY:** Environment enforces correctness by construction. Review is verification of environment contract compliance, not opinion. |
| Deploy | ⬛ **DARK FACTORY:** Deployment is a property of the environment — agents publish to AI-native runtime surfaces. No manual pipeline management. |

### Actors

| Actor | Role in this Stage |
|---|---|
| Human | Environment architect. Defines the shape of the world agents operate in: data contracts, API semantics, capability boundaries, ethical envelopes. Does not direct individual engineering tasks. |
| Agent | Environment-native executor. Works fluently within an AI-designed infrastructure. Errors are surfaced as environment signals, not prompt failures. |
| Agent Council | Environment stewards. Councils govern environment health, detect environment drift (when the real world diverges from the model), and propose environment evolution. Includes an Environment Council that proposes infrastructure changes to humans for approval. |

### Key Artefacts

- Environment maps (machine-readable models of the operational landscape)
- AI-native API contracts (formal, unambiguous, versioned)
- Data legibility standards (how data must be structured for agent consumption)
- Environment health reports (are the surfaces agents work on still accurate?)
- Capability boundary documents (what agents may and may not affect)
- Environment evolution proposals (from Agent Council to humans)
- Outcome verification records (did the environment produce the intended result?)

> **⚠ Stage Risk:** Environment ossification — AI-native environments become new legacy over time. The organisation must continuously evolve the environment itself or create a new class of technical debt at the infrastructure level.

---

## Summary Matrix

| Stage | CMMI Level | Human Role | Agent Role | Council Role | Primary Artefact |
|---|---|---|---|---|---|
| 1 — Prompt Eng. | Initial | Sole operator | None (oracle) | None | Prompt scripts & curated outputs |
| 2 — Context Eng. | Managed | System designer & reviewer | Bounded task executor | Informal pipeline | Context schemas, RAG configs, test suites |
| 3 — Intent Eng. | Defined | Intent author & governor | Intent-aware executor | Deliberation council | Intent manifests, ADRs, escalation logs |
| 4 — Spec. Eng. | Quant. Managed | Requirements author only | Autonomous within specs | Domain councils (Arch, Sec, Compliance) | Spec corpus, audit trails, escalation packages |
| 5 — Harness Eng. | Optimising | Exception approver only | Harness-managed executor | Self-constituting councils | Telemetry, self-healing logs, baselines |
| 6 — Env. Eng. | Transcending | Environment architect | Environment-native executor | Environment steward council | Environment maps, AI-native API contracts |
