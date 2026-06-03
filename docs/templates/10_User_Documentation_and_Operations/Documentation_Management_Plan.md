# Documentation Management Plan Template

> **Template purpose:** Lightweight Documentation Management Plan (DMP) structure inspired by the ISO/IEC/IEEE 2651x documentation-management family. Use this template to plan *how* a project's documentation gets produced, reviewed, kept current, and retired — not to write the documentation itself. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once a project has more than a couple of documents to keep honest. A DMP is the "who owns which doc, how does it get reviewed, when does it get re-checked, and when do we let it die" document. It manages the *doc set* as a whole. It sits alongside the SRS/SDD (which describe the system) and points at the individual documentation deliverables, but is itself a management plan — not a guide anyone reads to use the product.
>
> **Companion standard:** ISO/IEC/IEEE 26511:2018, ISO/IEC/IEEE 26512:2018, ISO/IEC/IEEE 26513:2017 (with ISO/IEC/IEEE 26514:2022 cross-reference for documentation design).
>
> **Status of this template:** Lightweight skeleton assembled from public summaries of the ISO/IEC/IEEE 2651x documentation-management family (26511:2018 management process, 26512:2018 acquisition/supply, 26513:2017 review/test, with a 26514:2022 design cross-reference). These are paywalled ISO/IEC/IEEE standards, so no normative text is reproduced — section names, ID conventions, and ordering are paraphrased or independently derived. Verify against the full standards for enterprise, regulated, or safety-critical contexts; suitable as-is for solo and small-team internal use.

---

# Documentation Management Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | DMP-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 26511:2018 / 26512:2018 / 26513:2017 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Plan period | {{Covers releases / dates this plan governs, e.g. v0.x through v1.0}} |
| Doc repository | {{Where the managed documents live — path/repo/site}} |
| Documentation lead | {{Role or person accountable for the doc set}} |
| Companion design template | {{Link to the documentation-design template (per 26514) that governs the documents themselves}} |

---

## 1. Introduction

> This document is the plan for managing **{{Project Name}}**'s documentation — how documents get produced, reviewed, kept current, and retired. It manages the doc set; it is **not** itself a piece of documentation that an end user reads to operate the system. Read it the way you'd read a maintenance schedule for a building, not the way you'd read a tenant's how-to guide. The four subsections below set up the rest of the plan: why it exists (1.1), what it does and does not govern (1.2), the plain-language definitions a first-time reader needs (1.3), and the documents this plan leans on (1.4).

### 1.1 Purpose

> One paragraph: why this plan exists. It should establish that the plan governs the *production and lifecycle* of the project's documents, names who is accountable, and makes clear that without it documentation tends to rot silently — written once, never re-checked, quietly wrong.

