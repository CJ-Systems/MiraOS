# Test Plan Template

> **Template purpose:** Lightweight Test Plan structure inspired by ISO/IEC/IEEE 29119-3 (test documentation). Use this template when you need to write down what you are going to test, how, and what "done" looks like — before you start testing. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once you have requirements (an SRS) and a design (an SDD) and you are deciding how to confirm the thing actually works. The Test Plan sits downstream of the SRS (WHAT the system must do) and the SDD (HOW it is built) — it documents HOW you will check that the built thing satisfies the requirements. For a tiny change you can keep this to a single page; for a release you can grow it.
>
> **Companion standard:** ISO/IEC/IEEE 29119-3 — Software and systems engineering — Software testing — Part 3: Test documentation. The older IEEE 829-2008 ("Standard for Software and System Test Documentation") is the legacy predecessor and you will still see it referenced in the wild; 29119-3 superseded it.
>
> **Status of this template:** Lightweight skeleton assembled from publicly available descriptions of 29119-3 and IEEE 829. The full ISO/IEC/IEEE standard is paywalled and was **not** reproduced — this organizes the same kinds of sections in plain English without copying normative text. Verify against the full standard for enterprise/regulated/safety-critical contexts.

---

# Test Plan — {{Project or Test Item Name}}

| Field | Value |
|---|---|
| Document ID | TP-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29119-3 (lightweight); legacy IEEE 829-2008 |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Test level(s) covered | {{Unit / Integration / System / Acceptance — or "all"}} |
| Related SRS | {{SRS-PROJECT-ID-001 or path}} |
| Related SDD | {{SDD-MODULE-ID-001 or path}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: what this document is for. It should establish that this is the plan for *how* the project (or a specific test item) will be tested, and that the actual results live elsewhere (test logs, reports) once testing runs.

{{This document specifies how {{Project or Test Item Name}} will be tested: what will be tested, at which levels and with which types of tests, what must be true before testing starts and before it can be called complete, and who is responsible. It is the plan, not the results — test logs and the test summary report capture what actually happened when the plan was executed.}}

### 1.2 Scope

> Define what this Test Plan covers and what it does not. A Test Plan can cover a whole project, a single release, or a single module. Say which. Naming what is *out* of scope here is just as useful as naming what is in.

In scope:
- {{Item / module / release this plan covers}}
- {{...}}

Out of scope:
- {{What this plan deliberately does not cover, and where that is covered instead}}
- {{...}}

### 1.3 Definitions and Acronyms

> Define testing terms used in this document, especially any used in a project-specific way. A few standard ones are pre-seeded below because beginners often trip on them — keep, edit, or delete.

| Term | Definition |
|---|---|
| Test level | The *stage* of testing, defined by how much of the system is assembled: **unit** (one function/class in isolation), **integration** (units wired together), **system** (the whole assembled product), **acceptance** (the product judged against user/business needs). |
| Test type | The *quality dimension* being checked, independent of level: **functional** (does it do the right thing?), **performance** (fast/scalable enough?), **security** (resistant to misuse?), **usability** (can a person actually use it?), and others (reliability, compatibility, accessibility). |
| Test item | A specific thing under test (a module, service, build, document) — tracked here as **TI-N**. |
| Test case | A single concrete check: given some preconditions and steps, what result is expected — tracked here as **TC-N**. |
| Entry criteria | Conditions that must be true *before* a test activity may start. |
| Exit criteria | Conditions that must be true *before* a test activity may be declared complete. |
| {{Term}} | {{Definition}} |

### 1.4 References

> List the documents this Test Plan depends on or traces to: the requirements being verified, the design being tested, prior plans, and external standards.

Foundational documents:
- {{SRS-PROJECT-ID-001 / path}} — requirements this plan verifies
- {{SDD-MODULE-ID-001 / path}} — design of the items under test
- {{path/to/test-case-repo}} — where detailed test cases live (if separate)

External standards:
- ISO/IEC/IEEE 29119-3 — test documentation
- IEEE 829-2008 — legacy test documentation standard (predecessor)
- {{Other standard / regulation, if any}}

---

## 2. Test Context

> This section answers "what exactly are we testing, and what are we deliberately *not* testing." Being explicit about both protects you later: when someone asks "did you test X?", a written "X is intentionally not tested because Y" is a real answer, not an oversight.

### 2.1 Test Items (TI-N)

> The concrete things under test. Each gets a TI-N id so test cases and criteria can point back to it. A test item is usually a module, build, service, or document version — name it precisely (include version/build where it matters).

| ID | Test item | Version / build | Source (SDD / repo / artifact) |
|---|---|---|---|
| TI-1 | {{Module / service / build}} | {{version}} | {{reference}} |
| TI-2 | {{...}} | {{...}} | {{...}} |

### 2.2 Features to Be Tested

> The behaviors/qualities you *will* check, ideally traced back to requirements in the SRS. Keep these at feature granularity here; the step-by-step checks go in §7.

| Feature | Test item(s) | Traces to requirement | Priority |
|---|---|---|---|
| {{Feature / behavior}} | TI-1 | {{SRS §3.x / req id}} | {{High / Med / Low}} |
| {{...}} | {{...}} | {{...}} | {{...}} |

### 2.3 Features NOT to Be Tested (and Why)

> The point of this subsection: every realistic project leaves some things untested *on purpose* — third-party code you trust, a feature frozen for this release, something covered by a different plan, or an area judged low-risk. Writing down the **reason** turns a silent gap into a deliberate, reviewable decision. Empty here is a smell; if you think you are testing everything, you probably have not thought about cost yet.

| Not tested | Why not | Risk accepted / mitigated by |
|---|---|---|
| {{Feature / area}} | {{frozen this release / vendor-tested / out of scope / low risk}} | {{who accepts the risk, or what covers it instead}} |
| {{...}} | {{...}} | {{...}} |

---

## 3. Test Approach / Strategy

> How you will go about testing — the levels, the types, the mix of automated vs manual, and the tools. This is where you make the deliberate choices; later sections (§5–§7) execute on them.

### 3.1 Test Levels Used

> Pick the levels that apply and say what each one targets here. A solo project might only do system + acceptance; that is fine — say so. Remember: levels are about *how assembled* the system is.

| Level | Used? | What it targets here | Notes |
|---|---|---|---|
| Unit | {{Yes/No}} | {{individual functions/classes}} | {{...}} |
| Integration | {{Yes/No}} | {{interfaces between units/services}} | {{...}} |
| System | {{Yes/No}} | {{the whole assembled product}} | {{...}} |
| Acceptance | {{Yes/No}} | {{product vs user/business needs}} | {{...}} |

### 3.2 Test Types Used

> Pick the quality dimensions you will exercise. Types are *orthogonal* to levels — e.g. you can do functional testing at unit level and at system level. Be honest about which non-functional types you can realistically cover.

| Type | Used? | Approach / what "good" looks like |
|---|---|---|
| Functional | {{Yes/No}} | {{does it produce the right results}} |
| Performance | {{Yes/No}} | {{throughput / latency / load targets}} |
| Security | {{Yes/No}} | {{auth, input validation, abuse cases}} |
| Usability | {{Yes/No}} | {{can the target user complete key tasks}} |
| {{Reliability / Compatibility / Accessibility / ...}} | {{Yes/No}} | {{...}} |

### 3.3 Tools, Automation, and Manual Testing

> What runs by machine vs by hand, and with what tooling. State the split deliberately — automation pays off for repeated regression checks; manual is better for exploratory and usability work.

- **Automated:** {{frameworks / runners / CI integration — what is automated and why}}
- **Manual:** {{what is checked by hand and why automation is not worth it (yet)}}
- **Tooling:** {{test runner, assertion lib, load tool, coverage tool, issue tracker}}

---

## 4. Test Deliverables

> The artifacts testing produces. A Test Plan is itself one of them; the others appear as you execute. List what you commit to producing so reviewers know what to expect and where to find it.

| Deliverable | Description | Location / format |
|---|---|---|
| Test Plan | This document | {{path}} |
| Test cases | The TC-N set (this doc §7 and/or external repo) | {{path}} |
| Test logs | What actually happened on each run (pass/fail, timestamps, environment) | {{path}} |
| Defect reports | Failures raised against the items under test | {{issue tracker}} |
| Test summary report | Roll-up at the end: what was run, results, what is still open | {{path}} |
| {{Other}} | {{...}} | {{...}} |

---

## 5. Test Environment and Data

> Where testing happens and what it runs against. A test is only meaningful if you can say what hardware, software, configuration, and data it ran under — otherwise "it passed" is not reproducible.

### 5.1 Environment

> Hardware, OS, runtime versions, services, and configuration. Be specific enough that someone else could stand up an equivalent environment. Note any difference from production and why it is acceptable.

| Aspect | Specification |
|---|---|
| Hardware | {{machine / VM / container spec}} |
| OS / platform | {{...}} |
| Runtime / dependencies | {{language version, key libs, services}} |
| Configuration | {{config flags, env vars, feature toggles}} |
| Differences from production | {{what differs and why it is acceptable}} |

### 5.2 Test Data

> What data the tests need, where it comes from, and how it is kept clean and repeatable. Cover sourcing (synthetic vs real), any privacy/sanitization needs, and how state is reset between runs so tests do not pollute each other.

- **Data needed:** {{datasets / fixtures / accounts the tests require}}
- **Source:** {{synthetic, generated, anonymized copy of real data, ...}}
- **Sensitivity / handling:** {{any PII / secrets concerns and how they are sanitized}}
- **Setup & teardown:** {{how data is seeded before and reset/cleaned after each run}}

---

## 6. Entry, Exit, Suspension, and Resumption Criteria

> The gates around test execution. These keep testing honest: you do not start until preconditions hold, you do not declare done until exit conditions hold, and you have an agreed rule for stopping early and restarting rather than burning effort against a broken build.

### 6.1 Entry Criteria

> What must be true *before* this testing may start.

- {{e.g. build deploys cleanly to the test environment}}
- {{e.g. test data is loaded; dependent services are up}}
- {{...}}

### 6.2 Exit Criteria

> What must be true *before* this testing is declared complete.

- {{e.g. all High-priority test cases executed}}
- {{e.g. no open Critical/High defects; coverage target met}}
- {{...}}

### 6.3 Suspension Criteria

> Conditions under which you stop testing early because continuing is not worth it.

- {{e.g. a blocking defect makes most cases unrunnable}}
- {{...}}

### 6.4 Resumption Criteria

> What must be fixed/verified before suspended testing restarts.

- {{e.g. blocking defect fixed and smoke test passes}}
- {{...}}

---

## 7. Test Cases and Procedures (TC-N)

> The concrete checks. Each test case is one specific scenario with an expected result and a trace back to the requirement (and/or test item) it covers. For small projects, keep the cases right here in the table below. For larger ones, keep a one-line summary here and point to a separate test-case repository (spreadsheet, test-management tool, or `tests/` directory) so this plan does not become unmaintainable.

> **Either** fill the example table **or** replace it with a pointer:
> *Detailed test cases are maintained in {{path / tool}}; this plan governs them. The table below is illustrative.*

| ID | Objective | Preconditions | Steps | Expected result | Traces to |
|---|---|---|---|---|---|
| TC-1 | {{What this case verifies}} | {{state required before running}} | {{1. ... 2. ... 3. ...}} | {{observable result that means PASS}} | {{req / TI-N}} |
| TC-2 | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

> **Procedure notes:** {{any shared setup/teardown, ordering constraints, or how to record pass/fail in the test log.}}

---

## 8. Risks and Contingencies

> What could derail the testing effort (not product defects — *project* risks like thin environment access, immature features, time pressure, single-person bottleneck) and what you will do if they materialize.

| Risk | Likelihood | Impact | Contingency |
|---|---|---|---|
| {{e.g. test environment unavailable}} | {{Low/Med/High}} | {{Low/Med/High}} | {{fallback plan}} |
| {{...}} | {{...}} | {{...}} | {{...}} |

---

## 9. Roles and Responsibilities

> Who does what. For a solo project this may be one row ("everything: me") — still worth writing so an outside reader knows there is no separate reviewer. For a small team, name the tester, the reviewer/approver, and who signs off acceptance.

| Role | Person / handle | Responsibility |
|---|---|---|
| {{Test author}} | {{name}} | {{writes & maintains this plan and the cases}} |
| {{Tester / executor}} | {{name}} | {{runs the cases, records results}} |
| {{Reviewer / approver}} | {{name}} | {{reviews plan, signs off exit criteria}} |
| {{...}} | {{...}} | {{...}} |

---

## 10. Schedule

> When testing happens relative to the work. Keep it as light as a few milestones — beginning, the runs, the gate dates. Tie to entry/exit criteria where it helps.

| Milestone | Target date | Depends on |
|---|---|---|
| {{Test environment ready}} | {{YYYY-MM-DD}} | {{...}} |
| {{Test execution start}} | {{YYYY-MM-DD}} | entry criteria (§6.1) met |
| {{Test execution complete}} | {{YYYY-MM-DD}} | exit criteria (§6.2) met |
| {{...}} | {{...}} | {{...}} |

---

## 11. Open Questions

> Test-planning questions still being resolved. Resolve and remove as work progresses.

- **OQ-1**: {{question}} — {{what's blocking, who needs to decide}}
- ...

---

## 12. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Test Context (especially §2.2 features tested and §2.3 features NOT tested)
- §3 Test Approach / Strategy
- §6 Entry, Exit, Suspension, and Resumption Criteria
- §7 Test Cases and Procedures (or a clear pointer to where they live)
- §12 Revision History

**Optional sections** (include if relevant):
- §4 Test Deliverables (omit if obvious for a tiny effort)
- §5 Test Environment and Data (omit only if the environment is trivial and stated inline)
- §8 Risks and Contingencies (omit for very small, low-risk efforts)
- §9 Roles and Responsibilities (collapse to one line for solo work)
- §10 Schedule (omit if untimed / continuous)
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- TI-N: test items / levels-and-items under test
- TC-N: test cases
- OQ-N: open questions

These prefixes enable cross-document traceability — requirements in the SRS can be traced to test cases here via the "Traces to" column.

**Tailoring**:
- Levels and types in §3 are menus, not mandates. A solo project doing only system + acceptance, functional + a little performance, is a legitimate plan — say so explicitly rather than leaving the table half-filled.
- Keep this plan about *how you will test*. The actual results belong in test logs and the test summary report (named in §4), not here.
- For a one-page plan covering a small change, keep §1, §2.2/§2.3, §6, §7, §12 and drop the rest.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29119-3, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
