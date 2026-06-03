# AI Impact Assessment Template

> **Template purpose:** Lightweight AI Impact Assessment structure for recording the AI-specific risks of a system, the real-world impacts it has on people, the mitigations that bring those risks down, and the disclosures owed to affected parties. An *impact assessment* answers two questions at once — "what could go wrong with this system?" and "who gets hurt if it does?" — and writes down what is being done about both. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Before deploying (or substantially changing) any AI or generative system that touches people — anything that decides, recommends, ranks, screens, generates content, or automates a judgment a human used to make. Start one as soon as the system's intended use is clear, and revisit it whenever the system, its use, or the law around it changes. For certain high-risk uses under the EU AI Act this skeleton can serve as the starting point for a Fundamental Rights Impact Assessment (FRIA), and for Colorado's AI Act as the consumer impact assessment — but see the status note below before relying on it for either.
>
> **Companion standard:** ISO/IEC 23894:2023 (AI risk management); NIST AI RMF 1.0 + Generative AI Profile (NIST-AI-600-1); EU AI Act (Reg. (EU) 2024/1689) Art. 27 Fundamental Rights Impact Assessment + Annex IV; Colorado AI Act (SB24-205); ISO/IEC TR 24028:2020 (AI trustworthiness); ISO/IEC TR 5469:2024 (functional safety + AI); OWASP AI Security & Privacy Guide.
>
> **Status of this template:** Lightweight skeleton assembled from public sources. It blends openly available frameworks (NIST AI RMF 1.0 and its Generative AI Profile, the OWASP AI Security & Privacy Guide) with public summaries of paywalled ISO/IEC standards (23894:2023, TR 24028:2020, TR 5469:2024) and the public legal text of the EU AI Act (Reg. (EU) 2024/1689) and the Colorado AI Act (SB24-205). No normative ISO text is reproduced — the structure is paraphrased from public descriptions. Verify against the full ISO/IEC standards and a qualified legal review before relying on this for an EU AI Act FRIA, the Colorado AI Act, or any regulated/high-risk deployment.

---

# AI Impact Assessment — {{System Name}}

