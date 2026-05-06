# Context Engineering — Reference Document Catalogue
## Source materials for the AI Operational Maturity Framework (dark_factory)

**Purpose:** This document provides direct references to real, publicly available documents that exemplify Context, Intent, and Specification artefacts at each of the six stages of the maturity framework. Each entry includes the document name, author/organisation, URL, format, and the specific qualities that make it a high-fidelity example.

---

## Stage 1 — Prompt Engineering
*Context is inline. Intent is implicit in wording. Specification is absent.*

---

### S1-C1 — Context Document: GitHub "What is prompt engineering?" guide
**Type:** Context (Stage 1 — inline system prompt examples)  
**Author:** GitHub (Microsoft)  
**URL:** https://github.com/resources/articles/what-is-prompt-engineering  
**Format:** Web article with verbatim prompt examples  
**Last updated:** March 2026  

**What it demonstrates:**  
The canonical Stage 1 context document form: a system message as a block of natural language. The article provides worked examples of system prompts that define persona ("Act as a technical assistant..."), establish tone, and set formatting expectations — all inline, with no separation between context, intent, or specification. The document also shows the Stage 1 "few-shot" pattern explicitly: providing 2-3 input/output examples as the context mechanism. This is the most widely-read definition of Stage 1 artefact structure in the developer community, authored by the organisation that hosts the majority of the world's code.

**Key quotes for reference:**  
- "System prompts set the rules, boundaries, or persona that guide how the model behaves throughout an interaction."
- "Few-shot prompting includes a few examples to set context and show the desired output style."
- "Saving effective prompts as templates helps build repeatable patterns that others can reuse across your organisation."

---

### S1-C2 — Context Document: OpenAI Help Center "Best practices for prompt engineering"
**Type:** Context (Stage 1 — inline prompt patterns with verbatim examples)  
**Author:** OpenAI  
**URL:** https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api  
**Format:** Help article  

**What it demonstrates:**  
The definitive Stage 1 reference from the organisation that created the dominant LLM API. Shows system prompts as raw text constraints: "The following is a conversation between an Agent and a Customer. DO NOT ASK USERNAME OR PASSWORD." This is the archetypal Stage 1 intent-as-instruction pattern — intent is fully embedded in the constraint text, not separated as a document. Also demonstrates the "show don't tell" principle through before/after prompt comparisons.

---

### S1-C3 — Context Document: Andrej Karpathy CLAUDE.md (Karpathy behavioural guidelines)
**Type:** Context (Stage 1→2 boundary — behavioural guidelines derived from practitioner experience)  
**Author:** Andrej Karpathy / forrestchang (GitHub)  
**URL:** https://github.com/forrestchang/andrej-karpathy-skills/blob/main/CLAUDE.md  
**Format:** Markdown, single file  

**What it demonstrates:**  
A distillation of Karpathy's publicly stated observations on LLM coding pitfalls, formatted as a CLAUDE.md. Represents the transition moment between Stage 1 (inline prompt) and Stage 2 (managed context document). Key patterns: "Don't assume. Don't hide confusion. Surface tradeoffs." and "Minimum code that solves the problem. Nothing speculative." Useful as the simplest possible Stage 2 context document — the point where practitioners first start externalising behavioural intent into a file rather than an inline prompt.

---

## Stage 2 — Context Engineering
*Context is a designed, versioned document. Intent starts to separate. Specification is soft.*

---

### S2-C1 — Context Document: shanraisshan/claude-code-best-practice CLAUDE.md ⭐ PRIMARY
**Type:** Context (Stage 2 — structured project context document)  
**Author:** Shan Raisshan (community, 21.1k GitHub stars)  
**URL:** https://github.com/shanraisshan/claude-code-best-practice/blob/main/CLAUDE.md  
**Format:** Markdown, 114 lines, 6.6KB  
**Stars:** 21,100 | Forks: 1,800  

