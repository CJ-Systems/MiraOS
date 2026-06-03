# Software Quality Assurance Plan Template

> **Template purpose:** Lightweight Software Quality Assurance (SQA) Plan structure following IEEE 730-2014. An SQA Plan defines the *activities* that assure the project is following a process capable of producing quality work — audits, reviews, evaluations, nonconformance handling, metrics, and reporting. It is not a test plan: testing checks whether a specific build is defect-free; SQA checks that the right work, reviews, and evaluations are actually happening at all. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once a project is large enough — or its work is important enough — that "we'll just be careful" is no longer a sufficient quality strategy. Write it when you want a repeatable, written answer to "are we building it right, the right way?" The plan works alongside the SRS (what to build), the Design Description (how), the Test/V&V plans (does this build pass), and the Configuration Management plan (how versions are controlled). It governs the *process*; the others govern the *product*.
>
> **Companion standard:** IEEE 730-2014 — IEEE Standard for Software Quality Assurance Processes.
>
> **Status of this template:** Lightweight extract following IEEE 730-2014 (Software Quality Assurance Processes), tailored for solo/small-team use. Faithful to the standard's SQA-activity and product/process-assurance structure but reduced. Verify against the full standard for enterprise/regulated/safety-critical contexts. FLAG: IEEE 730-2014 is a paywalled IEEE standard — this template was authored from the standard's published outline and the SWEBOK Software Quality Knowledge Area, NOT by copying normative text; it reproduces no copyrighted clause language, and the section wording here is the template author's own SWEBOK-aligned paraphrase. Anyone needing conformance must purchase and verify against the actual IEEE 730-2014 document; do not treat this lightweight template as a substitute for the normative standard.

---

