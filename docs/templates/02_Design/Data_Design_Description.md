# Data Design Description Template

> **Template purpose:** Lightweight Data Design Description (DDD) structure aligned to IEEE 1016-2009 (information/data viewpoint) and ISO/IEC 25012:2008 (data quality model). Use this template when documenting the data half of a system's design — what data the system holds, how it is shaped, and the rules that keep it trustworthy. Replace `{{placeholder}}` content with system-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When designing a system or module whose data needs deliberate design — entities, schemas, integrity rules, quality targets, security, migration, backup. The DDD sits beside the Software Design Description (SDD): the SDD covers HOW the code behaves; the DDD covers WHAT data exists and the rules that govern it. Together they realize the requirements in the SRS.
>
> **Companion standard:** IEEE 1016-2009 (information/data viewpoint) + ISO/IEC 25012:2008 (data quality model).
>
> **Status of this template:** A lightweight skeleton derived from public sources, aligned to IEEE 1016-2009 (information/data viewpoint) and ISO/IEC 25012:2008 (data quality model), structured for solo/small-team use. It paraphrases the publicly-known outline and characteristic names only and reproduces no normative text from the standards (both IEEE 1016-2009 and ISO/IEC 25012:2008 are paywalled). The §6 Data Quality characteristic list should be checked against the official ISO/IEC 25012 set before relying on it for compliance. Domain section set: Data Context, Data Model, Data Entities, Data Elements, Data Integrity Rules, Data Security and Privacy, Data Migration, Backup and Recovery. For regulated, safety-critical, or contractual contexts, verify against the full standards rather than relying on this lightweight version.

---

# Data Design Description — {{System Name}}

