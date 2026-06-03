# Test Case Specification Template

> **Template purpose:** Lightweight Test Case Specification structure inspired by ISO/IEC/IEEE 29119-3 (test documentation). Use this template when you need to write down — precisely and repeatably — exactly how a single requirement gets proven: the preconditions, the inputs, the steps, the expected results, and the rule that decides PASS or FAIL. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once you have an SRS (the requirements) and a Test Plan (the strategy), and you are about to write the actual checks. A Test Case Specification sits downstream of the SRS (WHAT must be true) and the Test Plan (HOW we will test overall), and upstream of the execution record (the evidence that it passed). One file can hold a single test case or a small family of related cases; for a tiny change a single case fits on a page, for a release you accumulate many.
>
> **Companion standard:** ISO/IEC/IEEE 29119-3:2021 — Software and systems engineering — Software testing — Part 3: Test documentation.
>
> **Status of this template:** Lightweight extract aligned to ISO/IEC/IEEE 29119-3:2021 (test case specification content), reduced for solo/small-team use and folding the related test-procedure content in for convenience. ISO/IEC/IEEE 29119-3 is a paywalled standard — this template was built from the publicly documented section structure and SWEBOK Software Testing KA guidance, **not** from the standard's copyrighted text; verify section names and required content against the purchased standard before relying on it for regulated, contractual, or safety-critical work. The execution-record sections (Actual Results, Defects) are kept here for convenience but properly belong to a separate Test Execution / Results record under 29119-3.

---

# Test Case Specification — {{System Name}}

