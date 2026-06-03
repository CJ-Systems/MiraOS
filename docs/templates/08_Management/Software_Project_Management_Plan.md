# Project Management Plan Template

> **Template purpose:** Lightweight Project Management Plan (PMP, sometimes SPMP — Software Project Management Plan) structure inspired by ISO/IEC/IEEE 16326:2019. Use this template when you need to write down how a project will be organized, estimated, scheduled, tracked, and reported. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** At the start of a project — or when an ad-hoc project has grown enough that "keeping the plan in your head" has stopped working. The PMP is the "how will the work be run" document. It complements the SRS (WHAT the system does) and the SDD (HOW the system is designed): the PMP is HOW THE WORK ITSELF will be carried out.
>
> **Companion standard:** ISO/IEC/IEEE 16326:2019 — Systems and software engineering — Life cycle processes — Project management.
>
> **Status of this template:** Lightweight skeleton assembled from public descriptions of the 16326 project-management process. The standard text itself is paywalled and was NOT reproduced — section organization is inspired-by, prose is original. Verify against the full standard when you have access, especially for enterprise or regulated work.

---

# Project Management Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | PMP-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 16326:2019 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Project sponsor | {{Who is accountable for this project succeeding — for a solo project, this is you}} |
| Planning horizon | {{e.g., "next 3 months" / "to v1.0" / "ongoing"}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: what this document is for. State that it describes how the project will be MANAGED (organized, estimated, scheduled, tracked, reported) — not what the software does (that's the SRS) or how it's designed (that's the SDD).

{{This document describes how the {{Project Name}} project will be managed: how the work is broken down, estimated, scheduled, tracked, and reported. It is the project's management plan. It does not specify what the software does (see the Software Requirements Specification) or how it is designed (see the Software Design Description).}}

### 1.2 Scope

> What this plan covers and what it does not. Note the planning horizon (the whole project, or a phase?). Note any work explicitly excluded from this plan.

In scope:
- {{Phase / deliverable / time window this plan governs}}

Out of scope:
- {{Work governed by a different plan, or explicitly deferred}}

### 1.3 Definitions and Acronyms

> Define project-management terms a reader might not know, plus any project-specific terms. Three definitions below are pre-filled because the later sections rely on them — keep them, edit if your project uses the words differently.

| Term | Definition |
|---|---|
| Work Breakdown Structure (WBS) | A list of the project's work broken into pieces small enough to estimate and track. You keep splitting big chunks ("build the import feature") into smaller ones ("parse the file," "validate rows," "write to store") until each piece is something one person can actually pick up and finish. The WBS is the "what are all the things that have to get done" inventory. |
| Milestone | A meaningful checkpoint with a clear yes/no answer — "is this reached or not?" A milestone has no duration of its own; it marks that a set of work items is finished (e.g. "first end-to-end run works"). Milestones are how you tell whether the project is actually moving, separate from how busy you feel. |
| Effort vs. duration | **Effort** is how much working time a task takes (e.g. "6 hours of actual work"). **Duration** is how much calendar time passes before it's done (e.g. "spread over 3 days because I only work evenings"). They are different numbers: a 6-hour task can have a 3-day duration. Estimate effort first, then map it onto your real calendar to get duration. Confusing the two is the most common reason schedules slip. |
| {{Project term}} | {{Definition}} |

### 1.4 References

> Documents this plan depends on or points to. Categorize for readability.

Project documents:
- {{path/to/srs.md}} — Software Requirements Specification (what the system does)
- {{path/to/sdd.md}} — Software Design Description (how it's designed)
- {{path/to/risk.md}} — Risk Management document (see §7)
- {{path/to/cm-plan.md}} — Configuration Management Plan (see §8)
- {{path/to/vnv-plan.md}} — Verification & Validation Plan (see §8)

External standards:
- ISO/IEC/IEEE 16326:2019 — Project management process
- {{Other standards relevant to your project}}

---

## 2. Project Overview

### 2.1 Objectives

> What is this project trying to achieve? State outcomes, not activities — "users can import their data and search it" rather than "write an import function." Keep it to a handful of clear objectives.

- **OBJ-1** {{Objective}}
- **OBJ-2** {{Objective}}
- ...

### 2.2 Deliverables

> The concrete things the project will produce — what someone can point at and say "that exists now." Software releases, documents, deployed services. Each deliverable should map to one or more objectives.

| Deliverable | Description | Serves objective(s) |
|---|---|---|
| {{Deliverable}} | {{What it is}} | {{OBJ-N}} |
| ... | ... | ... |

### 2.3 Key Assumptions and Constraints

> **Assumptions** are things you're treating as true that you haven't proven — if one turns out false, the plan changes (e.g. "the third-party API stays free"). **Constraints** are hard limits you must work within (e.g. "must run on one laptop," "no budget for paid services"). Writing both down makes the plan honest and makes it obvious later what broke.

Assumptions:
- {{Assumption — and what happens to the plan if it's wrong}}
- ...

Constraints:
- {{Constraint — budget, time, platform, dependency, legal}}
- ...

---

## 3. Project Organization

> Who does what. For a team, list roles and who fills them. For a SOLO project, this section mostly collapses — you wear every hat — but it's still worth a few lines naming the hats, because it surfaces work that's easy to forget you're responsible for (testing, releasing, support, deciding scope). See the tailoring note at the bottom.

### 3.1 Roles and Responsibilities

| Role | Responsibility | Who |
|---|---|---|
| {{Project lead}} | Direction, scope decisions, priorities | {{Name / "solo founder"}} |
| {{Developer}} | Build, test, fix | {{Name / "same person"}} |
| {{Reviewer / QA}} | Verify work meets its definition of done | {{Name / "same person — review own work against the DoD"}} |
| {{Stakeholder / user}} | Provide feedback, accept deliverables | {{Name / "early users" / "future me"}} |
| ... | ... | ... |

### 3.2 Solo-Project Note

> If this is a one-person project, say so here and note which roles genuinely collapse into "me" and which you might delegate or automate later. This is also where you note tooling that stands in for a role (e.g. "automated tests stand in for a separate QA person").

{{For {{Project Name}}, all roles above are filled by one person. The roles are kept distinct on paper so that the responsibilities — especially review and release — don't silently disappear. {{Note any tooling or automation that substitutes for a role.}}}}

---

## 4. Managerial Process

> How the work is actually run, day to day. This is the engine of the plan: how you estimate, schedule, track progress, and report it. Keep it as light as the project allows — but pick a real cadence and write it down, because "I'll just stay on top of it" is the thing that fails.

### 4.1 Estimation

> How you turn a work item into a number. State whether you estimate in effort (hours/days of actual work) or in rougher sizes (small/medium/large). Note that you estimate **effort** first, then convert to **duration** using your real availability (see §1.3). It's fine to be rough — the goal is a number you can check reality against, not a precise prediction.

{{Work items are estimated in {{effort hours / t-shirt sizes / story points}}. Effort is converted to duration using {{available working hours per week / per day}}. Estimates are rough and revised as work proceeds.}}

### 4.2 Scheduling

> How estimates become a timeline. Note dependencies (work that can't start until other work finishes) and how you decide what to do next. Reference the schedule in §9 rather than duplicating it here.

{{Describe how the schedule is built and maintained. See §9 for the schedule itself.}}

### 4.3 Tracking

> How you know where things stand. What's your single source of truth — a board, an issue tracker, a STATUS file, a checklist? How often is it updated? The point is that "current state" lives somewhere you can read in a minute, not only in your head.

{{Progress is tracked in {{tool / file}}. Each work item moves through {{To do → In progress → Done}}. Current overall state is summarized in {{STATUS file / board}}, updated {{when}}.}}

### 4.4 Reporting and Cadence

> How and how often the project is reviewed. For a team: standups, weekly reviews, sponsor updates. For a solo founder: a recurring self-check is enough, but schedule it. State the cadence explicitly.

| Activity | Cadence | Who's involved | Output |
|---|---|---|---|
| {{Progress review}} | {{Weekly}} | {{Solo / team}} | {{Updated STATUS, re-prioritized work}} |
| {{Milestone check}} | {{At each MS-N}} | {{Solo / team}} | {{Milestone reached: yes/no + what's left}} |
| ... | ... | ... | ... |

---

## 5. Work Breakdown Structure and Milestones

> The heart of the plan: the inventory of work (WBS) and the checkpoints (milestones). See §1.3 for what these terms mean. Keep work items small enough to estimate and finish; if you can't estimate a WBS item, it's too big — split it. Every milestone needs a **definition of "done"** so "reached or not?" has a clear answer.

### 5.1 Work Breakdown Structure

> List the work items. Use WBS-N IDs so they can be referenced from the schedule, from milestones, and from tracking. Group with sub-numbers (WBS-1, WBS-1.1) if helpful. Estimate effort per item.

| ID | Work item | Estimated effort | Depends on | Notes |
|---|---|---|---|---|
| WBS-1 | {{Work item}} | {{effort}} | {{— / WBS-N}} | {{notes}} |
| WBS-2 | {{Work item}} | {{effort}} | {{WBS-1}} | {{notes}} |
| ... | ... | ... | ... | ... |

### 5.2 Milestones

> The checkpoints. Each milestone bundles a set of WBS items and has a clear definition of done — the test you apply to decide if it's truly reached. A milestone with a vague DoD ("mostly working") isn't a milestone; it's a wish.

| ID | Milestone | Bundles work items | Definition of "done" | Target |
|---|---|---|---|---|
| MS-1 | {{Milestone}} | {{WBS-1, WBS-2}} | {{The specific, checkable condition that means this is reached}} | {{YYYY-MM-DD / TBD}} |
| MS-2 | {{Milestone}} | {{WBS-3, WBS-4}} | {{Checkable condition}} | {{YYYY-MM-DD / TBD}} |
| ... | ... | ... | ... | ... |

---

## 6. Resources and Budget

> What the project needs to run, and what it costs. People (or just your own time), services, hardware, licenses, anything you pay for. For a solo project on a tight budget, this is mostly "my time + a few subscriptions" — but write it down, because recurring costs and time limits are real constraints that shape the schedule.

### 6.1 People and Time

{{Available working time (e.g., "~10 hours/week"). For teams, list people and their availability.}}

### 6.2 Tools, Services, and Costs

| Resource | Purpose | Cost | Notes |
|---|---|---|---|
| {{Service / tool / hardware}} | {{What it's for}} | {{$/mo, one-time, or free}} | {{notes}} |
| ... | ... | ... | ... |

### 6.3 Budget Summary

{{Total recurring cost, total one-time cost, and any spending limit the project must stay under.}}

---

## 7. Risk Management

> Risks are things that might go wrong and would hurt the project if they did. This section is intentionally BRIEF — a few top risks for visibility — with the detailed register kept in a separate Risk Management document. The point here is a quick "what am I most worried about, and what's my plan if it happens."

Top risks (full register in `{{path/to/risk.md}}`):

| Risk | Likelihood | Impact | Mitigation / response |
|---|---|---|---|
| {{What might go wrong}} | {{Low/Med/High}} | {{Low/Med/High}} | {{What you'll do to prevent it or respond}} |
| ... | ... | ... | ... |

> If you don't have a separate Risk Management document yet, this short table can stand alone until risk management grows enough to deserve its own file.

---

## 8. Configuration and Quality Management

> Two quick pointers, intentionally BRIEF, each deferring to its own plan.
>
> - **Configuration Management (CM)** is how you keep control of versions and changes — what's in version control, how releases are versioned and tagged, how changes get reviewed in. Detailed rules live in the CM Plan.
> - **Quality / Verification & Validation (V&V)** is how you confirm the work is actually correct and meets its requirements — testing, review, acceptance criteria. Detailed approach lives in the V&V Plan.

### 8.1 Configuration Management

{{One or two sentences on the approach (e.g., "Git, semantic versioning, changes reviewed before merge to main"). Full detail in `{{path/to/cm-plan.md}}`.}}

### 8.2 Quality and Verification

{{One or two sentences on the approach (e.g., "Automated tests must pass before release; each deliverable checked against its definition of done"). Full detail in `{{path/to/vnv-plan.md}}`.}}

---

## 9. Schedule

> The timeline: when work items and milestones are expected to land. Built from the WBS effort estimates (§5.1) plus your real availability (§6.1), respecting dependencies. Keep it at the granularity you can actually maintain — a milestone-level schedule that stays current beats a day-by-day Gantt chart that goes stale in a week. Remember effort ≠ duration (§1.3) when filling in dates.

| Milestone / phase | Work items | Start | Target finish | Status |
|---|---|---|---|---|
| {{MS-1 / Phase}} | {{WBS-1, WBS-2}} | {{YYYY-MM-DD}} | {{YYYY-MM-DD}} | {{Not started / In progress / Done}} |
| ... | ... | ... | ... | ... |

> Note key dependencies that constrain the order: {{e.g., "MS-2 can't start until MS-1 is done because ..."}}.

---

## 10. Open Questions

> Decisions still being resolved that affect the plan. Each gets what's blocking it and who needs to decide. Resolve and remove as the project proceeds.

- **OQ-1** {{Question}} — {{what's blocking, who decides}}
- ...

---

## 11. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Project Overview
- §4 Managerial Process (at minimum: how you track and how often you review)
- §5 Work Breakdown Structure and Milestones
- §11 Revision History

**Optional sections** (include if relevant):
- §3 Project Organization (collapses heavily for solo projects — keep §3.2, trim §3.1)
- §6 Resources and Budget (omit the budget table if there's genuinely nothing to spend; keep the time note)
- §7 Risk Management (the inline table can stand alone before a separate Risk doc exists)
- §8 Configuration and Quality Management (omit if covered entirely by separate plans you'd rather link from the SRS)
- §9 Schedule (can be merged into §5 milestones for very small projects)
- §10 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- WBS-N: work items in the Work Breakdown Structure
- MS-N: milestones (each with a definition of "done")
- OBJ-N: project objectives
- OQ-N: open questions

These prefixes enable cross-document traceability — milestones (MS-N) can be tied to work items (WBS-N), and work items can trace up to objectives (OBJ-N) and across to requirements in the SRS.

**Tailoring**:
- **Solo founder, lightweight:** Most of this collapses. §3 becomes a couple of lines (§3.2). §6 is "my time plus a subscription or two." §7 is the inline table. §9 can fold into the §5 milestone table. What you should NOT skip: the WBS + milestones with real definitions of done (§5), and a tracking + review cadence you'll actually keep (§4.3, §4.4). Those two are what keep a one-person project from drifting.
- **Growing into a team:** As people join, §3 (roles) and §4.4 (reporting cadence) stop being formalities and start earning their keep. Split the inline risk table into a real Risk Management document, and let the CM and V&V plans referenced in §8 become standalone files. The IDs (WBS-N, MS-N) start paying off once more than one person needs to point at the same piece of work.
- Estimate effort before duration, always (§1.3). The plan slips when those two get confused.
- Revision history is mandatory. Track every substantive change with version bumps.

**For regulated/enterprise projects:** use the full ISO/IEC/IEEE 16326:2019, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
