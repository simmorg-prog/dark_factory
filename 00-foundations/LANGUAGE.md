# LANGUAGE.md — Structural Vocabulary

> **E1-08 · Foundations · Wave 1**  
> Structural vocabulary for the AI Operational Maturity Framework repository.  
> Defines how the framework is organised, how its components relate, and the precise terms Claude Code must use when navigating, extending, or discussing the framework's own architecture.  
> Distinct from the domain vocabulary in [Glossary](./glossary.md).  
> See also: [Reader Guide](./reader-guide.md)

---

## Why This File Exists

The [Glossary](./glossary.md) defines what this framework is *about* — intent engineering, harness, specification corpus, Dark Factory. This file defines what this framework *is* — its own structural anatomy.

Two distinct vocabularies serve two distinct purposes. Using "document" when you mean "backlog item", "section" when you mean "wave", or "chapter" when you mean "epic" produces inconsistency that accumulates into confusion at scale. A framework whose own structural language is imprecise cannot serve as a reference for precise specification elsewhere. Consistent structural language is not a style preference — it is the same discipline the framework teaches applied to the framework itself.

---

## Framework Structure Terms

---

### Epic

A thematic group of related backlog items. The six epics are: **Foundations**, **Stage Deep Dives**, **Actors**, **Artefacts**, **Examples**, and **Strategy**. An epic is not a folder — it is a logical grouping that may span multiple folders. The `02-artefacts/` folder contains backlog items from the Artefacts epic; the `05-strategy/` folder contains backlog items from both the Strategy epic and some Actors items.

*Avoid:* chapter, section, theme, category.

---

### Backlog Item

A discrete unit of content work with a unique compound ID, title, epic, wave, priority, effort estimate, and status. The atomic unit of work in the framework. Identified by a compound ID: epic prefix + sequence number (e.g. `E1-07`, `E4-00`, `E5-01a`).

A backlog item produces one or more files. It is not equivalent to a file — one backlog item may produce a content file plus a diagram pair. Conversely, a fix to an existing file is a backlog item (`E1-01-FIX`) even though it produces no new file.

*Avoid:* task, ticket, story, document, page.

---

### Wave

A breadth-first execution batch. All backlog items in Wave N are completed before Wave N+1 items begin. A wave groups items by thematic focus — not by difficulty, size, or file location. Wave 1 covers Foundations. Wave 7 covers Organisational & Strategic. Wave 8 covers Maintenance & Vocabulary.

Wave is not the same as stage. The framework has six maturity stages and eight execution waves. These are entirely independent concepts.

*Avoid:* sprint, phase, iteration, stage (reserved for the six maturity stages).

---

### Stage

One of the six maturity levels of the AI Operational Maturity Framework: Prompt Engineering (1) through Environment Engineering (6). Stage has a single precise meaning in this framework — do not use it to mean "phase of execution" or "wave".

*Avoid:* level (ambiguous with CMMI levels), tier, phase.

---

### Master Brief

The single authoritative instruction document for Claude Code. Versioned with semantic versioning (`v1.0`, `v1.5`, `v1.6`). The Master Brief is the specification that governs all content production. It supersedes all prior verbal or conversational instructions. When the Master Brief and a memory file conflict, the Master Brief governs.

Current version: `v1.6` — located at `:temp_docs/CLAUDE_CODE_MASTER_BRIEF_3.md`.

*Avoid:* brief (standalone), instructions, spec, guide.

---

### Authoring Note

A content direction decision stored in Section 10 of the Master Brief for a backlog item not yet being written. An authoring note is not a full content brief — it records a framing decision, a naming convention, or a structural requirement that must be applied when the item is eventually executed. Authoring notes prevent decisions from being re-litigated in a later session.

*Avoid:* note, comment, reminder, guideline.

---

### Content Brief

The full specification for a backlog item within the Master Brief — file path, header, diagrams required, content structure, and authoring guidance. Every backlog item being actively executed must have a content brief in the Master Brief before Claude Code begins writing it.

*Avoid:* spec, brief (standalone — always "content brief" to distinguish from Master Brief), instructions.

---

### Wave Status

