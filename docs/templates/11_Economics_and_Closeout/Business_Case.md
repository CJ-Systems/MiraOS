# Software Business Case Template

> **Template purpose:** Lightweight Software Business Case structure that captures the argument for whether a piece of software work is worth doing — the problem, the options weighed, the costs, the returns, and how we will know it paid off. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Before committing time or money to a body of work — a new project, a major feature, a rewrite, a tooling purchase, or a "build vs. buy" decision. The business case is written *before* the work is approved and is revisited at gates as estimates firm up. It is a decision document, not a plan: it explains *whether and why* to proceed, not *how* to build (that is the job of the SRS, the design docs, and the project plan).
>
> **Companion standard:** SWEBOK Software Engineering Economics KA (primary, structural); ISO/IEC/IEEE 16326:2019 — Systems and software engineering — Life cycle processes — Project management (touchpoints for decision rationale and gate review).
>
> **Status of this template:** Lightweight Software Business Case structure. There is no single normative ISO/IEC/IEEE standard that prescribes a "business case" document outline, so this template follows the structure of the SWEBOK (Software Engineering Body of Knowledge) Software Engineering Economics knowledge area — cost-benefit, options analysis, and economic measures (ROI, payback, NPV, cost avoidance) — and names no single normative standard. ISO/IEC/IEEE 16326:2019 (Project management life-cycle processes) is referenced only as a touchpoint for decision rationale and gate review; it is paywalled, so any structural alignment to it here is derived from public summaries and is a faithful skeleton pending verification against the authoritative text. The template paraphrases and derives field names and ordering independently and reproduces no normative standard text. Verify against the full SWEBOK guide and, for regulated, contractual, safety-critical, or enterprise investment-governance contexts, against your organization's investment-approval framework and qualified finance/legal counsel before relying on it — the economic figures it organizes are engineering estimates, not financial advice.

---

