# Stakeholder Requirements Specification Template

> **Template purpose:** Lightweight Stakeholder Requirements Specification (StRS) structure following ISO/IEC/IEEE 29148:2018. Use this template when starting an StRS document. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** At the very start of a project — before you write a System/Software Requirements Specification (SyRS/SRS). The StRS captures what the people who care about the system actually need, in *their own words*. It comes first because you cannot decide what to build until you know whose problem you are solving and why.
>
> **Companion standard:** ISO/IEC/IEEE 29148:2018 — Systems and software engineering — Life cycle processes — Requirements engineering (stakeholder requirements definition).
>
> **Status of this template:** Lightweight skeleton organized from publicly described 29148 structure. The standard text itself is paywalled — this template paraphrases the section organization only and reproduces no normative wording. Verify against the full standard when you have access, especially for enterprise/regulated contexts.

---

# Stakeholder Requirements Specification — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | StRS-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29148:2018 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Scope | {{Internal documentation / Public / Customer-facing}} |
| Successor document | {{SyRS / SRS that will translate these needs into system requirements}} |

---

## 1. Introduction

> **Key idea for beginners:** A Stakeholder Requirements Specification captures *needs* — what people want and why they want it — phrased in the **stakeholders' own language**, not in technical terms. It deliberately comes *before* the SyRS/SRS. The job here is "what's the problem and who has it"; the job of the later system spec is "what must the system do to solve it." Mixing the two is the most common beginner mistake: if you write "the system shall use a Postgres database" here, you've jumped to a solution before anyone has agreed on the need. Keep this document in the language of the people, not the machine.

### 1.1 Purpose

> One-paragraph statement of what this document is for. Establish that it captures stakeholder needs in stakeholder language, and that a later system/software requirements document will translate these into technical requirements.

{{This document specifies the needs and goals of the stakeholders of {{Project Name}}, expressed in their own terms. It is the highest-level statement of *why* the system is wanted and *what outcomes* it must produce for the people who care about it. A subsequent System/Software Requirements Specification will translate these stakeholder requirements into system and technical requirements.}}

### 1.2 Scope

> Define the boundary of the *needs* being captured — which stakeholder community, which business or mission area. Note what is intentionally left out so readers don't expect needs that aren't here.

**This StRS covers** {{the stakeholder community / business area / mission served, e.g. "the needs of individual users and maintainers of the X tool"}}

**This StRS does NOT cover** {{out-of-scope stakeholder groups, future phases, or the technical "how" — that lives in the SyRS/SRS}}

### 1.3 Definitions and Acronyms

> Define terms a reader would otherwise misread — including everyday words used in a specific way by this stakeholder community. Define "stakeholder," "need," and "stakeholder requirement" here if your audience is new to the practice.

| Term | Definition |
|---|---|
| Stakeholder | {{Any individual, group, or organization with an interest in, or affected by, the system.}} |
| Stakeholder requirement | {{A statement of a stakeholder need that the system must satisfy, with its rationale and source.}} |
| {{Term 3}} | {{Definition}} |
| ... | ... |

### 1.4 References

> List the documents that informed these needs — interview notes, prior products, business plans, external standards. Categorize for readability.

Source material:
- {{path/to/interview-notes.md}} — {{brief description}}
- {{path/to/business-context.md}} — {{brief description}}
- ...

Related specifications:
- {{path/to/SyRS-or-SRS.md}} — {{the document that will consume these stakeholder requirements}}
- ...

External standards:
- ISO/IEC/IEEE 29148:2018 — Requirements engineering (stakeholder requirements definition)
- {{Other standard with version}} — {{relevance}}

---

## 2. Stakeholders

> **What this section is for:** Before you can capture needs, you must name *whose* needs they are. A "stakeholder" is anyone with a stake in the system — direct users, but also people who pay for it, maintain it, regulate it, or are affected by it without ever touching it. List each stakeholder or stakeholder *class* (a group with shared interests) and give each one a stable ID (STK-1, STK-2, …) so every need can later be traced back to who has it. If you can't name a stakeholder for a need, that need is probably your own assumption, not a real one.

| ID | Stakeholder / class | Who they are | Their interest in the system |
|---|---|---|---|
| STK-1 | {{e.g. End user}} | {{description}} | {{what they want out of it / why they care}} |
| STK-2 | {{e.g. Maintainer}} | {{description}} | {{interest}} |
| STK-3 | {{e.g. Sponsor / payer}} | {{description}} | {{interest}} |
| ... | ... | ... | ... |

---

## 3. Business / Mission Context

> **What this section is for:** A system never exists for its own sake — it serves some larger goal: a business objective, a mission, a personal outcome. Capture that context here so every later requirement can be checked against "does this actually serve the goal?" This is where you record the *why behind the why*: the situation today, the desired situation, and what success looks like at the business/mission level (not the feature level).

**Current situation:** {{What is the world like today without the system? What problem or gap exists?}}

**Desired situation:** {{What outcome do stakeholders want to reach? Describe the changed world, not the software.}}

**Business / mission goals:**
- {{Goal 1 — the high-level objective the system must advance}}
- {{Goal 2}}
- ...

**Success measures (if known):** {{How will stakeholders judge, at the mission level, that this was worth doing? Keep these outcome-shaped, not feature-shaped.}}

---

## 4. Stakeholder Needs and Goals