{{This document plans the management of {{Project Name}}'s documentation: how each document is produced, who reviews and signs it off, how it is kept in sync with the system it describes, and how it is retired when no longer true. It exists so the doc set does not silently rot — so that a returning reader can trust that a published document still reflects reality. It is a management plan, not documentation itself; the managed documents live at {{path / repo / site}}.}}

### 1.2 Scope

> Define which documents and which phases/releases this plan governs, and — just as important — what it explicitly does **not** govern. Drawing the boundary plainly stops the plan from being blamed for things it never claimed to manage (code comments, throwaway chat logs, marketing copy).

This plan governs:
- {{e.g., the SRS, SDD, ADRs, architecture description, user guides, and READMEs listed in §3}}
- {{e.g., all documentation deliverables for releases {{v0.x}} through {{v1.0}}}}
- {{e.g., the living anchor document (STATUS.md or equivalent)}}

This plan does **not** govern:
- {{e.g., inline code comments — owned by the code, reviewed in code review}}
- {{e.g., chat logs and scratch notes — not deliverables}}
- {{e.g., marketing / landing-page copy — separate ownership}}
- {{e.g., the internal *design* of each document — see §8, which cross-references the 26514 design standard}}

### 1.3 Definitions and Acronyms

> Define the terms this plan uses, in plain words, the first time they matter. A first-time reader of formal documentation practice should be able to follow the whole plan from this table alone. The terms below are the load-bearing ones for a documentation-management plan; add project-specific terms as needed.

| Term | Definition |
|---|---|
| Documentation Management Plan (DMP) | A planning document that says **how** the project's documentation will be produced, kept current, reviewed, and retired. It manages the doc set — it is **not** itself a piece of user or product documentation. (This document.) |
| Information for users | The standards' formal term for what most people call "documentation" — any deliverable that helps a person use the system (guides, references, READMEs, specs treated as deliverables). Throughout this plan we use the plainer word **"documents."** |
| Doc inventory / doc set | The complete catalog of documents this plan is responsible for. Each is given a **DOC-N** identifier (see §3) so it can be tracked. |
| Acquirer vs. supplier | From 26512: the **acquirer** is whoever commissions a document; the **supplier** is whoever produces it. On a solo project both roles are usually the **same person** — we say so explicitly rather than pretending there is a vendor (see §6). |
| Review vs. edit vs. usability test | Three *different* checks done by *different* eyes (from 26513): a **review** checks technical correctness; an **edit** checks language, style, and consistency; a **usability test** checks whether a real reader can actually do the task the document describes. |
| Sign-off / approval gate | The named point at which a document is declared "good enough to publish," **by a named role** — not an implicit "looks done to me." |
| Lifecycle / cadence | Documents are not write-once. Each has a **state** (draft, reviewed, published, stale, retired) and a **re-check rhythm**. This plan defines that rhythm so documents don't silently go out of date. |
| Traceability | Linking a managed document back to what it documents (a requirement, a module, a release) via IDs, so you can answer "which documents are affected if *this* changes?" |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> List the documents and standards this plan depends on or points at. Categorize for readability. Include the companion standards, the project's own system documents (so the inventory in §3 can trace to them), and any house style guide.

Companion standards:
- ISO/IEC/IEEE 26511:2018 — managing the documentation process (the "manager of information for users" responsibilities).
- ISO/IEC/IEEE 26512:2018 — acquisition and supply of documentation (acquirer/supplier roles and agreements).
- ISO/IEC/IEEE 26513:2017 — requirements for testers and reviewers (review, edit, and usability testing of documentation).
- ISO/IEC/IEEE 26514:2022 — designing documentation (the *product* design standard this plan cross-references in §8).

Project documents this plan manages or relies on:
- {{SRS-PROJECT-ID-001}} — {{system requirements; documents in §3 trace to its requirements}}
- {{SDD-MODULE-ID-001}} — {{module design}}
- {{ADR-NNNN}} — {{architecture decisions the docs must stay consistent with}}
- {{path/to/STATUS.md}} — {{living anchor document}}

House conventions:
- {{Link to house style guide / terminology list / templates README}}

---

## 2. Documentation Strategy and Objectives

> This section is about **what outcomes** the documentation must achieve — who reads the docs, what they need to accomplish, and what "good" looks like for this project's doc set — not about the mechanics of producing them (that comes later). State the guiding principles up front as **DMP-N** objectives so the rest of the plan operates under them. Good objectives are concrete enough to check: "a newcomer can orient in under a minute" is checkable; "docs are high quality" is not.

### 2.1 Readers and what they need

> Name the audiences for the doc set and what each is trying to get done. Keep it short; the per-document audience lives in the inventory (§3). This is the project-wide picture.

| Audience | What they need from the docs |
|---|---|
| {{e.g., a returning maintainer}} | {{re-orient on current state in under a minute}} |
| {{e.g., a first-time contributor}} | {{understand the architecture and where decisions are recorded}} |
| {{e.g., an end user}} | {{accomplish their task without reading internals}} |

### 2.2 Documentation objectives

> The guiding principles. Each is a non-negotiable that the rest of the plan must honour. Use **DMP-N** so other documents (and other sections of this plan) can cite them.

- **DMP-1 {{Plain language over jargon.}}** {{User-facing prose uses the words readers think in; technical terms appear only when precision requires them.}}
- **DMP-2 {{Every decision is traceable.}}** {{Any significant decision a document relies on can be traced to an ADR or requirement ID.}}
- **DMP-3 {{Currency is scheduled, not hoped for.}}** {{Living documents have a re-check cadence (see §5); a document past its cadence is treated as stale.}}
- **DMP-4 {{Sign-off is by a named role.}}** {{No document is "published" without an explicit approval gate (see §10).}}
- **DMP-N** {{Additional guiding principle.}}

### 2.3 What "good" looks like

> A short, checkable definition of done for the doc set as a whole — the standard the plan is steering toward.

{{e.g., A returning reader can answer "where are we?" from the anchor document in under a minute; every published document is in the inventory with a current lifecycle state; no published document is past its re-check cadence; every load-bearing claim traces to a requirement or decision.}}

---

## 3. Document Inventory and Scope

> This is the master list the rest of the plan refers back to. Catalog **every** document the plan is responsible for, each with a **DOC-N** identifier, a title, its audience, the role that owns it, and its current lifecycle state. Record what each document **traces to** — the requirement, module, or release it documents — so that later, when something changes, you can do *impact analysis* (answer "which docs are affected?"). Treat **DOC-N** as parallel to any UserDoc-style identifiers so this inventory lines up with the user-documentation set if one exists separately.

| ID | Title | Audience | Owning role | Lifecycle state | Traces to |
|---|---|---|---|---|---|
| DOC-1 | {{Software Requirements Specification}} | {{maintainer / contributor}} | {{ROLE-2 Author}} | {{published}} | {{the system / release {{v0.x}}}} |
| DOC-2 | {{Software Design Description — {{Module}}}} | {{contributor}} | {{ROLE-2 Author}} | {{reviewed}} | {{module {{X}}; SRS req {{3.2}}}} |
| DOC-3 | {{Architecture Decision Records}} | {{contributor}} | {{ROLE-1 Lead}} | {{published}} | {{decisions; cross-cuts all docs}} |
| DOC-4 | {{STATUS.md (anchor / living)}} | {{returning maintainer}} | {{ROLE-1 Lead}} | {{living}} | {{current project state}} |
| DOC-5 | {{End-user getting-started guide}} | {{end user}} | {{ROLE-2 Author}} | {{draft}} | {{release {{v1.0}} features}} |
| DOC-N | {{Title}} | {{audience}} | {{role}} | {{state}} | {{what it documents}} |

> **Lifecycle states** used in the table above are defined in §9. A document marked `living` is one with a frequent re-check cadence rather than a one-time publish (e.g. an anchor/status document).

---

## 4. Roles and Responsibilities

> Name the documentation roles using **ROLE-N** identifiers and say what each is accountable for. On a solo or small project **one person usually wears several hats** — make that explicit (e.g. "ROLE-1 through ROLE-5 are all {{name/role}} until a second reader exists") rather than implying a team that does not exist. Then map roles to the documents in §3 so it is clear who owns, writes, reviews, and signs off each DOC-N. This is where the 26511 "manager of information for users" responsibilities land, in plain terms.

### 4.1 Roles

| ID | Role | Accountable for |
|---|---|---|
| ROLE-1 | Documentation lead | {{Owns the doc set as a whole; maintains this plan; runs the approval gate; the 26511 "manager of information" in plain terms.}} |
| ROLE-2 | Author | {{Produces and updates document content.}} |
| ROLE-3 | Technical reviewer | {{Checks technical correctness — REV-1 in §10.}} |
| ROLE-4 | Editor | {{Checks language, style, consistency — REV-2 in §10.}} |
| ROLE-5 | Approver | {{Signs off a document for publication — REV-4 in §10.}} |
| ROLE-N | {{Additional role}} | {{Accountability}} |

### 4.2 Who wears which hat

> The honest staffing picture. For a solo project, say so plainly.

{{On {{Project Name}} today, ROLE-1, ROLE-2, ROLE-3, ROLE-4, and ROLE-5 are all {{the same person / lead}}. This means several checks in §10 are *self-review*; §10 records which checks are genuinely independent and which are deferred until a second reader exists. As the team grows, split the hats and revise this section.}}

### 4.3 Role-to-document map

> Tie roles to the inventory so accountability per DOC-N is unambiguous.

| Document | Owner | Author | Reviewer(s) | Approver |
|---|---|---|---|---|
| DOC-1 | ROLE-1 | ROLE-2 | ROLE-3, ROLE-4 | ROLE-5 |
| DOC-N | {{role}} | {{role}} | {{role(s)}} | {{role}} |

---

## 5. Schedule and Milestones

> Tie documentation milestones (**SCHED-N**) to the *project's own* milestones — which documents must reach which lifecycle state by which release or date, including the **"documentation done" gate** that a release must pass before it ships. Then state the recurring **cadence** for re-checking living documents, so currency is scheduled rather than hoped for. Keep dates realistic for the actual team size: a slipped doc milestone should be visible *here*, not silently absorbed into "we'll get to it."

### 5.1 Milestones

| ID | Documentation milestone | Tied to | Target | Status |
|---|---|---|---|---|
| SCHED-1 | {{DOC-1 (SRS) reaches `published`}} | {{release {{v0.x}} planning}} | {{YYYY-MM-DD}} | {{planned}} |
| SCHED-2 | {{DOC-5 (getting-started) reaches `reviewed`}} | {{release {{v1.0}} feature-freeze}} | {{YYYY-MM-DD}} | {{planned}} |
| SCHED-3 | {{"Documentation done" gate for release {{v1.0}}}} | {{release {{v1.0}} ship}} | {{YYYY-MM-DD}} | {{planned}} |
| SCHED-N | {{Milestone}} | {{project milestone}} | {{date}} | {{status}} |

### 5.2 Re-check cadence for living documents

> Living docs (status anchors, specs that track a moving system) need a rhythm, not a one-time publish. State it so it is scheduled.

| Document | Re-check cadence | Trigger |
|---|---|---|
| {{STATUS.md (DOC-4)}} | {{every session / weekly}} | {{session start or end}} |
| {{specs (DOC-2…)}} | {{every release}} | {{release cut}} |
| {{ADRs (DOC-3)}} | {{when a decision is superseded}} | {{new ADR supersedes}} |
| {{DOC-N}} | {{cadence}} | {{trigger}} |

### 5.3 "Documentation done" gate

> The explicit checklist a release must pass on the documentation side before it ships. This is what stops "ship now, document later" from becoming "never documented."

{{Before release {{vN}} ships, the following must hold: every DOC-N affected by the release is at least `reviewed`; the anchor document (DOC-4) reflects the new state; no document tied to the release is `stale`; the approver (ROLE-5) has signed off the user-facing docs in the inventory.}}

---

## 6. Acquisition and Supply

> Following 26512, state who **commissions** each document (the *acquirer*) and who **produces** it (the *supplier*), and what the agreement between them is. For a solo project, note plainly that both roles are the **same person** and that this section is a lightweight placeholder until outside writers, contractors, or AI-generated drafts enter the picture. For any document produced by an outside party or tool, record a **SUP-N** entry with the deliverable, its acceptance criteria, and who accepts it. This section scales up later — do not over-engineer it for a one-person doc set.

### 6.1 Default arrangement

> The plain statement of who acquires and who supplies, today.

{{On {{Project Name}} today, the acquirer and supplier are the same person ({{the lead}}). There is no external vendor. This section is a placeholder that becomes load-bearing the moment an outside writer, a contractor, or an AI-generated draft produces a document the project depends on.}}

### 6.2 Supply agreements

> One row per document produced by an outside party or tool. Each needs a clear deliverable, acceptance criteria, and a named acceptor — so "is this draft acceptable?" has a defined answer.

| ID | Document / deliverable | Supplier | Acceptance criteria | Accepted by |
|---|---|---|---|---|
| SUP-1 | {{e.g., DOC-5 first draft}} | {{outside writer / AI tool / contractor}} | {{passes REV-1 and REV-2; covers tasks {{X, Y}}; in house style}} | {{ROLE-1 / ROLE-5}} |
| SUP-N | {{deliverable}} | {{supplier}} | {{criteria}} | {{role}} |

> **Note on AI-generated drafts:** if a document or draft is produced by an AI tool, treat the tool as a supplier and record it as a SUP-N entry. Whether such drafts need a distinct review path is tracked as an open question in §11.

---

## 7. Tooling and Infrastructure

> List the tools and infrastructure the documentation pipeline depends on, concretely enough that a new contributor could reproduce the setup: authoring format, version control and repository, any static-site generator or publish target, diagramming tools, and link-checking or linting. Note **where source documents live versus where published output goes**, and any constraints the project imposes (for example, no containerized toolchains). Concrete beats aspirational here — name the actual tools, not the ideal ones.

| Concern | Choice | Notes |
|---|---|---|
| Authoring format | {{e.g., Markdown}} | {{plain text, diffable, docs-as-code}} |
| Version control | {{e.g., git}} | {{docs live next to the code they describe}} |
| Source location | {{e.g., docs/ in the project repo}} | {{the source of truth for managed documents}} |
| Publish target | {{e.g., static site / internal repo / none}} | {{where rendered output goes; "none — repo is the surface" is a valid answer}} |
| Static-site generator | {{e.g., Hugo / none}} | {{if any}} |
| Diagramming | {{e.g., Mermaid / draw.io}} | {{kept in source where possible}} |
| Link / lint checks | {{e.g., markdown linter, link checker}} | {{run on {{commit / CI}}}} |
| Constraints | {{e.g., no containerized toolchains; native installs only}} | {{project-imposed limits the pipeline must respect}} |

> **Source vs. published:** source documents live at {{path/repo}}; rendered/published output (if any) goes to {{target}}. Editors change the source, never the published copy.

---

## 8. Documentation Design Reference

> The DMP manages **production and lifecycle**; it does **not** redefine what an individual document looks like — that is the job of the documentation *design* standard. Per ISO/IEC/IEEE 26514:2022, point **outward** to how the managed documents themselves are designed (structure, templates, style guide, terminology, accessibility conventions) and state which **house templates** apply to which DOC-N, rather than re-specifying all of that here. This keeps the management plan cleanly distinct from the documentation-product design it relies on.

### 8.1 Design authority

> Name where the design rules live, so this plan stays a *management* plan.

{{The design of individual documents — their structure, headings, style, terminology, and accessibility conventions — is governed by {{the house style guide / the 26514-aligned design template at {{link}}}}, not by this plan. This section is a cross-reference; if a design rule and this plan ever conflict, the design authority wins on *what a document looks like* and this plan wins on *how a document is produced and maintained*.}}

### 8.2 Template-to-document map

> Which house template each managed document is built from. Lets a reader find the right shape for a new DOC-N quickly.

| Document | House template | Design authority |
|---|---|---|
| DOC-1 (SRS) | {{SRS template}} | {{26514 design ref / style guide}} |
| DOC-2 (SDD) | {{SDD template}} | {{…}} |
| DOC-3 (ADRs) | {{ADR template}} | {{…}} |
| DOC-N | {{template}} | {{authority}} |

---

## 9. Maintenance and Lifecycle

> This is the section that keeps documentation **alive** across the whole project, not just at first write. Define the lifecycle **states** a managed document moves through and the **trigger** for each transition — including how a document is marked stale and eventually retired so the doc set does not silently rot. Then specify how a change to the *system* (a new requirement, a refactor, a superseded decision) propagates to the *affected documents*, using the traceability links recorded in §3.

### 9.1 Lifecycle states

> The defined states. Every DOC-N in §3 is in exactly one of these at any time.

| State | Meaning | Entry trigger |
|---|---|---|
| `draft` | Being written; not yet trustworthy. | Author starts the document. |
| `reviewed` | Passed technical review and edit (REV-1, REV-2 in §10); not yet signed off. | Reviews complete. |
| `published` | Signed off (REV-4) and trustworthy as current. | Approver signs off. |
| `living` | Published but on a frequent re-check cadence (see §5.2). | Designated as an anchor/status doc. |
| `stale` | Was published but is now suspected out of date. | Re-check cadence missed, **or** a traced change (§9.2) landed without the doc being updated. |
| `retired` | No longer applicable; kept for history but not trusted as current. | Superseded or the documented thing was removed. |

### 9.2 Change propagation

> How a change to the system reaches the documents that describe it. This is where the traceability column in §3 earns its keep.

{{When a requirement changes, a module is refactored, or a decision is superseded, look up which DOC-N entries *trace to* the changed thing (§3) and mark each affected document `stale`. A `stale` document must be updated and re-reviewed (§10) before it can return to `published`, or be `retired` if the documented thing is gone. Example: superseding ADR-{{NNNN}} marks any DOC-N that traces to it `stale` until reconciled.}}

### 9.3 Retirement

> How a document is actually retired, so retirement is a deliberate act and not just abandonment.

{{A document is `retired` by {{the lead (ROLE-1)}} when the thing it documents no longer exists or has been wholly superseded. Retired documents are {{moved to history/ / marked with a retirement banner}} and removed from the active inventory, but kept for traceability. Retirement is recorded in the document's own revision history and in §3.}}

---

## 10. Review, Edit, and Approval Workflow

> Per 26513, define the review stages with **REV-N** identifiers and keep the three checks **distinct** — they answer different questions and ideally use different eyes. End in an explicit **sign-off** by the named approver role: a document is published because someone with that role *approved* it, not because it "looks done." State how defects found in review are tracked and resolved. For a solo project, be honest about which checks are genuinely *self-review* and which are *deferred* until a second reader exists.

### 10.1 Review stages

| ID | Stage | Question it answers | Done by |
|---|---|---|---|
| REV-1 | Technical review | {{Is it correct? Does it match the system / requirement it documents?}} | {{ROLE-3 Technical reviewer}} |
| REV-2 | Edit | {{Is the language clear, consistent, and in house style?}} | {{ROLE-4 Editor}} |
| REV-3 | Usability check | {{Can a real reader actually do the task the document describes?}} | {{a reader who is not the author}} |
| REV-4 | Sign-off | {{Is it good enough to publish? — the explicit approval gate}} | {{ROLE-5 Approver}} |

### 10.2 Defect tracking

> Where review findings go and how they are closed, so nothing found in review is silently dropped.

{{Defects found in any of REV-1 through REV-3 are recorded as {{issues / a checklist in the PR / inline comments}} and must be resolved or explicitly waived before the document can reach REV-4. A document cannot be signed off with open, unwaived defects.}}

### 10.3 Approval gate

> The single explicit point that turns `reviewed` into `published`. Name the role; do not let "looks done to me" stand in for it.

{{A document moves to `published` only when {{ROLE-5}} records sign-off (in the revision history and in §3). Sign-off is by a named role, not an implicit judgement.}}

### 10.4 Solo-project honesty note

> Which checks are real and independent today, and which are deferred. Say it plainly rather than pretending a one-person project has three sets of eyes.

{{On {{Project Name}} today, REV-1 and REV-2 are *self-review* by {{the lead}}; REV-3 (usability) is *deferred* until a second reader exists and is flagged as OQ-{{N}} in §11; REV-4 sign-off is recorded by the same person but kept as an explicit, dated act so the gate still exists. When a second reader joins, REV-1 and REV-3 become independent.}}

---

## 11. Open Questions

> Track unresolved decisions about the documentation **process itself**, each as **OQ-N** with what is blocking it and who must decide. Distinguish **load-bearing** questions — ones that block adopting this plan — from **deferred-with-defaults** questions that already have a working default and can be revisited later. Resolve and remove entries as the plan matures, recording the resolution in §12.

### 11.1 Load-bearing (block adoption)

- **OQ-1** {{Question that must be answered before the plan can be followed}} — {{what's blocking, who must decide}}.

### 11.2 Deferred with defaults

- **OQ-DEF-1** {{e.g., Do AI-generated draft docs need a distinct review path?}} — *default: {{treat the tool as a SUP-N supplier and run the full REV-1…REV-4 workflow}}; blocked on first such draft.*
- **OQ-DEF-2** {{e.g., When does REV-3 usability testing become mandatory?}} — *default: {{deferred until a second reader exists; self-review stands in until then}}.*
- **OQ-DEF-N** {{Question}} — *default: {{default}}.*

### 11.3 Resolved (recorded for traceability)

- **OQ-N** {{Question}}: {{Resolution and date}}.

---

## 12. Revision History

> Record every substantive change to **this plan** in the table below — version, date, author, and a short summary of what changed — so the plan's own evolution is traceable. Bump the version on each meaningful revision. The plan is a living document, subject to the same lifecycle discipline (§9) it imposes on the documents it manages.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Documentation Strategy and Objectives
- §3 Document Inventory and Scope (the master list everything else refers back to)
- §4 Roles and Responsibilities
- §9 Maintenance and Lifecycle (the part that keeps docs from rotting)
- §10 Review, Edit, and Approval Workflow
- §12 Revision History

**Optional sections** (include if relevant):
- §5 Schedule and Milestones (omit or simplify if the project has no fixed release cadence yet)
- §6 Acquisition and Supply (a one-line placeholder is fine for a solo project; expand when outside writers, contractors, or AI-generated drafts appear)
- §7 Tooling and Infrastructure (omit if the pipeline is trivial and obvious)
- §8 Documentation Design Reference (omit if there is no separate design template/style guide yet — but add it as soon as one exists)
- §11 Open Questions (track elsewhere if you prefer, but keep load-bearing ones visible)

**Tailoring**:
- Section order follows the 26511/26512/26513 management → acquisition → review flow; reorder freely for your project, but keep the inventory (§3) early since the rest of the plan references DOC-N.
- Keep this a *management* plan. What an individual document looks like belongs in the design reference (§8), not here.
- On a solo project, do not invent a team. State plainly where one person wears several hats (§4.2, §6.1, §10.4) — honesty about who actually checks what is worth more than an org chart that doesn't exist.
- **Identifier conventions** (for cross-document traceability):
  - DMP-N: documentation objectives / guiding principles
  - DOC-N: managed documents in the inventory (parallels UserDoc-style identifiers)
  - ROLE-N: documentation roles
  - SCHED-N: scheduled milestones
  - SUP-N: acquisition/supply agreements
  - REV-N: review / edit / approval stages
  - OQ-N / OQ-DEF-N: open questions (load-bearing / deferred-with-defaults)
- These prefixes let other documents (SRS, SDD, ADRs) point back at this plan, and let this plan trace each DOC-N to what it documents.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 26511:2018, 26512:2018, and 26513:2017 standards (with 26514:2022 for documentation design), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
