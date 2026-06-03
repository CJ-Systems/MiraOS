# AI System Description (Model Card) Template

> **Template purpose:** Lightweight model-card-style structure for describing a whole AI system — its intended use, the models it depends on, the data that shaped it, how it performs, and where it should not be trusted. Inspired by the public "Model Cards for Model Reporting" pattern and the organization of ISO/IEC 23053:2022, ISO/IEC 22989:2022, and ISO/IEC TR 24028:2020, with metadata mapped loosely onto the EU AI Act Annex IV technical-documentation list. Replace `{{placeholder}}` content with system-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When you are shipping, sharing, or reviewing an AI/ML system and need one honest document that tells a reader what it does, how it was built, how well it works, and where it breaks. Useful whether you trained a model yourself or — the common case — only call a third-party model via API. Pairs with the SRS (what the system must do) and the Architecture Description (how it is built); this card focuses on the AI/ML-specific facts a user, reviewer, or regulator needs to judge fitness and risk.
>
> **Companion standard:** ISO/IEC 23053:2022 (framework for AI systems using ML) + ISO/IEC 22989:2022 (AI concepts and terminology) + ISO/IEC TR 24028:2020 (trustworthiness in AI); cross-referenced to EU AI Act Annex IV (technical documentation).
>
> **Status of this template:** Lightweight skeleton assembled from public summaries of its companion standards — ISO/IEC 23053:2022, ISO/IEC 22989:2022, and ISO/IEC TR 24028:2020 are all paywalled ISO standards, so section structure and field names here are paraphrased/derived independently and reproduce no normative text. The model-card framing draws on the publicly available "Model Cards for Model Reporting" pattern (Mitchell et al., 2019), and the metadata maps loosely onto the publicly published EU AI Act Annex IV technical-documentation list. For regulated or high-risk AI deployments, verify against the full ISO standards and the authoritative EU AI Act text — this template is an organizing aid, not a compliance instrument.

---

# AI System Description (Model Card) — {{System Name}}