**What it demonstrates:**  
The most widely-referenced Stage 2 context document template in the Claude Code ecosystem. Demonstrates the Command → Agent → Skill architecture as the structural context framework. Contains: repository overview (what this project is), key component descriptions, skill definition structure with YAML frontmatter fields (name, description, argument-hint, allowed-tools), subagent frontmatter (tools, model, permissionMode, maxTurns, hooks, memory, background), and git commit strategy for context artefacts. This is a reference implementation, not an application — it exists specifically to demonstrate best practice. The tool allowlist, model assignment per agent, and permission mode configuration are textbook Stage 2 specification-in-context patterns.

**Key structural elements:**
```
## Repository Overview → what this codebase is
## Key Components → architecture map
## Skill Definition Structure → YAML frontmatter spec
## Subagent Definition Structure → agent frontmatter spec
## Git Commit Strategy → versioning discipline
```

---

### S2-C2 — Context Document: MuhammadUsmanGM/claude-code-best-practices (minimal template)
**Type:** Context (Stage 2 — minimal CLAUDE.md template)  
**Author:** Muhammad Usman (community)  
**URL:** https://github.com/MuhammadUsmanGM/claude-code-best-practices/blob/main/examples/claude-md-minimal.md  
**Format:** Markdown, annotated template  

**What it demonstrates:**  
The "80/20" Stage 2 context document: the minimum viable CLAUDE.md that covers commands, structure, and key rules. Contains `npm test`, `npm run lint`, directory map, and three coding rules (strict TypeScript, response format, logger usage). Authored with the explicit philosophy that "a CLAUDE.md that grows organically from real problems is more useful than one written speculatively" — a useful design principle for the framework's guidance on Stage 2 context document evolution.

---

### S2-C3 — Context Document: tldraw/make-real CLAUDE.md (production SaaS project)
**Type:** Context (Stage 2 — real production project CLAUDE.md)  
**Author:** tldraw (open source, production product)  
**URL:** https://github.com/tldraw/make-real/blob/main/CLAUDE.md  
**Format:** Markdown, real project  
**Last updated:** February 2026  

**What it demonstrates:**  
A real-world production CLAUDE.md from a shipping SaaS product (an AI-powered wireframe-to-HTML tool). Includes: framework (Next.js), test commands, architecture summary, model configuration per provider (Claude, OpenAI, Google), API route structure, and explicit "no test suite" notification. Critically, it includes model-specific settings as context: `claude-3-7-sonnet-20250219 (thinking): extended thinking with budgetTokens: 12000, temperature: 0, seed: 42`. This is Stage 2 context engineering serving as the team's shared memory for an AI-collaborative development workflow.

---

### S2-C4 — Context Document: AGENTS.md Open Standard ⭐ IMPORTANT NEW STANDARD
**Type:** Context (Stage 2 — cross-platform open standard for agent context)  
**Author:** OpenAI, Google, Cursor, Factory, Sourcegraph (Linux Foundation / Agentic AI Foundation)  
**URL:** https://agents.md / https://github.com/agentsmd/agents.md  
**Format:** Open specification + canonical repository  
**Adoption:** 20,000+ GitHub repositories  

**What it demonstrates:**  
AGENTS.md is the emerging open cross-platform standard for Stage 2 context documents, formalised in August 2025 through collaboration between all major AI coding agent providers. It is now the dominant format alongside CLAUDE.md, with GitHub Copilot adding native support in August 2025. The specification is deliberately schema-free — plain Markdown with no required structure — making it the simplest possible Stage 2 context standard. Supports hierarchical override via nested files (nearest wins), which is a Stage 3 capability beginning to emerge at Stage 2. The canonical sample includes: dev environment tips, testing instructions, and CI plan references.

**The openai/codex repo AGENTS.md** (`https://github.com/openai/codex/blob/main/AGENTS.md`) is the highest-authority public example — OpenAI's own coding agent using AGENTS.md to guide development of itself, with detailed Rust-specific coding conventions, test strategy, and lint rules.

---

### S2-C5 — Context Document: anothervibecoder-s/claudecode-harness CLAUDE_EXAMPLE.md
**Type:** Context (Stage 2→3 boundary — production-grade harness CLAUDE.md template)  
**Author:** Community practitioner  
**URL:** https://github.com/anothervibecoder-s/claudecode-harness/blob/main/CLAUDE_EXAMPLE.md  
**Format:** Markdown template (sanitised/architectural blueprint)  

