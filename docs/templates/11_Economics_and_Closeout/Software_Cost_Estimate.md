# Software Cost Estimate Template

> **Template purpose:** Lightweight Software Cost Estimate structure following the SWEBOK v3.0 Software Engineering Economics Knowledge Area. Use this template when you need to put numbers — size, effort, cost, schedule — on a piece of software work *before* committing to it. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Whenever a decision (go/no-go, scope cut, deadline, budget request, bid) depends on knowing roughly how big, long, or expensive the work is. Produce the first version early (rough, order-of-magnitude) and re-issue tighter versions at milestones as unknowns resolve. The estimate feeds a project plan and a commitment; it is not itself the commitment.
>
> **Companion standard:** SWEBOK v3.0 Knowledge Area: Software Engineering Economics. Sizing/parametric methods named (not normatively required): COCOMO II (constructive cost model) and ISO/IEC 20926:2009 (IFPUG function point counting). Status of template note follows SWEBOK structure; no single normative standard governs the whole document.
>
> **Status of this template:** Lightweight Software Cost Estimate structure following the SWEBOK v3.0 Software Engineering Economics Knowledge Area. Because it follows a SWEBOK KA rather than a single normative standard, it names no single governing standard; SWEBOK organizes the section set (scope, method, size→effort→cost→schedule, risk/contingency, review). The sizing and parametric methods it references — COCOMO II and ISO/IEC 20926:2009 (IFPUG function point counting) — are named as methods, not reproduced. ISO/IEC 20926 is a paywalled ISO standard: this template paraphrases the function-point *concept* only and does not include counting rules, tables, or weights; verify against the purchased standard before performing a formal, auditable function-point count. SWEBOK is freely available from IEEE; COCOMO II model definitions and coefficients are published openly (USC). Suitable for solo/small-team and internal use; for contractual, regulated, or audited estimates, verify against the full referenced sources.

---

