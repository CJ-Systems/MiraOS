# Measurement Plan Template

> **Template purpose:** Lightweight Measurement Plan structure aligned to ISO/IEC/IEEE 15939:2017 (the systems-and-software measurement process) and ISO/IEC 25023:2016 (measures for product quality). Use this template when you need a deliberate, repeatable way to decide what a project will count, why, and what decisions the numbers feed — instead of gathering metrics ad-hoc and hoping they mean something. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Any project where decisions ought to be informed by evidence rather than gut feel — "are we on schedule," "is quality slipping," "is this release stable enough to ship." Start one as soon as the project has goals concrete enough to ask a stakeholder question against. A measurement plan is small at first (a handful of measures, few baselines) and grows as data accumulates; that is normal.
>
> **Companion standard:** ISO/IEC/IEEE 15939:2017 — Systems and software engineering — Measurement process; ISO/IEC 25023:2016 — Systems and software Quality Requirements and Evaluation (SQuaRE) — Measurement of system and software product quality.
>
> **Status of this template:** A lightweight skeleton derived from public sources, aligned to ISO/IEC/IEEE 15939:2017 (measurement process) and ISO/IEC 25023:2016 (product-quality measures), with the SWEBOK Software Engineering Management KA as the structural backbone. It follows the 15939 information-need → base/derived measure → indicator model, reduced for solo/small-team use, and paraphrases the publicly described process model while reproducing no normative text from these (often paywalled) standards. Verify measure definitions against the full standards — especially the ISO/IEC 25023 quality-measure catalog — before relying on them in a regulated, safety-critical, or contractual context.

---