**What it demonstrates:**  
A Stage 2→3 boundary document: a "Brain" CLAUDE.md that orchestrates multi-model workflows. Key features: Team/Ownership Matrix (zero-overlap rules preventing code collisions), multi-model Consensus Panel (spawning Gemini + Sonnet in parallel for plan review), Memory Persistence specification, and security masking rules (never expose .env values). The secret masking rule (`sed -E 's/=.{10,}/=<redacted>/g'`) is a Stage 3 boundary specification embedded in a Stage 2 context document.

---

### S2-C6 — Context Document: alirezarezvani/claude-skills CLAUDE.md (enterprise-scale)
**Type:** Context (Stage 2 — enterprise-scale agent skills registry)  
**Author:** Alireza Rezvani  
**URL:** https://github.com/alirezarezvani/claude-skills/blob/main/CLAUDE.md  
**Format:** Markdown, directory-level context index  

**What it demonstrates:**  
Stage 2 context at scale: a CLAUDE.md that serves as the index for 232+ agent skills across 8 domains (engineering, product, marketing, C-level advisory, compliance, finance, project management, business growth). Demonstrates the modular documentation pattern where the root CLAUDE.md points to domain-specific guidance rather than containing it all inline — a Stage 2→3 context architecture maturation.

---

## Stage 3 — Intent Engineering
*Intent becomes an explicit, separate, managed document. Context is retrieved dynamically.*

---

### S3-I1 — Intent Document: Anthropic Claude Constitution ⭐ THE GOLD STANDARD
**Type:** Intent (Stage 3 — comprehensive intent specification for an AI system)  
**Author:** Anthropic (primary author: Amanda Askell)  
**URL:** https://www.anthropic.com/constitution  
**PDF:** https://www-cdn.anthropic.com/9214f02e82c4489fb6cf45441d448a1ecd1a3aca/claudes-constitution.pdf  
**Format:** Web document + PDF, ~80 pages  
**Licence:** Creative Commons CC0 1.0 (public domain)  
**Published:** January 22, 2026  

**What it demonstrates:**  
The most complete, authoritative, publicly available Intent document in the field. Written *for Claude*, not about Claude — this is the defining characteristic of a Stage 3 intent document. Rather than rules, it encodes *reasoning frameworks*: how to handle conflicts between principals, how to weigh helpfulness against harm, when to deviate from specific instructions in favour of deeper intent. The four-tier priority hierarchy (broadly safe → broadly ethical → compliant with guidelines → genuinely helpful) is the canonical example of intent architecture. The hardcoded/softcoded distinction maps exactly to the framework's Stage 4 specification boundary conditions.

**Key architectural patterns:**
- Principal hierarchy (Anthropic → Operators → Users) with moral override conditions
- Hardcoded behaviours (absolute, never overridable) vs softcoded defaults (operator-adjustable)
- Intent over rules: "We want Claude to have such a thorough understanding of our goals that it could construct any rules we might come up with itself"
- Written primarily for Claude as audience, not for human readers — this is the key Stage 3 intent document design principle

**Why it is high-fidelity:** Released under CC0, openly versioned, authored by the team that trains the model on it, externally verified through the soul document discovery process, and formally acknowledged by Anthropic leadership. It is also the first major AI intent document to formally acknowledge the possibility of AI moral status — a significant design decision with governance implications.

---

### S3-I2 — Intent Document: OpenAI Model Spec ⭐ THE CROSS-PLATFORM STANDARD
**Type:** Intent (Stage 3 — model behavioural intent specification)  
**Author:** OpenAI (dozens of contributors across research, product, legal)  
**URL:** https://model-spec.openai.com (latest) / https://model-spec.openai.com/2025-12-18.html  
**GitHub:** https://github.com/openai/model_spec (markdown source, versioned)  
**Format:** HTML versioned document + GitHub Markdown source  
**Latest version:** December 18, 2025  

**What it demonstrates:**  
OpenAI's equivalent of the Anthropic Constitution, described as "first and foremost, a document for people" (unlike Anthropic's which is primarily written for the model). This difference is itself instructive for the framework: intent documents can be written for different audiences with different effects. The Model Spec establishes a chain of command (society → OpenAI → developers → users), specifies the transformation exception for handling user-provided content, defines when the assistant should act on instructions in AGENTS.md or README files, and includes worked examples of prompt injection defence. Continuously updated with dated versions — the GitHub repository archives all versions from 2025-02-12 onwards, making it the most versioned intent document in the public domain.

