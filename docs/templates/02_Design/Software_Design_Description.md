# Software Design Description Template

> **Template purpose:** Lightweight Software Design Description (SDD) structure following IEEE 1016-2009. Use this template when documenting the design of a software module or subsystem. Replace `{{placeholder}}` content with module-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When designing a module/subsystem and you need to document the design decisions, interfaces, and behavior for review and future reference. The SDD sits between the SRS (WHAT) and the implementation (CODE) — it documents HOW the requirements are realized.
>
> **Companion standard:** IEEE 1016-2009 — Standard for Information Technology — Systems Design — Software Design Descriptions.
>
> **Status of this template:** Lightweight extract from `docs/specs/personality.md` (Mira-OS project). Faithful to the IEEE 1016 viewpoint-based structure but tailored for module-level (not system-level) design. Verify against the full standard for enterprise/safety-critical contexts.

---

# Software Design Description — {{Module Name}}

| Field | Value |
|---|---|
| Document ID | SDD-{{MODULE-ID}}-001 |
| Version | 0.1 |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29148:2018 + IEEE 1016-2009 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: what this module is and what this document specifies about it.

This document specifies the design of the **{{Module Name}} Module** for {{Project Name}}. {{Brief description of what the module does and what it represents in the larger system.}}

### 1.2 Scope

> Define what design decisions this SDD covers and what it explicitly does NOT cover (out of scope for v1 or deferred).

In scope:
- {{Topic 1}}
- {{Topic 2}}
- {{...}}

Out of scope for v1:
- {{Deferred topic 1}} — {{reason for deferral}}
- {{Deferred topic 2}} — {{reason}}

### 1.3 Definitions and Acronyms

| Term | Definition |
|---|---|
| {{Term}} | {{Definition}} |
| ... | ... |

### 1.4 References

| Ref | Document |
|---|---|
| R1 | {{path/to/foundational/doc.md}} — {{description}} |
| R2 | {{path/to/related/spec.md}} — {{description}} |
| R3 | {{External reference / paper / standard}} |
| ... | ... |

---

## 2. Context

### 2.1 Module Purpose

> What does this module exist to do? Bullet the high-level purposes. Use PURP-1, PURP-2 etc. for traceability.

- **PURP-1** {{First purpose statement}}
- **PURP-2** {{Second purpose}}
- ...

### 2.2 Methodology

> What design principles guide this module's decisions? These are non-negotiables that the rest of the SDD operates under. Use METH-1, METH-2 etc.

- **METH-1 {{Principle name}}.** {{Description}}
- **METH-2 {{Principle name}}.** {{Description}}
- ...

### 2.3 Constraints

> Hard constraints on the module — what it must or must not do. Use CON-1 etc.

- **CON-1** {{Constraint}}
- **CON-2** {{Constraint}}
- ...

---

## 3. Information Design

> The data model, taxonomy, schemas. What state does this module own?

### 3.1 {{Domain Taxonomy / State Model}}

> If the module has a structured representation (taxonomy, state machine, ontology), describe it here.

{{Description with diagrams/tables as needed...}}

### 3.2 Data Model

> Schemas, tables, file structures. Be specific about types and constraints.

#### 3.2.1 Schema `{{schema_name}}` ({{audience}})

**Table `{{schema_name}}.{{table_name}}`** — {{purpose}}.

| Column | Type | Notes |
|---|---|---|
| {{column}} | {{TYPE}} | {{notes}} |
| ... | ... | ... |

#### 3.2.2 Schema `{{instrumentation_schema_name}}` ({{audience}}, if applicable)

{{Repeat schema structure for other schemas...}}

---

## 4. Interface Design

### 4.1 {{Primary}}-Facing API

> What operations are exposed? To whom? Use IF-1, IF-2 etc. for traceability.

| ID | Operation | Purpose |
|---|---|---|
| IF-1 | `{{operation_name}}` | {{Description}} |
| IF-2 | `{{operation_name}}` | {{Description}} |
| ... | ... | ... |

**IF-N rules:** {{Any constraints on usage, expected magnitudes, validation rules.}}

### 4.2 {{Other}}-Facing API (if applicable)

> Separate API surfaces for different audiences (agent vs human vs experimenter). State clearly which APIs each audience has access to.

{{Description...}}

---

## 5. Interaction Design

### 5.1 {{Lifecycle phase 1 — e.g., Bootstrap}}

> If the module has distinct lifecycle phases (bootstrap, steady-state, shutdown), describe each.

{{Phase description...}}

### 5.2 {{Lifecycle phase 2 — e.g., Update mechanism}}

{{Phase description...}}

### 5.3 {{Coupling / Surfacing}}

> How does this module surface state to the rest of the system? How does state enter and exit the module?

{{Coupling description...}}

### 5.4 Coupling with Other Modules

> Cross-module relationships. Be explicit about which modules can read/write what state.

| Module | Coupling |
|---|---|
| {{Module A}} | {{Description of relationship}} |
| {{Module B}} | {{Description}} |
| ... | ... |

---

## 6. Instrumentation (if applicable)

> If the module supports research/observation that is hidden from the agent or normal user, document it here.

### 6.1 Purpose

{{Why instrumentation exists...}}

### 6.2 Isolation Properties

> Use ISO-1, ISO-2 etc. for traceability. State explicit boundaries.

- **ISO-1** {{Isolation rule}}
- **ISO-2** {{Isolation rule}}
- ...

### 6.3 Storage

> Where instrumentation data lives (separate schema, separate database, etc.)

{{...}}

### 6.4 {{Special methodology if any — e.g., Multi-Model Peer Review}}

{{If the module uses unusual methods (multi-model ensembles, blind review, etc.), document here.}}

---

## 7. Antipatterns Avoided

> Explicit list of what this module is engineered NOT to do. References to antipattern catalog if applicable. Use AP-1, AP-2 etc.

This module is explicitly engineered to avoid:

- **AP-1** {{Antipattern}} — {{why excluded}}
- **AP-2** {{Antipattern}} — {{why excluded}}
- ...

---

## 8. Open Questions

> Questions still being resolved. Distinguish load-bearing OQs (block adoption) from deferred-with-defaults (have a default; revisit if defaults prove inadequate).

### 8.1 Deferred with defaults

- **OQ-DEF-1** {{Question}} — *default: {{default}}.*
- ...

### 8.2 Resolved (recorded for traceability)

- **OQ-1** {{Question}}: {{Resolution}}.
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
- §2 Context
- §3 Information Design (at minimum the data model)
- §4 Interface Design
- §9 Revision History

**Optional sections** (include if relevant):
- §5 Interaction Design (omit if module has no distinct lifecycle phases)
- §6 Instrumentation (omit if no research/observation layer)
- §7 Antipatterns Avoided (omit if not applicable; recommend including for any module that interacts with sensitive concerns)
- §8 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- PURP-N: purpose statements
- METH-N: methodology principles
- CON-N: constraints
- IF-N: interface operations
- ISO-N: isolation properties
- AP-N: antipatterns
- OQ-N / OQ-DEF-N: open questions (resolved / deferred-with-defaults)

These prefixes enable cross-document traceability — requirements in SRS can be traced to module designs in SDD via these IDs.

**For safety-critical or regulated software:** Use the full IEEE 1016-2009 standard with formal viewpoints (Context, Composition, Logical, Dependency, Information, Patterns Used, Interface, Interaction, Algorithmic). This lightweight template covers the most common viewpoints but is not the full set.
