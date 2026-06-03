# Test Summary Report Template

> **Template purpose:** Lightweight Test Summary Report (TSR), also called a Test Completion Report, aligned to ISO/IEC/IEEE 29119-3:2021 (Software testing — Part 3: Test documentation). Use this template to write up the outcome of a completed test cycle. Replace `{{placeholder}}` content with cycle-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** AFTER a test cycle has finished executing, not before. The TSR is the closing bookend to the Test Plan: where the plan said "here is what we will test and the conditions under which we will call it done," the TSR says "here is what we actually ran, what passed and failed, and whether the software is good enough to ship." Write one per test cycle, per release candidate, or per milestone — and re-issue it (version bump) whenever a retest changes the picture.
>
> **Companion standard:** ISO/IEC/IEEE 29119-3:2021 — Software and systems engineering — Software testing — Part 3: Test documentation (Test Completion Report / Test Summary Report).
>
> **Status of this template:** Lightweight Test Summary Report structure aligned to the SWEBOK Testing KA and to ISO/IEC/IEEE 29119-3:2021 (Software testing — Part 3: Test documentation), specifically its Test Completion Report content outline. ISO/IEC/IEEE 29119-3 is a PAYWALLED standard — this template is a clean-room, lightweight extract drawn from the publicly described content items (results summary, deviations, evaluation against completion criteria, residual risks, recommendation) and from the SWEBOK Testing KA; it reproduces no copyrighted text from the standard. VERIFY section content and naming against your licensed copy of ISO/IEC/IEEE 29119-3:2021 before using in a regulated, contractual, or certification context. Suitable as-is for solo/small-team and internal use.

---