**Key URL pattern for versioned access:**
- `https://model-spec.openai.com/2025-02-12.html` (first public version)
- `https://model-spec.openai.com/2025-12-18.html` (December 2025)
- Source: `https://github.com/openai/model_spec`

---

### S3-C1 — Context Document (dynamic): LangChain REWRITE_PROMPT pattern
**Type:** Context (Stage 3 — intent extraction from raw query before retrieval)  
**Author:** LangChain / open source community  
**URL:** https://docs.langchain.com/oss/python/langgraph/agentic-rag  
**Format:** Code + documentation  

**What it demonstrates:**  
The Stage 3 context document in code form: a dedicated prompt template that extracts semantic intent from raw user input before using it for retrieval. The REWRITE_PROMPT pattern (`"Look at the input and try to reason about the underlying semantic intent / meaning. Here is the initial question... Formulate an improved question:"`) is the practitioner implementation of Stage 3 intent separation — intent is extracted and managed separately from the raw context assembly. This is the RAG-era equivalent of the intent document: it exists at runtime, not as a static file.

---

### S3-S1 — Specification Document: Piebald-AI Claude Code System Prompts (sub-agent specs)
**Type:** Specification (Stage 3 — agent role and scope specifications)  
**Author:** Piebald-AI (reverse-engineered from Claude Code source)  
**URL:** https://github.com/Piebald-AI/claude-code-system-prompts  
**Format:** Markdown files, one per agent prompt  
**Updated:** Within minutes of each Claude Code release  

**What it demonstrates:**  
The complete set of Claude Code's internal specification documents for each sub-agent: Explore (575 tokens), Plan mode (715 tokens), Task, CLAUDE.md creation (384 tokens), Agent creation architect (1,110 tokens), /review-pr (211 tokens), /batch (1,106 tokens), Hook condition evaluator (145 tokens), Managed Agents onboarding (2,525 tokens). Each file is a Stage 3 specification document: it defines the role, scope, tool access, and behavioural constraints for a specific agent persona. The variation in token count reflects the variation in specification complexity — the Hook condition evaluator (145 tokens) vs the /schedule slash command (3,130 tokens) shows the range from minimal boundary specification to complex orchestration specification.

---

## Stage 4 — Specification Engineering
*Specification is the governing artefact. Agent behaviour is fully specified.*

---

### S4-S1 — Specification Document: OpenAI GPT-4.1 Prompting Guide ⭐ PRIMARY
**Type:** Specification (Stage 4 — production agent specification template)  
**Author:** OpenAI  
**URL:** https://developers.openai.com/cookbook/examples/gpt4-1_prompting_guide  
**Format:** Web guide with verbatim XML specification blocks  

**What it demonstrates:**  
The most complete public example of a Stage 4 agent specification in the wild. Specifies three mandatory categories of agent behaviour as XML blocks:

```xml
<!-- Persistence specification -->
"You are an agent — please keep going until the user's query is completely resolved, 
before ending your turn and yielding back to the user."

<!-- Tool-calling specification -->
"If you are not sure about file content or codebase structure pertaining to the 
user's request, use your tools to read files and gather the relevant information: 
do NOT guess or make up an answer."

<!-- Planning specification -->
"You MUST plan extensively before each function call, and reflect extensively on 
the outcomes of the previous function calls."
```

Also includes a complete 8-step "High-Level Problem Solving Strategy" specification for coding agents. Authored by OpenAI's model team based on empirical testing across production deployments.

---

### S4-S2 — Specification Document: OpenAI GPT-5 Prompting Guide
**Type:** Specification (Stage 4 — agentic workflow specification patterns)  
**Author:** OpenAI  
**URL:** https://cookbook.openai.com/examples/gpt-5/gpt-5_prompting_guide  
**Format:** Web guide with structured specification examples  