| Field | Value |
|---|---|
| Document ID | AISD-{{SYSTEM-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC 23053:2022 + ISO/IEC 22989:2022 + ISO/IEC TR 24028:2020 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| System type | {{LLM-based assistant / classifier / RAG pipeline / agentic system / ...}} |
| Primary model(s) | {{e.g. third-party foundation model via API / fine-tuned open-weights model / from-scratch}} |
| Training posture | {{None — inference only against vendor model / Fine-tuned / Trained from scratch}} |
| Risk classification | {{Self-assessed risk tier, e.g. minimal / limited / high per EU AI Act framing — note this is self-assessment, not certification}} |
| Reviewed by | {{Name / role of human reviewer, or 'unreviewed draft'}} |
| Review date | {{YYYY-MM-DD}} |

---

## 1. Introduction

> This document is a **model card** for {{System Name}} — a short, structured description of an AI system so that a reader can judge whether it fits their use, how it was built, how it performs, and where it should not be used. The "model card" idea comes from a 2019 research paper (Mitchell et al., *Model Cards for Model Reporting*); this template extends it from a single model to a whole **AI system** — the model *plus* everything around it: the data pipeline, prompts, tools, guardrails, and whoever (or whatever) consumes the output. Read this section to orient before the detail: it states why the card exists, what the system is and is not, the vocabulary you need to read the rest correctly, and the documents this card depends on.

{{This document is a model-card-style description of {{System Name}}. It covers the system's intended use, the models it depends on, the data sources and pipeline that shaped it, its runtime components, how it has been evaluated, its limitations, and its trustworthiness posture. It is written for the people who need to judge the system: end users deciding whether to rely on it, reviewers and auditors assessing risk, and — where applicable — regulators checking technical documentation.}}

### 1.1 Purpose

> One paragraph: why this document exists and who reads it. A model card earns trust by being honest about limits, not by looking impressive — name the audiences (users, reviewers, regulators) so the level of detail is calibrated to them.

{{This card exists so that {{audiences}} can make an informed decision about {{System Name}} without reading its source code. It documents what the system is built and validated to do, where it must not be relied upon, and the evidence behind any performance claim. Its readers are: {{end users / integrators / internal reviewers / external auditors / regulators}}.}}

### 1.2 Scope

> Define what the system IS and IS NOT, and state exactly which version or release this card describes. A model card is only trustworthy if it tracks a specific live system — a card describing "the system in general" describes nothing.

**{{System Name}} is** {{a one-sentence description of the system — e.g. an LLM-based assistant that drafts replies from a knowledge base}}.

**{{System Name}} is NOT** {{the boundary — e.g. not a decision-maker, not a source of legal/medical advice, not a replacement for human review}}.

**This card describes** release / version {{X.Y}} of the system, as deployed on {{YYYY-MM-DD}}. Behavior of earlier or later releases may differ; see §13 Revision History.

### 1.3 Definitions and Acronyms

> Define every term a beginner could misread. Below are the foundational terms this template assumes; replace or extend with system-specific vocabulary. Keep definitions plain — the goal is that someone new to formal AI documentation can read the rest of the card without a glossary open in another tab.

| Term | Definition |
|---|---|
| Model card | A short, structured document describing an AI/ML model (or system) so readers can judge whether it fits their use — what it does, how it was built, how it performs, where it should not be used. |
| Model | The trained artifact itself (e.g. an LLM, a classifier) — the thing that takes an input and produces an output. |
| AI system | The model *plus* everything around it: data pipeline, prompts, tools, guardrails, and the human or software that consumes the output. This card describes the whole system, not just the model. |
| Inference | Running a finished model to get an output. (Contrast: *training*, which builds a model from data.) |
| Training | Building a model from data. Many systems do no training at all. |
| Fine-tuning | Adjusting an already-trained model by training it further on extra data. |
| Foundation / third-party model | A large pre-trained model (e.g. an LLM accessed via API) that you use but did not train. |
| Bias | Systematic skew in a model's behavior that disadvantages some groups or inputs. |
| Provenance | Where a data source came from, who owns it, and what consent/licensing applies. |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> List the documents this card depends on or cross-references. If you consume a third-party model, include the *vendor's own model card* — it carries facts about the model you are accountable for citing but did not produce.

Foundational / internal documents:
- {{path/to/srs.md}} — Software Requirements Specification (what the system must do).
- {{path/to/architecture.md}} — Architecture Description (how the system is built).
- {{path/to/doc.md}} — {{brief description}}

Vendor / model documentation (if a third-party model is used):
- {{vendor model card URL}} — {{model name + version}}, the upstream card for the foundation model this system calls.

Companion standards (paywalled unless noted):
- ISO/IEC 23053:2022 — Framework for AI systems using machine learning.
- ISO/IEC 22989:2022 — AI concepts and terminology.
- ISO/IEC TR 24028:2020 — Overview of trustworthiness in AI.
- EU AI Act Annex IV — Technical documentation checklist (publicly published).
- Mitchell et al. (2019), *Model Cards for Model Reporting* (public).

---

## 2. System Overview

> Describe the whole AI system in plain language before drilling into parts. A reader should finish this section able to say, in one or two sentences, what the system does and where the AI/ML sits inside it. State up front the single most-clarifying fact: do you **train**, **fine-tune**, or only run **inference** against a vendor model? That one fact reframes who is accountable for what — if you only call someone else's model, the model's internal behavior is theirs, and your accountability is in the prompts, data, and how you use the output.

{{Plain-language description of {{System Name}}: what it does, who or what it serves, and the high-level flow from input to output. State the system type — {{assistant / classifier / RAG pipeline / agentic system}} — and where the AI/ML component sits inside the larger product (e.g. "the LLM call is one step in a four-stage request pipeline; the rest is deterministic code").}}

**Inputs-to-outputs (one line):** {{e.g. user question + retrieved documents → model call → post-processed answer with citations}}.

**Training posture (state plainly):** {{One of — "No training or fine-tuning performed; the system runs inference against a third-party foundation model via API." / "Fine-tuned an open-weights model on {{dataset}}." / "Trained from scratch on {{dataset}}."}} {{If inference-only: note that the model's internal training data and behavior are governed by the vendor, and this card's accountability centers on prompts, data handling, and use of outputs.}}

---

## 3. Intended Use and Out-of-Scope Use

> The most important section for safety. **Intended use** is what the system is built and validated for; **out-of-scope use** is what you explicitly do *not* support, and **prohibited use** is what could cause harm if someone tried it anyway. Naming the boundaries honestly is what makes the card trustworthy — an empty out-of-scope list is a red flag, not a sign of a safe system. Most real-world harm hides in uses the builder never intended but never ruled out either.

### 3.1 Intended use

> What the system is built and validated for, and the assumptions that hold for that use.

- {{Intended use 1 — e.g. "Drafting first-pass replies to customer support tickets, reviewed by a human before sending."}}
- {{Intended use 2}}

**Intended users:** {{who is meant to operate the system — e.g. internal support agents; not end customers directly}}.

**Operating context / assumptions:** {{where, by whom, and under what conditions — e.g. "English-language tickets; human-in-the-loop on every output; not used for billing or account-deletion decisions."}}

### 3.2 Out-of-scope and prohibited uses

> What you do NOT support (out-of-scope), and what must never be done (prohibited). Be specific; vague disclaimers do not protect anyone.

| Use | Out-of-scope / Prohibited | Why |
|---|---|---|
| {{e.g. Autonomous sending without human review}} | Prohibited | {{e.g. No safeguard against confidently-wrong output reaching a customer}} |
| {{e.g. Legal, medical, or financial advice}} | Out-of-scope | {{Not validated for these domains; outputs may be plausibly wrong}} |
| {{e.g. Non-English input}} | Out-of-scope | {{Untested; performance unknown}} |

---

## 4. Models

> One entry per model the system depends on, tagged **MODEL-1**, **MODEL-2**, etc. If you only call an external model, say so clearly and note that its internal training data and behavior are governed by the vendor, not by you — your job here is to record *which* model, *which* version, and *where the vendor's own card is*. Pinning the version matters: model behavior changes between versions, and a card that names a moving target ("the latest model") is not auditable.

| ID | Name & version | Provider | Build posture | Architecture family | Input limits | Vendor card |
|---|---|---|---|---|---|---|
| MODEL-1 | {{model name + exact version/snapshot}} | {{Vendor / your org}} | {{Used-as-is / Fine-tuned / From-scratch}} | {{e.g. transformer LLM}} | {{context window / max tokens / input size}} | {{URL or "n/a"}} |
| MODEL-2 | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

**MODEL-N notes:** {{For each model — anything a reader must know. If third-party: "Trained and maintained by {{vendor}}; we have no visibility into or control over its training data or weights. We control only how we prompt and consume it." If self-built: cross-reference §6 for training detail.}}

---

## 5. Data Sources and Data Pipeline

> Tag each data source **DATA-1**, **DATA-2**, etc. **Provenance** — where data came from, who owns it, what consent/licensing applies, and whether it is personal or sensitive — is required for both trust and legal/regulatory reasons. Then describe the **data pipeline** (ingestion → cleaning → transformation → storage → retention) so a reader can trace any output back to the data that shaped it. This section feeds directly into privacy (§9 TRUST-N) and the EU AI Act Annex IV data-governance cross-reference. "Personal data" means data about an identifiable person; "sensitive" means special categories (health, biometrics, etc.) that carry extra legal weight — flag both honestly.

### 5.1 Data sources

| ID | What it is | Provenance | License / consent | Personal or sensitive? | Role in system |
|---|---|---|---|---|---|
| DATA-1 | {{e.g. internal support ticket archive}} | {{where it came from / who owns it}} | {{license or consent basis}} | {{None / Personal / Sensitive}} | {{Retrieval corpus}} |
| DATA-2 | {{e.g. product documentation}} | {{...}} | {{...}} | {{None}} | {{Retrieval corpus}} |
| DATA-3 | {{e.g. live user input at runtime}} | {{provided by user at request time}} | {{terms of service}} | {{Personal — may contain PII}} | {{Runtime input}} |

> *Role-in-system values:* training set, fine-tuning set, retrieval corpus, or runtime input. State which — it determines what accountability attaches to the data.

### 5.2 Data pipeline

> Describe the path data takes through the system, so any output is traceable to its inputs.

1. **Ingestion** — {{how data enters: source, frequency, format}}.
2. **Cleaning / validation** — {{what is filtered, normalized, or rejected}}.
3. **Transformation** — {{chunking, embedding, indexing, redaction of PII, etc.}}.
4. **Storage** — {{where it lives; encryption at rest; access controls}}.
5. **Retention / deletion** — {{how long data is kept; how deletion requests are honored}}.

---

## 6. Training and Fine-Tuning Posture

> Document how the model(s) came to behave as they do, and be explicit about **which lever you actually own**. If you train or fine-tune, describe the procedure. If — the common case for LLM-based products — you only run inference against a vendor model, state "no training or fine-tuning performed" plainly, and instead document the behavior-shaping you *do* control: system prompts, tool definitions, retrieval configuration, and guardrails. Claiming control you do not have, or hiding the levers you do have, both make the card untrustworthy.

### 6.1 Posture statement

{{One of — pick and complete:}}

- **Inference-only (no training):** No training or fine-tuning was performed. {{System Name}} runs inference against {{MODEL-1}}, a third-party model. The vendor controls the model's training data and weights. The behavior we shape ourselves is documented in §6.3.
- **Fine-tuned:** We fine-tuned {{base model}} on {{cross-reference DATA-N}}. See §6.2.
- **Trained from scratch:** We trained {{MODEL-1}} from scratch on {{cross-reference DATA-N}}. See §6.2.

### 6.2 Training / fine-tuning detail (if applicable — omit for inference-only)

> Summary-level only; this is a card, not a training log. Cross-reference data sources by DATA-N.

| Item | Value |
|---|---|
| Datasets used | {{DATA-N references}} |
| Objective | {{what the training optimized for}} |
| Hyperparameters (summary) | {{learning rate, epochs, batch size — high level}} |
| Compute | {{hardware / time / approximate cost}} |
| Resulting model | {{which MODEL-N this produced}} |

### 6.3 Behavior-shaping levers we control (the inference-only case)

> For inference-only systems, *this* is where your accountability lives. Be specific.

- **System prompt(s):** {{what instructions are given to the model; where they live; how they are versioned}}.
- **Tool / function definitions:** {{what tools the model can call, and their constraints}}.
- **Retrieval configuration:** {{what is retrieved, from where, how many items, ranking}}.
- **Guardrails:** {{input filters, output validation, refusal rules, rate limits}}.

---

## 7. Inputs, Outputs, and Components

> Describe the **runtime contract**: what inputs the system accepts, what outputs it produces, and the components that connect them. Tag components **COMP-1**, **COMP-2**, etc. The goal is that a reader can follow one request from input to output through the named components — a numbered step list or a small flow diagram is ideal. This section is the "how a request actually flows" complement to the higher-level §2 overview.

### 7.1 Inputs

| Aspect | Specification |
|---|---|
| Accepted input types | {{text / image / structured JSON / ...}} |
| Format & encoding | {{e.g. UTF-8 text, max {{N}} tokens}} |
| Limits / validation | {{size caps, schema, rejected inputs}} |

### 7.2 Outputs

| Aspect | Specification |
|---|---|
| Output form | {{free text / structured data / an action / a score}} |
| Format | {{e.g. JSON with fields {{...}}; cited Markdown}} |
| Guarantees / caveats | {{e.g. "Output is a draft, not a final decision"; "May hallucinate; citations should be checked"}} |

### 7.3 Components and request flow

| ID | Component | Role |
|---|---|---|
| COMP-1 | {{Prompt assembly}} | {{Builds the prompt from input + retrieved context}} |
| COMP-2 | {{Retrieval}} | {{Fetches relevant items from DATA-N}} |
| COMP-3 | {{Model call}} | {{Sends prompt to MODEL-1, receives completion}} |
| COMP-4 | {{Post-processing}} | {{Parses, validates, formats output}} |
| COMP-5 | {{Guardrails}} | {{Applies safety / policy checks before returning}} |

**One request, end to end:**
1. {{Input arrives at COMP-1 ...}}
2. {{COMP-2 retrieves ...}}
3. {{COMP-3 calls MODEL-1 ...}}
4. {{COMP-4 post-processes ...}}
5. {{COMP-5 checks, then the output is returned.}}

---

## 8. Stakeholders and Affected Parties

> Tag each stakeholder **STK-1**, **STK-2**, etc. List who builds, operates, uses, and is *affected by* the system — including people who never touch it directly but whose data or outcomes it shapes. Distinguishing **direct users** from **indirectly-affected parties** is where most overlooked harm lives: a support agent uses the system, but the customer whose ticket it answers is affected by it without ever seeing it. ISO/IEC 22989 treats the affected-party view as first-class, not an afterthought.

| ID | Stakeholder | Relationship | What's at stake for them |
|---|---|---|---|
| STK-1 | {{e.g. Support agents}} | Direct user | {{Workload, accountability for sent replies}} |
| STK-2 | {{e.g. Customers}} | Indirectly affected | {{Quality of the answer they receive; their PII in DATA-3}} |
| STK-3 | {{e.g. Operators / on-call}} | Operates the system | {{Availability, incident response}} |
| STK-4 | {{e.g. Compliance / legal}} | Oversight | {{Regulatory exposure, audit}} |

---

## 9. Evaluation and Performance

> Pair **every** result with the test that produced it — a number with no test attached is meaningless. Tag results **EVAL-N** and record: what was tested, on what dataset/benchmark, with what metric, under what conditions, then the result. Include **disaggregated** results (broken out by group or input type) where possible, because an aggregate number can hide poor performance on a subgroup. If you rely on a vendor model you did not evaluate yourself, mark clearly which figures are the **vendor's claims** versus your **own measurements** — they carry very different weight.

| ID | What was tested | Dataset / benchmark | Metric | Conditions | Result | Source |
|---|---|---|---|---|---|---|
| EVAL-1 | {{e.g. Draft accuracy}} | {{held-out ticket set, n={{N}}}} | {{e.g. human-rated usefulness 1–5}} | {{human-in-the-loop}} | {{e.g. mean 4.1}} | Own measurement |
| EVAL-2 | {{e.g. Disaggregated by topic}} | {{same set, split by category}} | {{same}} | {{...}} | {{e.g. 4.4 billing / 3.2 technical}} | Own measurement |
| EVAL-3 | {{e.g. Base model reasoning}} | {{vendor benchmark}} | {{vendor metric}} | {{vendor conditions}} | {{vendor figure}} | Vendor claim |

**Disaggregation note:** {{Which groups/input-types were broken out, and any subgroup where performance is notably worse. If not disaggregated, say so and flag it as an OQ in §12.}}

---

## 10. Trustworthiness Considerations

> Walk the ISO/IEC TR 24028 trustworthiness characteristics — the qualities that make an AI system worthy of trust — and record where {{System Name}} stands on each, tagged **TRUST-N**. The standard frames these as things to *assess*, not boxes to tick. Honest "we have not assessed this yet" entries are better than silence: the point is a truthful map, not a clean scorecard. Cross-reference data sources (DATA-N), limitations (LIM-N), and evaluations (EVAL-N) rather than repeating them.

| ID | Characteristic | Where {{System Name}} stands |
|---|---|---|
| TRUST-1 | Reliability & robustness | {{Does it degrade gracefully on odd/adversarial input? What happens on malformed input or model timeout?}} |
| TRUST-2 | Safety | {{What harm could an output cause; what prevents it}} |
| TRUST-3 | Transparency & explainability | {{Can a user tell why an output was produced? Are citations / reasoning shown?}} |
| TRUST-4 | Bias & fairness | {{Known skews and their sources — training data, model, or deployment. Cross-ref EVAL-2 disaggregation.}} |
| TRUST-5 | Privacy | {{How personal data is protected. Cross-ref DATA-N and §5.2 retention.}} |
| TRUST-6 | Security | {{Prompt injection, data leakage, model misuse — threats and mitigations}} |

---

## 11. Limitations and Known Risks

> The counterpart to §3 Intended Use: it tells a reader exactly *when not to trust an output*. Tag each limitation **LIM-1**, **LIM-2**, etc.: failure modes, conditions under which the system performs poorly, known error patterns, and risks that remain after mitigation. Pair each with any mitigation/guardrail and the **residual risk** that still stands. Reviewers and regulators read this section most closely — a thorough limitations section signals a mature system, not a weak one.

| ID | Limitation / risk | Conditions / trigger | Mitigation | Residual risk |
|---|---|---|---|---|
| LIM-1 | {{e.g. Hallucinated facts}} | {{outside the retrieval corpus}} | {{citations required; human review}} | {{Confident-but-wrong output may still pass review}} |
| LIM-2 | {{e.g. Poor on non-English input}} | {{non-English tickets}} | {{language detection rejects them}} | {{Mis-detected language slips through}} |
| LIM-3 | {{e.g. Vendor model change}} | {{vendor updates MODEL-1}} | {{version pinning where possible}} | {{Pin may lag; behavior can shift}} |

---

## 12. Open Questions

> Tag open questions **OQ-1**, **OQ-2**, etc. — evaluations not yet run, trustworthiness characteristics not yet assessed, data-provenance gaps still being chased, or risk-classification calls still pending. For each, note what is blocking resolution and who needs to decide. An open question parked here honestly is a strength; an unstated one is a liability. Resolve and remove entries as the system matures.

- **OQ-1:** {{question}} — {{what's blocking, who needs to decide}}
- **OQ-2:** {{question}} — {{...}}

---

## 13. Revision History

> A table of every substantive change to this card — version, date, author, and a short description — so readers can see how the system's description (and the system itself) evolved. Bump the version whenever models, data sources, intended use, or evaluation results change: a model card is only trustworthy if it tracks the live system.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 System Overview
- §3 Intended Use and Out-of-Scope Use (the safety core — an empty out-of-scope list is a red flag)
- §4 Models
- §5 Data Sources and Data Pipeline
- §7 Inputs, Outputs, and Components
- §11 Limitations and Known Risks
- §13 Revision History

**Optional sections** (include if relevant):
- §6 Training and Fine-Tuning Posture — always include the one-line posture statement; the detailed §6.2 table is omitted for inference-only systems.
- §8 Stakeholders and Affected Parties — strongly recommended for any system that affects people indirectly.
- §9 Evaluation and Performance — include as soon as you have any measurement; if you have none yet, say so and log it as an OQ rather than omitting.
- §10 Trustworthiness Considerations — recommended for any system touching personal data, decisions about people, or safety.
- §12 Open Questions — track elsewhere if you prefer, but honesty about gaps belongs somewhere.

**Tailoring**:
- The section organization follows the companion standards' framing but is paraphrased for solo/small-team use; add or remove subsections as your system needs.
- The single most-clarifying fact is the **training posture** (§2, §6). State it early and plainly — inference-only against a vendor model is the common case and reframes who is accountable for what.
- Use the traceability prefixes so this card can cross-reference (and be referenced from) the SRS, Architecture Description, and Risk/Test documents:
  - **MODEL-N** — models the system depends on
  - **DATA-N** — data sources
  - **COMP-N** — runtime components
  - **STK-N** — stakeholders and affected parties
  - **EVAL-N** — evaluation results
  - **TRUST-N** — trustworthiness considerations
  - **LIM-N** — limitations and known risks
  - **OQ-N** — open questions
- The metadata table and §3/§5/§9/§10 are organized so they map loosely onto the EU AI Act Annex IV technical-documentation list (system description, design, data governance, monitoring, performance) — this is a cross-reference aid, not legal compliance in itself.
- Revision history is mandatory. Re-version the card whenever models, data, intended use, or evaluation results change.

**For regulated/safety-critical projects:** use the full ISO/IEC 23053:2022, ISO/IEC 22989:2022, and ISO/IEC TR 24028:2020 standards and the authoritative EU AI Act text, not this lightweight version. This template is an organizing aid suitable for solo/small-team projects, internal documentation, and early-stage products — it is not a compliance instrument.