# Test Summary Report (TSR) — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | TSR-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29119-3:2021 (lightweight) |
| Owner | {{Project name or owner}} |
| Reports on | TI-N: {{build / release candidate / version under test}} |
| Test period | {{YYYY-MM-DD}} to {{YYYY-MM-DD}} |
| Test level(s) | {{Unit / Integration / System / Acceptance}} |
| Test environment | {{environment name / config under which results were produced}} |
| Companion Test Plan | {{TP-{{PROJECT-ID}}-001 — path/to/test-plan.md}} |
| Overall verdict | {{Proceed / Proceed with limitations / Do not proceed}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph. Establish that this is a RECORD document: it reports the outcome of a test cycle that has already finished. State that it (a) reports the results for the test items named in the metadata, (b) evaluates those results against the exit criteria agreed in the companion Test Plan, and (c) recommends whether to proceed. Make explicit that the TSR does not itself plan or design tests — the Test Plan plans them and the Test Case Specification designs them; this document closes them out.

This document reports the outcome of the test cycle run against {{TI-N: build / release candidate / version under test}} during {{test period}}. It summarizes what was executed, what passed and failed, the defects found, the deviations from plan, and the risks that remain; it then evaluates those results against the exit criteria set in the companion Test Plan ({{TP-{{PROJECT-ID}}-001}}) and recommends whether to proceed. It is written **after** execution: it neither plans nor designs tests, and it adds no new evidence beyond what was observed during the cycle.

### 1.2 Scope

> Define what these RESULTS cover and what they do not. Cover: which test items (TI-N), which test levels, which time period. Exclude: test cases not yet executed, environments out of scope, test levels deferred to a later cycle. Beginner note: scope here means the scope of the RESULTS being reported, not the scope of the system. "We did not run the load tests this cycle" is a scope statement; it does not mean the system has no performance requirements.

**This report covers:**
- Test items: {{TI-1, TI-2 — the builds / modules / versions whose results are reported}}
- Test level(s): {{Unit / Integration / System / Acceptance — whichever were executed this cycle}}
- Test period: {{YYYY-MM-DD}} to {{YYYY-MM-DD}}
- Environment(s): {{environment name / config}}

**This report does not cover:**
- {{Test cases planned but not executed this cycle — disclosed as a coverage gap in §2}}
- {{Test levels deferred to a later cycle, e.g. acceptance testing scheduled after this build}}
- {{Out-of-scope environments / platforms}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Keep the term/definition table. Pre-seed it with the concepts a reader needs in order to read the rest of the report. Add project-specific terms as needed.

| Term | Definition |
|---|---|
| Test Summary Report (TSR) | A record document, also called a Test Completion Report, written after a test cycle finishes. Reports what was run, what passed/failed, and whether the software is good enough to ship. The closing bookend to the Test Plan. |
| Test item (TI-N) | The specific thing under test: a build, a release candidate, a module, a version. TI-N ids originate in the Test Plan; this report quotes them so the reader knows exactly which artifact the results describe. |
| Test case (TC-N) | One concrete check with steps, inputs, and an expected result. A test case has a single outcome per run: pass, fail, or blocked. TC-N ids originate in the Test Case Specification; this report aggregates many of their outcomes into counts. |
| Pass / Fail / Blocked | A test **passes** when actual behaviour matches expected; **fails** when it does not; is **blocked** when it could not be run at all (environment down, dependency missing, a prerequisite test failed). Blocked is distinct from fail: a blocked test has no result yet, so it is neither evidence of correctness nor of a defect. |
| Defect (bug) vs. failure | A **failure** is the observed symptom (a test went red). A **defect** is the underlying fault in the software that caused it. One defect can cause many failures; one failed test can be caused by bad test data or a flaky environment rather than a real defect. |
| Severity vs. priority | **Severity** is how bad a defect's impact is (data loss > cosmetic typo). **Priority** is how soon it should be fixed (business urgency). They are independent axes: a low-severity bug on the demo screen can be high priority; a high-severity edge case nobody hits can be low priority. |
| Exit criteria | The conditions agreed in the Test Plan that say "testing is done and the result is acceptable" (e.g. "100% of critical test cases pass, zero open critical defects"). The Evaluation section checks results against these — not against a gut feeling. |
| Requirements traceability | The ability to show, for each requirement, which test cases verified it and whether they passed. The traceability matrix makes coverage gaps visible: a requirement with no passing test is unverified. |
| Residual risk | A risk that remains after testing finishes: an untested area, a known-but-unfixed defect, a deferred feature. Shipping is a decision made with eyes open about residual risk, not a claim that risk is zero. |
| Verdict / recommendation | The report's bottom line — Proceed, Proceed with limitations, or Do not proceed. A recommendation to a decision-maker (the release authority), backed by the report's evidence; not the release decision itself. |
| {{Project term}} | {{Definition}} |

### 1.4 References

> List the documents that make this report meaningful. Beginner note: a Test Summary Report is almost meaningless without its references — the reader must be able to reach the plan it is graded against (for the exit criteria) and the requirements it claims to verify (for the traceability check). A TSR with no references is an unsupported claim.

| Ref | Document | Why it matters here |
|---|---|---|
| R1 | {{TP-{{PROJECT-ID}}-001 — path/to/test-plan.md}} | The companion Test Plan. Source of the exit criteria this report is graded against (§7) and of the TI-N / planned-count figures (§2). |
| R2 | {{SRS-{{PROJECT-ID}}-001 — path/to/srs.md}} | The Software Requirements Specification. Source of the REQ-N / SRS § ids whose verification status is reported in §3. |
| R3 | {{TCS-{{PROJECT-ID}}-001 — path/to/test-cases.md}} | The Test Case Specification(s) where the TC-N referenced in this report are defined. |
| R4 | {{Defect-tracker query / saved filter URL}} | The live defect data this report summarizes (§4). The report summarizes; the tracker holds the detail. |
| R5 | ISO/IEC/IEEE 29119-3:2021 | Software testing — Part 3: Test documentation. The standard whose Test Completion Report content outline this template follows. |
| ... | ... | ... |

---

## 2. Test Results Summary

> The report's headline dashboard. The narrative paragraph gives the one-sentence story the numbers tell; the table gives the numbers. Beginner note on WHY each row matters: **Blocked** counts tests that could not run (an environment/dependency problem, not evidence of quality); **Not Run** (Planned minus Executed) is a coverage gap to disclose, not hide; a high pass rate over a small executed fraction is weaker evidence than a lower pass rate over full coverage. The numbers must RECONCILE: `Executed = Passed + Failed + Blocked`, and `Not Run = Planned − Executed`. Each count is an aggregation of individual TC-N outcomes — say where the per-case log lives so a reader can drill down. If the cycle spanned several test levels or components, break the table out (optional sub-table below).

{{One-sentence story: e.g. "Of 120 planned cases, 110 ran; 98 passed and 9 failed against TI-1, with 3 blocked on the unavailable payment sandbox; the 10 not-run cases are the deferred acceptance level."}}

**Overall results** (test items {{TI-N}}, period {{YYYY-MM-DD}}–{{YYYY-MM-DD}}):

| Metric | Count | Notes |
|---|---|---|
| Planned | {{N}} | Total TC-N planned for this cycle (from {{TP-{{PROJECT-ID}}-001}}) |
| Executed | {{N}} | = Passed + Failed + Blocked (must reconcile) |
| Passed | {{N}} | Actual matched expected |
| Failed | {{N}} | Actual did not match expected — see §4 for the defects behind these |
| Blocked | {{N}} | Could not be run (environment/dependency/prerequisite) — not evidence of quality; see §5 for cause |
| Not Run | {{Planned − Executed}} | Coverage gap — disclose, do not hide; explain in §1.2 / §5 |
| Open defects | {{N}} | Defects not yet fixed-and-verified — see §4 |
| Critical defects (open) | {{N}} | Usually a hard exit-criteria gate — feeds §7 |

Pass rate over executed: {{Passed / Executed}}%. Pass rate over planned: {{Passed / Planned}}%. {{If these diverge sharply, note why — it usually means a coverage gap.}}

Per-test-case results log: {{path / tracker query where the individual TC-N pass/fail/blocked records live}}.

**Optional breakdown by level or component** (include if the cycle spanned several):

| Level / Component | Planned | Executed | Passed | Failed | Blocked | Not Run |
|---|---|---|---|---|---|---|
| {{Unit}} | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} |
| {{Integration}} | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} |
| {{System}} | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} |

