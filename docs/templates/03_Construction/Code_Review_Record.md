# Code Review Record Template

> **Template purpose:** Lightweight Code Review Record structure aligned to IEEE 1028-2008 (IEEE Standard for Software Reviews and Audits). Use this template to capture the outcome of a *single* code review of a *specific* work product. Replace `{{placeholder}}` content with the actual review's details. Section guidance (in blockquotes) can be deleted once the section is filled in.
>
> **When to use:** Each time you hold a code review you want a durable account of — typically a pull-request review, a commit-range inspection, or a walk-through of a module before merge. Unlike the SRS (WHAT) or SDD (HOW), this is a *record*: it documents one review event, gets signed off, and is then frozen. Open a new record per review.
>
> **Companion standard:** IEEE 1028-2008 — IEEE Standard for Software Reviews and Audits.
>
> **Status of this template:** Lightweight Code Review Record structure aligned to IEEE 1028-2008 (IEEE Standard for Software Reviews and Audits), reduced for solo/small-team use. IEEE 1028-2008 is a paywalled IEEE standard; this is a lightweight skeleton derived from public sources — it follows the standard's well-known structure (review types, defined roles, entry/exit criteria, and the anomaly/finding classification model) and paraphrases or reproduces NO normative text from the standard. Verify section content against the full standard before relying on this record in a regulated, safety-critical, or audited context. This is a record/instance document: it captures one specific review event and is frozen on sign-off, not maintained over time like a spec or template.

---

# Code Review Record — {{System Name}}

