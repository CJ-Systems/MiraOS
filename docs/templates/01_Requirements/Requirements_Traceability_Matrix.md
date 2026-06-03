# Requirements Traceability Matrix Template

> **Template purpose:** Lightweight Requirements Traceability Matrix (RTM) structure that realizes the bidirectional-traceability obligation of ISO/IEC/IEEE 29148:2018. Use this template to build the table that links each requirement across its whole life — from a stakeholder need through the software requirement, design, code, and tests that satisfy it. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once you have an SRS (and ideally an SDD and a test plan) and you need to *prove* every requirement is built and tested, and that nothing was built that no requirement asked for. The RTM is a companion record to the SRS, not a standalone requirements document — it indexes IDs that already live in those other documents.
>
> **Companion standard:** ISO/IEC/IEEE 29148:2018 — Systems and software engineering — Life cycle processes — Requirements engineering (traceability requirements, Clause 5.2.8 and bidirectional traceability provisions). The RTM is the instrument that realizes the bidirectional-traceability obligation 29148 places on a requirements process; it is a companion record to the SRS, not a standalone normative document.
>
> **Status of this template:** Lightweight traceability instrument — a skeleton derived from public sources and aligned in house depth/formatting with the SRS and SDD templates. It follows the bidirectional-traceability provisions of ISO/IEC/IEEE 29148:2018, which is a PAYWALLED standard — this template paraphrases the matrix structure and column semantics in original wording and reproduces NO normative text from the standard. As a companion record to the SRS rather than a standalone normative document, verify against the full purchased 29148 standard for enterprise, regulated, or safety-critical contexts. Suitable as-is for solo/small-team and internal documentation.

---

# Requirements Traceability Matrix (RTM) — {{System Name}}

| Field | Value |
|---|---|
| Document ID | RTM-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29148:2018 (lightweight — traceability provisions) |
| Owner | {{Project name or owner}} |
| Traces from | {{SRS-PROJECT-ID-001 and its baseline version}} — the source-of-truth requirements document this matrix indexes |
| Coverage baseline | {{e.g. Release REL-001 / sprint / milestone the matrix is current as of}} |
| Trace direction | Bidirectional (forward: need → test; backward: test → need) |
| Last reconciled | {{YYYY-MM-DD}} — date the matrix was last checked against the live SRS, design, and test artifacts |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: state plainly that this is a traceability *record*, not a requirements *definition*. The SRS defines requirements; this matrix only links the IDs that already exist in the SRS, the design documents, the code, and the tests — and surfaces where links are missing. For a beginner: the matrix exists to answer two questions. Reading a row left-to-right (forward) answers "is this need actually built and tested?" Reading right-to-left (backward) answers "is everything we built justified by a need?" If you can answer both for every row, you have *traceability* — the documented ability to follow a requirement in both directions across its whole life.

This document is the Requirements Traceability Matrix for **{{System Name}}**. It does not define requirements — that is the job of the SRS ({{SRS-PROJECT-ID-001}}). Instead it **indexes** each requirement across the lifecycle: stakeholder need → system requirement → software requirement → design element → code component → test case, plus supporting links to defects and releases. Its two jobs are to prove **forward coverage** (every need is built and tested) and **backward justification** (everything built is traceable to a need), and to make any **coverage gap** — a requirement with no design, no code, or no test — immediately visible.

### 1.2 Scope

> Define what this matrix covers and, just as importantly, what it does NOT. The RTM references the SRS, the design, the test plan, and the defect tracker — it is none of them. Note the small-project case (one matrix may be the only traceability instrument) and the large-project case (split per subsystem).

In scope:
- The requirement baseline {{SRS-PROJECT-ID-001 v{{X.Y}}}} and the releases {{REL-001 … REL-NNN}} it covers.
- Forward links from each requirement to its design, code, and tests; backward links from code and tests to their justifying requirement.
- Coverage and orphan analysis derived from the matrix (see §6).

Out of scope (referenced, not owned by this document):
- **The SRS** — defines the requirements; this matrix only links their IDs.
- **The test plan / test cases** — define *how* requirements are verified; this matrix only links TC-N IDs.
- **The defect tracker** — owns defect detail; this matrix only links DEF-N IDs.

For a small or solo project this single matrix may be the **only** traceability instrument. Larger systems may maintain one matrix per subsystem and roll them up; if so, note the split and the roll-up point here.

