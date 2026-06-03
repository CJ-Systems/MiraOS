# Test Log Template

> **Template purpose:** Lightweight Test Log structure inspired by ISO/IEC/IEEE 29119-3 (the "test execution log" work product). Use this template to capture, as a factual record, what actually happened when a set of tests was run — one row per run, plus the evidence and anomalies attached to each. Replace `{{placeholder}}` content with run-specific text. Section guidance (in blockquotes) can be deleted once the section is written, but the table headers are meant to stay.
>
> **When to use:** Once you have a Test Plan (TP-N) and test cases (TC-N) and you actually start *running* them. The Test Log sits downstream of the Test Plan: the Plan says what will be tested and how; the Test Log says what happened when a session was run — which build, in which environment, with which result, and what (if anything) went sideways. Open one when you begin executing and append to it as testing proceeds. For a single small change a one-page log with two or three rows is fine; for a release it grows.
>
> **Companion standard:** ISO/IEC/IEEE 29119-3:2021 — Software and systems engineering — Software testing — Part 3: Test documentation (the "Test execution log" and "Test incident report" work products). The older IEEE 829-2008 ("Standard for Software and System Test Documentation") is the legacy predecessor and called the equivalent artifact a "Test Log"; 29119-3 superseded it. This document is the *record* companion to the Test Plan (TP-N) — the Plan says what will be tested and how; the Test Log says what actually happened when a test session was run.
>
> **Status of this template:** Lightweight skeleton assembled from publicly available descriptions of ISO/IEC/IEEE 29119-3 (the "test execution log" / "test incident report" work products) and its legacy predecessor IEEE 829-2008. The full ISO/IEC/IEEE 29119-3 standard is paywalled and was **not** reproduced — this organizes the same kinds of execution-record sections in plain English without copying normative text. **Verify against the full standard for enterprise/regulated/safety-critical contexts.** This is an instance/record document: kept deliberately lean and execution-record-focused (a register of RUN-N records plus the evidence and anomalies attached to them), not a planning or analysis document — the plan lives in the Test Plan, the verdict lives in the Test Summary Report, and defect diagnosis lives in the Test Incident/Defect Report.

---

# Test Log — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | RUN-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29119-3:2021 (lightweight); legacy IEEE 829-2008 |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Test level(s) | {{Unit / Integration / System / Acceptance — or "mixed"}} |
| Related Test Plan | {{TP-PROJECT-ID-001 or path}} |
| Related Test Cases | {{path/to/test-case-spec — where TC-N are defined}} |
| Related Incident Report | {{path/to/incident-defect-report — where IR-N are diagnosed}} |
| Build(s) covered | {{version / commit / build ID(s) recorded in this log}} |
| Logging period | {{first run date}} – {{last run date}} |

---

## 1. Introduction

> Open the same way the SRS / SDD / Test Plan templates do, so the whole document pack reads consistently — but keep it short. This is a *record*, not a treatise: the introduction exists to tell a reader what they are looking at and which sibling documents the rest of the log points to.
>
> First, the three documents people confuse, because getting them straight is the whole point of this section. A **test plan** is written *before* testing — it says what will be tested and how. A **test log** (this document) is filled in *during and after a run* — it records what actually happened, verbatim. A **test summary report** is written *after* a whole campaign — it is the verdict ("good enough to ship?") across many runs. This document is the middle one: a factual record, not a judgement.

### 1.1 Purpose

> One paragraph. Beginner-facing: say plainly that this is the record of what happened, not the plan and not the verdict, and that it is meant to be appended to rather than rewritten.

{{This document is the factual record of what happened when the tests for **{{Project Name}}** were run. It is not the plan (that is the Test Plan, TP-{{PROJECT-ID}}-001) and not the verdict (that is the Test Summary Report). Each test session is captured as a **RUN-N** record with its result, the build it ran against, the environment, the evidence, and any anomalies observed. The log is meant to be *appended to* as testing proceeds, not rewritten: if something recorded turns out to be wrong, we add a correcting entry rather than overwriting history.}}

### 1.2 Scope

