# Software Project Status Report Template

> **Template purpose:** Lightweight Software Project Status Report structure for periodic project-management reporting, aligned to ISO/IEC/IEEE 16326:2019 (project status / progress reporting). Use this template each reporting period to communicate where the project actually stands. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** On a regular cadence — every week, every sprint, every month — whenever someone outside the day-to-day work (a sponsor, a customer, a teammate, your future self) needs a trustworthy, one-glance answer to "how is the project doing?" Each report is a fresh, point-in-time snapshot covering one slice of time; the report log at the end strings the snapshots into the project's health story over time.
>
> **Companion standard:** ISO/IEC/IEEE 16326:2019 — Systems and software engineering — Life cycle processes — Project management (project status / progress reporting). Lightweight extract; verify against the full standard for enterprise/regulated/contractual contexts.
>
> **Status of this template:** Lightweight extract aligned to ISO/IEC/IEEE 16326:2019 (project status/progress reporting), structured to preserve the SWEBOK Software Engineering Management KA reporting practice. ISO/IEC/IEEE 16326:2019 is a paywalled standard — this is a lightweight template derived from public sources and general project-management reporting practice; it paraphrases and reproduces NO normative text from the standard. Verify section content and terminology against the full standard before using in enterprise, regulated, or contractual contexts. Because this is a periodic record document, it is deliberately kept lean (13 focused sections, no padding); reduce further for very small projects by folding Cost/Effort, Scope, and Quality into a single "Health by Dimension" section if that better fits the cadence.

---

