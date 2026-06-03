# Software Maintenance Plan Template

> **Template purpose:** Lightweight Software Maintenance Plan (SMP) structure following ISO/IEC/IEEE 14764:2022. Use this template to plan how a delivered system will be maintained — how change requests arrive, get classified, analyzed, implemented, tested, released, and how the system is eventually retired. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** As a system approaches first delivery, or once it is in service. The Maintenance Plan picks up where the development documents leave off: the SRS said WHAT the system does, the SDD said HOW it was built, the test docs said how it was verified — this plan says how the system stays healthy and changeable *after* it ships, and how it is shut down cleanly at end of life.
>
> **Companion standard:** ISO/IEC/IEEE 14764:2022 — Software engineering — Software life cycle processes — Maintenance. (Companion: ISO/IEC/IEEE 12207:2017 for the broader life-cycle process context; SWEBOK V4 Knowledge Area 5, Software Maintenance, for the activity vocabulary used in the domain sections.)
>
> **Status of this template:** A lightweight skeleton derived from public sources, structured to follow ISO/IEC/IEEE 14764:2022 (with SWEBOK V4 KA 5 for the maintenance activity vocabulary). **ISO/IEC/IEEE 14764:2022 is a paywalled standard; this template paraphrases its activity structure and four-category taxonomy from public/SWEBOK descriptions and does NOT reproduce normative text — verify section content against the full standard for enterprise, regulated, safety-critical, or contractual contexts.** Suitable as-is for solo/small-team and internal use. PUBLIC: this template contains only generic software-engineering structure and no Mira-recreatable IP, so it passes the public/private IP test for publication.

---

# Software Maintenance Plan — {{System Name}}

