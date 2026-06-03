# Process Improvement Plan Template

> **Template purpose:** Lightweight Process Improvement Plan (PIP) structure for planning a deliberate change to *how* a team builds software. It follows an IDEAL-style improvement cycle — assess where you are, set objectives, plan and pilot changes, roll them out, then measure whether they helped — and uses the vocabulary of the process-assessment standards. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When a retrospective, a recurring failure, or a deliberate maturity push tells you that the *way you work* needs to change — not the product, the process. Use it when you want to make that change on purpose, with named objectives, assigned actions, and a way to prove afterward that it actually worked. The PIP is the plan for a single improvement effort, bounded by a planning horizon. It does not state what the system does (that is the SRS), how it is designed (the SDD), or which lifecycle processes the project runs day-to-day (the Software Development Plan) — it plans an *upgrade* to those processes.
>
> **Companion standard:** ISO/IEC 33001:2015 (process assessment — concepts and terminology) and ISO/IEC 33002:2015 (requirements for performing process assessment), the successor framework to ISO/IEC 15504 (SPICE). CMMI (Capability Maturity Model Integration) is referenced as a complementary capability/maturity model. ISO/IEC/IEEE 12207 (software life cycle processes) names the processes being improved.
>
> **Status of this template:** Lightweight skeleton derived from public sources, aligned to the SWEBOK Software Engineering Management / Process knowledge areas and following an IDEAL-style improvement cycle (assess -> objectives -> plan/pilot -> rollout -> measure). The companion standards ISO/IEC 33001:2015 and ISO/IEC 33002:2015 (the successor to ISO/IEC 15504 / SPICE), and CMMI as a reference model, are paywalled/licensed works: this template paraphrases their structure and vocabulary at a high level and reproduces no normative text. It is NOT a substitute for the standards themselves. For formal, certifiable, or regulated process assessment and improvement, obtain and follow the full ISO/IEC 330xx family and/or CMMI material — verify all level definitions, assessment requirements, and terminology against the licensed sources rather than relying on this lightweight extract.

---

