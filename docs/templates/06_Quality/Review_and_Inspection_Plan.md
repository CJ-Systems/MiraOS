# Review and Inspection Plan Template

> **Template purpose:** Lightweight Review and Inspection Plan structure inspired by IEEE 1028-2008 (Software Reviews and Audits). Use this template to write the *plan* that governs how work products on a project are reviewed and inspected — which review types are used, who plays which role, what makes a product ready to review, the procedure each review follows, the criteria reviewers apply, how findings are classified, and what records and metrics are kept. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once a project has work products worth examining before they reach testing or release (a Software Requirements Specification, a design, code, test plans). Write this plan once, early; then run individual reviews against it. This plan does **not** record the outcome of any single review — those are separate review records (and, for audits, the Audit Report). Think of it as the rulebook, not the scorecard.
>
> **Companion standard:** IEEE 1028-2008 — IEEE Standard for Software Reviews and Audits (defines the five review/audit types: management review, technical review, inspection, walk-through, and audit, and the procedures, roles, entry/exit criteria, and recorded outputs for each).
>
> **Status of this template:** Lightweight skeleton derived from the publicly documented structure of IEEE 1028-2008 (Software Reviews and Audits) — the five review/audit type names (management review, technical review, inspection, walk-through, audit), the role set, the entry/exit-criteria and procedure framing, and the recorded-output expectations are widely published, but the standard itself is paywalled and copyrighted by IEEE. No normative text is reproduced here; all guidance is paraphrase. Verify the type definitions, mandatory procedure steps, required record contents, and role responsibilities against the full IEEE 1028-2008 document before relying on this for regulated, safety-critical, contractual, or certification contexts. For solo/small-team and internal use this skeleton is sufficient as-is.

---

# Review and Inspection Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | RI-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 1028-2008 (lightweight, paraphrased — see status note) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Plan type | Review and Inspection Plan (governs the review process; individual review outcomes are recorded separately as review records / an Audit Report) |
| Companion SRS / SDD | {{SRS-{{PROJECT-ID}}-001 / SDD-... — the work products this plan governs reviews of}} |
| Companion V&V / Test Plan | {{VV-{{PROJECT-ID}}-001 / TP-... — reviews are the static-verification arm of overall V&V}} |
| Review types in use | {{which of the five IEEE 1028 types this project actually uses — e.g., Inspection + Technical Review + Walk-through; Management Review and Audit out of scope}} |
| Records location | {{where review records, findings logs, and metrics are stored and retained}} |
| Process owner | {{who owns and tailors the review process — often the quality lead or moderator}} |

---

## 1. Introduction

> This document is the *plan* for how work products on {{Project Name}} are reviewed and inspected. It defines which review types are used, who plays which role, what makes a product ready to review, the procedure each review follows, the criteria reviewers apply, how findings are classified, and what records and metrics are kept. It does **not** record the outcome of any single review — those live in separate review records (and, for an audit, in the Audit Report). This whole section folds Purpose, Scope, Definitions, and References into one introduction, matching the sibling SRS/SDD/Quality templates.

This document specifies how work products on **{{Project Name}}** are reviewed and inspected. It is the authoritative source for *how reviews are run* on this project: it names the review types in use, the roles people play, the readiness gates a product must pass, the step-by-step procedure each review follows, the quality criteria reviewers apply, the way findings are classified and dispositioned, and the records and metrics that are kept. It is the rulebook; the scorecards (individual review records and the Audit Report) are separate artifacts.

### 1.1 Purpose

> Why this plan exists. State the three things a review plan buys you: defects caught early through *static* examination (before they reach test or the field), a repeatable and fair process (so two reviewers reach comparable results), and the verification arm of the project's overall V&V (verification and validation). Make clear this is the single authoritative source for how reviews are run here.

{{This plan exists to:}}

- **Catch defects early through static examination.** A *review* examines a work product by reading and inspecting it — no execution. (Contrast with *testing*, which runs the software; see §1.3.) Defects found in a requirements document or a design cost far less to fix than the same defect found after it has been built, tested, and shipped. Reviews also catch defects in artifacts that *cannot be run at all* — requirements, plans, designs.
- **Establish a repeatable, fair review process.** Without an agreed procedure and explicit criteria, "review the document" means something different to every reviewer. This plan makes reviews repeatable so their results are comparable and trustworthy.
- **Satisfy the verification arm of V&V.** Reviews are primarily *verification* — "are we building the product right" (does it meet its specification and conform to its standards). They are the static-verification half of overall V&V; dynamic testing is the other half and lives in the {{Test Plan / V&V Plan}}.

