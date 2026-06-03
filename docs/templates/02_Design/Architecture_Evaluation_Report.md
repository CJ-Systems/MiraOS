# Architecture Evaluation Report Template

> **Template purpose:** Lightweight Architecture Evaluation Report structure following ISO/IEC/IEEE 42030:2019 (architecture evaluation), with ISO/IEC/IEEE 42010:2022 (architecture description) for the description being evaluated. Use this template when you need to *judge* an architecture — not document it — against the goals and concerns it is supposed to serve. Replace `{{placeholder}}` content with evaluation-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When a decision hangs on whether an architecture is good enough — before committing to a proposed design, when a suspected risk needs investigating, when a stakeholder concern needs confirming, or when two or more design options must be compared. An evaluation *judges*; a description (the Architecture Description, per ISO/IEC/IEEE 42010) just *documents what the architecture is*. This report points at a description and asks the harder question: "is it good enough, for whom, and how do we know?" It feeds into one or more ADRs but is broader than any single one.
>
> **Companion standard:** ISO/IEC/IEEE 42030:2019 (architecture evaluation) with ISO/IEC/IEEE 42010:2022 (architecture description) for the description being evaluated.
>
> **Status of this template:** Lightweight skeleton assembled from PUBLIC summaries of ISO/IEC/IEEE 42030:2019 (architecture evaluation) and ISO/IEC/IEEE 42010:2022 (architecture description) — vendor and community implementation guides, standards abstracts, and the overlapping public literature on scenario-based evaluation (ATAM/SAAM). Both standards are ISO-paywalled. No normative text is reproduced; section names, ordering, and ID conventions are paraphrased or derived independently. Verify against the full standards before relying on this for regulated, safety-critical, or enterprise/contractual architecture evaluations.

---

# Architecture Evaluation Report — {{System Name}}