**What it demonstrates:**  
Stage 4 specification at the model family level. Introduces `<context_gathering>` specification blocks that constrain agent exploration behaviour ("Parallelize discovery and stop as soon as you can act"). Includes `<tool_persistence_rules>` XML:
```xml
<tool_persistence_rules>
- Use tools whenever they materially improve correctness, completeness, or grounding.
- Do not stop early when another tool call is likely to materially improve the answer.
- Keep calling tools until: (1) the task is complete, and (2) verification passes.
- If a tool returns empty or partial results, retry with a different strategy.
</tool_persistence_rules>
```
This XML specification block is the clearest example of Stage 4 boundary specification: a machine-readable constraint set governing agent tool use.

---

### S4-S3 — Specification Document: OpenAI GPT-5.1 Prompting Guide
**Type:** Specification (Stage 4 — agentic persistence and verbosity specification)  
**Author:** OpenAI  
**URL:** https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-1_prompting_guide  
**Format:** Web guide  

**What it demonstrates:**  
Stage 4 solution persistence specification (`<solution_persistence>`) and output verbosity specification (`<output_verbosity_spec>`). The solution persistence block is particularly important: "Treat yourself as an autonomous senior pair-programmer: once the user gives a direction, proactively gather context, plan, implement, test, and refine without waiting for additional prompts at each step." This is intent-as-specification: the agent's operating philosophy is encoded in a named, structured block.

---

### S4-S4 — Specification Document: OpenAI GPT-5.2 Prompting Guide
**Type:** Specification (Stage 4 — output contract and tool efficiency specification)  
**Author:** OpenAI  
**URL:** https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide  
**Format:** Web guide  

**What it demonstrates:**  
Stage 4 output specification with `<output_verbosity_spec>` blocks constraining response length ("Default: 3-6 sentences or ≤5 bullets for typical answers") and web search behaviour specification (`<web_search_rules>`). Introduces the completeness pass specification: a three-step structured verification sequence embedded as agent instruction. These are Stage 4 specification patterns that govern *quality criteria*, not just behaviour.

---

### S4-S5 — Specification Document: humanlayer/12-factor-agents ⭐ PRACTITIONER GOLD STANDARD
**Type:** Specification (Stage 4 — production agent specification framework)  
**Author:** HumanLayer (practitioner-authored, 19.2k GitHub stars)  
**URL:** https://github.com/humanlayer/12-factor-agents  
**Format:** GitHub repository + specification document  

**What it demonstrates:**  
The practitioner equivalent of the OpenAI prompting guides: specification principles derived from shipping customer-facing agents at scale. The 12-factor methodology applied to agent specification identifies the failure modes of under-specified agents ("getting past 80% requires reverse-engineering the framework, prompts, flow"). The context loop specification is the key Stage 4 pattern:
```python
context = [initial_event]
while True:
    next_step = await llm.determine_next_step(context)
    context.append(next_step)
    if (next_step.intent === "done"):
        return next_step.final_answer
    result = await execute_step(next_step)
    context.append(result)
```
This explicit context loop is Stage 4 specification: it defines how the agent's execution model is structured, not just what it should do.

---

### S4-S6 — Specification Document: OpenAI GPT-5.4 Prompt Guidance (current production)
**Type:** Specification (Stage 4 — current flagship model specification)  
**Author:** OpenAI  
**URL:** https://developers.openai.com/api/docs/guides/prompt-guidance  
**Format:** Web guide (actively updated)  
**Last updated:** ~1 week ago at time of research  

**What it demonstrates:**  
The most current Stage 4 specification guidance from OpenAI, covering reasoning effort selection (none/low/medium/xhigh as a tunable parameter), dependency-aware workflow specification, and verification loop patterns. The key insight for Stage 4: "Use explicit rules to keep tool use thorough, dependency-aware, and appropriately paced, especially in workflows where later actions rely on earlier retrieval or verification."

---

### S4-S7 — Specification Document: wshobson/agents multi-agent specification
**Type:** Specification (Stage 4 — multi-agent role and routing specification)  
**Author:** Community practitioner  
**URL:** https://github.com/wshobson/agents/blob/main/docs/agents.md  
**Format:** Markdown  