| Field | Value |
|---|---|
| Document ID | CRR-{{REVIEW-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 1028-2008 (lightweight) |
| Owner | {{Project name or owner}} |
| Review type | {{Inspection / Technical review / Walk-through — per IEEE 1028-2008}} |
| Work product | {{PR / commit range / module under review}} |
| Version / Commit | {{tag, branch, or commit hash}} |
| Review date | {{YYYY-MM-DD}} |
| Moderator / Review leader | {{Name / role}} |
| Recorder | {{Name / role — who logged this record}} |
| Review decision | {{Accepted / Accepted with rework / Re-review required / Rejected}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> This section frames the record. In the SRS/SDD house style we fold Purpose, Scope, Definitions, and References into one numbered Introduction — we do the same here.
>
> **New to formal reviews?** Two ideas to anchor on before you read further:
> - A **software review** is a deliberate, structured examination of a *work product* (here, source code) by people *other than the author*, held to find problems early and confirm the work is fit to proceed. IEEE 1028-2008 defines five formal kinds — management review, technical review, inspection, walk-through, and software audit — that differ in how formal they are and what they aim at. A code review is normally a *technical review* (a peer assessment of fitness) or an *inspection* (a more rigorous, checklist-driven defect hunt led by a moderator). State which one this record captures.
> - A **record** document is filled in once per event and then *frozen*. That is the opposite of a template or a spec, which you maintain and revise over time. After sign-off, edits to this record are corrections or addenda, not ongoing development (see §8).

### 1.1 Purpose

> One paragraph. State that this document records the outcome of one code review of one specific work product, why the review was held, and that it is an *instance record* of a single event — not a reusable process definition.

This document records the outcome of a single code review of **{{work product — e.g. PR #123 / commit range a1b2c3d..d4e5f6g}}** for {{System Name}}. The review was held to {{reason — e.g. confirm the change meets the coding standard and traces to its requirements before merge}}. It is an *instance record*: it captures one review event held on {{YYYY-MM-DD}} and is frozen on sign-off. The reusable *process* that governs how we run reviews is defined elsewhere ({{link to review process / contributing guide}}), not here.

### 1.2 Scope

> Say what this record covers and what it explicitly excludes. Name the IEEE 1028-2008 review type.

In scope:
- The named work product **{{work product}}** at version/commit **{{tag, branch, or commit hash}}**.
- The review criteria applied (see §3) and the findings raised against that work product (see §4).

Out of scope:
- {{Other modules / files not in the work product}} — not examined in this review.
- {{Later changes made after the reviewed commit}} — a subsequent change requires its own record or a re-review.
- The review *process* definition itself — see {{link}}; this record is the *result* of applying that process once.

**Review type:** This was a {{Inspection / Technical review / Walk-through}} per IEEE 1028-2008. {{One line on why this type — e.g. "Technical review: peers assessed fitness-to-merge; no formal moderator-led inspection meeting was held."}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Pull in only the terms whose absence would cause misreading. Define each plainly the first time. Keep the table short.

| Term | Definition |
|---|---|
| Work product | The specific thing under review: a pull request, commit range, file set, or module. Pinned to an exact version or commit so the record is reproducible — "reviewed file X" is ambiguous; "reviewed X at commit `a1b2c3d`" is not. |
| Finding (anomaly) | A single issue raised during the review — a bug, a gap, a risk, a style violation, or an open question. IEEE 1028-2008 calls these *anomalies*. Each gets one ID (`FND-N`). One finding = one problem; do not bundle several issues under one ID. |
| Severity | How bad a finding is (e.g. Blocker / Major / Minor / Info). See §4 for the scale. |
| Disposition | The *decision* made about a finding (Fix now / Fix later / Won't fix / Not a defect / Deferred). Independent of severity and of open/resolved status. |
| Review decision | The single overall verdict on the *work product* (Accepted / Accepted with rework / Re-review required / Rejected). Distinct from per-finding dispositions. |
| Entry / exit criteria | IEEE 1028's gates around a review. *Entry criteria* must be true before the review starts (e.g. code compiles, tests pass, author self-reviewed). *Exit criteria* must be true to call the review done (e.g. all findings dispositioned, decision recorded). |
| {{Term}} | {{Definition}} |

### 1.4 References

> List the work product under review (with link), the coding standard or checklist applied, the SRS/SDD requirements the code is traced against, the defect tracker, and the standard itself.

| Ref | Document |
|---|---|
| R1 | {{Work product — PR link or commit range}} — the code under review |
| R2 | {{Coding standard / review checklist used}} — the lens applied (see §3) |
| R3 | {{SRS-…-001 / SDD-…-001 sections}} — requirements/design the code is traced against |
| R4 | {{Defect tracker / issue board}} — where follow-up tickets live |
| R5 | IEEE 1028-2008 — IEEE Standard for Software Reviews and Audits |
| ... | ... |

---

## 2. Review Identification

> This is the authoritative header for the review event — it answers "what exactly was reviewed, by whom, when, and in what form." Deepen the metadata table above into a complete, role-aware identification.
>
> **Beginner notes:**
> - **Pin the version.** Record an exact commit hash, tag, or immutable PR snapshot. If you write "the login module," nobody can reproduce what you saw — the code may have moved on. "the login module at commit `a1b2c3d`" is reproducible.
> - **Roles matter, and the author does not lead.** IEEE 1028-2008 separates roles so accountability is explicit: the *author* wrote the work product; the *reviewer / inspector* examines it; the *moderator / review leader* runs the review; the *recorder* logs the findings (often whoever fills in this record). The author is listed but does **not** lead the review — the standard deliberately keeps authorship and review leadership apart so no one grades their own work.

| Field | Value |
|---|---|
| Review ID | CRR-{{REVIEW-ID}} |
| Work product | {{PR #123 / commit range / module}} |
| Version / Commit | {{exact hash, tag, or branch@commit}} |
| Review type | {{Inspection / Technical review / Walk-through}} |
| Meeting format | {{Synchronous meeting / Asynchronous PR comments / Hybrid}} |
| Author | {{Name / role — wrote the work product; does not lead}} |
| Moderator / Review leader | {{Name / role — runs the review, holds decision authority}} |
| Reviewer(s) / Inspector(s) | {{Names / roles}} |
| Recorder | {{Name / role — logged this record}} |
| Review date | {{YYYY-MM-DD}} |
| Duration / effort | {{e.g. 45 min meeting, or 2 reviewer-hours async}} |

---

## 3. Review Criteria and Entry Criteria

> Two parts: the gate the work had to pass to be reviewed at all (entry criteria), and the lens the reviewers applied (review criteria / checklist).
>
> **Beginner notes:**
> - **Why fixed criteria?** Stating the criteria up front makes reviews consistent and reduces reliance on the reviewer's mood or memory. Two reviewers applying the same checklist converge; two reviewers "just looking it over" diverge.
> - **Why entry criteria?** *Entry criteria* stop a review from wasting effort on work that was not ready — there is no point hunting subtle defects in code that does not compile or whose tests fail. Confirm they were met before the review started; if any was waived, say so and why.

### 3.1 Entry criteria

> What had to be true before the review began. A short checklist. Mark each met / waived.

| Entry criterion | Met? | Notes |
|---|---|---|
| Code compiles / builds cleanly | {{Yes / No / Waived}} | {{notes}} |
| Automated tests pass | {{Yes / No / Waived}} | {{which suite; link to CI run}} |
| Author self-review completed | {{Yes / No / Waived}} | {{notes}} |
| Work product is at a stable, named version | {{Yes / No}} | {{commit/tag}} |
| {{Other entry criterion}} | {{Yes / No / Waived}} | {{notes}} |

Waivers: {{None / list each waived criterion and the justification — e.g. "Tests waived: this is a docs-only change with no executable paths."}}

### 3.2 Review criteria / checklist

> The dimensions the reviewers examined. Mark which were *in scope* for this review — a hotfix review may legitimately skip Maintainability. Reference the specific coding standard or checklist used.

Checklist / coding standard applied: {{link or name — e.g. "Project coding standard v2, OWASP secure-coding checklist"}}

| Criterion | In scope? | Notes |
|---|---|---|
| Correctness — does the code do what it should? | {{Yes / No}} | {{notes}} |
| Completeness — are all required cases handled? | {{Yes / No}} | {{notes}} |
| Traceability — does the code map to a requirement/design ID? | {{Yes / No}} | {{which SRS/SDD IDs}} |
| Maintainability — readability, structure, naming | {{Yes / No}} | {{notes}} |
| Security — input validation, secrets, authz, injection | {{Yes / No}} | {{notes}} |
| Testability — can it be tested; are tests present? | {{Yes / No}} | {{notes}} |
| Error handling — failure paths, logging, recovery | {{Yes / No}} | {{notes}} |
| Compliance with coding standard | {{Yes / No}} | {{which standard}} |
| {{Other criterion}} | {{Yes / No}} | {{notes}} |

---

## 4. Findings

> The substantive heart of the record: every issue the review raised, one row per finding, each with a stable `FND-N` ID.
>
> **Beginner notes — three independent axes that are easy to conflate:**
> - **Severity** = *how bad* (Blocker / Major / Minor / Info). Define the levels once so "Major" means the same thing in every review (scale below).
> - **Disposition** = *what was decided* (Fix now / Fix later / Won't fix / Not a defect / Deferred).
> - **Status** = *where it stands now* (Open / Resolved / Verified).
>   These are independent: a Minor finding can be "Fix now"; a Major finding can be "Deferred" with justification.
> - **One finding = one problem.** Do not bundle several issues under one ID — you cannot track resolution of a bundle.
> - IEEE 1028-2008 calls these findings *anomalies*. A finding dispositioned **"Not a defect"** is a valid, recordable outcome: it documents that a reviewer raised something, it was examined, and the team judged it not to be a problem. Recording it (rather than silently dropping it) is the point.
> - **Location** must let the finding be found again: file plus line/range, or a permalink to the PR comment.

**Severity scale** (define once; reuse across reviews):

| Severity | Meaning |
|---|---|
| Blocker | Must be fixed before the work product can be accepted; merging would cause failure, data loss, or a security hole. |
| Major | Significant defect or risk; should be fixed, but acceptance with a tracked follow-up may be justified. |
| Minor | Small defect or quality issue; low risk if it ships. |
| Info | Observation, suggestion, or praise; no action required. |

**Findings table:**

| ID | Finding | Severity | Location | Traces to | Owner | Disposition | Status |
|---|---|---|---|---|---|---|---|
| FND-1 | {{One concrete problem — e.g. "Null check missing on `user.email` before send"}} | {{Blocker / Major / Minor / Info}} | {{`auth/mailer.py:42` or PR-comment link}} | {{SRS-…-3.2 / SDD-…-IF-1 / —}} | {{Name}} | {{Fix now / Fix later / Won't fix / Not a defect / Deferred}} | {{Open / Resolved / Verified}} |
| FND-2 | {{Second distinct problem}} | {{...}} | {{location}} | {{trace ID or —}} | {{Name}} | {{...}} | {{...}} |
| FND-3 | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

> The **Traces to** column is optional but recommended: link each finding back to the requirement (`SRS-…`) or design element (`SDD-…`) it touches, so a finding is never orphaned from its source.

---

## 5. Review Decision

> The single overall verdict on the work product, plus the exit criteria that justify it.
>
> **Beginner notes:**
> - This overall **review decision** is distinct from the per-finding dispositions in §4. A work product can be **"Accepted with rework"** even while individual findings are still "Fix later" — provided the agreed *exit criteria* are satisfied (e.g. no open Blocker remains).
> - **Exit criteria** are the gate to call the review done: typically every finding has a disposition, no Blocker is left open, and a re-review is scheduled if one is required.
> - Decision authority normally sits with the **moderator / review leader**, not the author.

**Decision:** {{Accepted / Accepted with rework / Re-review required / Rejected}}

**Decision authority:** {{Name / role — typically the moderator / review leader}}

**Rationale:** {{Which findings drove this outcome — e.g. "Accepted with rework: no Blockers; FND-1 (Major) is dispositioned Fix-now and tracked as {{TICKET-ID}}; remaining findings are Minor/Info."}}

**Exit criteria check:**

| Exit criterion | Met? | Notes |
|---|---|---|
| Every finding has a disposition | {{Yes / No}} | {{notes}} |
| No open Blocker remains | {{Yes / No}} | {{notes}} |
| Required follow-up actions are owned and tracked (see §6) | {{Yes / No}} | {{notes}} |
| Re-review scheduled (if decision is "Re-review required") | {{Yes / No / N/A}} | {{when / who}} |
| {{Other exit criterion}} | {{Yes / No}} | {{notes}} |

---

## 6. Follow-up Actions

> The work that turns findings into fixes. Each action traces back to the finding(s) it resolves and, where it moves into a tracker, carries the external ticket ID so the thread does not break when it leaves this document.
>
> **Beginner notes:**
> - This section is what prevents *review theatre* — findings raised but never fixed. Every "Fix now" / "Fix later" disposition in §4 should have a matching action here.
> - A **contradiction to catch:** a closed/accepted review whose Blocker-gating actions are still open. If acceptance depended on an action, that action must close (or the decision is wrong).
> - Distinguish actions that **gate acceptance** (must close before exit) from actions **deferred** to later work. Note who confirms each is done and how (re-review, test, tracker close).

| Action | Resolves | Owner | Gates acceptance? | Tracker ID | Verified by / how | Due | Status |
|---|---|---|---|---|---|---|---|
| {{e.g. "Add null check + unit test for empty email"}} | FND-1 | {{Name}} | {{Yes / No}} | {{TICKET-123}} | {{re-review / CI test / tracker close}} | {{YYYY-MM-DD}} | {{Open / Done}} |
| {{Deferred refactor of mailer queue}} | FND-2 | {{Name}} | {{No}} | {{TICKET-124}} | {{...}} | {{YYYY-MM-DD}} | {{Open}} |
| {{...}} | {{FND-N}} | {{Name}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

---

## 7. Open Questions

> Anything the review surfaced that could not be resolved in the session. Placed near the end, before Revision History, matching the SRS/SDD house pattern. Use `OQ-N` IDs.
>
> **Beginner note — finding vs. open question:** a *finding* (§4) is a concrete problem with the code. An *open question* is an unresolved *decision* the review uncovered — often pointing back to the SRS or an ADR (Architecture Decision Record: a short document capturing one significant design decision and its rationale). Example finding: "Off-by-one in the retry loop." Example open question: "Should retries be capped at 3 or made configurable? — needs a product decision." Resolve and remove these as they close, or migrate them to the appropriate spec/ADR so they are not lost when this record is frozen.

- **OQ-1**: {{Unresolved decision the review exposed}} — {{what's blocking / who decides / where it should migrate (SRS section, ADR-NNNN)}}
- **OQ-2**: {{...}} — {{...}}

---

## 8. Revision History

> Must be the last body section, per house style. Track every substantive change with a version bump.
>
> **Beginner note — records behave differently from specs.** Once the review event is complete and signed off, this record is essentially *frozen*. Entries here after sign-off are corrections or addenda — for example "added FND-7 raised in async follow-up" or "recorded re-review outcome" — not ongoing edits. This keeps the record a faithful account of what actually happened, while still leaving an auditable trail of any later amendment.

| Version | Date | Author | Description of Change | Approval |
|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft | {{—}} |
| {{1.0}} | {{YYYY-MM-DD}} | {{Author}} | {{Review held; findings and decision recorded; signed off}} | {{Approver}} |
| {{1.1}} | {{YYYY-MM-DD}} | {{Author}} | {{Addendum: e.g. recorded re-review outcome for FND-1}} | {{Approver}} |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Review Identification
- §4 Findings (even if "no findings" — record that explicitly)
- §5 Review Decision
- §8 Revision History

**Optional sections** (include if relevant):
- §3 Review Criteria and Entry Criteria (always recommended; the entry-criteria checklist may be trimmed for a tiny change)
- §6 Follow-up Actions (omit only if the decision is a clean "Accepted" with zero Fix-now/Fix-later dispositions)
- §7 Open Questions (track elsewhere if you prefer, but don't lose them)

**Identifier conventions:**
- `CRR-{{REVIEW-ID}}` — the record itself (one per review event)
- `FND-N` — findings / anomalies (FND-1, FND-2, …)
- `OQ-N` — open questions
- Each `FND-N` should trace from this record to the work product, to the follow-up action that resolves it (§6), to any defect-tracker ticket, and — via the "Traces to" column — back to the `SRS-…` / `SDD-…` element it touches. These prefixes enable cross-document traceability so nothing raised in review silently disappears.

**Tailoring:**
- IEEE 1028-2008's role and review-type vocabulary is guidance, not a mandate. Use the parts that earn their place.
- **Solo developer / small team:** the record collapses naturally. With one developer, a true peer review may be impossible — record a *self-review against the checklist* and say so plainly in §2 (author = reviewer, no separate moderator); be honest that the "no one grades their own work" separation is not fully achievable solo, and lean harder on the §3 checklist to compensate. For a small team, the same person may fill several roles (e.g. reviewer + recorder); list each role and who covered it. Asynchronous PR-comment reviews are first-class — set Meeting format to "Asynchronous PR comments" and link the thread.
- Keep one record per review event. A later change to the same code gets its own `CRR-…` record or a logged re-review, never an in-place rewrite of a frozen record.
- Revision history is mandatory. After sign-off, only corrections/addenda — never silent edits.

**For regulated/safety-critical projects:** use the full IEEE 1028-2008, not this lightweight version. This template is suitable for solo/small-team projects, internal code reviews, and early-stage products; it is built from the standard's public structure and must be verified against the full standard before use in any audited or safety-critical context.
