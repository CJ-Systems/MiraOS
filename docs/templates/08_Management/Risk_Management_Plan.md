# Risk Management Plan Template

> **Template purpose:** Lightweight Risk Management Plan structure inspired by ISO/IEC/IEEE 16085:2021 (the risk management process for systems and software), with an AI-specific section drawing on the NIST AI Risk Management Framework (AI RMF 1.0). Use this template when you need a documented, repeatable way to find, judge, and handle the things that could go wrong on a project. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Any project where unmanaged surprises would hurt — slipping schedules, technical dead-ends, a dependency that vanishes, or (for AI systems) a model that is biased, unsafe, misused, or confidently wrong. Start one as soon as the project has enough shape that you can name real risks. Revisit it on a regular cadence, not just once.
>
> **Companion standard:** ISO/IEC/IEEE 16085:2021 — Systems and software engineering — Life cycle processes — Risk management. The AI-specific section (§7) draws on the NIST AI Risk Management Framework (AI RMF 1.0) and its Generative AI Profile.
>
> **Status of this template:** Lightweight skeleton for solo/small-team use. Inspired-by, not a reproduction — it paraphrases the standards' organization rather than copying their normative text. ISO/IEC/IEEE 16085 is published (and typically paywalled); the NIST AI RMF is free at nist.gov. Verify against the full documents for enterprise/regulated/safety-critical contexts.

---

