# System Requirements Specification Template

> **Template purpose:** Lightweight System Requirements Specification (SyRS) structure inspired by ISO/IEC/IEEE 29148:2018. Use this template when starting a new SyRS document. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When the thing you are building is a *system* — a combination of software, hardware, people, and processes working together — and you need to specify what the whole system must do before drilling into software-only requirements. The SyRS sits between the **stakeholder requirements** (StRS — the needs, in stakeholder language) and the **software requirements** (SRS — software-specific behavior). If your project is pure software with no meaningful hardware/people/process scope, you may not need a SyRS — an SRS alone often suffices.
>
> **Companion standard:** ISO/IEC/IEEE 29148:2018 — Systems and software engineering — Life cycle processes — Requirements engineering (system requirements clause).
>
> **Status of this template:** Lightweight skeleton assembled from public descriptions of the 29148 system-requirements structure. The standard text itself is paywalled and was not reproduced here — section organization is inspired-by, prose is paraphrased original. Verify against the full standard when accessible, especially for enterprise/regulated contexts.

---

# System Requirements Specification — {{System Name}}

| Field | Value |
|---|---|
| Document ID | SyRS-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29148:2018 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Source StRS | {{path/to/stakeholder-requirements.md or "N/A"}} |
| Derived SRS | {{path/to/software-requirements.md or "Planned"}} |

---

## 1. Introduction

> A SyRS specifies what the **whole system** must do — and a system is more than its software. It may include hardware, the people who operate it, and the processes they follow. Read this whole section as setting the frame: what document this is, what system it covers, the words we will use, and what it depends on.

### 1.1 Purpose

> One paragraph: what this document is for and what it specifies. Make clear that this is a *system*-level requirements document, that it derives from stakeholder needs (StRS), and that software-specific detail is delegated downstream to an SRS.

{{This document specifies the requirements for the {{System Name}} system — what the system as a whole (software, hardware, people, and processes together) must do and the qualities it must exhibit. It derives from the stakeholder requirements (StRS) and is the basis from which software-specific requirements (SRS) are elaborated. It describes WHAT the system must do, not HOW it is built.}}

### 1.2 Scope

> Define the **system boundary**: what is inside the system and what is outside it. This is the single most important thing a SyRS does — confusing "inside the system" with "in the surrounding environment" is the most common SyRS mistake. Name the system, what it is for, and what it explicitly is NOT.

**{{System Name}} is** {{the combination of software/hardware/people/process that delivers ...}}

**{{System Name}} is NOT** {{adjacent system / a single software component / the surrounding environment / ...}}

**Inside the boundary:** {{components, people-roles, and processes that this SyRS governs}}

**Outside the boundary (environment):** {{external systems, actors, and infrastructure the system depends on but does not own}}

### 1.3 Definitions and Acronyms

> Define every term that, if misread, would cause a requirement to be misunderstood. For a SyRS especially, define the difference between **system**, **subsystem**, **component**, and **external entity** if those words carry specific meaning in your project.

| Term | Definition |
|---|---|
| StRS | Stakeholder Requirements Specification — the *needs*, in stakeholder language (the layer above this document). |
| SyRS | System Requirements Specification — *this document*; what the whole system must do. |
| SRS | Software Requirements Specification — software-specific behavior derived from this SyRS. |
| {{Term 1}} | {{Definition}} |
| {{Term 2}} | {{Definition}} |
| ... | ... |

### 1.4 References

> List the documents this SyRS depends on or that inform it. The most important reference is the StRS it derives from. Categorize for readability.

Source stakeholder requirements:
- {{path/to/StRS.md}} — {{brief description}}

Related specifications:
- {{path/to/spec.md}} — {{brief description}}
- ...

Decision records:
- ADR-NNNN — {{description}}
- ...

External standards:
- ISO/IEC/IEEE 29148:2018 — requirements engineering (system requirements).
- {{Other standard with version}} — {{relevance}}

---

## 2. System Overview and Context

> Before listing requirements, paint the picture: what the system is, where its edges are, and who/what it talks to across those edges. A reader should be able to draw the system and its neighbours from this section alone.

### 2.1 What the System Is

> Substantive description of the system as a whole. What does it accomplish? What are its major parts (software, hardware, people, process) at a high level? Stay at WHAT, not HOW.

{{Description...}}

### 2.2 System Boundary

