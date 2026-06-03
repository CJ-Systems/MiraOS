# Architecture Description Template

> **Template purpose:** Lightweight Architecture Description (AD) structure following ISO/IEC/IEEE 42010:2022. Use this template when documenting the architecture of a system in a way that addresses each stakeholder and the concerns they care about. Replace `{{placeholder}}` content with system-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When a system is large enough that "how it's structured" needs to be written down for more than one audience. An AD organizes the architecture around *who cares about what*: it names stakeholders, the concerns they hold, the viewpoints (lenses) that frame those concerns, and the views that apply each lens to your specific system. Sits below the SRS (WHAT the system must do) and alongside ADRs (individual decisions); it is the structured picture of HOW the system is shaped to meet its requirements and concerns.
>
> **Companion standard:** ISO/IEC/IEEE 42010:2022 — Software, systems and enterprise — Architecture description.
>
> **Status of this template:** Lightweight skeleton assembled from publicly available summaries of ISO/IEC/IEEE 42010:2022 (the standard text itself is paywalled). Faithful to the standard's stakeholder → concern → viewpoint → view organization, but reduced for solo/small-team use. Verify against the full standard when accessible, and before relying on it for any regulated or contractual context.

---

# Architecture Description — {{System Name}}

| Field | Value |
|---|---|
| Document ID | AD-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 42010:2022 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Architecture scope | {{Whole system / a subsystem / a release / ...}} |
| Related SRS | {{SRS-{{PROJECT-ID}}-001 or path}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: what this document is and what it describes. Establish that this is the architecture description for the system named above, and that it is organized around stakeholders and their concerns rather than around a fixed list of diagrams.

{{This document describes the architecture of {{System Name}}. It identifies the system's stakeholders and the concerns they hold, the viewpoints used to frame those concerns, and the views that apply each viewpoint to {{System Name}} specifically. It is the structured picture of how the system is shaped to meet its requirements (see the related SRS) and to satisfy its stakeholders' concerns. Individual design decisions are recorded as ADRs and referenced from §5.}}

### 1.2 Scope

> What part of the system this AD covers and what it does NOT. An AD can describe a whole system, one subsystem, or one release. Be explicit so a reader knows whether the architecture they're looking for is in this document or elsewhere.

In scope:
- {{Subsystem / layer / release covered}}
- {{...}}

Out of scope:
- {{What this AD deliberately does not cover}} — {{where it lives instead, if anywhere}}
- {{...}}

### 1.3 Definitions and Acronyms

> Define the terms a reader needs to follow the rest of the document. The four core architecture-description terms are defined inline in §2 and §3; add project-specific terms here.

| Term | Definition |
|---|---|
| Architecture | The fundamental concepts or properties of the system — how it is organized, its parts, and how they relate — embodied in its elements and their relationships. |
| {{Term 1}} | {{Definition}} |
| {{Term 2}} | {{Definition}} |
| ... | ... |

### 1.4 References

> Documents this AD depends on or that inform it. The SRS is almost always the primary input (it supplies the requirements the architecture must meet). List ADRs that record decisions referenced here.

System requirements:
- {{SRS-{{PROJECT-ID}}-001 or path}} — {{brief description}}

Architecture Decision Records:
- ADR-NNNN — {{decision}}
- ...

Related specifications and diagrams:
- {{path/to/spec-or-diagram}} — {{description}}
- ...

External standards:
- ISO/IEC/IEEE 42010:2022 — Architecture description (companion standard for this document)
- {{other standard / notation reference}} — {{relevance}}

---

## 2. Stakeholders and Concerns

> **The core idea — read this first if you are new to formal architecture practice.** An architecture description is organized around *who cares about the system* and *what they care about*, not around a fixed set of diagrams. Two definitions:
>
> - A **stakeholder** is any individual, team, or role with an interest in the system — e.g., the developer who maintains it, the operator who runs it, the end user, the security reviewer, the person paying for it. Different stakeholders care about different things.
> - A **concern** is something a stakeholder cares about that the architecture must address — e.g., "can it be deployed without downtime?", "is user data protected?", "can a new contributor understand the code?", "will it cost too much to run?". A concern is *not* a requirement (the SRS holds requirements); it is an interest or worry that the architecture has to speak to.
>
> The whole document hangs off this: you name the stakeholders, name their concerns, and then (in §3 and §4) you make sure every concern is framed by at least one viewpoint and answered by at least one view. The stakeholder-vs-concern table at the end of this section is the checklist that nothing important is going unaddressed.

### 2.1 Stakeholders

> List each stakeholder with an STK-N id. Capture the *role* and what makes their interest distinct — not named individuals (this is a reusable, public template; use roles like "Maintainer," "Operator," "End user," "Security reviewer").

- **STK-1 {{Stakeholder role}}.** {{Who they are, what their relationship to the system is.}}
- **STK-2 {{Stakeholder role}}.** {{...}}
- **STK-3 {{Stakeholder role}}.** {{...}}
- ...

### 2.2 Concerns

> List each concern with a C-N id, and note which stakeholder(s) hold it. A concern should be phrased as the thing being cared about, ideally as a question the architecture must answer.

- **C-1 {{Concern name}}.** {{What is cared about; phrased as a question where possible.}} — held by {{STK-N, STK-M}}
- **C-2 {{Concern name}}.** {{...}} — held by {{STK-N}}
- **C-3 {{Concern name}}.** {{...}} — held by {{STK-N}}
- ...

### 2.3 Stakeholder-vs-Concern Matrix

> The checklist. Rows are stakeholders, columns are concerns; mark the cells where that stakeholder holds that concern. Reading down a column tells you who cares about a concern; reading across a row tells you what a stakeholder cares about. Every concern should be held by at least one stakeholder, and every concern should later be framed by at least one viewpoint in §3.

| Stakeholder \ Concern | C-1 | C-2 | C-3 | ... |
|---|---|---|---|---|
| STK-1 {{role}} | {{✓}} | | {{✓}} | |
| STK-2 {{role}} | | {{✓}} | {{✓}} | |
| STK-3 {{role}} | {{✓}} | {{✓}} | | |
| ... | | | | |

---

## 3. Architecture Viewpoints

> **The second core idea.** A **viewpoint** is a *reusable template or lens* for addressing a particular set of concerns. It says, in advance, "to answer concerns like these, look at the system this way, using this kind of notation." A viewpoint is generic — it could be reused on a different system. The notation a viewpoint prescribes is called a **model kind** (e.g., a box-and-line context diagram, an entity-relationship diagram, a deployment diagram, a sequence diagram). Think of a viewpoint as the *blank form*; the **view** in §4 is that form *filled in for this system*.
>
> The chain is: **stakeholder → concern → viewpoint → view.** A stakeholder *holds* a concern; a viewpoint *frames* one or more concerns (it declares which concerns it is good for); a view *applies* a viewpoint to this specific system to actually answer those concerns. For each viewpoint below, state which concerns (C-N) it frames and which model kinds (notations) it uses.
>
> The viewpoints listed below — context, functional/logical, information/data, deployment, security — are common, useful starting lenses. Keep the ones that frame real concerns from §2; drop the ones that don't; add others if a concern needs a lens not listed here.

- **VP-1 Context viewpoint.**
  - Frames concerns: {{C-N, C-M — e.g., "what is inside vs outside the system, and who/what does it talk to"}}
  - Model kinds: {{system context diagram (system as a single box with external actors and systems around it)}}
  - {{One line on what this viewpoint is for in this project.}}

- **VP-2 Functional / Logical viewpoint.**
  - Frames concerns: {{C-N — e.g., "what are the major components and what is each responsible for"}}
  - Model kinds: {{component diagram / responsibility table / box-and-line decomposition}}
  - {{One line on purpose.}}

- **VP-3 Information / Data viewpoint.**
  - Frames concerns: {{C-N — e.g., "what data does the system hold, how is it structured, how does it flow"}}
  - Model kinds: {{entity-relationship diagram / data-flow diagram / schema tables}}
  - {{One line on purpose.}}

- **VP-4 Deployment viewpoint.**
  - Frames concerns: {{C-N — e.g., "where does each part run, on what infrastructure, how is it released"}}
  - Model kinds: {{deployment diagram (nodes and the components mapped onto them) / environment table}}
  - {{One line on purpose.}}

- **VP-5 Security viewpoint.**
  - Frames concerns: {{C-N — e.g., "what are the trust boundaries, what protects user data, what are the attack surfaces"}}
  - Model kinds: {{trust-boundary diagram / data-classification table / threat list}}
  - {{One line on purpose.}}

- **VP-N {{Additional viewpoint if needed}}.**
  - Frames concerns: {{C-N}}
  - Model kinds: {{notation}}
  - {{Purpose.}}

---

## 4. Architecture Views

> **The third core idea — where the architecture actually gets described.** A **view** is a viewpoint *applied to this specific system*: it takes the lens defined in §3 and fills it in with {{System Name}}'s real components, data, nodes, and boundaries. There should be exactly one view per viewpoint you kept in §3 (V-1 applies VP-1, V-2 applies VP-2, and so on). Each view is where the diagrams and models live — embed them, or point to where they live (e.g., a `docs/diagrams/` folder, a drawing tool link), and write the prose that explains them.
>
> A view should explicitly answer the concerns its viewpoint framed. If a view doesn't actually address the concerns its viewpoint claimed in §3, either the view is incomplete or the viewpoint was mis-scoped.

### 4.1 V-1 Context view (applies VP-1)

> Show {{System Name}} as a single box and everything it interacts with — users, external systems, services. Answers the context concerns from §3.

{{Diagram: embed or link. Then prose describing the external actors, the system boundary, and the major inflows/outflows.}}

*Concerns addressed:* {{C-N, C-M}}

### 4.2 V-2 Functional / Logical view (applies VP-2)

> Show the major internal components of {{System Name}} and what each is responsible for.

{{Diagram or component table. For each component: name, responsibility, key dependencies.}}

| Component | Responsibility | Depends on |
|---|---|---|
| {{Component A}} | {{What it does}} | {{Component B, external service}} |
| {{Component B}} | {{...}} | {{...}} |
| ... | ... | ... |

*Concerns addressed:* {{C-N}}

### 4.3 V-3 Information / Data view (applies VP-3)

> Show what data {{System Name}} holds and how it flows. Schemas, key entities, and the relationships between them.

{{Diagram or schema tables. Describe the main data entities and how data enters, is stored, and leaves the system.}}

*Concerns addressed:* {{C-N}}

### 4.4 V-4 Deployment view (applies VP-4)

> Show where each component runs and on what infrastructure, plus how the system is released into each environment.

{{Diagram or environment table mapping components to nodes/hosts/services.}}

| Environment | What runs there | Notes |
|---|---|---|
| {{Local / Dev}} | {{components}} | {{...}} |
| {{Production}} | {{components}} | {{...}} |
| ... | ... | ... |

*Concerns addressed:* {{C-N}}

### 4.5 V-5 Security view (applies VP-5)

> Show the trust boundaries, how data of different sensitivities is handled, and the main protections in place.

{{Trust-boundary diagram or table. Identify boundaries, data classifications, and the controls at each boundary.}}

*Concerns addressed:* {{C-N}}

### 4.6 V-N {{Additional view}} (applies VP-N)

{{Apply any additional viewpoint here.}}

*Concerns addressed:* {{C-N}}

---

## 5. Architecture Decisions and Rationale

> The architecture is the sum of many decisions; this section is the index to the significant ones and *why* they were made. Don't re-litigate each decision in full here — record full decisions as ADRs (Architecture Decision Records) in their own documents and link to them. List the key decisions, a one-line rationale, and the concern(s) each one serves. If a decision was hard or has notable trade-offs, note the trade-off so a future reader doesn't undo it without understanding the cost.

| Decision | Rationale (one line) | Serves concern(s) | ADR |
|---|---|---|---|
| {{Decision summary}} | {{Why this over the alternatives}} | {{C-N}} | {{ADR-NNNN}} |
| {{Decision summary}} | {{...}} | {{C-N}} | {{ADR-NNNN}} |
| ... | ... | ... | ... |

{{Optional prose: any cross-cutting rationale or trade-offs that span multiple decisions.}}

---

## 6. Correspondences and Consistency

> The views describe the same system from different angles, so they must agree with each other. A **correspondence** is a relationship that must hold *across* views — e.g., "every component in the functional view (V-2) must appear somewhere in the deployment view (V-4)," or "every data entity in the information view (V-3) that crosses a trust boundary must be classified in the security view (V-5)." This section records those rules and is the place to check, after any change, that the views still line up. When one view changes, the correspondences tell you which other views to update.

| ID | Correspondence rule | Views involved |
|---|---|---|
| {{CORR-1}} | {{e.g., Every component in V-2 appears as a deployed unit in V-4}} | {{V-2 ↔ V-4}} |
| {{CORR-2}} | {{e.g., Every external actor in V-1 has a defined trust boundary in V-5}} | {{V-1 ↔ V-5}} |
| {{CORR-3}} | {{...}} | {{V-N ↔ V-M}} |
| ... | ... | ... |

{{Optional: known inconsistencies currently tolerated, and the plan to resolve them.}}

---

## 7. Architecture Framework and Conventions

> If you adopted a named architecture framework (e.g., a set of standard viewpoints from a methodology) or fixed notation conventions, record them here so every view is read the same way. This is also where to state diagramming conventions: what a box means, what an arrow means, what colors/line styles signify. For a small project this can be short — even "we use plain box-and-line diagrams; an arrow means 'calls' or 'sends data to'" is a worthwhile convention to write down.

- **Framework adopted:** {{None / name of framework and which of its viewpoints are used}}
- **Notation conventions:**
  - {{e.g., Boxes are components; cylinders are datastores; solid arrows are synchronous calls; dashed arrows are async/events.}}
  - {{...}}
- **Diagram source and location:** {{e.g., diagrams authored in {{tool}}, sources in `docs/diagrams/`, exported as PNG/SVG.}}

---

## 8. Open Questions

> Architectural questions still being resolved. Distinguish load-bearing OQs (a major structural choice is still open) from deferred-with-defaults (there's a working assumption; revisit if it proves wrong).

### 8.1 Open

- **OQ-1** {{Question}} — {{what's blocking, who needs to decide, which concern it affects}}
- ...

### 8.2 Deferred with defaults

- **OQ-DEF-1** {{Question}} — *default: {{working assumption}}.*
- ...

---

## 9. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Stakeholders and Concerns (including the matrix — it's the completeness check)
- §3 Architecture Viewpoints (at minimum the viewpoints that frame real concerns)
- §4 Architecture Views (one view per kept viewpoint)
- §9 Revision History

**Optional sections** (include if relevant):
- §5 Architecture Decisions and Rationale (omit if all decisions live solely in ADRs and you only want an index elsewhere — but a pointer table is cheap and usually worth it)
- §6 Correspondences and Consistency (omit for very small systems with one or two views; valuable as soon as you have three or more views that can drift apart)
- §7 Architecture Framework and Conventions (omit if you adopted no framework and use no special notation — but write down at least your arrow conventions if you have any diagrams)
- §8 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- STK-N: stakeholders
- C-N: concerns
- VP-N: architecture viewpoints
- V-N: architecture views (V-N applies VP-N)
- CORR-N: correspondence rules
- OQ-N / OQ-DEF-N: open questions (open / deferred-with-defaults)

These prefixes enable cross-document traceability — requirements in the SRS can be traced to the concerns they create (C-N), to the viewpoints that frame them (VP-N), and to the views that realize them (V-N).

**Tailoring**:
- The viewpoint list (context, functional, information, deployment, security) is a starting set, not a mandate. Keep a viewpoint only if it frames a real concern from §2; add viewpoints when a concern needs a lens not listed.
- Keep the stakeholder → concern → viewpoint → view chain unbroken: every concern should be framed by at least one viewpoint, and every viewpoint should be realized by exactly one view. The matrix in §2.3 and the "concerns addressed" line under each view are how you check.
- Diagrams can be embedded or linked. For a small team, a single `docs/diagrams/` folder of PNG/SVG exports plus prose in this document is plenty.

**For regulated/safety-critical projects:** Use the full ISO/IEC/IEEE 42010:2022 standard, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
