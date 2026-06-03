# Verification and Validation Plan Template

> **Template purpose:** Lightweight Verification and Validation (V&V) Plan structure inspired by IEEE 1012-2016. Use this template when planning how you will check that a project is being built right (verification) and that it is the right thing to build (validation). Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once you know what the system must do (you have an SRS or at least a clear requirements list) and you want a single plan for how you will check the work as it proceeds — not just at the end. The V&V Plan sits beside the SRS (WHAT) and SDD (HOW) and answers "how do we know it's correct, at every stage."
>
> **Companion standard:** IEEE 1012-2016 — IEEE Standard for System, Software, and Hardware Verification and Validation.
>
> **Status of this template:** Lightweight derivation inspired by the structure of IEEE 1012-2016, reduced for solo/small-team use. It paraphrases the standard's organizing ideas (V&V activities by lifecycle phase, integrity levels, independence) without reproducing its normative text. Verify against the full standard for the criticality-level details (integrity-level task tables, required independence) that apply to safety- or mission-critical systems.

---

# Verification and Validation Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | VVP-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 1012-2016 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Integrity / criticality level | {{e.g., Low / Medium / High — see §2.2}} |
| Degree of independence | {{Self / Peer / Independent (IV&V) — see §2.3}} |
| Related documents | {{SRS-{{PROJECT-ID}}-001, SDD-{{MODULE-ID}}-001, ...}} |

---

## 1. Introduction

### 1.1 Purpose

> One-paragraph statement of what this document is for. It should establish that this plan describes how the project will be verified and validated across its lifecycle — not how the system is built (that's the SDD) or what it must do (that's the SRS).

{{This document describes how {{Project Name}} will be verified and validated. It identifies the V&V activities to be performed at each lifecycle phase, the methods and pass/fail criteria for each, how anomalies are reported, and who is responsible. It is the single plan of record for answering "how do we know the work is correct."}}

### 1.2 Scope

> Define what this V&V Plan covers and what it does not. Note which components, releases, or phases are in scope. If V&V is being scaled to an integrity level, say so here and point to §2.2.

In scope:
- {{Component / subsystem / release in scope}}
- {{...}}

Out of scope:
- {{Component or activity explicitly not covered}} — {{reason}}
- {{...}}

### 1.3 Definitions and Acronyms

> Define the key terms so a reader new to formal V&V is not lost. The two most important are below — keep them, tailor the rest. **Verification** = "are we building the product *right*?" — does each work product meet the specification it was built against at that stage (e.g., does the design satisfy the requirements; does the code satisfy the design). **Validation** = "are we building the *right* product?" — does the finished system actually meet the real user need it was meant to serve. The two are different checks: you can build something perfectly to spec (verified) and still have the wrong spec (not validated).

| Term | Definition |
|---|---|
| Verification | Checking that a work product meets the specification it was built against at that stage ("building the product right"). |
| Validation | Checking that the system meets the actual user need ("building the right product"). |
| V&V activity | A grouped body of V&V work tied to a lifecycle phase (e.g., requirements V&V). Numbered VV-N in this plan. |
| Anomaly | Any observed deviation from expectation — a defect, ambiguity, missing requirement, or failed check — recorded for disposition. |
| Integrity / criticality level | A rating of how much harm a failure could cause; drives how much V&V rigour is applied (see §2.2). |
| IV&V | Independent Verification and Validation — V&V performed by someone organizationally separate from the developers (see §2.3). |
| {{Term}} | {{Definition}} |

### 1.4 References

> List the documents this plan depends on: the requirements it validates against, the design it verifies, and any external standards.

Foundational documents:
- {{path/to/SRS.md}} — requirements being validated
- {{path/to/SDD.md}} — design being verified
- {{path/to/test-plan.md}} — {{if test planning lives in a separate doc}}

Architecture Decision Records:
- ADR-NNNN — {{decision relevant to V&V}}

External standards:
- IEEE 1012-2016 — System, Software, and Hardware Verification and Validation (companion standard)
- {{Other applicable standard with version}} — {{relevance}}

---

## 2. V&V Overview

### 2.1 Objectives

> State, in plain terms, what this V&V effort is trying to achieve. Tie each objective back to verification (build it right) or validation (build the right thing). Keep it short — three to six objectives.