### 1.3 Definitions and Acronyms

> Seed with the core concepts so a beginner can read the rest of the document without guessing. Define every formal term plainly the first time it appears.

| Term | Definition |
|---|---|
| Traceability | The documented ability to follow a requirement *forwards* (from a stakeholder need, through the software requirement, design, code, and tests that satisfy it) and *backwards* (from any test or code element back to the need that justifies it). It is what lets you answer "why does this exist?" and "what breaks if I change this?" |
| Bidirectional traceability | Links that can be read in both directions: forward (need → test) proves every need is covered; backward (test → need) proves nothing exists without a justifying requirement. 29148 expects both, not just forward. |
| Requirements Traceability Matrix (RTM) | The table (the instrument) where each row is one *trace thread*: one requirement followed across the lifecycle columns. A derived/record document — it restates IDs from the SRS, design, and test artifacts rather than inventing new content. |
| Trace thread / row | One requirement followed across all lifecycle columns. The unit of the matrix: one row = one thread. |
| Coverage gap | A row missing a downstream link (a requirement with no design element, or no test case). Gaps are the main thing the RTM exists to surface — chiefly an *untested* requirement. |
| Orphan | A code component, design element, or test that traces backward to no requirement. Orphans signal either scope creep (work nobody asked for) or a missing requirement that should be written down. |
| Forward / backward reading | Reading a row left-to-right verifies a need was built and tested; reading right-to-left verifies built/tested things are all justified. |
| Status (per row) | The lifecycle state of a single trace thread (e.g. Draft / Designed / Implemented / Verified / Closed) — distinct from the Status of the whole document. Lets the matrix double as a lightweight coverage dashboard. |
| {{Term}} | {{Definition}} |

### 1.4 References

> The References here are *load-bearing*: every column in the matrix links into one of these documents. The matrix is the spine's index; these are the spine. List each with its Document ID and version so the links are unambiguous.

| Ref | Document |
|---|---|
| R1 | {{SRS-PROJECT-ID-001 v{{X.Y}}}} — Software Requirements Specification. **The spine the matrix hangs on**; supplies StR-N / SyR-N / SRS-N. |
| R2 | {{SDD-MODULE-ID-001 / architecture doc}} — Software Design Description(s). Supplies design IDs (ARCH-N, PURP-N, IF-N, CON-N). |
| R3 | {{Test plan / test case register}} — supplies TC-N IDs. |
| R4 | {{Defect tracker / issue register}} — supplies DEF-N IDs. |
| R5 | {{Release plan / changelog}} — supplies REL-N IDs. |
| R6 | {{ADR-NNNN}} — relevant Architecture Decision Records. |
| R7 | ISO/IEC/IEEE 29148:2018 — Requirements engineering (bidirectional traceability provisions). |

---

## 2. What the Matrix Is and Why Trace

> Plain-language onramp — read this before you meet the table in §4. A Requirements Traceability Matrix is a table where **each row follows one requirement across the lifecycle**. A project maintains one for four reasons:
> 1. **Prove coverage** — show every stakeholder need reaches a test, so nothing was quietly dropped.
> 2. **Impact analysis** — when a requirement changes, the row instantly shows which design, code, and tests are affected (so you know what to re-check).
> 3. **Gap and orphan detection** — missing links (gaps) and unjustified work (orphans) become visible at a glance.
> 4. **Standard obligation** — 29148 expects *bidirectional* traceability; the matrix is how you demonstrate it.
>
> This is deliberately a *short* document: the matrix in §4 is the deliverable, and the surrounding prose only explains how to read it, build it, and keep it honest.

A worked single-thread example, so the shape is concrete before the full table:

> **StR-003** "a user can recover a deleted note" → **SyR-007** "the system shall retain deleted notes for a recovery window" → **SRS-042** "deleted notes are restorable for {{N}} days via the recovery view" → **ARCH-012** (recovery subsystem) → **CODE-Recovery** (`{{path/to/recovery_module}}`) → **TC-088** "restore a note within the window" → **Status: Verified**.

Read left-to-right, that thread proves the need was understood, specified, designed, built, and tested. Read right-to-left, it proves the recovery code exists *because* a real stakeholder asked for it — not because someone felt like building it.