This plan is the authoritative source for how reviews are conducted on {{Project Name}}. Individual review outcomes are recorded elsewhere (§9).

### 1.2 Scope

> What this plan covers and what it deliberately excludes. Covers: the review process and the work products subject to it. Excludes: dynamic testing (that is the Test Plan's job — this is the *static*-verification side). Name which of the five IEEE 1028 types are in scope and which are out, so a reader knows what to expect.

**In scope:**
- The review process for {{Project Name}} — types, roles, entry/exit criteria, procedure, criteria, finding classification, records, and metrics.
- The work products subject to review (enumerated in §2).

**Out of scope:**
- **Dynamic testing** (executing the software to find defects) — that belongs to the {{Test Plan / V&V Plan}}. This plan is the *static*-verification side only.
- {{Any work products explicitly excluded from review — see §2 for the list and rationale.}}

**IEEE 1028 review/audit types in scope for this project:** {{e.g., Inspection, Technical Review, Walk-through}}.
**Types out of scope:** {{e.g., Management Review — handled by {{project management process}}; Audit — none planned, or handled separately via the Audit Report template}}. Each in/out decision is justified in §3.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define each term the first time a reader would otherwise have to guess. This is where the core concepts land in plain English — the five review types, the anomaly/defect/finding distinction, entry/exit criteria, severity vs. priority, disposition, DRE, and moderator independence. Add or remove rows to fit the project.

| Term | Definition |
|---|---|
| Management review | A review where **managers** check progress, resourcing, and risk against the plan and decide what happens next. About steering the project, not examining a work product line by line. |
| Technical review | A review where **qualified peers** evaluate whether a work product meets its specifications and conforms to applicable standards. The peers, not managers, reach the technical conclusion. |
| Inspection | The most rigorous review type: a **role-based, defect-finding** examination with formal entry/exit criteria, a trained and neutral moderator, individual preparation, and a structured meeting. The goal is to *find* defects, not to discuss fixes. |
| Walk-through | A **lighter, author-led** review in which the author leads peers through the product to gather feedback and educate. Less formal than an inspection; useful early or for shared understanding. |
| Audit | An **independent** evaluation of conformance to requirements, standards, and procedures, usually performed by someone outside the team. An audit produces its own output — the Audit Report (a separate template). |
| Static evaluation | Examining a work product by reading/inspecting it, with no execution. All reviews in this plan are static. |
| Dynamic testing | Running the software to observe behavior. Out of scope here (see §1.2); it lives in the Test Plan. |
| Work product | Any artifact subject to review — a document, model, code, test, plan, or configuration. |
| Anomaly | Anything observed that departs from expectation. Not yet confirmed to be a real flaw. |
| Defect | A confirmed flaw in a work product — an anomaly that has been validated as a genuine problem. |
| Finding | The neutral umbrella term for anything a review records (anomaly, confirmed defect, question, or even a positive observation). We avoid the word "bug" for non-code artifacts. |
| Entry criteria | The readiness gate: conditions a work product must meet **before** a review starts (e.g., spell-checked, complete, prior dependent reviews closed). |
| Exit criteria | The conditions that must hold **before** a review is declared complete (e.g., all major findings dispositioned, rework verified, record filed). |
| Severity | How bad a defect's impact would be if it shipped (e.g., Critical / Major / Minor / Cosmetic). |
| Priority | How soon a finding should be fixed. A *different axis* from severity — a Minor finding can be high-priority and vice versa. |
| Disposition | The decision recorded about each finding: fix, defer, reject (not a real defect), or duplicate. Every finding gets one so none are silently dropped. |
| Moderator independence | The rule that the person running an inspection or audit is **not** the author of the work being examined, so the examination stays objective. |
| DRE (Defect Removal Effectiveness) | The percentage of defects caught by reviews before they escape to a later phase: defects-found-in-review ÷ (defects-found-in-review + defects-found-later) × 100. |
| Defect density | Confirmed defects per unit of size (per page, per KLOC), so review yield can be compared across differently sized products. |
| V&V | Verification and Validation. Reviews are the *verification* / static arm; testing and audits round out the rest. |
| {{Term}} | {{Definition}} |

### 1.4 References

> List the documents this plan depends on or coordinates with. Beginner-facing point worth stating outright: a Software Requirements Specification (SRS) says **what** the system must do; a review *checks the SRS against criteria* — the review does not produce the product, it examines it. Categorize the references for readability.

Project work products this plan governs reviews of:
- {{SRS-{{PROJECT-ID}}-001}} — Software Requirements Specification ({{the "what" document; a requirements review checks it against the §7 criteria}})
- {{SDD-{{MODULE-ID}}-001}} — Software Design Description ({{the "how" document}})
- {{path/to/other/work-product}} — {{description}}

Plans this plan complements:
- {{VV-{{PROJECT-ID}}-001 / Test Plan}} — overall V&V; this plan is its static-verification arm
- {{Audit Report template}} — where audit outcomes are recorded (an audit's record *is* its report)

Decisions that fix a review policy:
- ADR-NNNN — {{e.g., "security-relevant modules require an independent inspector"}}

External standards:
- IEEE 1028-2008 — IEEE Standard for Software Reviews and Audits ({{paraphrased here; verify against the full standard for regulated use}})

---

## 2. Review Scope and Work Products

> A review needs a concrete *thing* to examine. This section names the work products that will be reviewed, the review type applied to each, and the trigger (when the review fires). Just as important: name what is **not** reviewed and why — deliberate tailoring keeps the process affordable, and a stated omission stops a future reader from mistaking it for an oversight. Not everything warrants the heaviest review: a one-page README does not need a formal inspection, while the SRS or a security-relevant module does. Each row gets an RI-N ID so a later review event (REV-N) can cite which planned scope it satisfies.

The following work products are subject to review on {{Project Name}}. "Rigor" indicates how heavy the review is (inspection = heaviest; walk-through = lightest — see §3).

| ID | Work product | Review type(s) | Trigger / when | Rigor |
|---|---|---|---|---|
| RI-1 | {{Software Requirements Specification (SRS)}} | {{Inspection}} | {{Before baseline}} | {{Inspection}} |
| RI-2 | {{Software Design Description (SDD)}} | {{Technical Review}} | {{At design phase gate}} | {{Technical review}} |
| RI-3 | {{Security-relevant module / code}} | {{Inspection}} | {{On pull request}} | {{Inspection}} |
| RI-4 | {{General application code}} | {{Walk-through / Technical Review}} | {{On pull request}} | {{Walk-through}} |
| RI-5 | {{Test Plan}} | {{Technical Review}} | {{Before test execution starts}} | {{Technical review}} |
| RI-N | {{Work product}} | {{Type}} | {{Trigger}} | {{Rigor}} |

**Deliberately out of review scope** (tailoring rationale, so the omission is not read as an oversight):
- {{README / changelog / scratch notes}} — {{too low-risk to warrant a formal review; a quick author self-check suffices}}
- {{Generated or vendored artifacts}} — {{not authored here; reviewed upstream}}
- {{...}}

---

## 3. Review Types

> This is the core domain section and maps directly to IEEE 1028's five review/audit types. For each type the project uses, a short subsection states what it is, who decides/attends, its purpose, its rigor level, and when this project uses it. The point of separating them is so the reader picks the right tool: a defect-hunting inspection is overkill for a friendly walk-through, and a walk-through will not give an SRS the scrutiny it needs. State explicitly which types are in scope and which are out, each with a one-line reason. Note that an **audit** has its own output — the Audit Report — which is a separate template.

The five IEEE 1028 review/audit types, summarized, then detailed for the ones this project uses:

| Type | Leader | Participants | Purpose | Formality | This project |
|---|---|---|---|---|---|
| Management review | Manager | Managers, project lead | Progress, resourcing, risk vs. plan | Medium | {{In / Out — reason}} |
| Technical review | Neutral peer / lead | Qualified peers | Does the product meet spec and standards? | Medium–High | {{In / Out — reason}} |
| Inspection | Trained moderator (not the author) | Inspectors in defined roles | Rigorous defect-finding | Highest | {{In / Out — reason}} |
| Walk-through | The author | Peers | Feedback + education | Low | {{In / Out — reason}} |
| Audit | Independent auditor (often external) | Auditor + auditee | Conformance to requirements/standards/procedures | High (independent) | {{In / Out — reason — note output is the Audit Report}} |

### 3.1 {{Inspection}}

> The most rigorous type. Role-based, with a trained and neutral moderator, formal entry/exit criteria, individual preparation, and a structured meeting whose job is to *find* defects — not to fix them or to discuss the author's style. Reserve for the highest-risk products.

- **What it is:** {{a rigorous, role-based defect-finding examination}}
- **Who leads / attends:** {{a trained moderator who is not the author; inspectors in the defined roles (§4)}}
- **Purpose:** {{find defects in high-risk products before they escape}}
- **Rigor:** Highest.
- **When this project uses it:** {{the SRS, security-relevant modules — see §2}}

### 3.2 {{Technical Review}}

> Qualified peers judge whether the product meets its specification and conforms to standards. The technical conclusion is theirs, not a manager's.

- **What it is:** {{a peer evaluation of conformance to spec and standards}}
- **Who leads / attends:** {{a neutral peer or lead; qualified peers}}
- **Purpose:** {{confirm the product meets its specification}}
- **Rigor:** Medium–High.
- **When this project uses it:** {{the SDD, the Test Plan — see §2}}

### 3.3 {{Walk-through}}

> The lighter, author-led type. The author leads peers through the product to gather feedback and educate the team. Good for early drafts and for spreading understanding; not a substitute for an inspection on high-risk products.

- **What it is:** {{an author-led walk-through for feedback and education}}
- **Who leads / attends:** {{the author leads; peers attend}}
- **Purpose:** {{gather feedback, share understanding}}
- **Rigor:** Low.
- **When this project uses it:** {{general application code, early drafts — see §2}}

### 3.4 {{Types out of scope}}

> State each excluded type and the one-line reason, so the choice is documented rather than implied.

- **Management review — {{Out}}.** {{Handled by the existing project-management cadence, not as a formal IEEE 1028 review.}}
- **Audit — {{Out / handled separately}}.** {{No internal audits planned; if an audit is performed, its outcome is recorded in the Audit Report template (AUD-{{PROJECT-ID}}-001), not here.}}

---

## 4. Roles and Responsibilities

> A review is fair and effective only when responsibilities are explicit. On a small team one person can wear two hats — with one hard rule: the **author must not moderate or lead the inspection/audit of their own work** (independence keeps the examination objective). The Manager role appears only in management reviews; it is not present in technical sessions. Use ROLE-N IDs so a review record can cite who held which role.

| ID | Role | Responsibility | May also hold | Independence rule |
|---|---|---|---|---|
| ROLE-1 | Author | Created the work product; answers questions; performs rework on findings (§6). | Recorder (in a small team) | **Must not** moderate/lead the inspection or audit of their own work. |
| ROLE-2 | Moderator / Leader | Runs the review neutrally; keeps it on procedure; ensures findings are logged, not debated into fixes; checks entry/exit criteria. | Reviewer | Should not be the author. |
| ROLE-3 | Inspection Leader / Audit Lead | For inspections/audits specifically: a Moderator with the added duty of enforcing the formal entry/exit gates and independence. | Reviewer | **Must** be independent of the author. |
| ROLE-4 | Reviewer / Inspector | Examines the product during preparation and the meeting; raises findings (FND-N). | Recorder | — |
| ROLE-5 | Recorder / Scribe | Logs each finding with its classification and disposition into the review record. | Reviewer, Author | — |
| ROLE-6 | Manager | Decides on management reviews (resourcing, go/no-go). **Not present** in technical reviews, inspections, or walk-throughs. | — | — |

**Solo / small-team tailoring.** When the team is one or two people, preserve the *spirit* of independence rather than the headcount:
- **Review across a time gap** — let a draft cool for {{a day or more}}, then review it as if it were someone else's work.
- **Invite an outside peer** for high-stakes products (the SRS, security-relevant code) so the inspection has a genuinely independent leader.
- One person legitimately holds several roles at once — Author + Recorder, or Moderator + Reviewer — **except** Author + Inspection Leader of the same product, which breaks the one hard rule.

---

## 5. Entry Criteria

> Entry criteria are the readiness gate — the checklist a work product must pass before reviewers spend time on it. Their job is to stop a review from being wasted on an obviously-unready draft. An inspection has stricter entry criteria than a walk-through. Each criterion gets a CRIT-N ID so completion can be recorded against it. The most important beginner point: if a product **fails** entry criteria, the review is **postponed, not run-and-failed**. Running a review on material that was not ready is a common first-timer mistake — it burns reviewer time and produces findings that are just "this isn't finished."

A review of {{work product}} may begin only when these criteria are met. Stricter criteria apply to the heavier review types (mark which apply to which type).

| ID | Entry criterion | Applies to |
|---|---|---|
| CRIT-1 | {{The work product is complete and internally self-consistent (no obvious gaps or contradictions).}} | All |
| CRIT-2 | {{The product passes automated checks — spell-check, lint, build — as applicable.}} | All |
| CRIT-3 | {{All prior dependent reviews are closed (e.g., the SRS inspection closed before the SDD review opens).}} | All |
| CRIT-4 | {{Reviewers have received the product with adequate preparation time before the meeting.}} | Inspection, Technical Review |
| CRIT-5 | {{The applicable §7 review checklist for this work-product type has been identified.}} | Inspection, Technical Review |
| CRIT-6 | {{A neutral moderator / inspection leader independent of the author is assigned.}} | Inspection |
| CRIT-N | {{Project-specific entry criterion}} | {{Type}} |

**If entry criteria are not met, the review is *postponed*, not conducted.** Record the unmet criterion (by CRIT-N), return the product to the author, and reschedule once it is ready. This protects reviewer time and keeps findings about real defects rather than incompleteness.

---

## 6. Review Procedure

> This is the second core domain section: the standard review lifecycle as ordered phases, so a first-timer can run one end to end. The phases are Planning, Overview/Kickoff (optional), Preparation, Meeting/Examination, Rework, and Follow-up/Closure. Three rules matter most for beginners: (1) **most defects are found in Preparation**, before the meeting — do not skip it; (2) the meeting's job is to *find* defects, **not fix them** — solution discussion derails the meeting and eats time the whole group is paying for; (3) **do not close while major findings are open**. A review event is identified as REV-N; findings raised in it are FND-N. Exit criteria live at the end of this section (§6.7).

### 6.1 Planning

> Pick the product, the type, and the participants; schedule the review.

The moderator (ROLE-2) confirms the work product, selects the review type (§3), assigns roles (§4), picks the applicable checklist (§7), and schedules the review. **Produces:** a scheduled review event with a unique ID (REV-N) and named participants.

### 6.2 Overview / Kickoff (optional)

> A brief orientation so reviewers know what they are looking at. Optional for familiar products; useful for novel or complex ones.

The author (ROLE-1) or moderator briefly orients reviewers to the product, its context, and the focus of the review. **Produces:** shared understanding; can be skipped for routine reviews.

### 6.3 Preparation

> The phase where most defects are actually found. Reviewers examine the product *individually*, against the checklist, and note findings **before** the meeting. Skipping this is the single biggest cause of weak reviews.

Each reviewer (ROLE-4) examines the product on their own, applies the §7 criteria, and records candidate findings (anomalies) ahead of the meeting. Preparation time is captured as a metric (§10) precisely because too little of it predicts a weak review. **Produces:** per-reviewer lists of candidate findings.

### 6.4 Meeting / Examination

> Findings are raised and logged. The rule: *find* defects, do not fix them. Logging a finding and moving on keeps the meeting productive; chasing a solution stalls everyone.

The moderator runs the meeting; reviewers raise their candidate findings; the recorder (ROLE-5) logs each as FND-N with a preliminary classification (§8). The group confirms whether each anomaly is a genuine defect. **Solution discussion is deferred to rework** — the meeting finds, it does not fix. **Produces:** a logged list of findings (FND-N) against the review event (REV-N).

### 6.5 Rework

> The author dispositions and fixes the findings. This is where solutions are actually designed and applied.

The author (ROLE-1) works through each finding, assigns or confirms its disposition (§8 — fix / defer / reject / duplicate), and applies fixes for those dispositioned "fix." A rejected finding is recorded with a reason, not deleted. **Produces:** an updated work product and a disposition for every FND-N.

### 6.6 Follow-up / Closure

> The moderator verifies the rework and checks the exit criteria. Only then is the review complete.

The moderator confirms that reworked findings were actually addressed, that every finding has a disposition, and that the exit criteria (§6.7) hold. The review record is filed (§9). **Produces:** a closed review event (REV-N) with a complete record and verified rework.

### 6.7 Exit Criteria

> The conditions that must hold to declare the review complete. These mirror the entry criteria (§5) in spirit — a gate, but at the end. The headline rule: do not close while a major finding is still open. Use CRIT-N IDs so closure can be recorded against each.

A review may be declared complete only when:

| ID | Exit criterion |
|---|---|
| CRIT-7 | {{Every finding (FND-N) has a recorded disposition (§8) — none silently dropped.}} |
| CRIT-8 | {{All Critical and Major findings are either fixed-and-verified or formally deferred with an owner and date.}} |
| CRIT-9 | {{Rework has been verified by the moderator (not merely claimed by the author).}} |
| CRIT-10 | {{The review record is filed in the records location and the metrics (§10) are captured.}} |
| CRIT-N | {{Project-specific exit criterion}} |

**Beginner pitfalls to avoid:** do not fix in the meeting (§6.4); do not skip preparation (§6.3); do not close while a major finding is open (CRIT-8).

---

## 7. Review Criteria and Checklists

> "Review the document" is not actionable. A checklist of explicit criteria is what makes a review repeatable and lets two reviewers reach comparable results — it is where reviewers' attention is focused, so it is worth depth. The standard quality dimensions are below, each with a one-line plain definition. Checklists should be **tailored per work-product type**: a requirements inspection checklist asks different questions than a code inspection checklist. Keep type-specific checklists as appendices or linked files and reference them here. Each checklist item gets a CRIT-N ID so a finding can cite the criterion it failed.

The quality dimensions reviewers apply (plain definitions):

- **Correctness** — says true things; statements match reality and intent.
- **Completeness** — nothing required is missing.
- **Consistency** — no internal contradictions; terms used the same way throughout.
- **Feasibility** — can actually be built within the project's constraints (time, budget, technology).
- **Traceability** — each item links to its source (a requirement) and/or its derivatives (design, tests).
- **Testability** — each requirement can be objectively verified (you can write a test or check that decides pass/fail).
- **Maintainability** — a future reader/maintainer can follow it.
- **Compliance** — conforms to applicable standards and regulations.

Example checklist (tailor per work-product type — this row set is for a **requirements** review):

| ID | Dimension | Checklist question (requirements example) | Pass/Fail/N-A |
|---|---|---|---|
| CRIT-11 | Correctness | {{Does each requirement state something true and intended?}} | {{ }} |
| CRIT-12 | Completeness | {{Are all required behaviors, constraints, and interfaces present?}} | {{ }} |
| CRIT-13 | Consistency | {{Are there any contradicting requirements or inconsistent terms?}} | {{ }} |
| CRIT-14 | Feasibility | {{Can each requirement be built within the stated constraints?}} | {{ }} |
| CRIT-15 | Traceability | {{Does each requirement link to its source and (where applicable) a test?}} | {{ }} |
| CRIT-16 | Testability | {{Can each requirement be objectively verified?}} | {{ }} |
| CRIT-17 | Maintainability | {{Can a new reader follow the document without tribal knowledge?}} | {{ }} |
| CRIT-18 | Compliance | {{Does it conform to applicable standards/regulations?}} | {{ }} |
| CRIT-N | {{Dimension}} | {{Type-specific question}} | {{ }} |

**Type-specific checklists** (link or appendix):
- {{Requirements review checklist}} — {{path/link}}
- {{Design review checklist}} — {{path/link}}
- {{Code inspection checklist}} — {{path/link}}

---

## 8. Finding Classification and Disposition

> Every observation a review produces is a *finding*; classifying findings consistently is what lets the team prioritize rework and measure the process. Classify on **separate axes** — they answer different questions and must not be collapsed into one: **Severity** (how bad if it ships), **Type** (what kind of problem), **Priority** (how soon to fix), and **Disposition** (the decision made). The non-negotiable rule: **every finding receives a disposition** so none are silently dropped, and a rejected finding is recorded **with a reason, not erased** (traceability). Findings use FND-N IDs and their dispositions tie to the exit criteria in §6.7. This classification is shared with the Audit Report template so findings cross-reference cleanly.

**Severity** — impact if the defect shipped:

| Level | Meaning |
|---|---|
| Critical | {{Would cause failure, data loss, or a safety/security breach; must not ship.}} |
| Major | {{Significant defect; the product does not meet a requirement or standard.}} |
| Minor | {{Real defect with limited impact; should be fixed but does not block.}} |
| Cosmetic | {{Wording/formatting; no functional impact.}} |

**Type** — what kind of problem the finding is:
- Missing — required content/behavior is absent.
- Wrong — present but incorrect.
- Extra — present but not required (scope creep).
- Ambiguous — unclear, open to more than one reading.
- Non-conformance — violates an applicable standard/procedure.
- Question — needs clarification before it can be classified.

**Priority** — how soon to fix, *independent of severity*: {{High / Medium / Low}}. (A Minor-severity finding can be High-priority — e.g., a one-word fix that unblocks others; a Major-severity finding can be Low-priority if it is in a deferred area.)

**Disposition** — the decision recorded for every finding:
- **Fix** — accepted as a defect; will be reworked.
- **Defer** — accepted but scheduled later; record owner and target date.
- **Reject (not a defect)** — not a real flaw; **record the reason**, do not delete the row.
- **Duplicate** — already captured as another finding; link to it.

Example findings log row (the live log is a separate review record — see §9, not embedded here):

| ID | Finding | Severity | Type | Priority | Disposition |
|---|---|---|---|---|---|
| FND-1 | {{Requirement R12 has no acceptance criterion — cannot be verified}} | Major | Missing | High | Fix |
| FND-2 | {{"User" and "operator" used interchangeably across §3}} | Minor | Ambiguous | Medium | Fix |
| FND-3 | {{Reviewer thought §4 contradicted §2 — actually consistent on re-read}} | — | Question | — | Reject (reason recorded) |
| FND-N | {{Finding}} | {{Severity}} | {{Type}} | {{Priority}} | {{Disposition}} |

Every FND-N must carry a disposition before the review can satisfy CRIT-7 / CRIT-8 (§6.7).

---

## 9. Review Records and Retention

> A review that leaves no record cannot be audited, measured, or learned from. This section says exactly what each review must capture, where it is stored, who files it, how long it is kept, and who can see it. The key boundary: this *plan* defines the record **format**; the records themselves are separate instance artifacts — **do not embed live review data in this plan**. An audit is the exception in degree: an audit's record *is* the Audit Report (a fuller template); ordinary review records are lighter.

Each review record must capture:

| Field | Content |
|---|---|
| Review identification | {{REV-N — unique ID for the event}} |
| Product reviewed | {{name + version of the work product (and its RI-N scope row)}} |
| Review type | {{inspection / technical review / walk-through}} |
| Participants and roles | {{names mapped to ROLE-N}} |
| Date | {{YYYY-MM-DD}} |
| Findings | {{the FND-N log with severity, type, priority, and disposition (§8)}} |
| Decision / recommendation | {{accept / accept-with-rework / re-review / reject}} |
| Exit-criteria check | {{which of CRIT-7..CRIT-10 (§6.7) were satisfied}} |
| Metrics captured | {{preparation time, rework time, defect count, size — feeds §10}} |

**Storage and retention:**
- **Records location:** {{where review records, findings logs, and metrics are filed}}
- **Responsible for filing:** {{the moderator / recorder}}
- **Retention period:** {{e.g., life of the project + N years}}
- **Access / visibility:** {{public vs. internal — note that these templates are public-facing; live review data may contain content that should stay internal, so keep records in the appropriate-visibility store}}

**Relationship to the Audit Report:** an audit's record *is* the Audit Report (template AUD-{{PROJECT-ID}}-001) — fuller, with corrective-action tracking. Ordinary review records (above) are lighter. In both cases, the *plan* defines the format and the *records* are separate artifacts.

---

## 10. Metrics

> Metrics turn the review process from a feeling ("reviews seem useful") into evidence ("reviews caught 78% of defects before test"), so you can tell whether the process is worth its cost and where to tune it. Four core metrics are below, each with a definition, a formula where one exists, a unit, and the decision it informs. A red-flag note matters as much as the numbers: **near-zero preparation time or near-zero findings is itself a signal the review was not done properly** — a "clean" review with no preparation usually means nobody looked hard, not that the product was perfect. Metrics roll up across REV-N events to evaluate the process over time.

| Metric | Definition / formula | Unit | What it tells you |
|---|---|---|---|
| Defect Density | confirmed defects ÷ size | defects per page (docs) or per KLOC (code) | {{Yield normalized for size; lets you compare review results across differently sized products and spot unusually defect-dense work.}} |
| Preparation Time | reviewer-hours spent examining the product **before** the meeting | reviewer-hours | {{Whether reviewers actually prepared. Too low predicts a weak review — a red flag, not a win.}} |
| Rework Time | effort to disposition and fix findings | person-hours | {{Cost of the defects found; helps weigh review cost vs. benefit and plan capacity.}} |
| Defect Removal Effectiveness (DRE) | defects found in review ÷ (found in review + found later) × 100 | percent | {{**The headline metric.** What share of defects reviews catch before they escape to test or the field. Rising DRE means reviews are paying off.}} |

**Healthy-range guidance / red flags:**
- {{Near-zero preparation time}} → the review likely was not really done; treat a clean result as suspect.
- {{Zero findings on a non-trivial product}} → usually means weak examination, not a flawless product.
- {{DRE trending down across REV-N events}} → defects are escaping reviews; revisit checklists (§7), entry criteria (§5), or preparation discipline (§6.3).

Metrics from individual review events (REV-N) roll up to evaluate the review process for {{Project Name}} as a whole over time.

---

## 11. Open Questions

> It is normal that not every process choice is settled when the plan is first written — record the open ones rather than pretending they are decided. Each open question gets an OQ-N ID, the question itself, what is blocking it, and who must decide. A point worth internalizing: an unresolved open question on a *must-do* review (e.g., the SRS inspection) is a **process risk**, not a footnote — flag it as such. Resolve and remove questions as the plan matures.

- **OQ-1**: {{Should security-relevant modules require an external independent inspector?}} — {{blocked on budget; owner: process owner.}}
- **OQ-2**: {{DRE (§10) needs a defined "later-phase defect source" before it can be computed.}} — {{blocked on test-tracking setup; owner: process owner + test lead.}}
- **OQ-N**: {{question}} — {{what's blocking, who must decide}} {{(mark as a process risk if it blocks a must-do review)}}

---

## 12. Revision History

> Mandatory closing section. Record every substantive change with a version bump, date, author, and a summary — **especially** changes to which review types are in scope (§3), to entry/exit criteria (§5, §6.7), or to the finding-severity scale (§8), since those change how reviews are run and how findings are judged.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Review Scope and Work Products
- §3 Review Types
- §4 Roles and Responsibilities
- §5 Entry Criteria
- §6 Review Procedure (including §6.7 Exit Criteria)
- §8 Finding Classification and Disposition
- §12 Revision History

**Optional sections** (include if relevant):
- §7 Review Criteria and Checklists (at minimum keep the dimension list; type-specific checklists can be appendices/links)
- §9 Review Records and Retention (keep at least the record-format table; can be light for tiny projects)
- §10 Metrics (defer if too early, but DRE and preparation time are cheap and high-value — adopt them as soon as you have a second phase to compare against)
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (for cross-document traceability):
- RI-N: this plan's own clauses / scope rows (doc-level)
- REV-N: individual review events/sessions (a finding or metric cites the review that produced it)
- FND-N: findings/anomalies raised in a review (shared with the Audit Report template)
- ROLE-N: role definitions
- CRIT-N: review-criteria checklist items and entry/exit criteria

Numbering is continuous across sections so each item has a unique, citable ID. These prefixes let the Test Plan, V&V Plan, and Audit Report cross-reference reviews cleanly (e.g., an Audit Report finding FND-N can cite the review REV-N that first raised it).

**Tailoring** (including solo / small-team collapse):
- Use only the review types you actually need (§3). A small project often runs **Walk-through + one Inspection on the riskiest product** and nothing else — state the in/out choices and move on.
- One person can hold several roles (§4) — the only hard rule is that the author does not lead the inspection/audit of their own work. **Solo collapse:** preserve independence with a time gap (review a cooled draft as if it were someone else's) or by inviting an outside peer for high-stakes products.
- Entry/exit criteria (§5, §6.7) can be a short bullet list rather than a table on a small project — but keep the "postpone, don't run-and-fail" rule and the "don't close with open major findings" rule; they are what make a review worth running.
- Metrics (§10) scale down to just **preparation time** and **DRE** for a small team; even two data points start to show whether reviews are paying off.
- This is a default. Deviate when needed, but deviate explicitly — record the choice in §11 or §12 so a future reader understands the omission was deliberate.

**For regulated/safety-critical projects:** use the full IEEE 1028-2008 standard, not this lightweight version. This template paraphrases the standard's public structure for solo/small-team and internal use; verify the type definitions, mandatory procedure steps, required record contents, and role responsibilities against the full IEEE 1028-2008 document before relying on it for regulated, safety-critical, contractual, or certification contexts.
