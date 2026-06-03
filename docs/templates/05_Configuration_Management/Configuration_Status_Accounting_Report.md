# Configuration Status Accounting Report Template

> **Template purpose:** Lightweight Configuration Status Accounting Report structure following IEEE 828-2012 (the status-accounting activity), reduced for solo/small-team and internal/public build-in-public use. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Issue this report on a schedule (e.g., per sprint, per release, monthly) or on demand when someone needs to know, as a matter of record, what versions of which parts make up the system right now, what changes are in flight, and how confident you are that the records match reality. It is the periodic OUTPUT of the status-accounting activity defined in your Configuration Management Plan (SCMP); it reports state, it does not decide it.
>
> **Companion standard:** IEEE 828-2012 — Standard for Configuration Management in Systems and Software Engineering. Status Accounting is one of the four core SCM activities IEEE 828 requires (identification, change control, status accounting, audit); this report is the periodic output of the third one.
>
> **Status of this template:** Lightweight Configuration Status Accounting Report structure following IEEE 828-2012 (the status-accounting activity), reduced for solo/small-team and internal/public build-in-public use. IEEE 828-2012 is a paywalled IEEE standard — this template is a faithful-to-the-outline lightweight extract, NOT a reproduction of standard text; verify section structure and any normative wording against the purchased standard before relying on it for regulated, contractual, or safety-critical contexts. No copyrighted standard text is reproduced here. Suitable as a public, reusable template.

---

# Configuration Status Accounting Report — {{System Name}}

| Field | Value |
|---|---|
| Document ID | CSAR-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 828-2012 (lightweight — status-accounting activity) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Reporting period | {{YYYY-MM-DD}} to {{YYYY-MM-DD}} (state 'as of' date if a point-in-time snapshot) |
| Baseline of record | {{BL-N — the baseline this report accounts against, e.g. 'Release 1.0 baseline'}} |
| Configuration manager | {{Name / role responsible for SCM}} |
| CM tooling / system of record | {{e.g. Git + tag scheme, issue tracker, artifact registry — where these figures are pulled from}} |
| Distribution | {{who receives this report — e.g. project board, release manager}} |

---

## 1. Introduction

> This section folds Purpose, Scope, Definitions, and References into one introduction, matching the SRS/SDD templates in this set. Before the detail: **Configuration Management (CM)** is the discipline of knowing, at any moment, exactly what versions of which parts make up a system, and controlling how those parts change. IEEE 828 names four core activities — *identification*, *change control*, *status accounting*, and *audit*. **Status accounting** is the third: recording and reporting the current state of every configuration item and every change so anyone can answer "what version is in production right now, and how did it get that way" without guessing. The "accounting" is literal — it is a ledger of the system's configuration over time. This document is the periodic output of that activity.

### 1.1 Purpose

> One paragraph. State plainly that this is a periodic RECORD, not a plan or a design — it reports state, it does not decide it. The decisions live in the Configuration Management Plan (which says HOW the project does CM) and in the change-control process; this report just photographs where things stand.