**What it demonstrates:**  
Stage 4 multi-agent specification: agents assigned to specific Claude models based on task complexity, with natural language invocation routing and slash command direct invocation. Shows model-to-role assignment specification (Opus for complex tasks, Haiku for lightweight background tasks) and specialisation through named personas (backend-architect, security-auditor, performance-engineer). This is the specification document form that enables Stage 5 harness routing.

---

## Stage 5 — Harness Engineering
*The harness governs agent orchestration infrastructure.*

---

### S5-H1 — Harness Document: SWE-bench evaluation harness ⭐ PRIMARY
**Type:** Harness (Stage 5 — production agent evaluation harness specification)  
**Author:** Princeton NLP (original) + OpenAI, Epoch AI, community  
**URL:** https://www.swebench.com/SWE-bench/  
**Harness reference:** https://www.swebench.com/SWE-bench/reference/harness/  
**GitHub:** https://github.com/princeton-nlp/SWE-bench  

**What it demonstrates:**  
The most externally validated agent harness specification in the public domain. 500 tasks, each in an isolated Docker container, with: bash-only tool access, no network (anti-cheating), git history removal after issue creation date (prevents solution access), resource requirements (120GB+ storage, `min(0.75 * cpu_count, 24)` worker limit), and Docker-based environment reproducibility. The dual evaluation of *both the harness and the model* is a key Stage 5 principle: the harness is itself a specification layer that shapes outcomes independently of model capability.

**Key harness specification properties:**
- Environment: barebones Linux Docker container
- Tool access: bash only (grep, find, sed, standard CLI tools)
- Network: disabled
- State: git history truncated at issue creation
- Evaluation: unit tests run against generated patch
- Storage: 120GB minimum for any cache level

---

### S5-H2 — Harness Document: Epoch AI SWE-bench Verified implementation
**Type:** Harness (Stage 5 — optimised production harness with verification layer)  
**Author:** Epoch AI  
**URL:** https://epoch.ai/benchmarks/swe-bench-verified  
**Blog:** https://epoch.ai/blog/swebench-docker  

**What it demonstrates:**  
Stage 5 harness optimisation: the Epoch AI team reduced 2,000GB of Docker images to 67GB through layer caching, enabling SWE-bench to run in 62 minutes on a single GitHub Actions VM. The harness specification includes an added verification layer: "gold tests are run several times and ensure they pass consistently" — a harness-level quality gate that the Princeton original lacks. The published Docker registry (`https://github.com/epoch-ai/swebench-docker`) is the harness as infrastructure: a deployable, versioned, publicly available agent operating environment.

---

### S5-H3 — Harness Document: undeadlist/claude-code-agents multi-agent harness
**Type:** Harness (Stage 5 — multi-agent orchestration harness for software delivery)  
**Author:** Community (UndeadList)  
**URL:** https://github.com/undeadlist/claude-code-agents  
**Format:** Markdown agent definitions + workflow specifications  

**What it demonstrates:**  
Stage 5 harness for a software delivery workflow: 11 parallel auditors feeding into a fix-planner, with pre-commit, pre-deployment, and full-audit workflow specifications. The CLAUDE.md reference requirement ("Make sure your project has a CLAUDE.md that references the agents") shows the Stage 5 harness's dependency on Stage 2 context documents — the stack is cumulative. The multi-stage workflow (`new-feature: test-writer → code-fixer → test-runner → browser-qa`) is a harness specification that governs agent sequencing.

---

### S5-H4 — Harness Document: shanraisshan/claude-code-best-practice global vs project settings reference
**Type:** Harness (Stage 5 — scope hierarchy specification for agent infrastructure)  
**Author:** Shan Raisshan  
**URL:** https://github.com/shanraisshan/claude-code-best-practice/blob/main/reports/claude-global-vs-project-settings.md  
**Format:** Markdown reference document  

**What it demonstrates:**  
The authoritative specification of Claude Code's scope hierarchy — the harness architecture that governs where different configuration artefacts live and how they override each other. Specifies: `~/.claude/` (user-level, all projects), `.claude/` in repo (project-level, team-shareable), `managed-settings.json` (organisation-enforced, highest precedence). The deny rule precedence principle ("deny rules have the highest safety precedence and cannot be overridden by lower-priority allow/ask rules") is a Stage 5 harness constraint that cannot be specified at Stage 2 or below. The Task system introduced in Claude Code v2.1.16 (January 22, 2026) — with filesystem-based task state, dependency graphs via `addBlockedBy/addBlocks`, and crash-recoverable session state — is described here as the most recent harness evolution.