- {{Confirm every requirement in the SRS is testable and traced to at least one V&V activity (verification).}}
- {{Confirm the delivered system satisfies the user need described in §X of the SRS (validation).}}
- {{Detect defects and ambiguities as early as the phase that introduced them, not at final test.}}
- {{...}}

### 2.2 Integrity / Criticality Level

> **For a beginner:** the *integrity level* (some standards call it *criticality level*) is a rating of how much harm a failure of the system could cause — to people, money, data, reputation, or mission. The higher the level, the more V&V rigour the standard expects: more activities, stricter criteria, and more independence (§2.3). A throwaway internal script is low integrity; software that controls a vehicle or handles money is high. You do not need a formal scheme to start — pick a level, say why, and let it set how heavy this plan should be.

- **Assigned level:** {{Low / Medium / High — or your own scale}}
- **Rationale:** {{What could go wrong if this system fails, and how bad it would be. This is what justifies the level.}}
- **What this level implies for V&V effort:** {{e.g., "Low: peer review of requirements and code, automated tests on core paths, no formal independence." / "High: independent review, full requirement-to-test traceability, anomaly disposition tracked formally."}}

### 2.3 Degree of Independence

> **For a beginner:** *independence* means the person checking the work is not the same person who built it. The idea behind **IV&V (Independent V&V)** is that the author of a work product is the worst-placed person to spot their own blind spots, so a separate reviewer catches more. Independence runs on a spectrum: **self-review** (you check your own work — better than nothing, weakest), **peer review** (a teammate checks it — practical for small teams), and **independent** (someone outside the development effort, organizationally and/or financially separate — what high-integrity systems require). Solo and small-team projects usually land at self or peer; name honestly where you are.

- **Degree adopted:** {{Self / Peer / Independent (IV&V)}}
- **Rationale:** {{Why this degree fits the integrity level and the team size.}}
- **Where independence is strongest / weakest:** {{e.g., "Requirements get peer review; code is self-reviewed only — a known gap, accepted for now."}}

---

## 3. V&V Scope

> Make the verify-vs-validate split concrete for *this* project. Verification items are checks against an internal specification (requirements, design, code, interfaces). Validation items are checks against the real-world need. The same artifact can appear in both — e.g., a feature is verified against its spec and validated against the user goal it serves.

### 3.1 What gets verified

> List the work products checked against their specifications, and against what.

| Work product | Verified against | Phase |
|---|---|---|
| {{Requirements}} | {{Stakeholder needs / completeness & consistency rules}} | {{Requirements}} |
| {{Design}} | {{Requirements (SRS)}} | {{Design}} |
| {{Code / module}} | {{Design (SDD)}} | {{Implementation}} |
| {{...}} | {{...}} | {{...}} |

### 3.2 What gets validated

> List what is checked against the actual user need, and how the need is expressed (acceptance scenarios, user goals, success metrics).

| Validation item | User need / goal | How expressed |
|---|---|---|
| {{End-to-end workflow}} | {{The job the user is actually trying to do}} | {{Acceptance scenario / success metric}} |
| {{...}} | {{...}} | {{...}} |

### 3.3 In / out of scope

- **In scope:** {{components, integrations, releases covered}}
- **Out of scope:** {{explicitly excluded — with reason; e.g., "third-party library internals — we verify our usage, not their code"}}

---

## 4. V&V Activities by Lifecycle Phase

> This is the heart of the plan. Group V&V work by the lifecycle phase it belongs to, and number each activity VV-N so it can be referenced from §5 (methods/criteria), from anomaly reports, and from other documents. Not every project has every phase — delete phases you don't have, and remember that finding a defect in the phase that *created* it is far cheaper than finding it at final test. Tailor the depth of each phase to the integrity level from §2.2.

### 4.1 Requirements V&V

> Check that requirements are complete, consistent, unambiguous, and testable (verification), and that they actually reflect the user's need (validation). This is the highest-leverage phase — a bad requirement caught here costs a sentence; caught at test it costs a rebuild.

- **VV-1** {{Requirements review — check each requirement is atomic, testable, and traced to a stakeholder need.}}
- **VV-2** {{Requirements validation — confirm the set of requirements, taken together, satisfies the real user goal.}}
- {{...}}

### 4.2 Design V&V

> Check that the design satisfies the requirements (verification) and that no requirement is left unaddressed or contradicted.