# Risk Management Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | RISK-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 16085:2021 + NIST AI RMF 1.0 (lightweight) |
| Owner | {{Project name or risk owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Scope | {{Whole project / specific subsystem / release}} |
| Review cadence | {{e.g., monthly, per release, per milestone}} |

---

## 1. Introduction

### 1.1 Purpose

> One-paragraph statement of what this document is for. Establish that this is the project's single place for recording what could go wrong, how bad it would be, and what is being done about it.

{{This document records how {{Project Name}} identifies, judges, treats, and monitors risk. A "risk" here is an uncertain event or condition that, if it happens, would affect the project's goals — usually for the worse. The aim is not to eliminate all risk (impossible) but to make the important risks visible, owned, and handled deliberately instead of by surprise.}}

### 1.2 Scope

> Define what this plan covers and what it does not. Is it the whole project, one subsystem, one release? Note anything explicitly out of scope (e.g., organization-wide enterprise risk handled elsewhere).

In scope:
- {{What this plan covers — e.g., technical, schedule, and resource risk for the v1 release}}
- {{AI-specific risk for the model/feature named in §7, if applicable}}

Out of scope:
- {{What is handled elsewhere — e.g., company-wide financial risk, legal/contract risk}}

### 1.3 Definitions and Acronyms

> Define the core vocabulary plainly. The four terms below are the load-bearing ones — keep their definitions even if you trim the rest. A reader who understands these can read the whole document.

| Term | Definition |
|---|---|
| Risk | An uncertain event or condition that, if it occurs, would affect a project goal. Usually negative; an upside version is called an *opportunity*. |
| Likelihood | How probable the risk is. Rate it on a simple scale (e.g., Low / Medium / High, or 1–5) so rows can be compared. |
| Impact | How bad it would be if the risk happened. Same kind of scale (Low / Medium / High, or 1–5). |
| Exposure | **Likelihood × Impact.** A single number (or band) that lets you rank risks against each other. A "Medium likelihood, High impact" risk and a "High likelihood, Low impact" risk can finally be compared on one axis. This is how you decide what to work on first. |
| Risk owner | The one person accountable for watching a given risk and driving its treatment. Not a committee — a name. |
| Treatment | The chosen response to a risk: avoid, mitigate, transfer, or accept (see §5). |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> Foundational documents and standards this plan depends on or that inform it.

External standards:
- ISO/IEC/IEEE 16085:2021 — Risk management process (companion standard for this plan).
- NIST AI Risk Management Framework (AI RMF 1.0) — free at nist.gov; informs §7.
- NIST AI RMF Generative AI Profile — companion profile for generative-AI risks; informs §7.

Project documents:
- {{path/to/srs.md}} — requirements this project must meet (risks often map to requirements).
- {{path/to/architecture.md}} — design context for technical risks.
- ADR-NNNN — {{decision that created or retired a risk}}.

---

## 2. Risk Management Process Overview

> Describe the loop the project runs. The whole discipline is a four-step cycle that repeats — it is not a one-time exercise. State the cadence so it actually happens. Keep it lightweight: for a solo/small-team project this can be a recurring 30-minute review, not a formal ceremony.

The risk process is a repeating loop:

1. **Identify** — Find risks. Brainstorm what could go wrong, review past projects' surprises, walk the architecture and the schedule, and ask "what are we assuming that might not hold?" New risks enter the register (§4) here.
2. **Analyze** — For each risk, rate **likelihood** and **impact**, then compute **exposure** (likelihood × impact). This ranks the list so attention goes to the biggest exposures first, not the loudest voice.
3. **Treat** — Choose a treatment strategy (§5: avoid / mitigate / transfer / accept) for each risk worth acting on, assign an owner, and record the planned action.
4. **Monitor** — Track whether treatments are working, watch for risks changing severity, and catch new risks (§6). Findings feed back into Identify, and the loop continues.

**Cadence:** {{State when each step runs. Example: identify + analyze at the start of each milestone; treat as part of milestone planning; monitor in a recurring {{weekly/monthly}} review and whenever a re-assessment trigger (§6) fires.}}

**Roles:** {{Who runs the loop. For a solo project this is you; for a small team, name the facilitator and confirm each risk has a single owner.}}

---

## 3. Risk Categories

> Categories are buckets that help you find risks you would otherwise miss — run down the list and ask "do we have any of these?" Use them to tag rows in the register so you can spot clusters (e.g., "most of our exposure is schedule risk"). Add or drop categories to fit the project.

- **Technical** — The system might not work as intended: an approach that turns out infeasible, integration that does not converge, performance/scaling shortfalls, fragile dependencies.
- **Schedule** — Work takes longer than planned: underestimated tasks, hidden dependencies, milestones that slip and cascade.
- **Resource** — People, money, or infrastructure fall short: a key contributor leaves, a budget is cut, required hardware or a paid service becomes unavailable.
- **External / Market** — Forces outside the project's control: a vendor changes terms or shuts down, a competitor ships first, regulations change, a third-party API or license disappears.
- **AI-specific** (if the system uses AI/ML) — Risks unique to learned, probabilistic systems. See §7 for treatment mapped to the NIST AI RMF. Core sub-types:
  - **Bias** — The model produces systematically unfair or skewed outputs across groups or inputs.
  - **Safety** — Outputs cause harm to users or third parties (unsafe instructions, harmful content, real-world side effects of agentic actions).
  - **Misuse** — The system is used for purposes it was not intended for, including adversarial prompts, jailbreaks, or weaponization of a feature.
  - **Hallucination** — The model states false information confidently as fact, leading users to trust and act on it.
- {{Add project-specific categories — e.g., Security, Privacy, Compliance, Operational.}}

---

## 4. Risk Register

> This is the heart of the document — the living table of known risks. Each row is one risk. Sort by exposure (highest first) so the top of the table is where attention goes. Keep it current: add rows as risks are found, update likelihood/impact as the situation changes, and move closed risks to a "Closed" status rather than deleting them (so the history survives). Use the ID `RISK-N` for traceability from other documents.

| ID | Description | Category | Likelihood | Impact | Exposure | Owner | Treatment | Status |
|---|---|---|---|---|---|---|---|---|
| RISK-1 | {{e.g., Chosen vector store cannot meet query latency at target data volume}} | Technical | {{Medium}} | {{High}} | {{High}} | {{Owner}} | Mitigate | Open |
| RISK-2 | {{e.g., Model hallucinates citations in user-facing answers, eroding trust}} | AI-specific (hallucination) | {{High}} | {{Medium}} | {{High}} | {{Owner}} | Mitigate | Open |
| RISK-N | {{Description}} | {{Category}} | {{L/M/H}} | {{L/M/H}} | {{computed}} | {{Owner}} | {{Strategy}} | {{Open / Monitoring / Closed}} |

> **Likelihood / Impact scale used in this register:** {{Define your scale once, here. Example — Likelihood: Low <25%, Medium 25–60%, High >60%. Impact: Low = minor rework, Medium = milestone slip, High = project goal at risk. Exposure band: combine the two, e.g., any High×High = critical, address now.}}

---

## 5. Risk Treatment Strategies

> For every risk worth acting on, pick one of four strategies. This is the decision layer — analysis tells you how big a risk is; treatment is what you do about it. Record the chosen strategy in the register and the concrete action in the notes.

- **Avoid** — Change the plan so the risk cannot occur. Drop the risky feature, choose a different approach, or remove the dependency entirely. Use when the exposure is high and the thing causing it is not essential. *Cost:* you give up whatever the risky path would have delivered.
- **Mitigate** — Reduce the likelihood, the impact, or both, while keeping the activity. Add tests, build a prototype/spike to retire technical uncertainty early, add redundancy, set a guardrail. Most active treatments are mitigations. *Record the specific action and who owns it.*
- **Transfer** — Shift the risk (or its cost) to someone better placed to carry it. Insurance, a support contract, an SLA with a vendor, or moving a component to a managed service. The risk still exists; someone else now bears more of it. *Note what residual risk you still hold.*
- **Accept** — Decide to live with the risk, consciously and on the record. Appropriate when exposure is low, or when treatment would cost more than the risk itself. For non-trivial accepted risks, note a **contingency** (what you will do if it happens) and a **trigger** (the signal that it has). Acceptance is a decision, not a default — it belongs in the register with a name attached.

> **Guidance:** Rank by exposure, treat top-down. Do not over-treat low-exposure risks. A risk can change strategy over time (an accepted risk that grows may need mitigation). Note residual risk — the exposure that remains *after* treatment — for anything you mitigate or transfer.

---

## 6. Monitoring and Review

> Risks are not static: a "Low" risk last month can be "High" today. This section says how the project keeps the register honest. Define both the regular rhythm and the events that force an unscheduled re-look.

**Review cadence:**
- {{Regular review — e.g., walk the register in the {{weekly/monthly}} project review: update likelihood/impact, check treatment progress, close resolved risks, capture new ones.}}
- {{Per-milestone or per-release re-assessment of the full register.}}

**Triggers for unscheduled re-assessment** (re-open the loop when any of these fire):
- A risk's treatment is not working as planned.
- A major change to scope, schedule, architecture, or team.
- A dependency, vendor, or external condition changes (price, terms, availability, regulation).
- An accepted risk's trigger condition appears.
- A near-miss or an actual occurrence of any risk (treat as a signal to re-scan related risks).
- {{For AI systems}} A model/version change, a shift in input data distribution, or a newly reported failure mode (bias, unsafe output, jailbreak, hallucination pattern).

**Metrics to watch (optional):** {{e.g., number of open high-exposure risks, age of oldest untreated risk, count of risks that materialized vs. were caught early.}}

---

## 7. AI-Specific Risk Considerations

> Complete this section only if the system includes AI/ML. Learned systems carry risks ordinary software does not: they are probabilistic, can be biased by their data, can be manipulated by inputs, and can be confidently wrong. The NIST AI Risk Management Framework (AI RMF 1.0) organizes the work into four functions — use them as a checklist alongside the register. The Generative AI Profile adds guidance specific to systems that generate text/images/code.

Map AI risks (from §3's AI-specific category) onto the four NIST AI RMF functions:

- **Govern** — Set the culture and accountability for AI risk. *Who owns AI risk? What is the acceptable-use policy? What are the escalation paths when a model behaves badly?*
  - {{Project's governance notes — owner, policies, human-oversight expectations.}}
- **Map** — Establish context and identify the AI risks. *Where is the model used? Who could be affected? What could go wrong — bias, safety, misuse, hallucination? What is the intended vs. foreseeable-misuse use?*
  - {{Context + identified AI risks; cross-reference the RISK-N rows that are AI-specific.}}
- **Measure** — Assess, analyze, and track the identified risks with appropriate methods. *How will bias be tested? How is hallucination rate measured? What red-teaming or evaluation is run before and after release?*
  - {{Evaluation/measurement approach — test sets, metrics, red-team plan, monitoring of live outputs.}}
- **Manage** — Act on the risks by priority: treat, monitor, and respond to incidents. *What guardrails, human-in-the-loop checks, content filters, rate limits, or rollback plans are in place? How are incidents handled?*
  - {{Treatments and operational controls; cross-reference §5 strategies for the AI-specific rows.}}

> **Generative AI Profile note:** If the system generates content (text, code, images), consult the NIST AI RMF Generative AI Profile for risks that are amplified in generative systems — confabulation/hallucination, harmful or biased generation, data-privacy leakage from training data, prompt-injection and jailbreak, and provenance/authenticity of outputs. Add any that apply as RISK-N rows.

---

## 8. Open Questions

> Risk-management decisions still being resolved. Resolve and remove as work progresses.

- **OQ-1**: {{question — e.g., "What likelihood/impact scale fits this project — 3-band or 5-point?"}} — {{what's blocking, who decides}}
- **OQ-2**: {{question — e.g., "Do we need a formal AI red-team pass before v1, or is internal eval enough?"}} — {{blocking / owner}}
- ...

---

## 9. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — especially the four core definitions in §1.3)
- §2 Risk Management Process Overview
- §4 Risk Register (the living heart of the plan)
- §5 Risk Treatment Strategies
- §9 Revision History

**Optional sections** (include if relevant):
- §3 Risk Categories (recommended — drives discovery; trim categories to fit)
- §6 Monitoring and Review (defer the metrics part if too early, but keep the cadence)
- §7 AI-Specific Risk Considerations (omit entirely if the system has no AI/ML)
- §8 Open Questions (track elsewhere if you prefer)

**Tailoring**:
- Pick ONE likelihood/impact scale and define it once (in §4); use it consistently so exposures compare.
- Keep the register sorted by exposure, highest first — the top of the table is where work goes.
- Give every non-trivial risk a single named owner, not a group.
- Don't over-engineer: a solo project can run the whole loop in a recurring short review. The discipline is in repeating it, not in the formality.
- The `RISK-N` IDs enable cross-document traceability — a risk can be referenced from the SRS, an ADR, or a design doc.

**For regulated/enterprise projects:** use the full ISO/IEC/IEEE 16085 (and NIST AI RMF for AI systems), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