**Instrument-document principle.** The RTM is a *derived* record. It restates IDs that live in the SRS, the design documents, and the test artifacts — it invents nothing. The direct consequence: **the matrix goes stale the moment any of those documents change.** That is why §6 prescribes a maintenance discipline; an unmaintained RTM is worse than none, because it asserts a coverage story that is no longer true.

---

## 3. Matrix Structure and Column Reference

> This is the heart's blueprint: it defines every column the table in §4 will use, where each column draws its IDs from, and what a blank cell *means*. For a beginner, the most important idea here is direction: a blank cell **downstream** (to the right) is a potential **gap** (something not yet designed/built/tested); a blank cell **upstream** (to the left) is a potential **orphan** (something built with no justifying need). The columns below follow the suggested trace chain. You may drop columns your project does not use yet (e.g. Defect/Release on an early prototype) — call that **honest tailoring**, not omission, and record it in §7.

| Column | Links to | Source document / ID prefix | How to fill it (beginner note) | Blank cell means |
|---|---|---|---|---|
| Stakeholder Need ID | The originating stakeholder need | Stakeholder Requirements Spec — `StR-N` | Copy the need ID that justifies this thread. Read backward, this is "why we did it." | Upstream blank → **orphan**: a requirement with no stakeholder justification. |
| System / Software Requirement ID | The system requirement and/or the software requirement | System Req. Spec — `SyR-N`; SRS — `SRS-N` | The skeleton collapsed system+software into one column. **You may split into two columns** if your project distinguishes a SyR from its derived SRS, **or keep one** if you do not. Be consistent. | Upstream blank → the design/code below traces to no requirement (orphan). |
| Design Element | The design that realizes the requirement | SDD / architecture — `ARCH-N`, or SDD IDs `PURP-N` / `IF-N` / `CON-N` | Copy the design ID(s) that satisfy this requirement. | Downstream blank → requirement **not yet designed** (gap). |
| Code Component | The code that implements the design | Code — `CODE-N` and/or module path | Copy the component ID or `{{path/to/module}}`. | Downstream blank → requirement **not yet implemented** (gap). |
| Test Case ID | The test that verifies the requirement | Test plan — `TC-N` | Copy the verifying test ID(s). | Downstream blank → requirement **untested** — the highest-risk gap. |
| Defect ID | Defects found against this thread | Defect tracker — `DEF-N` | Link any open/closed defects affecting this thread. Optional on early projects. | Blank → no known defects (normal). |
| Release ID | The release the thread is delivered in | Release plan — `REL-N` | Link the release the thread targets/ships in. Optional on early projects. | Blank → not yet scheduled to a release. |
| Status | The lifecycle state of *this thread* | (this matrix) | Set from the vocabulary below. **Per-row, not per-document.** | Blank → unstarted; set to `Draft`. |

**Status vocabulary (per row).** Define one canonical set and use it everywhere. A common minimal set:

| Status | Meaning |
|---|---|
| Draft | The requirement exists; no design/code/test linked yet. |
| Designed | A design element is linked; not yet implemented. |
| Implemented | Code is linked; not yet verified by a test. |
| Verified | A passing test case is linked — the thread is fully traced forward. |
| Closed | Verified and accepted into a release; no open work or defects. |

> Tailoring note: the Status set above is a starting point. If your project tracks a different lifecycle (e.g. adds `Blocked` or `Deferred`), record the canonical vocabulary in §7 (Open Questions) until it stabilizes, then fix it here. The whole matrix must use one vocabulary or the dashboard read in §6 is meaningless.

---

## 4. The Traceability Matrix

> The instrument itself — the reason the document exists. Below is the full table using the columns from §3. Two seed rows are included: one **complete** forward thread (shows what "done" looks like) and one **deliberately incomplete** thread (a requirement designed and built but not yet tested — shows what a gap looks like *in situ*, so you recognize one when you see it).
>
> Practical mechanics for a beginner:
> - **One row per requirement thread.** If one requirement maps to several tests or several design elements, you have two honest choices: (a) *one row, multiple IDs in a cell*, or (b) *row explosion* — one row per (requirement × test) pair. Pick one strategy and apply it everywhere; **consistency matters more than which one you choose**.
> - **Sort by `StR-N` or `SRS-N`** for stable, diff-friendly reading.
> - **Keep this file in version control alongside the SRS** so the two move together and a reviewer can see them change in the same commit.
> - For larger systems the canonical matrix may live in a **spreadsheet/CSV** and this Markdown table is a *snapshot*. That is a valid tailoring choice — but flag it (§7), because a snapshot has its own staleness risk: it is only as current as the last export.

