# Software Development Plan Template

> **Template purpose:** Lightweight Software Development Plan (SDP) structure inspired by the ISO/IEC/IEEE life-cycle-process standards (15288 for system-level, 12207 for software-level, and the 24748 series for how to apply them). Use this template when you need to write down *which* lifecycle processes the project actually runs, and *how* you have shrunk the full standards to fit a real project's size and risk. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Early in a project, once you have a rough idea of what you are building (SRS) and how it might be shaped (SDD), and you want to make the *way you will work* explicit instead of improvised. The SDP is the project's process-definition document: it describes and tailors the lifecycle processes used to build the system. It does not state the requirements (that is the SRS), the design (that is the SDD), or the schedule-and-budget management of the work itself (that is the Project Management Plan). The SDP answers "what processes do we run, in what order, with what gates, and what did we deliberately leave out."
>
> **Companion standard:** ISO/IEC/IEEE 15288:2023 + ISO/IEC/IEEE 12207:2017 + ISO/IEC/IEEE 24748 series (lightweight) — Systems and software engineering — System and software life cycle processes, and life-cycle-management guidance.
>
> **Status of this template:** Lightweight process-plan skeleton assembled from public summaries of ISO/IEC/IEEE 15288:2023, 12207:2017, and the 24748 series. These standards are ISO-paywalled, so no normative text is reproduced here — the structure paraphrases the publicly documented process/lifecycle-management framing only. Verify section content against the full standards for enterprise, contractual, or safety-critical/regulated contexts; this skeleton is sized for solo and small-team use.

---

# Software Development Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | SDP-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 15288:2023 + 12207:2017 + 24748 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Lifecycle model | {{Iterative / Incremental / Waterfall / Custom — name it}} |
| Companion docs | {{SRS-…, SDD-…, ProjectMgmt-… — the docs this plan coordinates}} |
| Review cadence | {{When this plan is re-checked — e.g. per cycle / per release / on major scope change}} |

---

## 1. Introduction

> This is the project's **process-definition** document. It describes and tailors the *lifecycle processes* the project uses to build the system. It does NOT state the requirements (that is the SRS — "what must the system do") or the design (that is the SDD — "how the requirements are realized"). It also does not manage the schedule and budget of the work (that is the Project Management Plan). Keep those concerns out of this document and point at the right companion doc instead.
>
> A few formal terms appear throughout this plan. Define them once, here, in plain English so the rest of the document reads cleanly:
> - **Lifecycle process** — a named, repeatable chunk of work the standards define (for example Requirements Definition, Design, Verification). 15288 covers system-level processes; 12207 covers the software-specific ones. This plan *picks which ones the project actually runs.*
> - **Lifecycle model** — the overall shape of the project: how the stages are sequenced and revisited (waterfall = one pass; iterative/incremental = repeated passes; or a custom model). The model decides where the gates and milestones fall.
> - **Tailoring** — deliberately adding, dropping, or shrinking standard processes to fit a project's real size and risk, *with the reasoning written down.* Tailoring is a sanctioned move in the standards, not corner-cutting. For a solo or small project, most of this plan IS the tailoring rationale.
> - **Decision gate (stage gate)** — a checkpoint between stages where the project decides go / no-go / rework before spending more effort.
> - **Milestone** — a dated, verifiable point of progress (a deliverable landed, a gate passed).

### 1.1 Purpose

> One paragraph: state that this plan governs *how the project works*, not what it builds. Establish that it is the place where the lifecycle is named and tailored, and that requirements, design, and project management live in their own documents.

