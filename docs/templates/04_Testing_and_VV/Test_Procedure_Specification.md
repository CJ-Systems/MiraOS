# Test Procedure Specification Template

> **Template purpose:** Lightweight Test Procedure Specification (TPS) structure following ISO/IEC/IEEE 29119-3:2021 (test documentation). A TPS is the *runnable script* half of test documentation — it says HOW to run one or more test cases, step by step, in the order a tester actually performs them. Use this template when you have test cases (the WHAT) and now need a repeatable, executable procedure (the HOW). Replace `{{placeholder}}` content with procedure-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** After you have a Test Plan and a Test Case Specification, when you need any qualified tester to be able to sit down, follow the steps, and produce the same result. A Test Case Specification says *what* to test (inputs, expected results); this document says *how* to execute it — the environment, the setup, the ordered steps, the evidence to capture, and the cleanup. In 29119-3 these are deliberately separate documents: the case describes the test, the procedure makes it runnable.
>
> **Companion standard:** ISO/IEC/IEEE 29119-3:2021 — Software and systems engineering — Software testing — Part 3: Test documentation (Test Procedure Specification content).
>
> **Status of this template:** Lightweight Test Procedure Specification structure following ISO/IEC/IEEE 29119-3:2021 (Test documentation), reduced for solo/small-team use. It is a lightweight skeleton derived from public sources — the standard is paywalled, so this template paraphrases the public structure of a TPS (its section set) and reproduces NO normative text. Verify section content against the full standard for enterprise, regulated, safety-critical, or contractual contexts. This is an instance/record-leaning document (a runnable procedure), so the section set is kept deliberately focused rather than padded to a fixed 8–12 count.

---

# Test Procedure Specification — {{System Name}}

| Field | Value |
|---|---|
| Document ID | TPS-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29119-3:2021 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Test item(s) | {{Build / version / component(s) under test, with identifiers}} |
| Traces to | {{Test Case IDs (TC-N), test plan, or requirements this procedure exercises}} |
| Procedure type | {{Manual / Automated / Hybrid}} |
| Estimated duration | {{Wall-clock time for one full run}} |

---

## 1. Introduction

> This is the HOW-to-run document. It does not invent new tests — it makes existing test cases executable in a repeatable order. A **test case** is one logical test (this input should produce that result); a **test procedure** groups one or more test cases into an ordered, executable sequence with setup, steps, and teardown. Many cases can share one procedure, and one procedure can chain several cases so you do not repeat the same setup. This first section folds together the purpose, scope, definitions, and references — the same opening shape used by the SRS and SDD in this pack so all the documents read alike.

### 1.1 Purpose

> One paragraph stating what this TPS specifies and which test plan and test cases it serves. The point of the procedure is **repeatability** — a different tester, on a different day, starting from the same state, should get a comparable result.

{{This document specifies the executable procedure(s) for running the test cases listed in §2 against {{System Name}}. It defines the environment, setup, ordered steps, evidence to record, and cleanup so that any qualified tester can run the procedure and produce comparable results. It is the *how-to-run* document: the matching Test Case Specification states *what* each test checks (inputs and expected outcomes); the Test Log and Incident Report capture *what actually happened* once this procedure is executed.}}

### 1.2 Scope

> Say what this procedure covers and what it explicitly excludes. Name the **test level** — the stage of testing defined by how much of the system is assembled (unit, integration, system, acceptance) — and note anything deliberately handled elsewhere so a reader does not assume this procedure does more than it does.

In scope:
- Test level: {{unit / integration / system / acceptance}}
- {{The test cases / behaviours this procedure exercises}}
- {{The test item(s) it runs against — see §2}}