> **What this section is for:** This is the heart of the document in plain language. Capture the problems, desires, and goals as the stakeholders actually express them — frustrations, wishes, "I just want to be able to…" statements. Do *not* polish these into formal requirements yet; that happens in §5. Keeping the raw need separate from the formal requirement preserves the *why*, which is the part that gets lost when needs are translated to technical specs too early. Group by stakeholder or by theme, whichever reads more clearly.

### 4.1 {{Stakeholder or theme 1}}

> Plain-language needs from this stakeholder/class. Reference STK-N where helpful.

- {{"As {{STK-N}}, I need ... because ..." — keep it in their voice}}
- {{...}}

### 4.2 {{Stakeholder or theme 2}}

- {{...}}

---

## 5. Stakeholder Requirements

> **What this section is for:** Now turn the plain-language needs from §4 into clear, traceable *stakeholder requirements*. Each one is still in stakeholder terms (an outcome they need, not a technical design), but it is written to be **testable and traceable**: a single clear need statement, the **rationale** (why — carried over from §4 so it isn't lost), and the **source stakeholder** (which STK-N it belongs to). Give each a stable ID (StR-1, StR-2, …). One need per requirement — if a statement contains "and," it's probably two requirements. These StR-N IDs are what the later SyRS/SRS will trace its system requirements back to.

> Use either the table form or the block form below — pick one and stay consistent.

**Table form:**

| ID | Stakeholder requirement (need statement) | Rationale | Source |
|---|---|---|---|
| StR-1 | {{The system shall let stakeholders ... / Stakeholders need to be able to ...}} | {{Why this matters — the underlying goal}} | STK-{{N}} |
| StR-2 | {{...}} | {{...}} | STK-{{N}} |
| ... | ... | ... | ... |

**Block form (use for requirements that need more room):**

- **StR-N** — {{Need statement in stakeholder terms.}}
  - *Rationale:* {{why this is needed; tie back to a §4 need and a §3 goal}}
  - *Source:* STK-{{N}}
  - *Acceptance signal:* {{how the stakeholder would recognize this need is met — keeps the requirement testable without prescribing a solution}}

---

## 6. Operational Concept Summary

> **What this section is for:** A short, narrative picture of how stakeholders expect to *use* the system in their day-to-day — the "a typical day with this system looks like…" sketch. This is deliberately brief here. If a full Operational Concept Document (ConOps / OpsCon) exists, reference it rather than duplicating it. The point is to give later readers enough of the usage story that the requirements in §5 make sense in context.

{{Brief narrative of expected use. Who does what, when, to achieve which goal. Reference the full ConOps if one exists: {{path/to/conops.md}}.}}

---

## 7. Constraints and Assumptions

> **What this section is for:** Record the boundaries the stakeholders impose or take for granted. **Constraints** are things the solution *must* respect regardless of design (budget, legal/regulatory limits, existing systems it must coexist with, hard deadlines, platform restrictions). **Assumptions** are things being taken as true that, if false, would change the requirements. Capturing assumptions explicitly is what lets you catch a wrong one before it becomes an expensive surprise.

**Constraints:**
- {{Constraint 1 — e.g. must run without paid cloud services}}
- {{Constraint 2}}
- ...

**Assumptions:**
- {{Assumption 1 — e.g. stakeholders have reliable internet}}
- {{Assumption 2}}
- ...

---

## 8. Validation Expectations

> **What this section is for:** *Validation* asks "did we build the right thing?" — i.e. are the stakeholders' actual needs met? (Distinct from *verification*, which asks "did we build the thing right?" against the technical spec.) Record here how stakeholders will confirm their needs were satisfied: demos, trials, sign-off, acceptance walkthroughs, real-world use over a period. Naming these expectations now keeps the §5 requirements honest — every stakeholder requirement should have a believable way to be validated by the stakeholder who owns it.

- {{How will STK-N confirm StR-M is met? e.g. "User trial over two weeks; success if they stop reaching for the old tool."}}
- {{Acceptance method 2}}
- ...

---

## 9. Open Questions

> Needs or stakeholder positions still unresolved. Include each question and what's blocking it / who must decide. Resolve and remove as the picture clarifies — unresolved stakeholder questions here become risks later.

- **OQ-1**: {{question}} — {{what's blocking, which stakeholder needs to decide}}
- ...

---

## 10. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Stakeholders
- §4 Stakeholder Needs and Goals
- §5 Stakeholder Requirements
- §10 Revision History

**Optional sections** (include if relevant):
- §3 Business / Mission Context (omit only if the goal is self-evident and captured elsewhere)
- §6 Operational Concept Summary (omit if a standalone ConOps already covers it)
- §7 Constraints and Assumptions (rarely truly empty — prefer to keep)
- §8 Validation Expectations (defer if too early, but it sharpens §5 when present)
- §9 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- STK-N: stakeholders / stakeholder classes (§2)
- StR-N: stakeholder requirements (§5)

These prefixes enable cross-document traceability — each StR-N traces *up* to the STK-N who owns it, and *down* to the system/software requirements that the SyRS/SRS will derive from it.

**Tailoring**:
- Keep everything in stakeholder language. The moment a statement names a technology or a design choice, it belongs in the SyRS/SRS, not here.
- One need per StR-N. Split anything containing "and."
- The StRS feeds the SyRS/SRS — finish (a draft of) this before you start translating needs into system requirements.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29148:2018 standard, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