{{This document defines and tailors the lifecycle processes used to build {{Project Name}}. It states which processes the project runs, the lifecycle model that sequences them, the decision gates and milestones that pace the work, and — most importantly for a lightweight project — the deliberate tailoring decisions that reduce the full standards to a subset matched to this project's size and risk. It does not specify what the system does (see the SRS) or how it is designed (see the SDD).}}

### 1.2 Scope

> Define which parts of the project lifecycle this plan covers and which it explicitly leaves to other plans. Be concrete about the boundary with the Project Management Plan (schedule/budget/staffing) and with the Configuration Management plan if one exists.

In scope:
- {{The lifecycle model and stage structure}}
- {{Which lifecycle processes run, and who owns each}}
- {{Decision gates and milestones that pace the work}}
- {{Tailoring decisions and their rationale}}

Out of scope (covered elsewhere):
- {{Requirements content}} — see the SRS ({{SRS-…}})
- {{Design content}} — see the SDD ({{SDD-…}})
- {{Schedule, effort, staffing, reporting}} — see the Project Management Plan ({{ProjectMgmt-…}})
- {{Version control / branching / release mechanics}} — see §9 (Supporting Practices) and/or a Configuration Management plan ({{ConfigMgmt-…}})

### 1.3 Definitions and Acronyms

> Define the formal terms used in this plan, including the beginner concepts introduced in the §1 guidance. Add project-specific terms as needed. The goal is that a reader who has never written a formal process plan can follow the rest of the document.

| Term | Definition |
|---|---|
| Lifecycle process | A named, repeatable chunk of work the standards define (e.g. Requirements Definition, Design, Verification). |
| Lifecycle model | The overall shape of the project — how stages are sequenced and revisited (waterfall, iterative, incremental, custom). |
| Tailoring | Deliberately adding, dropping, or shrinking standard processes to fit the project's real size and risk, with the reasoning recorded. |
| Decision gate (stage gate) | A checkpoint between stages where the project decides go / no-go / rework before committing further effort. |
| Milestone | A dated, verifiable point of progress (a deliverable landed, a gate passed). |
| Activity / task | The standards decompose a process into activities, and activities into tasks. Here, an activity is "the concrete work that realizes a process." |
| Process owner | The single person (or agent) accountable for a process running and producing its outputs — accountability is singular even when work is shared. |
| RACI | Responsible / Accountable / Consulted / Informed — a compact way to record who does the work, owns it, advises, and is kept informed. |
| V-model | A way of drawing the lifecycle that pairs each definition stage (requirements, design) with the verification/validation stage that checks it. |
| Verification | "Did we build it right?" — does the output meet its specification. |
| Validation | "Did we build the right thing?" — does the output meet the real need. |
| {{Project term}} | {{Definition}} |

### 1.4 References

> List the companion standards and the project documents this plan coordinates, plus any prior Architecture Decision Records (ADRs) that already fixed process decisions. An ADR is a short dated note recording a decision and why it was made — if process choices were settled in ADRs, cite them so this plan does not silently contradict them.

Companion standards:
- ISO/IEC/IEEE 15288:2023 — system-level life cycle processes
- ISO/IEC/IEEE 12207:2017 — software-specific life cycle processes
- ISO/IEC/IEEE 24748 series — guidance on applying and tailoring the above

Project documents this plan coordinates:
- {{SRS-…}} — requirements ("what")
- {{SDD-…}} — design ("how realized")
- {{ProjectMgmt-…}} — project management ("how the work is run")
- {{ConfigMgmt-… (if any)}} — configuration management

Prior decisions:
- ADR-NNNN — {{process decision already recorded, e.g. "chose iterative lifecycle"}}
- {{path/to/status-doc.md}} — {{current-state anchor, if used}}

---

## 2. Project Overview and Process Context

> Orient the reader: what is being built, the team size and shape, and where this plan sits relative to the SRS, SDD, and Project Management Plan. Keep it short — this is orientation, not a re-statement of the requirements. Crucially, name the **single biggest factor** driving the process choices (e.g. solo developer, prose-native build, exploratory research). That factor justifies most of the tailoring later, so stating it up front makes the rest of the plan make sense.

**What is being built:** {{One or two sentences. Point at the SRS for detail rather than repeating it.}}

**Team size and shape:** {{Solo / pair / small team of N. Note if work is shared with an agent or collaborators.}}

**Document map (who answers what):**

| Question | Document |
|---|---|
| What must the system do? | SRS ({{SRS-…}}) |
| How is it designed? | SDD ({{SDD-…}}) |
| How is the work scheduled and tracked? | Project Management Plan ({{ProjectMgmt-…}}) |
| What processes do we run, and what did we tailor out? | **This document** |

**Dominant process-shaping factor:** {{Name the single biggest factor — e.g. "solo developer, so any process requiring multiple distinct roles is collapsed onto one owner" or "exploratory research project, so requirements firm up across cycles rather than up front." This factor is the root of the tailoring in §8.}}

---

## 3. Lifecycle Model

> Name and describe the lifecycle model the project uses, then explain in plain terms why it fits this project's size, risk, and rate of change. Define the stages the model is divided into and how/when stages repeat. For an iterative project, describe what *one cycle* looks like end to end. This section sets the skeleton that the decision gates (§6) and milestones (§7) hang on — so make the stage boundaries explicit, because a gate or milestone with no clear stage to sit between is hard to act on.
>
> Lifecycle models in brief: **waterfall** runs the stages once, in order; **incremental** delivers the system in slices, each a smaller pass; **iterative** repeats passes over the same scope, refining each time; the **V-model** is a way of *drawing* the lifecycle that pairs each definition stage with the verification/validation that checks it. Most real small projects are a hybrid — say which, and why.

**Chosen model:** {{Iterative / Incremental / Waterfall / V-model / Custom hybrid — name it}}

**Why this model fits:** {{Plain-English rationale tied to size, risk, and rate of change. E.g. "Requirements are still discovered through use, so an iterative model that revisits requirements each cycle fits better than a single waterfall pass."}}

**Stages:** {{List the stages the model divides into, in order.}}

| Stage | Purpose | Repeats? |
|---|---|---|
| {{Stage 1 — e.g. Requirements}} | {{What this stage produces}} | {{Once / each cycle}} |
| {{Stage 2 — e.g. Design}} | {{…}} | {{…}} |
| {{Stage 3 — e.g. Implementation}} | {{…}} | {{…}} |
| {{Stage 4 — e.g. Verification & Validation}} | {{…}} | {{…}} |

**What one cycle looks like (if iterative/incremental):** {{Walk the reader from the start of a cycle to its end — e.g. "pick one thing → requirements → design → implement → verify → capture decisions → decide next thing or stop." Name where the cycle begins and ends so the gates in §6 have clear boundaries.}}

---

## 4. Processes In Scope

> List the lifecycle processes this project actually runs, drawn from 15288 (system-level) and 12207 (software-level). Give each a **PROC-N** id and a one-line statement of its purpose *on this project* (not the generic standard purpose). This is the in-scope list only — processes you deliberately dropped, merged, or shrank are recorded in the tailoring section (§8), not here. If you are unsure whether a process belongs in scope, ask whether the project produces or consumes anything for it; if not, it is probably a tailoring decision for §8.

| ID | Process | Purpose on this project | Source |
|---|---|---|---|
| PROC-1 | Requirements Definition | {{Capture and maintain what the system must do}} | {{12207 / 15288}} |
| PROC-2 | Architecture & Design | {{Define how the requirements are realized}} | {{12207}} |
| PROC-3 | Implementation | {{Build the system}} | {{12207}} |
| PROC-4 | Verification | {{Check the build meets its specification ("built it right")}} | {{12207}} |
| PROC-5 | Validation | {{Check the build meets the real need ("built the right thing")}} | {{12207}} |
| PROC-6 | Configuration Management | {{Keep versions, changes, and artifacts under control}} | {{12207}} |
| PROC-7 | {{Decision / Project Planning / Agreement process if applicable}} | {{…}} | {{15288}} |
| PROC-N | {{…}} | {{…}} | {{…}} |

---

## 5. Process Activities and Owners

> For each in-scope **PROC-N**, describe the concrete **activities (ACT-N)** that realize it — what work actually happens, what inputs it consumes, and what artifacts it produces — and name the single accountable **owner (ROLE-N)**, plus contributors if useful. Keep activities at the "what work happens" level, not a task-by-task checklist. This is where the abstract process list (§4) becomes the real division of labor. For a solo project, the owner column may be the same person every row — that is fine and worth stating plainly. A **RACI** column (Responsible / Accountable / Consulted / Informed) is optional; include it only if more than one person is involved.

**Roles:**

| ID | Role | Held by |
|---|---|---|
| ROLE-1 | {{e.g. Developer / Owner}} | {{Name or "solo"}} |
| ROLE-2 | {{e.g. Reviewer}} | {{Name, or "n/a for solo"}} |
| ROLE-N | {{…}} | {{…}} |

**Activities:**

| ID | Realizes | Activity (what work happens) | Inputs | Outputs / artifacts | Owner |
|---|---|---|---|---|---|
| ACT-1 | PROC-1 | {{Elicit and record requirements}} | {{User need, prior notes}} | {{SRS sections}} | ROLE-1 |
| ACT-2 | PROC-2 | {{Produce/refine the design}} | {{SRS}} | {{SDD sections, ADRs}} | ROLE-1 |
| ACT-3 | PROC-3 | {{Implement the design}} | {{SDD}} | {{Code, prose artifacts}} | ROLE-1 |
| ACT-4 | PROC-4 | {{Verify against spec}} | {{Build, SRS/SDD}} | {{Test results, review notes}} | ROLE-1 |
| ACT-5 | PROC-5 | {{Validate against real need}} | {{Build, original need}} | {{Validation notes}} | ROLE-1 |
| ACT-N | PROC-N | {{…}} | {{…}} | {{…}} | ROLE-N |

> *(Optional RACI form — use instead of a single Owner column when more than one person is involved: add columns R / A / C / I and mark each role per activity. Exactly one **A** per row — accountability is singular.)*

---

## 6. Decision Gates

> Define the checkpoints (**GATE-N**) between stages where the project decides **go / no-go / rework** before committing further effort. For each gate, give its position in the lifecycle (which stage boundary it sits at, from §3), its **entry criteria** (what must be ready to *hold* the gate), its **exit criteria** (what must be true to *pass*), and who makes the call. Tie each gate to the stage boundaries from §3 so it is clear when in the lifecycle each one fires. A gate is a *decision*; the event of passing it is a *milestone* (§7) — keep the two distinct.

| ID | Position (stage boundary) | Entry criteria (ready to hold) | Exit criteria (true to pass) | Decision maker |
|---|---|---|---|---|
| GATE-1 | {{End of Requirements → Design}} | {{SRS sections drafted; open questions logged}} | {{Requirements stable enough to design against; go/no-go recorded}} | ROLE-1 |
| GATE-2 | {{End of Design → Implementation}} | {{SDD drafted; design reviewed}} | {{Design approved or sent back for rework}} | ROLE-1 |
| GATE-3 | {{End of Implementation → V&V}} | {{Build complete for this cycle/increment}} | {{Build ready to verify; no known blockers}} | ROLE-1 |
| GATE-4 | {{End of V&V → Release / Next cycle}} | {{Verification and validation complete}} | {{Meets spec and need; release or iterate}} | ROLE-1 |
| GATE-N | {{…}} | {{…}} | {{…}} | {{…}} |

> For an iterative project, the same gate set may fire once per cycle. Say so here rather than duplicating the table per cycle.

---

## 7. Milestones and Schedule

> List the dated, verifiable points of progress (**MS-N**) — deliverables landed, gates passed, releases cut. **Keep the MS-N numbering consistent with the Project Management Plan** so the two documents share one milestone namespace rather than colliding: if the PMP already uses MS-1..MS-5, continue from there here (or, better, treat the PMP as the single source of milestone IDs and reference them). For each milestone, note what makes it "done" (the verifiable evidence) and which gate or deliverable it corresponds to. If the project is not calendar-driven, dates can be relative (per cycle / per release) — just say so explicitly rather than leaving dates blank.

**Dating basis:** {{Calendar dates / relative (per cycle, per release) — state which. If relative, say what anchors a "cycle."}}

| ID | Milestone | Verifiable "done" evidence | Corresponds to | Date / cycle |
|---|---|---|---|---|
| MS-1 | {{Requirements baselined}} | {{SRS at version X, gate passed}} | GATE-1 | {{YYYY-MM-DD or "cycle 1"}} |
| MS-2 | {{Design baselined}} | {{SDD reviewed and approved}} | GATE-2 | {{…}} |
| MS-3 | {{First working increment}} | {{Increment runs / artifact landed}} | GATE-3 | {{…}} |
| MS-4 | {{First validated release}} | {{V&V complete; release cut}} | GATE-4 | {{…}} |
| MS-N | {{…}} | {{…}} | {{…}} | {{…}} |

> Cross-doc note: MS-N here and MS-N in the Project Management Plan ({{ProjectMgmt-…}}) are the **same namespace**. Do not renumber independently.

---

## 8. Tailoring Decisions and Rationale

> This is the heart of a lightweight SDP. Record each deliberate departure from the full standards (**TAIL-N**) — processes dropped, merged, or shrunk — with the reasoning for each, so the cuts are *sanctioned and traceable* rather than accidental. State the project factors (size, risk, solo developer, exploratory nature) that justify the lightweight subset, and note any process that would need to be **reinstated** if the project's risk or scale grew. A reviewer should be able to look at this section and see exactly what was left out and why — that is what separates principled tailoring from corner-cutting.

**Project factors justifying a lightweight subset:**
- {{Factor 1 — e.g. solo developer: roles that assume separate parties collapse onto one owner}}
- {{Factor 2 — e.g. low external risk / internal-use software: heavy assurance processes are out of proportion}}
- {{Factor 3 — e.g. exploratory: requirements firm up across cycles, so a single up-front baseline is unrealistic}}

**Tailoring decisions:**

| ID | Standard process | Decision | Rationale | Reinstate if… |
|---|---|---|---|---|
| TAIL-1 | {{Acquisition / Supply / Agreement processes}} | Dropped | {{No external parties; nothing to acquire or supply}} | {{A contract, client, or vendor enters}} |
| TAIL-2 | {{Separate Verification + Validation processes}} | Merged into one V&V activity | {{Solo project; same person checks "built it right" and "built the right thing" together}} | {{Independent verification becomes a requirement}} |
| TAIL-3 | {{Formal Quality Assurance process}} | Shrunk to a review step in ACT-4 | {{Risk does not justify a standalone QA function}} | {{Regulatory or safety obligations appear}} |
| TAIL-N | {{…}} | {{Dropped / Merged / Shrunk}} | {{…}} | {{…}} |

> Each TAIL-N should reference the PROC-N it modifies (or the standard process it removes) so the in-scope list (§4) and the tailoring record stay consistent.

---

## 9. Supporting Practices

> Document the cross-cutting practices that hold the processes together — the "how we actually work day to day" practices that *support* the lifecycle processes in §4 rather than being lifecycle stages themselves. Keep each entry to a short, concrete statement of the practice actually in use (not an aspiration). If a practice is large enough to need its own document (e.g. a full Configuration Management plan), state the practice briefly here and point at that document.

| Area | Practice in use |
|---|---|
| Version control & branching | {{Tool and workflow — e.g. git with a feature-branch workflow off a develop branch}} |
| Decision capture | {{Where decisions get recorded — ADRs, a status doc, a memory file}} |
| Documentation standard | {{Where artifacts live and what format — e.g. Markdown specs under docs/}} |
| Tooling & environment | {{Key constraints — e.g. platform, language, "no containers," offline-first}} |
| Quality & review | {{How work is checked before it is considered done — self-review, peer review, automated checks}} |
| {{Other practice}} | {{…}} |

---

## 10. Open Questions

> Track unresolved **process** decisions (**OQ-N**) — lifecycle choices, gate criteria, or ownership questions still being worked out — with what is blocking each and who needs to decide. Distinguish questions that **block the next gate** from ones that can **ride with a working default**. Resolve and remove entries as the process matures; a closed question can be moved to the Revision History note for that version rather than lingering here.

**Blocking (must resolve before the next gate):**
- **OQ-1**: {{Process question}} — blocked by {{what}}; decided by {{who}}; blocks {{which GATE-N}}.

**Non-blocking (riding with a default):**
- **OQ-2**: {{Process question}} — *default for now: {{the default in use}}.* Revisit if {{condition}}.
- **OQ-N**: {{…}}

---

## 11. Revision History

> Record every substantive change to this plan with a version bump, date, author, and summary of what changed. Because the process definition evolves as the project learns, keep this current — a stale process plan is *worse* than none, since people will follow a model the project no longer actually uses. When a tailoring decision (§8) or gate (§6) changes, note it here so the reasoning trail is unbroken.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §3 Lifecycle Model
- §4 Processes In Scope
- §8 Tailoring Decisions and Rationale (the heart of a lightweight SDP — never skip)
- §11 Revision History

**Optional sections** (include if relevant):
- §2 Project Overview and Process Context (omit only if the orientation is obvious from companion docs)
- §5 Process Activities and Owners (collapse to a short list for a strictly solo project)
- §6 Decision Gates (omit for a tiny one-pass project, but recommended for anything iterative)
- §7 Milestones and Schedule (omit if the Project Management Plan already owns all milestones — but then reference it)
- §9 Supporting Practices (omit individual rows that don't apply)
- §10 Open Questions (track elsewhere if you prefer)

**Tailoring**:
- Section organization follows the 15288 / 12207 / 24748 process framing, but the specific subset is a project choice, not a requirement. Add, drop, or merge sections as the project needs — and record *that* tailoring in §8, the same way you record process tailoring.
- Keep this plan focused on PROCESS (how we work). Requirements (WHAT) belong in the SRS, design (HOW realized) in the SDD, and schedule/effort/staffing in the Project Management Plan.
- Keep the MS-N milestone numbering shared with the Project Management Plan — one namespace across both documents, never two competing ones.
- Identifier conventions for cross-document traceability:
  - **PROC-N** — lifecycle processes in scope
  - **ACT-N** — process activities
  - **ROLE-N** — owner / role assignments
  - **GATE-N** — decision / stage gates
  - **MS-N** — milestones (shared namespace with the Project Management Plan)
  - **TAIL-N** — tailoring decisions and rationale
  - **OQ-N** — open process questions
- Revision history is mandatory. A process plan that no longer matches how the project works misleads everyone who follows it.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 15288:2023, 12207:2017, and 24748-series standards, not this lightweight version. This template is suitable for solo and small-team projects, internal tooling, and early-stage products; it deliberately omits the assurance, agreement, and organizational-project-enabling processes that contractual, enterprise, or safety-critical work requires.