The execution state of a backlog item. Three states only: `To Do`, `In Progress`, `Done`. Maintained in both `BACKLOG.md` and the README Content Status table. These states are rendered as: 🔜 To Do, 🔄 In Progress, ✅ Done.

Do not invent intermediate states. Do not use "Complete", "Closed", "Open", or "Pending" — these are not part of the three-state vocabulary.

*Avoid:* open, closed, complete, pending, done (lowercase).

---

### Diagram Pair

A `.drawio` source file and its corresponding exported `.svg` — always produced together, always committed together, always stored in `/diagrams/`. A diagram pair is never split: committing one file without the other is a quality defect.

When referencing a diagram in a content file, always link the `.svg`. Never embed SVG inline. Never reference the `.drawio` directly in Markdown.

*Avoid:* diagram (ambiguous — always specify which file type or say "diagram pair" when referring to both files).

---

### Relative Link

An internal cross-reference using a path relative to the current file's location. Examples:

- From `00-foundations/glossary.md` to another foundations file: `./specification-discipline.md`
- From `00-foundations/glossary.md` to an artefacts file: `../02-artefacts/specification-corpus.md`
- From `00-foundations/glossary.md` to a diagram: `../diagrams/maturity-curve-overview.svg`

All internal links in this framework MUST be relative links. Absolute GitHub URLs (e.g. `https://github.com/simmorg-prog/dark_factory/blob/main/...`) are a quality defect — they break in forks, local previews, and any context other than the specific GitHub repository path they encode.

*Avoid:* link (unqualified), URL, reference — when the type matters, use "relative link" or "absolute URL" explicitly.

---

## Depth and the Deletion Test

Two concepts from John Ousterhout's *A Philosophy of Software Design* — as applied to this framework's own structure:

**Depth.** A backlog item is *deep* when a significant amount of content and understanding sits behind a small, clear title. The [Specification Quality Standard](./specification-quality-standard.md) is deep: the title is four words; the content behind it governs every specification artefact in the framework. A backlog item is *shallow* when its interface is as complex as its implementation — when reading the title and navigation links requires reading the whole document to understand what it covers.

Prefer deep backlog items. When a proposed item covers a topic already addressed in an existing deep item, merge rather than split.

**The deletion test.** Before creating a new backlog item, ask: if this item did not exist, would the framework's coverage become meaningfully incomplete? Would a reader encounter a gap they could not fill from existing items?

If yes — the item earns its place. If the same material would appear elsewhere, or if the item only restates what linked items already cover, it is a pass-through and should be merged or removed.

The deletion test applies to diagrams too: if removing a diagram from a content file leaves the reader able to understand the material from the prose alone, the diagram was decorative. If removing it creates a genuine gap in comprehension — a relationship, a comparison, a structure that prose cannot convey as efficiently — it was load-bearing.

---

## Rejected Terms

Explicit list of terms to avoid and what to use instead. These rejections are quality checks, not style preferences — using a rejected term signals a mismatch between what is meant and what the framework's structural vocabulary provides.

| Avoid | Use instead | Reason |
|---|---|---|
| document, page, chapter | backlog item | "Document" is too broad — every `.md` file is a document; the framework needs a more precise unit |
| task, ticket, story | backlog item | Borrows from project management vocabularies that carry connotations (sprints, points) that do not apply |
| phase, iteration, sprint | wave | Borrows from software delivery vocabularies |
| level | stage (maturity) | "Level" is ambiguous between the six maturity stages and CMMI capability levels |
| spec, brief (standalone) | content brief or Master Brief | Unqualified "brief" is ambiguous between the two distinct document types |
| diagram (standalone) | diagram pair | Never commit one file without the other; the term should signal both |
| link, URL (unqualified) | relative link or absolute URL | The distinction is a quality check — absolute URLs in content files are a defect |
| boundary | seam (architectural) or scope (specification) | "Boundary" carries Domain-Driven Design meanings that conflict with how the term is used here |
| complete, pending, open, closed | Done, To Do, In Progress | Wave Status uses exactly three states; other terms introduce ambiguity |

---

*Continue to: [Reader Guide](./reader-guide.md)*  
*Back to: [Glossary](./glossary.md)*