> Define what this log covers — which test level(s), which build(s) or release, and over what period — and, just as importantly, what it does *not*: detailed defect diagnosis and the overall pass/fail verdict live in sibling documents, not here. Also say what *kind* of log this is, because that decision changes how it accretes.

This log covers:
- **Test level(s):** {{Unit / Integration / System / Acceptance — or "mixed"}}
- **Build(s) / release:** {{which build IDs, commits, or release this log records}}
- **Period:** {{first run date}} – {{last run date}}

This log does **not** cover:
- **Defect diagnosis** — observed anomalies are *recorded* here (§4.1) and pointed at by **IR-N**; they are *diagnosed* in the Incident/Defect Report at {{path/to/incident-defect-report}}.
- **The pass/fail verdict** — whether the release is good enough lives in the Test Summary Report at {{path/to/test-summary-report}}; this log supplies it the raw numbers (§5).

This is a **{{one log per release / one log per test level / single rolling log}}**. {{State which, so a reader knows whether to expect this file to be sealed at release or to keep growing.}}

### 1.3 Definitions and Acronyms

> Define the terms a beginner trips on. A few standard ones are pre-seeded below because they recur throughout the log and are easy to get wrong — keep, edit, or delete, and add project-specific terms.

| Term | Definition |
|---|---|
| Run (RUN-N) | One execution session of one or more test cases against one build. A run has a start, an end, a who (tester or automated harness), and a where (environment). Each run is one RUN-N row in §2. |
| Build under test | The exact, identifiable snapshot of the software the run executed against — a version number, a git commit hash, or a build ID. A result is meaningless without it, because the next build may behave differently. |
| Pass / Fail / Blocked / Not Run | The four standard per-case outcomes. **Pass** = behaved as expected. **Fail** = produced the wrong result (a problem with the thing under test). **Blocked** = could not be run because something upstream stopped it (a problem *reaching* the test). **Not Run** = deliberately or accidentally not executed. |
| Evidence / artifact | The proof attached to a result — a screenshot, log file, console output, saved response, or run URL. Evidence is what lets someone *else* believe the result without re-running it. |
| Incident | An observed anomaly raised during a run ("something looked wrong"), tracked elsewhere as **IR-N**. An incident is not yet a confirmed defect — see §4.1. |
| Deviation | A departure from the documented test procedure during a run (a step skipped, reordered, or a workaround used). Recorded honestly because a result obtained off-script is a *different* result. |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> The log is a hub of pointers — make every pointer explicit. List the documents this log traces *to* (the plan it executes, where the test cases are defined, where incidents are diagnosed, the requirements being verified) and the external standard it follows.

| Ref | Document | What it provides |
|---|---|---|
| R1 | {{TP-PROJECT-ID-001 or path}} | The Test Plan being executed — what to test and how. |
| R2 | {{path/to/test-case-spec}} | The Test Case Specification — where **TC-N** are defined. This log references TC-N; it does not mint them. |
| R3 | {{path/to/incident-defect-report}} | The Incident/Defect Report — where **IR-N** are diagnosed. This log raises IR-N as observations; it does not diagnose them. |
| R4 | {{path/to/test-summary-report}} | The Test Summary Report — where the pass/fail verdict lives. Consumes the totals in §5. |
| R5 | {{SRS-PROJECT-ID-001 or path}} | The requirements being verified by these runs. |
| R6 | ISO/IEC/IEEE 29119-3:2021 (test execution log); legacy IEEE 829-2008 (test log) | The external standard this log is inspired by. |

---

## 2. Test Run Register (RUN-N)

> This is the spine of the document. Every time you sit down to run tests — or kick off an automated suite — you add **one RUN-N entry here first**, then fill in its case-level detail in §3 and any anomalies in §4. Think of this register as the index: a reader should be able to scan it and see every session at a glance, then drill into the sections below for detail.
>
> Two columns are **mandatory, not optional**: *build under test* and *environment*. A result without the exact build it ran against, and the environment it ran in, is not reproducible — and a result nobody can reproduce is not trustworthy. The same test can pass on one build and fail on the next, or pass on one machine and fail on another. Recording both is what turns "it worked for me" into evidence.
>
> Record times as wall-clock with a timezone if testers are distributed, so two runs logged "14:00" are not silently in different zones. For an automated run, the "tester" is the CI job or pipeline ID, and the evidence is the run URL / captured log rather than a screenshot.

