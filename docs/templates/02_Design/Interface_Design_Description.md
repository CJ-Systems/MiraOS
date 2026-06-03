# Interface Design Description Template

> **Template purpose:** Lightweight Interface Design Description (IxD) structure following the Interface viewpoint of IEEE 1016-2009. Use this template when documenting the externally-visible interfaces of a system or subsystem — the agreed boundaries across which it exchanges data and control. Replace `{{placeholder}}` content with system-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When two parts of a system, or your system and an outside party, exchange data and control across a boundary that needs to be agreed, written down, and built against. The IxD sits beside the Software Design Description (SDD): the SDD says HOW each component works inside; the IxD says exactly what crosses the line between them. Reach for it whenever a consumer will write code against your interface and you want one source of truth they can rely on.
>
> **Companion standard:** IEEE 1016-2009 (Interface viewpoint) — Standard for Information Technology — Systems Design — Software Design Descriptions.
>
> **Status of this template:** Lightweight Interface Design Description following the Interface viewpoint of IEEE 1016-2009 (the same standard the companion Software Design Description template cites; an IxD is essentially the Interface viewpoint elaborated as its own document at the inter-component / system boundary level). Faithful to the 1016 interface viewpoint outline but reduced for solo/small-team use, and aligned in shape to the SWEBOK Software Design knowledge area. IEEE 1016-2009 is a paywalled standard — this is a lightweight skeleton derived from public sources that paraphrases and reproduces NO normative text from the standard; verify against the full standard for enterprise, regulated, or safety-critical contexts before relying on it as normative.

---

# Interface Design Description — {{System Name}}