| Field | Value |
|---|---|
| Document ID | AIA-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC 23894:2023 + NIST AI RMF 1.0 + EU AI Act Art. 27 (lightweight) |
| Owner | {{Project name or accountable owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| System / Use Case | {{Name of the AI system or specific deployed use case being assessed}} |
| Lifecycle Stage | {{Design / Development / Pre-deployment / In-production / Major change}} |
| Risk Classification | {{e.g., EU AI Act: prohibited / high-risk / limited / minimal; or internal tier}} |
| Role | {{Provider / Deployer / Distributor / Both — your role under the applicable regime}} |
| Assessment Trigger | {{New system / Substantial modification / Periodic review / Incident / Regulatory request}} |
| Reviewers / Approvers | {{Named individuals or roles who reviewed and signed off}} |
| Next Review Due | {{YYYY-MM-DD — assessments are living documents; set a re-review date}} |

---

## 1. Introduction

> This section sets up everything that follows: why the document exists, exactly what it covers, the vocabulary a reader needs, and which laws and standards apply.
>
> A note on the shape of the whole document. This template loosely follows the four functions of the **NIST AI RMF** — *Govern / Map / Measure / Manage* (set up your process, understand the context and the risks, score and test them, then act on them). You do not need to memorize that; it is just the order the sections come in.
>
> The single most important idea to internalize first: an **AI Impact Assessment is not the same as a risk assessment.** A classic risk assessment looks *inward* — what threatens the system. An impact assessment looks *outward* — who is affected by the system, including people who never touch it. An AI Impact Assessment must do **both**. Most of the harm an AI system causes lands on people who are not its users, so the outward view is the one teams most often skip; this template forces it.

### 1.1 Purpose

> One-paragraph statement of what this document is for. Establish that it is the single place where this system's AI-specific risks, its impacts on people, and the mitigations and disclosures that address them are recorded.

{{This document assesses the AI-specific risks and real-world impacts of {{System Name}} and records the mitigations and disclosures that bring residual risk down to an acceptable level. It covers both the inward view (what could go wrong with the system) and the outward view (who is affected and how). The goal is not zero risk — that is impossible for a capable system — but to make the significant impacts visible, owned, and deliberately handled before the system reaches the people it affects.}}

### 1.2 Scope

> Be concrete about which system, which version, and which use case this assessment covers, and state plainly what is out of scope. An impact assessment for "the chatbot, generally" is not actionable; an assessment for "the v2 résumé-screening assistant used by the recruiting team in the EU" is.

In scope:
- System / use case: {{name, version, and the specific deployed use being assessed}}
- {{The model(s), data flows, and decisions covered}}

Out of scope:
- {{Other uses of the same model handled by a separate assessment}}
- {{Components or integrations assessed elsewhere — name where}}

### 1.3 Applicable Regimes and Our Role

> In one short table, name the regulatory regimes you believe apply and your role under each. This drives which later sections are mandatory versus optional, so it is worth getting right early. "Provider" generally means you build or supply the system; "Deployer" means you put it to use; you can be both.

| Regime | Applies? | Our role | Why / classification |
|---|---|---|---|
| EU AI Act (Reg. (EU) 2024/1689) | {{Yes / No / Unsure}} | {{Provider / Deployer / Both}} | {{e.g., high-risk under Annex III; FRIA required}} |
| Colorado AI Act (SB24-205) | {{Yes / No / Unsure}} | {{Developer / Deployer}} | {{e.g., consequential decision in employment}} |
| {{Sector rule — e.g., FCRA, GDPR, HIPAA}} | {{Yes / No / Unsure}} | {{role}} | {{relevance}} |
| {{Internal policy / governance tier}} | {{Yes / No}} | {{owner}} | {{internal classification}} |

### 1.4 Definitions

> Define the core vocabulary plainly. The terms below are the load-bearing ones — keep their definitions even if you trim the rest. A reader who understands these can read the whole document. Add project-specific terms in the empty rows.

| Term | Definition |
|---|---|
| AI Impact Assessment | A document that records both the risks to/from an AI system and the system's effects on the people and groups it touches, plus the mitigations and disclosures that address them. Differs from a plain risk assessment, which looks only inward at threats to the system. |
| Risk = likelihood × impact | The standard way to score a risk: how probable it is, multiplied by how bad it would be if it happened. Used to rank risks so the worst ones get attention first. |
| Likelihood scale | A simple ordinal scale (e.g., Low / Medium / High, or 1–5) with each level defined in words, so two people scoring the same risk land in roughly the same place. See §5. |
| Impact (severity) scale | The companion scale for how bad an outcome would be. Defined the same way. See §5. |
| Inherent risk | The risk *before* any controls are applied. |
| Residual risk | The risk *left over after* mitigations are in place. Regulators and reviewers care most about this number. |
| Algorithmic discrimination / bias | When a system produces systematically worse outcomes for people based on protected characteristics (race, sex, age, disability, etc.). The harm the Colorado AI Act and EU AI Act are most concerned with. |
| Hallucination | When a generative model produces fluent output that is false or fabricated. Treated as an AI-specific risk because the output looks confident regardless of truth. |
| Model drift | The slow degradation of a model's accuracy or fairness over time as the real world moves away from the data the model learned from. Why monitoring is a mitigation, not a one-time check. |
| Autonomy / human oversight | How much the system acts on its own versus requiring a human to review or approve. More autonomy generally means more impact and a stronger oversight control. |
| Information hazard (info-hazard) | Knowledge or output that causes harm simply by existing or being accessible (e.g., weapon-making instructions, exposure of private data). A risk category specific to capable generative systems. |
| Affected stakeholder / impacted group | The people or communities who experience the system's consequences — often *not* its users or operators. Identifying them is the core move of an impact assessment. |
| Fundamental Rights Impact Assessment (FRIA) | The EU AI Act Art. 27 obligation for certain high-risk deployers to assess effects on people's fundamental rights before use. This template can serve as its skeleton. |
| Transparency / disclosure measure | A documented commitment to tell affected people something (that they are dealing with AI, that a decision was AI-assisted, how to contest it). A control in its own right, not just paperwork. |
| Trustworthiness characteristics | The qualities NIST AI RMF and ISO/IEC TR 24028 use to define a "good" AI system: validity, reliability, safety, security, accountability, transparency, explainability, privacy, and fairness. Used here as a checklist of impact dimensions. |
| Govern / Map / Measure / Manage | The four functions of the NIST AI RMF — loosely: set up your process, understand context and risks, score and test them, then act. This document's flow mirrors that order. |
| {{Project-specific term}} | {{Definition}} |

### 1.5 References

> List the standards, regulations, and prior internal documents this assessment relies on. Categorize for readability.

External standards and frameworks:
- ISO/IEC 23894:2023 — AI risk management. {{relevance}}
- NIST AI RMF 1.0 + Generative AI Profile (NIST-AI-600-1). {{relevance}}
- ISO/IEC TR 24028:2020 — AI trustworthiness. {{relevance}}
- ISO/IEC TR 5469:2024 — functional safety + AI (if any safety-relevant use). {{relevance}}
- OWASP AI Security & Privacy Guide. {{relevance}}

Regulations:
- EU AI Act (Reg. (EU) 2024/1689) — Art. 27 FRIA; Annex IV. {{which articles apply}}
- Colorado AI Act (SB24-205). {{which obligations apply}}
- {{Sector regulation}} — {{relevance}}

Prior internal documents:
- {{path/to/SRS.md}} — {{system requirements}}
- {{path/to/RiskMgmt.md}} — {{project risk plan, if separate}}
- {{path/to/prior assessment}} — {{previous version of this assessment}}

---

## 2. System Description and Intended Purpose

> Reviewers cannot judge impact without knowing what the thing actually does. Describe the system in plain language: its intended purpose, the outputs or decisions it produces, the data it ingests, the model(s) or third-party services behind it, and where a human sits in the loop. This is the EU AI Act Annex IV–style "general description" that the whole rest of the assessment hangs on.
>
> Be especially concrete about two things, because they drive impact more than anything else: **(1) the outputs** — what the system actually emits, and whether those outputs become decisions about people; and **(2) the degree of autonomy** — does a human review every output, sample some, or none?

### 2.1 Intended Purpose

> What is this system *for*? State the problem it solves and the benefit it is meant to deliver. Note any uses you explicitly do not intend (which becomes relevant under misuse in §4).

{{Plain-language statement of intended purpose. What decision or task does it support, and for whom?}}

Explicitly *not* intended for: {{out-of-scope uses you are designing against}}

### 2.2 Inputs, Outputs, and Data

> What goes in, what comes out, and what data the system was trained on or retrieves at runtime. Name personal or sensitive data specifically — it drives the privacy analysis later.

| Aspect | Description |
|---|---|
| Inputs | {{What the system receives — user prompts, records, sensor data, documents}} |
| Outputs | {{What it produces — text, a score, a ranking, a recommendation, an automated action}} |
| Training data | {{Source, provenance, known limitations; or "third-party model, training data not disclosed"}} |
| Runtime data / retrieval | {{Documents or databases it queries at inference time, if any}} |
| Personal / sensitive data | {{What categories of personal or protected data are involved, if any}} |

### 2.3 Model(s) and Components

> Name the model(s) and any third-party services. For a model you did not build, note the provider and what you can and cannot see about it (this becomes a transparency limitation later).

- Primary model: {{name / version / provider}}
- Supporting services: {{retrieval, moderation, vector store, APIs}}
- {{What is visible to you vs. opaque (e.g., closed-weights API)}}

### 2.4 Autonomy and Human-in-the-Loop

> State plainly how much the system acts on its own. This is one of the strongest predictors of impact: a system that drafts a suggestion a human edits is very different from one that takes an action automatically.

| Question | Answer |
|---|---|
| Does a human review outputs before they take effect? | {{Every output / A sample / None}} |
| Can the system take action without human approval? | {{Yes — describe / No}} |
| Can a human override or reverse an output? | {{Yes — how / No}} |
| Degree of autonomy (overall) | {{Advisory only / Human-on-the-loop / Fully autonomous}} |

---

## 3. Deployment Context and Affected Stakeholders

> This is the outward-looking "impact" half of the assessment, and it feeds directly into the risk identification in §4. Map the context the system operates in, then identify **every group affected by it** — labeling each `STK-N` so later sections can point back.
>
> The key discipline: separate the people who *operate or use* the system from the often-overlooked people the outputs are *about* or *applied to*. A résumé screener's "users" are recruiters; its most affected stakeholders are the job applicants, who never see the tool. Note vulnerable or protected groups specifically (children, the elderly, people with disabilities, protected classes), the setting (consumer, workplace, public-sector, safety-critical), and the geographies and jurisdictions of use.

### 3.1 Deployment Context

| Aspect | Description |
|---|---|
| Setting | {{Consumer app / Workplace tool / Public-sector / Safety-critical / Internal}} |
| Geographies / jurisdictions | {{Where it is used — drives which laws in §1.3 apply}} |
| Scale | {{How many people are affected, how often}} |
| Consequence level | {{Informational / Influences a decision / Makes a consequential decision automatically}} |

### 3.2 Affected Stakeholder Groups

> List every group, using `STK-N` IDs. Mark whether they are an operator/user or an affected-but-not-using party, and whether they are vulnerable or protected.

| ID | Stakeholder group | Relationship to system | Vulnerable / protected? | Notes |
|---|---|---|---|---|
| STK-1 | {{e.g., End users / operators}} | Uses the system | {{No}} | {{...}} |
| STK-2 | {{e.g., People the outputs are about}} | Affected, does not use it | {{Possibly}} | {{The decisive group for impact}} |
| STK-3 | {{e.g., A protected or vulnerable group}} | {{relationship}} | {{Yes — which characteristic}} | {{...}} |
| STK-4 | {{e.g., Third parties / society / environment}} | {{relationship}} | {{n/a}} | {{...}} |

---

## 4. AI Risk and Hazard Identification

> Now list the AI-specific risks and hazards, labeling each `AIR-N`. The rule here is **identify, do not score yet** — identification and scoring are kept in separate sections (this one and §5) so that nothing gets dropped in a rush to put a number on it. For each risk, say what it is, how it could arise *in this system specifically*, and which stakeholder groups (`STK-N`) it threatens.
>
> Cover at minimum the categories below. They are the AI-specific failure modes the companion standards keep returning to; for misuse and adversarial abuse the **OWASP AI Security & Privacy Guide** is the practical reference. Add system-specific risks freely — the list is a floor, not a ceiling.
>
> - **Bias / algorithmic discrimination** — systematically worse outcomes for people based on protected characteristics.
> - **Hallucination / factual error** — confident, fluent output that is false or fabricated.
> - **Model drift / degradation** — accuracy or fairness sliding over time as the world changes.
> - **Inappropriate autonomy / loss of human oversight** — the system acting beyond where a human can catch it.
> - **Misuse and adversarial abuse** — prompt injection, jailbreaks, data poisoning, abuse for unintended ends.
> - **Privacy and data-protection harms** — leakage, memorization, re-identification, unlawful processing.
> - **Security exposures** — the system as an attack surface or a tool for attackers.
> - **Information hazards** — outputs harmful simply by being available.
> - **Environmental / societal effects** — energy cost, labor displacement, erosion of trust, scaled harms.

### 4.1 Identified Risks

| ID | Category | What it is / how it could arise here | Threatens (STK-N) |
|---|---|---|---|
| AIR-1 | Bias / discrimination | {{How biased outcomes could arise in this system}} | {{STK-2, STK-3}} |
| AIR-2 | Hallucination | {{Where false-but-confident output would cause harm}} | {{STK-1, STK-2}} |
| AIR-3 | Model drift | {{What real-world change would degrade it, and the effect}} | {{STK-2}} |
| AIR-4 | Autonomy / oversight | {{Where the system acts beyond effective human review}} | {{STK-2}} |
| AIR-5 | Misuse / adversarial | {{Prompt injection / jailbreak / poisoning scenario}} | {{STK-1, STK-4}} |
| AIR-6 | Privacy | {{Leakage / memorization / re-identification scenario}} | {{STK-2}} |
| AIR-7 | Security | {{Attack surface or attacker-tool scenario}} | {{STK-1, STK-4}} |
| AIR-8 | Information hazard | {{Harmful-by-availability output scenario}} | {{STK-4}} |
| AIR-9 | Environmental / societal | {{Energy, displacement, trust, or scaled-harm effect}} | {{STK-4}} |
| AIR-N | {{System-specific}} | {{...}} | {{...}} |

---

## 5. Risk Analysis and Evaluation

> This is the ISO/IEC 23894 analyze-and-evaluate step and the NIST "Measure" function in lightweight form. Score each `AIR-N` for **likelihood** and **impact (severity)** on the ordinal scales below, record the **inherent risk** (before any controls) and the resulting **priority**, and state your **risk-acceptance threshold** so a reader knows which risks must be treated and which can be lived with.
>
> The point of scoring is comparison, not precision. A simple Low/Medium/High scale that everyone applies consistently beats an elaborate numeric model nobody trusts. Define each level in words first — that is what keeps two reviewers from scoring the same risk three apart.

### 5.1 Scales

> Define the levels plainly. Edit these to fit; just make sure each level means something a reader can apply.

**Likelihood:**

| Level | Meaning |
|---|---|
| Low | {{Unlikely in normal operation; would require an unusual combination of events}} |
| Medium | {{Plausible; expect it occasionally over the system's life}} |
| High | {{Expected to happen regularly without intervention}} |

**Impact (severity):**

| Level | Meaning |
|---|---|
| Low | {{Minor inconvenience; easily reversed; affects few}} |
| Medium | {{Real harm to individuals or a group; reversible with effort}} |
| High | {{Serious or irreversible harm; affects protected groups, rights, safety, or many people}} |

### 5.2 Risk Acceptance Threshold

> State the line. Above it, a risk must be treated (§6) or escalated; below it, it can be accepted and monitored.

{{e.g., Any risk rated High impact, regardless of likelihood, must be treated before deployment. Any Medium/Medium or higher must have a named mitigation. Low/Low risks are accepted and monitored.}}

### 5.3 Inherent Risk Evaluation

> Score each risk *before* controls. Residual (post-control) risk is recorded later, in §6, after the mitigations are defined.

| Risk ID | Likelihood | Impact | Inherent rating | Priority | Above threshold? |
|---|---|---|---|---|---|
| AIR-1 | {{High}} | {{High}} | {{High}} | {{1}} | {{Yes}} |
| AIR-2 | {{Medium}} | {{High}} | {{High}} | {{2}} | {{Yes}} |
| AIR-3 | {{Medium}} | {{Medium}} | {{Medium}} | {{3}} | {{Yes}} |
| AIR-6 | {{Low}} | {{High}} | {{Medium}} | {{4}} | {{Yes}} |
| ... | ... | ... | ... | ... | ... |

---

## 6. Mitigations and Controls

> For each significant risk, document the mitigations and controls, labeling each `MIT-N`, and **trace each control back to the `AIR-N` it reduces**. Then record the **expected residual risk** once the control is in place. The whole purpose of this section is to show that residual risk has been driven below the acceptance threshold from §5.2 — and to flag, explicitly, any risk that has not.
>
> Cover three kinds of control, because no single kind is enough on its own:
> - **Technical** — guardrails, input/output filtering, evaluation and red-teaming, rate limits, human-review gates, drift monitoring.
> - **Process** — staff training, escalation paths, incident response, change management.
> - **Governance** — sign-off requirements, audit, accountability ownership.
>
> Note on monitoring as a control: model drift (AIR-3-type risks) cannot be fixed once and forgotten, because the world keeps changing under the model. The control for drift is *ongoing measurement*, detailed in §9 — list it here and point there.

### 6.1 Controls and Residual Risk

| ID | Mitigation / control | Type | Reduces (AIR-N) | Expected residual risk | Now below threshold? |
|---|---|---|---|---|---|
| MIT-1 | {{e.g., Bias evaluation on protected subgroups before release + recurring}} | Technical | AIR-1 | {{Medium}} | {{Yes}} |
| MIT-2 | {{e.g., Retrieval grounding + "I'm not sure" behavior + human review of high-stakes outputs}} | Technical / Process | AIR-2 | {{Low}} | {{Yes}} |
| MIT-3 | {{e.g., Scheduled drift monitoring — see §9}} | Technical | AIR-3 | {{Low}} | {{Yes}} |
| MIT-4 | {{e.g., Input/output guardrails + red-team test suite}} | Technical | AIR-5, AIR-8 | {{Medium}} | {{Yes}} |
| MIT-5 | {{e.g., PII minimization, no training on user data, access controls}} | Technical / Governance | AIR-6 | {{Low}} | {{Yes}} |
| MIT-6 | {{e.g., Human-approval gate before any consequential action}} | Process | AIR-4 | {{Low}} | {{Yes}} |
| MIT-N | {{...}} | {{...}} | {{AIR-N}} | {{...}} | {{Yes / No}} |

### 6.2 Risks Remaining Above Threshold

> List any risk whose residual rating is still above the acceptance threshold. Each one is an explicit open item — carry it into §11 (Open Questions) and do not treat the assessment as complete until it is resolved or formally accepted by a named approver.

- {{AIR-N — why it remains above threshold; what is needed to close it; who must decide}}
- {{None, if all residual risks are below threshold.}}

---

## 7. Trustworthiness and Fundamental Rights Impact

> This section assesses the system against the **trustworthiness characteristics** (the qualities NIST AI RMF and ISO/IEC TR 24028 use to define a good AI system) and against effects on people's **fundamental rights and freedoms**. If an EU AI Act Art. 27 **FRIA** is required, this is where it lives; if the use is safety-relevant, **ISO/IEC TR 5469:2024** (functional safety + AI) applies here too.
>
> For each characteristic, say whether the system **meets** it, **falls short**, or it is **not applicable**, and where it falls short, **link back to the relevant `AIR-N`** so the gap is traceable to a scored risk and (ideally) a mitigation.

### 7.1 Trustworthiness Characteristics

| Characteristic | Plain meaning | Status | Linked risk / note |
|---|---|---|---|
| Validity | Does it actually do what it claims, measured against ground truth? | {{Meets / Falls short / N/A}} | {{AIR-N}} |
| Reliability | Does it perform consistently across conditions and over time? | {{...}} | {{AIR-3}} |
| Safety | Can it cause physical or other serious harm? Controlled? | {{...}} | {{TR 5469 if safety-relevant}} |
| Security | Is it resilient to attack and misuse? | {{...}} | {{AIR-5, AIR-7}} |
| Accountability | Is there a named owner answerable for outcomes? | {{...}} | {{governance control}} |
| Transparency | Are people told they are dealing with AI? | {{...}} | {{DISC-N in §8}} |
| Explainability | Can an output be explained to an affected person? | {{...}} | {{DISC-N}} |
| Privacy | Is personal data handled lawfully and minimally? | {{...}} | {{AIR-6}} |
| Fairness | Are outcomes free of unjustified disparity across groups? | {{...}} | {{AIR-1}} |

### 7.2 Fundamental Rights Impact (FRIA, if required)

> If a FRIA is required under EU AI Act Art. 27, assess effects on specific rights. For each, note who is affected (`STK-N`), the nature and severity of the effect, and the safeguard (`MIT-N` / `DISC-N`). If a FRIA is not required, state that and why.

FRIA required? {{Yes — Art. 27 applies / No — explain}}

| Right / freedom | Affected group (STK-N) | Nature & severity of effect | Safeguard (MIT-N / DISC-N) |
|---|---|---|---|
| {{e.g., Non-discrimination}} | {{STK-3}} | {{...}} | {{MIT-1}} |
| {{e.g., Privacy / data protection}} | {{STK-2}} | {{...}} | {{MIT-5}} |
| {{e.g., Right to an effective remedy / to contest}} | {{STK-2}} | {{...}} | {{DISC-N}} |
| {{e.g., Human dignity / autonomy}} | {{...}} | {{...}} | {{...}} |

---

## 8. Transparency and Disclosure Measures

> Disclosures are controls in their own right, not afterthoughts. List the transparency commitments the system will make, labeling each `DISC-N`, and for each one state **who receives it, when, and through what channel**. These satisfy the EU AI Act's transparency duties and the Colorado AI Act's consumer-notice and explanation requirements.
>
> Typical disclosures: telling people they are interacting with AI; labeling AI-generated content; disclosing AI involvement in a consequential decision; providing an explanation of an output; and offering a way to **contest or appeal** an outcome (the right-to-contest is the one teams most often forget, and the one regulators most often require).

| ID | Disclosure / commitment | Who receives it | When | Channel | Satisfies |
|---|---|---|---|---|---|
| DISC-1 | {{"You are interacting with an AI assistant"}} | {{STK-1}} | {{At start of interaction}} | {{In-product banner}} | {{EU AI Act transparency}} |
| DISC-2 | {{AI-generated content is labeled as such}} | {{STK-1, STK-4}} | {{On every output}} | {{Content watermark / label}} | {{EU AI Act}} |
| DISC-3 | {{Notice that an AI was used in this decision}} | {{STK-2}} | {{When decision is delivered}} | {{Decision letter / UI}} | {{Colorado SB24-205}} |
| DISC-4 | {{Plain-language explanation of the decision}} | {{STK-2}} | {{On request / with decision}} | {{Explanation page}} | {{Colorado SB24-205}} |
| DISC-5 | {{How to contest or appeal the outcome}} | {{STK-2}} | {{With the decision}} | {{Appeal channel}} | {{Right to contest}} |
| DISC-N | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

---

## 9. Monitoring, Review, and Incident Response

> A capable system is never "done" — drift, fairness regression, new misuse patterns, and emerging harms all appear *after* deployment. This is the NIST "Manage" function and the ISO/IEC 23894 monitoring step. Specify **what is measured, how often, who is responsible, what triggers a re-assessment of this very document, and how AI incidents are reported and escalated** — including any regulatory reporting obligations (for example, serious-incident reporting under the EU AI Act).

### 9.1 Ongoing Monitoring

| What is measured | Why (links to) | Frequency | Responsible | Threshold for action |
|---|---|---|---|---|
| {{Output accuracy / quality}} | AIR-2, validity | {{Weekly}} | {{role}} | {{below X%}} |
| {{Fairness across STK-3 subgroups}} | AIR-1, fairness | {{Monthly}} | {{role}} | {{disparity > X}} |
| {{Drift indicators}} | AIR-3, MIT-3 | {{Continuous}} | {{role}} | {{drift > X}} |
| {{Misuse / abuse attempts}} | AIR-5, AIR-8 | {{Continuous}} | {{role}} | {{spike / new pattern}} |

### 9.2 Re-Assessment Triggers

> What forces this document to be revisited before its scheduled "Next Review Due" date.

- {{Substantial change to the system or model}}
- {{New use case or new affected group}}
- {{Monitoring threshold breached}}
- {{An AI incident (see §9.3)}}
- {{Change in applicable law or classification}}

### 9.3 Incident Response and Reporting

> How an AI incident is recognized, contained, escalated, and (where required) reported to a regulator.

| Step | Detail |
|---|---|
| What counts as an incident | {{e.g., a harmful output reaching a person, a fairness breach, a data leak, a security compromise}} |
| Containment | {{e.g., kill switch, rollback, disable feature}} |
| Escalation path | {{who is notified, in what order}} |
| Regulatory reporting | {{e.g., EU AI Act serious-incident reporting — deadline, recipient; or "none assessed as applicable"}} |
| Record | {{where incidents are logged for the audit trail}} |

---

## 10. Conformity and Regulatory Mapping

> Give a regulator or auditor a fast way to trace coverage: a short table mapping each applicable regime's obligations to **where in this document** they are satisfied. Note any obligation you assess as **not applicable** and why, and flag any **gap** where conformity is not yet demonstrated (carry gaps into §11).

| Regime | Obligation / element | Where satisfied | Status |
|---|---|---|---|
| EU AI Act | Annex IV general description | §2 | {{Covered}} |
| EU AI Act | Art. 27 FRIA | §3, §7.2 | {{Covered / In progress}} |
| EU AI Act | Transparency duties | §8 (DISC-1, DISC-2) | {{Covered}} |
| EU AI Act | Risk management system | §4, §5, §6 | {{Covered}} |
| EU AI Act | Post-market monitoring / serious-incident reporting | §9 | {{Covered / Gap}} |
| Colorado SB24-205 | Impact assessment elements | §2, §3, §4, §6 | {{Covered}} |
| Colorado SB24-205 | Consumer notice & explanation | §8 (DISC-3, DISC-4) | {{Covered}} |
| Colorado SB24-205 | Right to appeal / correct | §8 (DISC-5) | {{Covered}} |
| NIST AI RMF | Govern | §1.3, §9, governance controls | {{Covered}} |
| NIST AI RMF | Map | §2, §3, §4 | {{Covered}} |
| NIST AI RMF | Measure | §5, §7 | {{Covered}} |
| NIST AI RMF | Manage | §6, §9 | {{Covered}} |
| {{Regime}} | {{Obligation}} | {{§}} | {{Covered / Gap / N/A — why}} |

---

## 11. Open Questions

> Track the unresolved issues that block sign-off or need a decision, labeling each `OQ-N`. For each, note what is blocking resolution and who needs to decide. Because an impact assessment is a *living document, not a one-time gate*, resolve and remove these as the assessment matures.

- **OQ-1**: {{e.g., AIR-N remains above threshold — mitigation not yet built}} — {{blocking: build of MIT-N; decision: owner}}
- **OQ-2**: {{e.g., regulatory classification ambiguous — high-risk under Annex III?}} — {{blocking: legal review}}
- **OQ-3**: {{e.g., could not fully assess impact on STK-N}} — {{blocking: stakeholder consultation}}
- ...

---

## 12. Revision History

> Record every substantive change with a version bump, date, author, and a summary of what changed and why. Because risk classifications, mitigations, and regulations all evolve, this history is the evidence trail that the assessment was kept current. Re-assess on the cadence set in the metadata (or whenever the system, its use, or the regulatory landscape changes materially).

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (especially §1.3 Applicable Regimes — it determines what else is mandatory)
- §2 System Description and Intended Purpose
- §3 Deployment Context and Affected Stakeholders (the outward "impact" view — the part most teams skip)
- §4 AI Risk and Hazard Identification
- §5 Risk Analysis and Evaluation
- §6 Mitigations and Controls
- §12 Revision History

**Optional sections** (include if relevant):
- §7 Trustworthiness and Fundamental Rights Impact (§7.2 FRIA is mandatory only when EU AI Act Art. 27 applies; the §7.1 trustworthiness checklist is recommended for any system that affects people)
- §8 Transparency and Disclosure Measures (mandatory where EU AI Act or Colorado AI Act transparency duties apply; recommended otherwise)
- §9 Monitoring, Review, and Incident Response (defer detail for a pre-deployment design assessment; required before production)
- §10 Conformity and Regulatory Mapping (omit only if no external regime applies; include the moment one does)
- §11 Open Questions (track elsewhere if you prefer, but do not lose risks left above threshold)

**Identifier conventions**:
- AIA-N: this document
- AIR-N: AI risks / hazards
- STK-N: affected stakeholder groups
- MIT-N: mitigations / controls
- DISC-N: required disclosures / transparency measures
- OQ-N: open questions

These prefixes enable cross-document traceability — a risk (`AIR-N`) traces to the stakeholders it threatens (`STK-N`), the control that reduces it (`MIT-N`), and the disclosure that addresses it (`DISC-N`); requirements in an SRS or risks in a Risk Management Plan can point at these IDs in turn.

**Tailoring**:
- Section organization mirrors NIST AI RMF (Govern / Map / Measure / Manage) and the ISO/IEC 23894 process, but the headers are guidance, not law. Add or merge subsections as the system needs.
- Keep identification (§4) and scoring (§5) separate even under time pressure — collapsing them is how risks get dropped.
- The single non-negotiable discipline is the outward view: §3 must name the people affected who are *not* users. If §3 only lists operators and users, the assessment is incomplete.
- This is a living document. Set "Next Review Due" in the metadata and treat the revision history (§12) as the proof you kept it current.

**For regulated/safety-critical projects:** use the full ISO/IEC 23894:2023, the complete NIST AI RMF and Generative AI Profile, and a qualified legal review of the EU AI Act (including Art. 27 FRIA and Annex IV) and the Colorado AI Act — not this lightweight version. This template is a skeleton for solo/small-team use and is not a substitute for the full standards or for legal advice.
