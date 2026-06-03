# Problem Report Template

> **Template purpose:** Lightweight Problem Report (PR) — a single recorded observation that the system did something other than what was expected, tracked from first sighting through to closure. One Problem Report file = one PR-N record. Replace `{{placeholder}}` content with the specifics of the actual problem. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Whenever someone observes that {{System Name}} behaved other than expected and that observation needs to be captured accountably — so it is not lost, can be analyzed, dispositioned, and verified-closed. File one PR per distinct problem. A PR records *that something is wrong*; the authorized work to fix it lives in a separate Change Request (CR).
>
> **Companion standard:** IEEE 1044-2009 (Standard Classification for Software Anomalies) + ISO/IEC/IEEE 14764:2022 (Software Engineering — Software Life Cycle Processes — Maintenance).
>
> **Status of this template:** Lightweight Problem Report (instance/record document) — a lightweight skeleton derived from public sources, aligned to IEEE 1044-2009 (anomaly classification) and ISO/IEC/IEEE 14764:2022 (maintenance process); the SWEBOK Software Maintenance KA structure (Problem/Modification identification → Analysis → Disposition → Implementation → Verification → Status tracking) is the underlying organizing frame. Both companion standards are PAYWALLED IEEE/ISO publications — this template reproduces NO normative text from them; it follows their published outline and terminology only. Verify against the full standards for regulated, safety-critical, or contractually-bound contexts. This is a record/instance document: keep it lean — one PR per file, do not pad with sections that don't apply to the specific problem.

---

# Problem Report — {{System Name}}

