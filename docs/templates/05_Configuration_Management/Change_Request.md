# Change Request Template

> **Template purpose:** Lightweight Change Request (CR) record structure inspired by IEEE 828-2012 (configuration management) and the configuration management process of ISO/IEC/IEEE 12207:2017. Use this template when you need to formally propose, evaluate, decide, and close *one* change to something already under version control. Replace `{{placeholder}}` content with the specifics of the change. Section guidance (in blockquotes) can be deleted once the section is filled in. This is an *instance* document: you fill out one copy per proposed change, not a reusable spec.
>
> **When to use:** Whenever a project tracks artifacts under configuration management and a change to a frozen, agreed reference point is being proposed — a defect fix, an enhancement, a requirement change, a maintenance task, a compliance-driven edit. The Change Request is the single record that carries that one change from "someone wants to do this" through "the authority decided" to "it was done and verified." It pairs with the Configuration Management Plan (SCMP), which defines *the process*; this CR is one trip *through* that process.
>
> **Companion standard:** IEEE 828-2012 — Standard for Configuration Management in Systems and Software Engineering; and ISO/IEC/IEEE 12207:2017 — Systems and software engineering — Software life cycle processes (configuration management process).
>
> **Status of this template:** A lightweight skeleton derived from public sources, aligned to IEEE 828-2012 (configuration management) and the configuration management process of ISO/IEC/IEEE 12207:2017. Both are paywalled IEEE/ISO standards; this template paraphrases their section structure and reproduces no normative text from either. Verify the section set and any normative requirements against the full standards for regulated, safety-critical, or contractual contexts. This is an instance/record document: kept deliberately lean (no padding) — fewer focused sections is the correct shape for a change-request log entry, not a defect.

---

# Change Request (configuration management instance/record document) — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | CHG-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 828-2012 + ISO/IEC/IEEE 12207:2017 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Change Request ID | CHG-{{NNN}} |
| Type | Defect fix / Enhancement / Requirement change / Maintenance / Compliance / Operational |
| Priority | Critical / High / Medium / Low |
| Affected Baseline | {{baseline name or ID}} |
| Affected Configuration Items | {{CI-N, CI-N, ...}} |
| Disposition | Open / Approved / Rejected / Deferred / Implemented / Closed |

---

## 1. Introduction

> A Change Request (CR) is a *single, formal record that proposes one change* to something already under configuration management. Unlike a specification (which you write once and keep), this is an instance document — you fill out one CR per proposed change. This section fits the change into context and defines the vocabulary, so a reader who is new to configuration-management practice can follow the rest of the record. Keep it short: a CR is a record, not a spec.

### 1.1 Purpose

> One sentence. State that this document is a single change request, under configuration management, proposing one change to a controlled baseline for review by the change authority.