{{This report records the current configuration state of {{System Name}} as of the reporting date so that stakeholders can answer — without inspecting the system by hand — three questions: what versions of which parts make up the system, what changes are in flight, and how confident we are that the records match reality. It is a periodic record produced by the status-accounting activity defined in the project's Configuration Management Plan. It reports state; it does not decide it. Where this report and the live system disagree, the discrepancy is itself a finding (see §7).}}

### 1.2 Scope

> Define which baseline(s), configuration items, and reporting period this report covers — and what it deliberately excludes. **Scope here means "which slice of the system's configuration these numbers describe."** A report covering only the Release 1.0 baseline says nothing about an unreleased branch; if a reader assumes otherwise, every figure misleads them. Be explicit about exclusions (third-party items managed upstream, experimental branches, generated artifacts not under control).

**This report covers:**
- Baseline(s) of record: {{BL-1 — e.g. "Release 1.0 baseline"; list all baselines accounted for}}
- Configuration items: {{all CIs in the named baseline(s); or a stated subset — e.g. "application source and deployed artifacts only"}}
- Reporting period: {{YYYY-MM-DD}} to {{YYYY-MM-DD}} {{or: point-in-time snapshot as of YYYY-MM-DD}}

**This report excludes:**
- {{e.g., third-party CIs managed by upstream vendors (tracked only by pinned version, not change-controlled here)}}
- {{e.g., unreleased feature branches not yet baselined}}
- {{e.g., generated build output regenerated from source and not separately tracked}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Pre-seeded with the terms a first-time reader needs so the rest of the report reads standalone. Keep these; add project-specific terms below.

| Term | Definition |
|---|---|
| Configuration Item (CI) | Any part of the system put under CM control and tracked by version — source modules, specs, build scripts, deployed artifacts, even documents. Each gets a `CI-N` ID so it can be referenced everywhere. Not everything is a CI; the CM plan defines what is worth tracking. |
| Baseline (BL) | A named, frozen snapshot of a set of CIs at agreed versions — the reference point you measure change against (e.g., "Release 1.0 baseline"). Changes are made relative to a baseline; a new baseline is cut when that set of versions is re-frozen. Identified `BL-N`. |
| Change Request / Change (CHG) | A formally recorded request to alter one or more CIs, tracked from raised through approved/rejected to implemented and verified. Status accounting reports where each change sits in that flow. Identified `CHG-N`. |
| Defect (DEF) | Something broken — a bug. Distinct from a change: a *defect* is the broken thing; a *change* is any intended alteration (which may be the fix for a defect, or a new feature). A defect is usually resolved by an associated change. Identified `DEF-N`. |
| Configuration Audit | An independent check that the system as built actually matches what the records say. A *functional* audit checks it does what's specified; a *physical* audit checks the right versions are present. This report summarizes findings still open from such audits — it does not perform them. Findings identified `AUD-N`. |
| Build / Release (REL) | A *build* is a specific compiled/assembled instance of CIs at given versions, usually identified by a label and a checksum. A *release* is a build promoted to a deployment target. Tracking these ties "what is deployed" back to "which CI versions and which changes." Identified `REL-N`. |
| Checksum | A short fingerprint computed from a file's bytes (e.g., a SHA-256 hash). If two copies share the same checksum they are byte-identical; it is how you prove the artifact deployed is exactly the one that was built. |
| Reporting period / "as of" date | A status accounting report is a snapshot in time. Every figure in it is true *as of* a stated date — without that date the numbers are meaningless, because configuration state moves constantly. |
| {{Project term}} | {{Definition}} |

### 1.4 References

> List the records this report draws on and the documents that define what is being accounted for. Categorize as in the SRS template (governing CM plan first, then the source records the figures come from, then related specs, then external standards). The figures in this report should be traceable to these sources — a reader who doubts a number should know where to go check it.

**Governing CM plan:**
- {{path/to/SCMP.md}} — Configuration Management Plan this report fulfills (defines what is a CI, the baseline scheme, the change-control process)

**Source records (where the figures come from):**
- {{issue tracker URL / project}} — change requests (CHG-N) and defects (DEF-N)
- {{artifact registry / release page}} — builds and releases (REL-N) and their checksums
- {{version-control repo + tag scheme}} — CI versions and baseline tags (BL-N)
- {{audit log / report location}} — configuration audit findings (AUD-N)

**Related specifications:**
- {{path/to/SRS.md}} — requirements that define what the CIs must do
- {{path/to/architecture.md}} — architecture that defines what the CIs are

**External standards:**
- IEEE 828-2012 — Standard for Configuration Management in Systems and Software Engineering (status-accounting activity)

---

## 2. Configuration Summary

> The executive snapshot — the one-paragraph "state of the system as of this date" before the detailed ledgers below. A reader who only has thirty seconds should be able to read this section and stop. Lead with the **"as of" date** and explain why it governs everything: every figure below is a point-in-time snapshot, and configuration state moves constantly, so a number without its date is a number you cannot trust. Keep this section to counts and pointers — the detail lives in §3–§7.

**As of {{YYYY-MM-DD}}**, {{System Name}} is accounted against baseline **{{BL-1 — name}}**. {{One paragraph: e.g. "Twelve configuration items are under control; three changes are open (one in review, two implemented and awaiting verification); two defects remain outstanding, both low-severity; the latest release REL-3 was deployed to production on {{date}}; one physical-audit finding (AUD-1) is still open."}}

Every figure in this report is true **as of the date above** and no other. Configuration state changes continuously; for the state at a different date, see the prior issuance recorded in §9.

| Measure | Count (as of {{YYYY-MM-DD}}) | Detail in |
|---|---|---|
| Baselines (established / superseded) | {{2 / 1}} | §3 |
| Configuration items tracked | {{12}} | §4 |
| Open changes (CHG) | {{3}} | §5.1 |
| Outstanding defects (DEF) | {{2}} | §5.2 |
| Releases in scope (latest deployed) | {{3 (REL-3 on YYYY-MM-DD)}} | §6 |
| Open audit findings (AUD) | {{1}} | §7 |
| Open issues/risks (RISK) | {{1}} | §8.1 |

---

## 3. Baseline Status

> A **baseline** is a frozen, named set of CI versions you measure change against. This section reports which baselines exist, which is current, and which are superseded or retired. The IDs encode a relationship worth stating once: a baseline (`BL-N`) names a set of `CI-N` items at specific versions; a change (`CHG-N`) moves the system from one baseline toward the next. A baseline must be *auditable*, not just a label — so record which CIs each one contains (or point to the §4 list filtered by baseline), so that "the Release 1.0 baseline" resolves to a definite set of versions someone could reconstruct.

**Baseline status vocabulary** (use consistently in the table below):

| Status | Meaning |
|---|---|
| Draft | Proposed set of versions, not yet frozen or agreed. |
| Established | Frozen and agreed; the official reference point. |
| Superseded | Replaced by a later established baseline; kept for history. |
| Retired | No longer relevant or supported; kept only for the record. |

| Baseline ID | Name | Version | Date established | Status | Contains (CIs / pointer) | Notes |
|---|---|---|---|---|---|---|
| BL-1 | {{Release 1.0 baseline}} | {{1.0}} | {{YYYY-MM-DD}} | {{Established}} | {{CI-1@1.0, CI-2@1.0, … or "see §4 filtered by BL-1"}} | {{}} |
| BL-2 | {{Release 1.1 baseline}} | {{1.1}} | {{YYYY-MM-DD}} | {{Draft}} | {{see §4 filtered by BL-2}} | {{cut after CHG-2 verified}} |
| BL-0 | {{Pre-1.0 prototype baseline}} | {{0.9}} | {{YYYY-MM-DD}} | {{Superseded}} | {{see prior report}} | {{superseded by BL-1}} |

---

## 4. Configuration Item Status

> This is the core ledger. A **configuration item (CI)** is any part of the system put under version control and tracked; each gets a `CI-N` ID used everywhere else in the report. **This table is the canonical list** — every CI referenced anywhere else (in a change, a defect, an audit finding, a release) must appear here with a stable `CI-N` ID. "CI" is a deliberate choice, not a synonym for "file": not every file is a CI; the CM plan defines what is worth tracking. The point of the ID is stability — `CI-7` means the same item in this report and the next, even after its version changes.

**CI status vocabulary** (use consistently in the table below):

| Status | Meaning |
|---|---|
| New | Newly placed under control; not yet part of an established baseline. |
| Under change | Has an open change (CHG-N) against it; its version may move. |
| Baselined | Frozen at its current version as part of an established baseline. |
| Released | Part of a build/release deployed to a target. |
| Retired | No longer part of the system; kept for history. |

| CI ID | Name | Type | Current version | Status | Baseline | Location | Owner |
|---|---|---|---|---|---|---|---|
| CI-1 | {{Auth service}} | {{source}} | {{1.4.0}} | {{Baselined}} | {{BL-1}} | {{repo://services/auth}} | {{Name / role}} |
| CI-2 | {{API spec}} | {{spec / document}} | {{1.0}} | {{Baselined}} | {{BL-1}} | {{repo://docs/api.md}} | {{Name / role}} |
| CI-3 | {{Build script}} | {{build artifact}} | {{2.2}} | {{Under change}} | {{BL-2}} | {{repo://ci/build.sh}} | {{Name / role}} |
| CI-4 | {{Deployed web bundle}} | {{deployed artifact}} | {{1.0.3}} | {{Released}} | {{BL-1}} | {{registry://web@1.0.3}} | {{Name / role}} |

> **Type values:** `{{source / spec / build artifact / deployed artifact / document}}`. Add types as your system needs (config, data fixture, container image, etc.) but keep them consistent across reports.

---

## 5. Change Status

> This section accounts for items moving through a controlled flow: **change requests** (§5.1) and **defects** (§5.2). They are kept together deliberately — both track items moving from raised toward done, and both link back to CIs and releases. The linkage is the point of status accounting: a change names the CIs it touches and the release it targets; a defect names the change that fixes it and the release that carries the fix. Keeping the two in one section preserves that traceability without padding the report into two near-identical ledgers.

### 5.1 Change Requests

> A **change** is any intended alteration to one or more CIs, tracked from raised → reviewed → approved/rejected → implemented → verified. This sub-section reports where each one sits. Note the distinction from a defect (§5.2): a change is the *intended alteration*; it may be a fix, an enhancement, or an adaptation to a changed environment.

**Change status vocabulary** (use consistently in the table below):

| Status | Meaning |
|---|---|
| Raised | Recorded, not yet reviewed. |
| Under review | Being evaluated for approval. |
| Approved | Accepted; cleared to implement. |
| Rejected | Declined; kept for the record with a reason. |
| Implemented | Built; awaiting verification. |
| Verified | Confirmed working and merged into the relevant baseline. |

| CHG ID | Summary | Type | Status | Priority | Affected CIs | Owner | Target release |
|---|---|---|---|---|---|---|---|
| CHG-1 | {{Add token refresh}} | {{enhancement}} | {{Verified}} | {{High}} | {{CI-1}} | {{Name / role}} | {{REL-2}} |
| CHG-2 | {{Fix login timeout}} | {{corrective fix}} | {{Implemented}} | {{High}} | {{CI-1, CI-4}} | {{Name / role}} | {{REL-3}} |
| CHG-3 | {{Support new OS version}} | {{adaptive}} | {{Under review}} | {{Medium}} | {{CI-3}} | {{Name / role}} | {{BL-2 / REL-4}} |

> **Type values:** `{{corrective fix / enhancement / adaptive}}`. A *corrective* change fixes a defect; an *enhancement* adds capability; an *adaptive* change keeps the system working as its environment changes.

### 5.2 Defect Status

> A **defect (DEF-N)** is something broken. It is usually resolved by an associated change (`CHG-N`) — so link the two: the defect names its resolving change, and the change names the release that carries the fix. That chain (`DEF-N → CHG-N → REL-N`) is exactly the traceability status accounting exists to provide. Summarize counts by severity and status first, then table the open ones; closed defects can move to the revision-history context or be dropped.

**Defect summary (open, as of {{YYYY-MM-DD}}):**

| Severity | Open | In progress | Total open |
|---|---|---|---|
| {{Critical}} | {{0}} | {{0}} | {{0}} |
| {{Major}} | {{0}} | {{1}} | {{1}} |
| {{Minor}} | {{1}} | {{0}} | {{1}} |

**Open defects:**

| DEF ID | Summary | Severity | Status | Affected CIs | Resolving change | Fixed-in release |
|---|---|---|---|---|---|---|
| DEF-1 | {{Session not cleared on logout}} | {{Major}} | {{In progress}} | {{CI-1}} | {{CHG-2}} | {{REL-3 (pending)}} |
| DEF-2 | {{Typo in error message}} | {{Minor}} | {{Open}} | {{CI-4}} | {{(unassigned)}} | {{—}} |

---

## 6. Build and Release Status

> A **build** is a specific assembled instance of CIs at given versions, identified by a label and a **checksum**; a **release** is a build promoted to a deployment target. This section records what was built, from which baseline, what its fingerprint is, and where it went. A checksum is a short fingerprint of the artifact's bytes (e.g., a SHA-256 hash): if two copies share it, they are byte-identical. It belongs in a CM record because it ties "what is deployed" *provably* back to "which CI versions and which changes" — without it, "we deployed version 1.0.3" is a claim; with it, it is a fact you can re-check. Each release should be traceable to the baseline it was built from and the changes (`CHG-N`) it carries, so "what is in production" resolves to a definite set of CI versions.

**Release/build status vocabulary** (use consistently in the table below):

| Status | Meaning |
|---|---|
| Built | Assembled; not yet promoted anywhere. |
| Staged | Promoted to a pre-production / staging target. |
| Deployed | Promoted to its production target; currently live. |
| Rolled back | Was deployed, then withdrawn; superseded by an earlier or later release. |
| Retired | No longer deployed anywhere; kept for the record. |

| Release/Build ID | Label/tag | Built from baseline | Date | Checksum | Deployment target / environment | Status | Carries changes |
|---|---|---|---|---|---|---|---|
| REL-1 | {{v1.0.0}} | {{BL-1}} | {{YYYY-MM-DD}} | {{sha256:abcd…1234}} | {{production}} | {{Retired}} | {{CHG-? }} |
| REL-2 | {{v1.0.2}} | {{BL-1}} | {{YYYY-MM-DD}} | {{sha256:ef01…5678}} | {{production}} | {{Rolled back}} | {{CHG-1}} |
| REL-3 | {{v1.0.3}} | {{BL-1}} | {{YYYY-MM-DD}} | {{sha256:9abc…def0}} | {{production}} | {{Deployed}} | {{CHG-2}} |
| REL-4 | {{v1.1.0-rc1}} | {{BL-2}} | {{YYYY-MM-DD}} | {{sha256:1357…2468}} | {{staging}} | {{Staged}} | {{CHG-3}} |

---

## 7. Audit Findings

> A **configuration audit** is an independent check that the system as built actually matches what the records say. A *functional* audit checks it behaves as specified; a *physical* audit checks the correct CI versions are actually present. **This report does not perform the audit** — it summarizes findings still OPEN from audits already conducted, so management can see the gap between records and reality. That gap is the most important thing status accounting surfaces: a clean ledger that doesn't match the running system is worse than no ledger, because it is trusted. Closed findings can be dropped or moved to revision history; this section is for what is still unreconciled.

| Finding ID | Audit type | Date raised | Description | Affected CIs / baselines | Severity | Status | Owner |
|---|---|---|---|---|---|---|---|
| AUD-1 | {{physical}} | {{YYYY-MM-DD}} | {{Deployed bundle CI-4 checksum does not match the recorded REL-3 checksum}} | {{CI-4, REL-3}} | {{Major}} | {{open}} | {{Name / role}} |
| AUD-2 | {{functional}} | {{YYYY-MM-DD}} | {{Token-refresh behavior in CI-1 differs from API spec CI-2}} | {{CI-1, CI-2}} | {{Minor}} | {{in remediation}} | {{Name / role}} |

> **Status values:** `{{open / in remediation / closed}}`. When a finding is closed, record the change (`CHG-N`) that reconciled it so the closure is traceable, then move it out of this table on the next issuance.

---

## 8. Issues, Risks, and Open Questions

> The skeleton's SCM issues and the unresolved status-accounting decisions naturally sit together near the end of the report (the SRS and SDD templates likewise place Open Questions late). §8.1 captures problems and threats to configuration integrity; §8.2 captures decisions about the accounting itself that are not yet made.

### 8.1 Issues and Risks

> Record SCM concerns that need management attention. **Distinguish an *issue* (a problem happening now) from a *risk* (a problem that might happen)** — both belong here if they threaten configuration integrity. Examples: a CI with no owner (issue), a baseline that has drifted from its recorded versions (issue), a release whose checksum cannot be reproduced (issue), a single maintainer holding all the signing keys (risk).

| RISK ID | Description | Type | Impact | Likelihood | Affected CIs / baselines | Owner | Mitigation / status |
|---|---|---|---|---|---|---|---|
| RISK-1 | {{CI-3 has no assigned owner}} | {{issue}} | {{Changes go unreviewed}} | {{—}} | {{CI-3}} | {{Name / role}} | {{Assign owner by next issuance}} |
| RISK-2 | {{Release checksums stored only on one machine}} | {{risk}} | {{Cannot prove deployed artifacts if lost}} | {{Medium}} | {{REL-1..REL-4}} | {{Name / role}} | {{Mirror to registry — planned}} |

### 8.2 Open Questions

> Unresolved decisions about the status accounting itself, following the SRS/SDD style. Each names what is blocking resolution and who decides. Resolve and remove as work progresses.

| OQ ID | Question | What's blocking resolution | Who decides |
|---|---|---|---|
| OQ-1 | {{Should CI-5 (the data-fixture set) be promoted to a controlled item?}} | {{Unclear whether fixtures change often enough to warrant tracking}} | {{Configuration manager}} |
| OQ-2 | {{Which baseline does the hotfix branch descend from — BL-1 or BL-2?}} | {{Branch history is ambiguous; needs a git archaeology pass}} | {{Release manager}} |

---

## 9. Revision History

> Standard revision table. **For a status accounting report this table does double duty as the report's own publication log:** because each issuance is a fresh point-in-time snapshot, record each issuance and the "as of" date it covered, so a reader can find the prior snapshot and see how the configuration state changed between reports. The history is therefore not just "edits to this document" but "the sequence of snapshots this report has taken."

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |
| {{0.2}} | {{YYYY-MM-DD}} | {{Author}} | {{Second issuance — snapshot as of {{YYYY-MM-DD}}; BL-1 established, REL-3 deployed}} |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections) — without the "as of" date and scope, the figures are unreadable
- §2 Configuration Summary — the snapshot a busy reader stops at
- §4 Configuration Item Status — the canonical CI list everything else references
- §5 Change Status — what is moving through the controlled flow
- §9 Revision History — also the publication log of past snapshots

**Optional sections** (include if relevant):
- §3 Baseline Status — omit only if the project has a single, never-changing baseline (rare; usually keep it)
- §6 Build and Release Status — omit if nothing has been built or released yet
- §7 Audit Findings — omit if no configuration audit has been conducted; include as soon as one has, even with zero open findings ("audit conducted {{date}}, no open findings")
- §8 Issues, Risks, and Open Questions — track elsewhere if you prefer, but a report with no surfaced risks usually means risks aren't being looked for

**Identifier conventions** (cross-reference cleanly with sibling documents):
- `CI-N` — configuration items (the canonical list in §4)
- `CHG-N` — changes / change requests (§5.1)
- `BL-N` — baselines (§3)
- `DEF-N` — defects (§5.2)
- `REL-N` — builds / releases (§6)
- `AUD-N` — audit findings (§7)
- `RISK-N` — issues and risks (§8.1)
- `OQ-N` — open questions (§8.2)

These prefixes let the ledgers cross-reference: a baseline (`BL-N`) names its CIs; a change (`CHG-N`) names the CIs it touched and the release (`REL-N`) it targets; a defect (`DEF-N`) names its resolving change and the release that fixed it; an audit finding (`AUD-N`) names the CI or baseline it concerns. They also tie back to the Configuration Management Plan (`SCMP-…`) that defines the process this report records the output of.

**Tailoring**:
- The section organization follows IEEE 828's status-accounting activity but is guidance, not law. Add or remove sub-sections as the project needs; keep the identifier conventions stable so reports compare across periods.
- **Solo developer / small team collapse:** this whole report can shrink to a single page. Fold §3–§7 into one table per ledger (often the CI list in §4 plus a short "open changes" list in §5 is enough); keep §1.2 (scope, with the "as of" date), §2 (the one-paragraph summary), and §9 (the publication log) — those three carry the value. The discipline that matters is the **"as of" date and the canonical CI IDs**, not the number of tables. A solo developer's report can be as short as "as of {{date}}, baseline BL-1, 8 CIs all baselined, no open changes, REL-2 deployed, no open audit findings" plus the §4 table.
- Issue on a fixed rhythm (per release or per sprint) rather than only on demand — the value of status accounting is the *sequence* of snapshots, which only exists if you take them regularly.
- Every figure in the report must be traceable to the source records named in §1.4. If a number can't be traced to the issue tracker, registry, or repo, it shouldn't be in the report.

**For regulated/safety-critical projects:** use the full IEEE 828-2012 standard, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage / build-in-public products.