| Run | Date / Time (start–end) | Tester / harness | Build under test | Environment | Test level | Cases run | Pass / Fail / Blocked / Not-Run | Incidents raised |
|---|---|---|---|---|---|---|---|---|
| RUN-1 | {{YYYY-MM-DD HH:MM–HH:MM TZ}} | {{name or CI job ID}} | {{version / commit}} | {{env ref — see §1.3 / §4.3}} | {{Unit / Integration / System / Acceptance}} | {{n}} | {{p / f / b / nr}} | {{IR-N list, or "none"}} |
| RUN-2 | {{YYYY-MM-DD HH:MM–HH:MM TZ}} | {{name or CI job ID}} | {{version / commit}} | {{env ref}} | {{level}} | {{n}} | {{p / f / b / nr}} | {{IR-N list, or "none"}} |
| {{RUN-N}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

> Each RUN-N above gets a per-case results table in §3 and (if anything went sideways) an entry in §4. **RUN-N is the only identifier this document owns** — TC-N, TI-N, and IR-N are defined and diagnosed in the sibling documents (see §1.4); this log only points at them.

---

## 3. Executed Test Cases and Results

> This is the heart of the evidence trail: one row per test case, per run. Group the rows under the run they belong to so the record stays anchored to a specific build and environment.
>
> Four rules a beginner should internalise here:
> - **(a) Use the controlled vocabulary, not free text.** The Result column must be exactly one of *Pass / Fail / Blocked / Not Run* (defined in §1.3). If results are free text ("kinda worked", "flaky"), you cannot count them, and the totals in §5 fall apart.
> - **(b) Every Fail and every Blocked needs a Notes entry.** For a Fail, also link the incident (IR-N) it triggered — a Fail with no incident raised is a gap in the record, not a clean result. For a Blocked, say what stopped it.
> - **(c) Evidence makes the result believable.** Require a link or path for any non-Pass result; recommend it for Pass too. Evidence is what lets a reviewer accept the result without re-running the test.
> - **(d) Record the *actual* observed result on a Fail**, not just the word "failed". "Expected X, got Y" is the useful record; "failed" tells a future reader nothing.

### 3.1 RUN-1 — {{build / commit}} — {{environment}}

| Test case | Run | Result | Start | End | Evidence (link / path) | Notes |
|---|---|---|---|---|---|---|
| TC-1 | RUN-1 | {{Pass / Fail / Blocked / Not Run}} | {{HH:MM}} | {{HH:MM}} | {{screenshot / log / URL}} | {{observed actual result; on Fail: "expected X, got Y" + IR-N}} |
| TC-2 | RUN-1 | {{Pass / Fail / Blocked / Not Run}} | {{HH:MM}} | {{HH:MM}} | {{screenshot / log / URL}} | {{notes}} |
| {{TC-N}} | RUN-1 | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

### 3.2 RUN-2 — {{build / commit}} — {{environment}}

| Test case | Run | Result | Start | End | Evidence (link / path) | Notes |
|---|---|---|---|---|---|---|
| TC-1 | RUN-2 | {{...}} | {{HH:MM}} | {{HH:MM}} | {{...}} | {{...}} |
| {{TC-N}} | RUN-2 | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

> Add one results sub-section per run. The per-run Pass / Fail / Blocked / Not-Run counts here roll up into the §2 register and ultimately into the separate Test Summary Report — so keep the controlled vocabulary clean enough to add up.

---

## 4. Incidents, Deviations, and Environment Events

> When tests run, three kinds of thing can go sideways, and in a lean record document they are really the same kind of thing — an anomaly attached to a run. They are kept in three clearly-labelled subsections below so the content maps cleanly to the standard, but they share one principle: **record what you observed, point to where it gets resolved, and do not diagnose it here.**

### 4.1 Incidents observed (link to IR-N)

> An **incident** is any observed anomaly raised during a run ("something looked wrong"). A **defect** is a confirmed flaw *after* triage. The difference matters: you record *that* something looked wrong and point to where it gets diagnosed — you do **not** decide here whether it is a real bug. That decision belongs in the Incident/Defect Report (where IR-N are diagnosed). The "Severity" column here is a first impression, captured at the moment of observation, and may change after triage.

| Incident (IR-N) | Run | Related test case (TC-N) | What was observed | Severity (first impression) | Status / where tracked |
|---|---|---|---|---|---|
| IR-1 | RUN-1 | TC-2 | {{what looked wrong — observed behaviour, not a diagnosis}} | {{Critical / High / Medium / Low}} | {{Open / Triaging — tracked in {{incident-report ref}}}} |
| {{IR-N}} | {{RUN-N}} | {{TC-N}} | {{...}} | {{...}} | {{...}} |

### 4.2 Deviations from procedure

> A **deviation** is when the run did not follow the documented test procedure exactly — a step skipped or reordered, a workaround used. Recording an off-script result honestly is what keeps the log trustworthy: a result obtained by a workaround is a *different* result, and a reader has the right to know the steps were not the ones the plan specified.

| Run | Test case affected | What was done differently | Why | Effect on the result's validity |
|---|---|---|---|---|
| RUN-1 | TC-3 | {{e.g., skipped step 4, used staging data instead of prod-like}} | {{why the deviation was necessary}} | {{e.g., result still valid / result suspect / re-run needed}} |
| {{RUN-N}} | {{TC-N}} | {{...}} | {{...}} | {{...}} |

### 4.3 Environment events

> An **environment event** is a tool, data, network, account, or configuration problem that affected a run — the box flaked, the test data was stale, an account locked. Distinguish this carefully from a real defect: an environment event is a problem *reaching* the test, not a problem in the thing under test. That is exactly the **Blocked vs. Fail** distinction from §1.3 — a case blocked by a flaky environment is **Blocked**, not **Fail**.

| Run | Event | Impact (blocked cases? invalidated results?) | Resolution / carried-forward |
|---|---|---|---|
| RUN-2 | {{e.g., test DB unreachable for 20 min}} | {{e.g., TC-5..TC-8 marked Blocked}} | {{e.g., resolved, re-run in RUN-3 / carried forward to OQ-N}} |
| {{RUN-N}} | {{...}} | {{...}} | {{...}} |

---

## 5. Run Summary

> This section adds up what the rows above already say. It is a **factual roll-up, not a verdict** — and saying so out loud matters, because the temptation is to let the log quietly become the Test Summary Report. The judgement ("is the release good enough to ship?") belongs in the Test Summary Report, which *reads* these numbers. Keep this section to arithmetic plus pointers.

| Run | Passed | Failed | Blocked | Not Run | Total cases | Incidents raised |
|---|---|---|---|---|---|---|
| RUN-1 | {{n}} | {{n}} | {{n}} | {{n}} | {{n}} | {{n}} |
| RUN-2 | {{n}} | {{n}} | {{n}} | {{n}} | {{n}} | {{n}} |
| **Totals** | {{n}} | {{n}} | {{n}} | {{n}} | {{n}} | {{n}} |

Short factual note for this period:
- **Outstanding blocked cases:** {{which cases are still Blocked and why — e.g., TC-5..TC-8 blocked by the RUN-2 environment event, see §4.3}}
- **Abandoned runs:** {{any run stopped part-way and why — e.g., RUN-2 abandoned after the DB outage}}
- **Cases still Not Run that the plan required:** {{which TC-N the plan expected but no run executed}}

> These totals are consumed by {{Test Summary Report ref}}; open incidents are tracked in {{Incident/Defect Report ref}}. This section does not interpret the numbers — it hands them on.

---

## 6. Open Questions

> A short list of unresolved items *about the log or the runs themselves* — **not** about the product. Product defects live in the Incident/Defect Report; this section is for things that affect whether *this record* is complete or trustworthy. Use the document pack's **OQ-N** convention. For a small log this section can legitimately be empty or omitted. Keep the append-only spirit: when an item is resolved, move it out or strike it through rather than silently deleting it.

- **OQ-1** — {{RUN-3 evidence link is missing; tester to attach.}}
- **OQ-2** — {{Environment for RUN-2 not fully recorded; can the build be reproduced from what we logged?}}
- **OQ-3** — {{TC-12 marked Blocked across all runs; is it ever going to be runnable this release?}}
- {{OQ-N}} — {{...}}

---

## 7. Revision History

> The standard pack closer, and the last section. For a *record* document this table does double duty: because a log is meant to be **added to, not rewritten**, the revision history is where structural changes to the *log itself* are noted — new columns, a corrected entry, a sealed-at-release marker. That is distinct from the run-by-run content, which simply accretes in §2–§4 without needing a new version bump for every run added.
>
> **A correction to a previously recorded result is a new revision-history row plus an added or annotated entry — never a silent overwrite.** If RUN-1 recorded TC-4 as Pass and it was actually Fail, you add a row here ("v0.3 — corrected TC-4 result for RUN-1; original entry annotated, see §3.1") and annotate the entry in place; you do not edit the original to read Fail as though it had always said so. This is what an append-only record means, and it is why even a log that "just accretes data" still keeps a revision history.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial log created |
| {{0.2}} | {{YYYY-MM-DD}} | {{Author}} | {{e.g., added RUN-2 and RUN-3; corrected TC-4 result for RUN-1 (entry annotated, not overwritten)}} |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — the log is a hub of pointers; the references in §1.4 are what make it traceable)
- §2 Test Run Register (the spine — every run is one RUN-N row, with build and environment mandatory)
- §3 Executed Test Cases and Results (the per-case evidence trail)
- §5 Run Summary (the factual roll-up the Test Summary Report consumes)
- §7 Revision History