# Software Quality Assurance Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | SQA-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 730-2014 (lightweight) |
| Owner | {{Project name or quality owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| SQA independence model | {{Independent SQA function / Embedded reviewer / Self-audit checkpoint (solo)}} |
| Conformance basis | {{Standards, procedures, and criteria this plan holds work to — see §3}} |
| Related plans | {{Software Project Mgmt Plan / V&V Plan / Configuration Mgmt Plan / Test Plan — or "none, folded in here"}} |

---

## 1. Introduction

> This section frames the whole plan. It folds the four things every formal document opens with — purpose, scope, vocabulary, and references — into the standard SRS/SDD subsection pattern, so a reader who has seen the sibling documents will feel at home.
>
> **Software Quality Assurance (SQA)** is the discipline of assuring that the *process* the project follows is being followed and is capable of producing quality. That is different from **Quality Control (QC) / testing**, which checks whether a specific *product* (a build) is defect-free. SQA asks "are we building it right, the right way?"; testing asks "does this build work?". They are complementary, not the same thing — this document is the former.

### 1.1 Purpose

> One paragraph. State that this is the SQA Plan for {{Project Name}}, what it defines, and — for any beginner reading it — that it is *not* the test plan.

This document is the **Software Quality Assurance Plan** for **{{Project Name}}** (`SQA-{{PROJECT-ID}}-001`). It defines the SQA activities the project will perform, the standards and criteria that work will be held to, and how nonconformances and quality data are recorded and handled across the life cycle. This plan assures the project is *following a process capable of producing quality*. It is not itself the test plan — testing checks individual builds; SQA checks that the right work, reviews, and evaluations are happening at all. {{Add one sentence on what triggered writing this plan — e.g. "Written at the start of Phase 1 to make quality a defined process rather than an implicit habit."}}

### 1.2 Scope

> Define what this plan governs and what it explicitly leaves to other plans. Name the work products, processes, life-cycle phases, and (if any) suppliers it covers. State the tailoring posture honestly.

**This plan governs:**
- Work products: {{which artifacts — specs, designs, source, test reports, this plan itself}}
- Processes: {{which processes — review, change control, build/release}}
- Life-cycle phases: {{requirements / design / construction / test / maintenance — or "all phases"}}
- Suppliers/subcontractors: {{list, or "N/A — no external suppliers"}}

**This plan does not govern (lives elsewhere):**
- {{Detailed test design and execution → Master Test Plan `MTP-{{PROJECT-ID}}-001` / V&V Plan `VVP-{{PROJECT-ID}}-001`}}
- {{Version/baseline control → Configuration Management Plan `SCMP-{{PROJECT-ID}}-001`}}
- {{Schedule, budget, staffing → Software Project Management Plan}}
- {{Or: "those plans do not exist separately; their quality-relevant parts are folded into §4 and §5 of this document."}}

**Tailoring posture:** {{e.g. "Phase 1: solo-developer self-audit model. Independence (see §1.3) is achieved via defined checkpoints against a written checklist rather than a separate SQA organization. The plan scales up — add an embedded reviewer or independent function — if a second contributor joins."}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Pre-seed the terms a beginner needs so the rest of the document is readable. Define any project-specific quality terms too. Several of these terms are the load-bearing distinctions of formal quality practice — defining them once here prevents the common conflations.

| Term | Definition |
|---|---|
| SQA | Software Quality Assurance — assuring the *process* is followed and is capable of producing quality (audits, reviews, evaluations). |
| QC / testing | Quality Control — checking whether a specific *product/build* is defect-free. Complementary to SQA, not the same. |
| Verification | "Did we build the thing right?" — does each work product meet its specification / the output of the previous stage. |
| Validation | "Did we build the right thing?" — does the result meet the actual need. (Beginners routinely conflate this with verification.) |
| Work product | Any documented or built artifact the project produces — a spec, a design, source code, a test report, even this plan. Not all work products are code. |
| Process audit | An independent check that a *defined process was actually followed*, performed by someone not doing the work, so findings are objective. Contrast with a peer review, which evaluates the product. |
| Nonconformance (NC) | A found gap between what a process or work product was required to do and what it actually did. |
| Corrective action | Fixes the specific nonconformance that occurred. |
| Preventive action | Changes the process so the *class* of problem stops recurring; driven by root-cause analysis. |
| Acceptance criteria | The pre-agreed, testable conditions a work product must satisfy to be considered done/passing. |
| Independence / objectivity | Enough organizational separation that SQA can report problems without being overruled by the people whose work it evaluates. For a solo project, reframed as a defined, repeatable checkpoint. |
| Quality objective | The *goal* (e.g. "keep escaped defects low"). |
| Quality metric | The *measurement* that tells you whether you are meeting an objective. A metric without an objective is just a number; an objective without a metric is just a wish. |
| Tailoring | The sanctioned act of scaling a standard's provisions down to fit a solo/small-team project while keeping its intent. |
| {{Project term}} | {{Definition}} |

### 1.4 References

> List the documents this plan depends on, categorized like the SRS. The standards and procedures named here (and in §3) become the *conformance basis* that §3, §4, and §5 evaluate work against — so this is not a formality, it is load-bearing.

Applicable project / organizational / regulatory / contractual references:
- {{path/to/doc.md}} — {{brief description}}
- ...

Companion standard:
- IEEE 730-2014 — IEEE Standard for Software Quality Assurance Processes (paywalled; this template paraphrases its outline, see Status field).

Related plans:
- {{SPMP / V&V Plan `VVP-{{PROJECT-ID}}-001` / CM Plan `SCMP-{{PROJECT-ID}}-001` / Master Test Plan `MTP-{{PROJECT-ID}}-001` — or "none, folded in here"}}

Standards, procedures, and criteria work is held against (the conformance basis evaluated in §3 and §5):
- {{Coding standard / documentation standard / review procedure / branching workflow / ADR set — link or path}}
- ...

---

## 2. Quality Objectives

> A **quality objective** is a *goal* you can be held to; a **measure/target** is how you will know you met it; an **owner** is who is accountable for it. An objective with no measurable target is just a wish, so every objective here ties to a metric defined later in §9. Objectives usually derive from the project's non-functional / quality requirements and stakeholder needs — where an SRS or Quality Requirements Specification exists, trace back to it.
>
> Aim for **3–7 objectives** for a small project: enough to steer by, few enough to actually track. Use `OBJ-N` IDs so a review or report can cite a specific objective.

Quality objectives for {{Project Name}} derive from {{the non-functional requirements in `SRS-{{PROJECT-ID}}-001` / the Quality Requirements Specification `QR-{{PROJECT-ID}}-001` / stakeholder quality expectations}}. Each is paired with a measure and target, and traces forward to a metric in §9.

| ID | Objective | Measure | Target | Owner | Linked metric (§9) |
|---|---|---|---|---|---|
| OBJ-1 | Requirements are traceable to design and tests | Percent of requirements with a downstream link | 100% before release | {{role}} | MET-2 |
| OBJ-2 | {{Keep escaped defects low}} | {{Defects found after release}} | {{< {{n}} per release}} | {{role}} | MET-1 |
| OBJ-3 | {{Reviews happen before merge}} | {{Percent of changes peer/self-reviewed}} | {{100%}} | {{role}} | MET-3 |
| OBJ-N | {{Objective}} | {{Measure}} | {{Target}} | {{role}} | MET-N |

---

## 3. Standards, Procedures, and Criteria

> This section answers "the right way *according to what?*" SQA can only assure conformance to something written down: if a rule isn't captured somewhere, an audit can't check it. So this section names the **standards** (e.g. coding style, documentation/template conventions), the **procedures** (how reviews are run, how changes/branches are handled, how releases are cut), and the **acceptance criteria** (the testable "done" bar) that work products must meet.
>
> Use `STD-N` IDs. Everything listed here is fair game for a process audit in §6 and a work-product evaluation in §5. For a tailored solo project it is fine — and honest — for several entries to point at lightweight conventions, a CONTRIBUTING file, or ADR/memory entries rather than heavyweight org standards. Say so; a pointer to a real convention beats an aspirational standard nobody follows.

### 3.1 Product standards

> The standards a finished or in-progress artifact must conform to — what "good" looks like for the thing itself.

| ID | Standard | Applies to | Source / location |
|---|---|---|---|
| STD-1 | {{Coding style standard}} | {{Source code}} | {{linter config / style guide path}} |
| STD-2 | {{Documentation / template standard}} | {{Specs, design docs}} | {{this template set / docs/templates/}} |
| STD-3 | {{Design conventions}} | {{Architecture, module designs}} | {{ADR set / convention doc}} |

### 3.2 Process procedures

> The procedures that say *how the work is done* — these are what a process audit (§6) checks for actual compliance.

| ID | Procedure | Covers | Source / location |
|---|---|---|---|
| STD-4 | {{Review process}} | {{How reviews/inspections are run and recorded}} | {{path}} |
| STD-5 | {{Change-control / branching workflow}} | {{How commits, branches, merges are handled}} | {{CM Plan / gitflow convention}} |
| STD-6 | {{Build / release procedure}} | {{How a release is cut and verified}} | {{path}} |

### 3.3 Acceptance criteria

> The pre-agreed, testable conditions each *class* of work product must satisfy to count as done. Defining these *before* the work removes the "is this done?" argument afterward. Summarize the bar here; the per-work-product detail lives in the §5 evaluation table, which cites these `STD-N` IDs.

| ID | Work-product class | "Done" bar (acceptance criteria) |
|---|---|---|
| STD-7 | {{Requirements spec}} | {{All requirements atomic, testable, traceable}} |
| STD-8 | {{Source change}} | {{Builds clean, tests pass, reviewed, conforms to STD-1}} |
| STD-9 | {{Release}} | {{All open high-severity NCs closed; metrics within target}} |

---

## 4. SQA Activities

> This is the load-bearing section — the catalog of *what SQA actually does, when, and by whom*. SQA is a set of **recurring activities, not a one-time gate**: each activity has a *trigger* (when it fires), an *input* (what it examines), and an *output* (a record that proves it happened). Some activities are "always on" (they ride every change); others are "milestone-triggered" (they fire at a phase boundary or release).
>
> Use `ACT-N` IDs so an external test plan, V&V plan, or audit finding can cite a specific activity ("per ACT-3"). The standard activity set below is seeded for you — sections §5, §6, §7, §9, and §10 are the *deepened detail* behind these rows; this section is the index, those are the elaborations. Keep the supplier-oversight row even if it is N/A for a solo project, so the omission is a deliberate, recorded decision rather than an accidental gap.

| ID | Activity | Type | Trigger / cadence | Inputs | Output / record | Owner |
|---|---|---|---|---|---|---|
| ACT-1 | Process audits (see §6) | Process assurance | {{Milestone-based / periodic}} | {{Procedures from §3}} | {{Audit report (REC-2)}} | {{role}} |
| ACT-2 | Work-product evaluations / reviews & inspections (see §5) | Product assurance | {{Per work product / before phase exit}} | {{Work products + STD-N criteria}} | {{Evaluation result (REC-1)}} | {{role}} |
| ACT-3 | Testing oversight (see Test/V&V plan) | Product assurance | {{Per release / milestone}} | {{Test plan, test results}} | {{Confirmation test plan exists and was executed}} | {{role}} |
| ACT-4 | Supplier / subcontractor quality oversight | Process assurance | {{Per supplier deliverable}} | {{Supplier work products}} | {{Supplier evaluation}} | {{N/A — no suppliers; row kept deliberately}} |
| ACT-5 | Nonconformance management (see §7) | Both | {{On any finding}} | {{Findings from ACT-1, ACT-2, ACT-3}} | {{NC log (REC-3)}} | {{role}} |
| ACT-6 | Quality reporting & escalation (see §10) | Both | {{Per milestone / release}} | {{Audit results, open NCs, metrics}} | {{SQA report (REC-4)}} | {{role}} |

> **On ACT-3 (testing oversight):** SQA confirms that a test plan *exists* and *was executed* and that results are recorded — it does **not** run the tests itself. The actual test design and execution live in the Master Test Plan / V&V Plan (`MTP-{{PROJECT-ID}}-001` / `VVP-{{PROJECT-ID}}-001`). This keeps the SQA-vs-QC boundary clean.
>
> **Always-on vs. milestone-triggered:** {{State which activities ride every change (e.g. ACT-2 evaluation of each source change, ACT-5 logging any finding) and which fire only at milestones/releases (e.g. ACT-1 audits, ACT-6 reporting).}}

---

## 5. Work Product Evaluations

> A **work product** is any artifact the project produces — a spec, a design, source code, a test report, even this plan. A **work-product evaluation** checks an artifact against its **acceptance criteria** (the `STD-N` items from §3) using a **defined method**. Pre-naming the method, criteria, and timing is what removes the "is this done?" argument after the fact.
>
> This is the place to make **verification vs. validation** concrete: *verification* asks whether each work product meets its specification (does the design match the requirements?); *validation* asks whether the result meets the actual need (does the working system solve the real problem?). Note which evaluations are verification and which are validation.
>
> Evaluation **methods** scale with risk: a *desk-check* (quick self-read) for low-risk items, a *peer review* for normal work, a *formal inspection* (structured, role-based, defect-logging) for high-risk work products, and an *automated lint-and-test gate* for things a machine can check. Heavier methods for higher-risk products. For a small project the honest baseline is "self-review against a checklist at defined checkpoints" — say that rather than pretending to run formal inspections.
>
> Use `WPE-N` IDs, and trace each evaluation's criteria back to a `STD-N` from §3.

| ID | Work product | Method | V or V | Criteria source (STD-N) | Criteria summary | Timing | Owner |
|---|---|---|---|---|---|---|---|
| WPE-1 | SRS | Checklist self-review | Verification | STD-2, STD-7 | All requirements atomic and testable | Before design starts | {{role}} |
| WPE-2 | Design (SDD) | Peer / desk review | Verification | STD-3 | Design covers every requirement; no orphan components | Before construction | {{role}} |
| WPE-3 | Source change | Automated gate + review | Verification | STD-1, STD-8 | Builds clean, tests pass, conforms to style | Per change, before merge | {{role}} |
| WPE-4 | Release candidate | Acceptance check | Validation | STD-9 | Meets the actual stakeholder need; demo/acceptance passes | Before release | {{role}} |
| WPE-N | {{Work product}} | {{Method}} | {{V/V}} | {{STD-N}} | {{Criteria}} | {{Timing}} | {{role}} |

> **Method selection note:** {{State the project's default method and when you escalate — e.g. "Default is self-review against the relevant checklist. Escalate to peer review for changes touching {{high-risk area}} and to a structured inspection for {{the riskiest class, e.g. security-relevant or data-migration code}}."}}

---

## 6. Process Audits

> This is true-beginner formal-practice territory, so define it plainly. A **process audit** is an *independent check that a defined process was actually followed* — not whether the product is good, but whether the team did what the procedures in §3 say they'd do. "Independent" means the check is performed by someone not doing the work, so findings are objective rather than self-justifying.
>
> For a solo developer, "independent" sounds impossible — so reframe it: independence becomes a **scheduled self-audit checkpoint using a fixed checklist**, ideally at a remove (at a milestone, against the *written* procedure, recording findings *before* fixing them). The checklist is the stand-in for the independent auditor: you are auditing past-you against the written rule, not asking present-you whether present-you did fine.
>
> Audits and nonconformance handling are a pair: an audit *finds*, §7 *dispositions and closes*, and §6.6 *verifies* the fix. Findings from this section become NCs in §7.

### 6.1 Audit schedule / triggers

> When audits fire. Milestone-based, periodic, or both.

{{e.g. "One process audit at each phase exit (requirements → design → construction → release) plus a quarterly periodic audit. An unplanned audit may be triggered by a cluster of related nonconformances."}}

### 6.2 Scope

> Which procedures from §3 each audit checks. Audits need not cover everything every time — rotate or risk-prioritize.

| Audit | Procedures checked (STD-N) |
|---|---|
| {{Phase-exit audit}} | {{STD-4 review process, STD-5 change control}} |
| {{Release audit}} | {{STD-6 build/release, STD-9 acceptance}} |

### 6.3 Independence model

> Cross-reference the metadata row. State how objectivity is achieved at this project's scale.

{{e.g. "Self-audit checkpoint (solo). Objectivity comes from auditing against the *written* checklist at a milestone remove and recording findings before any fix. If a second contributor joins, audits become cross-reviews (each audits the other's process area)."}}

### 6.4 Conduct

> How the audit is run: against a checklist, evidence-based (point at the actual artifact/log, not memory).

{{e.g. "For each procedure in scope, the auditor walks the checklist, cites concrete evidence (commit history, review notes, build logs), and marks conform / nonconform / not-applicable. 'I'm pretty sure I did that' is not evidence; a link to the record is."}}

### 6.5 Reporting

> Audit findings become nonconformances per §7.

{{Each nonconforming checklist item is logged as an NC (NCR-N) in the §7 log with severity and disposition. The audit report (REC-2) summarizes conform/nonconform counts and lists opened NCs.}}

### 6.6 Follow-up

> Verifying that corrective actions from prior audits actually closed. This closes the find → disposition → close → verify loop with §7.

{{Each audit begins by re-checking that NCs opened by the previous audit are closed and verified. An NC is not closed on the word "fixed" — it is closed on evidence the fix worked (see §7.5).}}

---

## 7. Nonconformance Handling and Corrective Action

> A **nonconformance (NC)** is a found gap — a work product that fails its criteria, or a process that wasn't followed. This section defines the repeatable closed loop that catches everything §5 and §6 find, so nothing gets lost: **identify → classify → disposition → act → verify → close.**
>
> Two action types, and beginners usually only do the first: **corrective action** fixes *this* instance; **preventive action** changes the process so the whole *class* of problem stops recurring, driven by **root-cause analysis** (asking "why did this happen?" until you reach a process cause, not just a surface symptom). The signal that you need preventive action is a *recurring* NC — the same kind of gap appearing again means the process, not just the artifact, is broken.
>
> Use `NCR-N` IDs. Keep the severity scheme small (2–3 levels) for a small project — more levels than you will actually act on differently is wasted ceremony.

### 7.1 Identification & logging

> Where NCs are recorded. Tie to the §8 quality records.

{{All NCs are logged in {{the NC log REC-3 — location: issue tracker label / docs/quality/nc-log.md / ...}}. An NC can be raised by any SQA activity (ACT-1 audit, ACT-2 evaluation, ACT-3 testing oversight) or ad hoc by anyone who spots a gap.}}

### 7.2 Classification

> A small severity/priority scheme. Keep it to 2–3 levels.

| Severity | Meaning | Handling |
|---|---|---|
| {{High}} | {{Blocks release / risks correctness or safety}} | {{Stop-and-decide; must close before proceeding (see §10.3)}} |
| {{Medium}} | {{Should fix, doesn't block immediately}} | {{Disposition with owner + date}} |
| {{Low}} | {{Minor / cosmetic}} | {{Fix opportunistically or waive with rationale}} |

### 7.3 Disposition options

> What can happen to an NC once classified.

- **Fix now** — corrective action taken immediately.
- **Waive with rationale** — accepted as-is; record *why* it is acceptable and who approved.
- **Defer** — fix scheduled later; record owner and target date so it cannot silently vanish.

### 7.4 Corrective vs. preventive action

> When root-cause analysis is warranted.

{{Every NC gets a corrective action (fix this instance). Preventive action is warranted when an NC *recurs* or is severe: do a brief root-cause analysis, then change the relevant procedure in §3 (or add a missing one) so the class stops recurring. Record the process change as the preventive action on the NC.}}

### 7.5 Closure & verification

> An NC is not closed until the fix is verified. Links back to §6.6.

{{An NC moves to "closed" only when its corrective action has been verified — re-evaluated against the same criteria that flagged it (re-run the test, re-check the checklist item). The verifier is recorded. Verification of audit-raised NCs is re-checked at the next audit (§6.6).}}

**Minimal NC record template:**

| Field | Example |
|---|---|
| ID | NCR-1 |
| Found by (activity) | ACT-1 (process audit) |
| Description | {{What gap was found}} |
| Severity | {{High / Medium / Low}} |
| Disposition | {{Fix now / Waive / Defer}} |
| Action (corrective / preventive) | {{What was done}} |
| Owner | {{role}} |
| Status | {{Open / In progress / Verified / Closed}} |
| Closed date | {{YYYY-MM-DD}} |

---

## 8. Quality Records

> The plain truth here: **if it isn't recorded, the audit can't prove it happened.** Quality records are the durable evidence that the SQA activities in §4 actually occurred — review notes, audit findings, the NC log, metric snapshots, sign-offs. This section says *which* records are kept, *where*, in *what form*, and for *how long*.
>
> Use `REC-N` IDs. On **retention**: records support traceability and post-mortems, but indefinite hoarding has cost, so pick a period proportionate to the project (e.g. "life of project + one release" for a solo effort). On **location**: for a docs-and-repo project it is entirely legitimate for "location" to be the repository, the docs tree, or the ADR set rather than a formal records system — but it must still be *named*, not implicit.

| ID | Record | Produced by (ACT-N) | Location / format | Retention | Owner |
|---|---|---|---|---|---|
| REC-1 | Review / evaluation results | ACT-2 | {{PR threads / docs/quality/reviews/}} | {{Life of project + 1 release}} | {{role}} |
| REC-2 | Audit reports | ACT-1 | {{docs/quality/audits/}} | {{Life of project + 1 release}} | {{role}} |
| REC-3 | Nonconformance log | ACT-5 | {{Issue tracker label / docs/quality/nc-log.md}} | {{Life of project}} | {{role}} |
| REC-4 | Metrics history | ACT-6 | {{docs/quality/metrics.md / CI dashboard}} | {{Life of project}} | {{role}} |
| REC-5 | This plan's revision history | — | §12 of this document | {{Life of project}} | {{role}} |

---

## 9. Quality Metrics

> A **metric** is the number that tells you whether an **objective** (from §2) is being met. The two are bound: a metric with no objective is noise; an objective with no metric can't be verified. So every metric here traces to an `OBJ-N`, and carries a **target/threshold** so a single reading can be judged pass or fail.
>
> Steer toward **few, cheap-to-collect, decision-driving** metrics for a small team. Two beginner traps to avoid: **vanity metrics** (numbers that look good but change no decision) and **gameable metrics** (anything that, once it becomes a target, can be hit by gaming rather than by real improvement — e.g. "lines of code" or "number of commits"). Prefer metrics that ride existing tooling — git history, the issue tracker, CI output — over metrics that require manual bookkeeping nobody will sustain.
>
> Use `MET-N` IDs and trace each to the objective it serves.

| ID | Metric | Definition | Serves objective (OBJ-N) | Target / threshold | Collection method | Frequency |
|---|---|---|---|---|---|---|
| MET-1 | Escaped defects per release | Defects found after a release shipped | OBJ-2 | {{< {{n}}}} | {{Issue tracker label}} | Per release |
| MET-2 | Requirements-traceability coverage | Percent of requirements with a downstream design+test link | OBJ-1 | 100% before release | {{Traceability matrix / script}} | Per milestone |
| MET-3 | Review findings per work product | Findings raised per reviewed artifact | OBJ-3 | {{Trend, not a hard cap}} | {{From REC-1}} | Per work product |
| MET-4 | NC closure time | Median days from NC open to verified-closed | {{OBJ-N}} | {{< {{n}} days for High}} | {{From REC-3}} | Per milestone |
| MET-N | {{Metric}} | {{Definition}} | {{OBJ-N}} | {{Target}} | {{Method}} | {{Frequency}} |

> **Worked linkage:** MET-2 (requirements-traceability coverage) serves OBJ-1 ("requirements are traceable to design and tests"). When MET-2 reads below its 100% target, OBJ-1 is not being met, which is itself a nonconformance (raise an NCR-N per §7) and a reporting/escalation trigger (§10).

---

## 10. Reporting and Escalation

> SQA only adds value if its findings are **seen and acted on** — a finding nobody reads is wasted effort. This section defines the reports SQA produces, who receives them and how often, and the **escalation path** when a nonconformance or metric breach can't be resolved at the working level.
>
> For a solo project, "escalation" has no manager to escalate *to* — so reframe it as a **decision trigger**: a defined severity or threshold breach means *stop and decide before proceeding* rather than "email someone." That keeps the safeguard without inventing a hierarchy that doesn't exist.
>
> This section is the elaboration behind activity ACT-6 (§4), and it ties to the metric thresholds in §9: a threshold breach is a reporting/escalation trigger.

### 10.1 Reports

> What SQA report exists and what it contains — typically a roll-up.

{{A single SQA report (REC-4) is produced per {{milestone / release}}. It rolls up: §6 audit results (conform/nonconform counts), §7 open NCs (by severity), and §9 metric readings against their targets. One page is plenty for a small project — the report is a decision aid, not a deliverable in its own right.}}

### 10.2 Cadence & audience

> When reports are produced and who reads them.

| Report | Cadence | Audience |
|---|---|---|
| {{SQA roll-up}} | {{Per milestone / per release}} | {{Owner / stakeholders / "self, recorded for traceability"}} |

### 10.3 Escalation path

> When and how an unresolved or high-severity finding is escalated — or, for a solo project, what severity forces a stop-and-decide.

{{e.g. "Any High-severity NC (§7.2) that cannot be closed before the next phase or release is a stop-and-decide trigger: do not proceed until it is fixed, waived with explicit recorded rationale, or formally deferred with an owner and date. In a multi-person setup, escalate unresolved High NCs to {{the approval authority}}."}}

### 10.4 Management visibility / sign-off touchpoints

> Where quality information meets a go/no-go decision.

{{e.g. "The SQA roll-up is reviewed at each phase-exit and release sign-off. Sign-off (the metadata 'Approved by' authority, or the solo developer's recorded go/no-go) requires no open High-severity NCs and all §2 objectives within target."}}

---

## 11. Open Questions

> It is healthier for a lightweight plan to openly carry unresolved provisions than to fake completeness — name what is still soft and what would force a decision, rather than pretending every choice is final. Split into items you have a working default for (revisit only if the default proves inadequate) and items you have since resolved (kept for traceability). Resolve and migrate items as the project matures.

### 11.1 Deferred with defaults

- **OQ-DEF-1** Independence model — *default: self-audit checkpoint (solo). Revisit if a second contributor joins, at which point audits become cross-reviews.*
- **OQ-DEF-2** {{Severity scheme granularity}} — *default: {{three levels (High/Medium/Low)}}. Revisit if {{a level is never used or the team needs finer prioritization}}.*
- **OQ-DEF-N** {{Question}} — *default: {{default}}.*

### 11.2 Resolved (recorded for traceability)

- **OQ-1** {{Question}}: {{Resolution}}.
- ...

---

## 12. Revision History

> Revision history is mandatory for a quality document: the plan that *governs* traceability must itself be traceable. Every substantive change to objectives, standards, or activities gets a version bump and a row.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Quality Objectives
- §3 Standards, Procedures, and Criteria (the conformance basis — without it, nothing else is checkable)
- §4 SQA Activities
- §7 Nonconformance Handling and Corrective Action
- §12 Revision History

**Optional sections** (include if relevant):
- §5 Work Product Evaluations (fold into §4 if the project has only one or two work-product classes)
- §6 Process Audits (defer if the project is too early to have an audit-able process yet; add as soon as procedures exist)
- §8 Quality Records (can be a single line — "records live in the repo and issue tracker" — for the smallest projects, but name the location)
- §9 Quality Metrics (omit numeric targets if too early, but keep at least the objectives in §2)
- §10 Reporting and Escalation (collapse to a decision-trigger note for solo work)
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (for cross-document traceability):
- `SQA-{{PROJECT-ID}}-NNN`: the document itself and individual plan provisions
- `ACT-N`: SQA activities (audits, evaluations, testing oversight, supplier oversight, NC management, reporting)
- `OBJ-N`: quality objectives (§2)
- `STD-N`: standards / procedures / criteria — the conformance basis (§3)
- `WPE-N`: work product evaluations (§5)
- `NCR-N`: nonconformance records / dispositions (§7)
- `REC-N`: quality records (§8)
- `MET-N`: quality metrics (§9)
- `OQ-N` / `OQ-DEF-N`: open questions (resolved / deferred-with-defaults) (§11)

These prefixes let a sibling document cite a specific provision — an external test plan, V&V plan, or audit finding can reference "per ACT-3" or "fails WPE-2 criteria" and resolve cleanly back to this plan.

**Tailoring**:
- IEEE 730 is written for organizations with a separate SQA function. The biggest tailoring move is **independence**: where the standard expects an independent SQA department, a solo/small-team project substitutes a *defined, repeatable self-audit checkpoint against a written checklist* (see §6.3). The checklist is the stand-in for the independent auditor.
- **Solo-developer collapse:** keep §2 (objectives), §3 (what you hold work to), §4 (activities, even if several owners are all "you"), and §7 (the NC loop). §5 can fold into §4; §6 audits become milestone self-checks; §8 records can be "the repo and issue tracker"; §9 can be two or three metrics that ride git/CI; §10 escalation becomes a stop-and-decide rule. The discipline that survives the collapse is: *write down what good means, check against it on a schedule, log the gaps, and close them with evidence.*
- **Small-team collapse:** assign owners across people, make §6 audits reciprocal (each person audits the other's process area — that restores real independence cheaply), and keep the §10 report to one page per milestone.
- Don't grow the plan beyond what you will actually execute. An aspirational plan nobody follows is itself a nonconformance — the §3 conformance basis would flag it.

**For regulated/safety-critical projects:** use the full IEEE 730-2014, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products; it deliberately omits the standard's heavier provisions (formal independent SQA organization, full activity-by-life-cycle-process mapping, and the normative conformance requirements). Conformance claims must be verified against the purchased standard.