- **VV-3** {{Design review against SRS — every requirement maps to a design element.}}
- **VV-4** {{Interface review — module interfaces are consistent with each other and with the design.}}
- {{...}}

### 4.3 Implementation V&V

> Check that the code satisfies the design (verification) — typically through code review, static analysis, and unit tests.

- **VV-5** {{Code review against SDD.}}
- **VV-6** {{Unit tests covering {{core paths / specified behavior}}.}}
- **VV-7** {{Static analysis / linting as applicable.}}
- {{...}}

### 4.4 Test V&V

> Verify the integrated system against its specifications, and validate it against the user need. This is where verification and validation visibly converge: integration/system tests verify the build; acceptance tests validate the product.

- **VV-8** {{Integration tests — components work together per the design.}}
- **VV-9** {{System tests — the system meets its specified behavior (verification).}}
- **VV-10** {{Acceptance tests / acceptance scenarios — the system meets the user need (validation).}}
- {{...}}

### 4.5 Operation and Maintenance V&V

> V&V does not stop at release. Verify that changes (fixes, features) don't break existing behavior, and re-validate that the system still meets the need as it and its environment evolve.

- **VV-11** {{Regression testing on each change.}}
- **VV-12** {{Re-validation when user needs or the operating environment change.}}
- {{...}}

---

## 5. V&V Tasks, Methods, and Criteria

> For each activity in §4, say *how* it will be done and *how you'll know it passed*. The four classic methods are below; most activities use one or two. The pass/fail criterion is what turns "we looked at it" into "it passed" — write it so a different person could apply it and reach the same verdict.
>
> - **Review** — a structured walkthrough of a work product by people, looking for problems (e.g., requirements review).
> - **Inspection** — a more formal, checklist-driven review with defined roles, aimed at finding defects (a heavier form of review).
> - **Analysis** — reasoning about a work product without executing it (static analysis, modelling, math/logic checks, traceability checks).
> - **Test** — executing the software with chosen inputs and comparing observed behavior to expected (unit, integration, system, acceptance).

| Activity | Method(s) | Inputs | Pass / fail criterion |
|---|---|---|---|
| VV-1 | {{Review}} | {{SRS draft}} | {{No untestable or duplicated requirements; every requirement traced to a need.}} |
| VV-5 | {{Review + Analysis}} | {{Code, SDD}} | {{No design-conformance defects open; static analysis clean of {{severity}} findings.}} |
| VV-9 | {{Test}} | {{System build, test cases}} | {{100% of {{specified}} test cases pass; no open {{severity}} anomalies.}} |
| VV-10 | {{Test (acceptance)}} | {{Acceptance scenarios}} | {{All acceptance scenarios pass; stakeholder sign-off recorded.}} |
| {{VV-N}} | {{...}} | {{...}} | {{...}} |

> **Traceability note:** keep a mapping from requirements (SRS IDs) → V&V activities (VV-N) → results, so you can answer "is every requirement actually checked?" A simple table or spreadsheet is enough at small scale.

---

## 6. Anomaly Reporting and V&V Reporting

> Two related things: how individual *anomalies* (problems found) are recorded and escalated, and what *reports* the V&V effort produces overall. Even a solo project benefits from a lightweight version — a defect you can't reproduce or remember is a defect that ships.

### 6.1 Anomaly handling

> Describe how a finding moves from "noticed" to "closed." At small scale this can be issues in your tracker; at high integrity it should be a defined, auditable flow.