---

## 3. Requirement Verification Status

> This section answers "did we actually prove the system meets its requirements," which is a DIFFERENT question from "did the tests we ran pass." A traceability table maps each requirement to the test cases that exercise it and shows whether coverage is complete. Beginner note: a requirement with NO test case is UNVERIFIED even if every test that ran passed — list those rows explicitly rather than omitting them, because an absent row reads as "fine" when it actually means "unknown." Cross-references: Requirement IDs come from the SRS (REQ-N / SRS §); Test Case IDs are the TC-N consumed from the Test Case Specification; any requirement that failed or is only partially verified should point at the defect(s) in §4 and any residual risk it creates in §6.

| Requirement ID (SRS §) | Test Case IDs | Result | Coverage | Open Issues |
|---|---|---|---|---|
| {{REQ-1 (SRS §3.1)}} | {{TC-1, TC-2}} | {{Pass}} | Verified | — |
| {{REQ-2 (SRS §3.2)}} | {{TC-3}} | {{Fail}} | Partially verified | {{Defect DEF-12 in §4; RR-1 in §6}} |
| {{REQ-3 (SRS §3.3)}} | {{TC-4, TC-5}} | {{Pass / Blocked}} | Partially verified | {{TC-5 blocked — see §5 DEV-2}} |
| {{REQ-4 (SRS §4.1)}} | — | — | **Not verified** | {{No test case exists — coverage gap; RR-2 in §6}} |
| {{REQ-5 (SRS §3.4)}} | n/a | n/a | Not testable | {{Verified by inspection/review, not execution — note method}} |

**Coverage summary:** {{X of N requirements Verified, Y Partially verified, Z Not verified, W Not testable.}} {{One sentence on the most material gap.}}

> Coverage values: **Verified** = at least one passing test case covers the requirement and all its cases passed; **Partially verified** = some cases pass, others fail/blocked/missing; **Not verified** = no passing test case (includes "no test case at all"); **Not testable** = verified by a method other than execution (inspection, review, analysis) — name the method.

---

## 4. Defect Summary