| Field | Value |
|---|---|
| PR ID | PR-{{SYSTEM-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 1044-2009 + ISO/IEC/IEEE 14764:2022 (lightweight) |
| Owner | {{Project name or owner}} |
| Reporter | {{Who observed and filed this — name / role / 'external user'}} |
| Date observed | {{YYYY-MM-DD — when the problem was first seen, which may pre-date the filing date}} |
| Product / Version | {{Released or build version the problem was seen in, e.g. v1.4.2 / commit abc1234}} |
| Environment | {{OS, runtime, config, data set — enough to attempt reproduction}} |
| Anomaly class | {{Functional / Performance / Security / Usability / Data / Documentation — per IEEE 1044}} |
| Maintenance category | {{Corrective / Adaptive / Perfective / Preventive — per ISO/IEC/IEEE 14764}} |
| Severity | {{Critical / Major / Moderate / Minor — impact if it occurs}} |
| Priority | {{Urgent / High / Medium / Low — how soon to act}} |
| Disposition | {{Open / Correct / Defer / Duplicate / Cannot Reproduce / Not a Problem / Enhancement}} |
| Related CR / PR | {{CR-N this spawned; PR-N this duplicates; SRS-N / SDD-N implicated}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> This is a single recorded problem (one PR), tracked from first observation through to closure, against {{System Name}}. A **Problem Report (PR)** is a RECORD, not a plan: it captures one problem from first sighting through to closure. Its companion is the **Change Request (CR)** — the PR says "something is wrong," the CR is the authorized work to fix it. This introduction orients a reader who has never seen a PR before, then states purpose, scope, the few terms this record needs, and the documents it references.

### 1.1 Purpose

> One paragraph: why this record exists and what it is FOR — capturing one anomaly accountably so it is not lost, can be analyzed, dispositioned, and verified-closed. State plainly that a PR records a *problem*; the authorized fix lives in a Change Request. An **anomaly** (IEEE 1044) is the neutral umbrella word for "anything observed that deviates from expectation" — deliberately broader than "bug," because at filing time we do not yet know whether it is a real defect, a misunderstanding, an enhancement idea, or not-a-problem-at-all. The neutral word stops us from assuming the cause before we have analyzed it.

{{This document records a single observed anomaly in {{System Name}}: a case where the system did something other than what was expected. Its purpose is to capture that one problem accountably — so it is not lost, can be analyzed back to a probable cause, given an explicit decision (disposition), and, if fixed, verified closed. This PR records the problem. The authorized work to fix it, if any, is tracked in Change Request {{CR-{{SYSTEM-ID}}-NNN}}.}}

### 1.2 Scope

> What this single PR covers and explicitly does NOT cover. A PR is *one* problem. If reproduction reveals several distinct problems, split into separate PRs and note the split here. State the boundary: this record stops at closure of THIS anomaly; broader remediation (release planning, multi-bug epics, root-cause programs) tracks elsewhere.

This PR covers:
- {{The single anomaly described in §2 — one observed gap between expected and actual behavior.}}

This PR does NOT cover:
- {{Other problems noticed in passing — file those as separate PR-N records.}}
- {{The fix itself — that is authorized and tracked in the Change Request, see §5–§6.}}
- {{Broader remediation / release planning — tracked elsewhere.}}

Split note: {{If reproduction revealed more than one distinct problem, list the PR-N records this was split into, e.g. "split into PR-{{SYSTEM-ID}}-002 and PR-{{SYSTEM-ID}}-003."}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Keep this short for a record document — define only the terms a reader of THIS report needs. Do not redefine the whole glossary; link the project glossary and define only what is load-bearing here. Three words beginners constantly muddle are worth pinning down: a **failure** is the symptom you observed (the system crashed); a **defect** (a.k.a. fault/bug) is the flaw in the artifact that caused it (the off-by-one in the loop); an **error** is the human mistake that introduced the defect. A PR starts by recording the *failure*; analysis (§5) works back toward the *defect*.

| Term | Definition |
|---|---|
| PR | Problem Report — this record; one observed anomaly, tracked to closure. |
| CR | Change Request — the authorized work to fix a problem; lives in its own document. |
| Anomaly | Any observed deviation from expectation (IEEE 1044) — neutral word, broader than "bug." |
| Failure | The observed symptom (what happened). |
| Defect | The flaw in the artifact that caused the failure (fault / bug). |
| Severity | How bad the impact is *if it occurs* (see §4). |
| Priority | How soon we should *act* (see §4). |
| Disposition | The recorded decision about what to do with this PR (see §5). |
| {{Project-specific term}} | {{Definition — only if load-bearing here.}} |

Project glossary: {{path/to/glossary.md}} — refer here for terms not redefined above.

### 1.4 References

> The applicable project, organizational, regulatory, contractual, and standards references for THIS problem. Name the two companion standards and any SRS-N / SDD-N artifact this problem implicates — that cross-reference is what makes the anomaly traceable back to the requirement or design element it violates.

| Ref | Document |
|---|---|
| R1 | IEEE 1044-2009 — Standard Classification for Software Anomalies (anomaly class, §4). |
| R2 | ISO/IEC/IEEE 14764:2022 — Software Maintenance (maintenance category + disposition flow, §5). |
| R3 | {{SRS-{{SYSTEM-ID}}-NNN}} — requirement this problem implicates, if any (see §2 Expected behavior). |
| R4 | {{SDD-{{MODULE-ID}}-NNN}} — design element this problem implicates, if any (see §5 Affected components). |
| R5 | {{CR-{{SYSTEM-ID}}-NNN}} — Change Request spawned to fix this, if disposition is Correct. |
| R6 | {{path/to/project/doc.md}} — {{other applicable project / contractual / regulatory reference.}} |

---

## 2. Problem Description

> The heart of the record. Write three things, plainly and separately — and resist the urge to guess the cause here (that belongs in §5). A problem is a *gap* between observed and expected; if you cannot state the expectation, you cannot yet call it a problem. Watch for the two beginner failure modes: (1) writing only the symptom with no expectation ("it's broken"), and (2) writing a proposed solution instead of a description ("we need to add a null check") — the fix belongs in §6, not here.

### 2.1 Observed behavior

> What actually happened, in concrete terms. Quote exact error text; attach screenshots/logs by reference. This is the *failure* (the symptom), not the defect.

{{Describe exactly what happened. Quote the exact error message, status code, or output. Reference attached logs/screenshots by name or link, e.g. "see log-2026-XX-XX.txt, lines 412-440." Concrete and verbatim beats paraphrase.}}

### 2.2 Expected behavior

> What should have happened, and ideally why you believe that — cite the SRS-N requirement or SDD-N design element it violates if known. Without a stated expectation there is no gap, and no problem to act on.

{{Describe what should have happened. If a documented requirement or design element defines the expectation, cite it: "violates SRS-{{SYSTEM-ID}}-NNN" or "contradicts SDD-{{MODULE-ID}}-NNN." If the expectation is "obvious" / undocumented, state your reasoning so a reviewer can agree or push back.}}

### 2.3 Impact

> Who/what is affected and how badly — user impact, business impact, and any safety or security impact. This feeds Severity in §4.

| Dimension | Impact |
|---|---|
| User impact | {{Who is affected and how — e.g. "all users on save; data appears lost."}} |
| Business impact | {{Cost, reputation, SLA, blocked release, etc.}} |
| Safety impact | {{None / describe — physical or operational harm if any.}} |
| Security impact | {{None / describe — data exposure, auth bypass, etc. If any, flag in §4.}} |

---

## 3. Reproduction Information

> How to make the problem happen again — the recipe. The more precise this is, the cheaper the fix; good repro steps are the single most useful thing a reporter can provide. **Reproduction** means the exact recipe (steps, data, configuration, environment) that makes the problem happen. If the problem cannot be reproduced, say so explicitly and record what was tried — that is genuine, useful content and supports a "Cannot Reproduce" disposition in §5, not an empty section.

### 3.1 Steps

> Numbered, minimal, from a known starting state. "Minimal" matters: strip steps that do not affect the outcome so the true trigger is visible.

From starting state: {{e.g. "fresh install, default config, logged in as a standard user."}}

1. {{Step 1}}
2. {{Step 2}}
3. {{Step 3 — the action that triggers the failure}}
4. {{Observed result at this point: <quote what you see>}}

### 3.2 Test data / inputs

> Exact values or a reference to the data set used. Redact secrets and PII.

{{Exact input values, or a reference to the data set / fixture used. Redact secrets/PII — replace with placeholders and note "redacted."}}

### 3.3 Configuration & environment

> Anything that differs from default and might matter. This can repeat the front-matter Environment row if the repro needs a tighter spec.

{{OS / runtime versions, feature flags, config overrides, dependent service versions — anything non-default that could affect the outcome.}}

### 3.4 Frequency / conditions

> Always, intermittently, only under load, only after step X. Note the observed hit rate.

{{e.g. "Reproduces 3 of 10 attempts; only when the cache is cold; always under concurrent load." If you could NOT reproduce it, state that here and list what you tried — this supports a "Cannot Reproduce" disposition in §5.}}

---

## 4. Severity and Priority

> Record the two axes separately — they are NOT the same thing, and collapsing them is the single most common beginner error. **Severity** = how bad the impact is *if it happens* (data loss is high-severity). **Priority** = how soon we should *act* (a high-severity bug that almost never triggers may still be low-priority). Record both; never let one stand in for the other. Per IEEE 1044, also tag the **anomaly class** and note any safety/security dimension explicitly: security-affecting reports must be flagged here even if low-frequency, and never deferred silently.

| Axis | Value | One-line justification |
|---|---|---|
| Severity | {{Critical / Major / Moderate / Minor}} | {{Why — driven by §2.3 impact: data loss, safety, security, unrecoverable states push severity up regardless of how rare.}} |
| Priority | {{Urgent / High / Medium / Low}} | {{Why — driven by severity AND frequency (§3.4) AND business context. A rare high-severity bug can be lower priority than a constant moderate annoyance.}} |
| Anomaly class | {{Functional / Performance / Security / Usability / Data / Documentation}} | {{Per IEEE 1044.}} |
| Safety / security flag | {{None / Safety-affecting / Security-affecting}} | {{If security-affecting, do not defer silently — escalate per project policy.}} |

---

## 5. Analysis and Disposition

> This is where you may finally reason about CAUSE, having kept it out of the description (§2). Analysis leads directly to a decision; for a lean record they belong together. A **disposition** is the recorded decision about what to DO with the report. Record exactly one, with a one-line rationale and a date. Tag which of the four **maintenance categories** (ISO/IEC/IEEE 14764) the PR falls under — *corrective* (fix a defect), *adaptive* (keep working as the environment changes), *perfective* (improve performance/maintainability), *preventive* (fix latent problems before they bite) — because that tag often reveals whether the PR is truly a defect or really an enhancement in disguise. An undispositioned PR is an open liability; every PR ends with a recorded decision.

### 5.1 Analysis

> Reason toward the *defect* (the flaw), distinguished from the *failure* (the symptom) recorded in §2. Mark the cause as a hypothesis until verified.

| Item | Finding |
|---|---|
| Suspected cause | {{Working hypothesis for the defect. Mark "(hypothesis — unverified)" until confirmed.}} |
| Affected components | {{Modules/files implicated; cross-reference SDD-{{MODULE-ID}}-NNN where possible.}} |
| Related changes | {{Recent commits, deployments, or config changes that correlate — check the environment / what-changed before deep source reading.}} |
| Workaround | {{Any interim mitigation, even if ugly, so affected users have an off-ramp before the fix lands. "None known" is a valid answer.}} |

### 5.2 Disposition

> Record exactly one decision, with rationale and date.

| Field | Value |
|---|---|
| Disposition | {{Correct / Defer / Duplicate / Cannot Reproduce / Not a Problem / Enhancement}} |
| Rationale | {{One line: why this decision.}} |
| Maintenance category | {{Corrective / Adaptive / Perfective / Preventive — per ISO/IEC/IEEE 14764.}} |
| Date | {{YYYY-MM-DD}} |
| Carrying CR | {{If Correct: CR-{{SYSTEM-ID}}-NNN — the authorized fix. The PR records the problem; the CR records the work.}} |
| Canonical PR | {{If Duplicate: PR-{{SYSTEM-ID}}-NNN — the original this duplicates.}} |

---

## 6. Corrective Action and Verification

> Only relevant when the disposition is **Correct** (or an accepted **Enhancement**); for other dispositions this whole section is a single line: "N/A — see §5 disposition." This is the closing-the-loop section, and a fix is not done until it is verified. A fix declared done without re-running the reporter's actual reproduction is the classic declared-done-without-testing failure — the verification step exists specifically to catch that.

{{N/A — see §5 disposition.}} *(Delete this line and fill in §6.1–§6.2 only if disposition is Correct or an accepted Enhancement.)*

### 6.1 Corrective action

> What change was made and who is making it. The detail lives in the CR-N and the commit/PR it references; summarize here.

| Item | Value |
|---|---|
| Approved modification | {{Summary of the change. Detail lives in CR-{{SYSTEM-ID}}-NNN and its commit/PR.}} |
| Owner | {{Who is making the change.}} |
| Schedule / target | {{Target build, release, or date.}} |

### 6.2 Verification

> This is what actually closes the PR. Re-run the original reproduction; confirm neighbours still work; record where the fix shipped and who verified. Without closure evidence the PR stays open.

| Item | Value |
|---|---|
| Retest | {{Re-ran the exact §3 repro steps. Result: <failure no longer occurs / still occurs>.}} |
| Regression test | {{Confirmed the fix did not break neighbours; name the tests run.}} |
| Closure evidence | {{Build/version where the fix shipped, the date, and who verified. e.g. "Verified in v1.4.3, {{YYYY-MM-DD}}, by {{Name / role}}."}} |

---

## 7. Status History

> The audit trail of the record itself — distinct from the §9 Revision History (which tracks edits to this DOCUMENT; this table tracks the lifecycle of the PROBLEM). Each row is one state transition of the problem, so a reader can reconstruct how it moved from Open to Closed and who moved it. Status values follow the anomaly lifecycle implied by IEEE 1044 / 14764: Open → Analyzing → Dispositioned → (In Progress → Verifying →) Closed, or Open → Closed with a terminal disposition (Cannot Reproduce / Not a Problem / Duplicate). If the project has a ticketing system, this table can simply mirror the key transitions and link out — it is the lean substitute for a tracker, not a replacement.

| Date | Status | Owner | Notes |
|---|---|---|---|
| {{YYYY-MM-DD}} | Open | {{Reporter}} | Filed. |
| {{YYYY-MM-DD}} | Analyzing | {{Owner}} | {{e.g. began reproduction / root-cause analysis.}} |
| {{YYYY-MM-DD}} | Dispositioned | {{Owner}} | {{Disposition recorded, see §5.}} |
| {{YYYY-MM-DD}} | Verifying | {{Owner}} | {{Fix landed; retest in progress.}} |
| {{YYYY-MM-DD}} | Closed | {{Owner}} | {{Closure evidence recorded, see §6.2.}} |

---

## 8. Open Questions

> Short, optional — anything unresolved that blocks dispositioning or verifying THIS PR. A place to park "we don't know yet" honestly rather than guessing. Use PR-OQ-N for traceability. Each item: the question + what's blocking resolution + who needs to provide the answer. Resolve and remove as the PR progresses; an empty section means the record is complete.

- **PR-OQ-1**: {{Question — e.g. "missing log range from reporter."}} — {{what's blocking; who needs to provide the answer.}}
- **PR-OQ-2**: {{Question — e.g. "could not access the production environment to reproduce."}} — {{blocker; owner of the answer.}}

---

## 9. Revision History

> Standard house-style last section. This tracks changes to THIS DOCUMENT — not the problem's lifecycle, which lives in §7 Status History; do not duplicate them. For a record document, revisions are typically lightweight; the substantive history of the PROBLEM is §7. Bump the version on any material edit to the recorded facts (e.g. severity re-rated, disposition changed).

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial report filed |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Problem Description (observed, expected, impact — all three)
- §3 Reproduction Information (even if the answer is "cannot reproduce, here's what was tried")
- §4 Severity and Priority (both axes, separately)
- §5 Analysis and Disposition (a PR is not done until it has a recorded disposition)
- §7 Status History
- §9 Revision History

**Optional sections** (include if relevant):
- §6 Corrective Action and Verification — collapses to "N/A — see §5 disposition" for any disposition other than Correct / accepted Enhancement.
- §8 Open Questions — track elsewhere if you prefer; an empty section means the record is complete.

**Tailoring**:
- This is a record/instance document. Keep it lean: one PR per file, and do not pad with sections that do not apply to the specific problem. A "Cannot Reproduce" PR legitimately ends with §3 documenting the attempts, §5 recording the disposition, and §6 reading "N/A."
- **Solo developer / small team:** the front-matter metadata table carries the headline facts (severity, priority, disposition) and may be the bulk of a small PR. Sign-off rows collapse — one person is Reporter, Prepared by, Reviewed by, and Approved by; just name yourself in each, or delete the rows you genuinely don't use. §7 Status History can be two rows (Open → Closed). If you already use an issue tracker, let the tracker hold the lifecycle and use this file only when a problem needs more narrative than a ticket comfortably holds, linking the two.
- Keep observed/expected/cause strictly separated (§2 vs §5). The discipline of not guessing the cause in the description is what makes the analysis honest.
- Always record both Severity and Priority. They are different axes; never let one stand in for the other.

**Traceability ID conventions:**
- PR-N: this problem report (one per file). Front-matter PR ID is `PR-{{SYSTEM-ID}}-001`.
- CR-N: the Change Request that carries the authorized fix (cross-referenced when disposition is Correct).
- SRS-N / SDD-N: the requirement or design element this problem implicates (cross-referenced in §2.2 and §5.1 so the anomaly is traceable back to the artifact).
- PR-OQ-N: open questions on this PR (§8).

**For regulated/safety-critical projects:** use the full IEEE 1044-2009 and ISO/IEC/IEEE 14764:2022 standards, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
