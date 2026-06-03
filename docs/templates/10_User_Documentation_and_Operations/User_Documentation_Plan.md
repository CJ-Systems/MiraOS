# User Documentation Plan Template

> **Template purpose:** Lightweight User Documentation Plan structure inspired by ISO/IEC/IEEE 26515:2018 (developing user documentation in an agile environment). Use this template when planning the docs that ship alongside a product — what to write, for whom, in what order, and how to keep it current. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Early in a project, once you know roughly who the users are and what the product does. A documentation plan is the "what docs do we owe our users, and how do we keep them honest" document. It sits alongside the SRS (WHAT the system does) and points at the deliverables that teach users HOW to use it. Revisit it each release.
>
> **Companion standard:** ISO/IEC/IEEE 26515:2018 — Systems and software engineering — Developing information for users in an agile environment.
>
> **Status of this template:** Lightweight skeleton assembled from public descriptions of the 2651x documentation series; the normative standard text is paywalled and is NOT reproduced here. Structure and ideas are paraphrased and reorganized for solo/small-team use. Verify against the full standard for enterprise/regulated contexts.

---

# User Documentation Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | DOC-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 26515:2018 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Audience of this plan | {{Who maintains the docs — solo author / small team}} |
| Companion SRS | {{SRS-PROJECT-ID-001, if one exists}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: what this plan is for. It should establish that this document plans the *user-facing* documentation (not internal specs), names the deliverables, and says how they stay current as the product changes.

{{This document plans the user documentation for {{Project Name}}: what we will write, who it is for, how it is organized, and how it is kept in sync with releases. It is a planning document, not the documentation itself — the actual docs live at {{path / site / repo}}.}}

### 1.2 Scope

> Define what documentation this plan covers and what it does NOT. User docs (getting-started, how-to, reference, troubleshooting) are usually in scope; internal design specs, API-internals, and marketing copy usually are not.

In scope:
- {{e.g., end-user getting-started guide}}
- {{e.g., task/how-to docs}}
- {{e.g., reference material}}
- {{e.g., troubleshooting}}

Out of scope:
- {{e.g., internal architecture / SDD — covered by the design docs}}
- {{e.g., marketing and landing-page copy}}
- {{e.g., contributor/developer onboarding — separate plan}}

### 1.3 Definitions and Acronyms

> Define the documentation terms used in this plan, so a first-time reader is not guessing. A few worth defining plainly the first time they appear:
>
> - **Audience / task analysis** — figuring out *who* reads the docs and *what they are trying to get done*, before writing a word. Docs are written for a reader with a goal, not for the product.
> - **Doc types** — the common shapes user documentation takes: **getting-started/tutorial** (first success, learning-oriented), **how-to/task** (steps to accomplish one specific goal), **reference** (look-up facts: options, commands, settings), **troubleshooting** (symptom → cause → fix).
> - **Docs-as-code** — treating documentation like source code: it lives in version control next to the product, changes through the same review process, and ships with releases.

| Term | Definition |
|---|---|
| {{Term 1}} | {{Definition}} |
| {{Term 2}} | {{Definition}} |
| ... | ... |

### 1.4 References

> List the inputs this plan depends on — the SRS (so docs match real features), the project glossary, any style guide, the release schedule, and the standard itself.

- {{path/to/srs.md}} — requirements the docs must cover
- {{path/to/glossary.md}} — shared terminology (see §6)
- {{path/to/style-guide.md}} — voice/tone rules, if separate
- {{release schedule / roadmap}} — drives the doc cadence (see §5)
- ISO/IEC/IEEE 26515:2018 — companion standard (lightweight use)

---

## 2. Audience and Task Analysis

> This is the foundation of the whole plan: you cannot write good docs until you know *who* is reading and *what they are trying to do*. For a true beginner: an **audience/task analysis** lists each kind of user (a "user class"), what they already know, and the concrete goals ("tasks") they come to the docs to accomplish. Everything in §3 and §4 is downstream of this table — write it first.

### 2.1 User Classes

> Each distinct kind of reader. Capture what they already know, their environment, and what success looks like for them. Use UC-N for traceability.

| ID | User class | What they already know | Primary goal |
|---|---|---|---|
| UC-1 | {{e.g., first-time user}} | {{little/none}} | {{get to first success}} |
| UC-2 | {{e.g., regular user}} | {{the basics}} | {{accomplish recurring tasks}} |
| UC-3 | {{e.g., power user / integrator}} | {{fluent}} | {{look up specifics, extend}} |
| ... | ... | ... | ... |

### 2.2 Tasks and Goals

> The concrete things each user class is trying to get done. Phrase as user goals ("install and run the first time", "connect a data source"), not product features. These tasks map directly onto how-to docs in §3.

| ID | Task / goal | User class(es) | Notes |
|---|---|---|---|
| TASK-1 | {{e.g., install and run for the first time}} | UC-1 | {{}} |
| TASK-2 | {{e.g., {{do the core thing}}}} | UC-1, UC-2 | {{}} |
| TASK-3 | {{e.g., recover from {{common failure}}}} | UC-2 | {{}} |
| ... | ... | ... | ... |

---

## 3. Documentation Plan

> The deliverables. Each is a **DOC-N** topic mapped to one of the four common doc types. This is the heart of the plan — the list of docs you actually owe your users. Trace each deliverable back to the user classes and tasks in §2 so nothing is written for no one, and no task is left undocumented.
>
> The four types, plainly:
> - **getting-started / tutorial** — learning-oriented; gets a brand-new user to their first success.
> - **how-to / task** — goal-oriented; the steps to accomplish one specific thing.
> - **reference** — information-oriented; facts to look up (options, commands, settings, errors).
> - **troubleshooting** — problem-oriented; symptom → likely cause → fix.

| ID | Deliverable | Type | Serves | Covers tasks | Priority | Status |
|---|---|---|---|---|---|---|
| DOC-1 | {{Getting Started}} | getting-started | UC-1 | TASK-1, TASK-2 | {{must-have}} | {{Planned}} |
| DOC-2 | {{How to {{X}}}} | how-to | UC-1, UC-2 | TASK-2 | {{}} | {{}} |
| DOC-3 | {{{{Thing}} Reference}} | reference | UC-2, UC-3 | — | {{}} | {{}} |
| DOC-4 | {{Troubleshooting}} | troubleshooting | UC-2 | TASK-3 | {{}} | {{}} |
| ... | ... | ... | ... | ... | ... | ... |

> Coverage check: every TASK-N in §2.2 should appear in at least one DOC-N row. Every DOC-N should serve at least one UC-N. List any known gaps as Open Questions in §9.

---

## 4. Information Architecture

> How the docs are organized so a reader can actually *find* the answer. Information architecture is the topic structure and navigation — the table of contents, the categories, the cross-links. For a beginner: a reader almost never reads docs front-to-back; they arrive with a goal and need to land on the right page fast. Plan for arrival-by-search and arrival-by-browsing both.

### 4.1 Topic structure

> The top-level grouping. A common shape mirrors the four doc types (Get Started / Guides / Reference / Troubleshooting), but use whatever fits your users' mental model from §2.

{{Outline the sections/categories and the topics under each. A simple tree is fine.}}

### 4.2 Navigation and findability

> How readers move between topics and locate what they need: the navigation menu, search, cross-links between related topics (e.g. a how-to links to the relevant reference page), and entry points (where a new user lands vs. where a returning user lands).

{{Describe navigation, search, and cross-linking approach.}}

---

## 5. Content Development Approach

> How the docs actually get written and kept current. The 26515 standard is specifically about doing this in an **agile** setting — docs evolve release-by-release rather than being written once at the end.

### 5.1 Cadence

> When docs get written and updated relative to development. The agile norm: a feature is not "done" until its user-facing docs are updated. Decide whether docs land in the same change as the feature, or in a closely-following pass.

{{Describe the cadence — e.g., "docs ship in the same change as the feature; a doc update is part of the definition of done."}}

### 5.2 Docs-as-code

> Treating documentation like source. For a beginner: this means the docs live in version control (the same repo or a docs repo), are written in a plain text format (e.g. Markdown), change through the same review process as code, and build/publish through an automated pipeline. The payoff is that docs and product can never silently drift apart — a stale doc shows up as a change to review.

{{Describe where docs live, the format, the build/publish pipeline, and how doc changes are reviewed alongside code.}}

### 5.3 Review and edit workflow

> Who reviews docs and for what. At minimum: a technical-accuracy review (does it match the product?) and a clarity/edit pass (can the target reader follow it?). On a solo project these may both be you on a different day — name the checks anyway so they happen.

{{Describe the review steps and who performs them.}}

---

## 6. Style and Terminology

> The rules that keep the docs consistent and readable. Consistency matters more than flourish — a reader learns one voice and one set of terms, then trusts it.

### 6.1 Voice and tone

> Plain-English guidance on how the docs should sound: person ("you"), tense, formality, sentence length, use of examples. Favor plain words over jargon; define a term the first time it appears.

{{Describe the voice and tone. Reference a separate style guide if one exists.}}

### 6.2 Terminology and glossary

> One name per concept, used everywhere. Link to the project glossary so docs, UI, and specs all use the same words. Inconsistent terminology is one of the most common reasons readers get lost.

{{Link to the project Glossary at {{path}}. Note any doc-specific term conventions.}}

### 6.3 Note on AI-agent products

> For products where an AI agent is part of the product, the agent itself can be a documentation surface — it can answer help questions, walk a user through setup, and explain errors in its own voice at runtime, supplementing (not replacing) the written docs. If that applies, decide here where the line sits: what the agent handles conversationally vs. what stays as durable written reference, and keep the agent's help voice consistent with the style rules above. Keep this generic; product-specific agent behavior belongs in that product's own docs.

{{If applicable, describe how an in-product agent shares the documentation load with the written docs. Otherwise delete this subsection.}}

---

## 7. Validation

> How you confirm the docs actually work — not just that they exist. Three complementary checks:

### 7.1 Usability testing

> Watch a real member of the target user class try to accomplish a task using only the docs. If they get stuck, the doc is wrong, not the user. Even one or two informal sessions per major doc catch most problems.

{{Describe how and when docs are usability-tested, and with whom.}}

### 7.2 Technical review

> Confirm every instruction, command, and screenshot matches the current product. Tie this to the release cadence in §5 so it does not drift.

{{Describe the technical-accuracy check.}}

### 7.3 Readability checks

> Lightweight checks that the prose is at the right level for the audience: plain language, defined terms, scannable structure (headings, lists, short paragraphs). Optionally a readability score, but human judgment against the §2 audience is the real test.

{{Describe readability checks and any tooling used.}}

---

## 8. Maintenance and Versioning

> How docs stay correct over the life of the product. Decide: how docs are versioned relative to the product, how a release triggers a doc review, how outdated docs are flagged or archived, and who owns the upkeep. Stale documentation erodes trust faster than missing documentation.

{{Describe versioning (e.g., docs versioned with the product release), the per-release doc-update trigger, how deprecated content is handled, and the maintenance owner.}}

---

## 9. Open Questions

> Documentation questions still being resolved. Include each open question and what's blocking it. Resolve and remove as the plan firms up.

- **OQ-1**: {{question}} — {{what's blocking, who needs to decide}}
- ...

---

## 10. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Audience and Task Analysis — the foundation; everything else depends on it
- §3 Documentation Plan (the DOC-N deliverables)
- §10 Revision History

**Optional sections** (include if relevant):
- §4 Information Architecture (a small project with only a handful of docs can fold this into §3)
- §5 Content Development Approach (keep at least the docs-as-code note even if brief)
- §6 Style and Terminology (delete §6.3 unless the product includes an AI agent)
- §7 Validation (scale to the project — even one usability session beats none)
- §8 Maintenance and Versioning (don't omit if the product ships more than once)
- §9 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- UC-N: user classes (§2.1)
- TASK-N: user tasks/goals (§2.2)
- DOC-N: documentation deliverables (§3)
- OQ-N: open questions (§9)

These prefixes enable traceability: each DOC-N traces back to the TASK-N it covers and the UC-N it serves, so coverage gaps are visible at a glance.

**Tailoring**:
- The four doc types (getting-started, how-to, reference, troubleshooting) are a strong default, not a rule. Use the set that fits your users' goals from §2.
- Scale the validation and maintenance sections to the project — a solo side project needs less ceremony than a shipped product, but should still name the checks so they happen.
- Keep this plan focused on *user-facing* documentation. Internal design docs belong in the SDD.

**For regulated/enterprise projects:** use the full ISO/IEC/IEEE 26515:2018 (and the 2651x documentation series), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