# Process Improvement Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | PI-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC 33001:2015 + ISO/IEC 33002:2015 (lightweight) |
| Companion model | CMMI (reference) |
| Owner | {{Project name or owner}} |
| Improvement cycle | {{IDEAL / PDCA / custom}} |
| Planning horizon | {{e.g. 2026-Q3 through 2027-Q1}} |
| Sponsor | {{Name / role of the person funding/authorizing the effort}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> The Introduction exists so that a reader who has never seen this project can understand *what is being improved and why* before they hit the detailed plan. Read this section as the elevator pitch for the whole improvement effort.
>
> A few formal terms appear throughout this plan. Define them once, here, in plain English so the rest of the document reads cleanly:
> - **Process improvement** — the discipline of deliberately changing *how* a team builds software (its repeatable ways of working: how it plans, reviews, tests, releases) to get better outcomes, as opposed to changing *what* it is building. This document plans such a change.
> - **Process assessment** — a structured examination of a team's current processes against a reference model, to find strengths and weaknesses. ISO/IEC 33002 defines how to perform one rigorously; this template only needs a lightweight version (an honest internal review counts — see §2).
> - **Process capability / maturity** — a rating of how well-defined, managed, and predictable a process is. Frameworks like ISO/IEC 330xx (capability *levels* per process) and CMMI (maturity *levels* 1–5 for the organization) give vocabulary for saying "we are here, we want to get there." You do **not** need to formally rate yourself to use this template — the levels are just a shared ladder to point at.
> - **SPICE / ISO/IEC 15504** — the older name and number for the process-assessment standard now reorganized as the ISO/IEC 330xx family. You will see both names in the wild; they refer to the same lineage.
> - **IDEAL-style improvement cycle** — the common shape of a process-improvement effort: assess where you are, set objectives, plan and pilot changes, roll them out, then measure whether they helped. The section order of this document follows that cycle.
> - **Pilot** — trying a process change with one small team or project first, before forcing it on everyone, so you can learn cheaply and back out if it fails (see §5).
> - **Baseline and measure** — a *baseline* is a "before" number (e.g. average days to fix a defect today); a *measure* (metric) is the same number tracked over time. Improvement is only provable if you wrote down the baseline before you changed anything (see §7).
> - **Traceability ID** — a short label like `PI-3` or `OBJ-2` attached to an item so other documents (and other sections of this one) can point at it precisely instead of re-describing it. The prefix list in the Template usage notes explains which letters mean what.

### 1.1 Purpose

> One paragraph: state that this document plans a deliberate improvement to how {{Project Name}} builds software, names the processes in scope, and identifies the assessment that motivated it.

{{This document plans a deliberate improvement to how {{Project Name}} builds software. It targets the following processes / ways of working: {{e.g. code review, defect handling, and release}}. The effort is motivated by the assessment recorded in §2 — specifically the weaknesses tagged FIND-1 … FIND-N. It states the improvement objectives (§3, OBJ-N), the concrete actions that achieve them (§4, PI-N), how those changes will be piloted (§5) and rolled out (§6), and how we will measure (§7) whether the improvement actually worked. It does not change *what* the product does — only *how* the team produces it.}}

### 1.2 Scope

> State which processes/practices this plan covers and which it explicitly does NOT. Improvement efforts drift when the boundary is vague.

> **Beginner note:** "Scope" here means *which ways-of-working we are changing*, not which product features. "Covers code review and release; does not cover hiring or budgeting" is the right kind of sentence.

In scope (processes/practices being improved):
- {{e.g. Code review — adding a consistent review step before merge}}
- {{e.g. Release — moving from ad-hoc to a checklist-driven release}}

Out of scope (explicitly NOT covered by this plan):
- {{e.g. Hiring and team structure}} — {{reason / where it is handled instead}}
- {{e.g. Budget and tooling spend}} — {{reason}}

### 1.3 Definitions and Acronyms

> A term/definition table. Seed it with the concepts a first-time reader needs; remove rows that do not apply to your effort.

| Term | Definition |
|---|---|
| Process improvement | Deliberately changing *how* the team works to get better outcomes (not changing what is built). |
| Process assessment | A structured look at current processes against a reference model to find strengths and weaknesses. |
| Capability / maturity level | A rating of how well-defined, managed, and predictable a process is (ISO/IEC 330xx per-process capability; CMMI org-wide maturity 1–5). |
| SPICE / ISO/IEC 15504 | The older name/number for the process-assessment standard now reorganized as ISO/IEC 330xx. |
| Pilot | A small, reversible trial of a change with one team before wider rollout. |
| Baseline | The "before" number captured prior to changing anything, against which improvement is judged. |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> List what this plan rests on, categorized. The assessment evidence is load-bearing — without it, §2's findings are just opinions.

Assessment evidence (what §2 rests on):
- {{path/to/retrospective-notes.md}} — {{e.g. retro from {{date}} where the review gap surfaced}}
- {{path/to/metrics-export}} — {{e.g. defect-escape and lead-time numbers}}

Organizational policy / process standards:
- {{path/to/dev-process.md}} — {{the current documented way of working, if any}}
- {{Definition of Done / contributing guide}} — {{location}}

Companion standards and models:
- ISO/IEC 33001:2015 — process assessment concepts and terminology (successor to SPICE / ISO/IEC 15504).
- ISO/IEC 33002:2015 — requirements for performing a process assessment.
- CMMI — complementary capability/maturity model (reference vocabulary).
- ISO/IEC/IEEE 12207 — software life cycle processes (names the processes being improved).

Related ADRs / specs:
- ADR-NNNN — {{decision that motivated or constrains this effort}}
- {{path/to/spec.md}} — {{relevance}}

---

## 2. Current Process Assessment

> You assess BEFORE you plan because improving a process you have not honestly looked at tends to fix the wrong thing — you end up optimizing the part that hurt most *recently* rather than the part that costs most. This section is the honest "before" picture the rest of the plan is built on.
>
> **Beginner note:** A rigorous ISO/IEC 33002 assessment (trained assessors, formal capability ratings) is *optional* here. An honest internal review — a retrospective, a few interviews, a look at your defect and lead-time numbers — is a valid lightweight substitute. Just label which one you actually did, so a reader knows how much weight the findings carry.

### 2.1 Assessment method and scope

> Say how the current state was examined and at what rigor: interviews, retrospectives, metric review, a formal 33002 assessment, or honest reflection. Name the processes you looked at (the assessment scope) — they should match §1.2.

{{The current state was examined by {{e.g. a team retrospective on {{date}} plus review of the last quarter's defect and lead-time metrics}}. Rigor: {{lightweight internal review / partial 33002-style assessment / full 33002 assessment}}. Processes examined: {{code review, defect handling, release}}.}}

### 2.2 Strengths

> What is already working. Keep these visible so the improvement does not accidentally break them — a common failure is "fixing" a process and losing a good habit that was holding things together.

- {{e.g. Strong shared ownership — anyone will pick up a broken build without being asked.}}
- {{e.g. Fast local feedback — the test suite runs in under two minutes.}}
- {{...}}

### 2.3 Weaknesses and findings

> The problems. Give each one a `FIND-N` id so the objectives in §3 can trace back to the specific weakness that motivated them. State each finding as an observed problem, not a solution.

| ID | Finding (observed problem) | Affected process |
|---|---|---|
| FIND-1 | {{e.g. No consistent code-review step; changes can reach production unreviewed, and defects escape.}} | {{Code review}} |
| FIND-2 | {{e.g. Releases are manual and undocumented; each one takes a different path and occasionally skips smoke tests.}} | {{Release}} |
| FIND-3 | {{e.g. Defects are tracked in chat, not a system; root causes are rarely recorded.}} | {{Defect handling}} |

### 2.4 Evidence

> The measurements or observations backing each finding — even qualitative evidence ("three of four engineers said X in the retro") is fine, as long as it is named. This is also where you capture the raw numbers that become baselines in §7.

| Finding | Evidence | Type |
|---|---|---|
| FIND-1 | {{e.g. 6 of last 20 production defects traced to changes merged without review.}} | {{Quantitative}} |
| FIND-2 | {{e.g. Two recent releases skipped the smoke test; one caused a rollback.}} | {{Incident record}} |
| FIND-3 | {{e.g. Retro consensus: "we never know why something broke twice."}} | {{Qualitative / retro}} |

---

## 3. Improvement Objectives

> Objectives are the **goals** — *where we want to be*. They are distinct from actions (§4, the work that gets us there) and from measures (§7, the proof we arrived). A plan with objectives but no actions is a wish; a plan with actions but no objectives is busywork.
>
> **Beginner note:** An objective should be *outcome-shaped and measurable* — "cut average time-to-fix from 9 days to 3" — not *activity-shaped* — "do more code review" (that is an action, not an objective). The Measure and Target columns are what make an objective falsifiable rather than a hope: they let you say later, with a number, whether you hit it.

{{Lead-in: this effort pursues the objectives below. Each is owned, measurable, and traces back to the assessment finding(s) that justify it. If an objective does not trace to a FIND-N, ask whether it is actually a problem worth solving in this cycle.}}

| ID | Objective (outcome) | Rationale | Measure | Target | Traces to |
|---|---|---|---|---|---|
| OBJ-1 | {{Reduce defects reaching production}} | {{Unreviewed changes are the top escape source}} | {{Production defects per release}} | {{From {{8}} to {{≤3}}}} | FIND-1 |
| OBJ-2 | {{Shorten defect time-to-fix}} | {{Slow fixes erode trust and pile up}} | {{Median days from report to fix}} | {{From {{9}} to {{≤3}}}} | FIND-3 |
| OBJ-3 | {{Make releases repeatable}} | {{Ad-hoc releases cause rollbacks}} | {{% of releases following the checklist}} | {{≥{{95}}%}} | FIND-2 |

---

## 4. Improvement Actions

> This is the spine of the document — the section the `PI-N` prefix names. Each `PI-N` is a **concrete, assignable, finishable piece of work**: someone owns it, it has a due date, and you can tell when it is done.
>
> **Beginner note — the trace chain becomes load-bearing here:** `FIND-N` (a weakness in the assessment) -> `OBJ-N` (the goal it sets) -> `PI-N` (the action that achieves it) -> a Measurement entry in §7 that confirms it worked. An action with no objective is busywork; an objective with no action is a wish. The "Achieves" column is what keeps the chain honest.
>
> **Smallest-safe-change framing:** prefer several small `PI-N` actions over one sweeping reorganization — small changes are easier to pilot, easier to back out, and easier to attribute results to. Any action that touches *how the whole team works* should usually be piloted (§5) before it is rolled out (§6).

{{Lead-in: the actions below realize the objectives in §3. Each is sized to be finished within the planning horizon; large ambitions are broken into several PI-N actions rather than one monolithic one.}}

| ID | Action (concrete work) | Owner | Due Date | Resources | Expected Benefit | Achieves |
|---|---|---|---|---|---|---|
| PI-1 | {{Add a required one-reviewer approval before merge}} | {{Name / role}} | {{YYYY-MM-DD}} | {{Repo settings; 1 hr team agreement}} | {{Catches defects before production}} | OBJ-1 |
| PI-2 | {{Adopt a defect tracker with root-cause field}} | {{Name / role}} | {{YYYY-MM-DD}} | {{Tool {{name}}; 2 hr setup}} | {{Faster, learnable fixes}} | OBJ-2 |
| PI-3 | {{Write and adopt a release checklist}} | {{Name / role}} | {{YYYY-MM-DD}} | {{0.5 day to draft + review}} | {{Repeatable, rollback-free releases}} | OBJ-3 |

---

## 5. Pilot Approach

> The whole point of a pilot is plain: it is a *cheap, reversible experiment* so that if a process change is bad, you learn it on one team for a week — not on everyone for a quarter. Define what success and failure look like *before* you run it, or you will rationalize whatever happened as success.
>
> **Beginner note:** Not every action needs a pilot. A one-line CI-config tweak does not — just do it. Pilot the changes that ask *people to work differently* (a new review step, a new release ritual), because those are the ones that meet resistance and need real-world feedback before you commit everyone.

### 5.1 Pilot scope

> Which `PI-N` actions get piloted, with which team/project, over what window.

| Piloted action | Pilot team / project | Window |
|---|---|---|
| PI-1 | {{e.g. the {{payments}} squad}} | {{e.g. 2 weeks, {{YYYY-MM-DD}} → {{YYYY-MM-DD}}}} |
| {{PI-N}} | {{...}} | {{...}} |

### 5.2 Entry / exit criteria

> What must be true to *start* the pilot, and what success vs. failure looks like at the *end*. Write these before running it.

- **Entry criteria:** {{e.g. the review tooling is configured; the pilot team has agreed to participate; the baseline (§7) is recorded.}}
- **Exit / success criteria:** {{e.g. ≥80% of merges go through the new review step AND the pilot team reports the overhead is acceptable.}}
- **Failure criteria:** {{e.g. the step is routinely bypassed, or it adds >1 day median to merge time with no defect benefit.}}

### 5.3 Feedback collection

> How the pilot team's experience is captured — not just the metrics, but how it *felt* to work the new way.

{{e.g. A 15-minute mid-pilot check-in and an end-of-pilot retro; a short async survey; the metric snapshot from §7 for the pilot window.}}

### 5.4 Go / no-go decision

> Who decides to roll out, scale back, or abandon — and on what basis. Tie the decision to the §5.2 criteria, not to gut feel.

{{Decision made by {{Sponsor / improvement owner}} at the end of the pilot window, based on the §5.2 exit criteria and §5.3 feedback. Outcomes: **roll out** (proceed to §6) / **adjust and re-pilot** / **abandon** (record why in §9 / §10).}}

---

## 6. Rollout Plan

> Rollout is where process improvements most often die — not because the new process was bad, but because people were never brought along, were never trained, or quietly reverted under deadline pressure. This section exists to plan *against* that: treat adoption as a thing to actively manage, not assume.
>
> **Beginner note:** "Silent mandates" are the classic killer — a rule appears with no explanation of *why*, so people route around it the first time it is inconvenient. Announcing the change *and its reason* is part of the work, not a nicety.

| Rollout concern | Plan |
|---|---|
| **Training** | {{How people learn the new way — e.g. a 30-min walkthrough + a one-page how-to in the repo.}} |
| **Communication** | {{How the change AND its why are announced — e.g. a short note tracing the change to FIND-1, posted before it goes live.}} |
| **Tooling / automation** | {{Tool or CI changes needed to support the new process — e.g. branch-protection rules, a release-checklist template.}} |
| **Procedure / Definition-of-Done updates** | {{Which written procedures or DoD entries change — e.g. add "reviewed by ≥1 person" to the DoD.}} |
| **Sequencing** | {{Which PI-N actions roll out in what order — e.g. PI-1 first, then PI-3 once review is habitual.}} |
| **Adoption monitoring** | {{How you confirm people actually follow the new process, not just nod — e.g. track % of merges with a review for 4 weeks post-rollout.}} |

---

## 7. Measurement

> Measurement is plainly "did the change help, and how do we know." It is the section that *closes the trace chain*: each metric here should map back to an `OBJ-N` Measure/Target from §3, so this section mirrors the objectives table with real numbers over time.
>
> **Beginner note — two traps to avoid:**
> - *Vanity metrics* — numbers that move but do not reflect the objective (e.g. "lines of code reviewed" went up, but defects did not fall).
> - *Measuring effort instead of outcome* — "we held 12 reviews" is effort; "defects fell 40%" is outcome. Always prefer the outcome number. Effort numbers are fine as supporting context, never as the headline.

### 7.1 Baselines

> The "before" numbers, captured during or from §2. **Without a baseline, improvement is unprovable** — you cannot claim a drop if you never recorded the starting height. Record the baseline value, when it was taken, and where the data came from.

| Metric | Baseline value | As of | Source |
|---|---|---|---|
| {{Production defects per release}} | {{8}} | {{YYYY-MM-DD}} | {{FIND-1 evidence / metrics export}} |
| {{Median defect time-to-fix (days)}} | {{9}} | {{YYYY-MM-DD}} | {{FIND-3 evidence}} |
| {{% releases following checklist}} | {{~40%}} | {{YYYY-MM-DD}} | {{Release log review}} |

### 7.2 Metrics tracked

> The same numbers, now tracked over time, each tied back to the objective it proves. This table is the §3 objectives table re-read through the lens of "are we there yet."

| Metric | Proves objective | Baseline | Target | Current | Trend |
|---|---|---|---|---|---|
| {{Production defects per release}} | OBJ-1 | {{8}} | {{≤3}} | {{TBD}} | {{↘ / flat / ↗}} |
| {{Median defect time-to-fix (days)}} | OBJ-2 | {{9}} | {{≤3}} | {{TBD}} | {{...}} |
| {{% releases following checklist}} | OBJ-3 | {{~40%}} | {{≥95%}} | {{TBD}} | {{...}} |

### 7.3 Cadence and review

> How often the metrics are read and who reviews them. Numbers that are collected but never looked at do not improve anything.

{{e.g. Reviewed at the end of each two-week iteration by the improvement owner; summarized for the Sponsor monthly. A metric that has not moved after {{N}} reviews triggers a re-examination of the action that was supposed to move it.}}

### 7.4 Effectiveness criteria

> How you decide the improvement actually *worked* — versus was neutral, or made things worse — and what you do in each case. Plan the "it made things worse" branch now, while you are calm, not later under pressure.

- **Worked:** {{metric reached or trended clearly toward target within the horizon → keep the change; consider promoting it to standard practice.}}
- **Neutral:** {{metric did not move → re-examine whether the action addressed the real cause (FIND-N), or whether the metric was the wrong proxy.}}
- **Harmful:** {{metric got worse, or a side effect appeared → back the change out (this is why §5 piloted it reversibly) and record the lesson in §10.}}

---

## 8. Risks

> The dominant risk in process improvement is almost always **cultural / adoption** — people resisting, or quietly ignoring the change — not technical. Do not let this table fill up only with tooling risks. A mitigation should be a *concrete action with an owner*, not a hope ("we'll communicate well" is a hope; "PI-4: run a 30-min why-this-matters session, owned by {{name}}" is a mitigation).
>
> **Beginner note:** Use the categories below as a checklist of *prompts to cover*, not as the final list — your real risks may not fit neatly. A severe `RISK-N` may warrant its own `PI-N` action in §4 to address it up front.

Categories to cover (prompts): adoption, cost, schedule, tool, cultural, quality.

| ID | Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| RISK-1 | {{Team reverts to no-review under deadline pressure (adoption/cultural)}} | {{High}} | {{High}} | {{Branch-protection makes review structural, not optional; track adoption (§6)}} | {{Name / role}} |
| RISK-2 | {{New tracker adds overhead nobody maintains (tool)}} | {{Med}} | {{Med}} | {{Pilot it (§5) before mandating; pick the lowest-friction tool}} | {{Name / role}} |
| RISK-3 | {{Improvement work crowds out delivery (schedule)}} | {{Med}} | {{High}} | {{Cap improvement effort at {{X}}% of capacity; Sponsor protects it}} | {{Sponsor}} |

---

## 9. Open Questions

> Writing down what you have NOT yet decided is itself good practice: it keeps unresolved choices from silently hardening into accidental decisions, and it tells a reviewer exactly where their input is most needed. Resolve and remove entries as the effort proceeds; you may keep resolved ones recorded for traceability.

### 9.1 Load-bearing open questions

> Things that *block committing to the plan* — these need a decision before you proceed. State what is blocking and who decides.

- **OQ-1** {{Question — e.g. Will the Sponsor protect improvement capacity from delivery pressure?}} — {{what's blocking: needs Sponsor commitment; decider: {{Sponsor}}.}}
- **OQ-2** {{Question}} — {{what's blocking, who decides.}}

### 9.2 Deferred with defaults

> Questions that have a workable default and can be revisited later if the default proves inadequate.

- **OQ-DEF-1** {{Question — e.g. Which defect tracker?}} — *default: {{the tool we already pay for; revisit if it lacks a root-cause field.}}*
- **OQ-DEF-2** {{Question}} — *default: {{default.}}*

---

## 10. Revision History

> A Process Improvement Plan is a *living document* tracked over a planning horizon. Every substantive change to objectives, actions, or measures should bump the version and add a row here, so the team can see how the improvement effort itself evolved — including the changes you backed out and why.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Current Process Assessment (even if just an honest internal review)
- §3 Improvement Objectives
- §4 Improvement Actions
- §7 Measurement (at minimum the baselines — without them improvement is unprovable)
- §10 Revision History

**Optional sections** (include if relevant):
- §5 Pilot Approach (omit only if every action is a trivial, safely-reversible config change that asks no one to work differently)
- §6 Rollout Plan (omit if the change affects only one person; otherwise keep it — silent rollouts are where improvements die)
- §8 Risks (track elsewhere if you prefer, but at least name the cultural/adoption risk)
- §9 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (the trace chain):
- FIND-N: assessment findings (a weakness in §2)
- OBJ-N: improvement objectives (the goal a finding sets, §3)
- PI-N: improvement actions (the work that achieves an objective, §4) — the suggested primary prefix
- RISK-N: risks (§8)
- OQ-N / OQ-DEF-N: open questions (load-bearing / deferred-with-defaults, §9)

The intended trace chain is **FIND-N -> OBJ-N -> PI-N -> a §7 Measurement entry that confirms it worked.** These prefixes enable cross-document traceability: an objective in this plan can be traced to the requirement or ADR that motivated it, and an action can be traced to the lifecycle process (12207) it changes.

**Tailoring:**
- The section order follows an IDEAL-style cycle (assess -> objectives -> plan/pilot -> rollout -> measure). If your improvement cycle is PDCA or custom, keep the same content but rename in the metadata `Improvement cycle` row so reviewers read the section order correctly.
- You do not need to formally rate your capability/maturity level to use this template. The ISO/IEC 330xx and CMMI levels are a shared ladder to point at ("we're roughly here, we want to be there"), not a gate you must pass through.
- **Solo developer / small team collapse:** keep §2 (be honest about what is not working), §3, §4, and §7-baselines — those four are the irreducible core ("here's the problem, here's the goal, here's the work, here's how I'll know it helped"). For a solo developer, §5 Pilot and §6 Rollout often collapse to a single sentence ("I'll try it on my next feature branch and keep it if it sticks"), the sign-off block collapses to one name, and the Sponsor is yourself. Do not drop the baseline — even solo, an unmeasured change is an unprovable one.
- A finding with no objective, or an objective with no action, is a signal the plan is incomplete — re-check the trace chain before you commit to it.

**For regulated/safety-critical projects:** use the full ISO/IEC 330xx family and/or CMMI material, not this lightweight version. Verify all level definitions, assessment requirements, and terminology against the licensed sources. This template is suitable for solo/small-team projects, internal process work, and early-stage products.
