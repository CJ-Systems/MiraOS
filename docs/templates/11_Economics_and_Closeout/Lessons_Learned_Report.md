# Lessons Learned Report Template

> **Template purpose:** Lightweight lessons learned / project-closeout report structure, following the SWEBOK Knowledge Area organization (Software Engineering Management and Software Engineering Process). Use this template at the end of a project — or at the end of a major phase — to capture what worked, what did not, and what to do differently next time. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** At project closeout, or at the close of a significant phase/milestone, while memories are fresh. The lessons learned report is a *backward-looking* closeout deliverable: it records knowledge so it outlives the people and the project. It is not a status report, not a plan, and not a defect tracker. Run a short retrospective (the looking-back session) first, then write the report from what that session surfaced.
>
> **Companion standard:** SWEBOK (Software Engineering Body of Knowledge) Knowledge Areas — particularly Software Engineering Management and Software Engineering Process; project retrospective practice informed by ISO/IEC/IEEE 16326:2019 (Systems and software engineering — Life cycle processes — Project management, closure activities).
>
> **Status of this template:** Lightweight lessons learned / project-closeout report structure. This document follows the SWEBOK Knowledge Area structure (Software Engineering Management and Software Engineering Process) and names no single normative standard — SWEBOK is a body-of-knowledge guide, not a conformance standard. Retrospective and closeout activities are additionally informed by ISO/IEC/IEEE 16326:2019 (project closure); that ISO/IEEE standard is paywalled — this template is a skeleton paraphrasing common closeout practice, not a reproduction of standard text, and should be verified against the full standard for regulated, contractual, or safety-critical contexts. Suitable for solo/small-team and internal use as-is.

---