> Restate the boundary from §1.2 in operational terms. Everything that the project team can change or specify is *inside*; everything it must accept as given is *outside* (the environment). When in doubt, ask: "can we change this thing's behaviour?" — if no, it is environment.

{{Boundary description — what is in, what is out, and why the line is drawn there...}}

### 2.3 Major External Entities and Interfaces

> List the external entities (other systems, users, hardware, services) the system interacts with across its boundary, and name the interface to each at a high level. Detailed interface requirements go in §5; this is the inventory.

| External entity | Type (system / user / hardware / service) | Nature of interaction |
|---|---|---|
| {{Entity 1}} | {{type}} | {{what crosses the boundary}} |
| {{Entity 2}} | {{type}} | {{...}} |
| ... | ... | ... |

### 2.4 Context Diagram (described)

> A **context diagram** shows the system as a single box in the middle, with each external entity as a box around it and a labelled arrow for each interaction. You do not need drawing tools — describe it in prose or a simple list. The goal is that a reader can reconstruct the picture. If you have an actual diagram, embed or link it and keep a one-line caption here.

{{The system ({{System Name}}) sits at the centre. It exchanges {{data/signals/material}} with {{Entity 1}} ({{direction and content}}), receives {{...}} from {{Entity 2}}, and provides {{...}} to {{Entity 3}}. {{Continue until every entity in §2.3 is accounted for.}}}}

---

## 3. System Functional Requirements

> The substantive "what must the system DO" content. Each requirement describes a capability of the *whole system*, not of one software component (that belongs in the SRS). Number requirements **SyR-F-1, SyR-F-2, ...** so they can be referenced from the SRS, architecture, and tests. Each requirement should be:
> - **Atomic** — one capability per requirement.
> - **Testable** — written so you can later say "verified" or "failed" without argument.
> - **Free of design** — WHAT the system does, not HOW it is implemented.
>
> Use the pattern: *"The system shall {{do X}} {{under condition Y}} {{to within tolerance Z}}."* Group related requirements under sub-sections.

### 3.1 {{Capability group 1}}

- **SyR-F-1** The system shall {{...}}.
- **SyR-F-2** The system shall {{...}}.
- ...

### 3.2 {{Capability group 2}}

- **SyR-F-3** The system shall {{...}}.
- ...

---

## 4. System Non-Functional / Quality Requirements

> *How well* the system must do what §3 says it does. These are the quality attributes — performance, reliability, security, usability, maintainability, and so on. **Quantify wherever you can:** "fast" is not testable; "responds within 2 seconds for 95% of requests" is. Number them **SyR-NF-1, SyR-NF-2, ...**

### 4.1 Performance

- **SyR-NF-1** The system shall {{throughput / latency / capacity target, with numbers}}.
- ...

### 4.2 Reliability and Availability

- **SyR-NF-2** The system shall {{uptime / failure-rate / recovery-time target}}.
- ...

### 4.3 Security and Privacy

- **SyR-NF-3** The system shall {{access control / data protection / audit requirement}}.
- ...

### 4.4 Usability

- **SyR-NF-4** The system shall {{learnability / error-rate / accessibility target}}.
- ...

### 4.5 {{Other quality attribute — maintainability, portability, compliance}}

- **SyR-NF-5** The system shall {{...}}.
- ...

---

## 5. External System Interfaces

> Detailed requirements for each interface named in §2.3 — interfaces to **other systems**, to **users**, and to **hardware**. For each, specify what crosses the boundary and any constraints on format, protocol, timing, or volume. Number them **SyR-IF-1, SyR-IF-2, ...** An interface requirement is still WHAT-level: specify the contract, not the implementation.

### 5.1 Interfaces to Other Systems

- **SyR-IF-1** The system shall exchange {{data / message type}} with {{external system}} via {{protocol / format}}, {{constraints: rate, size, sync/async}}.
- ...

### 5.2 User Interfaces

- **SyR-IF-2** The system shall present {{...}} to {{user role}}, supporting {{key interactions}}.
- ...

### 5.3 Hardware Interfaces

> If the system has no hardware interfaces, state that explicitly rather than leaving the section blank.

- **SyR-IF-3** The system shall interface with {{device / sensor / actuator}} via {{connection / signal}}, {{constraints}}.
- ...

---

## 6. Constraints and Assumptions