| Field | Value |
|---|---|
| Document ID | DD-{{SYSTEM-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 1016-2009 (information viewpoint) + ISO/IEC 25012:2008 (data quality) (lightweight) |
| Owner | {{Project name or owner}} |
| Companion standards | IEEE 1016-2009 (information viewpoint) + ISO/IEC 25012:2008 (data quality) (lightweight) |
| Realizes | {{SRS-ID data requirements, e.g. SRS-{{SYSTEM-ID}}-001 §x}} |
| Related SDD | {{SDD-MODULE-ID(s) whose information design this DDD details}} |
| Data classification | {{Highest sensitivity tier held, e.g. Confidential / contains PII}} |
| Primary data store(s) | {{Engine(s) and version, e.g. PostgreSQL 16, SQLite, Parquet on object store}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> This section frames the document. A reader who knows nothing about the system should be able to read §1 and understand what this document is, what data it covers, what the words mean, and which other documents it connects to. A **Data Design Description (DDD)** is the document that pins down *what* data the system holds and the rules that keep it trustworthy — it is the data half of the design, sitting beside the Software Design Description (SDD), which covers *how* the code behaves. Both realize the requirements stated in the SRS. Fold the four standard subsections below into this section.

### 1.1 Purpose

> One paragraph, mirroring the SDD's voice. State plainly that this is the *data half* of the design — the SDD is the behavior half.

This document specifies the data design for **{{System Name}}**. It describes the data the system holds, its conceptual / logical / physical models, and the integrity, quality, security, and lifecycle rules that govern it. It realizes the data-related requirements in the SRS ({{SRS-ID}}) and complements the Software Design Description ({{SDD-MODULE-ID}}), which covers behavior and interfaces (HOW) rather than data shape (WHAT data). In short: the SDD is the behavior half of the design and this DDD is the data half — read together they describe how {{System Name}}'s requirements are realized.

### 1.2 Scope

> List what data domains and stores this DDD covers, and what it explicitly excludes (with a one-line reason each). This is the same two-list "In scope / Out of scope" shape the SDD uses — it tells the reader where to stop expecting detail.

In scope:
- {{Data domain 1 — e.g. user accounts and profiles}}
- {{Data domain 2 — e.g. orders and line items}}
- {{Primary store: {{engine}} holding {{which entities}}}}

Out of scope for v1:
- {{Application/operational logs and telemetry}} — {{deferred; covered by the observability design, not data-of-record}}
- {{Third-party-owned data (e.g. payment-processor records)}} — {{owned and stored by {{provider}}; we hold only references}}
- {{Deferred domain}} — {{reason for deferral}}

### 1.3 Definitions and Acronyms

> Define every term that, if misread, would derail the rest of the document. This table is pre-seeded with the core data-design vocabulary used below so a first-time reader is never blocked. Add system-specific terms; delete any you do not use.

| Term | Definition |
|---|---|
| Entity | A "thing" the system tracks (e.g. Customer, Order, Document). Almost always becomes a database table. |
| Element / Attribute | One piece of information about an entity (e.g. `Customer.email`, `Order.total`). Becomes a column. |
| Primary key (PK) | The column (or set of columns) that uniquely identifies one row of an entity — no two rows share it. |
| Foreign key (FK) | A column in one entity that points at the primary key of another; this is how a relationship is stored (e.g. `Order.customer_id` → `Customer.id`). |
| Referential integrity | The guarantee that every foreign key points at a row that actually exists — no orphaned `Order` left pointing at a deleted `Customer`. |
| Cardinality | How many of one entity relate to how many of another: 1:1, 1:many, or many:many. |
| Normalization | Organizing tables so each fact lives in exactly one place, to avoid contradictory copies. The starting instinct: don't store the same fact twice. |
| Data dictionary | The catalog of every data element with its meaning, type, format, allowed values, and sensitivity. §4 and §5 of this document *are* the data dictionary. |
| Conceptual / logical / physical model | Three zoom levels of the same data: real-world things and relationships (plain language) → tables/attributes/keys (engine-agnostic) → the actual schema for the chosen engine. |
| PII | Personally Identifiable Information — data that can identify a person; drives encryption, masking, and access rules. |
| RPO | Recovery Point Objective — how much recent data you can afford to lose (set by how often you back up). |
| RTO | Recovery Time Objective — how fast you must be back online after a failure. |
| ETL | Extract, Transform, Load — the standard frame for moving data from an old store into a new one. |
| {{System-specific term}} | {{Definition}} |

### 1.4 References

> A numbered reference table. List the SRS this DDD realizes, the related SDD(s), the data-store/engine documentation, any applicable regulations, and the two companion standards. Referencing the SRS here is what creates **traceability** — a reader can check that every data requirement landed somewhere in this document (an SRS data requirement should be findable as an ENT-N entity, an ELEM-N element, or an INT-N integrity rule below).

| Ref | Document |
|---|---|
| R1 | {{SRS being realized — e.g. `docs/srs.md` SRS-{{SYSTEM-ID}}-001 §x (data requirements)}} |
| R2 | {{Related SDD(s) — e.g. SDD-{{MODULE-ID}}-001, the module(s) whose information design this DDD details}} |
| R3 | {{Data-store / engine documentation — e.g. PostgreSQL 16 manual, SQLite docs}} |
| R4 | {{Applicable regulation — e.g. GDPR, HIPAA — only if regulated data is held; otherwise delete}} |
| R5 | IEEE 1016-2009 — Standard for Information Technology — Systems Design — Software Design Descriptions (information viewpoint). |
| R6 | ISO/IEC 25012:2008 — Software engineering — Software product Quality Requirements and Evaluation (SQuaRE) — Data quality model. |
| ... | ... |

---

## 2. Data Context

> This is the 30,000-foot view: where data comes **from**, where it goes **to**, and where it lives in between — *before* any table design. The reader should finish §2 with a mental map of the data's journey through the system. This section sets context only; the precise table shapes are pinned down in §3 onward.

### 2.1 Data sources

> Where does data enter the system? Each row is an input. "Trust level" matters because data from an external feed you don't control needs more validation (§7) than data your own form produces.

| Source | Type | Owner | Trust level |
|---|---|---|---|
| {{User registration form}} | {{User input}} | {{This system}} | {{Validated at entry — medium}} |
| {{Partner pricing feed}} | {{External feed}} | {{Partner X}} | {{Untrusted — full validation + reconciliation}} |
| {{Internal batch job}} | {{System-generated}} | {{This system}} | {{Trusted}} |
| ... | ... | ... | ... |

### 2.2 Data consumers

> Who or what reads the data once it is stored? Naming consumers up front prevents the "we forgot the reporting system also reads this" surprise that breaks a schema change later.

| Consumer | What it reads | Access mode |
|---|---|---|
| {{Web application}} | {{ENT-1, ENT-2}} | {{Read/write}} |
| {{Nightly reporting export}} | {{ENT-1 (read-only snapshot)}} | {{Read-only}} |
| {{Downstream service Y}} | {{ENT-3 via API}} | {{Read-only}} |
| ... | ... | ... |

### 2.3 Data flow

> Describe the path data takes from source through stores to consumers. A simple labeled flow is enough for most small systems; the formal name for a drawn version is a **Data Flow Diagram (DFD)** if you want to look it up.

{{Plain-language flow, e.g.:}}

`{{user form}} -> {{app-layer validation}} -> {{primary store (ENT-1)}} -> {{nightly export}} -> {{reporting system}}`

{{Add a second flow line per major path. Note any point where data is transformed, fanned out, or copied — those points are where integrity rules (§7) and quality checks (§6) usually live.}}

### 2.4 Data stores

> One row per place data physically lives. The "classes of data" column connects each store to the sensitivity tiers in §6 and to the backup design in §10.

| Store | Engine / version | Purpose | Classes of data held |
|---|---|---|---|
| {{Primary DB}} | {{PostgreSQL 16}} | {{System of record for ENT-1..ENT-3}} | {{Internal, Confidential, PII}} |
| {{Cache}} | {{Redis 7}} | {{Ephemeral session/lookup cache}} | {{Internal (no PII persisted)}} |
| {{Archive}} | {{Parquet on object store}} | {{Cold historical snapshots}} | {{Confidential}} |
| ... | ... | ... | ... |

### 2.5 Retention overview

> High-level "how long do we keep it, then what" per store. This is the headline only — the per-element retention is pinned down in §5, and the disposal mechanics in §7 and §8.

| Store | Retention (high-level) | Disposal |
|---|---|---|
| {{Primary DB}} | {{Active records retained while account is live}} | {{Soft-delete then purge after {{N}} days}} |
| {{Archive}} | {{{{N}} years for compliance}} | {{Automated expiry}} |
| ... | ... | ... |

---

## 3. Data Model

> This is the heart of the IEEE 1016 information viewpoint. The same data is described **three times** at increasing precision: **conceptual** (plain-language things and relationships), **logical** (tables / attributes / keys, independent of any specific database), and **physical** (the actual schema for the engine you chose). You move from conceptual down to physical as decisions firm up — it is completely fine for an early draft to have only the conceptual level filled in, with the logical and physical levels marked `{{TBD}}` until choices are made.

### 3.1 Conceptual model

> Name the major entities and how they relate, in plain language, plus a simple entity-relationship sketch. **Cardinality** notation appears here for the first time: 1:1 (one-to-one), 1:many (one-to-many), many:many (many-to-many). A many:many relationship almost always needs a **join / link table** sitting between the two entities to hold the pairings.

{{Prose, e.g.: "A {{Customer}} places many {{Order}}s (1:many). Each {{Order}} contains many {{Line Item}}s (1:many). {{Student}}s enroll in many {{Course}}s and each {{Course}} has many {{Student}}s (many:many) — so a `{{Enrollment}}` link table holds each student–course pairing."}}

Entity-relationship sketch (text form is fine for a draft):

```
{{Customer}}  1 ────< many  {{Order}}
{{Order}}     1 ────< many  {{Line Item}}
{{Student}} many >──< many  {{Course}}     (via {{Enrollment}} link table)
```

### 3.2 Logical model

> Turn the conceptual entities into tables with attributes, primary keys, and foreign keys — **still independent of any specific database engine**. This is where **normalization** enters: organize so each fact lives in exactly one place (don't store the same fact twice). Mark this `{{TBD}}` if the conceptual model is still settling.

**{{Customer}}** (PK: `id`)
- `id`, `email`, `display_name`, `created_at`

**{{Order}}** (PK: `id`; FK: `customer_id` → {{Customer}}.`id`)
- `id`, `customer_id`, `total`, `placed_at`, `status`

**{{Enrollment}}** (link table; PK: (`student_id`, `course_id`); FKs to {{Student}} and {{Course}})
- `student_id`, `course_id`, `enrolled_at`

{{Repeat per entity. Note any normalization decision and its reason.}}

### 3.3 Physical model

> The engine-specific realization: actual table/column types, indexes, partitioning, and any **denormalization** (deliberately duplicating a fact for speed) with its justification. This reuses the SDD's schema-table shape so physical schemas read consistently across the two documents. Mark `{{TBD}}` until the engine is chosen.

#### 3.3.1 Table `{{schema}}.{{customer}}`

**Table `{{schema}}.{{customer}}`** — {{the system of record for ENT-1 Customer}}.

| Column | Type | Notes |
|---|---|---|
| `id` | {{BIGINT / UUID}} | {{PK}} |
| `email` | {{VARCHAR(320)}} | {{ELEM-1; UNIQUE; PII}} |
| `display_name` | {{VARCHAR(255)}} | {{ELEM-2}} |
| `created_at` | {{TIMESTAMPTZ}} | {{default now()}} |

Indexes: {{`idx_customer_email` (UNIQUE)}}. Partitioning: {{none / by `created_at` month}}. Denormalization: {{none / `order_count` cached here, justified by hot read path — kept consistent by trigger INT-N}}.

#### 3.3.2 Table `{{schema}}.{{order}}`

{{Repeat the Column / Type / Notes table per physical table. Use {{TBD}} freely in early drafts.}}

---

## 4. Data Entities

> An **entity** is a "thing the system tracks," and it almost always becomes a table. This section is the entity-level catalog: one row per entity, traceable by **ENT-N** so an SRS data requirement or an SDD information-design entry can point straight at it. The **Owner** column answers a load-bearing question once data is shared: *who is allowed to change this data, and who is authoritative when two copies disagree?* The **Relationships** column should name the related entity **and** the cardinality.

| ID | Entity | Description | Key Attributes | Relationships | Owner | Volume / Growth |
|---|---|---|---|---|---|---|
| ENT-1 | {{Customer}} | {{A person/org with an account}} | {{`id` (PK), `email`}} | {{ENT-2 Order — 1:many}} | {{Accounts module}} | {{~50k rows, +5%/yr}} |
| ENT-2 | {{Order}} | {{A purchase placed by a customer}} | {{`id` (PK), `customer_id` (FK)}} | {{ENT-1 Customer — many:1; ENT-3 Line Item — 1:many}} | {{Orders module}} | {{~500k rows, +20%/yr}} |
| ENT-3 | {{Line Item}} | {{One product line within an order}} | {{`id` (PK), `order_id` (FK)}} | {{ENT-2 Order — many:1}} | {{Orders module}} | {{~2M rows, +20%/yr}} |
| ... | ... | ... | ... | ... | ... | ... |

> The **Volume / Growth** column is not decoration — a rough row count and growth rate drives storage sizing, indexing strategy, and backup window (§10).

For each non-trivial entity, add a short prose paragraph below covering lifecycle and ownership:

**ENT-1 {{Customer}}.** Lifecycle: {{rows created at registration; updated on profile edit; archived (soft-deleted) on account closure; hard-purged after {{N}} days per §7/§8}}. Ownership: {{the Accounts module is the system of record; other modules read but never write Customer fields directly — they request changes through the Accounts API. If a cached copy elsewhere disagrees, the Accounts store wins.}}

{{Repeat per non-trivial entity.}}

---

## 5. Data Elements (Data Dictionary)

> This is the per-field catalog — the **data dictionary**. Every column of every entity is defined exactly once, so nobody has to guess what a field means or what may legitimately go in it. Each element is traceable by **ELEM-N** and tied to its parent entity (**ENT-N**). Group elements under their parent entity for readability.
>
> **Beginner aside — Type vs. Format are not the same thing.** *Type* is the storage type the database uses (`VARCHAR(255)`, `INTEGER`, `TIMESTAMPTZ`). *Format* is the human/business shape the value must follow (`E.164 phone number`, `ISO-8601 date`, `lowercase email`). A field can be stored as `VARCHAR(20)` (Type) while being required to match the `E.164` pattern (Format). Both matter for validation, so both get a column.
>
> The **Sensitivity** column uses the classification scheme defined in §6 (Public / Internal / Confidential / PII) — it is what §6 (security), §7 (integrity/disposal), and §8 (backup scope) act on. The **Retention** column likewise feeds §7 and §8. **Required?** says whether the value may be null; **Default** gives the value used when none is supplied.

### 5.1 Elements of ENT-1 {{Customer}}

| ID | Entity | Element | Type | Format | Required? | Default | Valid Values | Sensitivity | Retention |
|---|---|---|---|---|---|---|---|---|---|
| ELEM-1 | ENT-1 | `email` | {{VARCHAR(320)}} | {{lowercase, RFC-5322}} | {{Yes}} | {{—}} | {{valid email}} | {{PII}} | {{life of account + {{N}}d}} |
| ELEM-2 | ENT-1 | `display_name` | {{VARCHAR(255)}} | {{free text}} | {{No}} | {{NULL}} | {{1–255 chars}} | {{Internal}} | {{life of account}} |
| ELEM-3 | ENT-1 | `phone` | {{VARCHAR(20)}} | {{E.164}} | {{No}} | {{NULL}} | {{`+` + digits}} | {{PII}} | {{life of account + {{N}}d}} |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

### 5.2 Elements of ENT-2 {{Order}}

| ID | Entity | Element | Type | Format | Required? | Default | Valid Values | Sensitivity | Retention |
|---|---|---|---|---|---|---|---|---|---|
| ELEM-10 | ENT-2 | `total` | {{NUMERIC(12,2)}} | {{decimal, 2 dp}} | {{Yes}} | {{0.00}} | {{>= 0}} | {{Internal}} | {{7 years (financial)}} |
| ELEM-11 | ENT-2 | `status` | {{VARCHAR(16)}} | {{enum}} | {{Yes}} | {{`pending`}} | {{`pending`/`paid`/`shipped`/`cancelled`}} | {{Internal}} | {{7 years}} |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

{{Repeat one sub-section per entity.}}

---

## 6. Data Quality (ISO/IEC 25012)

> **ISO/IEC 25012** is a standard that names the qualities that make data trustworthy — instead of *assuming* the data is good, you *state* what "good" means and how you'll measure it. This section turns those qualities into a checklist (**DQ-N**) so quality is explicit, not hoped-for.
>
> Keep only the characteristics that matter for **this** system and **delete the rest** rather than padding the table. The full publicly-known characteristic set is: **Accuracy, Completeness, Consistency, Credibility, Currentness** (up-to-dateness), and — system-dependent — **Accessibility, Compliance, Confidentiality, Efficiency, Precision, Traceability, Understandability, Availability, Portability, Recoverability.** (Verify this list against the official ISO/IEC 25012 set before relying on it for compliance — see the Status note.)
>
> These DQ targets must **agree** with the rest of the document: *Confidentiality* maps onto §8 security, *Recoverability / Availability* onto §10 backup, and *Accuracy / Completeness / Consistency* onto the §7 integrity rules. If a DQ target and an integrity rule disagree, one of them is wrong.

| ID | Characteristic | What it means here | Target / metric | How measured | Owner |
|---|---|---|---|---|---|
| DQ-1 | Accuracy | {{Stored value matches the real-world fact it represents}} | {{>= 99.5% of `email` deliverable}} | {{Bounce-rate sample / quarterly audit}} | {{Data steward}} |
| DQ-2 | Completeness | {{Required elements are present}} | {{100% of required fields non-null (enforced by INT-N)}} | {{Nightly null-scan count}} | {{Orders module}} |
| DQ-3 | Consistency | {{Copies of a fact agree; no contradictions across stores}} | {{0 reconciliation mismatches}} | {{Daily reconciliation job}} | {{Data steward}} |
| DQ-4 | Currentness | {{Data is up to date relative to its source}} | {{Pricing feed <= 24h stale}} | {{Feed timestamp check}} | {{Integrations}} |
| DQ-5 | Confidentiality | {{Only authorized parties can read sensitive elements}} | {{0 unauthorized-access events}} | {{Audit-log review (§8)}} | {{Security owner}} |
| DQ-6 | Recoverability | {{Data can be restored after loss within objectives}} | {{Meets RPO/RTO in §10}} | {{Quarterly restore test (§10.4)}} | {{Ops}} |
| ... | {{delete unused characteristics}} | ... | ... | ... | ... |

---

## 7. Data Integrity Rules

> These are the rules that **stop bad or contradictory data from entering or persisting.** A rule can live in three places, and where it lives matters: **in the data itself** (database constraints — `NOT NULL`, `UNIQUE`, `CHECK`, foreign-key constraints — the strongest because the database enforces them no matter what code runs); **in the application** (validation before a write); or **in periodic checks** (reconciliation jobs that catch drift after the fact). Prefer the database when you can.
>
> **Referential integrity** (defined here for the first time): the guarantee that every foreign key points at a row that actually exists. Without it you get **orphaned records** — e.g. an `Order` whose `customer_id` points at a `Customer` that was deleted, leaving data that can never be correctly interpreted again.
>
> Each rule is traceable by **INT-N**, and the **Realizes** column links it to the DQ-N quality characteristic it supports — so §6 and §7 stay in agreement. INT-N rules are directly testable and should be cited from the verification/test approach in the SRS or SDD.

| ID | Rule | Type | Enforcement point | On-violation behavior | Realizes |
|---|---|---|---|---|---|
| INT-1 | {{`Customer.email` must be unique}} | {{Entity}} | {{DB constraint (UNIQUE)}} | {{Reject}} | {{DQ-1}} |
| INT-2 | {{`Order.customer_id` must reference an existing Customer}} | {{Referential}} | {{DB constraint (FK)}} | {{Reject}} | {{DQ-3}} |
| INT-3 | {{`Order.total` must be >= 0}} | {{Domain}} | {{DB constraint (CHECK) + app}} | {{Reject}} | {{DQ-1}} |
| INT-4 | {{Sum of Line Item amounts must equal Order.total}} | {{Cross-entity}} | {{App + nightly reconciliation}} | {{Quarantine + log}} | {{DQ-3}} |
| INT-5 | {{`Order.shipped_at` must be after `placed_at`}} | {{Temporal}} | {{App}} | {{Reject}} | {{DQ-1}} |
| INT-6 | {{Required fields per §5 must be non-null}} | {{Entity}} | {{DB constraint (NOT NULL)}} | {{Reject}} | {{DQ-2}} |
| ... | ... | ... | ... | ... | ... |

> Type legend: **entity** (a rule about a single row's own fields), **referential** (foreign-key integrity), **domain** (allowed values/range of one field), **cross-entity** (a rule spanning two or more entities), **temporal** (ordering/recency of timestamps).

---

## 8. Data Security and Privacy

> The goal of this section is simple: **protect each element in proportion to its sensitivity** (the sensitivity set per element in §5). This section operationalizes the *Confidentiality* characteristic (and parts of *Compliance*) from §6.

### 8.1 Classification scheme

> Define the sensitivity tiers so §5's Sensitivity column actually means something. A common four-tier scheme is below — adjust the names/definitions to your context. **PII = Personally Identifiable Information** (data that can identify a person).

| Tier | Definition | Handling baseline |
|---|---|---|
| Public | {{Safe to disclose to anyone}} | {{No restriction}} |
| Internal | {{Non-sensitive but not for public release}} | {{Auth required}} |
| Confidential | {{Business-sensitive; limited audience}} | {{Encrypted, least-privilege}} |
| PII | {{Identifies a person}} | {{Encrypted, masked in logs, access-audited, retention-bound}} |

### 8.2 Access control

> Who/what may **read** vs **write** each tier. Default to **least privilege** — grant the minimum access a role needs, nothing more.

| Tier | Read | Write |
|---|---|---|
| Public | {{Anyone}} | {{Admins}} |
| Internal | {{Authenticated roles}} | {{Owning module}} |
| Confidential | {{Named roles}} | {{Owning module}} |
| PII | {{Named roles + business justification}} | {{Owning module}} |

### 8.3 Encryption

> **At rest** = data scrambled while stored on disk, so a stolen drive is useless. **In transit** = data scrambled while moving over the network, so it can't be read mid-flight. Different protections; usually both are needed. State which stores and channels are covered.

- At rest: {{full-disk + column encryption on PII fields (ELEM-1, ELEM-3) in the primary store}}
- In transit: {{TLS 1.2+ on all client and inter-service connections}}
- Key management: {{where keys live, how rotated}}

### 8.4 Masking / anonymization

> How sensitive fields are obscured where the full value isn't needed — **logs**, **non-production environments**, and **exports**. A leaked debug log full of real emails is a classic avoidable breach.

- Logs: {{PII redacted or tokenized before write}}
- Non-prod: {{production data masked/synthesized before loading into staging}}
- Exports: {{PII columns hashed/omitted unless export is explicitly authorized}}

### 8.5 Audit

> What data access and changes are logged, and where the audit trail lives. This is the evidence behind DQ-5 (Confidentiality).

- Logged events: {{reads of PII, all writes to Confidential/PII tiers, permission changes}}
- Where: {{append-only audit store, retained {{N}} days}}

### 8.6 Privacy and disposal

> Retention enforcement, secure deletion, and regulatory duties. **These only apply if regulated/PII data is held** — if none is, state that and move on.

- Retention enforcement: {{automated purge per the Retention column in §5}}
- Secure deletion: {{crypto-erase / overwrite; soft-delete then hard-purge after {{N}} days}}
- Regulatory duties (if PII): {{data-subject access requests, right-to-erasure — describe the mechanism, or state "N/A — no regulated data held"}}

---

## 9. Data Migration

> Moving data from an old store/format into the new one. The standard frame is **ETL**: **E**xtract from the old store, **T**ransform to the new shape (the entities and elements defined in §3–§5), **L**oad into the target. The non-negotiable beginner lesson: **a migration without a rollback plan is a one-way risk** — once you've overwritten the source, there may be no way back.
>
> If there is nothing to migrate, mark the whole section **"N/A — greenfield system, no source data"** rather than inventing content.

### 9.1 Source inventory

> What is being migrated, its current shape, who owns it, and any known quality problems you'll inherit.

| Source | Current shape | Owner | Quality caveats |
|---|---|---|---|
| {{Legacy CSV export}} | {{flat file, mixed encodings}} | {{Ops}} | {{~2% missing emails; duplicate rows}} |
| ... | ... | ... | ... |

### 9.2 Mapping

> Old field → new **ELEM-N**, with the transformation rule, and how unmappable or mismatched values are handled. This is where most migration bugs hide.

| Old field | New element | Transformation | Mismatch handling |
|---|---|---|---|
| {{`cust_email`}} | {{ELEM-1 `email`}} | {{lowercase, trim}} | {{invalid → quarantine row, log}} |
| {{`tel`}} | {{ELEM-3 `phone`}} | {{normalize to E.164}} | {{unparseable → set NULL, flag}} |
| ... | ... | ... | ... |

### 9.3 Validation

> Pre- and post-migration counts and checks that **prove** the move was faithful. Cite the INT-N rules and DQ-N targets you're validating against.

- Pre-migration: {{row counts per source; baseline null counts}}
- Post-migration: {{target counts == expected; INT-1..INT-6 all pass; DQ-2 completeness >= target}}

### 9.4 Rollback

> How to safely abort and restore the prior state, and the **point of no return** (the moment after which rollback is no longer clean).

- Rollback procedure: {{restore target from pre-migration snapshot; re-point app to old store}}
- Point of no return: {{first production write to the new store after cutover}}

### 9.5 Reconciliation

> After cutover, compare source and target to prove **nothing was lost or duplicated**.

- {{Row-count and checksum comparison of source vs target per entity; investigate any delta}}

---

## 10. Backup and Recovery

> Two numbers drive this whole section. **RPO (Recovery Point Objective)** = how much recent data you can afford to lose — set by how often you back up (a 1-hour RPO means at most 1 hour of data lost). **RTO (Recovery Time Objective)** = how fast you must be back online after a failure. Together they realize the *Recoverability* and *Availability* characteristics from §6.
>
> The beginner trap to avoid: **a backup that has never been restored is not a backup.** Until a test restore proves it works, you don't actually have a recovery capability — you have a hopeful copy.

### 10.1 Backup strategy

> What is backed up, full vs. incremental, how often, and where the copies live. An **offsite or immutable** copy protects against a disaster (or ransomware) that takes out the primary site.

| Store | What | Type | Frequency | Where copies live |
|---|---|---|---|---|
| {{Primary DB}} | {{ENT-1..ENT-3}} | {{Full weekly + incremental hourly}} | {{Hourly}} | {{Onsite + offsite object store (immutable)}} |
| {{Archive}} | {{snapshots}} | {{Full}} | {{Monthly}} | {{Offsite}} |
| ... | ... | ... | ... | ... |

### 10.2 Recovery objectives

> The agreed RPO and RTO per store/data class, with the rationale — *why* this number and not a stricter or looser one.

| Store / data class | RPO | RTO | Rationale |
|---|---|---|---|
| {{Primary DB (financial)}} | {{1 hour}} | {{4 hours}} | {{Financial records — minimal loss tolerable}} |
| {{Cache}} | {{N/A — rebuildable}} | {{minutes}} | {{Ephemeral; regenerated from primary}} |
| ... | ... | ... | ... |

### 10.3 Restoration procedure

> The actual steps to restore, and **who is authorized to run them**. A procedure nobody can execute under pressure is not a procedure.

1. {{Identify the backup to restore (timestamp closest to before the incident).}}
2. {{Provision/clear target store.}}
3. {{Restore full + replay incrementals.}}
4. {{Run INT-N integrity checks; reconcile counts.}}
5. {{Re-point application; verify.}}

Authorized operators: {{role(s)}}.

### 10.4 Testing

> How and how often restores are rehearsed. This is the step that makes §10 real (see the beginner trap above).

- {{Quarterly restore drill into an isolated environment; record RTO actually achieved vs target; sign-off by Ops.}}

---

## 11. Open Questions

> Write down the data questions you couldn't settle yet — engine choice, partitioning, exact retention, PII scope — rather than leaving them implicit. **An unrecorded open question is the thing that derails the next person.** Two buckets, same shape the SDD uses.

### 11.1 Deferred with defaults

> Each entry states the question **and** a working default, so the project isn't blocked while the question stays open.

- **OQ-DEF-1** {{Final retention period for audit logs}} — *default: {{90 days}}; revisit if compliance review requires longer.*
- **OQ-DEF-2** {{Partitioning strategy for ENT-2 Order}} — *default: {{none until table exceeds {{N}} rows}}.*
- **OQ-DEF-3** {{Exact PII scope of ELEM-{{N}}}} — *default: {{treat as PII until reviewed}}.*
- ...

### 11.2 Resolved (recorded for traceability)

> Kept so future readers see *why* a contested data decision went the way it did.

- **OQ-1** {{Chosen primary engine}}: {{resolved — {{PostgreSQL 16}}, for {{FK enforcement + JSON support}}; SQLite rejected for {{concurrency}}.}}
- ...

---

## 12. Revision History

> The document's own audit trail, identical in shape to the sibling templates. Bump the version and add a row for **every substantive change** to the data design — schema changes especially, because a data-design change ripples into migration (§9), backups (§10), and downstream code.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Data Context
- §3 Data Model (at minimum the conceptual level)
- §4 Data Entities
- §5 Data Elements (Data Dictionary)
- §7 Data Integrity Rules
- §12 Revision History

**Optional sections** (include if relevant):
- §6 Data Quality (recommended for any system where data correctness matters; keep only the ISO/IEC 25012 characteristics that apply and delete the rest)
- §8 Data Security and Privacy (required if any Confidential/PII data is held; omittable for purely public/internal non-sensitive data)
- §9 Data Migration (mark "N/A — greenfield system" if there is no source data)
- §10 Backup and Recovery (defer only for a throwaway prototype; required for anything holding data of record)
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (for cross-document traceability):
- ENT-N: data entities
- ELEM-N: data elements (attributes)
- INT-N: data integrity rules
- DQ-N: data-quality characteristics (ISO/IEC 25012)
- OQ-N / OQ-DEF-N: open questions (resolved / deferred-with-defaults)
- DD-{{SYSTEM-ID}}-001: this document

These prefixes enable cross-document traceability — an SRS data requirement or an SDD information-design entry can point at a specific ENT-N or ELEM-N here, and tests can cite INT-N integrity rules.

**Tailoring**:
- The conceptual / logical / physical split (§3) is a zoom control, not three mandatory documents. Early drafts fill in only the conceptual level and mark the rest `{{TBD}}`.
- Keep only the ISO/IEC 25012 quality characteristics in §6 that matter for the system; delete the rest rather than padding.
- **Solo developer / small team:** collapse to §1, §3 (conceptual + physical), §4, §5, §7, and §12 — that is a usable data design. Fold §6 quality targets into the §7 integrity table if a separate quality section is overkill, merge §2 into a few sentences in §1.2, and keep §8/§9/§10 only when you actually hold sensitive data, are migrating from a real source, or are storing data you can't afford to lose. The Owner column in §4 can name *you* — the point is recording who is authoritative, not implying a team.
- Revision history is mandatory. Track every substantive schema or rule change with a version bump, because data-design changes ripple into migration, backup, and downstream code.

**For regulated/safety-critical projects:** use the full IEEE 1016-2009 and ISO/IEC 25012:2008 standards, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products; it reproduces no normative text from either paywalled standard.