| StR-N | SyR-N | SRS-N | Design (ARCH-N / SDD ID) | Code (CODE-N / path) | Test (TC-N) | Defect (DEF-N) | Release (REL-N) | Status |
|---|---|---|---|---|---|---|---|---|
| StR-003 | SyR-007 | SRS-042 | ARCH-012 | CODE-Recovery (`{{path/to/recovery}}`) | TC-088 | — | REL-002 | Verified |
| {{StR-005}} | {{SyR-011}} | {{SRS-061}} | {{ARCH-020}} | {{CODE-Export}} | *(none yet — gap)* | — | {{REL-003}} | Implemented |
| {{StR-N}} | {{SyR-N}} | {{SRS-N}} | {{ARCH-N / PURP-N / IF-N}} | {{CODE-N / path}} | {{TC-N}} | {{DEF-N}} | {{REL-N}} | {{Draft / Designed / Implemented / Verified / Closed}} |

> The second seed row is the teaching case: `SRS-061` is implemented but its Test cell is empty and Status is `Implemented`, not `Verified`. That blank is **data, not an error to hide** — it is exactly the untested-requirement gap the matrix exists to surface, and §6 explains how to count it.

---

## 5. Building the Matrix

> How to populate the matrix from scratch, for someone who has never built one. Follow the ordered method below. The single most important beginner rule appears in step 5: **do not invent IDs here.** Every ID is *pulled* from its home document; if a link target does not exist yet, leave the cell blank — that blank is the gap the matrix is meant to expose, not a hole to paper over.