> **Constraints** are limits the system must respect — they narrow the solution space before any design begins. **Assumptions** are things you are taking as true; if an assumption turns out false, requirements may need to change, so write them down. Distinguish the two clearly.

### 6.1 Design and Implementation Constraints

- **CON-1** {{Mandated technology, platform, or architecture the system must use or avoid.}}
- **CON-2** {{Resource, budget, or schedule limit that shapes the system.}}
- ...

### 6.2 Regulatory and Compliance Constraints

- **CON-3** {{Standard, law, or policy the system must comply with.}}
- ...

### 6.3 Assumptions

- **ASM-1** {{Something assumed true about the environment, users, or external systems.}}
- **ASM-2** {{...}} — *if false, revisit: {{which requirements are affected}}.*
- ...

---

## 7. Traceability

> Every system requirement should exist *because of* a stakeholder need. **Traceability** is the documented link from each SyR back to the StR(s) it satisfies — and forward to the SRS/tests that realize and verify it. This is what lets you answer "why does this requirement exist?" and "what breaks if this need changes?" Maintain a simple table; tooling is optional for small projects.

> Example traceability table (replace with your real rows):

| System requirement | Traces back to (StR) | Traces forward to (SRS / test) |
|---|---|---|
| SyR-F-1 | StR-3 | SRS-F-12, TC-07 |
| SyR-F-2 | StR-3, StR-5 | SRS-F-14 |
| SyR-NF-1 | StR-8 | TC-21 (performance) |
| SyR-IF-1 | StR-2 | SRS-IF-4 |
| {{SyR-...}} | {{StR-...}} | {{SRS-... / TC-...}} |

> Every SyR row should have at least one StR it traces back to. A SyR with no backward link is a sign you invented a requirement no stakeholder asked for — challenge it.

---

## 8. Verification Approach

> For each *class* of requirement, state how it will be verified. The four classic verification methods are **Inspection** (review the artefact), **Analysis** (calculate/model), **Demonstration** (operate it and observe), and **Test** (run defined cases against defined criteria). You do not need a method per requirement here — one approach per requirement class is enough at SyRS level; detailed test cases come later.

| Requirement class | Verification method(s) | Notes |
|---|---|---|
| Functional (SyR-F-N) | {{Test / Demonstration}} | {{e.g., each SyR-F has at least one acceptance test case}} |
| Non-functional (SyR-NF-N) | {{Test / Analysis}} | {{e.g., performance measured under defined load}} |
| Interface (SyR-IF-N) | {{Test / Inspection}} | {{e.g., contract tests against each external interface}} |
| Constraints (CON-N) | {{Inspection / Analysis}} | {{e.g., compliance reviewed against the named standard}} |

---

## 9. Open Questions

> Requirements still being resolved. Capture the question and what is blocking it or who must decide. Resolve and remove as the work progresses.

- **OQ-1** {{question}} — {{what's blocking, who needs to decide}}
- **OQ-2** {{question}} — {{...}}
- ...

---

## 10. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — especially the boundary in §1.2)
- §2 System Overview and Context (the boundary and context are the heart of a SyRS)
- §3 System Functional Requirements
- §7 Traceability (at least a starter table — a SyRS with no link back to stakeholder needs is unanchored)
- §10 Revision History

**Optional sections** (include if relevant):
- §4 Non-Functional / Quality Requirements (omit only if genuinely none are known yet; usually present)
- §5 External System Interfaces (omit if the system has no external interfaces — rare)
- §6 Constraints and Assumptions (include if any exist; most systems have them)
- §8 Verification Approach (defer if too early, but plan to add before sign-off)
- §9 Open Questions (track elsewhere if you prefer)

**Tailoring**:
- The SyRS is a *system*-level document. Keep software-only detail out of it — that belongs in the SRS that derives from this one. If you find yourself specifying functions of a single software component, you have dropped a level; move it to the SRS.
- If your project is pure software with no meaningful hardware/people/process scope, consider skipping the SyRS and writing an SRS directly.
- Identifier conventions: **SyR-F-N** (functional), **SyR-NF-N** (non-functional / quality), **SyR-IF-N** (interface), **CON-N** (constraint), **ASM-N** (assumption), **OQ-N** (open question). These prefixes enable cross-document traceability — StR → SyR → SRS → test.
- Revision history is mandatory. Track every substantive change with a version bump.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29148:2018 standard, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