> A structured summary of defects, NOT a re-listing of every one — link to the defect tracker for the detail. Provide small tables by severity, by priority, by component, and by status, plus a one-line trend note (are open defects rising or falling across the cycle?). Beginner note, stated in-line because it is load-bearing here: **severity** is impact (how bad), **priority** is urgency (how soon) — independent axes. "Open critical defects" is usually a hard gate in the exit criteria, so this section feeds directly into §7 Evaluation. Distinguish a real defect (a fault in the software) from a failed test caused by bad test data or a flaky environment — the latter is a test-asset problem and belongs in §5 Deviations, not here.

Defect detail lives in the tracker: {{R4 — defect-tracker query / saved filter}}. The tables below summarize; they do not replace it.

**By severity:**

| Severity | Open | Fixed & verified | Deferred | Won't-fix | Total |
|---|---|---|---|---|---|
| Critical | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} |
| Major | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} |
| Minor | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} |
| Cosmetic | {{N}} | {{N}} | {{N}} | {{N}} | {{N}} |

**By priority:**

| Priority | Count | Notes |
|---|---|---|
| High | {{N}} | {{e.g. blocks demo / release path}} |
| Medium | {{N}} | {{}} |
| Low | {{N}} | {{}} |

**By component:**

| Component | Open defects | Notable |
|---|---|---|
| {{Component A}} | {{N}} | {{DEF-12 — short label}} |
| {{Component B}} | {{N}} | {{}} |

**Trend:** {{Open critical defects went from {{N}} to {{N}} over the cycle — falling / flat / rising. One sentence on whether the curve is converging toward the exit criteria.}}

> Reminder: an "open critical defect" count above the exit-criteria gate is the single most common reason a TSR's recommendation (§9) is "Do not proceed." This row is the one a skim-reader looks at first.

---

## 5. Deviations from Plan

> An itemized, traceable list of where the cycle diverged from the companion Test Plan — and WHY. Use DEV-N identifiers. Beginner note: a deviation is not an admission of failure; an UNDOCUMENTED deviation is. The reader needs to know if, say, a third of planned tests were dropped for time, or a test ran against a stubbed dependency instead of the real service, because that changes how much the green numbers in §2 can be trusted. Each DEV-N notes its impact on the result and cross-references any blocked tests in §2 and any residual risk it creates in §6.

| ID | Area | Planned (per Test Plan) | What actually happened | Reason | Impact on result | Traces to |
|---|---|---|---|---|---|---|
| DEV-1 | Scope | {{Run all 120 cases}} | {{10 acceptance cases not run}} | {{Acceptance level deferred to next cycle}} | {{Coverage gap; pass-over-planned understates}} | §2 Not Run; RR-2 |
| DEV-2 | Environment | {{Real payment provider}} | {{Ran against stubbed sandbox}} | {{Provider sandbox unavailable}} | {{TC-5 blocked; payment path unverified end-to-end}} | §2 Blocked; RR-1 |
| DEV-3 | Schedule / data / procedure | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

> Capture deviations in any of: scope, test environment, test data, schedule, entry/exit criteria, and test procedures. If an exit criterion was changed mid-cycle, record it here as a deviation AND flag it in §7 — a criterion that moved after results came in must be visible, not silently applied.

---

## 6. Residual Risks

> An itemized register of what testing did NOT put to rest. Use RR-N identifiers. Beginner note: residual risk is risk that survives the test cycle — an untested area, a deferred defect, a known limitation. Shipping is a decision made WITH residual risk, not after eliminating it; the honest job of this section is to make those risks visible so the release authority (recorded in the §9 / front-matter sign-off) decides with eyes open. Trace each RR-N back to its origin — an untested area from §3, a deferred defect from §4, or a deviation from §5 — so a reader can see it is grounded in evidence, not speculation.

| ID | Description | Likelihood | Impact | Source | Recommended mitigation / monitoring |
|---|---|---|---|---|---|
| RR-1 | {{Payment path not verified end-to-end against the real provider}} | {{Medium}} | {{High}} | {{DEV-2; TC-5 blocked}} | {{Retest against real sandbox before public launch; monitor first 24h of live transactions}} |
| RR-2 | {{Acceptance criteria for REQ-4 unverified — no test case}} | {{Low}} | {{Medium}} | {{§3 Not verified}} | {{Add TC in next cycle; flag REQ-4 as provisional}} |
| RR-3 | {{Known minor defect DEF-31 deferred}} | {{High}} | {{Low}} | {{§4 deferred}} | {{Fix in next maintenance window; document workaround}} |
| RR-N | {{...}} | {{L/M/H}} | {{L/M/H}} | {{§3 / §4 / §5 origin}} | {{...}} |

