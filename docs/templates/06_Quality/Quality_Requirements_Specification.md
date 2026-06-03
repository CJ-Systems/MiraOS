# Quality Requirements Specification Template

> **Template purpose:** Lightweight Quality Requirements Specification (QRS) structure for selecting and quantifying software-quality targets, organized around the SQuaRE product quality model. A *quality requirement* says how WELL the system must do something ("password reset completes in under 2 seconds for 95% of attempts"), as opposed to a *functional requirement*, which says WHAT it does ("the user can reset their password"). This document turns the loose category people call "non-functional requirements" into measurable, verifiable targets. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once you have (or are drafting) a Software Requirements Specification and you need to state — in numbers a test can check — how well the system must perform, how reliable it must be, how secure, how maintainable, and so on. Write it when "the system should be fast" is no longer good enough and someone needs a pass/fail line at acceptance. It qualifies the functional requirements; it does not replace them.
>
> **Companion standard:** ISO/IEC 25010:2023 (SQuaRE — product quality model); ISO/IEC 25012 (data quality model); ISO/IEC 25023 and ISO/IEC 25040 (quality measurement and evaluation) where access available.
>
> **Status of this template:** Lightweight skeleton assembled from public summaries of the ISO/IEC 25000 (SQuaRE) family — the characteristic and sub-characteristic names and the WHAT/HOW-WELL framing are widely published, but the standards themselves are paywalled and copyrighted by ISO/IEC. No normative text is reproduced here; all guidance is paraphrase. Verify characteristic names, sub-characteristics, and any measures against the full ISO/IEC 25010:2023, 25012, 25023, and 25040 documents before using in enterprise, regulated, or contractual contexts — the 2023 revision of 25010 in particular restructured several characteristics (e.g., Usability to Interaction Capability) and added Safety, so confirm the model version you cite.

---

# Quality Requirements Specification — {{System Name}}