# Software Project Status Report (periodic project management reporting record) — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | RPT-{{PROJECT-ID}}-{{YYYY-MM-DD}} |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 16326:2019 (lightweight) |
| Owner | {{Project name or report author}} |
| Reporting period | {{YYYY-MM-DD}} to {{YYYY-MM-DD}} |
| Period number | {{e.g. Week 12 / Sprint 7 / 2026-06}} |
| Distribution | {{who receives this report}} |
| Previous report | {{RPT-{{PROJECT-ID}}-previous or "N/A (first report)"}} |
| Overall RAG | {{Green / Yellow / Red}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> This section is mostly boilerplate that carries forward period to period — write it once, then tweak. Because a status report is a *recurring record*, keep each subsection to a few lines.
>
> **1.1 Purpose** — one sentence on what this report is for: communicating the current health and progress of the named project, for the named reporting period, to its distribution list. State plainly that it is a *point-in-time snapshot*, not the project's full record.
>
> **1.2 Scope** — one or two lines on what this report covers (which workstream / release / project) and what it deliberately excludes (e.g. financial detail held in a separate budget report, or sub-team reports rolled up elsewhere).
>
> **1.3 Definitions, Acronyms, and Abbreviations** — a small table of the load-bearing terms. Define a term here only if a reader skimming the status sections below would otherwise misread it.
>
> **1.4 References** — point at the authoritative sources this report summarizes. A status report mostly *points at* the real schedule, the real risk register, and the real issue log rather than restating them; keep these references current so the report stays a lean summary sitting on top of those sources.

### 1.1 Purpose

{{This report communicates the current health and progress of {{Project Name}} for the reporting period named above, to the distribution list above. It is a point-in-time snapshot taken as of the period end — not the project's full historical record. Older detail lives in the earlier reports indexed in the Revision History (§13).}}

### 1.2 Scope

This report covers:
- {{Which workstream / release / project — e.g. "the v1.0 release of the {{Project Name}} core service"}}

This report excludes:
- {{What is handled elsewhere — e.g. "detailed cost accounting (see the separate budget report); sub-team reports rolled up into §3"}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Beginner note: define a term here only if a reader could misread the sections below without it. The four core terms below are the load-bearing ones for any status report.

| Term | Definition |
|---|---|
| RAG status | A one-glance health indicator (**R**ed / **A**mber-Yellow / **G**reen). Green = on track; Yellow = at risk, watch it; Red = off track, needs intervention. Always paired with a one-line rationale — the color alone is not the report. |
| Baseline / forecast / actual | The **baseline** is the originally agreed plan (planned date, planned cost). The **forecast** is the current best estimate of where it will land. The **actual** is what really happened. **Variance** is the gap between them. |
| Milestone | A fixed, verifiable point in the schedule — a deliverable accepted, a gate passed — not a span of work. Referenced here as MS-N so the same milestone keeps the same handle every period. |
| Risk vs. issue | A **risk** is a problem that has not happened yet (it has a probability and a potential impact). An **issue** is a problem that is already happening (it is certain and needs action now). They are tracked separately — see §10 and §11. |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> Beginner-facing tip: keep these current. The report's leanness depends on it pointing at live sources rather than copying them.

| Ref | Source |
|---|---|
| R1 | {{Schedule / baseline source — the plan that defines the MS-N milestones}} |
| R2 | {{Risk register — the authoritative home of the RISK-N risks summarized in §10}} |
| R3 | {{Issue / decision log — the authoritative home of the ACT-N items in §11}} |
| R4 | {{Requirements baseline — defines the requirement / change-request IDs used in §8}} |
| R5 | {{Previous status report — RPT-{{PROJECT-ID}}-{{previous YYYY-MM-DD}}}} |
| R6 | ISO/IEC/IEEE 16326:2019 — project management (status/progress reporting) |

---

## 2. Reporting Period

> A status report's whole meaning is anchored to its time window, so be precise here. This section answers one question: **"as of when?"** Everything below is true as of the period end unless a line flags otherwise — that is exactly what makes a status report different from a living plan (a plan is always "now"; a report is frozen at a date).
>
> Beginner note: name the prior period too, so a reader can walk back to the previous snapshot. Note the report date separately if you write the report after the period closed.

| Field | Value |
|---|---|
| Period label | {{Week 12 / Sprint 7 / June 2026}} |
| Period covers | {{YYYY-MM-DD}} to {{YYYY-MM-DD}} (inclusive) |
| Report date | {{YYYY-MM-DD — if different from period end}} |
| Prior period | {{previous label / dates — see RPT-{{PROJECT-ID}}-{{previous YYYY-MM-DD}}}} |

{{One line if anything below is stated "as of" a date other than the period end — otherwise delete this line.}}

---

## 3. Overall Status

> This is the executive summary. A busy reader should be able to stop here and still get the whole story. It has four parts, and all four are non-negotiable.
>
> Beginner note on RAG: resist "Green because we're working hard." RAG is about **outcome against plan, not effort.** If the dimension sections below (schedule, cost, scope, quality) disagree, the overall color should reflect the **worst load-bearing one**, and the rationale should explain the trade-off — not quietly average them into a comfortable Yellow.

**Overall RAG:** {{Green / Yellow / Red}}

**(a) Rationale.** {{One or two sentences on *why* this color. Tie it to outcome against plan. E.g. "Yellow: core delivery is on schedule, but MS-3 acceptance slipped one week due to an unresolved third-party dependency."}}

**(b) Trend vs. last period.** {{Improving / Steady / Worsening}} — {{one line on what moved. E.g. "Worsening: was Green last period; the dependency slip is new this period."}}

**(c) The one thing to know or do.** {{The single most important item the reader should take away or act on. E.g. "We need a go/no-go decision on the third-party dependency by {{YYYY-MM-DD}} (see ACT-4)."}}

---

## 4. Accomplishments This Period

> Report **outcomes, not activity.** "Shipped the login API and it passed acceptance" is an accomplishment a reader can verify. "Worked on the login API" is activity — it tells the reader nothing about progress against plan.
>
> Keep this to what actually *finished* within the reporting window. In-progress work belongs in §5 (Planned Work) or in the dimension sections, not here. Where an accomplishment closed a milestone, reference it (MS-N); where it resolved a prior issue or risk, reference that (ACT-N / RISK-N) so the reader can connect this period's win to a previously open item.

Completed this period:
- {{Concrete, verifiable outcome — e.g. "Login API delivered and passed acceptance test; closes MS-2."}}
- {{Outcome that resolved a prior item — e.g. "Resolved the build-flakiness issue (ACT-3); CI now green."}}
- {{Outcome that retired a risk — e.g. "Vendor contract signed, retiring RISK-5."}}
- {{...}}

---

## 5. Planned Work Next Period

> This section sets the bar that *next* period's Accomplishments (§4) will be measured against. Keep it honest and achievable — the gap between what you planned here and what you actually delivered there is one of the clearest, hardest-to-fake health signals a reader has.
>
> Beginner note: call out the upcoming milestone(s) by MS-N with their target dates, and be explicit about anything you are *waiting on* from someone else — an input, an approval, a delivery. A dependency you are waiting on is the most common reason a plan slips, so name it and name who owns it.

Targeted for next period:
- {{Top planned item — e.g. "Complete payment integration; targets MS-3 ({{YYYY-MM-DD}})."}}
- {{Planned item — e.g. "Begin load testing of the core service."}}
- {{...}}

Waiting on (dependencies / inputs):
- {{Input needed}} — from {{who}}, expected {{YYYY-MM-DD}}. {{What slips if it is late.}}

{{One line on anything that would change this plan if it slips — otherwise delete.}}

---

## 6. Schedule Status

> This is the schedule-health view. Above the table, give a one-line summary: is the project **ahead of, on, or behind** plan, and by how much. Then the table tracks each milestone.
>
> Beginner note on baselines: the **baseline date is the originally agreed date and must NOT change report-to-report** — that is the entire point of a baseline; it is the fixed yardstick. The **forecast date moves** as reality unfolds. The growing (or shrinking) distance between the two, period over period, *is* the schedule story. For any milestone that has slipped, give the cause in one line and the recovery action (or a forward reference to an ACT-N / RISK-N). This report points *at* the schedule baseline (R1) rather than restating the full plan.

**Schedule RAG:** {{Green / Yellow / Red}} — {{one-line summary: ahead / on / behind, and by how much. E.g. "Behind: one milestone (MS-3) forecast one week late; others on baseline."}}

| Milestone | Baseline Date | Forecast / Actual Date | RAG | Note |
|---|---|---|---|---|
| MS-1 {{name}} | {{YYYY-MM-DD}} | {{YYYY-MM-DD (actual)}} | Green | Delivered on baseline. |
| MS-2 {{name}} | {{YYYY-MM-DD}} | {{YYYY-MM-DD (actual)}} | Green | Closed this period (see §4). |
| MS-3 {{name}} | {{YYYY-MM-DD}} | {{YYYY-MM-DD (forecast)}} | Yellow | Slipped ~1 wk — third-party dependency; recovery via ACT-4. |
| MS-N {{name}} | {{YYYY-MM-DD}} | {{YYYY-MM-DD}} | {{R/Y/G}} | {{note}} |

---

## 7. Cost / Effort Status

> Summarize budget or effort against plan. For a lightweight or solo project, a plain **effort line — hours or person-days spent vs. planned** — is usually enough; you do not need full earned-value accounting. (If a stakeholder ever asks for earned-value vocabulary, the terms are *planned value*, *earned value*, *actual cost*, and the *SPI / CPI* ratios; most lightweight projects never need them, but they are named here so you can look them up.)
>
> Beginner note: a cost overrun and a schedule slip very often share the same root cause. If they do, **tell the story once and cross-reference** rather than repeating it here and in §6. And if the project has no tracked budget, mark this section N/A — do **not** invent numbers to fill the section.

**Cost / Effort RAG:** {{Green / Yellow / Red}} — {{headline: on / under / over by X. E.g. "On budget: 42 of 80 planned person-days used at the period mid-point."}}

| Measure | Planned | Actual (to date) | Forecast at completion | Variance |
|---|---|---|---|---|
| {{Effort (person-days)}} | {{planned}} | {{actual}} | {{forecast}} | {{+/- and %}} |
| {{Budget (currency), if tracked}} | {{planned}} | {{actual}} | {{forecast}} | {{+/- and %}} |

{{If over: one line on the cause and the corrective action. If the cause is shared with a schedule slip, cross-reference §6 / the relevant MS-N rather than retelling it. If no budget/effort is tracked: replace this whole section with "N/A — this project tracks no formal budget or effort baseline."}}

---

## 8. Scope Status

> This section makes scope changes **visible and tied to a decision**, instead of letting them be silently absorbed. **Scope creep** — the uncontrolled growth of what the project promises — is one of the most common quiet killers, and a Green schedule sitting on top of growing, unmanaged scope is really a Yellow project. Report what moved this period: requirements added, changed, dropped, or deferred; change requests raised / approved / rejected; and the current state of the backlog or requirements baseline.
>
> Beginner note: reference affected requirements and change requests by their own IDs from the requirements baseline (R4) — this report does not invent scope IDs, it points at the baseline that owns them.

**Scope RAG:** {{Green / Yellow / Red}} — {{one-line summary. E.g. "Stable: one change request approved with a tracked schedule impact; no uncontrolled growth."}}

| Change | Requested by | Status | Impact |
|---|---|---|---|
| {{CR-12 — add export-to-CSV}} | {{requester}} | {{Approved}} | {{+2 person-days; absorbed in MS-4}} |
| {{REQ-08 — deferred to v1.1}} | {{requester}} | {{Deferred}} | {{No v1.0 impact}} |
| {{...}} | {{...}} | {{Raised / Approved / Rejected / Deferred}} | {{...}} |

{{One-line summary of the backlog / requirements-baseline state if no discrete changes this period — e.g. "No scope changes this period; baseline unchanged at 47 requirements."}}

---

## 9. Quality Status

> Summarize the quality signals for the period. **Report the trend, not just the count** — "14 open defects, down from 22" tells a reader far more about where things are heading than "14 open defects." Use the few metrics you genuinely track: open vs. closed defects (and their direction), test pass rate or coverage, reviews completed, nonconformances, and any quality-related risks.
>
> Beginner note: tie any quality concern that could threaten a milestone or release back to Schedule (MS-N) or Risk (RISK-N). And **omit metrics you do not actually track** rather than reporting hollow numbers — a fabricated coverage figure is worse than an honest blank.

**Quality RAG:** {{Green / Yellow / Red}} — {{one-line summary. E.g. "Improving: defect backlog shrinking, coverage steady."}}

| Metric | This period | Last period | Trend |
|---|---|---|---|
| Open defects | {{14}} | {{22}} | {{Improving}} |
| Defects closed this period | {{11}} | {{6}} | {{Improving}} |
| Test pass rate | {{96%}} | {{94%}} | {{Steady / Improving}} |
| {{Coverage / reviews completed / nonconformances}} | {{value}} | {{value}} | {{direction}} |

{{One line on any quality concern that threatens a milestone or release, with a reference — e.g. "Two open defects block MS-3 acceptance (see §6); tracked as RISK-7."}}

---

## 10. Risk Status

> This is the **top slice** of the risk register for this period — not the whole register. Report the current top risks (with their probability/impact and trend), any new risks raised this period, and any risks that closed or *materialized into issues*. Keep the table to what is live and material; the full register (R2) holds the detail.
>
> Beginner note: a risk that has already occurred is **no longer a risk** — it is an issue. Move it to §11 (Issues and Decisions), and if it hit a milestone, reflect it in §6 (Schedule). Reference every risk by its stable RISK-N handle so a reader can follow it across periods and into the register.

**Risk RAG:** {{Green / Yellow / Red}} — {{one-line summary. E.g. "Watch: one high-impact dependency risk trending worse."}}

| RISK-N | Description | Prob / Impact | Trend | Owner | Action |
|---|---|---|---|---|---|
| RISK-3 | {{Third-party API may not meet our latency budget}} | {{Med / High}} | {{Worsening}} | {{owner}} | {{Spike + fallback design; see ACT-4}} |
| RISK-7 | {{Open defects may block release acceptance}} | {{Med / Med}} | {{Steady}} | {{owner}} | {{Prioritized in current sprint}} |
| RISK-N | {{...}} | {{L/M/H / L/M/H}} | {{New / Steady / Improving / Worsening / Closed}} | {{owner}} | {{...}} |

{{One line on any risk that closed or materialized into an issue this period — e.g. "RISK-5 closed (vendor signed, see §4); RISK-2 materialized into issue ACT-6."}}

---

## 11. Issues and Decisions

> This is where **"who needs to do what by when"** lives. An issue is a problem happening *now* (certain, needs action); a decision is a choice made or needed this period. **An issue without an owner and a due date is just a complaint** — every row gets a name and a date.
>
> Beginner note: distinguish a decision *needed* (awaiting an authority to choose) from a decision *made* (recorded for the trail). Use stable ACT-N handles so an item that persists across periods keeps the same identity and a reader can follow its history. Add a one-line note for each item that escalated, resolved, or is blocked.

| ID | Issue / Decision | Owner | Due Date | Status |
|---|---|---|---|---|
| ACT-4 | {{Decision needed: go/no-go on third-party API}} | {{authority}} | {{YYYY-MM-DD}} | {{Open — escalated to sponsor}} |
| ACT-5 | {{Issue: staging environment down, blocking test}} | {{owner}} | {{YYYY-MM-DD}} | {{Blocked — awaiting infra}} |
| ACT-6 | {{Decision made: adopt fallback design for latency}} | {{authority}} | {{YYYY-MM-DD}} | {{Resolved — recorded}} |
| ACT-N | {{...}} | {{owner}} | {{YYYY-MM-DD}} | {{Open / Blocked / Resolved / Escalated}} |

{{One line per item that escalated, resolved, or is blocked this period — or delete if the Status column already says it clearly.}}

---

## 12. Open Questions

> List questions still open at period end that have **not yet hardened into a tracked issue or decision** — things you need an answer or a direction on. This differs from §11: open questions are unresolved *uncertainties* (you do not yet know enough to decide), whereas issues are known problems with owners.
>
> Beginner note: the moment a question is clear enough to act on, **promote it into §11** (give it an ACT-N and an owner); the moment it is answered, resolve and drop it. For a recurring record, **prune stale questions each period** so this section stays short. Each live entry is just the question plus what or who is blocking its resolution.

- **OQ-1:** {{Question — e.g. "Do we support offline mode in v1, or defer to v1.1?"}} — {{what/who is blocking — e.g. "Awaiting product direction from sponsor."}}
- **OQ-2:** {{Question}} — {{blocker}}
- {{...}}

---

## 13. Revision History

> This is the **report log** — and for a periodic record it doubles as the index across periods. Each row is one issued version of this report. A reader can scan it to see the arc of the project's health over time, which is why it helpfully carries the period covered and the overall RAG each issue reported.
>
> Beginner note: this section is **mandatory and append-only.** Never delete a history row, and never silently edit a prior issue in place — a correction to an already-issued report gets a *new* row, not an overwrite. Keep this section last so it is always in the same place across every issue of the report.

| Version | Date | Author | Period covered | RAG | Changes |
|---|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | {{period label / dates}} | {{Green/Yellow/Red}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit — these are the irreducible core of a status report):
- §1 Introduction (kept lean — mostly boilerplate carried period to period)
- §2 Reporting Period (the "as of when" anchor)
- §3 Overall Status (the executive summary — RAG + rationale + trend + the one thing to do)
- §4 Accomplishments This Period
- §5 Planned Work Next Period
- §6 Schedule Status
- §13 Revision History (the append-only report log / cross-period index)

**Optional sections** (include if relevant):
- §7 Cost / Effort Status (mark N/A if the project tracks no budget/effort baseline — don't invent numbers)
- §8 Scope Status (omit only if scope is genuinely frozen and change-controlled elsewhere)
- §9 Quality Status (report only metrics you genuinely track; omit hollow numbers)
- §10 Risk Status (the top slice of the risk register; omit if no register and no material risks)
- §11 Issues and Decisions (omit only if there are none this period)
- §12 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (this report *references* most of these rather than defining them, so they cross-reference cleanly with sibling documents):
- RPT-{{PROJECT-ID}}-{{YYYY-MM-DD}}: the report document itself (one ID per issue, dated)
- MS-N: project milestones — *owned by* the schedule baseline (R1); referenced in §3, §4, §5, §6, §9
- RISK-N: risks — *owned by* the risk register (R2); referenced in §4, §9, §10
- ACT-N: action / decision items — given a stable handle here in §11 so they persist across periods; referenced in §3, §6, §10, §12
- Requirement / change-request IDs in §8 come from the requirements baseline (R4); this report does not mint its own scope IDs

**Tailoring**:
- A status report is a *snapshot*, not a plan. Keep it short. If a section has nothing to report this period, write one honest line ("No change this period") rather than padding it.
- **Solo developer / very small team:** this collapses hard. Keep §3 (Overall Status), §4 (Accomplishments), §5 (Planned Work), and §13 (Revision History); fold §7 Cost/Effort, §8 Scope, and §9 Quality into a single **"Health by Dimension"** section with one RAG-rated line each; fold §10 Risk, §11 Issues, and §12 Open Questions into a single **"Watch list"** if the volume is low. The four core questions a solo report must still answer: where are we (RAG), what got done, what's next, and what's at risk.
- **Cadence:** pick one (weekly / per sprint / monthly) and hold it. A predictable, slightly-shorter report beats an occasional, exhaustive one — the *trend* is the value, and trends need regular data points.
- **Report deltas, not just absolutes.** A single period's numbers mean little; the useful signal is the direction of travel versus the prior period. Wherever you state a count or a date, pair it with last period's figure so the trend is visible.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 16326:2019, not this lightweight version. This template is suitable for solo/small-team projects, internal reporting, and early-stage products; it deliberately omits the formal contractual, earned-value, and audit reporting structures that regulated and contractual contexts require.