# Software Cost Estimate — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | EST-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | SWEBOK v3.0 Software Engineering Economics KA (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Estimate type | {{Order-of-magnitude / Budgetary / Definitive}} |
| Estimation method(s) | {{Expert judgment / Analogy / COCOMO II / Function points / Decomposition / Combined}} |
| Confidence / uncertainty range | {{e.g., -25% / +50% at current phase}} |
| Base currency & cost date | {{e.g., USD, rates as of YYYY-MM}} |
| Traces to | {{SRS-…, WBS / project plan, contract / SOW reference}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: state what this document records and, crucially, that it is an *estimate* — not a promise.
>
> **Software engineering economics** is the practice of putting numbers (size, effort, cost, time) on software work *before* you build it, so decisions about scope and schedule are made with evidence rather than guesswork. SWEBOK treats it as its own knowledge area; this document is one concrete output of it.
>
> **Estimate vs. commitment** — keep these two ideas separate from the first sentence. An *estimate* is your honest best assessment of how big, long, or costly the work *probably* is, expressed as a range. A *commitment* is what you promise to deliver. They are not the same number: a commitment is chosen from within an estimate's range after weighing risk. Confusing the two is the classic estimation failure.

{{This document records the size, effort, cost, and schedule estimate for {{Project Name}}, the method used to produce it, and the assumptions and uncertainty behind the numbers. It is an *estimate* — a defensible basis from which a commitment can be chosen — not the commitment itself. The numbers are ranges, not single guarantees, and they are expected to tighten as the project progresses (see §9).}}

### 1.2 Scope

> Define what this estimate covers and explicitly excludes *at the document level*. State the boundary plainly here; the deeper feature-by-feature inclusion/exclusion list lives in §2 Estimation Scope. The rule that makes an estimate honest: anything not stated as included is, by definition, excluded and out of the number.

This estimate covers: {{the work to deliver Phase 1 of {{Project Name}} — requirements through deployment of the features listed in §2.}}

This estimate excludes: {{ongoing operations, post-launch maintenance beyond warranty, future phases, and any item not enumerated in §2.}}

A precise, item-by-item Included / Excluded breakdown and the work-breakdown items (WBS-N) appear in §2.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define the terms that will trip a reader before they reach the tables. The four-way distinction (size / effort / cost / schedule) and the estimate/commitment pair are the load-bearing ones; get them straight here and the rest of the document reads cleanly.

| Term | Definition |
|---|---|
| Estimate | Honest best assessment of how big/long/costly the work probably is, expressed as a range. |
| Commitment | What is promised to be delivered; chosen from within the estimate's range after weighing risk. Not the same as the estimate. |
| Size | How much software there is (e.g., function points, source lines, stories, components). Independent of who builds it. |
| Effort | Person-time (person-hours or person-months) to build a given size — size run through a productivity rate or model. |
| Cost | Effort priced in money (labor) plus non-effort costs (tools, licenses, hardware, services). |
| Schedule | Calendar time to complete. NOT simply effort divided by headcount (see Brooks's Law, §8). |
| Function Point (FP) | A measure of size based on what the software does for the user (inputs, outputs, inquiries, internal files, external interfaces). ISO/IEC 20926 / IFPUG. |
| WBS | Work Breakdown Structure — the whole job chopped into smaller named items (WBS-1, WBS-2, …) small enough to estimate one at a time. |
| Contingency | Buffer for *known risks that might happen*, rolled into the estimate (see §9). |
| Management reserve | Separate buffer for *unknown unknowns*, held by the sponsor — not by the estimator (see §9). |
| Basis | The short note recording *where a number came from* (method, data, judgment, assumption). The audit trail of an estimate. |
| {{Term}} | {{Project-specific term}} |

### 1.4 References

> List the inputs this estimate stands on. Categorize for readability. The categories matter because of the principle in the note below: an estimate is only as trustworthy as the inputs it cites.

> **Beginner note — why references and "Basis" columns matter.** An estimate is only as trustworthy as the inputs it cites. A number with no stated source cannot be reviewed, defended, or improved — a reviewer has nothing to push on, and you have nothing to update when an input changes. That is why this document carries a References list here *and* a per-number **Basis** column in every estimate table (§§5–8). Together they form the audit trail: every number traces back to a method, a historical data point, a named assumption, or a person's judgment.

Foundational docs:
- {{path/to/charter-or-vision.md}} — {{brief description}}

SRS & plan:
- {{SRS-{{PROJECT-ID}}-001}} — requirements this estimate sizes against
- {{path/to/project-plan.md}} — schedule/plan this estimate feeds

Standards & methods:
- SWEBOK v3.0 — Software Engineering Economics Knowledge Area (organizes this document's section set)
- COCOMO II — constructive cost model; effort/schedule equations (USC, openly published)
- ISO/IEC 20926:2009 — IFPUG function point counting (paywalled; concept paraphrased only — see Status note)

Historical-data sources:
- {{path/to/past-project-actuals}} — {{which prior project, what was measured (size, effort, cost)}}
- {{organizational productivity baseline}} — {{e.g., person-hours per FP from N past projects}}

---

## 2. Estimation Scope

> This is the single most important section for estimate honesty: an estimate is meaningful *only* relative to a precisely-bounded scope. The same 100 hours of work can be a triumph or a disaster depending on what those hours were supposed to buy.

> **Beginner note — decomposition, and the iron rule of scope.** *Decomposition* (building a **Work Breakdown Structure**) means splitting the job into pieces small enough to guess one at a time, giving each a **WBS-N** label, then adding them up. Many small honest guesses beat one big heroic guess, because the small errors tend to cancel while a single big guess just compounds. The WBS-N IDs you create here are the *spine* of the whole document — the same IDs recur in the Size (§5), Effort (§6), Cost (§7), and Schedule (§8) tables, so one item can be traced end to end. The iron rule: **anything not listed as Included below is, by definition, Excluded and out of the number.** If it is not in the WBS, it is not in the estimate.

### 2.1 Included / Excluded

| Area | Included | Excluded |
|---|---|---|
| Functionality | {{features F1, F2, F3 from SRS}} | {{feature F4 (deferred to Phase 2)}} |
| Lifecycle activities | {{requirements, design, build, test, deployment}} | {{operations after go-live}} |
| Documentation | {{user guide, API reference}} | {{full training course materials}} |
| Testing types | {{unit, integration, system, acceptance}} | {{formal security audit, load testing at scale}} |
| Maintenance | {{30-day warranty/bug-fix window}} | {{ongoing maintenance contract}} |
| Support | {{handover and one walkthrough}} | {{help-desk / SLA support}} |

### 2.2 Work Breakdown Structure

> Name each estimated item with a WBS-N. Keep items small enough that you can put one honest number on each. Add or remove rows freely — but every WBS-N you list here must reappear in §§5–8.

| WBS ID | Item | Brief description |
|---|---|---|
| WBS-1 | {{Requirements & analysis}} | {{elaborate and confirm requirements}} |
| WBS-2 | {{Core feature A}} | {{the main user-facing capability}} |
| WBS-3 | {{Core feature B}} | {{secondary capability}} |
| WBS-4 | {{Integration with {{external system}}}} | {{connect to third-party / existing system}} |
| WBS-5 | {{Test & V&V}} | {{test design, execution, defect fixing}} |
| WBS-6 | {{Deployment & handover}} | {{release, docs, walkthrough}} |
| WBS-N | {{…}} | {{…}} |

---

## 3. Assumptions and Constraints

> Every estimate silently assumes things and is silently bounded by limits. This section makes both explicit so a reviewer can challenge them and so you can re-estimate cleanly when one breaks.

> **Beginner note — why estimators write assumptions down.** An *assumption* is something taken as true that, if false, moves the number. Writing it down does two jobs: it lets a reviewer challenge the shaky ones before you commit, and it gives you a clean lever when reality differs — "we assumed stable requirements (ASM-2); they changed; here is the delta." A *constraint* is a hard limit the estimate must respect (a fixed deadline, a budget cap, a mandated technology). Note the link to §8 Risk: a shaky assumption is a candidate risk — if an assumption feels fragile, it probably belongs in the risk register too.

### 3.1 Assumptions (ASM-N)

| ID | Assumption | If false … |
|---|---|---|
| ASM-1 | {{The team of {{N}} {{roles}} is available at {{X%}} allocation for the duration.}} | {{effort spreads over more calendar time; schedule slips}} |
| ASM-2 | {{Requirements are stable after the §1.4 SRS baseline.}} | {{re-work; size and effort grow — see RSK-2}} |
| ASM-3 | {{{{X%}} of code is reused from {{source}}.}} | {{size and effort rise toward from-scratch numbers}} |
| ASM-4 | {{Tooling/platform {{name}} is in place and licensed.}} | {{add setup effort and license cost}} |
| ASM-5 | {{Third-party/vendor {{name}} delivers {{deliverable}} by {{date}}.}} | {{schedule dependency slips — see §8}} |
| ASM-6 | {{Environment/access ({{e.g., test data, prod-like env}}) is granted by {{date}}.}} | {{test phase (WBS-5) starts late}} |

### 3.2 Constraints (CON-N)

| ID | Constraint | Kind |
|---|---|---|
| CON-1 | {{Must ship by {{fixed date}}.}} | {{Schedule}} |
| CON-2 | {{Budget cap of {{amount}}.}} | {{Cost}} |
| CON-3 | {{Must use {{mandated technology / language / cloud}}.}} | {{Technology}} |
| CON-4 | {{Must meet {{regulatory obligation}}.}} | {{Compliance}} |
| CON-5 | {{Team size fixed at {{N}}.}} | {{Resource}} |

---

## 4. Estimation Method

> Name the method(s) you used and *why*, so the estimate is repeatable and reviewable. A method is just a recipe for turning what you know into a number; which one fits depends on how much you know.

> **Beginner note — pick a method by how much you know.** A *method* is a repeatable recipe for turning what you know into a number. Early, when little is known, lean on **analogy** or an **order-of-magnitude** judgment. Later, when the work is well-specified, use **decomposition (bottom-up)** or a **parametric model**. Best practice when stakes are high: produce the number two *independent* ways and reconcile the difference — if they agree, confidence rises; if they diverge, you have found something worth understanding before you commit.
>
> The candidate methods, in plain terms:
> - **Expert judgment** — ask someone who has done similar work. Fast; only as good as the expert and prone to optimism.
> - **Analogy** — scale from a similar *finished* project ("that one was 80% of this, and took 6 months"). Needs a genuinely comparable past project.
> - **Parametric / model-based (COCOMO II)** — feed a size number plus adjustment factors (team experience, complexity, reuse, tooling) into a published formula that outputs effort and schedule. COCOMO II is the best-known open example.
> - **Function-point sizing (ISO/IEC 20926 / IFPUG)** — count *what the software does* (inputs, outputs, inquiries, internal files, external interfaces) to get a size, before any code exists.
> - **Decomposition + bottom-up** — estimate each WBS-N item from §2, then sum. The most reliable approach for a beginner.

### 4.1 Method(s) used

{{This estimate uses {{e.g., decomposition (bottom-up) over the §2 WBS as the primary method, reconciled against an analogy to {{past project}}}}. We chose this because {{reason — e.g., requirements are specified enough to decompose, and a comparable past project exists for a sanity check}}.}}

### 4.2 Reconciliation (if two methods used)

> If you produced the number two ways, show both and explain how you reconciled them. This is where divergence becomes insight.

| Method | Resulting effort | Notes |
|---|---|---|
| {{Decomposition (bottom-up)}} | {{X person-months}} | {{sum of §6}} |
| {{Analogy to {{past project}}}} | {{Y person-months}} | {{scaled by {{factor}}}} |
| **Reconciled** | {{Z person-months}} | {{how the gap was resolved}} |

---

## 5. Size Estimate

> Size is estimated *first*, because effort and cost are derived from it. State the size unit clearly and never mix units silently.

> **Beginner note — size is not effort.** *Size* is *how much software* there is, independent of who builds it or how fast — a 100-FP system is 100 FP whether a fast team or a slow team builds it. We size first, then apply a productivity rate (§6) to get effort. **Function Points** are useful this early because they can be counted from *requirements*, before any code exists, by counting what the software does for the user: inputs, outputs, inquiries (look-ups), internal files (data it stores), and external interfaces (data it shares). (This template paraphrases the FP *concept* only; for a formal, auditable count, use the rules and weights in the purchased ISO/IEC 20926 standard — see the Status note.)

### 5.1 Size by WBS item

| WBS ID | Item | Size measure | Estimate | Confidence / range | Basis |
|---|---|---|---|---|---|
| WBS-2 | {{Core feature A}} | {{FP / SLOC / stories}} | {{e.g., 40 FP}} | {{±20%}} | {{FP count from SRS §3.1; expert judgment}} |
| WBS-3 | {{Core feature B}} | {{FP}} | {{e.g., 25 FP}} | {{±30%}} | {{analogy to {{past feature}}}} |
| WBS-4 | {{Integration}} | {{FP}} | {{e.g., 15 FP}} | {{−10% / +50% (unproven interface)}} | {{see RSK-3}} |
| WBS-N | {{…}} | {{…}} | {{…}} | {{…}} | {{…}} |
| **Total** | | {{FP}} | {{e.g., 80 FP}} | {{rolled-up range}} | {{sum}} |

### 5.2 Function-point derivation (if FP used)

> If you counted function points, record the per-category counts so the size can be reviewed. Reference an appendix if the count is large. (Counts only — do not reproduce the standard's weight tables.)

| FP component category | Count | Notes |
|---|---|---|
| {{External inputs}} | {{n}} | {{e.g., forms the user submits}} |
| {{External outputs}} | {{n}} | {{e.g., reports the system produces}} |
| {{External inquiries}} | {{n}} | {{e.g., look-ups / searches}} |
| {{Internal logical files}} | {{n}} | {{e.g., data groups the system maintains}} |
| {{External interface files}} | {{n}} | {{e.g., data shared with other systems}} |

---

## 6. Effort Estimate

> Effort converts size into person-time. The most common beginner error is counting only coding — count the *whole* lifecycle.

> **Beginner note — the size→effort step, and why effort ≠ schedule.** *Effort = size ÷ productivity* (a historical rate such as person-hours per FP), or *size run through a model* (COCOMO II adjusts for team skill, complexity, and reuse via its cost drivers and scale factors). Two warnings. First, include the *whole* lifecycle — requirements, design, test, integration, documentation, and management overhead — not just coding; under-counting non-code activity is the classic way estimates come in low. Second, effort is *additive across people* (two people can do twice the person-hours) but **schedule is not** — you cannot always buy calendar time by adding bodies (see §8 and Brooks's Law).

### 6.1 Effort by WBS item and activity

| WBS ID | Activity | Effort | Range | Role | Basis |
|---|---|---|---|---|---|
| WBS-1 | {{Requirements & analysis}} | {{e.g., 0.5 pm}} | {{±20%}} | {{Analyst}} | {{decomposition}} |
| WBS-2 | {{Design + build, feature A}} | {{e.g., 2.0 pm}} | {{±25%}} | {{Developer}} | {{40 FP ÷ {{rate}} FP/pm}} |
| WBS-3 | {{Design + build, feature B}} | {{e.g., 1.2 pm}} | {{±30%}} | {{Developer}} | {{25 FP ÷ rate}} |
| WBS-4 | {{Integration}} | {{e.g., 1.0 pm}} | {{−10% / +50%}} | {{Developer}} | {{see RSK-3}} |
| WBS-5 | {{Test & V&V}} | {{e.g., 1.0 pm}} | {{±25%}} | {{Tester}} | {{% of build effort}} |
| WBS-6 | {{Deployment & handover}} | {{e.g., 0.3 pm}} | {{±20%}} | {{Developer}} | {{decomposition}} |
| — | {{Management / coordination overhead}} | {{e.g., 0.6 pm}} | {{±20%}} | {{Lead}} | {{{{X%}} of direct effort}} |
| **Total** | | {{e.g., 6.6 pm}} | {{rolled-up range}} | | {{sum}} |

*(pm = person-months; use person-hours if finer granularity helps.)*

---

## 7. Cost Estimate

> Cost is the money view: effort priced as labor, *plus* everything money buys that effort alone does not.

> **Beginner note — money is effort plus the things effort can't buy.** A person-month becomes dollars via a *loaded rate* (salary + overhead such as benefits, workspace, and management), not the bare salary. Then add the non-people costs — tools and licenses, cloud/hardware/infrastructure, third-party services, travel, training — because a build with cheap labor can still be expensive in licenses or cloud. Two honest-estimate rules apply here: (1) state the **base currency and the cost date**, because rates change; and (2) keep **contingency a visible, separate line** carried from §9 — never silently bake a buffer into the element amounts, or no one can see how much risk is priced in.

### 7.1 Cost by element

| Cost element | WBS ref (if applicable) | Amount | Basis |
|---|---|---|---|
| **Labor** | | | |
| {{Developer effort}} | {{WBS-2..6}} | {{e.g., 5.5 pm × {{loaded rate}}}} | {{§6 effort × loaded rate}} |
| {{Analyst / lead effort}} | {{WBS-1, overhead}} | {{e.g., 1.1 pm × {{loaded rate}}}} | {{§6 effort × loaded rate}} |
| **Non-labor** | | | |
| {{Tools / licenses}} | — | {{amount}} | {{{{N}} seats × {{price}}}} |
| {{Cloud / hardware / infrastructure}} | — | {{amount}} | {{{{months}} × {{monthly cost}}}} |
| {{Third-party services}} | {{WBS-4}} | {{amount}} | {{vendor quote}} |
| {{Travel / training}} | — | {{amount}} | {{estimate}} |
| **Subtotal** | | {{sum of above}} | |
| Contingency (from §9) | — | {{e.g., +15%}} | {{see §9; separate, visible line}} |
| **Total** | | {{subtotal + contingency}} | |

*Base currency: {{e.g., USD}}. Cost date: {{rates as of YYYY-MM}}.*

---

## 8. Schedule Estimate

> Schedule is calendar time. The trap is treating it as effort divided by headcount — it is not.

> **Beginner note — Brooks's Law and the critical path.** **Brooks's Law:** *"Adding people to a late software project makes it later."* Onboarding and communication overhead grow faster than the throughput the new people add, so beyond a point more bodies *slow* delivery. There is a *minimum* calendar time below which more people will not help and can hurt. The other idea is the **critical path:** the longest chain of must-finish-before-the-next-can-start tasks. That chain sets the floor on calendar time regardless of total headcount — speeding up a task that is *not* on the critical path buys you nothing. Tie every milestone back to its WBS-N items so schedule, effort, and cost all reference the same spine.

### 8.1 Milestones

| Milestone | Target date | Predecessor | WBS items |
|---|---|---|---|
| {{M1 — Requirements baselined}} | {{YYYY-MM-DD}} | {{—}} | {{WBS-1}} |
| {{M2 — Feature A complete}} | {{YYYY-MM-DD}} | {{M1}} | {{WBS-2}} |
| {{M3 — Feature B + integration complete}} | {{YYYY-MM-DD}} | {{M2}} | {{WBS-3, WBS-4}} |
| {{M4 — Test pass / acceptance}} | {{YYYY-MM-DD}} | {{M3}} | {{WBS-5}} |
| {{M5 — Deployed / handed over}} | {{YYYY-MM-DD}} | {{M4}} | {{WBS-6}} |

### 8.2 Critical-path / scheduling assumptions

- {{The critical path runs M1 → M2 → M3 → M4 → M5; WBS-4 depends on vendor delivery (ASM-5).}}
- {{Minimum calendar time is {{N}} months even with added staff (Brooks's Law); below this, schedule cannot be compressed by hiring.}}
- {{Team allocation per ASM-1 holds; reduced allocation stretches calendar time proportionally.}}

---

## 9. Risk and Contingency

> An estimate without stated risk and contingency is a single number pretending to be certain. This section tells the truth about what you don't yet know.

> **Beginner note — contingency vs. reserve, and why a single number is a trap.** *Contingency* is extra effort/cost/time set aside for *known risks that might happen* — it is rolled into this estimate (the visible line in §7). *Management reserve* is a separate buffer for *unknown unknowns*, held by the **sponsor**, not by the estimator; keeping them distinct keeps the estimate honest. And a lone single-point estimate is a trap because it *hides its own risk* — it looks precise while concealing how much is unknown. A range plus a stated contingency tells the truth. The **Cone of Uncertainty** describes why: early estimates can be off by 2–4×, and the range narrows only as the project progresses and unknowns resolve — which is exactly why you re-estimate at milestones (each producing a new Revision History row, §12) rather than treating the first number as final.

### 9.1 Estimation risks (RSK-N)

| ID | Risk | Likelihood | Impact | Threatens (line) |
|---|---|---|---|---|
| RSK-1 | {{Scope grows beyond §2 Included list.}} | {{Med}} | {{High}} | {{Size §5, Effort §6, Cost §7}} |
| RSK-2 | {{Requirements churn (ASM-2 fails).}} | {{Med}} | {{High}} | {{Effort §6, Schedule §8}} |
| RSK-3 | {{Integration with {{system}} is unproven.}} | {{High}} | {{Med}} | {{WBS-4 size & effort}} |
| RSK-4 | {{Productivity rate is optimistic vs. actuals.}} | {{Med}} | {{Med}} | {{Effort §6}} |
| RSK-5 | {{Vendor delivery slips (ASM-5 fails).}} | {{Low}} | {{High}} | {{Schedule §8}} |

### 9.2 Contingency and reserve

| Buffer | Amount | Basis | Held by |
|---|---|---|---|
| Contingency | {{e.g., +15% on effort & cost}} | {{weighted from RSK-1..5; in the §7 total}} | {{Estimator / project (in the estimate)}} |
| Management reserve | {{e.g., +10%, separate}} | {{for unknown-unknowns; not in the estimate total}} | {{Sponsor}} |

### 9.3 Stated uncertainty range

- Current confidence range: {{e.g., −25% / +50%}} (consistent with metadata "Confidence / uncertainty range").
- Re-estimation points: {{at M1 (requirements baselined), M3 (integration proven). Each re-estimate adds a Revision History row.}}

---

## 10. Estimate Review and Approval

> This section records the *independent technical review of the estimate's content* — distinct from the front-matter sign-off, which approves *the document*.

> **Beginner note — why estimates get reviewed separately from the work.** The person who made the estimate is the worst judge of its optimism — they share the assumptions that may be too rosy. An *independent reviewer* pressure-tests the assumptions (§3), challenges the method (§4), checks the basis behind each number, and reconciles any two-method gap (§4.2) *before* anyone commits to the number. The relationship to the front-matter sign-off block: that block approves *the document* exists and is authorized; this section records the technical *review of the estimate's content* and the agreed confidence at which it may be used as the basis for a commitment.

### 10.1 Review record

| Reviewer | Date | Concern raised | Resolution |
|---|---|---|---|
| {{Name / role}} | {{YYYY-MM-DD}} | {{e.g., productivity rate optimistic (RSK-4)}} | {{rate lowered; effort §6 updated; re-issued v0.2}} |
| {{Name / role}} | {{YYYY-MM-DD}} | {{e.g., WBS-4 size too low given unproven interface}} | {{range widened to −10%/+50%}} |
| {{…}} | {{…}} | {{…}} | {{…}} |

### 10.2 Agreed confidence and sign-off to commit

{{Reviewers agree this estimate may be used as the basis for a commitment at the {{Order-of-magnitude / Budgetary / Definitive}} level, confidence range {{−25% / +50%}}. The commitment chosen from this range is recorded in {{project plan / contract reference}}, not here.}}

---

## 11. Open Questions

> Name the known holes in the estimate. Naming them is honest and lets a reviewer weight the number accordingly. Resolve and delete each as the project firms up.

> **Beginner note — what an open question is.** An *open question* (OQ-N) is a known hole in the estimate — something unresolved that would move a number if answered differently. Naming it is honest: it lets a reviewer weight the estimate accordingly instead of trusting a falsely-precise figure. Distinguish *deferred-with-default* (it has a working assumption from §3, so the estimate can proceed) from *genuinely blocking* (no defensible number until it is answered). Resolve and delete each as the project firms up.

| ID | Open question | Blocked on / who decides | Line(s) it would move |
|---|---|---|---|
| OQ-1 | {{Will integration use vendor API v1 or v2?}} | {{vendor; decision by {{date}}}} | {{WBS-4 size §5, effort §6 (blocking)}} |
| OQ-2 | {{Is the 30-day warranty in scope or a separate contract?}} | {{sponsor}} | {{Effort §6, Cost §7 (deferred-with-default: assume in scope per ASM)}} |
| OQ-3 | {{Final team allocation %?}} | {{resource manager}} | {{Schedule §8 (deferred-with-default per ASM-1)}} |
| OQ-N | {{…}} | {{…}} | {{…}} |

---

## 12. Revision History

> Estimates are *living* documents. Per the Cone of Uncertainty (§9), re-estimation at each milestone should produce a new row here — so the history shows how and why the number changed over the project's life, not just that it changed.

| Version | Date | Author | Description of Change | Approval |
|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft | {{—}} |
| {{0.2}} | {{YYYY-MM-DD}} | {{Author}} | {{Re-estimated at M1; range tightened to −25%/+40%}} | {{Reviewer}} |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Estimation Scope (the Included/Excluded boundary and the WBS are non-negotiable — they define what the number means)
- §4 Estimation Method (an undefended method makes every later number unreviewable)
- §5 Size, §6 Effort, §7 Cost (the core size→effort→cost chain; produce at least one even at order-of-magnitude)
- §9 Risk and Contingency (at minimum the stated uncertainty range — never ship a bare single-point number)
- §12 Revision History

**Optional sections** (include if relevant):
- §3 Assumptions and Constraints (strongly recommended; omit only for the most trivial estimates — but note that omitting it hides the levers a reviewer needs)
- §5.2 Function-point derivation (omit if you sized by SLOC, stories, or analogy rather than FP)
- §8 Schedule Estimate (omit if only cost is needed; include whenever a deadline is in play)
- §10 Estimate Review and Approval (omit for a quick internal sanity-check; required for any estimate that backs a commitment to others)
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- WBS-N: work-breakdown items — the spine; the same ID recurs in Size (§5), Effort (§6), Cost (§7), and Schedule (§8) so one item traces end to end.
- ASM-N: assumptions
- CON-N: constraints
- RSK-N: estimation risks / contingency drivers
- OQ-N: open questions

These prefixes enable cross-document traceability — requirements in an SRS (`SRS-…`) can be traced to the WBS items they are estimated under, and risks here can be linked to a project risk register.

**Tailoring**:
- Section headers from the SWEBOK Economics KA are guidance, not requirements. Add/remove subsections as the project needs.
- Match the *estimate type* to how much you know: early/little-known → order-of-magnitude (this whole document can be one page, a coarse WBS, and a wide range); later/well-specified → budgetary, then definitive, with the size→effort→cost chain filled in fully.
- Re-issue at milestones rather than editing in place — each re-estimate is a new Revision History row, so the Cone of Uncertainty (§9) is visible in the history.
- **Solo developer / very small team:** collapse the metadata sign-off so Prepared/Reviewed/Approved are the same person (still fill them in — a self-review with a day's gap catches optimism). Merge §3 Assumptions and §9 Risk into a single short list. Keep the WBS (§2), at least one of size/effort/cost (§5–7), and the stated range (§9) — those three are what make it an estimate rather than a guess. Skip §10 independent review, but write down §11 open questions even so; they are the cheapest honesty you can buy.

**For regulated/safety-critical projects:** use the full SWEBOK v3.0 Software Engineering Economics Knowledge Area together with the complete referenced methods — COCOMO II's published model definitions and the purchased ISO/IEC 20926:2009 standard for any formal, auditable function-point count — not this lightweight version.