---

## Stage 6 — Environment Engineering
*The environment is the complete operational world specification.*

---

### S6-E1 — Environment Document: Anthropic Claude Constitution (environment governance layer) ⭐
**Type:** Environment (Stage 6 — complete normative environment specification)  
**Author:** Anthropic  
**URL:** https://www.anthropic.com/constitution  
**Format:** PDF + web (CC0 licence)  

**What it demonstrates:**  
In addition to its Stage 3 intent function, the Claude Constitution operates as a Stage 6 environment governance document: it specifies the *complete normative world* within which Claude operates, including how to handle conflicts between layers of the stack (Anthropic intent overrides operator instructions overrides user requests), what the absolute boundaries of the environment are (hardcoded prohibitions), and how exceptions flow. The "operator adjustable defaults" system is environment architecture: it specifies what the entire environment looks like across all deployment contexts, not just a single agent's behaviour.

---

### S6-E2 — Environment Document: VILA-Lab "Dive into Claude Code" architectural analysis
**Type:** Environment (Stage 6 — complete agent environment decomposition)  
**Author:** VILA-Lab (academic/research)  
**URL:** https://github.com/VILA-Lab/Dive-into-Claude-Code  
**Format:** GitHub repository with systematic architectural documentation  
**Last updated:** 3 days before research date  

**What it demonstrates:**  
The most complete public decomposition of a production Stage 6 agent environment: 7 components (User → Interfaces → Agent Loop → Permission System → Tools → State & Persistence → Execution Environment) across 5 architectural layers, with a 9-step turn pipeline, 5-layer context compaction, and 7 independent safety layers. The analysis references a principal hierarchy, auto-approve rate progression (from ~20% to 40%+ with experience), and sandbox-based security (84% reduction in permission prompts). This is Stage 6 environment engineering made visible: the complete specification of the operational world within which agents act.

---

### S6-E3 — Environment Document: Piebald-AI system prompt changelog (live environment evolution)
**Type:** Environment (Stage 6 — live environment specification evolution log)  
**Author:** Piebald-AI  
**URL:** https://github.com/Piebald-AI/claude-code-system-prompts/blob/main/CHANGELOG.md  
**Format:** Markdown changelog, updated within minutes of each release  
**Versions tracked:** 169 versions since v2.0.14  

**What it demonstrates:**  
The most real-time window into Stage 6 environment specification evolution in the public domain. Recent additions visible in the changelog: Managed Agents memory stores reference (FUSE mounts, memory CRUD, concurrency, versions, redaction), background agent state classification examples, assistant voice and values template, user profile memory template, and background session instructions. Each changelog entry is a Stage 6 environment specification delta — a change to the operational world within which agents run. The velocity of these changes (169 versions) demonstrates that Stage 6 environment engineering is not a destination but an active, continuous engineering practice.

**Recent Stage 6 environment additions (sample):**
- `Data: Managed Agents memory stores reference` — FUSE mounts, session attachment, redaction
- `Data: Background agent state classification examples` — JSON outputs classifying agent state, tempo, needs, result
- `System Prompt: Background session instructions` — instructs background sessions to use job-specific directories
- `Data: User profile memory template` — personal details, work context, schedule, communication preferences

---

### S6-E4 — Environment Document: SWE-bench Pro environment construction specification
**Type:** Environment (Stage 6 — human-verified agent operating environment)  
**Author:** Academic research team (arXiv 2509.16941)  
**URL:** https://arxiv.org/pdf/2509.16941  
**Format:** Academic paper with environment construction methodology  

**What it demonstrates:**  
Stage 6 environment engineering at research-grade fidelity: professional software engineers construct Docker-based environments by systematically incorporating system packages, repository documentation, build tools, and dependencies. Environment verification: gold tests run multiple times, flaky test detection, human verification pipeline for each test. The automated verification ("ensure that the environment is working as expected... ensure that there are not any flaky tests that may change run by run") is Stage 6 environment quality assurance — the environment itself is tested before any agent is permitted to operate within it.