Out of scope (covered elsewhere):
- {{e.g. Performance soak / load runs — covered by {{ref}}}}
- {{e.g. Security penetration testing — covered by {{ref}}}}
- {{Test cases not exercised by this procedure — see §2}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Define every term that, if misread, would lead a tester to run the procedure wrong. The rows below pre-seed the concepts this document leans on most — keep, edit, or delete.

| Term | Definition |
|---|---|
| Test Procedure Specification (TPS) | The runnable-script half of test documentation: it says **how** to run one or more test cases, step by step, in the order a tester performs them. Tracked here at procedure granularity as **TP-N**. |
| Test case | One logical test — given some inputs and preconditions, what result is expected. Defined in the Test Case Specification and referenced here as **TC-N**. |
| Test procedure | An ordered, executable sequence that runs one or more test cases, with setup, steps, and teardown. One procedure can chain several cases to avoid repeating setup. |
| Test item | The specific thing being tested — a build, version, service, or component, with identifiers. Recording the exact test item is what makes a later pass/fail meaningful: "it passed" means nothing without "on what version." Referenced as **TI-N** where the test plan tracks items. |
| Precondition / setup | The state the system must be in **before** execution step 1 (data loaded, accounts created, services up). Setup is the ordered work that establishes it. |
| Postcondition / teardown (cleanup) | The work that restores the pre-run state afterward so the next run starts clean and shared environments are not polluted. |
| Expected result vs. actual result | The **expected** observation is written **in advance**, per step. The **actual** result is what the tester records during the run. A mismatch is what gets escalated to an incident/anomaly report. |
| Evidence (objective record) | Artifacts that prove a step's outcome to someone who was not in the room: logs, screenshots, measured values, exported files, timestamps, environment snapshots. A result with no evidence is an opinion. |
| Repeatability / reproducibility | The property that a different tester running the procedure from the same starting state gets the same result. Hidden assumptions ("obviously you log in first") are the enemy; the procedure must spell them out. |
| Verification & Validation (V&V) | **Verification** asks "did we build the thing right" (does it meet the spec). **Validation** asks "did we build the right thing" (does it meet the real need). A test procedure is a unit of verification evidence feeding the larger V&V picture. |
| {{Term}} | {{Definition}} |

### 1.4 References

> List the documents this procedure depends on or traces to. Categorized for readability, as in the SRS. The Test Case Specification and the System/build under test are the two that *must* be pinned — a procedure with no named cases and no named build is not reproducible.

Test documentation:
- {{TP-PROJECT-ID-001 / path}} — Test Plan this procedure serves
- {{path/to/test-case-spec}} — Test Case Specification defining the TC-N exercised here
- {{path/to/test-log}} — where run results are recorded (separate document)

Requirements and design:
- {{SRS-PROJECT-ID-001 / path}} — requirements ultimately verified
- {{SDD-MODULE-ID-001 / path}} — design of the item(s) under test

System / build under test:
- {{Build / version / commit / image identifier}} — see §2 Test Items

Tooling:
- {{Test runner / capture tool / monitor docs}}

External standards:
- ISO/IEC/IEEE 29119-3:2021 — Software testing, Part 3: Test documentation (Test Procedure Specification content)

---

## 2. Procedure Scope and Test Items

> This is the manifest: WHAT this procedure exercises and AGAINST WHAT. A procedure is only meaningful if you pin down the exact thing under test — "it passed" is worthless without "on which build." The first table is the list of procedures and the test cases each covers; the second names the exact test item(s) with identifiers a future reader can reproduce (a commit hash and a config flag, not "the latest version").

### 2.1 Procedures and covered test cases

> One **TP-N** row per procedure documented here. A single TPS may document one or more procedures; if several are chained (procedure B assumes the state procedure A leaves), say so in the notes.

| Procedure ID | Test case(s) covered (TC-N) | Objective (one line) | Type (manual / automated) |
|---|---|---|---|
| TP-1 | {{TC-1, TC-2}} | {{What this procedure verifies in one line}} | {{Manual / Automated / Hybrid}} |
| TP-2 | {{TC-5}} | {{...}} | {{...}} |
| {{TP-N}} | {{TC-N ...}} | {{...}} | {{...}} |

Procedure relationships:
- {{e.g. TP-2 assumes the logged-in state TP-1 leaves; run TP-1 first, or perform TP-1's setup steps (§4) standalone.}}
- {{e.g. TP-1 and TP-3 are independent and may run in any order.}}

### 2.2 Test items

> Name the exact build/version/component(s) under test, with identifiers. State configuration flags explicitly — a flag flipped differently is the most common reason two testers get different results.

| Item ID | Test item | Identifier | Notes |
|---|---|---|---|
| TI-1 | {{Service / component name}} | {{version tag / commit hash / image digest}} | {{config flags, feature toggles in effect}} |
| TI-2 | {{Dependency or fixture under test}} | {{version}} | {{...}} |
| {{TI-N}} | {{...}} | {{...}} | {{...}} |

Test cases explicitly NOT covered here:
- {{TC-N}} — {{why it is out of scope for this procedure, and where it is covered}}

---

## 3. Required Environment

> This is the **precondition inventory** — everything that must exist before setup begins, so a different tester on a different day can stand up the same conditions. The reason results differ between testers is almost always an undocumented environment difference, so state configuration values explicitly rather than "configure as usual." Use a table per subsection where it helps.

### 3.1 Hardware / platform

| Item | Requirement |
|---|---|
| {{Machine / host}} | {{spec, OS family, arch}} |
| {{Network}} | {{access to {{endpoint}}, offline-only, etc.}} |
| {{...}} | {{...}} |

### 3.2 Software and versions

> Pin versions. "Latest" is not a version. Include the system-under-test build from §2.

| Component | Version | Notes |
|---|---|---|
| Operating system | {{OS x.y}} | {{...}} |
| Runtime / interpreter | {{e.g. language runtime x.y}} | {{...}} |
| Dependencies | {{lib@version, ...}} | {{from lockfile {{path}} if applicable}} |
| System under test | {{TI-1 build from §2}} | {{...}} |

### 3.3 Test data

> The datasets, fixtures, and seed values the procedure needs — and where they come from, so they can be regenerated. Note whether data is loaded fresh each run or assumed pre-existing.

| Dataset / fixture | Source | Loaded by | Notes |
|---|---|---|---|
| {{seed dataset}} | {{path / generator script}} | {{setup step SETUP-N}} | {{size, key records}} |
| {{...}} | {{...}} | {{...}} | {{...}} |

### 3.4 Tools and instrumentation

> Test runners, capture tools, monitors — anything that runs the steps or records evidence.

| Tool | Purpose | Version |
|---|---|---|
| {{test runner}} | {{executes automated steps}} | {{x.y}} |
| {{capture tool}} | {{collects logs / screenshots — see §6}} | {{x.y}} |
| {{...}} | {{...}} | {{...}} |

### 3.5 Accounts, credentials, and access

> Roles and permissions the procedure needs. **Never inline real secrets** — reference a secret store and the role required, not the value.

| Role / account | Permissions needed | Source |
|---|---|---|
| {{test user}} | {{read/write on {{resource}}}} | {{secret store ref — not the value}} |
| {{admin/service account}} | {{...}} | {{...}} |

---

## 4. Setup Steps

> Setup is everything that is NOT the thing you are testing but must be true for the test to be valid — logging in, loading data, starting services, setting flags. Keeping setup separate from execution is what lets you tell a **setup failure** ("the test never really ran") apart from a **genuine defect** ("the test ran and the system misbehaved"). These ordered actions move the environment from "nothing prepared" to "precondition met, ready for execution step 1." Each step states the action, the expected state after it, and a quick check that confirms that state.

| Step ID | Action | Expected state after | How to confirm |
|---|---|---|---|
| SETUP-1 | {{Start services / bring up environment}} | {{all services healthy}} | {{health endpoint returns 200 / process list shows N processes}} |
| SETUP-2 | {{Load test data from §3.3}} | {{N records present}} | {{count query returns N}} |
| SETUP-3 | {{Create / authenticate test account from §3.5}} | {{session valid for role X}} | {{whoami / token introspection shows role X}} |
| SETUP-4 | {{Set configuration flags to baseline}} | {{flags at known values}} | {{config readout matches §3.2}} |
| {{SETUP-N}} | {{...}} | {{...}} | {{...}} |

**Entry criteria met (checkpoint):** before running §5, confirm all of:
- [ ] {{All §3 environment requirements satisfied}}
- [ ] {{Test data loaded (SETUP-2 confirmed)}}
- [ ] {{Test account authenticated with required role (SETUP-3 confirmed)}}
- [ ] {{Configuration flags at baseline (SETUP-4 confirmed)}}
- [ ] {{Evidence capture (§6) is running / ready}}

> If any entry-criterion check fails, do **not** start execution — a failure here is a setup failure, not a defect. Fix the environment and re-confirm before proceeding.

---

## 5. Execution Steps

> This is the heart of the document. Each row is **one observable action with its expected result written down in advance**; the tester records the actual result during the run, and any mismatch becomes an incident. Writing expected results *before* running is the discipline that prevents "looks fine to me." The Actual Result and Pass/Fail columns are filled in *during* a run — leave them as `{{ }}` in the template so each run starts from a clean copy.
>
> When authoring steps:
> - **Make each step atomic** — one action, one checkable result. If a step has two checks, split it.
> - **Avoid ambiguous verbs.** "Verify the page loads" → "confirm HTTP 200 **and** that the heading text reads `{{X}}`." A second tester must reach the same verdict from the same observation.
> - **Reference the test case** (TC-N) each block of steps exercises, so a reader can trace a step back to the case it implements.
> - **Mark decision/branch points explicitly** — say which step to go to next on each outcome.
> - **Never bury a setup action inside an execution step.** If a step needs the system in a state, that state belongs in §4 or as an explicit, labelled sub-step — not silently mixed into the thing under test.
> - **Automated procedures** may reference a script or command per step rather than manual clicks — but the Expected Observation and Evidence Required columns still apply to the script's output.

**Exercises:** {{TC-1, TC-2}} (state which test case each block below implements)

### TC-1 — {{Case objective in one line}}

| Step ID | Action | Expected observation | Evidence required | Actual result | Pass/Fail |
|---|---|---|---|---|---|
| STEP-1 | {{Manual: click {{control}} / Automated: run `{{command}}`}} | {{Confirm HTTP 200 and heading reads `{{X}}`}} | {{screenshot + response body capture}} | {{ }} | {{ }} |
| STEP-2 | {{Submit input `{{value}}` to `{{field/endpoint}}`}} | {{Response field `{{name}}` equals `{{expected}}`}} | {{exported response JSON}} | {{ }} | {{ }} |
| STEP-3 | {{Decision point: inspect `{{state}}`}} | {{If `{{A}}` → go to STEP-4; if `{{B}}` → go to STEP-6}} | {{log excerpt showing branch taken}} | {{ }} | {{ }} |
| {{STEP-N}} | {{...}} | {{...}} | {{...}} | {{ }} | {{ }} |

### TC-2 — {{Case objective in one line}}

| Step ID | Action | Expected observation | Evidence required | Actual result | Pass/Fail |
|---|---|---|---|---|---|
| STEP-7 | {{...}} | {{...}} | {{...}} | {{ }} | {{ }} |
| {{STEP-N}} | {{...}} | {{...}} | {{...}} | {{ }} | {{ }} |

> Step IDs are continuous across the whole procedure (STEP-1 … STEP-N), not restarted per test case, so a Test Log or Incident Report can cite an exact step unambiguously (e.g. "STEP-3 failed").

---

## 6. Data Recording

> Evidence is what proves the outcome to someone who was not watching — and what lets the run be audited or reproduced later. A result with no evidence is an opinion. This section defines the objective record captured during a run and where it lands. Keep it consistent with the **Evidence Required** column of §5 — every artifact named there should have a home defined here. This document *produces* the evidence; the separate Test Log and Incident Report (29119-3) *interpret* it.

### 6.1 What to record

| Artifact | When | Mandatory / on-failure | Format & naming convention |
|---|---|---|---|
| Run log | Whole run | Mandatory | {{`{{run-id}}.log`}} |
| Step screenshots | Per manual step | Mandatory | {{`STEP-N_{{run-id}}.png`}} |
| Measured values | Per measurement step | Mandatory | {{recorded in §5 Actual Result column + `{{run-id}}-values.csv`}} |
| Exported files / responses | Steps that emit data | Mandatory | {{`STEP-N_{{run-id}}.json`}} |
| Environment snapshot | Once, at SETUP completion | Mandatory | {{`{{run-id}}-env.txt` — versions from §3.2, config from §3.4}} |
| Timestamps | Start, each step, end | Mandatory | {{ISO 8601 in the run log}} |
| Stack traces / core dumps | On failure | On-failure-only | {{`STEP-N_{{run-id}}-failure.txt`}} |
| {{...}} | {{...}} | {{...}} | {{...}} |

### 6.2 Where artifacts are stored

- **Storage location:** {{path / bucket / artifact store}}
- **Run identifier:** {{`{{run-id}}` convention — e.g. `{{TP-N}}-{{YYYY-MM-DD}}-{{seq}}`}}
- **Test-log reference:** {{the run's row/ID in the Test Log, linking these artifacts to the recorded verdict}}

> Note: evidence captured here is **kept**, not cleaned up. The cleanup in §7 restores the environment but must preserve these artifacts — they are the whole point of the run.

---

## 7. Cleanup Steps

> Cleanup is what makes the procedure safe to run again and safe to run on a shared environment. Without it, run N+1 inherits the leftovers of run N (stale data, half-open sessions, flipped flags) and results stop being comparable. These ordered teardown actions restore the environment to its pre-run state. Each step states the action and the expected restored state. Use IDs in their own consistent series (CLEAN-N) so a step can be cited if cleanup itself fails.

| Step ID | Action | Expected restored state |
|---|---|---|
| CLEAN-1 | {{Delete / roll back test data loaded in SETUP-2}} | {{datastore back to baseline record count}} |
| CLEAN-2 | {{Log out / revoke test session from SETUP-3}} | {{no active test sessions}} |
| CLEAN-3 | {{Return configuration flags to baseline}} | {{flags match the pre-run values}} |
| CLEAN-4 | {{Stop / restart services as needed}} | {{services in pre-run state}} |
| CLEAN-5 | {{Remove temporary artifacts (NOT the §6 evidence)}} | {{scratch dirs cleared; evidence retained}} |
| {{CLEAN-N}} | {{...}} | {{...}} |

> **Evidence preservation:** CLEAN-5 must not delete anything stored under §6. If cleanup and evidence share a directory, move evidence out *before* clearing scratch space.

**Exit state (checkpoint):** after cleanup, the environment the next run starts from is:
- {{Test data: {{baseline state}}}}
- {{Sessions/accounts: {{none active / reset}}}}
- {{Configuration: {{baseline flags}}}}
- {{Services: {{running at baseline / stopped, as appropriate}}}}
- {{Evidence: retained at {{§6 storage location}}}}

---

## 8. Exceptions and Anomaly Handling

> This is the path that is NOT "everything passed." The most valuable moments in testing are the failures, so the procedure must say how to handle them rather than leaving the tester to improvise — improvisation destroys repeatability and loses evidence. Cover how to record a blocked or failed step, when to stop vs. continue, how to raise an incident and which STEP-N to cite, and any safe-state action to take on failure.

### 8.1 When a step fails or is blocked

> A **failed** step ran and the actual result did not match the expected. A **blocked** step could not run at all (a dependency was down, a precondition was missing).

- Mark the step **Fail** (or **Blocked**) in the §5 Pass/Fail column and record the actual result.
- Capture the on-failure evidence listed in §6 (stack traces, core dumps, extra logs) **in addition** to the normal artifacts.
- Note the timestamp and the exact STEP-N in the run log.

### 8.2 Stop vs. continue

> Decide in advance whether a given failure halts the whole procedure or only skips the steps that depend on it. State the rule per step or per block so the tester does not have to guess mid-run.

| Failure at | Action | Rationale |
|---|---|---|
| {{A setup step (SETUP-N)}} | **Stop.** The test never validly started. | {{Setup failure → invalid run, not a defect.}} |
| {{STEP-N where later steps depend on its output}} | **Stop dependent steps**, continue independent ones if any. | {{Avoid cascading false failures.}} |
| {{STEP-N that is independent}} | **Record and continue.** | {{One failure should not mask other results.}} |

### 8.3 Setup failure vs. genuine defect

> This distinction matters because the two route to different places. A **setup failure** means the test was invalid — fix the environment and re-run; it does not get an incident report against the product. A **genuine defect** means the test ran correctly and the system behaved wrong — that gets an incident/anomaly report.

- **Setup failure** (test invalid): a §4 entry-criterion was not actually met, a dependency was misconfigured, test data was wrong. → Fix, re-confirm §4 entry criteria, re-run. Note it in the run log; do **not** file a product defect.
- **Genuine defect** (system wrong): §4 entry criteria were met, the step ran, the actual result did not match the expected. → Raise an incident.

### 8.4 Raising an incident / anomaly report

- File against the Incident/Anomaly Report (29119-3), citing: the **STEP-N** that failed, the **TC-N** it exercises, the **test item (TI-N / build)** from §2, the expected vs. actual result, and the §6 evidence references.
- {{Severity / priority assignment rule, if your process defines one}}.

### 8.5 Safe-state / rollback on failure

- On failure, leave the system in a safe state before investigating: {{e.g. stop in-flight jobs, revoke elevated sessions, do not leave half-written data in shared stores}}.
- {{Any rollback action specific to this procedure}}.
- Then proceed to the relevant §7 cleanup steps (failures still require teardown so the next run is clean).

---

## 9. Open Questions

> A half-finished procedure is honest if it says where it is half-finished — undocumented uncertainty is what bites a later tester. List aspects still unresolved, each with what is blocking it and who must decide. Use OQ-N IDs. Resolve and remove as the procedure matures; optionally keep a "Resolved" subsection for traceability, as the SDD does.

### 9.1 Open

- **OQ-1** {{e.g. dependency `{{X}}` is not yet pinned to a version}} — {{blocking: awaiting release of {{X}} x.y; decide: {{owner}}}}
- **OQ-2** {{e.g. TC-N's expected result is still disputed}} — {{blocking: requirement {{REQ}} ambiguous; decide: {{owner}}}}
- **OQ-3** {{e.g. STEP-N is manual but should be automated}} — {{blocking: no runner for {{tool}} yet; decide: {{owner}}}}
- **OQ-4** {{e.g. evidence-retention policy not yet decided}} — {{blocking: storage/cost policy TBD; decide: {{owner}}}}

### 9.2 Resolved (recorded for traceability)

- **OQ-0** {{Question}}: {{Resolution and date}}.

---

## 10. Revision History

> Every substantive change to a procedure gets a version bump and a line here — because a test result is only meaningful against a known procedure version, and "we changed the steps but did not record it" silently invalidates every prior run's comparability.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — Purpose, Scope, Definitions, References)
- §2 Procedure Scope and Test Items (a procedure with no named cases and no named build is not reproducible)
- §3 Required Environment
- §4 Setup Steps
- §5 Execution Steps
- §7 Cleanup Steps
- §10 Revision History

**Optional sections** (include if relevant):
- §6 Data Recording (fold into §5's Evidence column for a tiny throwaway run, but keep it for anything anyone else will read)
- §8 Exceptions and Anomaly Handling (recommended for any procedure run on a shared environment, or where failures route to an incident process)
- §9 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (for cross-document traceability):
- **TP-N**: a test procedure documented here (one TPS may document several). Procedures trace upward to the test cases they exercise and to test items / requirements.
- **TC-N**: a test case from the Test Case Specification that a procedure runs. Steps cite the TC-N they implement.
- **TI-N**: a test item (build / version / component) under test, matching the Test Plan's item IDs.
- **STEP-N**: an individual execution step, continuous across the whole procedure, so a Test Log or Incident Report can cite the exact step that passed or failed.
- **SETUP-N / CLEAN-N**: setup and cleanup steps, kept in their own series so a teardown step can be cited if cleanup itself fails.
- **OQ-N**: open questions.

These prefixes let a procedure trace **upward** (STEP-N → TC-N → TI-N / requirement) and let downstream records (Test Log, Incident Report) trace **back down** to the exact step.

**Tailoring**:
- The section headers follow the 29119-3 TPS shape but are guidance, not requirements. Add or remove subsections as the procedure needs.
- Keep the procedure focused on HOW to run — the WHAT (inputs, expected results at the case level) belongs in the Test Case Specification, and the results of a run belong in the Test Log / Incident Report. Don't duplicate them here.
- **Solo developer / small team:** collapse aggressively. A one-procedure TPS can be a single page: keep §1.1 Purpose (one line), §2 (which TC-N, which build), §3 as a short bullet list, fold setup/cleanup into §5 as the first and last steps, and keep §5 and §10. Drop §6, §8, and §9 until a second person needs to run it or a result needs auditing. The moment someone *else* runs the procedure, or a result has to be defended later, promote the collapsed sections back.
- One run = one filled-in copy. Keep this file as the blank master (Actual Result / Pass-Fail columns empty); copy it per run and fill the columns, or record results in the Test Log against `{{run-id}}`.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29119-3:2021 standard, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
