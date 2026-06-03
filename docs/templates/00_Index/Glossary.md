# Glossary Template

> **Template purpose:** Lightweight project Glossary structure, styled after ISO/IEC/IEEE 24765:2017 (SEVOCAB — the Systems and Software Engineering Vocabulary). Use this template when a project needs one place that fixes the meaning of its shared terms. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** As soon as more than one document (SRS, architecture, module specs, ADRs) starts using project-specific terms — or as soon as two people use the same word to mean two different things. The glossary is the single source of truth for what each term means, so the other documents don't drift apart in meaning over time.
>
> **Companion standard:** ISO/IEC/IEEE 24765:2017 — Systems and software engineering — Vocabulary (SEVOCAB). This template borrows SEVOCAB's *style* (short, neutral, source-cited definitions). It does **not** copy SEVOCAB's definitions — write your own in your project's own words.
>
> **Status of this template:** Lightweight, project-specific glossary in SEVOCAB style. Suitable for solo/small-team and open-source projects. For a controlled, organization-wide vocabulary, consult the full ISO/IEC/IEEE 24765:2017 standard and SEVOCAB directly (https://pascal.computer.org/).

---

# Glossary — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | GLO-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 24765:2017 (SEVOCAB) — style reference |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Scope | {{Internal documentation / Public / Customer-facing}} |
| Maintained alongside | {{SRS / architecture / module specs / ADRs}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: what this document is for. The core idea for anyone new to formal practice — a glossary fixes the project's *shared vocabulary* so the project's documents can't quietly drift apart in meaning. When the SRS says "session," the architecture doc says "session," and a new contributor reads "session," all three should mean exactly the same thing. The glossary is where that one meaning lives.

{{This document defines the project-specific terms, names, and abbreviations used across {{Project Name}}'s documentation. It is the single source of truth for what each term means. When any other document uses a defined term, the meaning here governs. The goal is one shared vocabulary so documents and contributors don't drift apart in how they read the same words.}}

### 1.2 Scope

> Say what kinds of terms belong here and what kinds don't. A good rule: define a term if leaving it undefined would let two readers reasonably disagree about what it means. Don't define common English words used in their ordinary sense.

In scope:
- {{Terms unique to this project (coined names, internal concepts)}}
- {{Standard terms used in a project-specific or narrowed way}}
- {{Acronyms and abbreviations the project uses}}

Out of scope:
- {{Ordinary English used in its ordinary sense}}
- {{Terms already defined adequately by a cited external standard — reference the standard instead of redefining}}

### 1.3 How terms enter the glossary

> Explain the lightweight workflow for adding a term, so the glossary stays current instead of going stale. Keep it low-friction — a heavyweight process means terms never get added.

A term enters the glossary when:
- {{It appears in two or more project documents and needs one fixed meaning, or}}
- {{A reviewer flags that a word is being read two different ways, or}}
- {{A new concept is coined and named during design or an ADR.}}

### 1.4 How to propose a new term

> The actual steps a contributor takes. Keep it to a few bullets.

- {{Add the entry alphabetically in §3 using the entry format from §2.}}
- {{Write an original one- or two-sentence definition; cite a source if the term comes from a standard or an ADR.}}
- {{Add any see-also cross-references to related terms already defined.}}
- {{Record the addition in §6 Revision History.}}

---

## 2. Conventions

> Define the exact format every entry uses, so entries stay uniform and machine-scannable. Uniformity is the whole point — a reader should be able to skim any entry and know where the definition, source, and cross-references are.

### 2.1 Entry format

Each term is a bold term followed by an em dash and an original, self-contained definition. Source and see-also lines are optional and italicized:

> **{{Term}}** — {{One- or two-sentence definition in the project's own words. Define what the term means, not how it is implemented.}} *Source:* {{citation — e.g., ADR-NNNN, a named standard, or "this project"}} *See also:* {{Related Term 1}}, {{Related Term 2}}

- **Definition** — required. Original wording. Self-contained: a reader shouldn't need another entry to understand it.
- ***Source*** — optional. Where the term or its definition comes from (an ADR, a cited standard, or "this project" if coined here). Cite the *source of the term*; never paste a copyrighted definition.
- ***See also*** — optional. Cross-references to related entries, comma-separated.

### 2.2 Ordering

> State the ordering rule so entries are findable.

{{Entries are listed alphabetically by term, case-insensitive. Multi-word terms sort by the full phrase. Acronyms appear in §4, not inline in §3 (cross-reference them with *See also* if helpful).}}

### 2.3 Marking deprecated terms

> Terms get retired as a project evolves. Say how a term is marked deprecated so old documents that still use it can be understood, without encouraging new use.

{{A deprecated term stays in §3 with a **(deprecated)** marker after the term and a *See also* pointing to its replacement, and is also recorded in §5. Example: **{{Old Term}}** *(deprecated)* — {{former meaning}}. *See also:* {{New Term}}}}

---

## 3. Terms

> The substantive content: the alphabetical list of defined terms. Use the §2.1 format for every entry. The examples below show the format — replace them with your project's real terms. Keep definitions short, neutral, and original (SEVOCAB style), but write them yourself; do not copy any standard's wording.

**{{Artifact}}** — {{A named, versioned output of the project that other work depends on, such as a document, build, or dataset.}} *Source:* this project *See also:* {{Build}}, {{Release}}

**{{Build}}** — {{The process, and the resulting output, of turning source material into a runnable or publishable form.}} *Source:* {{adapted from ISO/IEC/IEEE 24765 sense; original wording}} *See also:* {{Artifact}}

**{{Session}}** — {{A bounded period of interaction with the system, from start to explicit end, treated as one unit for the purposes of {{state / logging / accounting}}.}} *Source:* ADR-NNNN *See also:* {{State}}

---

## 4. Acronyms and Abbreviations

> A separate, scannable table for short forms. Keep it distinct from §3 so readers can quickly expand an unfamiliar acronym without hunting through prose definitions. Notes column is for disambiguation (e.g., "our usage, not the common one").

| Acronym | Expansion | Notes |
|---|---|---|
| {{SRS}} | {{Software Requirements Specification}} | {{Highest-level "what" document; see ISO/IEC/IEEE 29148}} |
| {{ADR}} | {{Architecture Decision Record}} | {{One decision per record; see §3 "Artifact"}} |
| ... | ... | ... |

---

## 5. Deprecated and Superseded Terms

> A retirement log. When a term is replaced or dropped, record it here so anyone reading older documents can find out what it used to mean and what to use now. This is what lets vocabulary evolve without breaking old documents.

| Old term | Replaced by | Date | Reason |
|---|---|---|---|
| {{Old Term}} | {{New Term}} | {{YYYY-MM-DD}} | {{Why retired — e.g., name was ambiguous, concept merged into another}} |
| ... | ... | ... | ... |

> **Retirement process:** {{When a term is retired, (1) add the row above, (2) mark the §3 entry **(deprecated)** with a *See also* to its replacement per §2.3, and (3) record the change in §6.}}

---

## 6. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (at minimum Purpose and how terms enter/are proposed)
- §2 Conventions (the entry format is what keeps the glossary uniform)
- §3 Terms
- §6 Revision History

**Optional sections** (include if relevant):
- §4 Acronyms and Abbreviations (omit only if the project uses no acronyms — rare)
- §5 Deprecated and Superseded Terms (start empty; it fills up as the vocabulary evolves)

**Tailoring**:
- The §2.1 entry format is the heart of the template — keep it consistent across every entry, even if you trim other sections.
- Keep definitions short, neutral, and original. Write your own wording even when a term comes from a standard; cite the source of the *term*, not a copied definition.
- A glossary is only useful if it stays current. Favor the low-friction add process in §1.3–§1.4 over a heavyweight review gate, or terms will never get added and documents will drift anyway.
- For a small project, a single Glossary document is enough. For larger efforts, consider one glossary per major subsystem with a shared top-level glossary for cross-cutting terms.

**Vocabulary reference:** ISO/IEC/IEEE 24765:2017 (SEVOCAB) is the systems and software engineering vocabulary reference. Use it as a *style* model for writing clear, source-cited definitions, and as a place to check whether a standard term already exists before coining a new one. Do not copy its definitions into this project-specific glossary — write your own.