**Optional sections** (include if relevant):
- §4 Incidents, Deviations, and Environment Events — keep the subsections that apply; if a clean run had no anomalies at all, a one-line "No incidents, deviations, or environment events recorded for this period" is enough.
- §6 Open Questions — omit for a small log, or track elsewhere if you prefer. Empty is fine.

**Identifier conventions**:
- **RUN-N** — test-execution records; one per run. **This is the only identifier this document owns.**
- **TC-N** — test cases (defined in the Test Case Specification / Test Plan; this log references them).
- **TI-N** — test items / builds under test (defined in the Test Plan; referenced here).
- **IR-N** — incidents / defect reports (owned and diagnosed in the Incident/Defect Report; raised as observations here).
- **OQ-N** — open questions about the log or the runs.

These prefixes let the log cross-reference cleanly with its sibling documents: a RUN-N row points at the TC-N it executed, the TI-N build it ran against, and any IR-N it raised — so a reader can trace a single result from the run, to the case, to the requirement (in the SRS), and to the defect (in the Incident/Defect Report).

**Tailoring**:
- The Test Log is one of three documents people confuse — keep the boundaries sharp. The *plan* (what/how) is the Test Plan; the *record* (what happened) is this log; the *verdict* (good enough?) is the Test Summary Report. When a section starts to feel like analysis or judgement, it has drifted into Test Summary Report territory — move it there.
- Decide the log's *shape* up front (§1.2): one log per release, one per test level, or a single rolling log. It changes whether the file gets sealed or keeps growing.
- **Solo developer / small team:** the whole log can collapse to §2 (the run register) plus §3 (the results) plus §7 (revision history). For a tiny change, a single RUN-1 row, its per-case results, and a one-line summary in §5 is a complete and honest record. Do not skip the build and environment columns even when working alone — they are what make a result reproducible by *future you*. For automated-only testing, the run register can be largely auto-generated from CI output, with this document holding the human-readable index and the deviations/incidents a machine cannot infer.
- The append-only discipline is the point of a record document, even solo: correct by adding, never by overwriting (see §7). It is cheap to do and it is the difference between a trustworthy log and a tidied-up story.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29119-3:2021 standard (and the formal test execution log / test incident report work products), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