# Measurement Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | MEA-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 15939:2017 + ISO/IEC 25023:2016 (lightweight) |
| Owner | {{Project name or measurement owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Measurement period | {{e.g., per sprint / monthly / per release}} |
| Primary audience | {{who consumes the indicators — PM / team / sponsor / customer}} |
| Tooling | {{issue tracker, CI system, spreadsheet, dashboard tool used to collect and present measures}} |
| Related plans | {{Software Project Management Plan, Quality Plan, Risk Management Plan that this plan feeds}} |

---

## 1. Introduction

> This document is the plan for *how* the project will measure itself — what it will count, why it counts those things, and what decisions the resulting numbers feed. The core idea behind a **measurement process** (ISO/IEC/IEEE 15939) is that measurement is a *planned activity*, not ad-hoc number-gathering: you decide what you need to know, pick what to count, combine the counts into something meaningful, and interpret the result against a target. This section sets up the rest of the plan by stating its purpose, drawing its boundary, defining the load-bearing vocabulary, and listing the documents it depends on.

### 1.1 Purpose

> One paragraph. Establish that this is the project's single place that defines its measurement program — the deliberate, repeatable way it turns questions into numbers and numbers into decisions. Name the information needs it serves and who relies on the results.

{{This document defines the measurement program for {{Project Name}} following ISO/IEC/IEEE 15939. It names the information needs the project must answer (e.g., "will we hit the release date?", "is product quality improving?"), the measures collected to answer them, and the decisions those measures feed. The plan exists so that measurement is deliberate and repeatable rather than ad-hoc: every number has a reason to exist and a person who acts on it. Product-quality measures, where used, follow ISO/IEC 25023 so the numbers mean the same thing to everyone.}}

### 1.2 Scope

> What this plan covers and what it explicitly excludes. Note whether it covers *process* measures (how the work is going — velocity, cycle time, throughput), *product-quality* measures (how good the thing being built is — per ISO/IEC 25023), or both. Beginner note: scope is what stops a measurement program from sprawling into "measure everything." Counting things nobody needs to know is waste; the boundary keeps the program honest.

**In scope:**
- {{Process measures — e.g., velocity, cycle time, defect arrival rate}}
- {{Product-quality measures — e.g., defect density, reliability, performance against NFRs (ISO/IEC 25023)}}
- {{Lifecycle phases covered — e.g., construction and testing through release}}

**Out of scope:**
- {{e.g., individual-developer productivity ranking — excluded to avoid gaming and morale harm}}
- {{e.g., post-release operational telemetry — covered by a separate operations plan}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Define the vocabulary the rest of the plan leans on. The pre-seeded terms below are load-bearing — if a reader misreads them, they misread the whole plan. Add project-specific counting conventions here too (e.g., exactly what your project calls a "defect").

| Term | Definition |
|---|---|
| Information need | The actual question a stakeholder has (e.g., "are we going to hit the date?"). Measures exist to answer information needs. |
| Base measure | A single counted or timed quantity captured directly (e.g., lines changed, hours spent, defects found). |
| Derived measure | Two or more base measures combined by a formula (e.g., defects per thousand lines = defects ÷ KLOC). |
| Indicator | A measure plus interpretation — the thing a human reads to decide (e.g., "defect density is GREEN below X, RED above Y"). |
| Baseline | The reference value a measure is compared against (last release's rate, the historical average, a target). |
| Threshold | The line that, when crossed, means "pay attention" or "act." |
| Operational definition | The precise, unambiguous recipe for capturing a measure — what counts, when the clock starts/stops, who records it. If two people follow it and get different numbers, it is not operational yet. |
| {{KLOC}} | {{thousands of lines of code — define project counting convention: physical vs. logical lines, generated code included or not}} |
| {{Defect}} | {{project-specific: what qualifies as a defect, at what severity, found by whom}} |

### 1.4 References

> The documents this plan depends on or feeds. Beginner note: references are how a reader checks that a measure's definition matches an external standard — when a measure says "per ISO/IEC 25023," the reader can go verify it means what the catalog says.

**Companion standards:**
- ISO/IEC/IEEE 15939:2017 — measurement process model (information need → base/derived measure → indicator).
- ISO/IEC 25023:2016 — catalog of measures for the eight product-quality characteristics.

**Plans this measurement program feeds:**
- {{Software Project Management Plan — schedule/effort measures inform planning}}
- {{Quality Plan — product-quality measures inform quality gates}}
- {{Risk Management Plan — threshold breaches feed risk identification (see §8)}}

**Requirements driving product measures:**
- {{SRS / NFR document — quality requirements (NFR-N) that a 25023 measure verifies}}

**Tool documentation:**
- {{issue tracker, CI system, dashboard tool — links to how each is configured for collection}}

---

## 2. Measurement Objectives

> Every measure in this plan must trace to an objective, and every objective must come from a real stakeholder question — not from what happens to be easy to count. This section uses the **Goal-Question-Metric (GQM)** pattern: state a *goal*, ask the *questions* that would tell you whether you are meeting it, then attach *measures* to each question. That order matters — measures earn their place by answering a question, so the questions come first. An objective with no decision attached to it is a candidate to drop; you are measuring something nobody will act on.

State each measurement objective with an ID so the measures in §3 can point back to it.

| ID | Information need / Goal | Question it answers | Stakeholder | Decision it informs | Linked measures |
|---|---|---|---|---|---|
| OBJ-1 | {{Deliver on schedule}} | {{Will we hit the date?}} | {{PM}} | {{Re-scope or add capacity if at risk}} | MEA-1, MEA-2 |
| OBJ-2 | {{Ship at acceptable quality}} | {{Is defect density trending down?}} | {{QA lead}} | {{Hold release / add review gate}} | MEA-3 |
| OBJ-3 | {{Meet performance NFR}} | {{Is response time within target?}} | {{Tech lead / customer}} | {{Block release until within budget}} | MEA-4 |
| ... | ... | ... | ... | ... | ... |

For each objective, state plainly **who needs the answer** and **what decision changes** based on it. If an objective's "Decision it informs" cell is empty, flag it — measuring to answer a question nobody acts on is waste, and the objective (with its measures) is a candidate for removal.

**Traceability:** Each OBJ-N links downward to the MEA-N rows in §3 that serve it. Where the goal is a product-quality characteristic (e.g., performance efficiency, reliability — per ISO/IEC 25023), the objective also links upward to the SRS quality requirement (NFR-N) that defines the target.

---

## 3. Measures

> This is the heart of the plan. ISO/IEC/IEEE 15939 stacks three layers: a **base measure** is a single counted/timed quantity (defects found, hours spent); a **derived measure** combines base measures with a formula (defects per KLOC); an **indicator** adds interpretation so a human can decide (GREEN/AMBER/RED, or a trend direction). Each measure needs an **operational definition** precise enough that two people following it get the same number — otherwise the measure drifts and comparisons become meaningless. Where a measure relates to product quality and ISO/IEC 25023 already defines it, **prefer the standard's definition** over inventing a local one, so your numbers are comparable to everyone else's.
>
> Two cautions that belong here. First, **Goodhart's Law**: "when a measure becomes a target, it ceases to be a good measure." People optimize the number instead of the thing the number was supposed to represent — this is the most common way measurement programs backfire. Second, balance **leading** and **lagging** indicators: a lagging indicator measures an outcome after the fact (escaped defects in production); a leading indicator predicts trouble early enough to change course (rising code-review rework rate). A healthy catalog has some of each.

### 3.1 Measure catalog

> The full list of measures, one row each, with everything needed to collect and interpret them. Keep `Type` honest — most rows will be base or derived measures; the human-facing GREEN/RED rollups live in §3.3 as indicators.

| ID | Name | Type (base/derived/indicator) | Operational definition | Formula | Unit | Source | Frequency | Owner | Serves (OBJ) | Lead/Lag | 25023 ref |
|---|---|---|---|---|---|---|---|---|---|---|---|
| MEA-1 | {{Velocity}} | base | {{story points accepted in a sprint; counts only "Done" items}} | {{sum of accepted points}} | {{points/sprint}} | {{issue tracker}} | {{per sprint}} | {{PM}} | OBJ-1 | {{lagging}} | n/a |
| MEA-2 | {{Schedule variance}} | derived | {{planned vs. actual progress at checkpoint}} | {{(actual − planned) ÷ planned}} | {{%}} | {{plan + tracker}} | {{per sprint}} | {{PM}} | OBJ-1 | {{leading}} | n/a |
| MEA-3 | {{Defect density}} | derived | {{what counts as a defect (see §1.3); measured at release}} | {{defects ÷ KLOC}} | {{per KLOC}} | {{issue tracker + repo}} | {{per release}} | {{QA lead}} | OBJ-2 | {{lagging}} | {{25023 reliability ref or n/a}} |
| MEA-4 | {{Mean response time}} | base | {{p95 latency under defined load; clock from request to first byte}} | {{p95 of sampled requests}} | {{ms}} | {{CI perf test}} | {{per release}} | {{tech lead}} | OBJ-3 | {{lagging}} | {{25023 performance-efficiency ref}} |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

### 3.2 Operational definitions

> Where a catalog cell in §3.1 is too small to hold the full recipe, give it room here. An operational definition pins down every ambiguity: when the clock starts and stops, what is included and excluded, who records the value, what state qualifies. The test is repeatability — two people, same definition, same number.

- **MEA-3 (Defect density) — full definition.** {{A "defect" is a confirmed deviation from a documented requirement, logged in {{tracker}} with severity ≥ {{level}}. Counted at the moment a release branch is cut. Excludes: enhancement requests, duplicates, and items rejected as "works as designed." KLOC counts {{physical/logical}} lines in {{which paths}}, excluding generated code and vendored dependencies. Recorded by {{QA lead}} from the {{tracker}} report named {{report name}}.}}
- **MEA-{{N}} — full definition.** {{Clock start/stop, inclusion/exclusion rules, recorder...}}

### 3.3 Indicators and decision rules

> An indicator is where base and derived measures become something a human reads in seconds and acts on. State the decision rule explicitly — the thresholds, and what GREEN/AMBER/RED (or a trend direction) means. These rules tie directly to the analysis thresholds in §5 and the corrective-action triggers in §8.

| Indicator | Built from | GREEN | AMBER | RED | Reading guidance |
|---|---|---|---|---|---|
| {{Quality health}} | MEA-3 | {{< X / KLOC}} | {{X–Y / KLOC}} | {{> Y / KLOC}} | {{One RED is noise; RED two periods running is signal — see §8}} |
| {{Schedule health}} | MEA-2 | {{within ±5%}} | {{−5% to −15%}} | {{worse than −15%}} | {{Leading indicator; act before the date slips, not after}} |
| ... | ... | ... | ... | ... | ... |

---

## 4. Data Collection

> A measure is only as good as the data behind it. Collection should be **automated wherever possible** — automation removes transcription error and, just as importantly, removes the bias that creeps in when a person knows their number is being watched. Where collection must be manual, it needs a named owner and a clear trigger. Beginner note: capturing a value at the moment the event happens always beats reconstructing it later from memory, which is guesswork dressed as data.

Describe collection per measure (or in groups where the method is shared), keyed by MEA-N.

| MEA | Method (automated/manual) | Timing / trigger | Tool (system of record) | Validation at capture | Storage location |
|---|---|---|---|---|---|
| MEA-1 | {{automated}} | {{sprint close}} | {{issue tracker API}} | {{reject sprints with no end date}} | {{measurement DB / sheet}} |
| MEA-3 | {{automated}} | {{release branch cut}} | {{tracker + CI}} | {{KLOC > 0; defect count ≥ 0}} | {{measurement DB}} |
| MEA-4 | {{automated}} | {{CI perf stage}} | {{CI system}} | {{discard runs below sample size; flag outliers}} | {{CI artifacts + DB}} |
| ... | ... | ... | ... | ... | ... |

- **Method.** Prefer automated pulls from the CI system or issue tracker over manual recording; reserve manual capture for things that genuinely cannot be instrumented, and give those a named owner (see the table).
- **Timing / trigger.** State the exact moment collection fires (on commit, at sprint close, on release branch cut). Cross-reference the Tooling metadata row for the systems involved.
- **Validation at capture.** Cheap sanity checks that catch garbage at the source — range checks, required-field checks, sample-size minimums. A bad value caught at capture costs nothing; one that reaches a report costs a wrong decision.
- **Storage.** Where raw measurement data lands and in what form. This is the source of record that auditability (§7) and retention (§9) depend on.

---

## 5. Analysis

> Raw numbers are meaningless without a reference point — "12 defects" tells you almost nothing until you know whether last release had 4 or 40. Analysis is where measures become decisions. It rests on three things: a **baseline** to compare against, **thresholds** that say when to act, and **trends** that separate signal from noise. Beginner note: a baseline is the reference value (the historical average, the prior release, the target); a single data point past a threshold may be noise, but a trend moving the wrong way over several periods is a signal worth acting on.

- **Baselines.** State what each measure is compared against. {{e.g., MEA-3 is compared against the trailing three-release average; MEA-4 is compared against the NFR target value from the SRS.}} For a brand-new project with no history, note that the baseline is not yet established and will be set after {{N}} periods of data (track this in §10).
- **Thresholds / control limits.** The lines that trigger attention or action, tied to the indicator decision rules in §3.3. {{e.g., AMBER at one standard deviation above baseline, RED at two.}}
- **Trends.** Look at direction over time, not just the latest point. {{e.g., three consecutive sprints of rising rework rate is investigated even if no single value crossed RED.}} One bad point is noise; a trend is signal.
- **Interpretation guidance.** How to read common patterns, and explicit cautions against over-reacting to a single noisy reading or against optimizing the metric instead of the underlying goal (the Goodhart's Law trap named in §3). {{e.g., a sudden velocity spike may mean a sprint of small tasks, not faster delivery — read it alongside cycle time.}}

Note which analyses are **leading** (predict, act early) versus **lagging** (confirm an outcome after it happened), so readers know whether a given number lets them steer or only lets them learn.

---

## 6. Reporting

> Reporting closes the loop. A measure that no one sees, or that reaches the wrong person, or that arrives too late, drives no decision — and a measure that drives no decision is waste. The aim of this section is to get the right **indicator** to the right **audience** at the right **cadence** in a **format** they can read in seconds. Beginner note: if no decision hangs on a report, that is the question to ask — why is it being reported at all?

| Report / dashboard | Shows | Audience | Cadence | Format |
|---|---|---|---|---|
| {{Sprint health board}} | {{MEA-1, MEA-2 + schedule indicator}} | {{team, PM}} | {{per sprint}} | {{RAG status + burndown}} |
| {{Release quality summary}} | {{MEA-3, MEA-4 + quality indicator}} | {{PM, sponsor}} | {{per release}} | {{RAG + trend chart}} |
| {{Sponsor rollup}} | {{top-level indicators only}} | {{sponsor / customer}} | {{monthly}} | {{one-page RAG}} |
| ... | ... | ... | ... | ... |

- **Audience.** Not everyone needs every measure (cross-reference the Primary audience metadata row). A sponsor wants top-level RAG status; the team wants the detail behind it. Match the report's depth to the decision the audience makes.
- **Cadence.** Align frequency to the decision the report supports — a sprint-level metric reported only monthly is useless because the moment to act has passed.
- **Format.** Present indicators so they read in seconds: RED/AMBER/GREEN status, trend arrows, simple charts. The reader should not have to do arithmetic to know whether to worry.

---

## 7. Data Quality

> Confident decisions made on bad data are worse than no decision at all — they carry the authority of a number while being wrong. This section is the program's self-check. The standard **data-quality dimensions** are completeness (did we capture everything?), accuracy (are the values right?), consistency (is the same thing counted the same way every time?), timeliness (is it fresh enough to act on?), and auditability (can a reported number be traced back to its source?). State how each is assured and who owns the check.

| Dimension | What it means | Assurance check | Owner |
|---|---|---|---|
| Completeness | All events that should be captured, are | {{reconcile collected count vs. expected event count each period}} | {{measurement owner}} |
| Accuracy | Recorded values are correct | {{spot-check N records against source per period}} | {{measure owner}} |
| Consistency | Same thing counted the same way each time | {{review against operational definitions in §3.2 on any tooling change}} | {{QA lead}} |
| Timeliness | Data is fresh enough to act on | {{collection lag stays under {{X}}; alert if stale}} | {{tooling owner}} |
| Auditability | Any number traces back to its source | {{raw data retained per §9; report links to source query}} | {{measurement owner}} |

Consistency in particular ties straight back to the **operational definitions** in §3.2: if the definition is loose, the same situation gets counted differently by different people and the consistency check is what surfaces it. Auditability depends on the storage and retention choices in §4 and §9 — you cannot trace a number whose source you deleted.

---

## 8. Corrective Action

> Measurement only matters if crossing a threshold triggers a response. A threshold with no defined action is just an alarm nobody answers. This section defines the action loop and makes each trigger traceable. Distinguish two responses: to **investigate** (look closer — the number is concerning but the cause is unknown) and to **act** (change the work — re-plan, add a gate, escalate). Beginner note: write down *who* does *what* when a given indicator goes RED, before it goes RED, so the response is a plan and not an improvisation under pressure.

| ID | Trigger (indicator / threshold) | Investigation step | Action / escalation | Owner | Feeds into |
|---|---|---|---|---|---|
| AP-1 | {{MEA-3 RED for 2 periods}} | {{root-cause review of defect clusters}} | {{add review gate; re-plan if systemic}} | {{QA lead}} | {{Risk Management Plan}} |
| AP-2 | {{MEA-2 schedule variance worse than −15%}} | {{scope and capacity review}} | {{re-scope release or add capacity}} | {{PM}} | {{Project Management Plan}} |
| AP-3 | {{MEA-4 exceeds NFR target}} | {{profile hot paths}} | {{block release until within budget}} | {{tech lead}} | {{Quality Plan}} |
| ... | ... | ... | ... | ... | ... |

State explicitly where corrective actions hand off: a sustained threshold breach often *becomes* a risk and should feed the **Risk Management Plan**; a schedule or scope action feeds the **Software Project Management Plan**; a quality gate feeds the **Quality Plan** (cross-reference the Related plans metadata row). The investigate-versus-act split keeps the team from over-reacting to a single noisy reading (investigate first) while ensuring a real, sustained signal actually changes the work (then act).

---

## 9. Retention

> Measurement data has a useful life and a disposal point. Keeping the right history is what makes baselines and trend analysis possible — you cannot compare against last year if you threw last year away. But keeping everything forever creates clutter and, where the data includes people, real privacy and compliance risk. This section says what is kept, for how long, and how it is disposed of. Beginner note: retention also underwrites auditability (§7) — you cannot trace a number whose source you have deleted.

| Data class | Retained? | Period | Disposal | Notes |
|---|---|---|---|---|
| Raw base measures | {{yes}} | {{e.g., 13 months}} | {{archive then purge}} | {{enough to recompute a year of derived measures}} |
| Derived measures / aggregates | {{yes}} | {{e.g., project life + 1 year}} | {{archive}} | {{baselines need long history}} |
| Reports / dashboards snapshots | {{yes}} | {{per release, kept indefinitely}} | {{archive}} | {{decision record}} |
| Person-linked measures (if any) | {{minimize}} | {{shortest defensible}} | {{delete on schedule}} | {{privacy/compliance constraints — see below}} |

- **What is retained.** Distinguish raw measures (needed to recompute and audit) from derived/aggregated values (needed for baselines) from report snapshots (the decision record).
- **Retention period.** State how long each class is kept and why — baselines and trends need history; high-volume per-event raw data may age out once the aggregates it fed are stable.
- **Disposal.** How data is archived or deleted at end of life, and any **privacy/compliance constraints** on measurement data that includes people. Measures that can be traced to an individual (e.g., per-developer numbers) carry obligations and gaming risk — retain the minimum defensible and dispose on schedule.

---

## 10. Open Questions

> Track unresolved measurement decisions here so they do not get lost between sessions. Resolve and remove items as the program matures. Beginner note: it is completely normal to start with few or no baselines and fill them in as data accumulates over the first several periods — an empty baseline is an open question, not a failure.

### 10.1 Deferred with defaults

> Items that have a working default so the program can run today, but that may need revisiting once data arrives.

- **OQ-DEF-1** {{Defect severity weighting in MEA-3}} — *default: all severities counted equally.* {{Revisit once enough defects accumulate to see whether weighting changes the signal.}}
- **OQ-DEF-2** {{Baseline for MEA-4 on this new project}} — *default: use the SRS NFR target as the baseline until {{N}} releases of history exist, then switch to trailing average.*
- **OQ-DEF-3** {{Whether MEA-1 (velocity) is gameable}} — *default: report alongside cycle time so a velocity spike can be cross-checked.* {{Watch for Goodhart's-Law drift.}}
- ...

### 10.2 Resolved (recorded for traceability)

- **OQ-1** {{Should we measure per-developer output?}}: {{Resolved — no; excluded in §1.2 to avoid gaming and morale harm.}}
- **OQ-2** {{Which leading indicator predicts schedule slip earliest?}}: {{Resolved — MEA-2 schedule variance; designated leading in §3.1.}}
- ...

---

## 11. Revision History

> Every substantive change to objectives, measures, thresholds, or owners gets a version bump. The plan is a living document — a stale measure (one whose definition, baseline, or owner no longer matches reality) is worse than no measure, because people still trust the number.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Measurement Objectives — without objectives, the measures have no reason to exist
- §3 Measures (at minimum the §3.1 catalog and §3.3 indicators)
- §4 Data Collection
- §11 Revision History

**Optional sections** (include if relevant):
- §5 Analysis (fold into §3.3 if your decision rules are simple)
- §6 Reporting (omit if the audience is one person who reads the dashboard directly)
- §7 Data Quality (recommended for any program whose numbers feed real decisions; can be brief for a tiny team)
- §8 Corrective Action (omit only if thresholds are purely informational — but then question why they are thresholds)
- §9 Retention (omit if no data is kept beyond the current period; include the moment baselines matter or person-linked data exists)
- §10 Open Questions (track elsewhere if you prefer)

**Identifier conventions:**
- OBJ-N: measurement objectives / information needs (§2)
- MEA-N: individual measures (§3) — trace upward to OBJ-N and, for quality measures, to SRS NFR-N
- IND (in §3.3): indicators built from base/derived measures
- AP-N: corrective-action triggers (§8)
- OQ-N / OQ-DEF-N: open questions (resolved / deferred-with-defaults)

These prefixes enable cross-document traceability: a quality requirement in the SRS (NFR-N) drives an objective (OBJ-N) here, which is served by a measure (MEA-N), whose breach fires a corrective action (AP-N) that may feed the Risk Management Plan.

**Tailoring:**
- The 15939 stack (information need → base measure → derived measure → indicator) is the backbone — keep the *order* even when you compress the sections. Decide what you need to know before you decide what to count.
- Prefer ISO/IEC 25023 definitions for product-quality measures so your numbers are comparable; only invent a local measure when no standard one fits, and write the operational definition in §3.2.
- **Solo developer / small team:** collapse hard. A single page can carry it: a short objectives list (§2), a five-row measure catalog with built-in indicators (§3.1 + §3.3), one line each on collection and analysis (§4–§5), and the revision history (§11). Skip §6 Reporting if you are the only audience and §9 Retention until you have history worth keeping. Keep §2 and §3 no matter how small — measuring without objectives is the very ad-hoc number-gathering this plan exists to prevent.
- Start with few baselines and accept it. A new project has no history; set provisional baselines from targets (§5) and record the gaps as deferred-with-defaults in §10.1, then fill them in as data accumulates.
- Revision history is mandatory. Stale measures mislead with the authority of a number — bump the version on every substantive change.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 15939:2017 and ISO/IEC 25023:2016 standards, not this lightweight version. In particular, verify every product-quality measure against the purchased ISO/IEC 25023 catalog before relying on it in a contractual or compliance context — this template paraphrases the public process model and does not reproduce the standards' normative measure definitions.