| Field | Value |
|---|---|
| Document ID | IxD-{{SYSTEM-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 1016-2009 (Interface viewpoint, lightweight) |
| Owner | {{Project name or owner}} |
| Companion document(s) | {{SDD / SRS / Architecture Description this interface design realizes — e.g. SDD-{{MODULE-ID}}-001}} |
| Interface stability | {{Draft / Stable / Frozen — signals consumers how safe it is to build against this contract}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: state that this document specifies the externally-visible interfaces of the system — the agreed boundaries across which it exchanges data and control with other components or outside parties — and that it does NOT specify the internals on either side of those boundaries (the SDD and the code do that). Name the companion document this interface design realizes, so a reader can trace up to the design or requirement that called for the interface.
>
> Beginner note: an **interface**, in design terms, is the agreed boundary across which two parts of a system (or the system and an outside party) exchange data and control. This document describes the *boundary itself* — what crosses it and under what rules — not what happens on either side of it. IEEE 1016 calls this the "Interface viewpoint."

This document specifies the externally-visible interfaces of **{{System Name}}** — the agreed boundaries across which it exchanges data and control with other components or outside parties. It defines, for each boundary, what crosses it (the data), and the rules of the exchange (the protocol, error behavior, security, and versioning). It does **not** specify the internal design or implementation on either side of those boundaries; that belongs to {{the companion SDD-{{MODULE-ID}}-001 and the implementation code}}. This interface design realizes {{the design / requirement named in the companion document — e.g. the interface obligations described in SDD-{{MODULE-ID}}-001 §4 and the requirements in SRS-{{PROJECT-ID}}-001 §3}}.

### 1.2 Scope

> List the interfaces this document covers (each will get an `IF-N` ID in §2) and, just as importantly, list what is explicitly OUT of scope: internal calls that never cross a contract boundary, and interfaces deferred to a later version. Stating the out-of-scope boundary prevents a reader assuming this document covers more than it does.
>
> Beginner note: an interface here is a **contract at a boundary**, not a screen or a GUI. "The login *screen*" is a user interface; "the call another service makes to check a credential" is the kind of interface this document is about. If nothing crosses a documented contract boundary, it is not in scope here.

In scope:
- {{IF-1 — interface name and the two parties it connects}}
- {{IF-2 — interface name and the two parties it connects}}
- {{...}}

Out of scope:
- {{Internal call X}} — does not cross a contract boundary; lives entirely inside {{component}} and is covered by its SDD.
- {{Deferred interface Y}} — planned for {{a later version}}; not yet a stable contract.
- {{User-facing GUI / screens}} — covered by {{a separate UI design document}}, not this IxD.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define every term that, left undefined, would let a reader misread the rest of the document. The table is pre-seeded with the core interface concepts so the later sections read cleanly — keep the ones you use, add project-specific terms (message names, protocol names), and delete any that do not apply.

| Term | Definition |
|---|---|
| Interface | The agreed boundary across which two parts of a system, or the system and an outside party, exchange data and control. This document describes the boundary, not the internals on either side. |
| Provider | For a given interface, the party that exposes / offers it. |
| Consumer | For a given interface, the party that calls / uses it. (Provider vs. consumer — "who offers it" — is a *different* axis from "who speaks first"; see Direction below.) |
| Direction | Which party initiates the exchange ("who speaks first"). Not the same as provider/consumer: a provider can offer an interface that the *consumer* always initiates, or one where the *provider* pushes messages to the consumer. |
| Synchronous | The caller waits for the response before continuing (request/reply). |
| Asynchronous | The caller sends and continues; the response, if any, arrives later via a separate message or event. |
| Schema | A written, checkable description of a payload's shape: which fields exist, their types, which are required, units, ranges. |
| Validation | Checking an actual payload against its schema before trusting it. |
| Idempotency | A property where making the same call more than once has the same effect as making it once — so the call is safe to retry. |
| Protocol | The agreed rules of an exchange over time: message order, who speaks first, what an acknowledgement looks like, timing/timeout expectations, and how retries work. (The data format says *what* a message contains; the protocol says *when* and *in what order* messages flow.) |
| Authentication | Establishing *who* is calling (identity). |
| Authorization | Establishing whether that caller is *allowed* to do this (permission). Distinct from authentication. |
| Backward-compatible change | A change that lets existing consumers keep working without modification. |
| {{Project term}} | {{Definition}} |

### 1.4 References

> List the documents and external standards this interface design depends on, categorized for readability. Companion design/requirement documents (so a reader can trace upward), related interface specs (so neighboring contracts are findable), and the external protocol/data-format standards the interface actually uses on the wire (so a consumer knows what their tooling must speak).

Companion design / requirement documents:
- {{SDD-{{MODULE-ID}}-001}} — {{the module design this interface realizes}}
- {{SRS-{{PROJECT-ID}}-001}} — {{the requirements the interface satisfies}}
- {{Architecture Description}} — {{where this boundary sits in the system landscape}}

Related interface specifications:
- {{IxD-{{OTHER-SYSTEM-ID}}-001}} — {{a neighboring interface this one connects to or depends on}}

External protocol / data-format / standard references:
- {{Wire protocol — e.g. HTTP/1.1, gRPC, MQTT, AMQP — with version}} — {{how the interface is carried}}
- {{Data-format standard — e.g. JSON (RFC 8259), Protocol Buffers, CSV (RFC 4180)}} — {{the payload encoding}}
- {{Security standard — e.g. TLS 1.3, OAuth 2.0}} — {{transport / auth protection}}

---

## 2. Interface Summary

> This section is the index of boundaries. Each row names one interface, gives it an `IF-N` ID, and points at the parties and shape; the sections that follow detail each contract. Every later section refers back to these IDs, so assign them here and do not renumber them later.
>
> Beginner note — two axes people conflate:
> - **Provider vs. Consumer** = *who offers the interface* vs. *who uses it*. The provider publishes the contract; the consumer builds against it.
> - **Direction** = *who initiates / speaks first*. A consumer can initiate (it calls the provider), or a provider can initiate (it pushes an event to the consumer). These are independent: a provider may offer an interface whose messages it *itself* sends. Name both per interface so the boundary is unambiguous.
>
> Synchronicity (sync/async) and Stability (Draft/Stable/Frozen) belong here too because they shape how a consumer must build: synchronous means they wait for a reply; a Frozen interface is a promise they can safely depend on. For the lightweight tier, a one-line context sketch ("IF-1 connects the {{client app}} to the {{order service}}") is an acceptable stand-in for a formal diagram.

The table below is the master list of interfaces. Each `IF-N` is a contract detailed in §3–§8 and verified in §9.

| Interface ID | Name | Provider | Consumer | Type | Direction (who initiates) | Synchronicity | Stability |
|---|---|---|---|---|---|---|---|
| IF-1 | {{Order Submission API}} | {{Order Service}} | {{Client App}} | {{HTTP/JSON request-reply}} | {{Consumer}} | {{Synchronous}} | {{Stable}} |
| IF-2 | {{Order-Status Events}} | {{Order Service}} | {{Notification Service}} | {{Message queue topic}} | {{Provider}} | {{Asynchronous}} | {{Draft}} |
| IF-N | {{Name}} | {{Provider}} | {{Consumer}} | {{Type}} | {{Initiator}} | {{Sync / Async}} | {{Draft / Stable / Frozen}} |

Context sketch (lightweight, in lieu of a diagram):
- {{IF-1: Client App → (calls) → Order Service}}
- {{IF-2: Order Service → (publishes events to) → Notification Service}}

---

## 3. Operations and Messages

> For each interface from §2, list the individual operations or messages it carries, grouped under that interface's `IF-N` so each operation is addressable as `IF-N.M` (e.g. `IF-1.1`). For every operation, state what triggers it, the input and output payloads (point to §4 for the field-level schema rather than repeating field lists here), and the error response shape (detailed in §6). Record an Idempotent? flag and Preconditions/Postconditions, because those drive the sequencing rules in §5 and the retry rules in §6.
>
> Beginner note:
> - **Idempotent?** marks whether a call is safe to repeat: an idempotent call has the same effect whether you make it once or five times, so it is safe to retry after a timeout; a non-idempotent one (e.g. "charge the card") is not.
> - **Preconditions** are what must be true *before* the call (e.g. "a session must exist"); **postconditions** are what is guaranteed *after* it succeeds (e.g. "the order is persisted and has an ID"). Stated together, they let a consumer reason about the call without reading the provider's code — they *are* the contract.

### 3.1 IF-1 — {{Order Submission API}}

| Operation / Message (ID) | Direction | Trigger | Input (→ §4) | Output (→ §4) | Idempotent? | Error Response (→ §6) |
|---|---|---|---|---|---|---|
| IF-1.1 `{{submitOrder}}` | {{Consumer → Provider}} | {{User confirms checkout}} | {{`OrderRequest` (§4.1)}} | {{`OrderConfirmation` (§4.2)}} | {{Yes — keyed by client request ID}} | {{`Error` (§6.1)}} |
| IF-1.2 `{{getOrder}}` | {{Consumer → Provider}} | {{Client polls for status}} | {{`OrderId` (§4.3)}} | {{`OrderRecord` (§4.4)}} | {{Yes — read-only}} | {{`Error` (§6.1)}} |

**IF-1.1 preconditions / postconditions:** {{Pre: caller is authenticated (§8) and the referenced items exist. Post: an order is persisted with a unique ID; the same client request ID submitted twice yields the same order, not two.}}

### 3.2 IF-2 — {{Order-Status Events}}

| Operation / Message (ID) | Direction | Trigger | Input (→ §4) | Output (→ §4) | Idempotent? | Error Response (→ §6) |
|---|---|---|---|---|---|---|
| IF-2.1 `{{OrderStatusChanged}}` | {{Provider → Consumer}} | {{Order state transition}} | {{n/a (event push)}} | {{`StatusEvent` (§4.5)}} | {{Yes — consumer dedupes on event ID}} | {{Dead-letter (§6.2)}} |

**IF-2.1 preconditions / postconditions:** {{Pre: consumer is subscribed to the topic. Post: at-least-once delivery — the consumer may see an event more than once and must dedupe on its event ID.}}

---

## 4. Data Formats

> This section is the contract for *what* crosses the boundary. For each payload referenced in §3, give a field table. Specify the encoding (JSON / Protobuf / CSV / binary), character set, byte order if binary, how null/empty is represented, and how *unknown extra fields* are treated — reject them or ignore them (this choice interacts directly with §7 versioning). Keep this focused on the shape of the data; the *order in time* is §5.
>
> Beginner note: a **schema** is a written, checkable description of a payload's shape — which fields exist, their types, which are required, their units and ranges. **Validation** is checking a real incoming message against the schema *before* trusting it. Always state units and precision explicitly: a number with no unit (is `weight` grams or kilograms?) is a bug waiting to happen.

### 4.0 Encoding and general rules

| Property | Value |
|---|---|
| Encoding | {{JSON / Protocol Buffers v3 / CSV / binary}} |
| Character set | {{UTF-8}} |
| Byte order (if binary) | {{Little-endian / Big-endian / n/a}} |
| Null / empty handling | {{Absent field = not provided; explicit null = cleared. Empty string is distinct from null.}} |
| Unknown extra fields | {{Ignore (tolerant reader — enables forward compatibility) / Reject (strict — safer but breaks on additive change). See §7.}} |
| Validation point | {{Each provider validates inbound payloads against the schema before acting; invalid payloads are rejected with the §6 error.}} |

### 4.1 `{{OrderRequest}}` (input to IF-1.1)

| Field | Type | Required? | Units / Range | Notes (validation rule) |
|---|---|---|---|---|
| {{clientRequestId}} | {{string (UUID)}} | {{Yes}} | {{36 chars}} | {{Idempotency key for IF-1.1; reject if malformed.}} |
| {{items}} | {{array of LineItem}} | {{Yes}} | {{1–{{100}} entries}} | {{Reject empty array.}} |
| {{currency}} | {{string}} | {{Yes}} | {{ISO 4217 code}} | {{Must be a supported currency.}} |
| {{requestedAt}} | {{timestamp}} | {{No}} | {{ISO 8601 UTC}} | {{Defaults to server receive time if absent.}} |

### 4.2 `{{OrderConfirmation}}` (output of IF-1.1)

| Field | Type | Required? | Units / Range | Notes |
|---|---|---|---|---|
| {{orderId}} | {{string}} | {{Yes}} | {{—}} | {{Stable identifier for IF-1.2.}} |
| {{totalAmount}} | {{integer}} | {{Yes}} | {{minor units (cents), ≥ 0}} | {{Units are MINOR units to avoid float rounding — state this explicitly.}} |
| {{status}} | {{enum}} | {{Yes}} | {{`accepted` \| `pending`}} | {{Closed set; reject unknown values.}} |

> Repeat a field table for each remaining payload referenced in §3 (`OrderId`, `OrderRecord`, `StatusEvent`, the §6 `Error` shape, …).

---

## 5. Protocols and Sequencing

> This section describes the rules of the exchange *over time*: who initiates, the expected order of messages, what an acknowledgement looks like, whether the exchange is request/reply or fire-and-forget, timing and timeout expectations, the retry policy (and which operations are safe to retry — link to the Idempotent? flags in §3), and any state assumptions (must a session or handshake exist first?). A short numbered call-sequence or a simple sequence sketch for the common path is encouraged.
>
> Beginner note — draw the line from §4 sharply: the **data format** is *what* a message contains; the **protocol** is *when* and *in what order* messages flow, and what a well-behaved party does while waiting. **Synchronous** means the caller blocks until the reply arrives; **asynchronous** means the caller sends and continues, and any response arrives later as a separate message. The whole section hinges on which of those an interface is.

### 5.1 IF-1 — {{request/reply, synchronous}}

- **Initiation:** {{Consumer initiates each call; provider responds.}}
- **State assumptions:** {{Caller must hold a valid auth token (§8); no other session state required.}}
- **Acknowledgement:** {{The HTTP response IS the acknowledgement; a 2xx confirms receipt and processing.}}
- **Timing / timeout:** {{Consumer applies a {{5 s}} timeout. On timeout the result is *unknown*, not *failed*.}}
- **Retry policy:** {{Safe to retry IF-1.1 and IF-1.2 because both are idempotent (§3.1). Retry up to {{3}} times with exponential backoff (see OQ in §10). Reuse the same `clientRequestId` so a retried `submitOrder` does not create a duplicate order.}}

Common-path sequence (IF-1.1):
1. {{Consumer builds `OrderRequest`, validating against §4.1 locally first.}}
2. {{Consumer sends the request with its auth token.}}
3. {{Provider authenticates (§8), validates the payload (§4), processes, persists.}}
4. {{Provider returns `OrderConfirmation` (§4.2) with a 2xx, OR an `Error` (§6).}}
5. {{On timeout (no reply within {{5 s}}), consumer retries with the same `clientRequestId`.}}

### 5.2 IF-2 — {{publish/subscribe, asynchronous}}

- **Initiation:** {{Provider initiates by publishing; consumer reacts.}}
- **Ordering:** {{Per-key ordering only; cross-key order is not guaranteed. Consumer must not assume global order.}}
- **Delivery guarantee:** {{At-least-once — consumer dedupes on event ID (§3.2).}}
- **No reply:** {{Fire-and-forget; there is no acknowledgement back to the provider beyond broker ack.}}

---

## 6. Error Handling

> Error handling is part of the contract, not an afterthought — a consumer needs to know not just the happy-path output but exactly how failure is signalled and what it is expected to do. Enumerate the failure modes per interface, give each the error response shape (the `Error` payload defined in §3/§4), say whether the consumer should retry or give up, and describe recovery/reconciliation for partial failures. Keep retry guidance consistent with the idempotency flags (§3) and the timeout/retry policy (§5).
>
> Beginner note: a robust consumer is written against the *failure* contract as much as the success contract. "What does an invalid request look like coming back? Should I retry, or is retrying pointless? If half my batch succeeded, how do I find out which half?" — those answers live here.

### 6.1 IF-1 failure modes

| Failure mode | Signalled as | Retry? | Recovery / reconciliation |
|---|---|---|---|
| {{Invalid input (schema violation, §4)}} | {{`Error` code `INVALID_REQUEST`, HTTP 400}} | {{No — retrying the same bad payload will fail again}} | {{Consumer fixes the payload and resubmits.}} |
| {{Unauthorized caller (§8)}} | {{`Error` code `UNAUTHORIZED`, HTTP 401/403}} | {{No}} | {{Consumer re-authenticates (§8) then retries.}} |
| {{Provider unavailable / timeout (§5)}} | {{No response, or `Error` code `UNAVAILABLE`, HTTP 503}} | {{Yes — idempotent (§3.1), same `clientRequestId`}} | {{Backoff and retry per §5.1.}} |
| {{Downstream dependency failure}} | {{`Error` code `DEPENDENCY_FAILED`, HTTP 502}} | {{Yes, with backoff}} | {{If persistent, surface to operator; do not silently drop.}} |

### 6.2 IF-2 failure modes

| Failure mode | Signalled as | Retry? | Recovery / reconciliation |
|---|---|---|---|
| {{Consumer fails to process an event}} | {{Negative-ack to broker}} | {{Yes — broker redelivers}} | {{After {{N}} failures the event goes to a dead-letter queue for manual inspection.}} |
| {{Partial batch failure}} | {{Per-item status in the response}} | {{Retry only the failed items}} | {{Consumer reconciles by re-requesting status of the items it is unsure about (idempotent reads, IF-1.2).}} |

---

## 7. Compatibility and Versioning

> State the current interface version and how it is signalled (URL path, header, or a message field). Define, *for this interface specifically*, what counts as a backward-compatible change versus a breaking change. Describe version negotiation (if any), how old and new consumers coexist during a transition, and the deprecation policy: how a version is announced as deprecated and how long it remains supported. Tie the "unknown extra fields" decision from §4 to compatibility — a tolerant reader (ignore unknown fields) makes additive change non-breaking.
>
> Beginner note: a change is **backward-compatible** if existing consumers keep working *without any modification*. A **Stable** or **Frozen** interface is a promise other people build their code on — changing it carelessly breaks them silently (their code still compiles, it just stops working correctly). **Versioning** is how the interface signals "this is a different contract" so old and new consumers can coexist during a transition; **deprecation** is the announced, time-boxed path to retiring an old version.

| Property | Value |
|---|---|
| Current version | {{v1}} |
| How version is signalled | {{URL path `/v1/...` / `Accept-Version` header / `version` field in the message}} |
| Version negotiation | {{None — consumer pins a version / Server picks highest mutually supported}} |

**Backward-compatible (non-breaking) for this interface:**
- {{Adding a new *optional* field to a request or response}}
- {{Adding a new operation / message type}}
- {{Adding a new enum value the consumer is documented to tolerate (relies on §4 "ignore unknown")}}

**Breaking (requires a new version):**
- {{Removing or renaming a field}}
- {{Making an optional field required, or tightening validation (narrowing a range)}}
- {{Changing a field's type, units, or meaning}}
- {{Removing an operation or an enum value}}

**Coexistence and deprecation:**
- {{`v1` and `v2` are served in parallel during the transition window.}}
- {{A version is announced deprecated {{X months}} before removal, with a migration note; it is supported for at least {{that window}} after announcement.}}

---

## 8. Security

> Per interface, specify five distinct controls: **authentication** (how the caller proves identity), **authorization** (what that identity is permitted to do), **transport protection** (encryption in transit), **integrity protection** (tamper detection), and **audit logging** (what is recorded about each call). Note any sensitive data crossing the boundary and how it is protected or redacted. Cross-reference §6 so the way a failed-auth call is reported back to the consumer agrees between the security and error-handling contracts.
>
> Beginner note: keep **authentication** ("who are you") and **authorization** ("are you allowed to do this") visibly separate — they are different controls and beginners commonly merge them. A caller can be perfectly authenticated and still be *unauthorized* for a specific operation. State the default posture explicitly: **deny by default** means anything not explicitly permitted is refused.

| Control | IF-1 | IF-2 |
|---|---|---|
| Authentication | {{Bearer token (OAuth 2.0) on every request}} | {{Broker credentials per consumer}} |
| Authorization | {{Scope `orders:write` for IF-1.1, `orders:read` for IF-1.2; deny by default}} | {{Topic-level subscribe permission}} |
| Transport protection | {{TLS 1.3 required; plaintext refused}} | {{TLS to the broker}} |
| Integrity protection | {{TLS provides integrity; {{optional message signature for high-value calls}}}} | {{Broker-level / signed payload}} |
| Audit logging | {{Log caller identity, operation, timestamp, result code — NOT payload bodies}} | {{Log event ID, topic, consumer, delivery outcome}} |

**Sensitive data crossing this boundary:** {{e.g. payment tokens — never log the raw value; store/transmit only a redacted reference. PII is encrypted in transit (above) and redacted from audit logs.}}

**Default posture:** {{Deny by default — an unauthenticated or unauthorized call is refused and reported per §6 (`UNAUTHORIZED`), never silently dropped and never partially honored.}}

---

## 9. Verification

> Describe how each interface is shown to meet its contract: interface/contract tests, schema-validation tests against §4, sequencing/protocol tests against §5, a negative test for *each* §6 error mode, security tests for §8, and any stubbing/simulation of the other side of the boundary. A small traceability table mapping each `IF-N` (and the key `IF-N.M` operations) to its verification cases makes coverage gaps visible at a glance. State the acceptance criteria — what "this interface is verified" actually means.
>
> Beginner note: verifying an interface means exercising the *contract* from the consumer's side — does the boundary behave exactly as this document says? — not testing the provider's internal logic. The IxD is the source of truth the tests check against; if a test and this document disagree, one of them is wrong and you stop until you know which.

**Acceptance criteria:** {{An interface is "verified" when every operation in §3 has at least one happy-path contract test, every §4 payload has a schema-validation test (valid and invalid cases), every §6 error mode has a negative test, the §8 auth controls have a deny-by-default test, and all pass against the current version.}}

| Verifies | IF / operation | Verification case(s) | Type |
|---|---|---|---|
| {{Happy path}} | {{IF-1.1 `submitOrder`}} | {{VC-1: valid order → `OrderConfirmation`}} | {{Contract test}} |
| {{Schema, invalid}} | {{IF-1.1 input (§4.1)}} | {{VC-2: missing `clientRequestId` → `INVALID_REQUEST`}} | {{Schema/negative}} |
| {{Idempotency}} | {{IF-1.1}} | {{VC-3: same `clientRequestId` twice → one order}} | {{Sequencing}} |
| {{Error mode}} | {{IF-1 / §6.1 timeout}} | {{VC-4: provider down → consumer retries, no duplicate}} | {{Negative}} |
| {{Auth}} | {{IF-1 / §8}} | {{VC-5: missing token → `UNAUTHORIZED`}} | {{Security}} |
| {{Async delivery}} | {{IF-2.1}} | {{VC-6: duplicate event → consumer dedupes}} | {{Protocol}} |

---

## 10. Open Questions

> Track interface decisions still unresolved so they are not lost in chat. For each, note what is blocking it and who must decide. Split into **deferred-with-defaults** (there is a working default; revisit only if it proves inadequate) and **load-bearing** (these block adoption of the interface and must be settled before consumers build against it). Resolve and remove rows as the contract firms up.
>
> Beginner note: this is where honest uncertainty lives. Writing "we defaulted retry count to 3, revisit if it causes load problems" is far better than leaving it implicit — the next person sees the decision *and* knows it is provisional.

### 10.1 Deferred with defaults
- **OQ-DEF-1** {{Retry count and backoff curve}} — *default: {{3 retries, exponential backoff starting at 200 ms}}; revisit if it causes provider load problems.*
- **OQ-DEF-2** {{Unknown-field handling}} — *default: {{ignore (tolerant reader)}}; revisit if a stricter posture is needed for safety.*

### 10.2 Load-bearing (block adoption)
- **OQ-1** {{Should IF-2 guarantee per-key ordering or is best-effort acceptable?}} — blocking: {{consumer's dedupe/ordering logic depends on the answer}}; decision owner: {{interface owner + consumer team}}.
- **OQ-2** {{Version-signalling mechanism — URL path vs. header?}} — blocking: {{must be fixed before any consumer pins a version}}; decision owner: {{architecture owner}}.

---

## 11. Revision History

> Every substantive change to the interface *contract* gets a row and a version bump. Because consumers build against this document, the history is how they know what changed and when — and the Approval column records who signed off on a contract change. Seed with the initial draft row.

| Version | Date | Author | Description of Change | Approval |
|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft | {{Approval authority}} |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Interface Summary (the master list of `IF-N`)
- §3 Operations and Messages
- §4 Data Formats (at minimum a schema for every payload in §3)
- §5 Protocols and Sequencing
- §6 Error Handling
- §11 Revision History

**Optional sections** (include if relevant):
- §7 Compatibility and Versioning (always include once an interface has any consumer; safe to omit only for a throwaway internal contract that nothing else builds against)
- §8 Security (omit only if the interface crosses no trust boundary — rare; when in doubt, include it)
- §9 Verification (defer if the interface is still Draft and unconsumed, but add before declaring it Stable)
- §10 Open Questions (track elsewhere if you prefer, but record load-bearing ones *somewhere* durable)

**Identifier conventions**:
- `IxD-{{SYSTEM-ID}}-NNN` — the document itself.
- `IF-N` — one row per interface in the §2 Interface Summary; the master ID every later section refers back to.
- `IF-N.M` — an operation or message within interface `IF-N`, so sequencing (§5), error-handling (§6), and verification (§9) can cross-reference a specific operation.
- `VC-N` — verification cases in §9.
- `OQ-N` / `OQ-DEF-N` — open questions (load-bearing / deferred-with-defaults).

These prefixes let an SRS requirement (e.g. `SRS-{{PROJECT-ID}}-001 §3`) or an SDD interface entry (e.g. `SDD-{{MODULE-ID}}-001` `IF-N`) trace *down* to a specific interface here, and let verification cases trace *back up* to the contract they exercise.

**Tailoring**:
- The §2 summary plus §3 and §4 are the irreducible core — they say which boundaries exist, what crosses them, and in what shape. Everything else elaborates the rules around that core.
- For a **solo developer or small team**, collapse aggressively: a single interface can be a one-row §2, a short §3 table, one §4 payload schema, a sentence each for §5/§6/§8, and the §11 history. The discipline that earns its keep even at the smallest scale is writing down the *schema* (§4) and the *error contract* (§6) — those are what future-you and any second consumer will get wrong otherwise.
- Keep the IxD about the *boundary*. Anything that is internal to one side belongs in that side's SDD, not here.
- Bump the version and add a §11 row for every contract change, however small — a renamed field is a breaking change even if it feels trivial.

**For regulated/safety-critical projects:** use the full IEEE 1016-2009 standard with its formal Interface viewpoint (and the surrounding Context, Dependency, Interaction, and Algorithmic viewpoints as applicable), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
