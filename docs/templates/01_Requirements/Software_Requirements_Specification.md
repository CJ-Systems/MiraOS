# Software Requirements Specification Template

> **Template purpose:** Lightweight Software Requirements Specification structure following ISO/IEC/IEEE 29148:2018. Use this template when starting a new SRS document. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Start of any project that needs documented requirements. The SRS is the highest-level "what does this system do, for whom, under what constraints" document. Subsequent documents (architecture, module specs, ADRs) describe HOW the requirements are realized.
>
> **Companion standard:** ISO/IEC/IEEE 29148:2018 — Systems and software engineering — Life cycle processes — Requirements engineering.
>
> **Status of this template:** Lightweight extract from `docs/srs.md` (Mira-OS project). Faithful to the 29148 outline but reduced for solo/small-team use. Verify against the full standard for enterprise/regulated contexts.

---

# Software Requirements Specification — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | SRS-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29148:2018 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Scope | {{Internal documentation / Public / Customer-facing}} |

---

## 1. Introduction

### 1.1 Purpose

> One-paragraph statement of what this document is for and what it specifies. Should establish that this is the highest-level requirements document for the project and that subsequent docs describe HOW.

{{This document specifies what {{Project Name}} is, why it exists, what it must do, for whom, and under what constraints. It is the highest-level system requirements specification for the project. Subsequent documents (Architecture Description, module specs, ADRs) describe how the requirements are realized.}}

### 1.2 Scope

> Define what the system IS and what it IS NOT. Distinguish the system from related concepts that might be confused with it. Note phases if multi-phase.

**{{Project Name}} is** {{the OS / substrate / methodology / tooling for ...}}

**{{Project Name}} is NOT** {{specific instance / a specific named entity / ...}}

**Phase 1** (current): {{describe current phase scope}}

**Phase 2** (future): {{describe future phase if known, or "out of scope for this version"}}

### 1.3 Definitions and Acronyms

> Define all project-specific terminology. Include both terms unique to this project and standard terms used in a project-specific way. Aim for terms that, if undefined, would lead to misreading the rest of the document.

| Term | Definition |
|---|---|
| {{Term 1}} | {{Definition}} |
| {{Term 2}} | {{Definition}} |
| ... | ... |

### 1.4 References

> List foundational documents (memory entries, prior specs, ADRs, external standards) that this SRS depends on or that inform its content. Categorize for readability.

Foundational documents:
- {{path/to/doc.md}} — {{brief description}}
- ...

Module specifications:
- {{path/to/spec.md}} — {{brief description}}
- ...

Architecture Decision Records:
- ADR-NNNN — {{description}}
- ...

External standards:
- {{ISO/IEEE standard with version}} — {{relevance}}

---

## 2. Overall Description

### 2.1 What {{Project Name}} Is

> Substantive description of the system. What does it do? What's the inhabitant model? What's the system perspective? Avoid implementation details — focus on the WHAT.

{{Description...}}

### 2.2 Why It Exists

> The motivating hypothesis, problem statement, or user need that drove the project. Include the foundational claim being tested or the gap being filled. If the project has an experimental hypothesis, state it explicitly.

{{Motivation...}}

### 2.3 {{Inhabitant Model / User Model / Stakeholder Model}}

> Who uses this system, who is affected by it, who interacts with whose state. Define inhabitant/user/stakeholder relationships clearly.

{{User model description...}}

### 2.4 System Perspective

> Where this system fits in the broader landscape. What it is adjacent to, what it is NOT, what existing alternatives exist and how this differs. Be specific — name competitors / adjacent products / related work.

{{Perspective...}}

### 2.5 Constraints and Assumptions

> Three categories of constraint:
> - **Methodological** — non-negotiable design principles
> - **Technology** — hard technical constraints (platforms, infrastructure)
> - **Operational** — assumptions about deployment environment

**Methodological constraints** (foundational, non-negotiable):
- {{Constraint 1}}
- {{Constraint 2}}

**Technology assumptions**:
- {{Assumption 1}}
- {{Assumption 2}}

**Operational assumptions**:
- {{Assumption 1}}
- {{Assumption 2}}

---

## 3. Functional Requirements

> The substantive "what must the system do" content. Number requirements (3.1, 3.2, ...) so they can be referenced from architecture and tests. Each requirement should be:
> - Specific (testable)
> - Atomic (one thing per requirement)
> - Free of implementation detail (WHAT, not HOW)
>
> Use sub-sections to group related requirements.

### 3.1 {{Requirement category 1}}

{{Requirement description with sub-requirements as needed...}}

### 3.2 {{Requirement category 2}}

{{...}}

---

## 4. Non-Functional Requirements

> Performance, scalability, reliability, security, usability, compliance, etc. Quantify where possible.

### 4.1 Performance

{{...}}

### 4.2 Reliability

{{...}}

### 4.3 Security & Privacy

{{...}}

### 4.4 Compliance

> List any standards/regulations the system must comply with.

{{...}}

---

## 5. Verification Approach

> How will the requirements be verified? Test types, V&V approach, acceptance criteria.

{{...}}

---

## 6. Open Questions

> Requirements that are still being resolved. Include each open question and what's blocking resolution. Resolve and remove as work progresses.

- **OQ-1**: {{question}} — {{what's blocking, who needs to decide}}
- ...

---

## 7. Planned Architecture and ADRs

> Forward references: list planned architecture documents and ADRs that will describe how the requirements are realized.

| Document | Scope | Status |
|---|---|---|
| `docs/architecture.md` | System architecture | {{Planned / Draft / ...}} |
| `docs/specs/{{module}}.md` | {{Module}} specification | {{Status}} |
| ADR-NNNN | {{Decision}} | {{Status}} |

---

## 8. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Overall Description (most subsections; tailor to project)
- §3 Functional Requirements
- §8 Revision History

**Optional sections** (include if relevant):
- §4 Non-Functional Requirements (omit if early prototype with no quantifiable NFRs yet)
- §5 Verification Approach (defer if too early)
- §6 Open Questions (track elsewhere if you prefer)
- §7 Planned Architecture and ADRs (omit if not applicable)

**Tailoring**:
- Section headers from 29148 are guidance, not requirements. Add/remove subsections as the project needs.
- Keep the SRS focused on WHAT and WHY. Architecture (HOW) belongs in a separate document.
- Revision history is mandatory. Track every substantive change with version bumps.

**For regulated/safety-critical projects:** Use the full ISO/IEC/IEEE 29148:2018 standard, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