| Field | Value |
|---|---|
| Document ID | AE-{{SYSTEM-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 42030:2019 + ISO/IEC/IEEE 42010:2022 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Evaluation Subject | {{System / architecture under evaluation, and the version/baseline of its description}} |
| Architecture Description Ref | {{ArchDesc-template or doc + version being evaluated, per ISO/IEC/IEEE 42010:2022}} |
| Evaluation Type | {{Single-architecture assessment / Options comparison / Periodic re-evaluation / Risk-driven review}} |
| Evaluators | {{Names/roles of who performed the evaluation, and their independence from the design team}} |
| Evaluation Date / Window | {{When the evaluation was conducted — distinct from the document Date}} |

---

## 1. Introduction

> **Purpose.** State in one paragraph that this document *evaluates* a named architecture against the concerns and drivers it must serve, and that it *judges* rather than *describes*. The description itself lives elsewhere — typically an Architecture Description (ArchDesc) written per ISO/IEC/IEEE 42010:2022. Keep the line between the two clear from the first paragraph, because conflating "what the architecture is" with "is the architecture good enough" is the most common way these reports go wrong.
>
> A note on the load-bearing vocabulary, defined plainly the first time it appears (and collected in §1.3):
> - **Architecture evaluation vs. architecture description** — an *evaluation* (this document, per ISO/IEC/IEEE 42030) JUDGES an architecture against goals and concerns; a *description* (per ISO/IEC/IEEE 42010, e.g. an ArchDesc) just DOCUMENTS what the architecture is. This report points at a description and asks "is it good enough, and for whom?"
> - **Stakeholder and concern** — a *stakeholder* is anyone with an interest in the system (user, owner, operator, regulator, developer); a *concern* is the specific thing they care about (cost, performance, security, maintainability). Concerns are what the evaluation ultimately serves.
> - **Evaluation driver** — the goal or trigger that motivates the evaluation: a decision to be made, a risk to investigate, a concern to confirm, or a comparison between options. Drivers explain WHY this evaluation exists and what question it must answer.
> - **Evaluation criterion** — a concrete, checkable statement (ideally measurable) derived from a concern, against which the architecture is assessed. "Median response under 200 ms at 1000 concurrent users" is a criterion; "fast" is not.
> - **Evaluation method/technique** — the procedure used to gather evidence and reach a judgement (scenario-based analysis like ATAM/SAAM, checklist review, prototyping/measurement, expert inspection, simulation, trade-off analysis). The method makes the evaluation repeatable rather than an opinion.
> - **Finding** — an evidence-backed observation produced by applying a method to a criterion: it states what was assessed, what evidence supports it, and the resulting judgement (pass / concern / risk / fail).
> - **Distinction from an ADR** — an ADR records ONE decision and its rationale; this report assesses a WHOLE architecture (or a set of options) against many criteria and may feed into one or more ADRs as input.

### 1.1 Purpose

> One-paragraph statement of what this report is for. Establish that it is an evaluation of a specific named architecture against specific concerns and drivers, and that judging (not describing) is the job.

{{This document evaluates the architecture of **{{System Name}}** against the concerns of its stakeholders and the drivers that triggered this review. It judges whether the architecture — as documented in the referenced Architecture Description — is good enough to serve those concerns, and for whom. It does not re-describe the architecture; the description lives in the referenced document. The outcome is a recommendation, traceable from each stakeholder concern through to a finding.}}

### 1.2 Scope

> Name exactly which system/architecture and which version is under evaluation, and what is explicitly out of scope. Vague scope is how an evaluation silently drifts to assessing a different design than the one decided on.

**In scope:**
- {{The architecture of {{System Name}} as described in {{ArchDesc ref + version}}}}
- {{Specific qualities/concerns being judged — e.g. latency, recoverability, maintainability}}

**Out of scope:**
- {{Aspects deliberately not evaluated this round — e.g. cost modelling, UI design}} — {{reason}}
- {{Future capability not yet designed}} — {{reason}}

### 1.3 Definitions and Acronyms

> Define the load-bearing terms plainly. Reuse the definitions introduced in the §1 guidance block; collect them here so a reader can find them in one place.

| Term | Definition |
|---|---|
| Architecture evaluation | A judgement of an architecture against goals and concerns (per ISO/IEC/IEEE 42030:2019); *judges*, does not *describe*. |
| Architecture description | A document of what the architecture *is* (per ISO/IEC/IEEE 42010:2022); the input this report evaluates. |
| Stakeholder | Anyone with an interest in the system (user, owner, operator, regulator, developer). |
| Concern | The specific thing a stakeholder cares about (cost, performance, security, maintainability). |
| Evaluation driver | The goal or trigger motivating the evaluation — a decision, a risk, a concern to confirm, a comparison. |
| Evaluation criterion | A concrete, checkable (ideally measurable) statement derived from a concern. |
| Evaluation method | The procedure used to gather evidence and reach a judgement (ATAM/SAAM, inspection, measurement, simulation, trade-off analysis). |
| Finding | An evidence-backed observation with a verdict (pass / concern / risk / fail). |
| {{Term}} | {{Definition}} |

### 1.4 References

> List the architecture description being evaluated, the source requirements (SRS/ADRs), any prior evaluations, and the companion standards. The first entry should always be the version-pinned description this report assesses.

Architecture description under evaluation:
- {{ArchDesc-{{SYSTEM-ID}}-001 vX.Y / path}} — the description this report judges (per ISO/IEC/IEEE 42010:2022)

Source requirements and decisions:
- {{SRS-{{SYSTEM-ID}}-001 / path}} — requirements the architecture must satisfy
- ADR-NNNN — {{decision that shaped the architecture}}

Prior evaluations (if any):
- {{AE-{{SYSTEM-ID}}-000 / path}} — {{prior evaluation; note what changed since}}

External standards:
- ISO/IEC/IEEE 42030:2019 — architecture evaluation
- ISO/IEC/IEEE 42010:2022 — architecture description

---

## 2. Evaluation Context and Subject

> Identify the architecture being evaluated — what system it serves, its current lifecycle stage (concept / proposed / in development / deployed), and the *exact* description and baseline version this report assesses (cite the ArchDesc per ISO/IEC/IEEE 42010:2022). Note any assumptions or environmental conditions that bound the evaluation, and state whether you are evaluating one architecture or comparing options. The point of this section is to pin everything that follows to a specific, version-locked subject so the report cannot silently drift to a different design partway through — that drift is the single most common failure in architecture evaluation, because the design keeps moving while the evaluation is being written.

### 2.1 Subject Under Evaluation

> Name the system, the architecture, and the exact baseline. If you are comparing options, list each option here with a short label you will reuse throughout (Option A, Option B, ...).

| Item | Value |
|---|---|
| System | {{System Name}} |
| Architecture description (baseline) | {{ArchDesc ref + version + date}} |
| Lifecycle stage | {{Concept / Proposed / In development / Deployed}} |
| Single architecture or options? | {{Single}} / {{Options — see table below}} |

If comparing options:

| Option | Label | Short description | Description ref |
|---|---|---|---|
| {{Option A}} | A | {{e.g. monolith with read replicas}} | {{ref}} |
| {{Option B}} | B | {{e.g. event-sourced services}} | {{ref}} |

### 2.2 Bounding Assumptions and Environment

> State the conditions that bound the evaluation: assumed load, data volumes, deployment environment, team size, budget envelope, and anything held constant. If a finding later depends on one of these holding true, it must be cited here so a reader can see what the judgement rests on.

- **{{Assumption}}** — {{e.g. expected peak of 1000 concurrent users; evaluation does not consider 10x growth}}
- **{{Environment}}** — {{e.g. single-region deployment; multi-region is out of scope}}
- **{{Constant held}}** — {{e.g. team of three; no dedicated ops staff assumed}}

---

## 3. Stakeholders and Concerns

> List the stakeholders with an interest in the architecture (owner, users, operators, developers, regulators, security/privacy reviewers) and the specific concern each one holds (cost, performance, security, maintainability, scalability, compliance). Concerns are the *root* from which criteria are derived in §5, so capture them honestly here — including uncomfortable ones — before turning them into checkable statements. If a concern never becomes a criterion, the traceability matrix in §10 will flag it as a gap; that is the system working, not failing.
>
> A *stakeholder* is anyone with a stake in the system; a *concern* is the specific thing they care about. The same person can hold several concerns, and the same concern can be shared by several stakeholders — that is normal. Priority records whose concerns win when two pull against each other (the trade-offs in §8).

| Stakeholder | Concern | Priority | Notes |
|---|---|---|---|
| {{Owner / sponsor}} | {{e.g. total cost of ownership stays within budget}} | {{High}} | {{}} |
| {{End user}} | {{e.g. responses feel instant}} | {{High}} | {{}} |
| {{Operator}} | {{e.g. system recovers without manual intervention}} | {{Medium}} | {{}} |
| {{Developer}} | {{e.g. a new feature can be added without touching unrelated modules}} | {{Medium}} | {{}} |
| {{Security/privacy reviewer}} | {{e.g. user data is encrypted at rest and in transit}} | {{High}} | {{}} |
| {{Regulator (if any)}} | {{e.g. audit log is tamper-evident}} | {{High}} | {{}} |

---

## 4. Evaluation Drivers and Objectives

> State WHY this evaluation is being run and what decision or question it must answer, using **ED-N**. A driver is typically one of: a pending decision, a suspected risk, a concern needing confirmation, or a need to compare alternatives. Make the *success condition* explicit for each driver — the thing that, at the end of the report, lets a reader say "yes, the evaluation answered its question" or "no, it did not." An evaluation with no stated success condition can never be judged complete; it just stops.
>
> Drivers are the link between "someone is worried about X" (a concern, §3) and "here is the checkable bar for X" (a criterion, §5). They explain the *motivation*; criteria provide the *measurable test*.

| ID | Driver type | Driver statement | Success condition |
|---|---|---|---|
| ED-1 | {{Pending decision}} | {{e.g. Confirm the proposed design meets the latency budget before committing to it.}} | {{e.g. Latency criteria EC-1..EC-3 all pass, or risks are explicitly accepted by the owner.}} |
| ED-2 | {{Suspected risk}} | {{e.g. Investigate whether the single database is a recoverability risk.}} | {{e.g. A clear finding on failover behaviour, pass or fail, with evidence.}} |
| ED-3 | {{Concern to confirm}} | {{e.g. Confirm the design satisfies the security reviewer's encryption concern.}} | {{e.g. EC-N for encryption is assessed with evidence.}} |
| ED-4 | {{Options comparison}} | {{e.g. Determine which of Option A / Option B better serves maintainability and cost.}} | {{e.g. A ranked recommendation with the trade-offs named.}} |

---

## 5. Evaluation Criteria

> Turn the concerns (§3) and drivers (§4) into concrete, ideally measurable criteria using **EC-N**, each traced back to the concern(s) and driver(s) it serves. A *good* criterion is checkable — "EC-3: recovers from a single node failure within 30 s with no data loss" — because it states a threshold and a way to judge it. A *bad* criterion is vague — "reliable" — because two honest people will disagree on whether it was met. For each criterion, record the target/threshold and how a pass/fail (or concern/risk) verdict will be decided, so the findings in §7 have an objective bar to compare against rather than an argument to win.
>
> Not every criterion can be a number. Where a quality genuinely resists measurement (e.g. "a new developer can understand the module boundaries in under a day"), make the *test* concrete even if the *metric* is qualitative — name who judges, against what, and how.

| ID | Criterion (checkable statement) | Target / threshold | Derived from | How judged | Method (§6) |
|---|---|---|---|---|---|
| EC-1 | {{e.g. Median response time under load}} | {{< 200 ms at 1000 concurrent users}} | {{Concern: user latency; ED-1}} | {{Measurement against benchmark}} | {{Prototype + measurement}} |
| EC-2 | {{e.g. 95th-percentile response time under load}} | {{< 500 ms at 1000 concurrent users}} | {{Concern: user latency; ED-1}} | {{Measurement against benchmark}} | {{Prototype + measurement}} |
| EC-3 | {{e.g. Recovery from single node failure}} | {{< 30 s, no data loss}} | {{Concern: operator recoverability; ED-2}} | {{Failure-injection scenario}} | {{Scenario-based (ATAM)}} |
| EC-4 | {{e.g. User data encrypted at rest and in transit}} | {{All PII paths encrypted}} | {{Concern: security; ED-3}} | {{Inspection of data-flow against checklist}} | {{Expert inspection / checklist}} |
| EC-5 | {{e.g. New feature added without modifying unrelated modules}} | {{Change confined to ≤ 2 modules for the reference scenario}} | {{Concern: maintainability}} | {{Change-impact scenario walkthrough}} | {{Scenario-based (SAAM)}} |

---

## 6. Evaluation Methods and Techniques

> Describe HOW the architecture was assessed against the criteria. Name the method(s) used and say why each fits the criteria it serves. Recording the method is what makes an evaluation *repeatable* rather than an opinion — it lets a later reader (or a re-evaluation) weigh how much trust the findings deserve and reproduce them if needed. Also note the *inputs* each method consumed: the description, prototypes, benchmark harnesses, expert sessions, simulations.
>
> Common methods, in plain terms:
> - **Scenario-based analysis (ATAM / SAAM and relatives)** — walk a concrete scenario ("a node fails", "we add feature X") through the architecture and see what happens to a quality. Good for recoverability, modifiability, and trade-off discovery. (ATAM = Architecture Trade-off Analysis Method; SAAM = Software Architecture Analysis Method — both public, scenario-driven techniques.)
> - **Checklist or expert inspection** — a knowledgeable reviewer checks the design against a list of known good/bad properties. Cheap; quality depends on the reviewer.
> - **Prototyping and measurement** — build a slice, run a benchmark, record numbers. The strongest evidence for performance criteria; the most expensive.
> - **Simulation** — model the system and run synthetic load when a real prototype is impractical.
> - **Trade-off analysis** — explicitly examine where improving one quality costs another (feeds §8).

| Method | Used for (criteria) | Why it fits | Inputs consumed | Confidence it yields |
|---|---|---|---|---|
| {{Scenario-based (ATAM)}} | {{EC-3}} | {{Best way to test failure behaviour without a full outage}} | {{Description; failure scenarios}} | {{Medium–High}} |
| {{Prototype + measurement}} | {{EC-1, EC-2}} | {{Performance claims need real numbers}} | {{Prototype; benchmark harness; load profile}} | {{High}} |
| {{Expert inspection / checklist}} | {{EC-4}} | {{Encryption coverage is checkable against a known list}} | {{Description; data-flow diagram; security checklist}} | {{Medium}} |
| {{Scenario-based (SAAM)}} | {{EC-5}} | {{Modifiability is best judged by walking a change scenario}} | {{Description; reference change scenario}} | {{Medium}} |

---

## 7. Findings

> The substantive core of the report. Present the evidence-backed results using **EF-N**, one finding per criterion (or per scenario), each citing the criterion (EC-N) it assesses, the evidence gathered, and a clear verdict: **pass / concern / risk / fail**. Keep findings factual and traceable — and keep the *observed evidence* separate from your *interpretation* of it, so a reader can disagree with your reading while still trusting your data. The table keeps it scannable; add prose underneath for the significant findings (the ones that drive the recommendation or surface a risk).
>
> A **finding** is what you get when you apply a method (§6) to a criterion (§5): "I tested EC-1 by running the benchmark; here are the numbers; therefore pass/concern/risk/fail." If a criterion could not be evaluated, that is itself a finding — record it as a gap and move it to Open Questions (§11).

| ID | Assesses | Method | Evidence (observed) | Verdict |
|---|---|---|---|---|
| EF-1 | EC-1 | {{Prototype + measurement}} | {{Median 140 ms at 1000 users over 3 runs}} | {{Pass}} |
| EF-2 | EC-2 | {{Prototype + measurement}} | {{p95 620 ms — exceeds 500 ms target}} | {{Concern}} |
| EF-3 | EC-3 | {{Scenario-based (ATAM)}} | {{Failover took 45 s in the injected-failure scenario; no data lost}} | {{Risk}} |
| EF-4 | EC-4 | {{Expert inspection}} | {{All PII paths encrypted; one internal log path stores plaintext}} | {{Concern}} |
| EF-5 | EC-5 | {{Scenario-based (SAAM)}} | {{Reference change touched 2 modules as designed}} | {{Pass}} |

**Significant findings (prose):**

- **EF-2 (concern):** {{The 95th-percentile latency exceeds the EC-2 target by ~24%. Evidence: three benchmark runs at 1000 concurrent users. Interpretation: the tail is dominated by {{cause}}; this is a concern rather than a hard fail because the median (EF-1) passes comfortably and the cause has a known mitigation (see REC-N).}}
- **EF-3 (risk):** {{Failover exceeds the EC-3 30 s target (observed 45 s) although no data was lost. Evidence: failure-injection scenario. Interpretation: recoverability is a real risk against the operator's concern; the gap is in {{component}}. See R-N in §8 and REC-N in §9.}}
- **EF-4 (concern):** {{Encryption coverage is nearly complete; one internal log path writes plaintext PII. Evidence: data-flow inspection against the checklist. Interpretation: a bounded, fixable gap rather than a systemic failure.}}

---

## 8. Risks, Trade-offs, and Sensitivity Points

> Call out where the architecture trades one concern against another (e.g. caching improves latency but weakens consistency), which decisions are **sensitivity points** (a small change there has a large effect on a quality), and which findings translate into open **risks**. This is where scenario-based analysis earns its keep: naming the trade-offs makes the recommendation honest, rather than presenting the design as free of tension. Link each risk back to the finding (EF-N) and concern that produced it, so nothing appears from nowhere.
>
> Plain definitions:
> - **Trade-off** — a point where you cannot maximise two qualities at once; improving one costs the other. The job here is to *name* the trade-off and say which side the architecture chose, not to pretend it does not exist.
> - **Sensitivity point** — a single decision or parameter where a small change produces a large change in a quality (e.g. cache TTL strongly affecting both latency and staleness). Worth flagging because it is where future tuning — or future breakage — concentrates.
> - **Risk** — a finding (usually a *risk* or *fail* verdict) that threatens a concern and is not yet resolved.

**Trade-offs:**

| ID | Trade-off | Qualities in tension | Choice made by the architecture | Source |
|---|---|---|---|---|
| TO-1 | {{e.g. Aggressive caching}} | {{Latency ↑ vs. consistency ↓}} | {{Favours latency; accepts brief staleness}} | {{EF-1, concern: latency}} |
| TO-2 | {{e.g. Single primary database}} | {{Simplicity ↑ vs. recoverability ↓}} | {{Favours simplicity; recoverability gap}} | {{EF-3}} |

**Sensitivity points:**

| ID | Sensitivity point | Quality affected | Why it matters |
|---|---|---|---|
| SP-1 | {{e.g. Cache TTL}} | {{Latency and staleness}} | {{Small TTL change swings both qualities}} |

**Risks:**

| ID | Risk | Severity | From finding | Threatens concern |
|---|---|---|---|---|
| R-1 | {{Failover exceeds the 30 s recoverability target}} | {{High}} | EF-3 | {{Operator recoverability}} |
| R-2 | {{Plaintext PII in internal log path}} | {{Medium}} | EF-4 | {{Security/privacy}} |
| R-3 | {{Latency tail exceeds p95 target}} | {{Medium}} | EF-2 | {{User latency}} |

---

## 9. Conclusion and Recommendation

> State the overall verdict the drivers (§4) asked for, then give specific, actionable recommendations using **REC-N**. Each recommendation should be one of a small, honest set of shapes — *adopt as-is / adopt with conditions / revise / reject / compare further* — and each should be tied to the findings (EF-N) and risks (R-N) that justify it. If options were compared, name the recommended option and say why it beat the others. Be explicit about your *confidence level* and any *conditions* that must hold for the recommendation to stand. Finally, note which recommendations should become ADRs, since an ADR is where a single decision and its rationale get recorded for the long term.

### 9.1 Overall verdict

> Answer the drivers directly. For each ED-N, did the evaluation meet its success condition?

| Driver | Met its success condition? | Summary |
|---|---|---|
| ED-1 | {{Yes / Partially / No}} | {{e.g. Latency budget met at the median; p95 needs work — see REC-1}} |
| ED-2 | {{Yes / Partially / No}} | {{e.g. Failover risk confirmed — see R-1, REC-2}} |
| ED-3 | {{Yes}} | {{e.g. Encryption concern largely satisfied; one gap — REC-3}} |

**Overall:** {{e.g. The proposed architecture is sound on cost and maintainability, passes median latency, but carries a recoverability risk and two bounded concerns. Recommendation: adopt with conditions.}}

**Confidence:** {{High / Medium / Low}} — {{why; what would raise it}}

### 9.2 Recommendations

| ID | Recommendation | Shape | Justified by | Should become ADR? |
|---|---|---|---|---|
| REC-1 | {{e.g. Add request batching to bring p95 under 500 ms before launch}} | {{Adopt with conditions}} | EF-2, R-3 | {{Yes — ADR-NNNN}} |
| REC-2 | {{e.g. Introduce a standby replica to meet the 30 s failover target}} | {{Revise}} | EF-3, R-1 | {{Yes — ADR-NNNN}} |
| REC-3 | {{e.g. Redact PII from the internal log path}} | {{Adopt with conditions}} | EF-4, R-2 | {{No — tracked as a bug}} |
| REC-4 | {{e.g. Prefer Option A over Option B for lower operational load}} | {{Compare further}} | {{EF-N, TO-N}} | {{Yes}} |

**Conditions that must hold for the recommendation to stand:** {{e.g. the 1000-user load assumption from §2.2; if traffic is expected to 10x, re-evaluate.}}

---

## 10. Traceability

> Provide a matrix linking concerns → evaluation drivers (ED-N) → criteria (EC-N) → findings (EF-N) → recommendations (REC-N), so a reader can follow any stakeholder concern through to its outcome and confirm nothing was dropped on the way. This is the audit trail that separates a structured evaluation from an opinion. Read each row left to right; if a concern has no criterion, or a criterion has no finding, that is a **gap** — flag it explicitly here and route it to Open Questions (§11) rather than letting it disappear.

| Concern | Driver | Criterion | Finding | Verdict | Risk | Recommendation |
|---|---|---|---|---|---|---|
| {{User latency}} | ED-1 | EC-1 | EF-1 | Pass | — | — |
| {{User latency}} | ED-1 | EC-2 | EF-2 | Concern | R-3 | REC-1 |
| {{Operator recoverability}} | ED-2 | EC-3 | EF-3 | Risk | R-1 | REC-2 |
| {{Security/privacy}} | ED-3 | EC-4 | EF-4 | Concern | R-2 | REC-3 |
| {{Maintainability}} | {{—}} | EC-5 | EF-5 | Pass | — | — |
| {{Cost}} | ED-4 | {{— GAP}} | {{— GAP}} | {{not evaluated}} | — | {{→ OQ-N}} |

**Gaps flagged:** {{e.g. the cost concern has no criterion this round — see OQ-1.}}

---

## 11. Open Questions

> List the questions still unresolved at the time of writing using **OQ-N** — criteria that could not yet be evaluated, evidence that was unavailable, or trade-offs awaiting a stakeholder decision — and note what is blocking each and who must resolve it. Distinguish **blockers** that hold up the recommendation from **revisit-later** items that can wait for a future re-evaluation. Resolve and remove as the work progresses; an open question that has been answered should move into a finding or a recommendation, not linger here.

| ID | Open question | Blocking / Revisit-later | What's blocking it | Who resolves |
|---|---|---|---|---|
| OQ-1 | {{e.g. Does the cost concern need a criterion this round?}} | {{Revisit-later}} | {{Cost model not yet available}} | {{Owner}} |
| OQ-2 | {{e.g. Can we get a real benchmark for the 10x-growth scenario?}} | {{Revisit-later}} | {{No representative load generator}} | {{Dev team}} |
| OQ-3 | {{e.g. Will the owner accept the residual failover risk if REC-2 slips?}} | {{Blocking}} | {{Awaiting owner decision}} | {{Owner}} |

---

## 12. Revision History

> Track every substantive change to the report with version, date, author, and a brief description of what changed. Because an evaluation reflects a *specific architecture baseline at a specific time*, note in this history when the underlying architecture version changes — a new baseline usually means a fresh evaluation (a new AE-…-002), not an in-place edit, because the findings were tied to the old design.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Evaluation Context and Subject (the version-pinned subject is non-negotiable — an evaluation with no fixed baseline is meaningless)
- §3 Stakeholders and Concerns
- §4 Evaluation Drivers and Objectives
- §5 Evaluation Criteria
- §6 Evaluation Methods and Techniques
- §7 Findings
- §9 Conclusion and Recommendation
- §12 Revision History

**Optional sections** (include if relevant):
- §8 Risks, Trade-offs, and Sensitivity Points (strongly recommended; omit only if the architecture genuinely has no trade-offs worth naming — rare)
- §10 Traceability (omit only for a tiny single-criterion evaluation; otherwise it is the audit trail that earns trust)
- §11 Open Questions (track elsewhere if you prefer)

**Tailoring:**
- The section organization derives from ISO/IEC/IEEE 42030:2019's evaluation flow (context → drivers → criteria → methods → findings → conclusion) but is reduced for solo/small-team use. Add or merge subsections as the evaluation needs.
- For a **single-architecture assessment**, ignore the Option A / Option B columns. For an **options comparison**, carry the option labels through §5–§9 so each criterion is assessed per option and the recommendation names a winner.
- Keep this report focused on *judging*. What the architecture *is* belongs in the Architecture Description (per ISO/IEC/IEEE 42010:2022, e.g. `ArchDesc-template.md`); individual decisions belong in ADRs. This report consumes the first and feeds the second.

**Identifier conventions** (for cross-document traceability):
- ED-N: evaluation drivers (objectives/triggers the evaluation must answer)
- EC-N: evaluation criteria (checkable statements derived from concerns)
- EF-N: evaluation findings (evidence-backed verdicts)
- REC-N: recommendations
- R-N / TO-N / SP-N: risks / trade-offs / sensitivity points
- OQ-N: open questions

These prefixes let an SRS requirement or an ArchDesc concern be traced through this evaluation to a finding and on into an ADR.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 42030:2019 (with ISO/IEC/IEEE 42010:2022 for the description), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
