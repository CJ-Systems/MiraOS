# Interface Requirements Specification Template

> **Template purpose:** Lightweight Interface Requirements Specification (IRS) structure following ISO/IEC/IEEE 29148:2018, in which interface requirements are a defined requirements category. Use this template to specify WHAT must cross each boundary between your system and the external systems, devices, and people it interacts with — and the rules and quality levels those exchanges must meet. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When your system exchanges data, control, or signals across a boundary with something you do not fully control — another team's service, a vendor API, a partner's message bus, a hardware device, or a human operator — and you need a single document that pins down what each interface must do before anyone agrees on the as-built wire details. The IRS sits beside the SRS/SyRS (the broader WHAT) and feeds the architecture, design, and tests (the HOW). It stays on the requirements side; the agreed-design contract (exact endpoints, payload shapes, an Interface Control Document) belongs in the design layer.
>
> **Companion standard:** ISO/IEC/IEEE 29148:2018 — Systems and software engineering — Life cycle processes — Requirements engineering. Interface requirements are a defined requirements category within 29148. Where an interface crosses a system boundary, 29148's interface requirements often pair with an Interface Control Document (ICD) practice; this template stays on the requirements side (WHAT each interface must do), not the agreed-design side (the as-built ICD).
>
> **Status of this template:** A lightweight skeleton based on ISO/IEC/IEEE 29148:2018 (its interface-requirements category) and public SWEBOK-aligned requirements-engineering practice, reduced for solo/small-team use; it paraphrases the outline only and reproduces NO normative text from the standard, which is PAYWALLED. VERIFY this template's section set and any specific clause numbering against the full standard before relying on it for enterprise, regulated, or safety-critical / contractual interface work. For those contexts also consider pairing the IRS with a formal Interface Control Document (ICD) per 29148 interface-agreement practice — this template stays on the requirements (WHAT) side and does not capture the as-built interface design.

---

# Interface Requirements Specification — {{System Name}}