> Qualitative likelihood/impact (Low/Medium/High) is fine for solo/small-team use. Reach for a numeric scale only if your release authority or a regulator requires it.

---

## 7. Evaluation

> The analytical core: where the report stops describing and starts CONCLUDING. Restate each exit / acceptance criterion from the companion Test Plan and mark it Met / Partially met / Not met, with the specific evidence behind the call (which §2 metric, §3 coverage figure, or §4 defect gate). Beginner note: the discipline here is that the conclusion must be anchored to the criteria agreed IN ADVANCE, not to after-the-fact optimism. If a criterion was changed mid-cycle, that belongs in §5 Deviations and must be flagged here. The output of this section is the justification the §9 Recommendation rests on — a recommendation with no traceable evaluation behind it is just an opinion.

| Exit criterion (from Test Plan) | Status | Evidence |
|---|---|---|
| {{100% of critical (P1) test cases pass}} | {{Met}} | {{§2: all {{N}} critical cases passed}} |
| {{Zero open critical-severity defects}} | {{Not met}} | {{§4: {{N}} open critical — DEF-12}} |
| {{≥ 95% of planned cases executed}} | {{Partially met}} | {{§2: {{Executed/Planned}}% executed; 10 acceptance cases deferred (DEV-1)}} |
| {{All SRS §3 requirements Verified}} | {{Not met}} | {{§3: REQ-4 Not verified (RR-2)}} |
| {{...}} | {{Met / Partially met / Not met}} | {{§ reference}} |

**Evaluation summary:** {{Two to four sentences synthesizing the table: which criteria are met, which are not, and what the gap to "all met" is. This is the bridge to §9 — state the overall picture, but keep the actual verdict in §9.}}

---

## 8. Open / Follow-Up Items

> The house-style Open Questions section, framed for a record document: items still unresolved at report time that the decision-maker needs visibility into. Use OQ-N identifiers. Beginner note: a TSR is a snapshot at a moment in time; some things are genuinely still in flight when it is written, and naming them here is more honest than forcing a clean-looking report. Distinguish items that BLOCK the recommendation (must resolve before proceeding) from those that can be carried as follow-ups after release. Resolve and remove as work progresses, or carry forward into the next cycle's plan.

**Blocking — must resolve before the §9 recommendation can change:**

| ID | Open item | Blocked on / awaiting | Owner / action |
|---|---|---|---|
| OQ-1 | {{Retest TC-5 against real payment sandbox}} | {{Provider sandbox availability (DEV-2)}} | {{QA — retest, then re-issue this TSR}} |
| OQ-2 | {{Fix and verify open critical DEF-12}} | {{Dev fix + re-run TC-3}} | {{Dev → QA}} |

**Follow-up — can be carried after release:**