{{This document is a single Change Request for {{Project Name}}. It proposes one change — identified as CHG-{{NNN}} — to a controlled baseline, and records that change from submission through the authority's decision to verification and closure. It does not itself authorize work; §7 (Decision) does.}}

### 1.2 Scope

> Say what this CR covers (the one proposed change) and what it does NOT. A CR is not the implementation, and filling it out does not by itself authorize any work — the Decision section is what authorizes (or stops) the work.

In scope:
- {{The one proposed change, summarized in a phrase — e.g. "make {{behavior X}} happen instead of {{behavior Y}}".}}

Out of scope:
- The implementation itself — this record *describes and decides* the change; the work is tracked against §8 once approved.
- Authorization of work — no work begins on the strength of this record alone; §7 (Decision) is the authorizing act.
- {{Any related-but-separate change you might be tempted to fold in.}}

> **One change request = one proposed change.** If you have two unrelated changes, open two CRs (CHG-{{NNN}} and CHG-{{NNN+1}}). Bundling unrelated changes into one record makes the decision harder and the audit trail murkier. When in doubt, split.

### 1.3 Definitions, Acronyms, and Abbreviations

> A small table. Don't assume the reader already knows configuration-management vocabulary — these terms are pre-seeded because the rest of the record relies on them.

| Term | Definition |
|---|---|
| Change Request (CR) | A formal, single record proposing one change to something already under configuration control. This document is one CR. |
| Configuration Item (CI) | Any artifact placed under formal control (a requirement, a design doc, a source file, a build, a config). Changes are described in terms of which CIs they touch, traced as CI-N. |
| Baseline | A named, frozen snapshot of one or more CIs agreed at a point in time (e.g. "Release 1.0 baseline"). A CR proposes to move the system off an agreed baseline — which is why it needs review before it happens. |
| Change Control Board (CCB) | The person or group with authority to approve, reject, or defer a change. On a solo/small-team project the CCB may be one person, but the role still exists and §7.2 records who exercised it. |
| Disposition | The formal outcome assigned to a CR — Open / Approved / Rejected / Deferred / Implemented / Closed (and, as a recommendation/decision value, *Request More Information*). The header field tracks the current disposition. |
| {{Other term}} | {{Definition}} |

### 1.4 References

> List the affected baseline, any upstream requirement / ADR / defect IDs, the project's Configuration Management Plan, and the companion standards. One line each: a path or ID and a short note.

| Ref | Document / ID |
|---|---|
| R1 | {{Affected baseline name or ID}} — the controlled snapshot this change proposes to move off. |
| R2 | REQ-{{N}} / ADR-{{N}} / DEF-{{N}} — {{upstream requirement, decision, or defect that drives or is touched by this change}}. |
| R3 | `docs/.../Software_Configuration_Management_Plan.md` (SCMP-{{PROJECT-ID}}-001) — the CM process this CR runs through. |
| R4 | IEEE 828-2012 — Standard for Configuration Management in Systems and Software Engineering. |
| R5 | ISO/IEC/IEEE 12207:2017 — Software life cycle processes (configuration management process). |

---

## 2. Identification

> This table is the record's primary key — the anchor that everything downstream quotes when it refers to this change. Several of these fields also appear in the front-matter metadata header; that repetition is intentional for a record. The metadata block is the at-a-glance header; this section is the authoritative source.

| Field | Value |
|---|---|
| Change Request ID | CHG-{{NNN}} |
| Submitter | {{Name / role}} |
| Date submitted | {{YYYY-MM-DD}} |
| Type | {{Defect fix / Enhancement / Requirement change / Maintenance / Compliance / Operational}} |
| Priority | {{Critical / High / Medium / Low}} |
| Affected Baseline | {{baseline name or ID}} |
| Affected Configuration Items | {{CI-N, CI-N, ...}} |

> The **Change Request ID (CHG-{{NNN}})** is what every other part of the project will quote when it refers to this change. Assign it once and never reuse it — even if this CR is rejected, its number stays retired so the audit trail is unambiguous.
>
> **Affected Configuration Items** should list **CI-N identifiers**, not loose prose ("the login screen"). Naming CI-N items is what lets the change be traced to exactly what it touches, and it ties this section to the per-dimension list in §5 (Impact Analysis). If an artifact is affected but not yet under control as a CI, that itself is worth noting in §10 (Open Questions).

---

## 3. Change Description

> Describe *what* should change — plainly and concretely. State the current behavior or state and the proposed behavior or state, side by side if that helps. Describe the change itself: not *why* you want it (that is §4) and not *how* you will do it (that is §8). Avoid solution-bias — say what must be true *after* the change, not necessarily the mechanism. The test of this section: someone who is not you should be able to read it and understand exactly what is being asked for.

**Current state / behavior:**
{{What is true today, on the affected baseline — the thing the change would move away from.}}

**Proposed state / behavior:**
{{What should be true after the change — the condition that defines success, stated without committing to a particular mechanism.}}

| Aspect | Current | Proposed |
|---|---|---|
| {{Aspect 1}} | {{current}} | {{proposed}} |
| {{Aspect 2}} | {{current}} | {{proposed}} |

---

## 4. Reason for Change

> Give the driver behind the request — the justification the change authority will weigh against the cost surfaced in §5. Tie it to the **Type** field from §2. The reason answers "why is this worth moving off an agreed baseline?" One change usually has one dominant driver; name the category and give a sentence of substance for each that applies.

**Primary driver (matches Type in §2):** {{Defect / Enhancement / Requirement change / Risk reduction / Compliance / Maintenance / Operational need}}

| Category | Applies? | Substance / linked ID |
|---|---|---|
| Defect | {{yes/no}} | {{If yes, reference the defect — e.g. DEF-{{N}} — and what it causes.}} |
| Enhancement | {{yes/no}} | {{If yes, what capability or improvement this adds.}} |
| Requirement change | {{yes/no}} | {{If yes, reference REQ-{{N}} and how the requirement changed.}} |
| Risk reduction | {{yes/no}} | {{If yes, the risk being reduced.}} |
| Compliance | {{yes/no}} | {{If yes, name the obligation or standard driving it.}} |
| Maintenance | {{yes/no}} | {{If yes, the upkeep/technical-debt reason.}} |
| Operational need | {{yes/no}} | {{If yes, the operational pressure driving it.}} |

---

## 5. Impact Analysis

> This is the heart of a change request. Its purpose is to make the *real* cost and reach of the change visible **before** anyone commits to it — surprises discovered *after* approval are the failure mode this section exists to prevent. Work through each dimension the change could ripple into. List the affected **CI-N** items explicitly: this is the traceability link back to §2. Important: "no impact" on a dimension is a valid and useful answer — *record* it rather than leaving it blank, so the reader knows it was considered, not forgotten.

| Dimension | Affected? | What specifically (name CI-N) | Estimated effort / risk |
|---|---|---|---|
| Requirements | {{yes/no}} | {{Which REQ-N / CI-N requirements change or are touched}} | {{e.g. low — one clause reworded}} |
| Design | {{yes/no}} | {{Which design CI-N items are affected}} | {{...}} |
| Code | {{yes/no}} | {{Which source CI-N items are modified}} | {{...}} |
| Tests | {{yes/no}} | {{Which test CI-N items need updating or adding}} | {{...}} |
| Data | {{yes/no}} | {{Migrations, schema changes, data backfills}} | {{...}} |
| Documentation | {{yes/no}} | {{Which docs/CI-N need revising}} | {{...}} |
| Cost | {{yes/no}} | {{Direct cost — licenses, services, time}} | {{...}} |
| Schedule | {{yes/no}} | {{Effect on milestones / release dates}} | {{...}} |
| Risk | {{yes/no}} | {{New or changed risks introduced}} | {{...}} |
| Quality | {{yes/no}} | {{Effect on reliability, performance, maintainability}} | {{...}} |
| Operations | {{yes/no}} | {{Deployment, monitoring, runbook impact}} | {{...}} |
| Users | {{yes/no}} | {{Who is affected and how; training/comms needed}} | {{...}} |

**Summary of reach:** {{One or two sentences pulling the table together — the headline cost and the widest ripple. This is what the authority reads first.}}

---

## 6. Alternatives and Consequences of No Change

> The change authority cannot make a good decision without knowing the *options* and the *cost of inaction*. List other ways to achieve the same reason-for-change (§4), each with a brief trade-off. Then state plainly what happens if the change is **not** made — the "do nothing" baseline. Do-nothing is always an option and should be evaluated as one. Keep this lean: a short list, not an essay.

**Alternatives considered:**

| # | Alternative | Trade-off |
|---|---|---|
| A1 | {{Proposed change (this CR)}} | {{Why it is the recommended path}} |
| A2 | {{Another way to satisfy §4}} | {{Cost / benefit / why not chosen}} |
| A3 | {{Another option}} | {{...}} |

**Consequences of no change (the do-nothing option):**
{{What happens if the request is rejected or deferred indefinitely — the defect persists, the requirement stays unmet, the compliance gap remains open, the risk continues to accrue. Be concrete: this is the cost the authority weighs against the cost in §5.}}

---

## 7. Recommendation and Decision

> This is the change-control pivot of the record. The **Recommendation** is advisory — the proposer's suggested outcome. The **Decision** is binding — it is what actually authorizes (or stops) the work, and entering it should update the **Disposition** field in the metadata header. Both live under one heading to keep an instance document lean.

### 7.1 Recommendation

> The proposer's suggested disposition, with a one-line rationale.

- **Recommended disposition:** {{Approve / Reject / Defer / Request More Information}}
- **Rationale:** {{One line — why this disposition follows from §4, §5, and §6.}}

### 7.2 Decision

> The binding outcome from the change authority. On a solo project the CCB may be the same person who submitted the CR — that is fine, but the role is still recorded, so there is an audit trail of *who* authorized the change and *when*.

| Field | Value |
|---|---|
| Decision authority (CCB) | {{Name / role of the person or group exercising change-control authority}} |
| Decision date | {{YYYY-MM-DD}} |
| Disposition | {{Approved / Rejected / Deferred / Request More Information}} |
| Rationale | {{Why the authority decided this way}} |
| Conditions (if approved) | {{Any conditions attached — e.g. "approved provided rollback is tested first"; "none"}} |

> On entering the Decision: update the **Disposition** row in the front-matter metadata table to match, and log the decision as a row in §11 (Revision History).

---

## 8. Implementation Plan

> Fill this in **only once the Decision is Approve.** For a Rejected or Deferred CR this section correctly stays empty. Keep it a brief, actionable plan — not a full project schedule. The **rollback plan is required, not optional**: name *how to undo this* **before** implementing, not after something breaks. "How do we undo this" is part of controlling the change.

| Field | Value |
|---|---|
| Assigned owner | {{Name / role responsible for carrying out the change}} |
| CI-N items to be modified | {{CI-N, CI-N, ... — the actual artifacts that will change}} |
| Work tasks | {{Short list of the steps to make the change}} |
| Target schedule | {{Start / target completion — milestone or date}} |
| Verification approach | {{How the change will be checked once made — points to §9}} |
| **Rollback plan (required)** | {{The pre-agreed way to undo this change if it goes wrong — e.g. "revert commit {{hash}}; restore baseline {{name}}; re-run smoke test {{TEST-N}}."}} |

---

## 9. Verification and Closure

> Fill this in **after implementation.** A change request is not "done" when the code is written — it is done when the change has been *verified to do what it claimed* **and** the controlled items and baseline reflect it. Closing the CR updates the Disposition to **Closed** and is the last formal act on the record.

| Field | Value |
|---|---|
| Verification evidence | {{What was checked, by whom, the result — e.g. TEST-{{N}} passed; review notes; links to runs}} |
| Affected CIs updated under control? | {{yes/no — confirm the CI-N items now reflect the change in version control}} |
| Baseline updated? | {{yes/no — confirm the affected baseline now reflects the change, or note the new baseline name/ID}} |
| Closed by | {{Name / role}} |
| Closure date | {{YYYY-MM-DD}} |

> On closure: update the **Disposition** row in the metadata table to **Closed**, and add a Revision History row recording the closure.

---

## 10. Open Questions

> The honest "what we still do not know" list — unresolved items blocking a clean decision or closure. For a CR, these are things like an impact dimension not yet estimated (§5), a dependency not yet confirmed, or an approval pending from someone external. Track each with what is blocking it and who needs to resolve it. Resolve and remove as the CR progresses. An open question still standing at closure is a signal the CR should **not** yet be closed.

- **OQ-1**: {{Question}} — {{what's blocking, who needs to resolve}}
- **OQ-2**: {{Question}} — {{what's blocking, who needs to resolve}}
- ...

---

## 11. Revision History

> Every substantive edit to this record gets a row — re-scoping the change, a new impact estimate, the decision being entered, closure. For a record document, this doubles as the audit trail of how the request evolved from submission to closure.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Identification
- §3 Change Description
- §4 Reason for Change
- §5 Impact Analysis
- §7 Recommendation and Decision
- §11 Revision History

**Optional sections** (fill in when the stage is reached):
- §6 Alternatives and Consequences of No Change (always worth a few lines; collapse to just the "do nothing" consequence if there are genuinely no alternatives)
- §8 Implementation Plan (stays empty until the Decision is Approve — empty is correct for a Rejected/Deferred CR)
- §9 Verification and Closure (filled in after implementation; empty until then)
- §10 Open Questions (track elsewhere if you prefer; resolve before closing)

**Identifier conventions**:
- CHG-N: the change request itself — one record is one CHG-N (e.g. CHG-001). Assign once, never reuse.
- CI-N: configuration items the change affects (named in §2 and §5).
- REQ-N / ADR-N / DEF-N: upstream requirements, decisions, or defects referenced in §4 and §5.
- OQ-N: open questions (§10).
- Affected baseline is referenced by its name/ID, not a numbered prefix.

These prefixes let a change be traced across documents — the CIs and requirements named here line up with the Configuration Management Plan, the SRS, and the design docs.

**Tailoring**:
- A change request is an *instance* record. Fill one out per proposed change; don't try to make it reusable.
- The record fills in over time, not all at once: §1–§7 at submission and decision, §8 after approval, §9 after implementation. A CR sitting at "Approved" with §8 and §9 blank is normal and correct.
- **Solo developer / small team:** the Change Control Board may be one person — often the same person who submitted the CR. That is fine. Keep §7.2 anyway: recording *who* decided and *when* is the audit trail, and future-you is a different reader than today-you. You can keep CRs as short markdown files in the repo (one file per CHG-N) rather than in a ticket system.
- If a dimension in §5 truly does not apply, write "no impact" — never leave it blank. The whole point of impact analysis is making considered-and-cleared visible.
- This template is deliberately lean. For a single change-request log entry, fewer focused sections is the correct shape, not a shortcoming.

**For regulated/safety-critical projects:** use the full IEEE 828-2012 and ISO/IEC/IEEE 12207:2017 configuration management process, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
