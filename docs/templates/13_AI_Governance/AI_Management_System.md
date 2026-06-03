# AI Management System (AIMS) Description Template

> **Template purpose:** Lightweight AI Management System (AIMS) Description structure inspired by ISO/IEC 42001:2023 (the management system standard for artificial intelligence), arranged on the ISO Annex SL harmonized 10-clause skeleton it shares with ISO/IEC 27001:2022. Use this template when you want to write down, in one place, how your organization governs the AI it builds or operates — its policy, objectives, controls, and review loop — so that the system can be audited and improved rather than run ad hoc. Replace `{{placeholder}}` content with your own text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When you decide to put deliberate governance around AI work — whether to prepare for certification, to satisfy a customer or regulator who is asking how you manage AI, or simply because "we'll keep it responsible" has stopped being a good enough answer. Start one as soon as you have at least one AI system worth governing. The AIMS Description is the "how do we run AI responsibly, and prove it" document; it complements the SRS (what a system does), the SDD (how it's designed), and the Risk Management Plan (what could go wrong).
>
> **Companion standard:** ISO/IEC 42001:2023 (AI management system); ISO/IEC 27001:2022 Annex SL harmonized structure (cross-reference). The clauses 4–10 used below mirror the shared Annex SL skeleton, so an organization already familiar with 27001 will recognize the shape.
>
> **Status of this template:** Lightweight skeleton assembled from public summaries of ISO/IEC 42001:2023 and the ISO/IEC 27001:2022 Annex SL harmonized structure. ISO standards are paywalled and copyrighted; no normative text is reproduced here — clause intents are paraphrased only. Verify all clause numbering, Annex A control selection, and Statement-of-Applicability requirements against the full purchased standard before relying on this for an actual certification audit. Suitable for solo/small-team certification-readiness planning, not as a substitute for the standard itself.

---

# AI Management System (AIMS) Description — {{System Name}}

| Field | Value |
|---|---|
| Document ID | AIMS-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC 42001:2023 (+ ISO/IEC 27001:2022 Annex SL structure) (lightweight) |
| Owner | {{Project name or AIMS owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| AIMS Scope Statement | {{What AI systems, processes, sites, and boundaries the AIMS covers}} |
| Organizational Role re: AI | {{Provider / Developer / Deployer / User — per 42001 role taxonomy}} |
| Certification Target | {{None / Readiness only / Stage 1 / Stage 2 — and target date}} |
| Statement of Applicability Ref | {{Link or doc ID of the SoA register}} |
| Last Management Review | {{YYYY-MM-DD or 'not yet held'}} |

---

## 1. Introduction

> This document describes your organization's **AI Management System (AIMS)** — the documented, repeatable way you govern the AI you build or operate. Two terms to fix up front, because the rest of the document leans on them:
>
> - A **management system** is a documented, repeatable way of running an activity so it can be audited and improved, not just done once and forgotten. ISO has management-system standards for quality (9001), information security (27001), and now AI (42001).
> - An **AIMS** is the 42001 management system specifically for governing AI: policy, objectives, controls, and review all working together as one repeating cycle.
>
> This section covers four things: **Purpose** (why the AIMS exists and what this document specifies), **Scope** (which AI systems, processes, and organizational boundaries are in and out — this becomes the formal scope statement an auditor checks first), **Definitions** (the plain-language vocabulary the document relies on), and **References** (the standard, related policies, prior specs, and any regulatory drivers). Sections 4–10 below follow the **Annex SL** structure — the shared 10-clause skeleton ISO uses across its management-system standards (42001, 27001, 9001) so they fit together. Clauses 1–3 are scope/normative-references/terms; the real content lives in clauses 4–10.

### 1.1 Purpose

> One paragraph: what this document is for. State that it describes how AI is GOVERNED (policy, objectives, controls, review) — not what any single AI system does (that's the SRS) or how it's designed (that's the SDD).

{{This document describes the AI Management System (AIMS) for {{System Name}}: the policy, objectives, controls, and review loop by which {{the organization}} governs the AI it builds and/or operates. Its purpose is to make AI governance deliberate, documented, and auditable, and to establish readiness for assessment against ISO/IEC 42001:2023. It does not specify what any individual AI system does (see the relevant Software Requirements Specification) or how it is designed (see the relevant Software Design Description).}}

### 1.2 Scope

> Define what the AIMS covers and what it does not — this is the single most important boundary in the document, because everything else (controls, audits, the Statement of Applicability) references it, and an auditor checks it first. Be concrete: name the AI systems, the processes, the sites/environments, and the organizational units in scope. State exclusions explicitly and say why. Also record your organizational role re: AI (below) — your obligations differ depending on whether you build the model, deploy someone else's, or just use one.

In scope:
- AI systems: {{name the in-scope AI systems / models / features}}
- Processes: {{e.g., development, data handling, deployment, monitoring}}
- Sites / environments: {{e.g., the production environment, the dev laptop, the cloud account}}
- Organizational units: {{e.g., "the whole company (solo)" / "the ML team"}}

Out of scope (with reason):
- {{What is explicitly excluded and why — e.g., "internal experimental notebooks never shipped to users"}}

Organizational role re: AI: {{Provider / Developer / Deployer / User — 42001 distinguishes these because obligations differ. A *developer/provider* builds or supplies an AI system; a *deployer* puts someone else's AI into use under their own responsibility; a *user* simply uses it. State which you are for each in-scope system; you may be more than one.}}

### 1.3 Definitions and Acronyms

> Define the load-bearing vocabulary plainly. The terms below are pre-filled because later sections depend on them — keep these, edit if your organization uses a word differently, and add your own project terms at the bottom. A reader who understands these can read the whole document.

| Term | Definition |
|---|---|
| Management system | A documented, repeatable way of running an activity (here, building/operating AI) so it can be audited and improved, not just done ad hoc. The "system" is the policy + objectives + controls + review working together. |
| AIMS (AI Management System) | The ISO/IEC 42001 management system specifically for governing AI: policy, objectives, controls, and review operating as one cycle. |
| Annex SL / harmonized structure | The shared 10-clause skeleton ISO uses across management-system standards (42001, 27001, 9001) so they fit together. Clauses 4–10 carry the real content; this document's §§2–10 map onto them. |
| PDCA (Plan-Do-Check-Act) | The improvement loop the standard is built around: **Plan** the system, **Do** (run it), **Check** it (audit and review), **Act** on what you find. The AIMS is meant to turn this loop continuously, not be written once. |
| Statement of Applicability (SoA) | The central register listing each Annex A control, whether you apply it, and why it is included or excluded. It is the auditor's primary checklist (see §6). |
| Annex A controls vs Annex B guidance | **Annex A** is the list of control objectives and controls you select from. **Annex B** explains how to implement them. You decide applicability against Annex A; you take implementation help from Annex B. |
| AI risk assessment vs AI system impact assessment | **Risk assessment** asks "what could go wrong *for us / for the system*?" and protects the organization. **Impact assessment (AIIA)** looks *outward* at effects on individuals, groups, and society. 42001 requires both (see §5). |
| Interested parties (stakeholders) | Anyone with a stake in your AI: users, the people affected by its outputs, regulators, customers, and the development team. |
| Nonconformity / corrective action | A **nonconformity** is a place where reality doesn't match the documented system. The **corrective action** is the recorded fix plus handling of the root cause so it doesn't recur (see §9). |
| Internal audit vs management review | An **internal audit** checks the system against the standard. A **management review** is the recorded meeting where leadership decides what to change based on the evidence. Both produce records an external auditor will want (see §8). |
| Certification readiness | Having the documented system, records, and evidence in place so an external auditor can assess conformance — whether or not you actually pursue the certificate. |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> Foundational documents and standards this AIMS depends on or points to. Categorize for readability. Include any regulatory drivers (e.g., an AI regulation a customer must comply with) since those often dictate which controls become mandatory.

External standards:
- ISO/IEC 42001:2023 — AI management system (companion standard for this document).
- ISO/IEC 27001:2022 — Information security management system (shares the Annex SL structure; cross-reference if you also run an ISMS).
- {{Any regulatory driver — e.g., a regional AI regulation a customer is subject to}}.

Project / organizational documents:
- {{path/to/soa.md}} — Statement of Applicability register (see §6).
- {{path/to/srs.md}} — requirements for the in-scope AI system(s).
- {{path/to/risk.md}} — Risk Management Plan (AI risks often live here; cross-reference RISK-N).
- {{path/to/ai-policy.md}} — the signed AI Policy (see §3), if held separately.
- ADR-NNNN — {{decision relevant to AI governance}}.

---

## 2. Context of the Organization

> This is **clause 4** of the harmonized structure, and it sets up everything else. In plain terms: write down *who cares about your AI, what they expect, and exactly which AI systems and activities the management system governs.* That last part — the boundary — is what every later section references, so getting it precise here saves confusion downstream. There are three pieces: internal/external issues, interested parties and their needs, and the AIMS scope (which you may carry up from §1.2 and refine here).

### 2.1 Internal and External Issues

> The conditions that shape your AI work. **Internal** issues: your skills, resources, existing systems, culture, how AI fits your business. **External** issues: the market, applicable laws and regulations, the expectations of the field, what your competitors and customers are doing. The point is to surface the forces that make some risks and controls relevant to *you* specifically.

Internal issues:
- {{e.g., "single developer; limited time for formal process"}}
- {{e.g., "AI feature is core to the product, not a side experiment"}}

External issues:
- {{e.g., "customers in a regulated sector ask how we govern AI"}}
- {{e.g., "an applicable AI regulation is coming into force in {{region}}"}}

### 2.2 Interested Parties and Their Needs

> List the **interested parties** (stakeholders) and what each expects from your AI. Include the people *affected by* the AI's outputs, not just the people who buy or use it — that outward view is what distinguishes responsible-AI governance from ordinary product management. Use ROLE-N elsewhere for *internal* roles; here, capture *external and affected* parties too.

| Interested party | What they need / expect | Why it matters to the AIMS |
|---|---|---|
| {{Users}} | {{Reliable, transparent behavior; to know they're interacting with AI}} | {{Drives transparency control CTRL-N}} |
| {{People affected by outputs}} | {{Not to be harmed or unfairly treated}} | {{Drives impact assessment IMP-N}} |
| {{Customers}} | {{Evidence we govern AI responsibly}} | {{Drives certification target}} |
| {{Regulators}} | {{Compliance with applicable AI law}} | {{Drives mandatory controls}} |
| {{Development team}} | {{Clear policy and workable process}} | {{Drives competence/awareness §7}} |
| ... | ... | ... |

### 2.3 Determining the AIMS Scope

> Restate (and refine) the boundary from §1.2: the exact set of AI systems, processes, sites, and organizational units the AIMS governs, plus your role(s) re: AI. Note any interfaces or dependencies that cross the boundary (e.g., a third-party model you call). This becomes the formal scope statement the auditor checks first; make it unambiguous.

{{The AIMS covers {{in-scope systems/processes/sites}}. Boundaries and interfaces: {{e.g., "the AIMS governs our use of third-party model X but not X's internal development, which is the provider's responsibility"}}. Organizational role(s): {{Provider / Developer / Deployer / User}}.}}

---

## 3. Leadership and AI Policy

> This is **clause 5**. Two things live here: a demonstrated commitment from whoever leads the organization (for a solo founder, that's you — and it still counts), and the **AI Policy** itself. The policy is the short, signed statement of intent — "we commit to responsible, transparent, accountable AI…" — that every later section operationalizes. Treat it as the constitution the rest of the AIMS implements: brief, principled, signed, and dated. List individual commitments as **POL-N** so objectives (OBJ-N) and controls (CTRL-N) can be traced back to the policy they serve.

### 3.1 Leadership Commitment

> How leadership shows the AIMS is real, not decorative: providing resources, setting direction, holding the management review (§8), and making AI governance part of how decisions get made. For a solo/small-team project, this is short but should still be explicit — name who is accountable.

{{Leadership commitment to the AIMS is demonstrated by {{e.g., allocating time/budget, owning the policy, chairing the management review}}. Accountable leader: {{name / role}}.}}

### 3.2 AI Policy

> The signed statement of intent. Keep it short and principled. Each numbered statement is a commitment the rest of the document must implement and an auditor can trace. State that it aligns with the organization's purpose and values, and record approval (who signed, when).

The organization commits to the following AI Policy statements:

| ID | Policy statement | Implemented by |
|---|---|---|
| POL-1 | {{e.g., "We develop and operate AI responsibly, lawfully, and in line with our stated values."}} | {{OBJ-N / CTRL-N}} |
| POL-2 | {{e.g., "We are transparent with users about when they are interacting with AI and about its limitations."}} | {{CTRL-N (transparency)}} |
| POL-3 | {{e.g., "We keep meaningful human oversight over consequential AI decisions."}} | {{CTRL-N (human oversight)}} |
| POL-4 | {{e.g., "We assess and act on the impact of our AI on people and society, not only on the organization."}} | {{IMP-N}} |
| POL-N | {{Statement}} | {{Trace}} |

Policy alignment and approval: {{One line on how the policy aligns with the organization's purpose and values.}} Approved by {{name / role}} on {{YYYY-MM-DD}}.

---

## 4. Roles, Responsibilities, and Authorities

> This is the **clause 5.3** assignment: who owns what in the AIMS, named and authorized. The whole point is that an auditor can ask "who is accountable for X?" and get a named, authorized answer rather than a vague "the team." Use a **RACI-style** table — RACI is a simple way to record, per responsibility, who is **R**esponsible (does the work), **A**ccountable (owns the outcome — exactly one person), **C**onsulted, and **I**nformed. For a solo project, most cells collapse to one name; keep the rows anyway so the responsibilities don't silently disappear. Use **ROLE-N** identifiers so other documents can reference a role.

| ID | Role | Key responsibilities | R / A / C / I assignment (who) |
|---|---|---|---|
| ROLE-1 | AIMS owner | Overall accountability for the management system; chairs management review | A: {{name}} |
| ROLE-2 | AI risk owner | Owns the AI risk register; drives treatment (cross-ref RISK-N) | A: {{name}} |
| ROLE-3 | Control owner(s) | Operates and evidences assigned Annex A controls (CTRL-N) | R: {{name(s)}} |
| ROLE-4 | Internal audit lead | Plans and runs internal audits independently of the work audited | A: {{name}} |
| ROLE-5 | Management-review participants | Review evidence and decide changes | C/I: {{names / roles}} |
| ROLE-N | {{Role}} | {{Responsibilities}} | {{R/A/C/I}} |

> **Solo-project note:** {{If one person fills every role, say so — and note any tooling that stands in for a role (e.g., "automated evaluation stands in for an independent test reviewer"). Audit independence is the one place a true solo project should be honest about its limits: self-audit is weaker evidence than an independent check, and an external auditor will know it.}}

---

## 5. Planning: AI Objectives, Risks, and Impacts

> This is **clause 6**, and it carries the part of 42001 that ordinary software governance often misses. Three things: measurable **AI objectives** (what the AIMS is trying to achieve), an **AI risk assessment** (what could go wrong *for us / for the system*), and an **AI system impact assessment** (who our AI could *harm*, and how). The distinction matters and the standard requires both: risk assessment protects the organization; impact assessment looks outward at people and society. Use **OBJ-N** for objectives (parallels the Project Management template), **RISK-N** for risks (cross-reference your Risk Management Plan rather than duplicating the full register), and **IMP-N** for impact findings.

### 5.1 AI Objectives

> Measurable outcomes the AIMS aims for — and how you'll know you got there. Tie each to a policy statement (POL-N). "Measurable" need not mean a fancy metric; it means there's a clear way to check progress. State the target and how it's measured.

| ID | Objective | Serves policy | How measured | Target |
|---|---|---|---|---|
| OBJ-1 | {{e.g., "Every in-scope AI feature has a current impact assessment."}} | {{POL-4}} | {{% of features with an IMP record}} | {{100% before release}} |
| OBJ-2 | {{e.g., "Users are clearly told when they interact with AI."}} | {{POL-2}} | {{transparency review pass/fail}} | {{Pass at each release}} |
| OBJ-N | {{Objective}} | {{POL-N}} | {{measure}} | {{target}} |

### 5.2 AI Risk Assessment and Treatment

> The inward view: what could go wrong for the organization or the system, how likely, how bad, and what you'll do about it. Keep the *process* description here and the living register in your Risk Management Plan; reference rows by **RISK-N**. State the method briefly (how you rate likelihood/impact and decide treatment) so an auditor can see it's repeatable, not improvised. (See the Risk Management Plan template for the full register and the avoid/mitigate/transfer/accept strategies.)

{{AI risks are identified, analyzed (likelihood × impact), and treated using the process in `{{path/to/risk.md}}`. The AI risk owner (ROLE-2) maintains the register.}}

| ID | AI risk (summary) | Treatment | Status | Full row |
|---|---|---|---|---|
| RISK-1 | {{e.g., "Model produces biased outputs across user groups"}} | {{Mitigate}} | {{Open}} | {{risk.md#RISK-1}} |
| RISK-2 | {{e.g., "Third-party model changes behavior without notice"}} | {{Mitigate / monitor}} | {{Open}} | {{risk.md#RISK-2}} |
| RISK-N | {{Summary}} | {{Strategy}} | {{Status}} | {{ref}} |

### 5.3 AI System Impact Assessment (AIIA)

> The outward view, and the one most likely to be skipped: not "what could go wrong for us" but "who could our AI **harm**, and how?" Look at effects on individuals, groups, and society — fairness, safety, dignity, autonomy, the consequences of being wrong about a real person. Record each finding as **IMP-N** with the affected party, the potential impact, and what you'll do to prevent or reduce it (which usually links to a control, CTRL-N, or a risk, RISK-N).

| ID | Affected party / context | Potential impact | Likelihood / severity | Response (control / mitigation) |
|---|---|---|---|---|
| IMP-1 | {{e.g., applicants screened by the AI}} | {{e.g., unfair rejection due to biased training data}} | {{Med / High}} | {{CTRL-N bias testing + human review}} |
| IMP-2 | {{e.g., a user acting on a confident wrong answer}} | {{e.g., real-world harm from a hallucinated instruction}} | {{Med / High}} | {{CTRL-N disclaimers + human oversight}} |
| IMP-N | {{Party}} | {{Impact}} | {{rating}} | {{response}} |

---

## 6. Statement of Applicability and Operational Controls

> This is the **heart of certification readiness**. The **Statement of Applicability (SoA)** is a register that lists *every* Annex A control, records whether you apply it, and justifies the decision either way. It is the auditor's master checklist: every Annex A control must be *consciously* included with reasoning or excluded with reasoning — "we never thought about it" is the one answer that fails. (Annex A is the catalog of controls; Annex B explains how to implement them — take the help from B, make the applicability decision against A.) For each control you *do* apply, this section also says how it's actually operationalized — which spills into **clause 8** territory (data governance, transparency to users, human oversight, lifecycle management, third-party/supplier controls). Use **CTRL-N** IDs so risks (RISK-N) and impacts (IMP-N) can point at the control that addresses them.

### 6.1 Statement of Applicability (SoA) Register

> One row per Annex A control. Record the control reference (from the standard's Annex A — fill these in against the purchased standard; do not copy the control text here), your applicable/not-applicable decision, the justification, and the implementation status. Keep this register current — it is the document an auditor opens first after the scope statement.

| ID | Annex A control ref | Control (short, your wording) | Applicable? | Justification | Implementation status |
|---|---|---|---|---|---|
| CTRL-1 | {{A.x.x}} | {{Data governance for AI}} | {{Yes}} | {{Required by RISK-1, IMP-1}} | {{Implemented / Partial / Planned}} |
| CTRL-2 | {{A.x.x}} | {{Transparency to users}} | {{Yes}} | {{Required by POL-2, IMP-2}} | {{Implemented}} |
| CTRL-3 | {{A.x.x}} | {{Human oversight of decisions}} | {{Yes}} | {{Required by POL-3}} | {{Partial}} |
| CTRL-4 | {{A.x.x}} | {{Third-party / supplier controls}} | {{Yes}} | {{Required by RISK-2}} | {{Planned}} |
| CTRL-5 | {{A.x.x}} | {{e.g., a control irrelevant to your context}} | {{No}} | {{Not applicable because {{reason — e.g., "we do not train models, only deploy"}}}} | {{N/A}} |
| CTRL-N | {{A.x.x}} | {{Control}} | {{Yes/No}} | {{Why included or excluded}} | {{status}} |

> **Reminder:** every Annex A control needs a row — including the ones you exclude. An excluded control with a clear "not applicable because…" is fine; an Annex A control with *no* row is the gap that fails an audit.

### 6.2 How Applied Controls Are Operationalized (clause 8 operation)

> For the controls marked applicable, describe how they actually run day to day. These are the operational details an auditor asks to *see evidence of*, not just read about. Group by the common AI control areas; tie each back to its CTRL-N.

- **Data governance** ({{CTRL-N}}): {{how training/input data is sourced, documented, quality-checked, and handled for privacy}}.
- **Transparency to users** ({{CTRL-N}}): {{how users are told they're interacting with AI and informed of its limitations}}.
- **Human oversight** ({{CTRL-N}}): {{where a human reviews or can override consequential AI outputs}}.
- **Lifecycle management** ({{CTRL-N}}): {{how systems are governed from requirements through decommissioning — expanded in §8}}.
- **Third-party / supplier controls** ({{CTRL-N}}): {{how external models/components/vendors are assessed and contractually controlled}}.
- {{Other applied control areas}}: {{operational description}}.

---

## 7. Support: Resources, Competence, Awareness, and Documented Information

> This is **clause 7** — the support layer that keeps the AIMS running. In plain terms it answers: *do the people doing AI work know the policy, have the skills, and keep records under control?* Four pieces: resources, competence, awareness/communication, and **documented information** (document control). That last piece includes *this document and the SoA themselves* — a management system is expected to control its own records (versioned, approved, retained), and an auditor will check that you practice what you preach.

### 7.1 Resources

> The people, time, tools, and infrastructure the AIMS needs to operate. For a solo project this is mostly your own time plus whatever tooling supports the controls; write it down so the commitment is real.

{{Resources allocated to the AIMS: {{time, people, tooling, infrastructure}}.}}

### 7.2 Competence

> The skills the people doing in-scope AI work need, how you ensure they have them, and the evidence. "Competence" here means demonstrable ability, not just good intentions.

| Role (ROLE-N) | Competence needed | How ensured | Evidence |
|---|---|---|---|
| {{ROLE-N}} | {{e.g., understands bias testing}} | {{training / experience}} | {{record}} |
| ... | ... | ... | ... |

### 7.3 Awareness and Communication

> How the people involved know the AI Policy and their part in it, and how AIMS matters are communicated (internally and, where relevant, to interested parties from §2.2).

{{How awareness is maintained (e.g., policy acknowledged at onboarding) and how AIMS communication happens.}}

### 7.4 Documented Information (document control)

> How AIMS documents — including this one and the SoA — are versioned, approved, retained, and protected from uncontrolled change. State where they live, who approves changes, and how old versions are kept. Document control is itself an audited requirement.

{{AIMS documents are version-controlled in {{tool/location}}. Changes are approved by {{ROLE-N}} before becoming current. Superseded versions are retained per the Revision History (§10). The SoA (§6) is controlled the same way.}}

---

## 8. Operation: AI System Lifecycle and Third-Party Management

> This is the operational planning and control of **clause 8**, told as a lifecycle: how an in-scope AI system is governed *from concept to retirement*, and how the outside components it depends on are controlled. The goal is that an auditor can follow one system through its life and see the right controls applied at each stage. Tie each stage back to the relevant **CTRL-N** and **RISK-N** so the trace is visible. (The control *catalog* is in §6; this section shows the controls *in motion* along the lifecycle.)

### 8.1 AI System Lifecycle Governance

| Lifecycle stage | What is governed | Controls applied (CTRL-N) | Risks addressed (RISK-N) |
|---|---|---|---|
| Requirements | {{intended use, constraints, who's affected}} | {{CTRL-N}} | {{RISK-N}} |
| Data | {{sourcing, quality, privacy, documentation}} | {{CTRL-N}} | {{RISK-N}} |
| Development | {{model/feature build, change control}} | {{CTRL-N}} | {{RISK-N}} |
| Verification | {{evaluation, bias/safety testing, sign-off}} | {{CTRL-N}} | {{RISK-N}} |
| Deployment | {{release gating, transparency to users}} | {{CTRL-N}} | {{RISK-N}} |
| Monitoring | {{live-output monitoring, drift, incidents}} | {{CTRL-N}} | {{RISK-N}} |
| Decommissioning | {{retiring a system; data/model disposal}} | {{CTRL-N}} | {{RISK-N}} |

### 8.2 Third-Party and Supplier Management

> Most small teams don't train their own foundation models — they call someone else's. That doesn't move the responsibility off your plate; it makes supplier control part of *your* AIMS. Record how third-party models, components, and vendors are assessed before use and controlled while in use.

| Supplier / component | What it provides | Assessment before use | Ongoing control | Controls (CTRL-N) |
|---|---|---|---|---|
| {{e.g., model API provider}} | {{the model behind feature X}} | {{terms review, capability/eval check}} | {{monitor for version/behavior change}} | {{CTRL-4}} |
| ... | ... | ... | ... | ... |

---

## 9. Performance Evaluation: Monitoring, Internal Audit, and Management Review

> This is **clause 9** — how you check that the AIMS and the AI systems are actually working. Three parts: ongoing **monitoring/measurement**, the **internal audit** programme, and the **management review**. The distinction to hold onto: an internal audit *checks the system against the standard* (does reality match the documented AIMS?); a management review is the recorded *leadership meeting that turns findings into decisions*. Both produce records an external auditor will want to see — "we review things informally" without records is the same as not reviewing.

### 9.1 Monitoring and Measurement

> What you measure about the AIMS and the AI systems, and how. Tie back to the objectives (OBJ-N) and impacts (IMP-N) so measurement isn't busywork.

| What is monitored | Method / metric | Frequency | Relates to |
|---|---|---|---|
| {{Objective progress}} | {{OBJ-N measure}} | {{cadence}} | {{OBJ-N}} |
| {{Live model behavior}} | {{e.g., output sampling, drift check}} | {{cadence}} | {{RISK-N / IMP-N}} |
| ... | ... | ... | ... |

### 9.2 Internal Audit

> The programme that checks the AIMS against the standard. State scope (what's audited), frequency, who audits (ideally someone not auditing their own work — see the solo note in §4), and what evidence is produced. Findings become nonconformities (NC-N, §9 below — see §10 cross-ref) where reality doesn't match the documented system.

{{Internal audits cover {{scope}}, run {{frequency}}, led by {{ROLE-4}}. Each audit produces {{evidence: checklist, findings, NC records}}. Findings that show a gap between reality and the documented system are logged as nonconformities (NC-N) per §10.}}

### 9.3 Management Review

> The recorded leadership meeting where the evidence is examined and *decisions* are made — what to change in the policy, objectives, controls, or scope. Record the inputs reviewed (audit results, risks, impacts, objective progress, incidents) and the outputs (decisions, action items, owners). Update the "Last Management Review" field in the metadata table when held.

Management review inputs: {{audit results, status of RISK-N/IMP-N, OBJ-N progress, NC-N status, changes in context}}.
Management review outputs (decisions): {{changes to policy/objectives/controls/scope, with owners and dates}}.
Cadence: {{e.g., per release / quarterly}}. Last held: {{YYYY-MM-DD or 'not yet held'}}.

---

## 10. Improvement: Nonconformities and Corrective Action

> This is **clause 10** — the part that proves the AIMS is *alive*. A **nonconformity (NC)** is a place where reality doesn't match the documented system. A **corrective action** is the recorded fix *plus* root-cause handling so the same gap doesn't recur. Read this section as: "when reality doesn't match the documented system, here is the logged process for fixing it and stopping it coming back." Continual improvement over PDCA cycles is the evidence of a living system rather than a static binder that was written once and shelved.

### 10.1 Nonconformity and Corrective Action Log

> One row per nonconformity, found in audit, monitoring, an incident, or day-to-day work. Record the gap, its root cause, the correction (immediate fix), the corrective action (stop-it-recurring), the owner, and verification that it worked. Use **NC-N**.

| ID | Nonconformity (the gap) | Source | Root cause | Correction + corrective action | Owner | Verified |
|---|---|---|---|---|---|---|
| NC-1 | {{e.g., "a deployed feature had no impact assessment"}} | {{internal audit}} | {{e.g., "no release gate enforced it"}} | {{add IMP record; add a release-checklist gate}} | {{ROLE-N}} | {{Y/N + date}} |
| NC-N | {{Gap}} | {{audit / monitoring / incident}} | {{cause}} | {{fix + prevention}} | {{owner}} | {{Y/N}} |

### 10.2 Continual Improvement

> How the AIMS improves over time through PDCA — the changes made as a result of reviews, audits, and corrective actions. A short narrative is fine; the evidence is in the NC log above and the management-review records (§9.3).

{{How the AIMS is continually improved: {{e.g., "each management review produces at least one improvement action; corrective actions are tracked to verified closure"}}.}}

---

## 11. Open Questions

> Unresolved AIMS decisions, tracked as **OQ-N**: scope edges not yet settled, Annex A controls not yet justified in the SoA, risks or impacts still under assessment, or certification-path choices still pending. Note what blocks each and who must decide. Resolve and remove as readiness matures.

- **OQ-1**: {{e.g., "Is the third-party model provider's behavior in or out of our AIMS scope boundary?"}} — {{what's blocking, who decides}}
- **OQ-2**: {{e.g., "Which Annex A controls can we justifiably exclude given we deploy but don't train?"}} — {{blocking / owner}}
- **OQ-3**: {{e.g., "Readiness-only or pursue Stage 1 certification this year?"}} — {{blocking / owner}}
- ...

---

## 12. Revision History

> Record every substantive change to this AIMS document with version, date, author, and a summary. Document control is itself an audited requirement (see §7.4), so keep this current — and where a revision results from a management-review decision (§9.3), say so, since that ties the change back to the governing loop.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — especially the scope in §1.2 and the definitions in §1.3)
- §2 Context of the Organization (the AIMS scope boundary is load-bearing)
- §3 Leadership and AI Policy (the policy is the constitution the rest implements)
- §5 Planning (objectives, risks, AND impacts — the impact assessment is the part most often skipped)
- §6 Statement of Applicability and Operational Controls (the heart of certification readiness)
- §9 Performance Evaluation (at minimum: a real management review with records)
- §10 Improvement (the nonconformity/corrective-action log is what proves the system is alive)
- §12 Revision History

**Optional sections** (include if relevant):
- §4 Roles, Responsibilities, and Authorities (collapses heavily for solo projects — keep it, but note honestly where roles merge and where audit independence is limited)
- §7 Support (trim resources/competence for a solo project, but keep §7.4 document control — the standard checks that you control your own records)
- §8 Operation (omit the lifecycle stages that genuinely don't apply to your role — a pure *deployer* may have a thinner development/data story but a heavier third-party story in §8.2)
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- POL-N: AI Policy statements
- OBJ-N: AI objectives (parallels the Project Management template's OBJ-N)
- CTRL-N: Annex A operational controls (rows in the Statement of Applicability)
- RISK-N: AI risks (cross-reference the Risk Management Plan rather than duplicating)
- IMP-N: AI system impact-assessment findings
- ROLE-N: roles and responsibilities
- NC-N: nonconformities and corrective actions
- OQ-N: open questions

These prefixes enable cross-document traceability — a policy statement (POL-N) drives an objective (OBJ-N) and a control (CTRL-N); that control addresses a risk (RISK-N) or an impact finding (IMP-N); a gap in it becomes a nonconformity (NC-N); and a named role (ROLE-N) owns each. An auditor can follow any of these threads end to end.

**Tailoring**:
- **Solo founder / small team, lightweight:** Most roles in §4 collapse to one name — keep the rows so the responsibilities don't vanish, and be honest about audit independence. The two things you should NOT skip: the **Statement of Applicability** (§6, every Annex A control consciously included or excluded) and the **impact assessment** (§5.3, the outward "who could we harm" view) — those two are what make this an *AI* management system rather than generic process. A recurring management review with records (§9.3) is the third non-negotiable.
- **Deployer rather than developer:** If you use someone else's model rather than building one, your §8 lifecycle is thinner on data/development and heavier on §8.2 third-party management — and several Annex A controls may legitimately be "not applicable because we do not train models." That's fine, as long as each such exclusion is *justified in the SoA*, not just absent.
- **Growing toward certification:** As you move from "readiness only" to an actual Stage 1/Stage 2 audit, the records start mattering more than the prose — internal-audit evidence (§9.2), management-review minutes (§9.3), and a closed-loop nonconformity log (§10) are what an external auditor samples. Start keeping those records early, even informally; back-filling them before an audit is painful and unconvincing.
- Keep the SoA (§6) and this document under the same document control (§7.4) you describe — practicing what you document is itself audited.
- Revision history is mandatory. Track every substantive change with version bumps, and tie major revisions to management-review decisions where applicable.

**For regulated/safety-critical projects:** use the full ISO/IEC 42001:2023 (and ISO/IEC 27001:2022 where an information-security management system also applies), not this lightweight version. ISO standards are paywalled and copyrighted — verify all clause numbering, Annex A control selection, and Statement-of-Applicability requirements against the purchased standard before relying on this for an actual certification audit. This template is suitable for solo/small-team certification-readiness planning, internal documentation, and early-stage products.