# Lessons Learned Report — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | LLR-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | SWEBOK (Mgmt + Process KAs) + ISO/IEC/IEEE 16326:2019 closure (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Reporting period | {{Project start – end, or phase covered}} |
| Retrospective date(s) | {{YYYY-MM-DD — when the looking-back session(s) occurred}} |
| Participants | {{Roles/people who contributed lessons — keeps the report from being one person's opinion}} |
| Project outcome | {{Delivered as planned / Delivered with changes / Cancelled / Superseded}} |

---

## 1. Introduction

> This is the standard front matter. A reader who picks this report up cold needs to know what it is, what it covers, what the project's words mean, and what other documents it leans on — before any individual lesson can land. Fold the Purpose / Scope / Definitions / References subsections in below.
>
> **New to formal practice?** A **lessons learned report** is a closeout document captured at the end of a project (or a major phase) that records what worked, what did not, and what to do differently next time — so the knowledge survives the project's end. SWEBOK treats this as part of Software Engineering Process / Management; it is the written output of a **retrospective** (also called a *post-mortem* or *post-project review*) — the structured looking-back session that produces the lessons. "Post-mortem" is just the informal name; it does **not** imply the project failed.

### 1.1 Purpose

> One paragraph: state plainly that this report captures what was learned so the knowledge survives the project's end and improves the next one. Make clear this is a *closeout deliverable*, not a status report.

{{This document captures the lessons learned during {{Project Name}} so that the knowledge gained — what worked, what did not, and what to change next time — survives the project's end and improves future work. It is a closeout deliverable produced from the retrospective held on {{retrospective date}}. It is a backward-looking record of a completed unit of work; it is not a status report, a plan, or a defect tracker.}}

### 1.2 Scope

> Define what the report covers (which project or phase, which reporting period) and what it deliberately excludes. Two exclusions are worth stating up front in plain language so expectations are right: this report does **not** re-open or re-litigate past decisions, and it does **not** assign blame to individuals.

**This report covers:** {{which project / which phase, and the reporting period — e.g., "the v1.0 development effort, {{start date}} through {{end date}}"}}.

**This report excludes:**
- {{Out-of-scope item — e.g., "the v2 roadmap (forward-looking; belongs in a plan, not a retrospective)"}}
- Re-litigating decisions already made. Lessons describe what we now know, not who was right.
- Assigning blame. We name *situations* and *root causes*, not people. (See the no-blame rule in §4.)

> **Beginner note:** a lessons learned report looks **backward** at a completed unit of work. If you find yourself writing about what *will* happen, that belongs in a plan; if you are logging a still-open bug, that belongs in the issue tracker. Keep this report retrospective.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define the project-specific shorthand a reader would otherwise misread, plus the few formal terms this report depends on. At minimum define *lesson learned* and *root cause*.

| Term | Definition |
|---|---|
| Lesson learned | A specific, recorded finding from this project — something that worked, failed, or was observed — captured so it can inform future work. Each is given an `LL-N` id for traceability. |
| Root cause | The underlying reason a problem happened, not its surface symptom. "Tests failed" is a symptom; "no one owned writing tests" may be the root cause. A lesson is only actionable once you reach the root cause. |
| Actionable recommendation | A concrete, owned, dated change for next time — as opposed to a vague wish. "Improve testing" is not actionable; "add a coverage gate to CI, owned by {{X}}, by {{date}}" is. Each is given a `REC-N` id. |
| Retrospective | The structured looking-back session (a.k.a. post-mortem / post-project review) that produces the lessons in this report. |
| Reusable asset | Any artifact made during the project (template, script, checklist, config, test fixture, document) worth keeping for the next project rather than rebuilding. |
| Metric | A measured number describing the project objectively (schedule variance, defect count, cycle time). Metrics anchor opinion ("it felt slow") to evidence ("the build took 40 minutes"). |
| Closeout / closure | The formal end of a project, where remaining artifacts are archived and the project is declared complete. This report is a standard closeout deliverable. |
| {{Project term 1}} | {{Definition}} |
| {{Project term 2}} | {{Definition}} |

### 1.4 References

> List the applicable project, organizational, regulatory, contractual, and standards references. Linking the SRS, SDD, ADRs, and plans lets a reader trace a lesson back to the artifact it concerns.

Project documents:
- {{path/to/srs.md}} — Software Requirements Specification for {{Project Name}}
- {{path/to/sdd.md}} — Software Design Description(s)
- {{path/to/project-plan.md}} — project / management plan, schedule baseline
- ADR-NNNN — {{decision the lessons relate to}}

Organizational / contractual references (if any):
- {{policy / contract / SLA}} — {{relevance}}

Standards:
- SWEBOK — Software Engineering Body of Knowledge (Software Engineering Management; Software Engineering Process Knowledge Areas)
- ISO/IEC/IEEE 16326:2019 — Systems and software engineering — Life cycle processes — Project management, closure activities

---

## 2. Project Summary

> This is the "you are here" map. Someone who never touched the project should be able to read this section alone and understand enough for the lessons that follow to make sense. Keep it factual and brief — analysis belongs in later sections. State what the project was, its lifecycle model and major phases, the major deliverables, the team/roles, the planned-vs-actual timeline at a glance, and the final outcome.
>
> **Lifecycle model** simply means the shape the work followed — e.g., a few iterations (iterative/agile), one pass through requirements → design → build → test (waterfall), or a phased rollout. Naming it tells a future reader what kind of project this was.

**What it was:** {{One or two sentences — what {{Project Name}} set out to build and for whom.}}

**Lifecycle model & phases:** {{e.g., "Three two-week iterations, then a hardening phase" or "Single waterfall pass, four phases."}}

**Major deliverables:** {{the main things shipped — the product, key docs, releases}}.

**Team & roles:** {{who did what — by role, not just names; e.g., "1 developer (build + test), 1 reviewer, 1 stakeholder/approver."}}

**Final outcome:** {{Delivered as planned / Delivered with changes / Cancelled / Superseded}} — {{one sentence of context}}.

**At a glance (planned vs. actual):**

| Dimension | Planned | Actual | Note |
|---|---|---|---|
| Start date | {{YYYY-MM-DD}} | {{YYYY-MM-DD}} | {{}} |
| End / release date | {{YYYY-MM-DD}} | {{YYYY-MM-DD}} | {{e.g., slipped {{N}} weeks}} |
| Scope | {{planned scope summary}} | {{delivered scope summary}} | {{features cut / added}} |
| Effort | {{planned person-days}} | {{actual person-days}} | {{}} |

---

## 3. What Went Well

> Capture the effective practices, decisions, tools, and behaviors worth repeating. Each one becomes a numbered lesson (`LL-N`) so it can be referenced later. Be **specific and evidence-backed**: "the daily 10-minute sync caught the integration bug on day 3" beats "communication was good." For each, say what happened, *why* it worked, and whether it is repeatable on other projects.
>
> **Beginner note:** positives matter as much as negatives. Naming what worked tells the next project what to **keep**, not just what to fix. A report that only lists problems quietly throws away the practices that saved the project.

| LL-N | Observation (what happened) | Why it worked | Repeatable? |
|---|---|---|---|
| LL-1 | {{e.g., "Daily 10-minute sync caught the integration bug on day 3, before it spread."}} | {{e.g., "Short, fixed cadence surfaced blockers early without meeting overhead."}} | {{Yes — any team size}} |
| LL-2 | {{e.g., "Adopting the SRS template up front gave reviewers a shared structure."}} | {{e.g., "Consistent structure cut review time and missed-requirement risk."}} | {{Yes}} |
| LL-3 | {{Observation}} | {{Why}} | {{Yes / Project-specific}} |

> Add an `LL-N` row per finding. Numbering is continuous across §3, §4, and §5 so every lesson has a unique id (see §8 for how recommendations trace back to these ids).

---

## 4. What Did Not Go Well

> Capture the problems — but the house-depth move here is to push past the **symptom** to the **root cause**. Each problem becomes a lesson (`LL-N`) carrying the problem, its root cause, its impact, and (if known) what would have prevented it.
>
> **Symptom vs. root cause:** "the release slipped two weeks" is a symptom; "scope was never frozen, so new requirements kept arriving" is a candidate root cause. A lesson you can act on lives at the root-cause level, not the symptom level.
>
> **No-blame rule (state it and mean it):** name the *situation* and the *cause*, not the person. "Nobody owned test coverage" is a process gap; "{{name}} didn't write tests" is blame and it poisons the retrospective. The goal is a better process next time, not a verdict.

| LL-N | Problem (symptom) | Root cause | Impact | Preventable by |
|---|---|---|---|---|
| LL-4 | {{e.g., "Release slipped 2 weeks."}} | {{e.g., "Scope was never frozen; new requirements kept arriving mid-iteration."}} | {{e.g., "Late nights; one feature shipped under-tested."}} | {{e.g., "A scope-freeze gate at iteration start."}} |
| LL-5 | {{e.g., "Integration broke repeatedly in week 4."}} | {{e.g., "No shared interface contract between the two modules."}} | {{e.g., "~3 days of rework."}} | {{e.g., "Agree the interface in the SDD before parallel work begins."}} |
| LL-6 | {{Problem}} | {{Root cause — push past the symptom}} | {{Impact}} | {{What would have prevented it}} |

> Each `LL-N` in this section is what the Recommendations in §8 will trace back to. A problem with no root cause is unfinished; keep asking "why" until the cause is something you could actually change next time.

---

## 5. Process Observations

> Sections 3 and 4 are mostly about *what* happened on specific items. This section is about *how the work was done* — the process itself, independent of any single deliverable. Walking the SWEBOK Knowledge Areas / lifecycle activities one by one makes coverage systematic rather than ad hoc, so a whole class of problem (say, configuration management) doesn't get silently skipped. Emit an `LL-N` lesson wherever an activity produced something worth carrying forward.
>
> **Two acronyms a beginner may not know:**
> - **SCM (Software Configuration Management)** — how you keep track of versions, branches, and changes so everyone is working against a known, controlled state (think: the discipline around your version control, releases, and what's in each build).
> - **QA (Quality Assurance)** — the activities that check the work meets its standard: reviews, testing process, definition-of-done, gates. (QA is the *process* of assuring quality; testing in §6's metrics is one of its measurements.)
>
> This is where systemic, cross-cutting lessons surface — the ones that aren't about one bug or one good meeting but about how an entire activity was run.

| Activity | How the process performed | Lesson (LL-N, if any) |
|---|---|---|
| Requirements | {{How requirements were gathered, baselined, changed. Stable? Churned?}} | {{LL-N or "—"}} |
| Design | {{Was design documented before build? Did it hold up?}} | {{LL-N or "—"}} |
| Construction | {{Coding flow, standards, reviews, build setup.}} | {{LL-N or "—"}} |
| Testing | {{Test approach, coverage, when defects were found.}} | {{LL-N or "—"}} |
| Maintenance | {{If applicable — how fixes/changes after release were handled.}} | {{LL-N or "—"}} |
| Software Configuration Management (SCM) | {{Branching, versioning, release control — did the team always know what was in a build?}} | {{LL-N or "—"}} |
| Quality Assurance (QA) | {{Reviews, gates, definition-of-done — did quality checks happen and catch things?}} | {{LL-N or "—"}} |
| Project Management | {{Planning, estimation, tracking, risk handling.}} | {{LL-N or "—"}} |
| Communication | {{How information flowed among people and stakeholders.}} | {{LL-N or "—"}} |

> Example: `LL-7` — "Estimates were consistently 30% low because they omitted review/rework time; future estimates should budget a rework buffer." (Project Management.)

---

## 6. Metrics Summary

> This section is the evidence anchor for everything qualitative above. Summarize whatever the project actually measured: schedule (planned vs. actual, variance), cost/effort, quality (defect counts, escaped defects, rework), productivity, and customer/user satisfaction.
>
> **What is a metric, and why here?** A **metric** is a measured number that describes the project objectively. Metrics keep the report honest — they turn "it felt slow" into "cycle time was 40% over plan." Opinions are easy to argue with; measurements are not. **If a metric isn't available, say so plainly** ("not tracked this project") rather than guessing a number — a fabricated metric is worse than an absent one.

| MET-N | Metric | Planned / Target | Actual | Variance | Source |
|---|---|---|---|---|---|
| MET-1 | Schedule (end date) | {{YYYY-MM-DD}} | {{YYYY-MM-DD}} | {{+N weeks}} | {{project tracker}} |
| MET-2 | Effort (person-days) | {{N}} | {{N}} | {{+/- %}} | {{timesheet / estimate}} |
| MET-3 | Defects found pre-release | {{target / —}} | {{N}} | {{}} | {{issue tracker}} |
| MET-4 | Escaped defects (post-release) | {{target / —}} | {{N}} | {{}} | {{support log}} |
| MET-5 | Rework (% of effort) | {{—}} | {{N%}} | {{}} | {{estimate}} |
| MET-6 | User/customer satisfaction | {{target}} | {{score / "not measured"}} | {{}} | {{survey / —}} |

> Tie notable variances back to the lessons that explain them — e.g., "the `MET-1` two-week slip is explained by `LL-4` (scope never frozen)." That linkage is what makes the metrics *mean* something rather than just sit in a table.

---

## 7. Reusable Assets

> This is the salvage list. Inventory the concrete artifacts worth keeping so the next project rebuilds nothing it doesn't have to. For each asset record what it is, where it lives now, and what it's good for next time.
>
> **Reusable asset** = any artifact made during the project (template, script, test fixture, config, pattern, checklist, document, example) that is worth keeping rather than rebuilding from scratch. Distinguish **ready to reuse as-is** from **reusable after cleanup** — knowing which is which saves the next project from inheriting half-finished work it assumed was done.

| Asset | Type | Location | Reuse value / when to use | State |
|---|---|---|---|---|
| {{e.g., CI pipeline config}} | {{Config}} | {{repo path / wiki}} | {{"Drop-in for any project on the same stack."}} | Ready as-is |
| {{e.g., Test fixtures for {{X}}}} | {{Test asset}} | {{repo path}} | {{"Saves a day of setup on similar features."}} | Reusable after cleanup |
| {{e.g., Onboarding checklist}} | {{Checklist}} | {{path}} | {{"Use at the start of the next project."}} | Ready as-is |
| {{Asset}} | {{Type}} | {{Location}} | {{When to reuse it}} | {{Ready / After cleanup}} |

---

## 8. Recommendations

> This is the actionable, traceable heart of the report. Each recommendation gets a `REC-N` id and traces back to the `LL-N` lesson(s) that motivated it. The discipline runs both ways: a recommendation that can't point at a lesson is unsupported guessing, and a lesson with no recommendation is just an anecdote.
>
> **What makes a recommendation actionable?** It is **concrete, owned, and dated** — "add a coverage gate to CI, owned by {{X}}, by {{date}}" — not a vague wish like "improve testing." If you can't name an owner or a date, it isn't a recommendation yet; it's an open question (see §9).
>
> **Prioritize:** mark each as **must-do** (the project will repeat the same failure without it) or **nice-to-have** (a real improvement, but survivable to defer). Not everything can be first.

| REC-N | Recommendation (concrete, owned, dated) | Traces to (LL-N) | Benefit | Priority | Owner | Target date |
|---|---|---|---|---|---|---|
| REC-1 | {{e.g., "Add a scope-freeze gate at iteration start; no new requirements mid-iteration without a tradeoff decision."}} | LL-4 | {{e.g., "Removes the recurring late-slip cause."}} | Must-do | {{role}} | {{YYYY-MM-DD}} |
| REC-2 | {{e.g., "Define module interfaces in the SDD before parallel work begins."}} | LL-5 | {{e.g., "Eliminates integration rework."}} | Must-do | {{role}} | {{YYYY-MM-DD}} |
| REC-3 | {{e.g., "Budget a rework buffer in estimates (start at +30%)."}} | LL-7 | {{e.g., "Estimates stop running short."}} | Nice-to-have | {{role}} | {{YYYY-MM-DD}} |
| REC-N | {{Recommendation}} | {{LL-N(s)}} | {{Benefit}} | {{Must-do / Nice-to-have}} | {{Owner}} | {{Date}} |

---

## 9. Open Questions

> Capture the items the retrospective surfaced but could not settle: lessons that need more data, disagreements about a root cause, or recommendations whose owner or feasibility is still undecided. Each gets an `OQ-N` id; name the question and what is blocking resolution (or who must decide). Resolve and remove items as answers arrive.
>
> **Beginner note:** it is honest — not a failure — for a closeout report to ship with open questions. Recording them is precisely what stops the knowledge from quietly evaporating after the project disbands. The alternative (forcing a fake answer to look "complete") is how real uncertainty gets buried.

- **OQ-1:** {{Question — e.g., "Was the week-4 integration breakage really a missing interface contract (LL-5), or an environment-config mismatch? We disagree on the root cause."}} — *Blocking:* {{more data / who decides}}.
- **OQ-2:** {{Question — e.g., "REC-3's rework buffer: is +30% right, or should it be per-task? Needs a second project's data."}} — *Blocking:* {{what / who}}.
- **OQ-N:** {{Question}} — *Blocking:* {{what's blocking resolution, who needs to decide}}.

---

## 10. Closure Approval

> This is the formal closeout act: it records that the lessons have been reviewed and accepted, and that the project (or phase) is declared complete.
>
> **Closure vs. the document sign-off (they are different):** the **sign-off block** in the metadata table at the top says *"this document is approved"* — it's about the report. **This section** says *"the project is closed and these lessons are owned going forward"* — it's about the project. A report can be approved as a document even while closure is "accepted with conditions"; keep the two distinct.

| Role | Name | Decision (Accepted / Accepted with conditions / Not accepted) | Date |
|---|---|---|---|
| {{Project owner / sponsor}} | {{Name}} | {{Accepted / Accepted with conditions}} | {{YYYY-MM-DD}} |
| {{Technical lead}} | {{Name}} | {{Accepted / Accepted with conditions}} | {{YYYY-MM-DD}} |
| {{Other approver}} | {{Name}} | {{Decision}} | {{YYYY-MM-DD}} |

**Conditions / notes:** {{Any conditions attached to acceptance — e.g., "Accepted on condition REC-1 and REC-2 are scheduled before the next project kickoff." If none, write "None — project closed unconditionally."}}

---

## 11. Revision History

> A lessons learned report is sometimes amended after it's first circulated — a late root cause gets confirmed, a recommendation is re-owned, an open question closes. Track every substantive change with a version bump so the record stays trustworthy.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Project Summary
- §3 What Went Well
- §4 What Did Not Go Well
- §8 Recommendations
- §11 Revision History

**Optional sections** (include if relevant):
- §5 Process Observations (omit only if the project was too small to have distinguishable activities; usually keep it — this is where systemic lessons live)
- §6 Metrics Summary (omit if nothing was measured — but prefer to keep it and write "not tracked," which is itself a lesson)
- §7 Reusable Assets (omit if the project produced nothing reusable)
- §9 Open Questions (track elsewhere if you prefer)
- §10 Closure Approval (omit for purely informal internal retros; keep it whenever closure is a contractual or organizational deliverable)

**Identifier conventions:**
- `LL-N` — individual lessons learned (the traceable unit). Number continuously across §3, §4, and §5 so each lesson has a unique id.
- `REC-N` — recommendations, each tracing back to the `LL-N` lesson(s) that motivated it (§8).
- `MET-N` — metric rows, for citing a measurement from a lesson (§6).
- `OQ-N` — open questions (§9).

These prefixes enable cross-document traceability — a recommendation points at its lesson, a lesson can point at the SRS requirement or SDD design it concerns, and a metric anchors the lesson in evidence.

**Tailoring:**
- The SWEBOK activity list in §5 is a checklist for coverage, not a mandate — drop activities the project never had (e.g., "Maintenance" for a project with no post-release phase).
- Keep the report honest over complete: a short report with real root causes beats a long one full of symptoms.
- **Solo developer / small team:** this collapses cleanly. The retrospective is you (or two or three of you) spending 30 minutes looking back. §2 can be three sentences. §3 and §4 might be five `LL-N` rows total. The metadata sign-off and §10 closure rows can name the same one or two people — and for a purely personal project, "Approved by" and the §10 closure can simply be yourself, recording that you reviewed the lessons. The value isn't the ceremony; it's that next-you reads `LL-N`/`REC-N` instead of relearning the same lesson the hard way.
- The point of the `LL-N` → `REC-N` trace survives any amount of trimming: even one well-traced lesson-and-recommendation pair is worth more than a tidy form full of "N/A."

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 16326:2019 closure process (and your organization's mandated retrospective/closeout procedure), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