# Software Business Case — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | BC-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | SWEBOK Software Engineering Economics KA (lightweight); ISO/IEC/IEEE 16326:2019 (touchpoint) |
| Owner | {{Project name or owner}} |
| Decision sought | {{Approve to proceed / Approve with conditions / Defer / Reject}} |
| Decision authority | {{Role / person who can commit the funds or effort}} |
| Decision-by date | {{YYYY-MM-DD — when the decision is needed to be useful}} |
| Recommended option | {{OPT-N short name — fill once §4 is settled}} |
| Time horizon | {{period the economic analysis covers, e.g. 3 years / one release cycle}} |
| Currency / unit | {{USD / engineer-hours / story points — the unit costs and benefits are stated in}} |
| Confidence | {{Low / Medium / High — overall confidence in the estimates and recommendation}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> **What a business case is (read this first if the term is new).** A *business case* is a short, structured argument for whether a piece of work is worth doing. It states the problem it solves, the options weighed, what each costs, what it returns, and how we will know later that it paid off. It is written *before* anyone commits money or effort, and it is revisited at decision *gates* (checkpoints where someone with authority decides to continue, pause, change course, or stop). A business case is a *decision-rationale* document — its job is to make a yes/no/which-one decision easy to make and easy to challenge. It is **not** a project plan (no Gantt charts, no task breakdown) and **not** a requirements spec (no detailed "the system shall…"). Those come *after* the case is approved.
>
> This section orients the reader. The four subsections below are the standard front matter; fold any project-specific context into them rather than inventing new top-level sections.

### 1.1 Purpose

> One paragraph: why this document exists, what decision it supports, and a plain statement that it is a *decision-rationale* document, not a plan or a requirements spec. Name the framing it follows so reviewers know what to expect.

{{This document makes the case for {{the work / change / investment}} on {{Project Name}}. It exists to support a single decision — whether to {{proceed / approve with conditions / defer / reject}} — by laying out the problem, the options considered, their whole-life costs and expected benefits, the risks, and the measures by which success will later be judged. It follows the SWEBOK *Software Engineering Economics* knowledge area: the discipline of making software decisions in money-and-value terms — comparing alternatives by cost, benefit, and risk over the whole life of the system rather than by technical preference or gut feel alone. This is a decision document, not a plan or a requirements specification; detailed scope and "the system shall…" statements belong in a companion SRS, and detailed effort sizing belongs in a companion Software Cost Estimate.}}

### 1.2 Scope

> What this case covers and explicitly excludes. Name the *time horizon* (how far into the future the economic analysis looks) and the *unit/currency* the numbers are stated in (e.g. USD, or engineer-hours for a team that budgets in effort rather than dollars). State plainly that detailed sizing and effort estimation belong in a companion Software Cost Estimate, not here — this case carries rolled-up figures, not their derivation.

**In scope:**
- {{The decision area this case covers — e.g. "whether to build, buy, or do nothing about the manual {{X}} process."}}
- {{...}}

**Out of scope:**
- {{Detailed effort sizing and per-task estimates — see the companion Software Cost Estimate ({{COST-EST-{{PROJECT-ID}}-001}}).}}
- {{Detailed requirements — see the companion SRS ({{SRS-{{PROJECT-ID}}-001}}).}}
- {{Adjacent decision deliberately left for later — e.g. "vendor selection within the buy option."}}

**Time horizon:** {{e.g. 3 years from go-live / one release cycle / 18 months}} — the period over which costs and benefits in this case are counted.

**Currency / unit:** {{USD / engineer-hours / story points}} — all figures below are stated in this unit unless noted.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define the economics terms actually used in this case so a beginner reader is never gated by jargon. At minimum cover the ones that appear below. Drop any you do not use; add any you do.

| Term | Definition |
|---|---|
| Business case | A structured, pre-commitment argument for whether work is worth doing: problem, options, cost, benefit, success measures. A decision document, not a plan. |
| Software engineering economics | The SWEBOK knowledge area on making software decisions in money-and-value terms — comparing options by cost, benefit, and risk over the whole life of the system. |
| Cost-benefit analysis | Laying expected costs beside expected benefits so they can be compared directly. Benefit may be money saved/earned, time saved, risk reduced, or strategic position gained. |
| Baseline / do-nothing option | The "change nothing" alternative. The comparison floor — every other option must *beat* it to earn its keep. |
| TCO (total cost of ownership) / whole-life cost | The full cost of an option across its entire life — not just building it, but running, maintaining, training, migrating, and eventually retiring it. |
| Opportunity cost | The value of the best thing given up by choosing this option. Spending capacity here means not spending it elsewhere. |
| Sunk cost | Money or effort already spent that cannot be recovered. It must **not** influence the decision; the case looks forward at future cost vs. future benefit. |
| Discounting / time value of money | Adjusting future cash flows *down* to a "present value" because a dollar (or hour) today is worth more than one next year. Often skipped for short small-team cases — state plainly if you are not discounting. |
| ROI (return on investment) | Net benefit divided by cost, usually a percentage. A simple "value per dollar spent" ratio. |
| Payback period | How long until cumulative benefit covers the cost. Short payback = the bet de-risks itself quickly. |
| NPV (net present value) | The sum of all future benefits minus all future costs, each discounted to today's value. Positive NPV = the option is expected to create net value. Optional for lightweight cases. |
| Cost avoidance | A benefit that is a cost you will *not* incur (e.g. a penalty avoided, a hire not made). Real value, but label it as avoidance so reviewers do not double-count it against new revenue. |
| Tangible vs. intangible benefit | Tangible = measurable in money or countable units (hours, tickets, conversions). Intangible = real but hard to quantify (morale, brand, strategic optionality). |
| Sensitivity | How much the recommendation depends on assumptions that might be wrong — "if estimate X is off by 30%, does the decision flip?" |
| {{Other term}} | {{Definition}} |

### 1.4 References

> Applicable project, organizational, regulatory, contractual, and standards references, plus links to any companion documents this case depends on. Categorize for readability so a reviewer can find the source behind any figure.

| Ref | Document |
|---|---|
| R1 | {{path/to/companion/Software_Cost_Estimate.md}} — source of the rolled-up cost figures cited in §6 |
| R2 | {{SRS-{{PROJECT-ID}}-001}} — requirements this work would satisfy |
| R3 | ADR-NNNN — {{decision this case depends on or feeds}} |
| R4 | {{Organizational investment / budget policy}} — approval thresholds and gate process |
| R5 | {{Regulatory / contractual obligation}} — {{relevance, if any}} |
| R6 | SWEBOK — Software Engineering Economics knowledge area ({{edition}}) |
| R7 | ISO/IEC/IEEE 16326:2019 — Project management life-cycle processes (gate-review touchpoint) |
| ... | ... |

---

## 2. Problem or Opportunity

> This section justifies the entire document. Beginner framing: if there is no real problem or genuine opportunity, the strongest recommendation is to **do nothing** — and that is a legitimate, money-saving outcome of a business case. State the need in concrete terms, name what makes it worth addressing *now* (the trigger), say who is affected, and spell out the cost of inaction. *Quantify the pain where you honestly can* — hours lost per week, error rates, customers churned, releases delayed — and write "qualitative" plainly where you cannot, rather than inventing numbers. This section sets up the baseline "do-nothing" option that §3 measures every alternative against.

### 2.1 Current situation and its cost

> What is happening today and what it costs us — in pain, missed value, or risk. Be concrete.

{{Today, {{describe the current state — the manual process, the missing capability, the failing system, the unserved demand}}. The cost of this is {{quantify where honest: e.g. "~{{N}} engineer-hours/week" or "an estimated {{N}} support tickets/month" or "{{N}}% of {{X}} lost"}}. Where the cost is real but not measurable, name it as qualitative: {{e.g. "team frustration and onboarding friction — qualitative, not quantified"}}.}}

### 2.2 Why now (the trigger)

> What changed in the world or the project that makes this worth addressing now rather than later or never? A trigger answers "why isn't this just sitting on the backlog?"

{{The trigger is {{e.g. "a contract renewal in {{month}}", "a platform end-of-life", "a competitor shipping {{X}}", "demand crossing a threshold we can no longer serve manually"}}. Without this trigger the work could wait; with it, delay has a cost (see §2.4).}}

### 2.3 Stakeholders affected

> Who feels the problem and who would feel the change. Naming them grounds the benefits in §5 (each benefit should have a "who realizes it").

| Stakeholder | How they are affected today | What changes for them |
|---|---|---|
| {{End users / customers}} | {{current pain}} | {{expected change}} |
| {{Engineering / support team}} | {{current pain}} | {{expected change}} |
| {{Business / sponsor}} | {{current pain}} | {{expected change}} |
| ... | ... | ... |

### 2.4 Consequence of inaction

> What continues to cost us — or gets worse — if we change nothing. This is the floor the baseline option carries into §3, and it is sometimes the strongest argument in the whole case.

{{If we do nothing, {{the ongoing cost continues at ~{{value}}/{{period}} and/or worsens because {{driver}}}}. Note explicitly whether inaction is *stable* (the pain stays flat) or *escalating* (it compounds) — an escalating do-nothing cost can make even a risky option look attractive.}}

---

## 3. Options Considered

> This is the analytical heart of the case and where the **OPT-N** traceability prefix is established. Beginner framing: the goal is **not** to find a perfect option — it is to make the trade-offs *visible* so the decision-maker chooses with eyes open. Three rules make the comparison fair and honest:
>
> 1. **Always include a do-nothing / baseline option** (use **OPT-0** or **OPT-1**). It is the floor every other option must beat. An option only earns its keep by beating doing nothing.
> 2. **Give every option a stable ID and a short name** (OPT-1, OPT-2, …) so the rest of this document — and downstream documents like a Software Cost Estimate or Lessons Learned Report — can cite it precisely.
> 3. **Judge every option on the same dimensions** so the comparison is apples-to-apples: Description, indicative Cost, expected Benefit, key Risk, and a confidence note.
>
> Use the summary table for scanability, then a short paragraph per option for the reasoning the table cannot hold — the assumptions behind it, and *what would make this option win or lose*. Cross-reference downstream: each option's cost rolls up to the **COST-N** entries in §6, its benefit to the **BEN-N** entries in §5, and its risk to the **BR-N** entries in §7. That way §4's recommendation can cite exactly which benefit, cost, and risk entries justify the choice.

### 3.1 Options summary

| Option (OPT-N) | Description | Indicative cost | Expected benefit | Key risk | Confidence |
|---|---|---|---|---|---|
| OPT-0 | {{Do nothing / baseline — keep the current {{process / system}}}} | {{none new; ongoing cost ~{{value}}/{{period}} continues}} | {{none beyond status quo}} | {{the problem in §2 persists / escalates (BR-1)}} | {{High}} |
| OPT-1 | {{Build it ourselves — {{short approach}}}} | {{~{{value}} one-time + ~{{value}}/{{period}} run (COST-1, COST-2)}} | {{~{{value}} (BEN-1, BEN-2)}} | {{{{e.g. effort overrun}} (BR-2)}} | {{Medium}} |
| OPT-2 | {{Buy / subscribe — {{vendor or category}}}} | {{~{{value}}/{{period}} subscription (COST-3)}} | {{~{{value}} (BEN-1, BEN-3)}} | {{{{e.g. vendor lock-in}} (BR-3)}} | {{Medium}} |
| OPT-3 | {{Hybrid / partial — {{short approach}}}} | {{~{{value}} (COST-4)}} | {{~{{value}} (BEN-2)}} | {{{{risk}} (BR-4)}} | {{Low}} |
| ... | ... | ... | ... | ... | ... |

### 3.2 OPT-0 — {{Do nothing / baseline}}

> The mandatory floor. Describe what continues if nothing is approved.

{{Keeping the status quo carries no new cost but leaves the §2 problem in place. We include it so every other option is judged against a real alternative, not against zero. This option "wins" only if no other option's benefit clears its cost — a legitimate outcome.}}

### 3.3 OPT-1 — {{Short name}}

> One paragraph of the reasoning the table cannot hold.

{{Description and assumptions. What would make this option **win**: {{condition}}. What would make it **lose**: {{condition}}. Key assumption this option rests on: {{assumption — flag if load-bearing for the recommendation in §4}}.}}

### 3.4 OPT-2 — {{Short name}}

{{Description, assumptions, win/lose conditions as above.}}

### 3.5 OPT-N — {{Short name}}

{{... repeat per option ...}}

---

## 4. Recommended Option

> Beginner framing: a recommendation reviewers can *challenge* is one where the reasoning is exposed, not hidden behind a conclusion. Do not just state "we pick OPT-2" — show *why* it beats the others by citing the specific **BEN-N** benefits it captures, the **COST-N** cost it accepts, and the **BR-N** risks it tolerates or mitigates. Name the runner-up explicitly and say why the recommended option edged it out; that single comparison is usually the most decision-useful sentence in the document. State any guardrails (conditions the recommendation depends on) and link forward to the sensitivity note in §8 for what would change the call. Echo the chosen option into the **Recommended option** metadata row at the top.

### 4.1 Recommendation

> One sentence.

{{We recommend **OPT-{{N}} — {{short name}}**, {{proceed / proceed with conditions}}.}}

### 4.2 Why it wins

> The decisive factors, with traceability citations.

{{OPT-{{N}} is recommended because it captures {{BEN-1, BEN-2}} (the highest-value benefits in §5) at an accepted cost of {{COST-1, COST-2}} (§6), while keeping {{BR-2}} within tolerance via {{mitigation}}. We chose it over the runner-up **OPT-{{M}}** because {{the decisive difference — e.g. "OPT-M's lower build cost is outweighed by its recurring run cost (COST-3) over the {{time horizon}}, and it does not deliver BEN-3."}}}}

### 4.3 Conditions and guardrails

> What must be true for the recommendation to hold. These become conditions of approval.

- {{Proceed only if {{budget / headcount / dependency}} is confirmed by {{date}}.}}
- {{Re-confirm at the {{gate name}} gate once {{estimate}} firms up.}}
- {{...}}

### 4.4 What would change this recommendation

> Forward link to §8. Name the one or two things that, if they moved, would flip the call.

{{The recommendation would change if {{e.g. "the build estimate (COST-1) exceeds {{value}}", or "the trigger in §2.2 slips past {{date}}"}}. See the sensitivity note in §8 (EM-{{N}}).}}

---

## 5. Expected Benefits

> Enumerate the benefits of the *recommended* option with **BEN-N** IDs so they can be traced and later checked against reality in a Lessons Learned Report. The single most common beginner error here is **over-claiming**, so apply three disciplines:
>
> 1. **Separate tangible from intangible.** *Tangible* benefits are measurable in money or countable units (hours, tickets, conversions) — state the number *and its basis*. *Intangible* benefits are real but unquantified (morale, brand, strategic optionality) — name them honestly; do **not** invent figures for them.
> 2. **Label cost avoidance distinctly.** A *cost-avoidance* benefit is a cost you will *not* incur (a penalty avoided, a hire not made). It is real value but is **not** new revenue or hard savings — labelling it prevents reviewers from double-counting.
> 3. **Say who realizes it and when.** Benefits often *lag* the spend; a benefit that lands in year two should say so.
>
> These BEN-N entries feed the Economic Analysis in §8 and the Success Criteria in §9 (each success criterion confirms a BEN-N).

| BEN-N | Benefit | Type (tangible / intangible / avoidance) | Estimated value | Who realizes it | When realized | Basis & confidence |
|---|---|---|---|---|---|---|
| BEN-1 | {{e.g. reclaimed engineering time}} | Tangible | {{~{{N}} hrs/{{period}} ≈ {{value}}}} | {{Engineering team}} | {{from go-live}} | {{from §2.1 time study; Medium}} |
| BEN-2 | {{e.g. penalty no longer incurred}} | Avoidance | {{~{{value}}/{{period}} not spent}} | {{Business}} | {{from {{date}}}} | {{contract terms; High}} |
| BEN-3 | {{e.g. faster onboarding / morale}} | Intangible | {{not quantified}} | {{Team}} | {{gradual}} | {{qualitative; stated honestly}} |
| ... | ... | ... | ... | ... | ... | ... |

> **Beginner note on totals:** when you sum benefits for §8, add tangible and avoidance values but keep intangibles *out of the arithmetic* — list them as a qualitative "plus." A total that silently includes a made-up number for morale is the over-claiming trap.

---

## 6. Costs

> The whole-life — *total cost of ownership* — view of the recommended option, with **COST-N** IDs. The key beginner lesson: **under-counting cost is the single most common business-case failure.** Look past build cost. Walk the full lifecycle:
>
> - **Acquisition** (licences, hardware, vendor fees)
> - **Development** (build effort)
> - **Operation** (the costs beginners most often forget: ongoing hosting/run, support burden, monitoring)
> - **Maintenance** (bug fixes, dependency upkeep, security patching)
> - **Training** (getting people able to use or run it)
> - **Migration** (moving off the old way; data migration; parallel-running)
> - **Retirement** (eventual decommissioning, archival, data export)
> - **Opportunity cost** (what we give up by spending this capacity here rather than elsewhere)
>
> Distinguish **one-time** costs from **recurring** costs, and capital from operating where your organization cares about that split. For each cost, state the *basis* — is it a firm quote, an estimate, or a historical analogy? Note explicitly that detailed sizing and effort estimation live in a companion **Software Cost Estimate**; this case carries the rolled-up figures and their confidence, not the derivation. (And remember *sunk cost*: money already spent does not belong in this table — the decision looks forward only.)

| COST-N | Cost element | One-time / recurring | Amount | Basis & confidence |
|---|---|---|---|---|
| COST-1 | {{Development / build effort}} | One-time | {{~{{value}} ({{N}} eng-hrs)}} | {{estimate, rolled up from Software Cost Estimate; Medium}} |
| COST-2 | {{Hosting / run}} | Recurring | {{~{{value}}/{{period}}}} | {{vendor pricing page quote; High}} |
| COST-3 | {{Support & maintenance burden}} | Recurring | {{~{{value}}/{{period}} ({{N}} hrs/{{period}})}} | {{historical analogy to {{similar system}}; Low}} |
| COST-4 | {{Training}} | One-time | {{~{{value}}}} | {{estimate; Medium}} |
| COST-5 | {{Migration / parallel-run}} | One-time | {{~{{value}}}} | {{estimate; Low}} |
| COST-6 | {{Opportunity cost — {{what we forgo}}}} | One-time | {{~{{value}} of forgone {{work}}}} | {{judgement; stated as qualitative if not costed}} |
| COST-7 | {{Retirement / decommissioning}} | One-time (future) | {{~{{value}}}} | {{rough; Low}} |
| ... | ... | ... | ... | ... |

**Whole-life cost summary:** one-time total ≈ {{value}}; recurring total ≈ {{value}}/{{period}}; over the {{time horizon}} ≈ {{value}}. {{Note any large uncertainty band here and carry it into §8.}}

---

## 7. Risks

> The economics-level risk view: **does the bet pay off?** Beginner framing — this is *distinct from* a project-level Risk Management Plan (which tracks threats to delivery). Here we track threats to the *case's costs and benefits*, given **BR-N** IDs. For each risk, note: what it threatens (which **BEN-N** benefit it would shrink or which **COST-N** it would inflate), a rough likelihood and impact, and the planned response — **avoid** (don't do the thing that creates the risk), **reduce** (mitigate it), **accept** (live with it), or **transfer** (insure/contract it away). Include the risk of the *recommended option* **versus** the risk of *doing nothing* — sometimes inaction is the riskier choice, and the case should say so plainly. These BR-N entries inform the contingency in §8 and should be testable against reality later.

| BR-N | Risk | Threatens | Likelihood | Impact | Response (avoid/reduce/accept/transfer) | Owner |
|---|---|---|---|---|---|---|
| BR-1 | {{Doing nothing: §2 problem escalates}} | {{the whole case / BEN-1, BEN-2}} | {{High}} | {{High}} | {{the recommendation itself addresses this}} | {{role}} |
| BR-2 | {{Build effort overruns estimate}} | COST-1 | {{Medium}} | {{Medium}} | Reduce — {{phase the build; checkpoint at {{gate}}}} | {{role}} |
| BR-3 | {{Vendor price increase / lock-in}} | COST-2 | {{Low}} | {{High}} | Transfer/Reduce — {{contract cap; exit plan}} | {{role}} |
| BR-4 | {{Benefit lags longer than expected}} | BEN-1 | {{Medium}} | {{Medium}} | Accept — {{lengthen payback expectation; note in §8}} | {{role}} |
| ... | ... | ... | ... | ... | ... | ... |

**Recommended option vs. do-nothing:** {{State plainly whether proceeding is *less* risky than inaction. E.g. "BR-1 (escalating do-nothing cost) is rated higher than BR-2 + BR-3 combined, so proceeding is the lower-risk path despite its new risks."}}

---

## 8. Economic Analysis

> This is the section a true beginner most needs walked through, and it permits a *light touch*. Here the costs (§6) and benefits (§5) are brought together into decision-useful measures, each given an **EM-N** ID. Choose the measures appropriate to the size of the bet:
>
> - **ROI (return on investment)** = net benefit ÷ cost, as a percentage. Simple "value per dollar."
> - **Payback period** = when cumulative benefit covers the cost. Short payback = the bet de-risks itself quickly.
> - **NPV (net present value)** — for multi-year cases: future benefits minus future costs, each *discounted* to today's value at a stated rate. Positive NPV = expected net value. Optional for small cases.
> - For very small bets, a plain **cost-avoidance / value framing** ("this avoids ~{{value}}/{{period}} for a one-time ~{{value}}") is enough.
>
> **State explicitly whether you are discounting** future cash flows, and why or why not. *Not* discounting is fine and common for short, small-team cases — just say so ("Costs and benefits are stated in nominal {{unit}}; not discounted, because the horizon is under {{N}} years and amounts are small relative to {{org}}'s thresholds"). **Always include a sensitivity / confidence note**: which one or two assumptions, if wrong, would *flip* the recommendation? Beginner caution: a single number like "ROI = 240%" with no assumptions and no sensitivity is *theatre* — the honest analysis shows the range and the load-bearing assumptions. Each measure's EM-N ID lets §4's rationale and §9's success criteria cite it.

### 8.1 Measures

| EM-N | Measure | Value | Inputs (BEN-N / COST-N) | Notes |
|---|---|---|---|---|
| EM-1 | ROI over {{horizon}} | {{~{{N}}%}} | {{(BEN-1+BEN-2 − COST-1−COST-2) ÷ (COST-1+COST-2)}} | {{tangible + avoidance only; intangibles excluded}} |
| EM-2 | Payback period | {{~{{N}} months}} | {{COST-1 ÷ (BEN-1 monthly)}} | {{point at which cumulative benefit ≥ cost}} |
| EM-3 | NPV over {{horizon}} | {{~{{value}} (or "not computed — see §8.2")}} | {{discounted BEN-N − COST-N}} | {{discount rate {{r}}%, or "n/a"}} |
| ... | ... | ... | ... | ... |

### 8.2 Discounting stance

> One short paragraph. Either state the discount rate and why, or state plainly that you are not discounting and why that is acceptable here.

{{We {{are / are not}} discounting future cash flows. {{If discounting: rate = {{r}}%, chosen as {{basis — e.g. org's cost of capital}}. If not: amounts are stated in nominal {{unit}}; the {{horizon}} is short and the sums are small relative to {{org}}'s approval thresholds, so present-value adjustment would not change the decision.}}}}

### 8.3 Sensitivity / confidence note

> The most important paragraph in the section. Name the one or two assumptions the recommendation hangs on, and whether being wrong by a plausible margin flips the call.

{{The recommendation is most sensitive to {{assumption A — e.g. "the build estimate COST-1"}} and {{assumption B — e.g. "the reclaimed-time benefit BEN-1"}}. If COST-1 is 30% higher than estimated, payback extends from {{N}} to {{M}} months but the decision {{holds / flips}}. If BEN-1 is half what we assume, ROI (EM-1) falls to {{~{{N}}%}} and the decision {{holds / flips to OPT-{{M}}}}. Other inputs are not load-bearing at plausible error margins. Overall confidence: {{Low / Medium / High}} — echoed in the metadata row.}}

---

## 9. Success Criteria

> Define measurable outcomes that will tell us, *after the fact*, whether the case's promised value actually arrived — given **SC-N** IDs and traced back to the **BEN-N** benefits and **EM-N** measures they confirm. Beginner discipline: each criterion must be *measurable* (a number, a threshold, a date) and have an *owner* and a *check-point*. The shape is: "we will know by {{date}}, measured as {{metric}}, that {{benefit}} landed." This is what makes a business case **auditable** rather than aspirational, and it is the natural hand-off to a later **Lessons Learned Report**, which checks realized value against these SC-N entries. A criterion with no metric or no check-point date is not a success criterion — it is a wish.

| SC-N | Success criterion | Metric & threshold | Confirms (BEN-N / EM-N) | Check-point date | Owner |
|---|---|---|---|---|---|
| SC-1 | {{Reclaimed time is real}} | {{≥ {{N}} eng-hrs/{{period}} freed, measured by {{method}}}} | BEN-1, EM-2 | {{YYYY-MM-DD}} | {{role}} |
| SC-2 | {{Avoided cost was avoided}} | {{{{penalty / hire}} did not occur}} | BEN-2 | {{YYYY-MM-DD}} | {{role}} |
| SC-3 | {{Run cost stayed within plan}} | {{recurring cost ≤ {{value}}/{{period}}}} | COST-2, EM-1 | {{YYYY-MM-DD}} | {{role}} |
| ... | ... | ... | ... | ... | ... |

---

## 10. Open Questions

> A business case is written under uncertainty; naming the open questions is more honest than papering over them, and it tells the decision authority what is *firm* versus *pending*. Place these near the end so the analysis above stands first. For each question, note what is blocking resolution, who needs to decide, and — critically — whether the recommendation in §4 *depends on it* (**load-bearing**) or merely *refines it* (**deferred-with-a-default**). Use **OQ-N** IDs. Resolve and remove as the case firms up, or move resolved items to a short traceability list so the decision trail survives.

### 10.1 Load-bearing (block or could flip the decision)

- **OQ-1** {{Question}} — *blocking:* {{what / who must resolve}}; *affects:* {{which OPT-N / BEN-N / COST-N}}; the §4 recommendation depends on this.
- ...

### 10.2 Deferred with a default (refine, do not block)

- **OQ-DEF-1** {{Question}} — *default:* {{the assumption we proceed on unless told otherwise}}; revisit at {{gate / date}}.
- ...

### 10.3 Resolved (recorded for traceability)

- **OQ-2** {{Question}}: {{resolution and date}}.
- ...

---

## 11. Revision History

> Mandatory and last, per house style. Business cases are *living* documents — revisited at gates and as estimates firm up — so the history matters for audit and for the decision authority, who may be re-approving. The **Approval** column carries the sign-off into the change record so each revision records who committed to it, matching the sign-off block in the metadata table.

| Version | Date | Author | Changes | Approval |
|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft | {{pending}} |
| ... | ... | ... | ... | ... |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all four subsections — the reader must know the decision, the horizon, and the unit before any number means anything)
- §2 Problem or Opportunity (no problem = recommend do-nothing)
- §3 Options Considered (must include a do-nothing / baseline OPT)
- §4 Recommended Option
- §6 Costs (the whole-life view — under-counting cost is the classic failure)
- §11 Revision History

**Optional sections** (include if relevant):
- §5 Expected Benefits — required when *any* option is recommended over do-nothing; can be folded into §3 only for the very smallest cases.
- §7 Risks — keep it; only the lightest cases (a few hours of work) can fold risk into the option paragraphs in §3.
- §8 Economic Analysis — scale to the bet. A multi-year or six-figure decision needs ROI/payback (and ideally NPV); a small one can carry a one-line cost-avoidance framing in §3 and drop this section.
- §9 Success Criteria — strongly recommended; this is the hand-off to a Lessons Learned Report. Omit only if there is genuinely nothing to measure later (rare).
- §10 Open Questions (track elsewhere if you prefer).

**Identifier conventions:**
- OPT-N: options considered (the primary prefix; OPT-0 or OPT-1 is the do-nothing baseline)
- BEN-N: expected benefits
- COST-N: cost elements
- BR-N: business/economic risks
- EM-N: economic measures in the analysis
- SC-N: success criteria
- OQ-N / OQ-DEF-N: open questions (load-bearing / deferred-with-a-default)

These prefixes enable cross-document traceability: the Recommended Option (§4) cites the exact BEN/COST/BR/EM entries that justify it; a downstream Software Cost Estimate can trace its figures back to a COST-N; and a Lessons Learned Report can check realized value against the SC-N criteria and the OPT-N that was chosen.

**Tailoring:**
- The section list follows the SWEBOK Software Engineering Economics organization; treat it as guidance, not a mandate. Add or merge subsections as the decision needs.
- Keep the business case about *whether and why* to proceed. *How* to build belongs in the SRS and design docs; *how long / how much effort* belongs in a companion Software Cost Estimate. The case carries rolled-up figures, not their derivation.
- **Solo developer / small team:** the case collapses to one page. Keep §2 (one paragraph), §3 (a three-row table: do-nothing, build, buy), §4 (one sentence + the runner-up comparison), §6 (a short whole-life cost list — do not skip the run/maintenance lines, they are where solo budgets actually go), and §8 (one line: "avoids ~{{value}}/{{period}} for a one-time ~{{value}}; not discounting — horizon under two years"). Fold §5, §7, and §9 into a sentence each. Even at one page, keep the do-nothing option and the sensitivity note — those two are what stop a solo developer from talking themselves into a build that never pays back.
- Revisit at gates. When estimates firm up or the trigger date moves, bump the version and re-record approval in §11 — that is the audit trail the decision authority relies on.

**For regulated/safety-critical projects:** use the full SWEBOK Software Engineering Economics guidance and your organization's investment-approval framework with qualified finance and legal counsel, not this lightweight version. The economic figures this template organizes are engineering estimates, not financial advice.