| ID | Open item | Carry to | Owner / action |
|---|---|---|---|
| OQ-3 | {{Add test case for REQ-4 (RR-2)}} | {{Next cycle's Test Plan}} | {{QA}} |
| OQ-4 | {{Sign-off on accepting RR-3 (deferred minor defect)}} | {{Release authority}} | {{Release authority — record acceptance}} |

---

## 9. Recommendation

> The report's bottom line — short and decisive. State the verdict, then one to three sentences justifying it by pointing at §7 (criteria met / not met), §4 (open critical defects), and §6 (residual risks accepted). If "Proceed with limitations," enumerate the limitations and the conditions/monitoring attached. Beginner note: this is a RECOMMENDATION to the release authority, not the release decision itself — the decision and its owner are recorded in the sign-off block in the front-matter ("Approved by"). Keep this section free of new evidence; everything cited here must already appear in earlier sections. Mirror the verdict in the "Overall verdict" metadata row so a skim-reader sees it without scrolling.

**Verdict:** {{Proceed / Proceed with limitations / Do not proceed}}

**Justification:** {{One to three sentences. E.g. "Recommend Proceed with limitations: all critical test cases passed (§7) and the one open critical defect was reclassified after fix-and-verify, but the payment path could not be verified end-to-end against the real provider (RR-1, DEV-2). Proceed only with the payment feature flagged off until OQ-1 closes."}}

**Limitations and conditions (if "Proceed with limitations"):**
- {{Limitation 1 — e.g. payment feature flagged off until RR-1 retest closes}}
- {{Condition / monitoring — e.g. monitor first 24h of live transactions; rollback trigger defined}}

> The decision-maker's actual go/no-go and their name go in the front-matter sign-off block (Approved by), not here. This section recommends; the sign-off decides.

---

## 10. Revision History

> Mandatory final section. Note the extra **Approval** column: because the TSR is a sign-off-bearing record, each re-issue records who approved it. Beginner note: a TSR is often re-issued — for example, after a retest closes blocked or failed cases, a v0.1 "Do not proceed" report becomes a v1.1 "Proceed" report. Each re-issue is a version bump with a one-line note on what changed and who approved it, so readers can tell the two apart at a glance.

| Version | Date | Author | Description of Change | Approval |
|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft | {{Pending}} |
| {{1.0}} | {{YYYY-MM-DD}} | {{Author}} | {{First issued report — verdict: Do not proceed (open critical DEF-12)}} | {{Approver}} |
| {{1.1}} | {{YYYY-MM-DD}} | {{Author}} | {{Re-issued after retest — DEF-12 fixed-and-verified, OQ-1 closed; verdict: Proceed with limitations}} | {{Approver}} |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — the references in §1.4 are what make the report verifiable)
- §2 Test Results Summary
- §3 Requirement Verification Status
- §4 Defect Summary
- §7 Evaluation (the conclusion must be anchored to the plan's exit criteria)
- §9 Recommendation
- §10 Revision History

**Optional sections** (include if relevant):
- §5 Deviations from Plan (omit only if the cycle ran exactly to plan — rare; usually keep it, even if to say "no deviations")
- §6 Residual Risks (omit only if every requirement is Verified and zero defects are open/deferred — also rare; honesty usually means at least one RR-N)
- §8 Open / Follow-Up Items (track in your tracker instead if you prefer, but keep blocking items visible to the decision-maker somewhere)

**Identifier conventions**:
- TI-N: test items (build / release candidate / version) — **consumed** from the companion Test Plan, not coined here
- TC-N: test cases — **consumed** from the Test Case Specification, not coined here
- REQ-N / SRS §: requirement ids — **quoted** from the SRS for the §3 verification matrix
- DEV-N: deviations from plan (report-local)
- RR-N: residual risks (report-local)
- OQ-N: open / follow-up items (report-local)

These prefixes enable cross-document traceability: the TSR closes out the Test Plan (TP-N), reports on its test items (TI-N) and test cases (TC-N), and reports the verification status of SRS requirements (REQ-N). Coin only DEV-N, RR-N, and OQ-N here; reference the rest.

**Tailoring**:
- The TSR is a record — write it after execution, and re-issue (version bump in §10) whenever a retest changes the verdict. A frozen "Do not proceed" report next to a later "Proceed" report, both versioned, tells the real story.
- Keep §4 a summary; link to the defect tracker for detail. The TSR should fit on a few screens — the tracker holds the long tail.
- Every claim in §9 Recommendation must already appear in §2–§7. If you find yourself introducing new evidence in the recommendation, it belongs in an earlier section.
- **Solo developer / small team:** collapse aggressively. Merge §5/§6 into a single "Deviations and residual risks" list; use qualitative L/M/H for risk; let the defect "tracker" be a GitHub issues label or even a list in §4; keep the per-case log as the test runner's own output. What you must NOT drop, even solo: the §7 evaluation against pre-agreed exit criteria and the §9 verdict — those are the discipline that stops "it mostly works" from becoming "ship it." If you are both author and approver, say so in the sign-off rather than leaving it blank.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29119-3:2021 standard, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products; confirm section content and naming against your licensed copy of the standard before any contractual, certification, or audit use.