- **Recording:** {{Where anomalies are logged — issue tracker, this doc's appendix, etc. — and the minimum fields: what, where found (which VV-N), severity, status.}}
- **Severity / classification:** {{e.g., Blocker / Major / Minor — and what each means for release.}}
- **Escalation:** {{When and to whom an anomaly is escalated; what severity blocks a release.}}
- **Disposition / closure:** {{What "closed" requires — fix verified, deferred-with-rationale, or won't-fix with sign-off.}}

### 6.2 V&V reports produced

> List the reports this V&V effort generates and when. Keep only what you'll actually use.

| Report | Produced when | Contents |
|---|---|---|
| {{Phase V&V summary}} | {{End of each phase}} | {{Activities run, anomalies found/open, pass/fail against §5 criteria}} |
| {{Traceability report}} | {{Before release}} | {{Requirements-to-V&V coverage; any unverified requirement flagged}} |
| {{Final V&V report}} | {{At release}} | {{Overall verdict, open anomalies and their disposition, sign-off}} |
| {{...}} | {{...}} | {{...}} |

---

## 7. Roles, Responsibilities, and Independence

> Who does which V&V activity, and at what degree of independence (§2.3). For a solo project, name yourself in each role and be honest about where independence is absent. For a small team, assign reviewers who are not the authors wherever the integrity level calls for it.

| Role | Responsibility | Independence |
|---|---|---|
| {{Author / Developer}} | {{Produces work products; runs self-review and unit tests}} | {{Self}} |
| {{Reviewer}} | {{Reviews requirements, design, code}} | {{Peer / Independent}} |
| {{V&V owner}} | {{Maintains this plan; tracks anomalies and coverage; produces reports}} | {{...}} |
| {{Stakeholder / User proxy}} | {{Defines the need; signs off acceptance (validation)}} | {{...}} |
| {{...}} | {{...}} | {{...}} |

> **Independence note:** {{State any place where the same person is both author and reviewer, and why that is acceptable at this integrity level. Naming the gap is part of the plan.}}

---

## 8. Schedule and Resources

> When V&V activities happen relative to the lifecycle, and what they need (people, tools, environments, time). Tie milestones to the phases in §4. Keep it realistic — V&V that isn't scheduled doesn't happen.

**Schedule:**

| Milestone | V&V activities | Target date |
|---|---|---|
| {{Requirements baseline}} | {{VV-1, VV-2}} | {{YYYY-MM-DD}} |
| {{Design baseline}} | {{VV-3, VV-4}} | {{YYYY-MM-DD}} |
| {{Code complete}} | {{VV-5..VV-7}} | {{YYYY-MM-DD}} |
| {{Release candidate}} | {{VV-8..VV-10}} | {{YYYY-MM-DD}} |
| {{...}} | {{...}} | {{...}} |

**Resources:**
- **People:** {{who, and how much of their time}}
- **Tools:** {{test frameworks, static analysis, CI, tracker}}
- **Environments:** {{test/staging environments needed}}
- **Time / budget:** {{rough allocation}}

---

## 9. Open Questions

> V&V planning decisions still unresolved. Distinguish load-bearing OQs (block the plan) from deferred-with-defaults (have a working default; revisit if it proves inadequate).

### 9.1 Load-bearing (block the plan)

- **OQ-1** {{Question}} — {{what's blocking, who needs to decide}}

### 9.2 Deferred with defaults

- **OQ-DEF-1** {{Question}} — *default: {{default}}.*
- {{...}}

---

## 10. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 V&V Overview (objectives, integrity level, independence)
- §4 V&V Activities by Lifecycle Phase
- §5 V&V Tasks, Methods, and Criteria
- §10 Revision History

**Optional sections** (include if relevant):
- §3 V&V Scope (fold into §1.2 if the project is small enough that the verify/validate split is obvious)
- §6 Anomaly Reporting (use a lightweight version even when solo; omit the formal report table for throwaway work)
- §7 Roles and Independence (collapse to a sentence for solo projects — but still name where independence is absent)
- §8 Schedule and Resources (omit if V&V tracks alongside the project schedule elsewhere)
- §9 Open Questions (track elsewhere if you prefer)

**Tailoring**:
- Scale everything to the integrity level (§2.2). Low integrity: a few reviews and tests, self/peer independence. High integrity: full traceability, independent review, formal anomaly disposition.
- Delete lifecycle phases in §4 you don't have. Add phases (e.g., installation, migration, retirement) if your project has them.
- Keep the verify-vs-validate distinction visible throughout — it's the spine of the document. If an activity isn't clearly one or the other, work out which before writing it down.

**Identifier conventions**:
- VV-N: V&V activities/tasks (referenced from §4, §5, anomaly reports, and other documents)
- OQ-N / OQ-DEF-N: open questions (load-bearing / deferred-with-defaults)

These prefixes enable cross-document traceability — requirements in the SRS can be traced to the V&V activities (VV-N) that check them.

**For regulated/safety-critical projects:** use the full IEEE 1012-2016, not this lightweight version. The full standard defines integrity-level-specific task tables, minimum required activities per level, and formal independence criteria that this template only gestures at.