| Field | Value |
|---|---|
| Document ID | QR-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC 25010:2023 (SQuaRE) + 25012 / 25023 / 25040 (lightweight) |
| Owner | {{Project name or quality owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Companion SRS | SRS-{{PROJECT-ID}}-001 (the functional requirements these quality requirements qualify) |
| Quality model | ISO/IEC 25010:2023 product quality (8 characteristics; 2023 revision adds Safety and restructures Usability as Interaction Capability — note which model version you used) |
| Measurement basis | {{ISO/IEC 25023 measures / project-defined measures / mixed}} |
| Verification owner | {{who runs the measurements and signs off acceptance}} |

---

## 1. Introduction

> One paragraph: state that this document selects and quantifies the SQuaRE product quality characteristics for {{System Name}} as verifiable quality requirements, and that it *qualifies* (does not replace) the functional requirements in the companion SRS. The four subsections below set the frame: why the document exists, what it covers, the vocabulary it uses, and what it depends on.

This document specifies the quality requirements for **{{System Name}}** — the measurable targets for how well the system must perform, not what features it provides. It selects the relevant characteristics from the SQuaRE product quality model (ISO/IEC 25010:2023), pairs each with a defined measure, sets target levels and acceptance thresholds, and names how each is verified. It qualifies the functional requirements in the companion SRS (`SRS-{{PROJECT-ID}}-001`); the SRS says WHAT the system does, this says HOW WELL.

### 1.1 Purpose

> Why this document exists and what it specifies. Establish that it is the authoritative source for quality targets — the place a tester or reviewer looks to learn the pass/fail line for performance, reliability, security, and the rest. Establish too that it sits beside the SRS, not above or below it.

{{This document exists to make the quality expectations for {{System Name}} explicit, measurable, and verifiable. It converts vague goals ("fast," "secure," "reliable") into numbered requirements with measures, targets, and acceptance thresholds, so that at release time there is an objective basis for deciding whether quality goals were met. It is the companion to SRS-{{PROJECT-ID}}-001.}}

### 1.2 Scope

> Define which parts or releases of the system the quality requirements cover, and what is explicitly out of scope. Quality targets are often release-specific (a v1 may accept lower availability than a v2), so anchor the scope to a release or milestone where that matters.

In scope:
- {{Subsystem / release / deployment the targets apply to}}
- {{...}}

Out of scope (for this version):
- {{Excluded subsystem or concern}} — {{reason / where it is handled instead}}
- {{...}}

### 1.3 Definitions and Acronyms

> Define the vocabulary this document leans on, especially the few formal terms a first-time reader needs to follow the rest. Define each one the first time it would otherwise be guessed at. Add project-specific terms as needed.

| Term | Definition |
|---|---|
| Quality characteristic | A top-level category of "goodness" — e.g., Reliability. Each splits into *sub-characteristics* (Reliability = maturity, availability, fault tolerance, recoverability). You select which matter for your system rather than maximizing all of them. |
| Sub-characteristic | A named facet of a characteristic, finer-grained and usually where the measurable target actually lands. |
| Quality measure (metric) | A defined way to turn a characteristic into a number you can check. "Reliability" is not testable; "mean time between failures" is. A quality requirement pairs a target value with a measure so it can be verified. |
| Target level | The value you are aiming for (e.g., 99.95% uptime). |
| Acceptance threshold | The line that decides pass/fail at acceptance (e.g., minimum-acceptable 99.9% uptime). Target and threshold can differ. |
| Verifiable requirement | A requirement you can prove was met by test, measurement, inspection, or analysis. "The system should be fast" is not verifiable; "p95 response time ≤ 300 ms under 100 concurrent users" is. |
| SQuaRE | *Systems and software Quality Requirements and Evaluation* — the ISO/IEC 25000 family. 25010 names the product quality characteristics; 25012 covers data quality; 25023 and 25040 cover how to measure and evaluate quality. |
| {{Project term}} | {{Definition}} |

### 1.4 References

> List what this document depends on or draws from: the companion SRS, any architecture decisions that fix a quality target, the ISO/IEC 25000-family standards used, and the docs for any tools that produce the measurements. Categorize for readability.

Project documents:
- `SRS-{{PROJECT-ID}}-001` — functional requirements these quality requirements qualify
- {{path/to/architecture.md}} — {{relevance, e.g., where an availability target is realized}}

Architecture Decision Records:
- ADR-NNNN — {{decision that fixes or constrains a quality target}}

External standards:
- ISO/IEC 25010:2023 — product quality model (characteristics and sub-characteristics)
- ISO/IEC 25012 — data quality model (used in §6, if applicable)
- ISO/IEC 25023 — measurement of product quality (source of measures, if used)
- ISO/IEC 25040 — quality evaluation process (used in §8, if applicable)

Measurement tooling:
- {{tool / harness}} — {{which measures it produces}}

---

## 2. Quality Goals and Stakeholders

> Before any numbers, capture the WHY. Who cares about quality here — end users, operators, the buyer, regulators — and what "good enough" means to each of them? This is the honesty check on every later target: a 99.99% uptime target needs a stakeholder who actually requires that figure and will pay for it, otherwise it is an invented cost. Keep this short: name the top 3–5 quality goals and tie each to a stakeholder. These goals motivate the characteristic selection in §3.

| Goal | Stakeholder | What "good enough" means to them |
|---|---|---|
| {{e.g., the app feels instant in normal use}} | {{End users}} | {{e.g., common actions complete without a visible wait}} |
| {{e.g., it stays up during business hours}} | {{Operator / on-call}} | {{e.g., unplanned downtime is rare and short}} |
| {{e.g., customer data is protected}} | {{Buyer / data subjects / regulator}} | {{e.g., access is controlled and breaches are detectable}} |
| {{...}} | {{...}} | {{...}} |

{{Optional: a sentence or two of narrative on which goal dominates when money or time is tight. The dominant goal should reflect itself in the priority ranking in §3.}}

---

## 3. Quality Characteristic Selection and Prioritization

> This is the *tailoring* step — deliberately choosing which characteristics apply to your system rather than trying to satisfy all of them. Not every system needs heavy portability or strict performance; you justify what you include and what you leave out. List the eight ISO/IEC 25010 product quality characteristics, mark each in-scope or out-of-scope with a one-line justification, then rank the in-scope ones so trade-offs can be decided later (§7). Give each selected characteristic a QSC-N ID so the requirements that quantify it (§5) can trace back here.
>
> Beginner note: the 2023 revision of 25010 restructured some names (Usability is presented as *Interaction Capability*) and added *Safety* as a ninth characteristic. The eight below are the long-standing product characteristics; confirm the exact set and names against the model version you cite (see the metadata table).

| ID | Characteristic | In scope? | Priority | Justification |
|---|---|---|---|---|
| QSC-1 | Functional suitability | {{Yes/No}} | {{High/Med/Low}} | {{e.g., functional correctness is the core promise — High}} |
| QSC-2 | Performance efficiency | {{Yes/No}} | {{...}} | {{e.g., interactive UI — responsiveness matters — High}} |
| QSC-3 | Compatibility | {{Yes/No}} | {{...}} | {{e.g., single-platform, no interop needs — out of scope}} |
| QSC-4 | Interaction capability (usability) | {{Yes/No}} | {{...}} | {{e.g., non-technical users — Medium}} |
| QSC-5 | Reliability | {{Yes/No}} | {{...}} | {{e.g., used during business hours — High}} |
| QSC-6 | Security | {{Yes/No}} | {{...}} | {{e.g., stores personal data — High}} |
| QSC-7 | Maintainability | {{Yes/No}} | {{...}} | {{e.g., small team, long-lived codebase — Medium}} |
| QSC-8 | Portability | {{Yes/No}} | {{...}} | {{e.g., fixed deployment target — out of scope}} |

> If you cite the 2023 model and treat Safety as a separate characteristic, add a QSC-9 row for it.

**Tailoring rationale:** {{One short paragraph explaining why the out-of-scope characteristics are genuinely not concerns for {{System Name}} — e.g., "Portability is out of scope because the system deploys only to a single managed environment for the foreseeable releases." Recording the reason protects against a future reader assuming it was an oversight.}}

---

## 4. Quality Measures and Method

> This section is what makes the difference between "fast" and "p95 latency ≤ 300 ms at 100 concurrent users." A *quality measure* is a defined way to turn a characteristic into a number you can check. Define each measure ONCE here, with a QM-N ID, so the individual requirements in §5 can reference it instead of re-explaining the math. For each measure give: the unit, the measurement function (how the number is computed), the conditions under which it is measured (load, environment, data set), and the source — an ISO/IEC 25023 measure, a tool's output, or a project-defined measure.

| ID | Measure | Unit | Measurement function | Conditions | Source |
|---|---|---|---|---|---|
| QM-1 | {{e.g., p95 response time}} | {{ms}} | {{95th-percentile of request latency over the run}} | {{100 concurrent users, reference environment, warm cache}} | {{tool output / 25023 / project-defined}} |
| QM-2 | {{e.g., availability}} | {{% over period}} | {{uptime ÷ (uptime + downtime) over a rolling 30 days}} | {{production-equivalent environment, planned maintenance excluded}} | {{monitoring tool / project-defined}} |
| QM-3 | {{e.g., mean time to recover}} | {{minutes}} | {{average elapsed time from fault detection to restored service}} | {{induced-fault test}} | {{project-defined}} |
| QM-N | {{measure}} | {{unit}} | {{how computed}} | {{when / where / under what load}} | {{source}} |

> Reusing a measure across several requirements is normal and encouraged — that is the point of defining them here. If two requirements need the same number under different conditions, define the conditions on the requirement (§5), not by duplicating the measure.

---

## 5. Quality Requirements

> The core of the document: one numbered requirement (QR-N) per quantified quality target. Organize by characteristic — one subsection per in-scope QSC from §3. For each QR-N, name the characteristic/sub-characteristic, the QM-N measure it uses, the target level, the acceptance threshold (the pass/fail line), and the verification method. Each requirement must be *atomic* (one target per requirement), *measurable* (references a QM-N), and free of implementation detail — it says HOW WELL, not HOW. If you find yourself writing "by using a cache" or "via a load balancer," that is design and belongs in the architecture doc, not here.

### 5.1 {{Performance Efficiency}} (QSC-2)

| ID | Sub-characteristic | Measure | Target | Acceptance threshold | Verification |
|---|---|---|---|---|---|
| QR-1 | Time behaviour | QM-1 | {{≤ 250 ms p95}} | {{≤ 300 ms p95}} | {{Load test, measurement}} |
| QR-2 | {{Resource utilization}} | {{QM-N}} | {{target}} | {{threshold}} | {{method}} |

### 5.2 {{Reliability}} (QSC-5)

| ID | Sub-characteristic | Measure | Target | Acceptance threshold | Verification |
|---|---|---|---|---|---|
| QR-3 | Availability | QM-2 | {{99.95%}} | {{99.9%}} | {{Measurement over 30-day window}} |
| QR-4 | Recoverability | QM-3 | {{≤ 5 min}} | {{≤ 15 min}} | {{Induced-fault test}} |

### 5.3 {{Security}} (QSC-6)

| ID | Sub-characteristic | Measure | Target | Acceptance threshold | Verification |
|---|---|---|---|---|---|
| QR-5 | {{Confidentiality}} | {{QM-N}} | {{target}} | {{threshold}} | {{Inspection / pen test / analysis}} |
| QR-6 | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

### 5.N {{Other in-scope characteristic}} (QSC-N)

> Add one subsection per in-scope characteristic. Keep numbering of QR-N continuous across subsections so each requirement has a unique ID for cross-referencing from tests and the verification plan.

| ID | Sub-characteristic | Measure | Target | Acceptance threshold | Verification |
|---|---|---|---|---|---|
| QR-N | {{...}} | {{QM-N}} | {{target}} | {{threshold}} | {{method}} |

---

## 6. Data Quality Requirements

> If the system stores or processes data that matters — records, content, model inputs — specify data quality targets per ISO/IEC 25012, using the same QR-N pattern. Data quality has its own characteristics: *accuracy* (the data correctly represents the real-world value), *completeness* (expected values are present, not missing), *consistency* (the same fact does not contradict itself across the data set), *currentness* (the data is up to date), and others. For a data-centric system this is often where the real risk lives, so do not skip it lightly. If data quality genuinely is not a concern, keep the section and mark it out of scope with a one-line reason.

In scope: {{Yes — the system's value depends on data quality / No — see reason below}}.

{{If out of scope: "Data quality is not a distinct concern for {{System Name}} because {{reason, e.g., the system is stateless and processes transient inputs only}}." Then omit the table.}}

| ID | Data quality characteristic | Measure | Target | Acceptance threshold | Verification |
|---|---|---|---|---|---|
| QR-D1 | Accuracy | {{QM-N — e.g., % records matching source of truth}} | {{≥ 99.5%}} | {{≥ 99%}} | {{Sample audit}} |
| QR-D2 | Completeness | {{QM-N — e.g., % mandatory fields populated}} | {{100%}} | {{≥ 99.9%}} | {{Automated validation}} |
| QR-D3 | Consistency | {{QM-N}} | {{target}} | {{threshold}} | {{method}} |
| QR-D4 | Currentness | {{QM-N — e.g., max age of a record}} | {{target}} | {{threshold}} | {{method}} |

---

## 7. Trade-offs and Conflicts

> Quality characteristics fight each other: more security can cost usability (extra authentication steps); more performance can cost maintainability (hand-tuned code is harder to change); more portability can cost performance. List the known tension pairs for {{System Name}}, state which side wins when they collide, and point to the ADR or the QSC priority ranking (§3) that justifies the call. Writing these down is what stops the team from silently optimizing one number at build time at the quiet expense of another.

| Tension pair | What pulls each way | Which wins | Basis |
|---|---|---|---|
| {{Security vs. Interaction capability}} | {{stronger auth ↔ fewer friction steps}} | {{Security}} | {{QSC-6 (High) > QSC-4 (Medium); ADR-NNNN}} |
| {{Performance vs. Maintainability}} | {{micro-optimization ↔ readable code}} | {{Maintainability up to QR-1 threshold, then Performance}} | {{QSC-7 ranking; team capacity}} |
| {{...}} | {{...}} | {{...}} | {{...}} |

{{Optional narrative: note any trade-off that is deliberately left unresolved and tracked as an open question in §10.}}

---

## 8. Verification and Acceptance

> Define how each QR-N is proven met. The four standard methods are: *test* (run it and observe), *measurement* (instrument it and read the number), *inspection* (examine the artifact or config by eye/checklist), and *analysis* (reason or model it where direct measurement is impractical). If you are following the ISO/IEC 25040 evaluation flow, align this section with it. State the acceptance gate clearly: which requirements are *must-pass* for release versus *monitored-only*, who runs the measurements, and what evidence is recorded. A quality requirement with no verification method here is not yet verifiable — flag it as an open question (§10) rather than leaving it aspirational.

| Requirement | Method | Must-pass for release? | Who verifies | Evidence recorded |
|---|---|---|---|---|
| QR-1 | {{Measurement}} | {{Yes}} | {{Verification owner}} | {{Load-test report, run ID}} |
| QR-3 | {{Measurement}} | {{Yes}} | {{Operator}} | {{Monitoring dashboard export}} |
| QR-5 | {{Inspection / pen test}} | {{Yes}} | {{Security reviewer}} | {{Review checklist, findings log}} |
| QR-N | {{method}} | {{Yes / Monitored-only}} | {{owner}} | {{artifact}} |

**Acceptance gate:** {{State the rule in one sentence — e.g., "All must-pass requirements meet their acceptance threshold; monitored-only requirements are recorded but do not block release." Name who signs off.}}

---

## 9. Assumptions and Constraints

> Record what the targets depend on, so a missed number can be diagnosed as "conditions changed" rather than "we failed." Capture the *reference environment* (the hardware, network, and data volume the targets assume), the assumed usage load, the availability of measurement tooling, and any hard constraints — regulatory minimums, platform limits — that set floors or ceilings on the targets. If a target only holds under stated conditions, say so here.

Assumptions:
- **Reference environment:** {{hardware, network, data volume the targets assume}}
- **Assumed load:** {{e.g., up to 100 concurrent users; peak {{N}} req/s}}
- **Measurement tooling:** {{which tools must be available to verify the targets}}
- {{...}}

Constraints (floors and ceilings on targets):
- {{e.g., regulatory minimum availability of 99.9% — sets the floor for QR-3}}
- {{e.g., platform caps a single request at {{N}} MB — sets a ceiling on a payload target}}
- {{...}}

---

## 10. Open Questions

> Track quality requirements not yet resolved: characteristics selected but not yet quantified, targets awaiting a stakeholder decision, or measures lacking a verification method. Use OQ-N with what is blocking each and who must decide. Resolve and remove as the document matures. An unresolved OQ on a *must-pass* characteristic is a release risk, not a footnote — treat it accordingly.

- **OQ-1:** {{question — e.g., availability target for QSC-5 not yet agreed}} — {{what's blocking, who must decide}}
- **OQ-2:** {{question — e.g., QR-6 has no verification method yet}} — {{blocking, owner}}
- {{...}}

---

## 11. Revision History

> Mandatory. Record every substantive change with a version bump, date, author, and summary — especially target/threshold changes, since those alter the acceptance contract that §8 enforces. Note which ISO/IEC 25010 model version (e.g., the 2023 revision) the requirements were authored against, so a future reader knows the baseline the characteristic names and structure came from.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft (authored against ISO/IEC 25010:{{model version, e.g., 2023}}) |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Quality Goals and Stakeholders — the WHY that keeps targets honest
- §3 Quality Characteristic Selection and Prioritization — the tailoring step
- §4 Quality Measures and Method — without defined measures, the requirements are not verifiable
- §5 Quality Requirements — the core
- §8 Verification and Acceptance
- §11 Revision History

**Optional sections** (include if relevant):
- §6 Data Quality Requirements (omit/mark out of scope for systems where data quality is not a concern; include for anything data-centric)
- §7 Trade-offs and Conflicts (omit if no characteristics meaningfully conflict — but most non-trivial systems have at least one tension worth recording)
- §9 Assumptions and Constraints (omit only if targets are unconditional, which is rare)
- §10 Open Questions (track elsewhere if you prefer)

**Tailoring**:
- The eight characteristics in §3 are the long-standing 25010 product set. Confirm the exact list and names against the model version you cite — the 2023 revision restructured some names (Usability → Interaction Capability) and added Safety. Note your model version in the metadata table and the Revision History.
- Select characteristics deliberately; do not try to maximize all eight. A justified "out of scope" is a stronger document than a half-hearted target for a characteristic nobody needs.
- Keep this document focused on HOW WELL. Anything describing HOW the target is achieved (caches, replicas, algorithms) belongs in the architecture document, not here.
- Define each measure once in §4 and reference it by QM-N everywhere else. Keep QR-N numbering continuous across §5 subsections so each requirement has a unique, citable ID.

**Identifier conventions**:
- QR-N: individual quality requirements (parallels SRS-F / SRS-IF numbering in the SRS)
- QR-D-N: data quality requirements (§6)
- QM-N: quality measures (the metrics behind a requirement)
- QSC-N: selected/prioritized quality characteristics
- OQ-N: open questions

These prefixes enable cross-document traceability — a functional requirement in the SRS can be traced to the quality requirement that qualifies it, and each QR-N can be traced to the measure (QM-N) and characteristic (QSC-N) it rests on.

**For regulated/safety-critical projects:** use the full ISO/IEC 25010:2023, 25012, 25023, and 25040 standards, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products; it paraphrases the SQuaRE organization and reproduces no normative text.