---

### S6-E5 — Environment Document: claudecode-harness production harness CLAUDE_EXAMPLE.md (Stage 6 patterns)
**Type:** Environment (Stage 6 — multi-model orchestration environment specification)  
**Author:** Community practitioner  
**URL:** https://github.com/anothervibecoder-s/claudecode-harness/blob/main/CLAUDE_EXAMPLE.md  
**Format:** Markdown template  

**What it demonstrates:**  
Stage 6 environment patterns embedded in a CLAUDE.md: The Hub (Opus) for strategy and memory consolidation, Consensus Panel triggered by user phrase spawning Gemini + Sonnet in parallel, Memory Persistence at filesystem path with MEMORY.md as index, automatic retrospective generation at `docs/retros/YYYY-MM-DD-[topic].md`. These are environment specifications: they define the complete computational and memory infrastructure within which agents operate, including cross-model coordination patterns. The "Retro Habit" specification (automatic session retrospective generation) is a Stage 6 environment feature: the environment itself produces governance artefacts.

---

## Cross-Cutting Reference Documents

### The Anthropic Prompt Engineering Overview (Stage 1→2)
**URL:** https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview  
*Canonical reference for the Stage 1→2 transition: XML tags, chain-of-thought, role assignment, iterative prompt design.*

### The dair-ai/Prompt-Engineering-Guide (community canonisation)
**URL:** https://github.com/dair-ai/Prompt-Engineering-Guide  
**Stars:** Most-starred PE repository on GitHub  
*The community reference that canonised Stage 1 and Stage 2 vocabulary for 3M+ learners.*

### The davidkimai/Context-Engineering handbook (Stage 2 definition)
**URL:** https://github.com/davidkimai/Context-Engineering  
*"Context engineering is the delicate art and science of filling the context window with just the right information for the next step." — Andrej Karpathy. First-principles handbook for Stage 2, with biological metaphor progression from atoms to neural systems.*

### The Meirtz/Awesome-Context-Engineering survey (Stage 2→5)
**URL:** https://github.com/Meirtz/Awesome-Context-Engineering  
*Comprehensive survey of hundreds of papers and frameworks covering the evolution from prompt engineering to production-grade AI systems. Includes 2026 shift to agent harnesses, open protocols (MCP, A2A, AG-UI), and coding agent project memory.*

### OpenAI Agents SDK (Stage 5 harness standard)
**URL:** https://github.com/openai/agents.md (AGENTS.md standard)  
**GitHub:** openai/agents (Python SDK)  
*The production harness SDK that operationalises Stage 4 specification into Stage 5 infrastructure. Includes handoffs, guardrails, tracing.*

---

## Document Priority Guide for dark_factory

The following prioritisation is suggested for the framework's worked examples and reference citations:

**Tier 1 — Cite in all stage descriptions:**
- S3-I1: Anthropic Claude Constitution (anthropic.com/constitution)
- S3-I2: OpenAI Model Spec (model-spec.openai.com / github.com/openai/model_spec)
- S2-C1: shanraisshan CLAUDE.md (21k stars, reference implementation)
- S2-C4: AGENTS.md standard (20k+ repos, Linux Foundation)
- S4-S1: OpenAI GPT-4.1 Prompting Guide (canonical Stage 4 spec)
- S5-H1: SWE-bench harness (most validated)

**Tier 2 — Reference in stage deep dives:**
- S4-S5: 12-factor-agents (practitioner gold standard)
- S2-C3: tldraw/make-real (real production CLAUDE.md)
- S5-H4: Scope hierarchy reference (Stage 5 infrastructure)
- S6-E2: VILA-Lab Dive into Claude Code (Stage 6 decomposition)
- S6-E3: Piebald-AI changelog (live Stage 6 evolution)

**Tier 3 — Use in anti-patterns and examples:**
- S1-C1: GitHub prompt engineering guide (Stage 1 exemplar)
- S2-C5: claudecode-harness (Stage 2→3 boundary patterns)
- S4-S6: GPT-5.4 prompt guidance (current state of art)
- S6-E4: SWE-bench Pro (Stage 6 environment quality)