| Field | Value |
|---|---|
| Document ID | MNT-{{SYSTEM-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 14764:2022 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| System / Product Under Maintenance | {{System Name}} and version range this plan covers |
| Maintenance Phase | {{Pre-delivery (transition planning) / In-service (active maintenance) / Retirement}} |
| Maintainer | {{Team or individual responsible for maintaining the system}} |
| Maintenance Window | {{Standard window(s) for routine maintenance releases, or N/A}} |
| Supersedes | {{Prior plan Document ID, or — for first issue}} |

---

## 1. Introduction

> The Introduction tells a first-time reader what this document is, what it covers, and what words it uses — before any of the detail. We fold four standard subsections in here (Purpose, Scope, Definitions, References), the same shape as the SRS and SDD documents in this pack.
>
> A note on the word **maintenance**, because it is easy to misread: in formal software engineering, *software maintenance* means everything done to the software **after** it is first released and in use — fixing defects, adapting it to a changed environment, improving it, and keeping it healthy. It is **not** the original development work, and it is **not** the day-to-day running of the software (that is *operations*). ISO/IEC/IEEE 14764 is the international standard that defines how to plan and run this post-release work; this plan follows it in a lightweight form.

### 1.1 Purpose

> One paragraph: state that this document plans the maintenance of {{System Name}} after delivery, name the standard it follows, and say where it connects to the rest of the document set.

This document plans how **{{System Name}}** will be maintained after delivery: how maintenance requests are received, classified, analyzed, implemented, tested, and released, and how the system is eventually retired. It follows ISO/IEC/IEEE 14764:2022 in lightweight form. It picks up where the development documents leave off — the SRS ({{SRS-{{SYSTEM-ID}}-001}}) defined *what* the system does, the SDD ({{SDD-...}}) defined *how* it was built, and the test documents defined how it was verified. The hand-off from development to maintenance happens here: once {{System Name}} is in service, the activities in this plan govern every change made to it.

### 1.2 Scope

> Define what this plan covers and — just as important — what it explicitly does NOT cover. The "is not" list prevents the plan from being blamed for gaps that belong to other documents (operations runbooks, the original SRS, unrelated systems).

**This plan covers:**
- {{System Name}}, versions {{lowest version}} through {{highest version / "all in-service versions"}}.
- All four maintenance categories — corrective, adaptive, perfective, and preventive (see §3).
- The in-service period: from {{first delivery / go-live date}} until retirement (see §11).

**This plan does NOT cover:**
- Original development of {{System Name}} — that is documented in the SRS/SDD/test pack, not here.
- Day-to-day operations (keeping the system running, monitoring, on-call rotations) where those live in a separate operations runbook — {{ref: 10_User_Documentation_and_Operations, or "covered in §9 of this plan"}}. Operations *feeds* maintenance (see §9) but is a distinct activity.
- Systems other than {{System Name}}: {{name any adjacent systems explicitly out of scope}}.

> Beginner note: "maintenance" in this document means *everything done to the software after its first release*. If a task is about changing the software, it belongs here; if it is about running the software as-is, it belongs in operations.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define every term that, if misread, would derail the rest of the document. The four maintenance categories and the request/test/release vocabulary are seeded below because a first-time reader genuinely cannot follow §3–§11 without them.

| Term | Definition |
|---|---|
| Software maintenance | All work done on the software *after* first release: fixing defects, adapting to a changed environment, improving it, and keeping it healthy. Not the original development. |
| Corrective maintenance | Fixing reported defects (bugs) in the delivered software. |
| Adaptive maintenance | Changing the software to keep it working in a changed environment — new OS, new API, new dependency version, new law or regulation. |
| Perfective maintenance | Improving the software while it still works — performance, new features, readability, reduced technical debt. |
| Preventive maintenance | Fixing latent problems *before* they cause a failure — addressing fragile code, expiring certificates, or known-risky patterns proactively. |
| Correction / Enhancement | The standard's two top-level groupings: *Correction* = Corrective + Preventive; *Enhancement* = Adaptive + Perfective. |
| Maintenance Request (MR) / Modification Request | A single tracked item — a bug report, change request, or improvement idea. The unit of work the whole process acts on. Each MR is classified into one of the four categories. |
| Impact analysis | Studying, *before* changing anything, what else a proposed change will touch (requirements, design, code, tests, docs, data, operations) and what it will cost in time and risk. |
| Regression testing | Re-running tests after a change to confirm you did not break things that previously worked. A *regression* is when something that used to work stops working because of a new change. |
| Rollback | A planned way to undo a release and return to the last known-good version if a change goes wrong in production. |
| Maintainability | How easy the software is to change correctly. It can be measured (e.g. mean time to repair, defect re-open rate, time to onboard a new maintainer). |
| Retirement / decommissioning | The planned end-of-life of the software: deciding when to stop maintaining it, migrating users and data to a replacement, archiving what must be kept, and shutting it down cleanly. |
| Migration | Moving software, its data, and its users from one environment (or system) to another while keeping things working. Appears mid-life (adaptive) and at end-of-life (retirement). |
| Operations | Running the software day to day. Distinct from maintenance (changing the software); operations feedback is the main source of maintenance requests. |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> List the documents this plan depends on, grouped for readability. Mirror the SRS reference grouping: foundational project docs, the sibling engineering documents this plan connects to, ADRs, and external standards.

Foundational documents:
- {{path/to/project-overview.md}} — {{brief description}}

Sibling engineering documents this plan depends on:
- `01_Requirements/Software_Requirements_Specification.md` — SRS-{{SYSTEM-ID}}-001 — the requirements maintenance changes must continue to satisfy.
- `02_Design/Software_Design_Description.md` — SDD-{{...}} — the design that impact analysis (§6) reasons over.
- `04_Testing_and_VV/Master_Test_Plan.md` — the test plan the regression strategy (§7) extends.
- `05_Configuration_Management/Software_Configuration_Management_Plan.md` — the versioning/baseline scheme releases (§8) follow.
- `05_Configuration_Management/Change_Request.md` — the change-request record an MR may map onto.

Architecture Decision Records:
- ADR-NNNN — {{decision relevant to maintenance, e.g. release cadence, supported-version policy}}

External standards:
- ISO/IEC/IEEE 14764:2022 — Software engineering — Software life cycle processes — Maintenance (this plan's companion standard).
- ISO/IEC/IEEE 12207:2017 — Systems and software engineering — Software life cycle processes (broader process context).
- SWEBOK V4, Knowledge Area 5 — Software Maintenance (activity vocabulary).

---

## 2. Maintenance Process and Activities

> Before we dive into individual topics, this section gives the whole document its spine. A **process** here just means *the agreed, repeatable steps the maintainer follows so that every change is safe and traceable* — written down so the work does not depend on one person remembering how it goes.
>
> The standard organizes maintenance into a handful of named activities. We assign each one an ID (**MA-1, MA-2, …**) so later sections can point back to "which activity am I detailing." Crucially, the activities form a **loop**, not a line: operational feedback raises a request → the request is analyzed → the change is made → it is tested → it is released → and operations feeds back again. The detail of each activity lives in §5–§11; this table is the map.

The maintenance of {{System Name}} is organized into the following activities, paraphrasing the ISO/IEC/IEEE 14764 process structure:

| ID | Activity | What it covers | Where detailed |
|---|---|---|---|
| MA-1 | Intake & classification / problem & modification analysis | Receiving each request, classifying it into a category, and analyzing it before work starts. | §3, §5, §6 |
| MA-2 | Impact analysis | Determining the blast radius of a change before approving it. | §6 |
| MA-3 | Modification implementation | Making the actual change to code, design, data, and docs. | §5, §8 |
| MA-4 | Maintenance review & acceptance | Confirming the change is correct, regression-free, and accepted before closure. | §5, §7, §8 |
| MA-5 | Migration | Moving the system, its data, and its users to a new environment or replacement. | §3 (mid-life), §11 (end-of-life) |
| MA-6 | Retirement | Planned end-of-life: stop maintaining, transition users/data, archive, shut down. | §11 |

> The loop in one sentence: **feedback (§9) → request & classify (MA-1, §5) → analyze impact (MA-2, §6) → implement (MA-3) → test (§7) → release (MA-3/MA-4, §8) → review & accept (MA-4) → back to feedback.** Process implementation and transition planning (setting up this process before go-live) are covered by establishing this plan itself.

---

## 3. Maintenance Categories

> Not all changes are equal, and the single most important early step in maintenance is *classifying* each request — because the category decides who must approve it, how urgent it is, and how much testing it needs. A security defect (corrective) and a nice-to-have feature (perfective) travel very different paths.
>
> The standard uses four categories, grouped into two families:
> - **Correction** — fixing what is wrong: *Corrective* (fix reported defects) + *Preventive* (fix latent problems before they bite).
> - **Enhancement** — making it better or keeping it viable: *Adaptive* (keep working in a changed environment) + *Perfective* (improve while it still works).

| Category | Definition | Example for {{System Name}} | Typical trigger | Default priority |
|---|---|---|---|---|
| Corrective | Fix a reported defect in delivered behavior. | {{e.g. "incorrect total on the export report"}} | Bug report, failed transaction, incident (§9). | {{High — or Critical if security/data-loss}} |
| Adaptive | Change the software to keep it working in a changed environment. | {{e.g. "upgrade to the new {{dependency}} API before the old one is removed"}} | External deadline: dependency/OS/API end-of-life, new regulation. | {{Medium — driven by external deadline}} |
| Perfective | Improve the software while it still works correctly. | {{e.g. "speed up the dashboard load" / "add CSV export"}} | User request, performance data, technical-debt review. | {{Low–Medium; scheduled, not urgent}} |
| Preventive | Fix latent problems before they cause a failure. | {{e.g. "replace the certificate that expires in 60 days" / "harden the fragile parser"}} | Trend analysis (§9), audit, maintainer judgment. | {{Medium; planned ahead of the failure window}} |

**Grouping and why it matters:**
- *Correction* (Corrective + Preventive) is about restoring or protecting correct behavior. It tends to follow the MA-1 → MA-2 → MA-3 → MA-4 path quickly, sometimes via the emergency path (§5).
- *Enhancement* (Adaptive + Perfective) is about new capability or new viability. It is usually scheduled into a routine release (§8) and gets the same impact analysis (§6) but less time pressure — except adaptive changes with a hard external deadline.
- **Classification drives three things:** the *approval authority* (§4), the *urgency/SLA*, and the *testing depth* (§7). Misclassifying a corrective security fix as a perfective nice-to-have is how urgent work sits in a backlog. Record the category on every MR (§5).

---

## 4. Maintenance Organization and Responsibilities

> This section names the **hats** — the responsibilities that must be covered for maintenance to work — and who wears each one. The point is not headcount; it is that each responsibility is *named and owned*, so nothing falls into the "I thought you were handling that" gap.
>
> Two terms worth defining plainly: a **configuration manager** is the function that controls versions and baselines (what is the official current version, what changed between releases) — it is a *role*, not necessarily a separate person. A **support analyst** is the function that takes in user/operational feedback and turns the real ones into Maintenance Requests. On a solo or small team, one person wears several of these hats — that is fine and expected. Writing the hats down still matters: it tells future-you (and any new contributor) which decisions sit with which function.

| ID | Role | Responsibility | Authority (what this role decides/approves) | Hands off to |
|---|---|---|---|---|
| ROLE-1 | Maintenance Manager | Owns this plan; prioritizes the MR backlog; decides what goes in each release. | Approves enhancements and the release contents; sets priority. | Developer (ROLE-2) for implementation. |
| ROLE-2 | Developer / Maintainer | Performs impact analysis (§6) and implements approved changes (MA-3). | Decides *how* to implement within the approved scope. | Tester (ROLE-3) for verification. |
| ROLE-3 | Tester | Runs regression and acceptance tests (§7); confirms the fix and no new regressions. | Signs off that a change is verified (or fails it back). | Configuration Manager (ROLE-4) for release. |
| ROLE-4 | Configuration Manager | Controls versions/baselines; packages and tags releases (§8); owns rollback readiness. | Approves the release for deployment; controls version numbers. | Support Analyst (ROLE-5) / users for communication. |
| ROLE-5 | Support Analyst | Receives operational feedback (§9); triages and files Maintenance Requests (MR-N). | Decides whether incoming feedback becomes an MR. | Maintenance Manager (ROLE-1) for prioritization. |

**Escalation path (emergency / security changes):** {{Name who can authorize an out-of-band emergency change — e.g. "Maintenance Manager, or in their absence the Developer, may authorize a hotfix for a Critical-severity corrective MR; the change still gets retroactive impact analysis and documentation per §5."}}

> Solo / small-team note: one person commonly holds ROLE-1 through ROLE-5 at once. Keep the table anyway — the value is the *list of decisions* you are making (prioritize, implement, verify, release, triage), not the number of people. When you grow, you assign hats; you do not invent the responsibilities for the first time mid-incident.

---

## 5. Problem and Modification Process

> This is the procedural heart of the plan: the life of a single change, start to finish. Each Maintenance Request (MR) moves through the same numbered stages so that every change is safe, reviewed, and traceable. The unit that travels through it is the **MR record** (MR-N) — a tracked item that carries everything we know about the change.
>
> Why this matters for a beginner: without a defined flow, a "quick fix" goes straight from idea to production with no analysis, no test, and no record. The stages below are the guardrails that turn an idea into a safe, documented change.

**The standard flow (normal path):**

1. **Intake** (MA-1, ROLE-5) — the request arrives (bug report, change request, idea) and an MR record is created.
2. **Classification** (MA-1) — the MR is classified into a category (§3): corrective / adaptive / perfective / preventive.
3. **Analysis** (MA-1 → MA-2) — the MR is studied; impact analysis (§6) determines the blast radius and cost.
4. **Approval** (MA-1) — the authority for that category (§4) accepts, defers, or rejects the MR.
5. **Implementation** (MA-3, ROLE-2) — the change is made to code, design, data, and docs.
6. **Testing** (ROLE-3) — regression and new tests run (§7); the fix is confirmed and locked with a test.
7. **Release** (MA-3/MA-4, ROLE-4) — the change is packaged and deployed (§8), with rollback ready.
8. **Verification / acceptance** (MA-4) — the change is confirmed correct in the target environment.
9. **Closure** (MA-4) — the MR is closed with links to the commit(s), test(s), and release.

**MR record fields (MR-N):**

| Field | Example |
|---|---|
| MR ID | MR-{{NNN}} |
| Reporter / source | {{name / "incident INC-42" / "user ticket"}} |
| Date raised | {{YYYY-MM-DD}} |
| Category (§3) | {{Corrective / Adaptive / Perfective / Preventive}} |
| Severity / priority | {{Critical / High / Medium / Low}} |
| Affected components | {{module(s), interface(s) — from impact analysis §6}} |
| Impact analysis | {{link to or summary of §6 analysis}} |
| Decision & authority | {{Accepted by ROLE-1 on YYYY-MM-DD / Deferred / Rejected}} |
| Implementation links | {{commit hash(es), branch, PR}} |
| Test links | {{regression suite run, new test id}} |
| Release | {{version this shipped in}} |
| State | {{see state list below}} |

**MR states (the lifecycle an MR moves through):**

`New` → `Classified` → `Analyzed` → `Approved` (or `Deferred` / `Rejected`) → `In progress` → `In test` → `Released` → `Verified` → `Closed`.

**Worked example (end to end, for a first-timer):**
> A user reports the export total is wrong (Intake → MR-017 created). It is a defect, so it is classified *Corrective* with severity High. Impact analysis (§6) finds it touches the report module and one shared rounding helper used in two other places. The Maintenance Manager approves it. The developer fixes the helper *and* adds a regression test that would have caught the bug. The tester re-runs the affected tests (targeted regression, §7) — all pass. It ships in the next routine release v{{1.4.2}} with rollback ready (§8). The user confirms the total is correct (Verified). MR-017 is closed with links to the commit and the new test.

**Emergency / expedited path:** For a Critical corrective or security MR, the change may be implemented and deployed ahead of the normal queue under the escalation authority in §4. The deviation is *only* in sequencing and speed — the change still gets **retroactive impact analysis (§6), a regression test (§7), and full MR documentation** once the fire is out. An undocumented emergency fix is a future incident waiting to happen.

---

## 6. Impact Analysis

> Impact analysis is the **gate between "accepted request" and "work starts."** Before changing anything, you ask: *what else does this change touch, and how would I know?* The classic failure it prevents is the "one-line fix" that silently breaks three other things because nobody looked at what depended on the line being changed. Impact analysis is how you see the **blast radius before you swing.**
>
> For a beginner: a small code change can ripple outward — a fix in a shared function affects every caller; a database change affects every reader of that data; a behavior change affects the tests, the docs, and the users who relied on the old behavior. Listing those dimensions on purpose, every time, is what turns "I think it's fine" into "I checked."

For every non-trivial MR, assess each dimension below and record the result on the MR (§5). The output of this analysis drives both the **approval decision** (§5) and the **regression scope** (§7) — impact analysis is literally what tells you *which* tests to re-run.

| Dimension | Question to ask | How would we know? |
|---|---|---|
| Requirements | Does this change any behavior the SRS promised? | Trace to SRS requirement IDs. |
| Architecture / design | Does it cross a design boundary or change a documented decision? | Check SDD; check ADRs. |
| Code modules | Which modules and shared helpers does it touch? | Search callers/usages of the changed code. |
| Interfaces | Does it change any API, CLI, file format, or contract others depend on? | List consumers of the interface. |
| Data / schema | Does it require a data or schema migration? Is it reversible? | Check schema, write a migration + rollback. |
| Tests | Which existing tests cover the affected area? | Map affected modules → covering tests. |
| Documentation | Which docs, runbooks, or help text describe the old behavior? | Grep docs for the affected feature. |
| Operations / runbooks | Does it change how the system is deployed, monitored, or recovered? | Check the operations runbook (§9). |
| Security / privacy | Does it touch auth, secrets, personal data, or attack surface? | {{ref 12_Security_and_Privacy}} |
| Cost / schedule | How long, and what does it displace in the backlog? | Estimate effort; check release window (§8). |
| Risk | What is the worst case if this change is wrong? | Rate risk; size rollback (§8) accordingly. |

**Recording:** Capture the impact analysis as part of the MR record (MR-N), not in a side conversation. A change whose impact analysis is in someone's head is a change nobody can review or learn from later. For trivial changes (typo, doc fix), a one-line "no impact beyond X" note is sufficient — but write the line.

---

## 7. Regression Testing

> A **regression** is when something that used to work stops working because of a new change. **Regression testing** is re-running tests after a change to catch exactly that. The guiding rule of safe maintenance: *every bug fix should ship with a test that would have caught the bug* — so the same defect cannot silently return six months later.
>
> For a beginner: fixing a bug without adding a test means you fixed it *this once*. The next refactor can quietly reintroduce it, and you will not find out until a user does. The test you add is the lock that keeps the fix in place.

**Test selection (driven by §6).** Impact analysis decides which tests run:
- **Targeted regression** — re-run the tests covering the modules the change touched, plus their direct consumers. The default for a well-scoped change.
- **Full regression** — re-run the whole suite. Use when the change touches a shared/core component, a schema, or a cross-cutting interface, or when impact analysis is uncertain.

**Relationship to the project Test Plan.** The maintenance regression suite is the project's existing test suite, maintained and extended over time — see `04_Testing_and_VV/Master_Test_Plan.md`. Maintenance does not invent a parallel testing approach; it *grows* the existing one. Every fix that adds a test (below) makes the suite stronger for the next change.

**Automation vs. manual.** {{State which parts are automated (CI on every change) vs. manual (exploratory, UI smoke). Prefer automation for anything that will be re-run; automation is what makes targeted regression cheap.}}

**Acceptance criteria for a maintenance change ("done" means all three):**
1. The original defect or requested change is verified fixed/delivered.
2. No regressions — the selected regression tests pass.
3. A new test exists that locks the change (for a fix: a test that would have caught the bug; for an enhancement: a test covering the new behavior).

**Emergency fixes (special case).** Under the expedited path (§5), regression may be *abbreviated* under time pressure — run the smallest safe set to ship the fix. The abbreviated coverage is then **completed afterward**: the full targeted (or full) regression and the locking test are added before the MR is closed. "We'll test it later" is only acceptable if "later" is a recorded, closed loop, not a hope.

---

## 8. Release and Deployment

> A maintenance **release** is how changes actually reach users. This section plans *how* changes are packaged, versioned, deployed, and — critically — *undone*. The key beginner insight: you decide **how to roll back before you ship**, not during a 2 a.m. incident when the new version is on fire.
>
> Why batch changes into scheduled releases? Grouping several small, tested changes into one planned release reduces risk and churn: fewer deployments, fewer moments where something can go wrong, clearer communication. A **hotfix** (an out-of-band emergency release for one urgent change) is the exception, not the rhythm.

**Release types:**

| Type | When | Contents | Cadence |
|---|---|---|---|
| Routine / scheduled | Planned interval or when a batch is ready. | A reviewed batch of corrective/adaptive/perfective/preventive MRs. | {{e.g. every 2 weeks / monthly}} |
| Hotfix / emergency | A Critical corrective or security MR cannot wait. | One (or a minimal set of) urgent change(s). | As needed, via the §5 expedited path. |

**Versioning.** {{State the scheme — e.g. semantic versioning `MAJOR.MINOR.PATCH`: PATCH for corrective, MINOR for backward-compatible enhancements, MAJOR for breaking changes.}} Versioning and baselines follow the Configuration Management Plan — see `05_Configuration_Management/Software_Configuration_Management_Plan.md`.

**Packaging & deployment procedure.** {{Describe how a release is built, tagged, and deployed — the concrete steps. Keep it runnable: a maintainer should be able to follow it without guessing.}}

**Rollback plan (mandatory).**
- **Known-good state:** {{what is the last-good version/baseline, and where is it kept — tag, artifact, snapshot?}}
- **How to get back to it:** {{the concrete rollback steps — redeploy previous artifact, reverse the data migration (note if irreversible), restore snapshot.}}
- **Decision trigger:** {{who decides to roll back, and on what signal — e.g. "error rate > X within 30 min of deploy."}}
- A release with an irreversible data migration needs *extra* care: {{forward-fix plan, since rollback alone won't restore data.}}

**Stakeholder communication.**
- **Release notes:** {{what changed, in plain language; who reads them.}}
- **Who is told what:** {{users, operators, downstream teams — and through what channel.}}
- **Maintenance-window / downtime notice:** {{lead time and channel for any planned downtime; tie to the Maintenance Window in the metadata table.}}

> Communication is part of the release, not an afterthought. The people affected by a change should hear about it *from the maintainer, in clear language* — what changed, what to expect, and what to do if something looks wrong — rather than discovering it by surprise. Binds to MA-3 / MA-4.

---

## 9. Operational Feedback

> This section describes the loop that **feeds** the whole process. *Operations* runs the software day to day; when it notices something — an incident, a slowdown, a complaint — that signal becomes (or is consciously decided *not* to become) a Maintenance Request flowing into §5. Operations tells maintenance what is wrong; maintenance changes the software; the next round of operations confirms it is better.
>
> For a beginner: this is where **preventive maintenance** gets its early warning. A single incident is noise; the *same* incident three times is a trend that says "fix the underlying thing before it happens a fourth time."

**Feedback sources and how each becomes an MR:**

| Source | What it looks like | Becomes an MR when… |
|---|---|---|
| Incident reports | Something broke in production. | The cause is in the software → corrective MR; if recurring → preventive MR. |
| Defect trends | The same kind of bug keeps appearing. | The pattern points at a fixable root cause → preventive/perfective MR. |
| Performance / monitoring data | Latency, error rate, resource use over thresholds. | A degradation traces to the software → perfective or preventive MR. |
| User feedback / support tickets | "It's confusing" / "can it also do X." | A real, repeated need is identified → perfective (or corrective) MR. |
| Dependency / environment notices | "API v1 retires in 90 days." | An external deadline requires a change → adaptive MR. |

**Triage cadence.** {{State how often incoming feedback is reviewed — e.g. "support analyst (ROLE-5) triages new feedback {{weekly}}; recurring/high-severity items become MRs immediately."}} Not every signal becomes an MR; the triage decision (and its reasoning) is itself worth a one-line record so the same "won't fix" is not re-litigated monthly.

**Trend analysis.** {{Describe how recurring incidents and defect clusters are reviewed periodically to spot candidates for preventive or perfective work — e.g. "monthly review of the incident log and reopened-defect list."}} This trend data is also one of the inputs to the maintainability measures in §10. The loop closes back on §2: feedback → request → analyze → change → release → feedback.

---

## 10. Maintainability Measures

> **Maintainability** means *how easy the software is to change correctly.* The important and slightly surprising claim: you can actually **measure** it. The point of measuring is not the number itself — it is to **notice the system getting harder to maintain *before* it becomes unmaintainable.** A codebase rarely dies suddenly; it gets a little harder to change each month until one day nobody wants to touch it. These measures are the early-warning instruments.
>
> For a beginner: track the **trend**, not the absolute number. Hitting a perfect MTTR in month one matters far less than noticing it doubling over six months.

| ID | Measure | Definition | How collected | Target / threshold | Action if breached |
|---|---|---|---|---|---|
| MM-1 | Mean time to repair (MTTR) | Average time from a corrective MR being raised to its fix released. | MR timestamps (§5). | {{e.g. < 5 working days for High}} | {{Investigate the slow step — analysis? testing? release?}} |
| MM-2 | Defect re-open rate | % of closed corrective MRs reopened within {{30}} days. | MR state transitions. | {{< 10%}} | {{Strengthen acceptance criteria / regression (§7).}} |
| MM-3 | Regression escape rate | # of regressions found in production per release. | Incident log (§9) tagged "regression." | {{0–1 per release}} | {{Widen regression selection (§6→§7).}} |
| MM-4 | Time to onboard a maintainer | Time for a new maintainer to make their first safe merged change. | Observation / onboarding log. | {{< 2 weeks}} | {{Improve docs / reduce coupling.}} |
| MM-5 | Change failure rate | % of releases needing a rollback or hotfix. | Release log (§8). | {{< 15%}} | {{Deepen impact analysis (§6) / testing (§7).}} |
| MM-6 | Backlog age | Age of the oldest open MR, and median backlog age. | MR backlog. | {{No High-severity MR older than 30 days}} | {{Re-prioritize (ROLE-1); consider capacity.}} |

> Targets are **tailorable** — start with rough numbers and adjust as you learn what "normal" is for this system. Early on, the goal is simply to *have* the measure and watch which way it moves. Feedback data from §9 is one of the main inputs here.

---

## 11. Retirement

> **Retirement** (also called *decommissioning*) is the planned end-of-life of the system — and the standard treats it as a real maintenance activity, not "we'll just turn it off someday." The risky parts are almost never the shutdown itself; they are the **data migration** (moving data to a replacement without losing or corrupting it) and **making sure nobody is left stranded** (a user, an integration, or a legal retention obligation you forgot about).
>
> A distinction to keep straight: **mid-life migration** is an *adaptive* change (§3) — moving a still-living system to a new platform. **End-of-life migration** is part of retirement (here) — moving users and data *off* this system onto a replacement as the system is shut down. Same word, different moment. Both bind to MA-5 (migration); retirement as a whole is MA-6.

**Retirement criteria — when does it make sense to stop maintaining?**
- A replacement system is available and ready to take the load.
- The cost of maintaining {{System Name}} exceeds the value it provides.
- A critical dependency has reached end-of-life and cannot be adapted around (an adaptive path is exhausted).
- {{Other project-specific trigger}}

**Retirement plan (the steps):**

| Step | What it covers |
|---|---|
| 1. Notification | Tell all stakeholders — users, operators, downstream/integrating systems — with adequate lead time. State the sunset date. |
| 2. Transition / migration (MA-5) | Move users and their data to the replacement. Verify the data arrived correctly *before* anything is deleted. |
| 3. Parallel running (if any) | {{Run old and new side by side for {{period}} so users can fall back if the replacement has gaps; or "N/A — clean cutover."}} |
| 4. Data archival & retention | Identify what must be kept ({{records, audit logs, personal data}}), for how long ({{retention period / legal obligation}}), and where ({{archive location and format}}). |
| 5. Final decommissioning | Shut down services, revoke credentials/access, release infrastructure, and record the final state. |

> Archival/retention is an explicit step on purpose: turning off a system can destroy records someone is legally or operationally required to keep. Decide *what must survive the system* before you shut anything down.

---

## 12. Open Questions

> This is where maintenance-plan decisions that are not settled yet live — so they are *tracked instead of forgotten*. It is a lightweight tracking aid, not a contract. As questions get answered, the answers move down into 12.2 for traceability.
>
> For a beginner: every plan has unsettled corners ("what's our hotfix SLA?", "do we keep a staging environment?"). Writing them here, with a working default where you have one, means the plan can ship and improve rather than stall waiting for perfect answers.

### 12.1 Deferred with defaults

> Each has a working default; revisit if the default proves inadequate.

- **OQ-DEF-1** {{What is the hotfix SLA for a Critical corrective MR?}} — *default: {{respond within 4 hours, fix released within 24}}.*
- **OQ-DEF-2** {{Do we maintain a staging environment, or test against production-like locally?}} — *default: {{local production-like, given solo/small-team scale}}.*
- **OQ-DEF-3** {{How many prior versions do we support / keep rollback artifacts for?}} — *default: {{the current and one previous release}}.*

### 12.2 Resolved (recorded for traceability)

- **OQ-1** {{Question}}: {{Resolution and date}}.

---

## 13. Revision History

> Every substantive change to *this plan* gets a version bump and a row, so the plan's own history is traceable. A maintenance plan that is not itself maintained is a smell — the document that governs change should model the discipline it asks for.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Maintenance Process and Activities (the MA-N backbone the rest of the plan references)
- §3 Maintenance Categories
- §5 Problem and Modification Process
- §6 Impact Analysis
- §13 Revision History

**Optional sections** (include if relevant):
- §4 Maintenance Organization and Responsibilities (collapse heavily for solo — see Tailoring)
- §7 Regression Testing (cross-reference the Test Plan rather than duplicating it; keep the acceptance-criteria triad)
- §8 Release and Deployment (the rollback plan is the non-optional part even when the rest is light)
- §9 Operational Feedback (omit only if operations is fully documented elsewhere and explicitly cross-referenced)
- §10 Maintainability Measures (start with one or two measures; add as the project matures)
- §11 Retirement (may be a stub early in life — but write the criteria and the archival step even then)
- §12 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (for cross-document traceability):
- MNT-{{SYSTEM-ID}}-NNN: this document's ID.
- MA-N: maintenance process activities (§2) — the load-bearing IDs the rest of the plan references.
- ROLE-N: maintenance roles (§4).
- MR-N: maintenance / modification request records (§5).
- MM-N: maintainability measures (§10).
- OQ-N / OQ-DEF-N: open questions (resolved / deferred-with-defaults) (§12).

These prefixes let maintenance work trace cleanly to the sibling documents: MRs reference SRS requirement IDs and SDD design IDs through impact analysis (§6), and releases reference the Configuration Management Plan's baselines (§8).

**Tailoring**:
- Section structure from 14764 is guidance, not a mandate. Add/remove subsections as the system needs; deviate explicitly (a one-line "skipping §10 — too early for metrics" is better than silent omission).
- **Solo developer / small team collapse:** §4 collapses to a single line ("all roles held by {{name}}") — but keep the list of *hats* so the decisions are still named. §8 can be "tag the release, deploy with {{command}}, roll back by redeploying the previous tag." §10 can start with a single measure (MTTR). The discipline that does *not* collapse: classify every change (§3), do at least a one-line impact analysis (§6), and ship every fix with a locking test (§7). Those three survive at any scale because skipping them is what makes a system unmaintainable.
- Keep the plan focused on *changing* the software. Running it day to day belongs in operations; building it the first time belonged in development.
- Revision history is mandatory. Track every substantive change with a version bump.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 14764:2022 standard, not this lightweight version. This template paraphrases the standard's activity structure and category taxonomy from public/SWEBOK sources and is suitable for solo/small-team projects, internal documentation, and early-stage products — verify section content against the purchased standard for enterprise, regulated, or safety-critical contexts.