1. **Start from the SRS requirement list.** Every `SRS-N` gets a row. Doing this first guarantees forward coverage of *requirements*: no software requirement can be silently missing from the matrix.
2. **Walk backward to attach each `SRS-N` to its `SyR-N` and `StR-N`.** This surfaces any requirement with no stakeholder justification — a candidate orphan. (If you split system/software requirements into two columns per §3, fill both.)
3. **Walk forward to attach design elements** (`ARCH-N` / `PURP-N` / `IF-N`) to each requirement, **then code components** (`CODE-N` / path), **then test cases** (`TC-N`).
4. **Set Defect and Release links** where they apply (skip if those columns are out of scope for this project's maturity — see §7).
5. **Leave cells genuinely blank where the link does not exist yet, and set Status accordingly.** Blanks are *data*. A blank Test cell with Status `Implemented` truthfully says "built, not yet verified." **Pull every ID from its home document** — never mint a new ID inside the matrix; the RTM carries no requirement IDs of its own.

**Run both build directions.** Steps 1–3 are *top-down* (from needs to code/tests) — they catch forward gaps. Now run the complement, *bottom-up*: walk the code modules and the test register and check that each traces back to a row. Anything that does not is an **orphan** (scope creep, or a missing requirement to write down). Top-down alone never catches orphans on the code side; only the bottom-up pass does. Running both is what makes the traceability genuinely *bidirectional*.

Keep this section short in practice — the RTM is an instrument document, not a methodology essay. The deliverable is the populated table, not prose about it.

---

## 6. Maintaining the Matrix and Coverage Analysis

> Two jobs in one section: keeping a derived document honest (maintenance), and reading the story out of it (coverage analysis). A beginner should leave this section able to (a) know *when* to update the matrix and (b) know *what numbers to read off it*.

**Maintenance — keeping a derived record honest.** The RTM sits *downstream* of the SRS, the SDD/architecture, and the test artifacts. It goes stale the instant any of them change. Therefore:

- Define a **reconciliation trigger** and stick to it: reconcile on every requirement change, on every release, or on a fixed cadence ({{e.g. weekly / per sprint}}) — pick one and record it.
- Update the **Last reconciled** metadata row every time you reconcile, so any reader can judge how much to trust the coverage story.
- The per-change rule for a beginner: **when you change a requirement, walk its row and update or invalidate every downstream link before you call the change done.** A requirement edit that leaves stale design/code/test links is a half-finished change.

**Coverage analysis — what the matrix is FOR.** Read the matrix as a lightweight dashboard:

- **Rows with no `TC-N`** → untested requirements. **The highest-risk gap** — something specified and possibly built that no test guards.
- **Rows with no design/code** → unimplemented requirements (specified, not yet built).
- **Code/test entries that trace back to no requirement** → orphans / scope creep (found only by the bottom-up pass in §5).

Keep a tiny **coverage roll-up** at the top of the matrix so the headline number is always visible, e.g.:

> Coverage as of {{YYYY-MM-DD}}: **{{X}} of {{Y}} requirements Verified** · {{G}} forward gaps · {{O}} orphans outstanding.

**Tie back to 29148.** Bidirectional traceability is only *true* when **both** sides are actively reconciled — forward gaps closed (every need reaches a test) **and** backward orphans resolved (everything built traces to a need). Filling the forward columns once and never checking the backward direction is forward traceability only; it does not satisfy the standard's bidirectional expectation.

---

## 7. Open Questions

> Tailoring and coverage decisions not yet settled. For a matrix these are usually about *shape* (which columns, what Status vocabulary, where the canonical copy lives) and *current gaps* (which requirements are knowingly uncovered). Use the `OQ-N` convention from the house templates; put settled-for-now decisions under "deferred with defaults." Resolve and remove as the matrix matures.

### 7.1 Deferred with defaults

- **OQ-DEF-1** Split `SyR` and `SRS` into separate columns? — *default: keep one combined column until the project distinguishes system from software requirements.*
- **OQ-DEF-2** Are Defect/Release columns in scope at this maturity? — *default: Defect column omitted until first release; track defects in the issue tracker and add the column at v1.0.*
- **OQ-DEF-3** Canonical Status vocabulary — *default: Draft / Designed / Implemented / Verified / Closed (per §3); revisit if the team's lifecycle needs more states.*
- **OQ-DEF-4** Where does the source-of-truth copy live and how are snapshots synced? — *default: Markdown table in version control is canonical for solo/small-team; revisit a spreadsheet/CSV master with a Markdown snapshot if the matrix outgrows hand-editing.*

### 7.2 Open

- **OQ-1** Which requirements currently have known coverage gaps awaiting resolution? — {{list `SRS-N` rows with no `TC-N`, owner, target release}}.
- **OQ-2** {{Question}} — {{what's blocking, who decides}}.

---

## 8. Revision History

> Mandatory final section. For an RTM specifically, this document-level history tracks changes to the matrix's *structure and reconciliation events* — columns added or dropped, the requirement baseline re-synced, a coverage milestone reached. It is **distinct from the per-row Status field**, which tracks individual trace threads. Keeping them separate stops routine cell edits from polluting the document history.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — especially §1.4 References, since every column links into one of them)
- §3 Matrix Structure and Column Reference
- §4 The Traceability Matrix (the deliverable)
- §8 Revision History

**Optional sections** (include if relevant):
- §2 What the Matrix Is and Why Trace (omit only if every reader already knows the RTM concept; recommended for any document with new contributors)
- §5 Building the Matrix (omit if the team already has a standing build procedure recorded elsewhere)
- §6 Maintaining the Matrix and Coverage Analysis (strongly recommended — an unmaintained matrix lies)
- §7 Open Questions (track elsewhere if you prefer)

**Tailoring**:
- The columns in §3 are guidance, not a mandate. **Drop columns the project does not use** (e.g. Defect/Release on an early prototype) — record the choice in §7 so it reads as honest tailoring, not omission.
- Choose **one** row-explosion strategy (one row with multiple IDs per cell, *or* one row per requirement×test pair) and apply it everywhere; consistency beats the specific choice.
- Keep the ID-prefix conventions (`StR-N`, `SyR-N`, `SRS-N`, `ARCH-N` / `PURP-N` / `IF-N` / `CON-N`, `CODE-N`, `TC-N`, `DEF-N`, `REL-N`) identical to the SRS and SDD templates so cross-document links resolve cleanly. The RTM mints no IDs of its own.
- **Solo developer / small team collapse:** keep §1, §3, §4, §8 and the coverage roll-up line from §6; fold §2 and §5 into a sentence each; this single Markdown matrix in version control is then your only traceability instrument. As the project grows, promote the matrix to a spreadsheet/CSV master (§7 OQ-DEF-4) and split per-subsystem if it outgrows one table.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29148:2018, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