| Field | Value |
|---|---|
| Document ID | IRS-{{SYSTEM-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29148:2018 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Scope | {{Internal documentation / Public / Customer-facing}} |
| Parent SRS / SyRS | {{Document ID of the requirements doc this IRS elaborates, e.g. SRS-{{SYSTEM-ID}}-001}} |
| Interfaces covered | {{Count and one-line list, e.g. 4 — Auth API, Billing webhook, Telemetry stream, Operator CLI}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph stating what this document is for. This is a *requirements* document: it specifies WHAT must be true of each interface, not how either side is built. A quick beginner orientation: an **interface** is the agreed boundary across which two systems (or a system and a person/device) exchange data, control, or signals — the IRS pins down what crosses that boundary and under what rules, not the internals of either side. The exact endpoints, payload shapes, and the as-built **Interface Control Document (ICD)** — a document that records the agreed design of an interface once both sides have settled it — belong in the design layer, not here.

{{This document specifies the interface requirements for {{System Name}}: what must cross each boundary between {{System Name}} and the external systems, devices, and people it interacts with, and the rules and quality levels those exchanges must meet. It is a requirements document — it states WHAT must be true of each interface (the data and messages that cross it, the expected responses, and the performance, security, and failure behaviour required), not HOW either side realizes that. The as-built contract details — exact endpoints, payload shapes, and any Interface Control Document — are recorded in the design layer (architecture, design descriptions, ICDs) and trace back to the requirements stated here.}}

### 1.2 Scope

> Define which interfaces are IN scope and which are explicitly OUT. As a rule of thumb: purely internal, in-process calls between modules of the same system are usually out of scope (they belong in the design of that system); cross-system, cross-process, cross-organization, and human/device boundaries are usually in. Beginner note: the single most common defect at this stage is leaving a boundary *unowned* — neither side records that it exists, so neither builds or tests it. List every boundary you can think of, even the ones you decide to mark out of scope, so the omission is a deliberate decision and not an accident.

**In scope** — interface requirements for the following boundaries:
- {{Boundary 1, e.g. {{System Name}} ↔ external Auth provider}}
- {{Boundary 2, e.g. {{System Name}} ↔ Billing partner webhook}}
- {{Boundary 3, e.g. {{System Name}} ↔ human operator (CLI / console)}}

**Out of scope** (listed deliberately so the boundary is not left unowned):
- {{Internal in-process call A ↔ B}} — internal to {{System Name}}; covered by the module design, not this IRS.
- {{Boundary X}} — {{reason it is excluded, e.g. owned by another team's IRS / deferred to a later phase}}.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define every term that, if read loosely, could cause two teams to build different things. The interface vocabulary below is where most cross-team misreadings start, so define it even when it feels obvious — plus every project-specific endpoint, partner, or product name.

| Term | Definition |
|---|---|
| Interface | The agreed boundary across which two systems (or a system and a person/device) exchange data, control, or signals. The IRS specifies WHAT must cross it and under what rules, not HOW either side is built internally. |
| Interface requirement | A statement of WHAT must be true of an interface (e.g. "the order service must accept a confirmed-payment event within 2 s"). Distinct from the interface *design* / ICD, which says HOW (e.g. "POST /events with this JSON over TLS 1.3"). |
| Interface Control Document (ICD) | The as-built design contract for an interface, recording the agreed endpoints, payloads, and wire details. Lives in the design layer; referenced from here, not authored here. |
| Source system / target system | For each interface, the source is the side that originates the exchange; the target is the side that receives it. Naming both prevents the "each team assumed the other owned it" gap. |
| Protocol | The rules governing an exchange: transport, message ordering, who speaks first, how a message is acknowledged, how errors are signalled. A data format alone is not a protocol. |
| Synchronous / asynchronous | Synchronous = the caller waits for a reply (request/response). Asynchronous = the sender fires a message or event and continues; any reply arrives later. This choice drives timeout, retry, and ordering requirements. |
| Idempotency | The property that receiving the same message twice has the same effect as receiving it once. It is what makes safe retries possible; without it a retry after a timeout can double-charge or duplicate an order. |
| Schema / data contract | The agreed structure, types, and valid values for the data crossing an interface. Versioning the schema is how the two sides evolve without breaking each other. |
| Backpressure / rate limiting | Mechanisms that protect an interface from overload: the receiver signals "slow down" (backpressure) or caps requests per window (rate limiting). |
| {{Partner / endpoint name}} | {{Project-specific definition}} |

### 1.4 References

> List, with a one-line relevance note each, every document that this IRS depends on or that the reader needs to interpret it. Categorize for readability. The parent SRS/SyRS is mandatory — an interface requirement only makes sense as the elaboration of some broader system requirement.

Parent requirements:
- {{SRS-{{SYSTEM-ID}}-001}} — the system/software requirements this IRS elaborates; each IFR-N traces up to a requirement here.

Partner / vendor interface docs:
- {{Vendor API reference / partner ICD}} — {{which interface(s) it governs}}.

Protocol and message-bus specs:
- {{Message-bus / queue spec}} — {{relevance, e.g. delivery-guarantee semantics for IF-3}}.
- {{Wire-protocol RFC, e.g. HTTP/1.1, gRPC, MQTT}} — {{relevance}}.

Security / compliance references:
- {{Org security policy / data-classification standard}} — {{relevance to Section 7}}.

External standards:
- ISO/IEC/IEEE 29148:2018 — requirements-engineering life-cycle processes; interface requirements category (companion standard, paywalled — see Status).
- {{Any wire-protocol RFC or domain standard}} — {{relevance}}.

---

## 2. Interface Identification

> This is the index every later section refers back to, so it comes first among the domain sections. Each row catalogues one interface and gets an **IF-N** ID. Beginner-facing guidance: naming BOTH the source system (the side that originates the exchange) and the target system (the side that receives it) is the single cheapest defence against the classic gap where each team assumes the other owns an interface — if the table forces both names, the gap surfaces while it is still cheap to fix. **Direction** (inbound / outbound / bidirectional, always from {{System Name}}'s point of view) and **Interaction style** (synchronous request-response / asynchronous message / event / batch-file / streaming) are chosen here because they drive almost every later requirement: a synchronous inbound API needs different performance and failure handling than an outbound nightly batch file. **Criticality** (essential / degradable / optional) feeds the failure-and-recovery decisions in Section 8 — an essential interface must fail soft, an optional one may simply be skipped. Each IF-N catalogued here is elaborated by one or more IFR-N functional requirements in Section 3.

**Context (narrative):** {{Describe {{System Name}} at the centre with each catalogued interface as an arrow to a named external party. For example: "{{System Name}} sits between the {{Auth provider}} (inbound token validation), the {{Billing partner}} (inbound webhooks, outbound usage reports), the {{Telemetry sink}} (outbound streaming), and the {{operator}} (bidirectional CLI). No other system touches {{System Name}}'s boundary."}}

| Interface ID | Name | Source system | Target system | Direction | Interaction style | Criticality | Owner |
|---|---|---|---|---|---|---|---|
| IF-1 | {{Auth token validation}} | {{Auth provider}} | {{System Name}} | Inbound | Synchronous request-response | Essential | {{Owning team / role}} |
| IF-2 | {{Billing webhook}} | {{Billing partner}} | {{System Name}} | Inbound | Asynchronous event | Essential | {{Owning team / role}} |
| IF-3 | {{Telemetry stream}} | {{System Name}} | {{Telemetry sink}} | Outbound | Streaming | Degradable | {{Owning team / role}} |
| IF-4 | {{Operator CLI}} | {{Operator}} | {{System Name}} | Bidirectional | Synchronous request-response | Optional | {{Owning team / role}} |
| ... | ... | ... | ... | ... | ... | ... | ... |

---

## 3. Functional Interface Requirements

> This is the heart of the document: the numbered, atomic, testable **IFR-N** requirements describing the services, messages, events, commands, and data exchanges that cross each interface, and the expected response for each. Group requirements by interface — 3.1 elaborates IF-1, 3.2 elaborates IF-2, and so on — so every catalogued interface from Section 2 is covered. For each IFR-N state: the trigger or request, the required behaviour, the expected response (the success result AND the defined error responses), and any ordering, sequencing, or idempotency rules. Beginner-facing guidance: a good interface requirement is **atomic** (one exchange per IFR-N — so it can be traced and tested on its own), **testable** (you can write a pass/fail check directly from the wording), and **free of internal implementation detail** (say "the system must reject an order referencing an unknown product with a 'not found' response" — not how the product lookup is coded). Be explicit about which party initiates each exchange, and about what the system MUST send or accept versus what is OPTIONAL. The non-functional aspects — how fast (Section 6), how secure (Section 7), what happens on failure (Section 8) — are forwarded to those sections rather than buried here, but each IFR-N cross-references the relevant PERF-N / SEC-N / FR-N so the link is explicit. (An umbrella note on IDs: IFR-N is the umbrella requirement type; a single IFR-N may be realized through several PROTO-N, DAT-N, or SEC-N clauses in later sections, all tracing back to it.)

### 3.1 IF-1 — {{Auth token validation}}

> Elaborate the IF-1 catalogue row into atomic exchanges.

- **IFR-1** — {{System Name}} must accept a token-validation request initiated by {{the caller}}, carrying {{the bearer token}}, and return a synchronous response indicating valid / invalid / expired. *Initiated by:* {{caller}}. *Success response:* {{200 with the resolved principal and scopes}}. *Error responses:* {{401 for an invalid or expired token; 400 for a malformed request}}. *Idempotency:* validation is read-only and naturally idempotent. *Cross-refs:* performance PERF-1, security SEC-1.
- **IFR-2** — {{Next atomic exchange for IF-1}}. *Initiated by:* {{...}}. *Success response:* {{...}}. *Error responses:* {{...}}. *Cross-refs:* {{...}}.

### 3.2 IF-2 — {{Billing webhook}}

- **IFR-3** — {{System Name}} must accept a `{{payment.confirmed}}` event delivered by {{the Billing partner}} and acknowledge receipt. *Initiated by:* {{Billing partner}}. *Required behaviour:* {{record the confirmed payment and mark the order paid}}. *Success response:* {{2xx acknowledgement so the partner stops retrying}}. *Error responses:* {{4xx for a malformed or unverifiable event; the system must not 2xx an event it could not process}}. *Ordering / idempotency:* events may arrive out of order and more than once (the delivery guarantee is recorded in PROTO-N and OQ-DEF-N); processing MUST be idempotent on the event ID. *Cross-refs:* data DAT-N, protocol PROTO-N, failure FR-N.
- **IFR-4** — {{Next atomic exchange for IF-2}}. *Cross-refs:* {{...}}.

### 3.3 IF-3 — {{Telemetry stream}} *(and one sub-section per remaining IF-N)*

- **IFR-5** — {{Outbound exchange description}}. *Initiated by:* {{System Name}}. *Required behaviour:* {{...}}. *Cross-refs:* {{...}}.
- ...

---

## 4. Data Requirements

> This section is the data-contract specification for what crosses the interfaces. A **data contract** (also called a schema) is the agreed structure, types, and valid values for the data crossing an interface — and the reason to write it down is that a shared, versioned contract is what lets the two sides of an interface evolve independently without breaking each other. Each data element gets a **DAT-N** ID. Beginner-facing guidance: the **Valid Values** column is where range, enum, and null rules are pinned — it is the cheapest place in the whole lifecycle to catch a defect, because a value rejected at the boundary never becomes a corrupt record downstream. The **Sensitivity / Classification** column (public / internal / PII / secret) is what makes the Security section (Section 7) *enforceable* rather than vague — Section 7 protects exactly what is tagged sensitive here. And note **units explicitly**: mismatched units (seconds vs. milliseconds, dollars vs. cents, metres vs. feet) are a recurring and expensive interface bug precisely because both sides "look" correct in isolation.

**Data contract overview.** {{For each interface, describe the schema(s) that cross it, how the schema is versioned (e.g. a `schema_version` field, or a versioned media type / endpoint), and the compatibility rule when it changes. State the rule plainly — e.g. "additive-only: new optional fields may be added without a version bump; removing or retyping a field requires a major version and a {{N}}-day deprecation window during which both versions are accepted."}}

| DAT-N | Data element | Type | Format | Valid values | Required/Optional (cardinality) | Unit / Precision | Sensitivity / Classification | Source | Destination |
|---|---|---|---|---|---|---|---|---|---|
| DAT-1 | {{order_id}} | {{string}} | {{UUID v4}} | {{any valid UUID}} | Required (1) | n/a | Internal | {{Billing partner}} | {{System Name}} |
| DAT-2 | {{amount}} | {{integer}} | {{minor units}} | {{>= 0}} | Required (1) | {{cents (NOT dollars)}} | Internal | {{Billing partner}} | {{System Name}} |
| DAT-3 | {{customer_email}} | {{string}} | {{RFC 5322}} | {{valid email}} | Optional (0..1) | n/a | PII | {{Billing partner}} | {{System Name}} |
| DAT-4 | {{api_key}} | {{string}} | {{opaque}} | {{issued keys only}} | Required (1) | n/a | Secret | {{Caller}} | {{System Name}} |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

---

## 5. Protocol and Communication Requirements

> A **protocol** is the full set of rules governing an exchange — and the key beginner point is that a data format alone is not a protocol. The format says what a message looks like; the protocol additionally fixes the **transport** (e.g. HTTPS/TLS, gRPC, a message queue, an SFTP file drop), the **message-exchange pattern** (request/response, publish/subscribe, streaming, batch), who speaks first, how a message is acknowledged, how errors are returned, and what "delivered" means. Each requirement here gets a **PROTO-N** ID. Beginner-facing guidance on delivery guarantees: **at-least-once** delivery (the sender keeps retrying until it gets an ack, so a message may arrive twice) is common and cheap — but it forces **idempotency** (Section 4 and Section 8), because the receiver will sometimes see duplicates. **Exactly-once** delivery is usually expensive or impossible to guarantee truly end-to-end, so most systems choose at-least-once + idempotent handling instead. Encryption-in-transit is *named* here (it is a property of the transport); the broader confidentiality, integrity, and authorization requirements live in Section 7 — cross-reference rather than duplicate.

| PROTO-N | Interface | Transport | Exchange pattern | Delivery / ordering guarantee | Connection lifecycle | Encoding / serialization | Error signalling |
|---|---|---|---|---|---|---|---|
| PROTO-1 | IF-1 | {{HTTPS / TLS 1.2+}} | {{Request/response}} | {{At-most-once (read-only)}} | {{Keep-alive; client retries on connection error}} | {{JSON, UTF-8}} | {{HTTP status + error body}} |
| PROTO-2 | IF-2 | {{HTTPS / TLS 1.2+}} | {{Publish/subscribe (webhook)}} | {{At-least-once, unordered — duplicates possible (see OQ-DEF-1)}} | {{Partner reconnects and retries on non-2xx}} | {{JSON, UTF-8}} | {{2xx = accepted; 4xx = rejected}} |
| PROTO-3 | IF-3 | {{gRPC / message queue}} | {{Streaming}} | {{At-least-once, ordered per partition}} | {{Heartbeat every {{N}} s; auto-reconnect with resume token}} | {{Protobuf}} | {{Stream error frame + reason code}} |
| ... | ... | ... | ... | ... | ... | ... | ... |

**Per-interface protocol notes:** {{Anything the table cannot hold — e.g. the exact handshake sequence, the ack semantics ("an event is 'delivered' only once {{System Name}} returns 2xx"), or who initiates the connection. Cross-reference the encryption-in-transit requirement to SEC-N in Section 7.}}

---

## 6. Performance Requirements

> Every requirement here is a **PERF-N** with a number and a measurement condition — because the whole point of a performance requirement is that it can be verified, and "low latency" cannot be verified while "p95 round-trip under 200 ms at 50 req/s" can. Beginner-facing guidance on percentiles: **p95** means 95% of calls are at least this fast (only the slowest 5% may exceed it). Percentiles matter because an *average* hides the slow tail that users actually feel — a 50 ms average can still mean one call in twenty takes two seconds, and that one is the call someone complains about. For each interface, specify latency (state the percentile), throughput (requests or messages per second, sustained and peak), capacity (max concurrent connections, max payload or batch size), availability target (e.g. 99.9% measured over a stated window), and timeout values for each direction. Note that the **timeout values chosen here are inputs to the failure/recovery requirements in Section 8** — a retry policy is only well-defined once the timeout it triggers on is fixed. Cross-reference each PERF-N to the IFR-N it constrains so every number is tied to a concrete exchange.

| PERF-N | Interface (IFR-N) | Latency target | Throughput (sustained / peak) | Capacity | Availability (window) | Timeout (per direction) |
|---|---|---|---|---|---|---|
| PERF-1 | IF-1 (IFR-1) | {{p95 < 200 ms round-trip}} | {{50 / 200 req/s}} | {{1 000 concurrent connections; 8 KB max request}} | {{99.9% over 30 days}} | {{Client → {{System Name}}: 2 s}} |
| PERF-2 | IF-2 (IFR-3) | {{p95 < 1 s to acknowledge}} | {{20 / 100 events/s}} | {{256 KB max event}} | {{99.5% over 30 days}} | {{Inbound processing: 5 s before 5xx}} |
| PERF-3 | IF-3 (IFR-5) | {{p99 < 5 s end-to-end}} | {{500 / 2 000 msg/s}} | {{1 MB max batch}} | {{99% over 30 days}} | {{Outbound publish: 10 s}} |
| ... | ... | ... | ... | ... | ... | ... |

**Measurement conditions:** {{State how each number is measured — at which point (client-observed vs. server-observed), under what load, over what window — so "met / not met" is unambiguous.}}

---

## 7. Security and Privacy Requirements

> The two questions this section answers are different and both are mandatory: **authentication** answers "who are you" (how a party's identity is proven), and **authorization** answers "what are you allowed to do" (what an authenticated party may do). Each requirement gets a **SEC-N** ID. For each interface, state: the authentication mechanism (API key, mTLS, OAuth token, etc.), the authorization model (roles/scopes), credential rotation and expiry expectations, what must be logged for audit AND what must NOT be logged (secrets and full PII must never land in logs), and any data-handling constraints (retention, residency, minimization) tied to the **Sensitivity** column from Section 4. Beginner-facing guidance: privacy is never traded away for convenience here — if a data element was marked PII or secret in Section 4, this section must say how it is protected end-to-end and who may see it. Confidentiality and integrity in transit build on the encryption-in-transit requirement named in Section 5 (PROTO-N); cross-reference it rather than restating it.

| SEC-N | Interface | Authentication | Authorization (roles/scopes) | Credential rotation / expiry | Confidentiality & integrity | Audit: must log / must NOT log |
|---|---|---|---|---|---|---|
| SEC-1 | IF-1 | {{OAuth bearer token}} | {{Scope `auth:validate`}} | {{Tokens expire in 1 h; refresh out-of-band}} | {{TLS 1.2+ (PROTO-1)}} | {{Log: principal, decision, timestamp. Never log: the token}} |
| SEC-2 | IF-2 | {{HMAC signature on payload + shared secret}} | {{Webhook source identity only}} | {{Secret rotated every 90 days, dual-secret overlap window}} | {{TLS 1.2+; signature verifies integrity}} | {{Log: event ID, source, verify result. Never log: full PII (DAT-3), the secret}} |
| SEC-3 | IF-3 | {{mTLS client cert}} | {{Publish-only to {{topic}}}} | {{Cert rotated every 30 days}} | {{TLS 1.2+}} | {{Log: connection ID, byte counts. Never log: payload bodies}} |
| ... | ... | ... | ... | ... | ... | ... |

**Data-handling constraints (privacy):** {{For each element tagged PII/secret in Section 4 (DAT-3, DAT-4, ...), state retention period, residency/region constraint, and minimization rule (collect only what the interface needs). State who may see each sensitive element end-to-end.}}

---

## 8. Failure and Recovery Requirements

> This section says how each interface behaves when things go wrong, with one **FR-N** per requirement. Beginner-facing guidance, because this is where most real interface incidents live: the typical incident is not "it broke" but "it was retried and double-applied" or "it timed out and the two sides now disagree on what happened." So the two load-bearing parts are (1) the **safe-retry story** — retries are only safe when the exchange is **idempotent** (Section 4) and the timeout that triggers a retry is fixed (Section 6) — and (2) the **reconciliation story** — how the two sides detect and repair missed or duplicated messages, especially under at-least-once delivery. Also specify **degraded operation**: a well-designed interface **fails soft** (keeps serving a reduced function — a cached / last-known-good response, a queue-and-forward, a default) rather than **failing hard** (returns nothing) wherever possible. Which behaviour is required for each interface follows from its **Criticality** in Section 2: an essential interface must fail soft; an optional one may fail hard or be skipped. State the required behaviour for each failure class: partner unreachable, partner slow (timeout), malformed/invalid message, authentication failure, and partial success. **Backpressure / rate limiting** (a receiver signalling "slow down", or capping requests per window) belongs here too — it is how an interface protects itself when a partner sends faster than it can absorb.

| FR-N | Interface (Criticality) | Retry policy | Idempotency mechanism | Timeout & fallback (degraded mode) | Backpressure / circuit-breaking | Reconciliation |
|---|---|---|---|---|---|---|
| FR-1 | IF-1 (Essential) | {{3 retries, exponential backoff, on 5xx/network only}} | {{Read-only; naturally idempotent}} | {{On timeout: serve last-known-good validation for ≤ 60 s; then deny}} | {{Honour 429; back off}} | {{n/a (stateless read)}} |
| FR-2 | IF-2 (Essential) | {{Partner retries non-2xx; {{System Name}} must accept duplicates}} | {{Dedupe on event ID (DAT-1); apply once}} | {{On internal failure: return 5xx so partner re-sends; queue-and-forward}} | {{Return 429 when ingest queue full}} | {{Nightly reconcile against partner's event log; replay gaps}} |
| FR-3 | IF-3 (Degradable) | {{Buffer locally up to {{N}} MB / {{M}} min, then drop oldest}} | {{Sequence numbers; consumer dedupes}} | {{On sink unreachable: buffer then drop, never block the producer}} | {{Slow producer when buffer > 80%}} | {{Consumer detects sequence gaps and requests resend}} |
| ... | ... | ... | ... | ... | ... | ... |

**Per-failure-class behaviour:** {{For each interface, state explicitly the required behaviour on: partner unreachable; partner slow (timeout fires); malformed/invalid message; authentication failure; partial success (some of a batch applied). Cross-reference the timeout (PERF-N) and idempotency (DAT-N) each one relies on.}}

---

## 9. Open Questions

> An open interface question that carries an explicit **default** is what lets two teams proceed in parallel without silently assuming different answers — the default is the shared assumption made visible. Split open items into deferred-with-defaults (open, but usable now because a working default is recorded) and resolved (decided, kept for the record). Beginner-facing guidance: the resolved log matters as much as the deferred list — keeping *why* the chosen answer won means a future reader (or the other side of the interface) does not reopen a settled decision by accident.

### 9.1 Deferred with defaults

- **OQ-DEF-1** {{Delivery guarantee for the telemetry stream}} — *default: at-least-once with idempotent ingest; revisit if duplicate volume proves costly.*
- **OQ-DEF-2** {{Schema-change deprecation window length}} — *default: {{30 days, additive-only between major versions}}.*
- ...

### 9.2 Resolved (recorded for traceability)

- **OQ-1** {{Should IF-2 acknowledge before or after persisting the event?}}: {{Resolved — acknowledge only after the event is durably recorded, so a 2xx genuinely means "we have it" and the partner can safely stop retrying.}}
- ...

---

## 10. Traceability

> Traceability is the explicit thread that lets a change be followed in both directions — upward ("which stakeholder or system need does this interface serve?") and downward ("if we change this interface, which design, code, tests, and runbooks are affected?"). The matrix below collects, per interface requirement, the parent requirement it satisfies and the design, code, test, and operational artefacts that realize and verify it. Beginner-facing guidance: the **IFR-N / IF-N / DAT-N / PROTO-N / SEC-N / FR-N** prefixes used throughout this document exist precisely so other documents can point at them — this matrix is where those pointers are collected. For a small project, a single table here is enough. A larger project may instead keep a separate Requirements Traceability Matrix (RTM) and reference it from here rather than duplicating it.

| IFR-N | Parent requirement (SRS/SyRS or stakeholder need) | Architecture / Design element | Code / Component | Test case | Operational procedure |
|---|---|---|---|---|---|
| IFR-1 | {{SRS-{{SYSTEM-ID}}-001 §3.x}} | {{ICD / design doc ref}} | {{auth_client module}} | {{TC-AUTH-01}} | {{Runbook: token-validation outage}} |
| IFR-3 | {{SRS-{{SYSTEM-ID}}-001 §3.y}} | {{Webhook intake design}} | {{billing_webhook handler}} | {{TC-BILL-04}} | {{Runbook: webhook reconcile}} |
| IFR-5 | {{SRS-{{SYSTEM-ID}}-001 §3.z}} | {{Telemetry stream design}} | {{telemetry_publisher}} | {{TC-TLM-02}} | {{Runbook: sink-unreachable buffering}} |
| ... | ... | ... | ... | ... | ... |

**Supporting items** also trace upward to their umbrella IFR-N: each DAT-N, PROTO-N, SEC-N, and FR-N realizes part of one or more IFR-N (recorded in the per-section cross-references), so a change to a clause can be tracked back to the functional requirement it serves.

---

## 11. Revision History

> Every substantive change to interface requirements gets a version bump and a one-line note here. Interface specs are contracts between teams — so a clear change log is how the other side of each interface learns that something they depend on has moved. (The "Approved by" record lives in the metadata sign-off block above, so it is not repeated per row here.)

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — the Parent SRS/SyRS reference is mandatory)
- §2 Interface Identification (the catalogue every other section refers back to)
- §3 Functional Interface Requirements
- §4 Data Requirements
- §11 Revision History

**Optional sections** (include if relevant):
- §5 Protocol and Communication Requirements (fold into §3 if every interface uses one simple, shared transport)
- §6 Performance Requirements (omit if no quantifiable targets exist yet — but add them before going to production)
- §7 Security and Privacy Requirements (omit only if no interface carries data classified above "public"; recommended for any cross-organization interface)
- §8 Failure and Recovery Requirements (strongly recommended for any interface marked essential or degradable in §2)
- §9 Open Questions (track elsewhere if you prefer)
- §10 Traceability (for a small project, a single table; a larger project may keep a separate RTM and reference it here)

**Identifier conventions**:
- IFR-N: interface requirements — the primary, atomic, traceable item the SRS, architecture, and tests link to. One exchange per ID.
- IF-N: catalogued interfaces in the §2 identification table.
- DAT-N: data-element requirements (§4).
- PROTO-N: protocol / communication requirements (§5).
- PERF-N: performance requirements (§6).
- SEC-N: security / privacy requirements (§7).
- FR-N: failure / recovery requirements (§8).
- OQ-N / OQ-DEF-N: open questions (resolved / deferred-with-defaults).

IFR-N is the umbrella requirement type; a single IFR-N may be realized through several PROTO-N, DAT-N, SEC-N, or FR-N clauses, all tracing back to it. These prefixes enable cross-document traceability — requirements in the SRS/SyRS can be traced down to specific interface requirements here, and up again from tests and runbooks.

**Tailoring**:
- The section set above is guidance, not law. Add or merge subsections as the project needs, but deviate *explicitly* — note in §1.2 when a section is intentionally omitted.
- Keep the IRS on the requirements side: WHAT each interface must do. The as-built design (exact endpoints, payloads, an Interface Control Document) belongs in the design layer and references the IFR-N here.
- **Solo developer / small team collapse:** for a single interface or two, you can collapse §5–§8 into a short per-interface paragraph under each §3 entry (transport, latency, auth, failure-behaviour in one place), keep §2 as a two- or three-row table, and fold §10 traceability into the parent SRS rather than maintaining a separate matrix. Keep §1, §3, §4, and §11 — they are what a future reader (or the other side of the interface) needs to understand the contract. Even at smallest scale, do not drop the Source/Target naming in §2 or the Valid-Values and Sensitivity columns in §4 — those two prevent the most common and most expensive interface defects.
- Revision history is mandatory at every scale. Interface requirements are contracts; a version bump is how the other side learns the contract moved.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29148:2018, not this lightweight version. For those contexts also pair the IRS with a formal Interface Control Document (ICD) per 29148 interface-agreement practice — this template stays on the requirements (WHAT) side and does not capture the as-built interface design.