| Field | Value |
|---|---|
| Document ID | TC-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29119-3:2021 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Requirement(s) under test | {{REQ-NNN, REQ-NNN — IDs traced from the SRS}} |
| Test level | {{Unit / Integration / System / Acceptance}} |
| Test type | {{Functional / Performance / Security / Usability / Regression}} |
| Priority | {{High / Medium / Low}} |
| Automation status | {{Manual / Automated / To be automated}} |
| Related test plan | {{path/to/test-plan.md or N/A}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: state that this document specifies one or more test cases for the system, what each case is meant to verify or validate, and where it sits in the document chain. A Test Case Specification sits **below the SRS** (the WHAT — what the system must do), **below the Test Plan** (the strategy — what we will test and how), and **above the execution record** (the evidence that a case actually passed). It is the concrete, runnable bridge between a requirement and proof that the requirement is met.

This document specifies the test case(s) for **{{System Name}}** that verify or validate one or more requirements drawn from the SRS. Each case pins down the preconditions, inputs, procedure, expected results, and the objective rule that turns an observation into a PASS/FAIL verdict. It is the lowest-level "how do we prove this?" document in the testing chain.

> **Beginner note.** A *Test Case Specification* answers one question: **"exactly how do we prove this requirement is met, repeatably?"** Where the SRS says *what* must be true and the Test Plan says *how we will go about testing*, a test case is the precise, re-runnable check — written so that anyone, on any matching environment, reaches the same verdict.

### 1.2 Scope

> State what this specification covers and what it excludes. Be concrete: name the feature, the requirement IDs, and the test level(s). If this file holds a range of cases, say so (e.g., "covers TC-001..TC-020 for the login feature only"). Excluding things is as important as including them — call out what is tested elsewhere so a reader does not assume a gap is an oversight.

In scope:
- {{Feature / capability under test, e.g., "user authentication — login happy path and credential errors"}}
- {{Requirement IDs covered, e.g., "REQ-014, REQ-015, REQ-021"}}
- {{Test case range, e.g., "TC-001 .. TC-008"}}
- {{Test level(s), e.g., "System and Acceptance"}}

Out of scope (tested elsewhere or deferred):
- {{Excluded area, e.g., "Load/performance of the login endpoint — see the performance test suite"}} — {{reason / pointer}}
- {{Excluded area, e.g., "Password-reset flow"}} — {{covered by TC-030..TC-040}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Define the terms the rest of this document leans on, so a first-time reader is not lost. The seed rows below define the formal testing concepts used throughout — keep them, add project-specific terms as needed.

| Term | Definition |
|---|---|
| Test level | Where in the build the test runs — **unit** (one function/class), **integration** (modules working together), **system** (the whole running system), **acceptance** (the customer signs off). Each level catches a different class of defect. |
| Test type | The quality attribute under test — **functional** (does it do the right thing), **performance**, **security**, **usability**, **regression** (did a change break something that used to work). A case has both a level and a type. |
| Precondition | A state the system must already be in *before* the test starts (e.g., a registered account exists, the database is seeded). Distinct from an input — see §4 and §6. |
| Input | A value supplied *during* the test (a field value, a file, an API payload). See §6. |
| Expected result | What should be *observable* when the case behaves correctly (a screen shows X, a log records Y, a row is written). See §8. |
| Pass/fail criteria | The objective rule that converts observations into a verdict (PASS / FAIL / BLOCKED / NOT RUN). See §9. |
| Verification | "Did we build the thing right?" — does it meet the specification. Most unit/integration cases verify. |
| Validation | "Did we build the right thing?" — does it meet the user's actual need. Acceptance cases validate. |
| Traceability | The documented link from a test case back to the requirement it proves (and forward to any defect it surfaces). |
| {{Project term}} | {{Definition}} |

### 1.4 References

> List the upstream and governing documents. Make the requirement reference **explicit** — this is the upstream end of the traceability chain (requirement → test case → run → defect). Categorize as in the SRS/SDD exemplars.

Requirements under test (upstream traceability):
- {{SRS-PROJECT-ID-001}} — Software Requirements Specification for {{System Name}}
- {{REQ-NNN}} — {{requirement statement being verified}}
- {{FR-NNN}} — {{functional requirement being verified}}

Governing test documents:
- {{TP-PROJECT-ID-001 or path/to/test-plan.md}} — Test Plan governing this case
- {{TL-NNN}} — {{test level definition, if the plan enumerates levels}}

Environment and configuration:
- {{path/to/environment.md}} — {{test environment / build configuration}}
- {{path/to/fixtures/}} — {{test data / fixtures referenced by inputs}}

External standards:
- ISO/IEC/IEEE 29119-3:2021 — Software testing — Part 3: Test documentation (companion standard, paraphrased)

---

## 2. Test Case Identification

> This is the header-of-record for the case — the at-a-glance facts that let someone find it, run it, and know what it proves. The **Related Requirement ID** is what makes the case *traceable*: if it traces to nothing, ask whether the requirement is missing from the SRS, or whether the test itself is redundant. A case that proves nothing in the requirements is a candidate for deletion.
>
> If this file holds **many** test cases, repeat §2 through §12 once per case, and add a one-line index table of all cases at the top of the file for navigation (see the example index below the identification table).

| Field | Value |
|---|---|
| Test Case ID | TC-NNN |
| Title | {{short human-readable name, e.g., "Login with valid credentials"}} |
| Related Requirement ID(s) | {{REQ-NNN}} (the traceability link — never leave blank) |
| Test Level | {{Unit / Integration / System / Acceptance}} |
| Test Type | {{Functional / Performance / Security / Usability / Regression}} |
| Priority | {{High / Medium / Low}} |
| Automation status | {{Manual / Automated / To be automated}} |
| Author | {{Name / role}} |
| Status | {{Draft / Ready / Deprecated}} |

Optional index (use when this file holds several cases):

| Test Case ID | Title | Requirement(s) | Level | Type | Status |
|---|---|---|---|---|---|
| TC-001 | {{Login with valid credentials}} | {{REQ-014}} | {{System}} | {{Functional}} | {{Ready}} |
| TC-002 | {{Login rejects wrong password}} | {{REQ-015}} | {{System}} | {{Functional}} | {{Draft}} |
| TC-003 | {{Login locks account after N failures}} | {{REQ-021}} | {{Security}} | {{Security}} | {{Draft}} |

---

## 3. Objective

> State, in one or two sentences, **exactly which behavior or quality attribute this case exercises**, and whether it **verifies** (meets the specification) or **validates** (meets the user's actual need). Tie this back to the definitions in §1.3. Keep it to **one objective per case** — if you find yourself writing "and also...", that "also" is a second test case. A single-purpose case is easier to reproduce, easier to attribute a failure to, and easier to retire when its requirement changes.

{{This case }}{{verifies / validates}}{{ that ... — one precise sentence.}}

Example (filled, for shape): *"Verifies that a registered user supplying valid credentials is granted access (REQ-014), confirming the happy-path authentication behavior. This is a verification case — it checks behavior against the specification, not against an end-user's stated need."*

---

## 4. Preconditions

> List **everything that must already be true before the procedure begins** — the state, seed data, configuration, accounts, permissions, and environment facts that you are **not** going to set up as part of the test steps. Preconditions are pre-existing *state*; the values you type or send during the run are *inputs* (§6) — confusing the two is the classic cause of a non-reproducible, "works on my machine" test.
>
> Reproducibility lives or dies in this section. An unstated precondition is a hidden assumption, and a hidden assumption is a flaky test waiting to happen. Pin the **test environment** here too: build/version, OS, browser/runtime, and the dataset in use.

| # | Precondition | How to establish | Verified? |
|---|---|---|---|
| PC-1 | {{A registered account `{{username}}` exists with a known password}} | {{Run the seed script `seed_users.sql`}} | {{☐}} |
| PC-2 | {{The application is running on build {{build-id}} in the test environment}} | {{Deploy {{build-id}} to {{env}}}} | {{☐}} |
| PC-3 | {{No active session exists for `{{username}}` (logged out)}} | {{Clear sessions / use a fresh browser profile}} | {{☐}} |
| PC-4 | {{Test database seeded with the {{dataset-name}} fixture}} | {{Load `fixtures/{{dataset}}.json`}} | {{☐}} |

> **Beginner note.** A *precondition* is what is **already true** when the case starts; an *input* (§6) is what you **do** during the case. "User account exists" is a precondition. "Type `correct-password` into the password field" is an input. Keep the line between them sharp.

---

## 5. Test Items and Environment

> Name **what is under test** and **where it runs**, so a verdict can be attributed to a known build. The *test item* is the specific component, service, build number, or version of the system being exercised. The *environment* is the hardware, OS, runtime versions, network conditions, and external dependencies (real or stubbed/mocked).
>
> Pinning the build version is what lets you say *"this defect exists in v0.3.1"* rather than the useless *"it failed once."* If the environment is already fully captured in §4 Preconditions, keep this section short and cross-reference rather than duplicate.

Test item(s):
- {{Component / service under test, e.g., "Authentication service `auth-svc`"}}
- {{Build / version, e.g., "build {{build-id}} / v{{0.3.1}}"}}

Environment:
- {{Hardware / host, e.g., "test VM, 2 vCPU / 4 GB"}}
- {{OS and runtime, e.g., "Ubuntu 24.04, {{runtime}} {{version}}"}}
- {{Client, e.g., "Browser {{name}} {{version}}" or "API client {{tool}}"}}
- {{External dependencies and their mode, e.g., "Email gateway — STUBBED; payment API — MOCKED; database — REAL ({{dataset}})"}}
- {{Network conditions, if relevant, e.g., "no artificial latency"}}

> **Beginner note.** Saying which dependencies are *real* versus *stubbed/mocked* matters: a case that passes against a stubbed email service has **not** proven that real email delivery works. State the mode so the verdict's scope is honest.

---

## 6. Inputs

> Every value the operator (or the automation) **supplies during the run** goes here — field values, files, API payloads, timings, environment variables. This is distinct from §4 preconditions: inputs are what you **do** during the test; preconditions are what was already **true**. For data-driven cases that iterate over many rows, point at the dataset or fixture file rather than inlining hundreds of rows.

| Input | Value | Type/Format | Source |
|---|---|---|---|
| {{Username}} | {{`{{username}}`}} | {{string}} | {{Fixed (matches PC-1)}} |
| {{Password}} | {{`{{correct-password}}`}} | {{string (secret)}} | {{Fixture `fixtures/{{dataset}}.json`}} |
| {{Login request payload}} | {{`{ "user": "...", "pass": "..." }`}} | {{JSON}} | {{Generated from the two values above}} |
| {{Timestamp}} | {{request time}} | {{ISO-8601}} | {{Generated at run time}} |

> **Beginner note.** The **Source** column matters because a magic constant with no provenance is unreproducible. Say whether each value is **fixed** (a literal pinned in the case), **generated** (computed at run time), or **drawn from a fixture** (a named data file). A value nobody can re-derive is a value nobody can re-test.

---

## 7. Procedure

> The numbered, executable heart of the case. Number steps sequentially, **one observable action per step**, and give each step a *local* expected result — the checkpoint that confirms you are on track. The overall outcome lives in §8; these per-step results are the breadcrumbs that tell you *where* a case went wrong, not just *that* it did. Steps must be specific enough that a **different person** following them gets the same result.
>
> For automated cases, point at the script/path and keep the human-readable steps here as the **specification of record** — the script implements the steps; the steps define what the script is supposed to do.

| Step | Action | Expected Result (this step) |
|---|---|---|
| 1 | {{Navigate to the login page `/{{login}}`}} | {{The login form is displayed with username and password fields}} |
| 2 | {{Enter `{{username}}` into the username field}} | {{The field shows the entered value; no validation error}} |
| 3 | {{Enter `{{correct-password}}` into the password field}} | {{The field is masked; no validation error}} |
| 4 | {{Click "Sign in"}} | {{A request is sent; a brief loading state is shown}} |
| 5 | {{Observe the response}} | {{The user is redirected to the dashboard at `/{{home}}`}} |

> **Beginner note — the specification/procedure boundary.** Under ISO/IEC/IEEE 29119-3 the *test procedure* (these ordered steps) is treated as a **separate artifact** from the *test case specification* (objective, inputs, expected results, criteria). We fold the procedure in here for solo/small-team convenience. **But** if the same procedure is shared across many cases (e.g., "log in as admin" before twenty different cases), factor it out into its own procedure file and reference it, instead of copy-pasting steps into every case.

---

## 8. Expected Results

> The authoritative statement of correct behavior for the **whole case** — the per-case counterpart to the per-step results in §7. Describe **every observable the case asserts on**: UI state, returned values, persisted data changes, emitted logs or events, messages, and any quantitative limits. State quantitative limits as **concrete thresholds** ("response within 500 ms," "memory ≤ 256 MB"), never as "fast" or "reasonable."

On correct behavior, all of the following are observable:
- {{UI: the dashboard at `/{{home}}` is displayed showing the user's name}}
- {{Returned value: HTTP 200 with a session token in the response body/cookie}}
- {{Persisted data: a row is written to `sessions` with `user_id = {{id}}` and a future `expires_at`}}
- {{Log/event: an `auth.login.success` event is logged with the username and timestamp}}
- {{Quantitative limit (if applicable): the login response completes within {{500}} ms}}

> **Beginner note.** An expected result must be **observable** — you have to be able to point at *where to look* (a specific screen, a named log line, a named database row, a returned field). If you cannot say where the evidence appears, the case cannot be judged, and "expected result" is just a wish.

---

## 9. Pass / Fail Criteria

> The exact rule that turns the observations in §8 into a verdict — written so the verdict is **mechanical**, not a matter of opinion. Define every verdict value the project uses. Quantitative cases state the numeric threshold **here**, not in vague language.

Verdict rule for this case:
- **PASS** if and only if **every** expected result in §8 is observed.
- **FAIL** if **any** expected result in §8 is not observed (or a wrong result is observed).
- **BLOCKED** if a precondition in §4 could not be established, so the case could not be run as specified.
- **NOT RUN** if the case was deliberately skipped this cycle (record why).

Verdict-value definitions used by this project:

| Verdict | Meaning |
|---|---|
| PASS | All expected results met; the requirement is satisfied for this case. |
| FAIL | At least one expected result was not met; raise a defect (§12). |
| BLOCKED | Could not run — a precondition or environment dependency was unavailable. Not a failure of the system under test. |
| NOT RUN | Skipped this cycle; not yet judged. |

> **Beginner note.** The whole point of this section is to **remove judgment from the moment of execution.** Two people running the case should reach the **same verdict without debate**. If deciding PASS vs FAIL requires an argument, the criteria are too vague — sharpen §8 and §9 until the verdict is mechanical.

---

## 10. Postconditions

> The case's **exit contract** — the state the system should be in *after* the case completes (where possible, regardless of PASS or FAIL), and any teardown/cleanup needed so the **next** case starts clean. List what to delete, which sessions to close, which files to remove, which services to reset.

After this case completes:
- {{The created session may remain active (PASS) or no session exists (FAIL) — state which}}
- {{Teardown: delete any rows written to `sessions` during the run}}
- {{Teardown: log out / clear the browser profile}}
- {{Teardown: reset any stubbed service counters}}
- {{The {{dataset}} fixture is left unmodified (read-only during this case)}}

> **Beginner note.** Leftover state from one case is a common cause of a *later* case passing or failing for the wrong reason — a "phantom" result that has nothing to do with the code under test. Explicit postconditions keep cases **independent**, which is what lets you run them in any order and trust each verdict on its own.

---

## 11. Actual Results (Execution Record)

> This is the **execution record** — filled in **at run time**, not at design time, and typically by a different person than the case author. Record the **verdict**, the **date/time**, the **tester**, the exact **build/environment** used, and the **evidence** (logs, screenshots, captured output, links to the CI run). Use one row per run so the same case can be executed many times and you keep the history.

| Run date | Build/Env | Tester | Verdict | Evidence |
|---|---|---|---|---|
| {{YYYY-MM-DD HH:MM}} | {{build {{build-id}} / {{env}}}} | {{Name / role}} | {{PASS / FAIL / BLOCKED / NOT RUN}} | {{link to CI run / screenshot / log excerpt}} |
| {{YYYY-MM-DD HH:MM}} | {{build {{build-id}} / {{env}}}} | {{Name / role}} | {{...}} | {{...}} |

> **House-depth note.** Under ISO/IEC/IEEE 29119-3 this content properly belongs to a **separate Test Execution / Test Results record**, not the Test Case Specification — the specification is *designed once and stays stable*, while results *accumulate over many runs*. We keep the record here for solo/small-team convenience. If execution volume grows (many runs, many cases, CI history), split this out into its own results log and leave §1–§10 as the stable specification.

---

## 12. Defects

> The **forward end of the traceability chain** — every defect this case surfaced. Give each a stable **DEF-N** ID, a severity, a current status, and a link back to the §11 run that exposed it. This closes the loop: **requirement (§1.4) → test case (§2) → run (§11) → defect (§12)** — so anyone can trace a bug back to the requirement it violates.

| Defect ID | Summary | Severity | Status | Linked run |
|---|---|---|---|---|
| DEF-NNN | {{short description of the defect}} | {{Critical / High / Medium / Low}} | {{Open / Fixed / Won't fix}} | {{run date from §11}} |
| DEF-NNN | {{...}} | {{...}} | {{...}} | {{...}} |

> **Beginner note.** Like §11, this is **execution-time content**. In a larger process, defects live in a dedicated tracker (issue tracker / bug database) and this table is just a **pointer** into it — the DEF-N IDs match the tracker so you do not maintain two sources of truth.

---

## 13. Open Questions

> Unresolved questions about the **test case itself** — not about the product. Typical items: an ambiguous requirement that makes the expected result uncertain, missing test data, environment access not yet available, or an undecided "should we automate this?" Use **OQ-N** IDs and note what is blocking resolution and who must decide. Resolve and remove as work progresses.

- **OQ-1**: {{question, e.g., "REQ-021 does not state the lockout threshold N — expected result in §8 is uncertain until clarified"}} — {{what's blocking, who must decide}}
- **OQ-2**: {{question, e.g., "test account with the {{role}} permission not yet provisioned in the test env"}} — {{blocked on env access}}

> **Note.** An open question that affects the **pass/fail criteria** (§9) blocks the case from reaching status **Ready** — you cannot reliably judge a case whose correct outcome is still undefined.

---

## 14. Revision History

> Track every substantive change to the **specification** — the objective (§3), inputs (§6), procedure (§7), and pass/fail criteria (§9) — with a version bump. Note that the **execution records (§11) and defects (§12) are appended at run time** and do **not** require a version bump of the specification itself; only changes to the *design* of the case do.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — especially §1.4 References, which anchors traceability)
- §2 Test Case Identification (the Related Requirement ID is non-negotiable)
- §3 Objective
- §4 Preconditions
- §6 Inputs
- §7 Procedure
- §8 Expected Results
- §9 Pass / Fail Criteria
- §14 Revision History

**Optional sections** (include if relevant):
- §5 Test Items and Environment (fold into §4 if the environment is fully captured there; keep separate when builds/versions matter)
- §10 Postconditions (omit only for read-only cases with no side effects — but be honest about whether there really are none)
- §11 Actual Results / §12 Defects (these are execution-time content; keep them inline for solo/small-team work, or replace with a pointer to a separate results log / defect tracker as volume grows)
- §13 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- **TC-N**: test cases (e.g., TC-001)
- **REQ-N / FR-N**: the requirement under test, traced back to the SRS — the load-bearing traceability link; **every test case should trace to at least one requirement**
- **TL-N**: test level (if your Test Plan enumerates them)
- **DEF-N**: defects raised during execution
- **OQ-N**: open questions

These prefixes enable cross-document traceability: a requirement in the SRS (REQ-N) traces to a test case here (TC-N), which traces to an execution run (§11) and any defect (DEF-N) — so you can answer "is every requirement tested?" and "if this requirement changes, which tests must I revisit?"

**Tailoring**:
- The line between *specification* (designed once, stable: §1–§10) and *execution record* (filled each run: §11–§12) is the most important boundary in this template. Honor it: edit the spec via a version bump; append runs without one.
- One objective per case (§3). If a case is trying to prove two things, split it into two cases — small cases are easier to reproduce, attribute, and retire.
- **Solo developer / small team:** collapse aggressively. A single file can hold many cases (use the §2 index table). You can run the procedure (§7) straight from the steps without a separate procedure document, record results inline (§11), and skip a formal defect tracker (note defects in §12). The sign-off block can be a single name in all three rows, or struck through entirely — keep it only if a real review is happening.
- As you scale up, factor out in this order: shared procedures (§7) into their own files, then execution records (§11/§12) into a results log / defect tracker, leaving §1–§10 as the stable, version-controlled specification.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29119-3:2021 standard, not this lightweight version — including the separation of test case, test procedure, test data, test execution, and test result documentation into distinct work products. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
