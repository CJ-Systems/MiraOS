# Coding Standard Template

> **Template purpose:** Lightweight Coding Standard structure for solo/small-team and internal use. The document it produces is the human-readable, source-of-truth policy for *how code is written* in a project — the rules a reviewer cites, the rules your formatter and linter enforce a portion of, the rules a new contributor reads before their first commit. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When a project has more than one author (now or soon), or when one author wants consistency across a long-lived codebase. Write it early — a coding standard agreed before the code grows is cheap; one imposed on a large inconsistent codebase is expensive. It sits alongside the SRS (WHAT the system does) and the SDD (HOW the design is structured); this document governs HOW the source text itself is written, named, formatted, and guarded.
>
> **Companion standard:** SWEBOK V4.0 Software Construction Knowledge Area (structural basis; no single normative standard); ISO/IEC 5055:2021 — Information technology — Software measurement — Automated Source Code Quality Measures (input/reference for the security, error-handling, resource-management, and prohibited-practices rule sets).
>
> **Status of this template:** Lightweight, public, reusable extract for solo/small-team and internal use. Structurally follows the SWEBOK V4.0 Software Construction Knowledge Area — SWEBOK is a body-of-knowledge structure, not a single normative standard, so this document names no certifying standard and claims no conformance; it organizes coding rules against SWEBOK's Construction topics. ISO/IEC 5055:2021 is used as an INPUT for the security, error-handling, resource-management, and prohibited-practices rule sets (its automated source-code quality measures inform what to rule on) — ISO/IEC 5055:2021 is a paywalled ISO/IEC standard; this template paraphrases its measure categories and copies no normative text. Verify the rule sets against the full ISO/IEC 5055:2021 standard before relying on them in any regulated, safety-critical, or contractual context, and obtain the standard from ISO/IEC if formal conformance is required. The RULE-N rules themselves are the project's own policy and carry the project's chosen license; this skeleton structure is freely reusable.

---

# Coding Standard — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | STD-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | SWEBOK V4.0 Software Construction KA (structure) + ISO/IEC 5055:2021 (input, lightweight) |
| Owner | {{Project name or owner}} |
| Applies to | {{Languages / repositories / components this standard governs — e.g., all Python under `dna/`; excludes generated code and vendored dependencies}} |
| Enforcement | {{How rules are checked: formatter + linter in CI, code review, or advisory only. Note which rule classes are machine-enforced vs. review-only}} |
| Rule-strength keywords | RFC 2119 (MUST / SHOULD / MAY) as used throughout this document |
| Supersedes | {{Prior coding-standard document or ad-hoc conventions this replaces, if any}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> This section sets up everything the rest of the document relies on: why the standard exists, what code it governs, the vocabulary it uses, and the documents it points at. A *coding standard* is the human-readable policy for how code is written; it is distinct from a *style guide* (the formatting subset of that policy) and from a *linter/formatter config* (the machine-enforced subset). The standard is the source of truth; the tooling enforces a portion of it automatically. If you read only one section before your first commit, read this one — it tells you what you are bound by.

### 1.1 Purpose

> One paragraph on why this document exists and what it binds. Name that it is the source-of-truth coding policy for the project, that tooling enforces only a *subset* of it, and that downstream artifacts (the linter/formatter configs, the CI rules, the review checklist in §11) *implement* it rather than replace it. State the rule-strength convention here so a reader knows, from the start, what "MUST" versus "SHOULD" means in this document.

This document is the source-of-truth coding policy for **{{Project Name}}**. It states, as numbered rules, how source code in this project is named, formatted, documented, and guarded against common defects. Automated tooling (formatter, linter, static analysis — see §10) enforces a *subset* of these rules; code review enforces the rest. The linter and formatter configuration files, the CI rules, and the review checklist in §11 are *realizations* of this standard — when they disagree with this document, this document is correct and the tooling is updated to match, or a waiver (§10) records the gap.

Rules in this document use the **RFC 2119** strength keywords so their force is unambiguous:

- **MUST** / **MUST NOT** — required. Deviation requires a recorded waiver (§10).
- **SHOULD** / **SHOULD NOT** — strongly recommended. Deviate only with a stated reason in the code or review.
- **MAY** — permitted; the author's choice.

A rule's text is **normative** (it states a requirement you are bound by). The guidance blockquote that opens each section is **informative** (it explains and gives examples; it binds nothing). When the two ever appear to conflict, the numbered rule governs.

### 1.2 Scope

> State exactly what code this standard governs — which languages, which repositories or directories — and what it excludes. Mirror the *Applies to* metadata row so the two never drift. Then draw the three-way distinction plainly for a beginner: this standard (human policy) is broader than a style guide (its formatting subset) which is broader than a linter config (the machine-checkable subset). Knowing the scope prevents the two most common arguments: "does this rule apply to *that* file?" and "isn't this the formatter's job?"

**In scope:** {{Which languages and which repositories/directories this standard governs — e.g., all first-party Python and shell under `dna/`. Match this to the *Applies to* metadata row.}}

**Out of scope:**

- {{Generated code — written by tools, not humans; not reviewed against this standard.}}
- {{Vendored / third-party dependencies — governed by their own upstream standards.}}
- {{Throwaway spikes and experiments not intended to merge — exempt until promoted to first-party code.}}

This standard (the human policy) is broader than the project's **style guide** (the formatting subset, §3) which is broader than the project's **linter/formatter config** (the machine-checkable subset, §10). The standard is the source of truth; the narrower artifacts implement parts of it.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define every term that would cause misreading. For a true beginner at formal software-engineering practice, this is where the jargon gate comes down — spend the words. At minimum define the terms below; add project-specific terms (your domain nouns, your toolchain) as needed.

| Term | Definition |
|---|---|
| Coding rule (RULE-N) | One atomic, checkable expectation about how code is written (e.g., "public functions have a documented contract"). *Atomic* means one rule states one thing, so a reviewer can mark it pass/fail without ambiguity. Numbering rules lets code review and tooling cite them. |
| Normative | Text that states a requirement you must follow. The RULE statements are normative. |
| Informative | Text that explains or gives examples but binds nothing. The guidance blockquotes are informative. |
| MUST / SHOULD / MAY | RFC 2119 rule-strength keywords. MUST = required (no exception without a recorded waiver); SHOULD = strongly recommended (deviate only with a stated reason); MAY = permitted (your choice). |
| Style guide | The formatting subset of a coding standard — indentation, line length, ordering. Here, §3. |
| Formatter | A tool that rewrites code layout automatically (indentation, spacing, line breaks) without changing behavior. |
| Linter | A tool that reads source without running it and flags rule violations (unused variables, risky patterns, some prohibited constructs). |
| Static analysis | Deeper than a linter — analyzes data flow and control flow without running the code (e.g., to find a value that reaches a dangerous sink unvalidated). ISO/IEC 5055:2021 defines automated quality measures such tools can compute. |
| Waiver (deviation record) | A documented, approved exception to a MUST rule. Names the rule (RULE-N), the reason, the approver, and the review/expiry date. See §10. |
| {{Project term}} | {{Definition — add your domain nouns and toolchain names here}} |

### 1.4 References

> List the documents this standard depends on or is realized by. Categorize for readability the way the SRS template does. The companion standards belong here; so do the project's own SRS/SDD (so a rule about, say, testability can trace to the project's verification intent) and — importantly — the actual config files that enforce this standard, because a reader needs to know where the machine-checked subset lives.

Foundational project documents:

- {{`docs/srs.md`}} — Software Requirements Specification; this standard's testability rules (§8) trace to its verification approach.
- {{`docs/specs/{{module}}.md`}} — Software Design Description(s); §4 keeps in-code documentation from duplicating design-level documentation.

Enforcement artifacts (where the machine-checked subset is realized):

- {{path to formatter config — e.g., `pyproject.toml [tool.<formatter>]`}} — realizes §3 (formatting).
- {{path to linter config}} — realizes the lint-checkable rules across §2–§9.
- {{path to CI rule / pipeline step}} — runs the above on every change.

Standards (structure and input):

- SWEBOK V4.0 — Software Construction Knowledge Area — structural basis for §2–§9.
- ISO/IEC 5055:2021 — Automated Source Code Quality Measures — input for the rule sets in §5, §6, §7, and §9. *(Paywalled; paraphrased here, not reproduced.)*
- RFC 2119 — Key words for use in RFCs to Indicate Requirement Levels — source of the MUST/SHOULD/MAY convention.

Organizational / regulatory references:

- {{Any internal policy or external regulation the code must comply with}}

---

## 2. Naming Conventions

> Names are the cheapest documentation in a codebase: a good name removes the need for a comment. This section states naming rules as `RULE-NAME-N` — one atomic rule each, with an RFC 2119 keyword and a tiny good/bad example. A machine can check the *shape* of a name (is it `snake_case`? is the constant `UPPER_CASE`?) but it *cannot* judge whether a name is *meaningful* — that semantic quality is review-only, and the rules below mark which is which.

| ID | Rule | Strength | Enforced by |
|---|---|---|---|
| RULE-NAME-1 | {{Functions and variables use `snake_case`}} | MUST | {{Linter}} |
| RULE-NAME-2 | {{Classes and types use `PascalCase`}} | MUST | {{Linter}} |
| RULE-NAME-3 | {{Module-level constants use `UPPER_SNAKE_CASE`}} | MUST | {{Linter}} |
| RULE-NAME-4 | {{Files use `snake_case.{{ext}}`; one primary unit per file where the language allows}} | SHOULD | {{Review}} |
| RULE-NAME-5 | {{Names describe intent in the project's domain vocabulary; avoid generic `data` / `manager` / `helper` / `tmp` / `obj`}} | SHOULD | {{Review}} |
| RULE-NAME-6 | {{Abbreviations are spelled out unless the abbreviation is more recognizable than the full term (e.g., `url`, `id` are fine); acronyms follow the casing rule of their category (`HttpClient` not `HTTPClient` if PascalCase rules treat acronyms as words)}} | SHOULD | {{Review}} |
| RULE-NAME-7 | {{Names that carry a unit include the unit: `timeout_seconds`, `size_bytes`, not `timeout`, `size`}} | SHOULD | {{Review}} |
| RULE-NAME-8 | {{Branch names follow `{{type}}/{{short-description}}`; test names follow the convention in RULE-TEST-N}} | SHOULD | {{Review}} |

**Example (RULE-NAME-5, RULE-NAME-7):**

```
# Bad — generic noun, hidden unit
def process(data, timeout): ...

# Good — domain noun, explicit unit
def index_document(document, timeout_seconds): ...
```

**Notes:** Casing rules (RULE-NAME-1..3) are machine-checkable and belong to the linter. Meaning rules (RULE-NAME-5..7) need a human — a linter cannot tell that `manager` is a worse name than `index_writer`. {{Add per-language casing conventions and the project's domain nouns here, drawn from the SRS glossary so code and spec use the same words.}}

---

## 3. Formatting and Layout

> Formatting is the rule class most fully delegated to tools — so this section is deliberately short. The actual enforcement surface is the formatter config named in §1.4; this section is a *policy statement* that points at it, not a hand-maintained rulebook the formatter already owns. The one thing worth saying plainly: for formatting, *consistency* is the value, not the specific choice. Two spaces or four, the argument is not worth having — pick one, encode it in the formatter, and move on. (That argument has a name: *bikeshedding* — spending disproportionate effort on a trivial, easy-to-have-an-opinion-on decision.)

| ID | Rule | Strength | Enforced by |
|---|---|---|---|
| RULE-FMT-1 | {{Indentation is N spaces; tabs MUST NOT be used (or the reverse — state one)}} | MUST | {{Formatter}} |
| RULE-FMT-2 | {{Maximum line length is N columns}} | MUST | {{Formatter}} |
| RULE-FMT-3 | {{Brace/bracket placement and blank-line rules follow the formatter's default profile}} | MUST | {{Formatter}} |
| RULE-FMT-4 | {{Imports/declarations are ordered as: standard library, third-party, first-party — each group sorted}} | MUST | {{Formatter / linter}} |
| RULE-FMT-5 | {{Within-file order: module docstring, imports, constants, public API, internal helpers}} | SHOULD | {{Review}} |

**The actual rulebook lives in the formatter config:** {{name the formatter and config path — e.g., the project's auto-formatter configured in `pyproject.toml`}}. Code MUST be formatted by that tool before review (RULE-FMT-1..3 are simply "whatever the configured formatter produces"). Reserve prose here only for choices the formatter cannot make for you — e.g., RULE-FMT-5's within-file ordering, which is a convention a human applies. Do not restate the formatter's rules by hand; they will drift.

---

## 4. Comments and Documentation

> Code says *what* happens; comments say *why*, and only where the why is not obvious. A comment that restates the code ages badly and adds noise; a comment that records a non-obvious intent, an assumption, or a known limitation is worth its weight. This section also requires a *documented contract* on public APIs: a short statement of what each public function or class promises — its parameters, what it returns, what errors it can raise, and any side effects — so a caller can use it without reading its body. This standard governs *in-code* documentation; design-level documentation lives in the SDD (§1.4) — keep the two from duplicating.

| ID | Rule | Strength | Enforced by |
|---|---|---|---|
| RULE-DOC-1 | {{Every public function/class/module has a documented contract: parameters, return value, raised errors, and notable side effects}} | MUST | {{Linter (presence) + review (quality)}} |
| RULE-DOC-2 | {{Comments explain *why* / intent / assumptions / limitations; they MUST NOT merely restate what the code already says}} | SHOULD | {{Review}} |
| RULE-DOC-3 | {{Non-obvious assumptions and known limitations are recorded at the point they apply (e.g., "assumes input is already validated by the caller")}} | SHOULD | {{Review}} |
| RULE-DOC-4 | {{Docstrings/headers follow the project's chosen format}} | MUST | {{Linter}} |
| RULE-DOC-5 | Commented-out code MUST NOT be committed; delete it (version control remembers it) | MUST | {{Review / linter}} |

**Example (RULE-DOC-2):**

```
# Bad — restates the code
i = i + 1  # add one to i

# Good — records the why
i = i + 1  # skip the header row; the parser counts it as data otherwise
```

**Boundary with the SDD:** rationale for a *design* decision (why this module exists, why this interface shape) belongs in the SDD, not in a code comment. A code comment captures the local why a maintainer needs *at this line*. If a comment is explaining architecture, it probably belongs in the design doc with a pointer from the code.

---

## 5. Error Handling

> Most bugs that reach a user are mishandled errors, not wrong logic — which makes this a high-value section. ISO/IEC 5055:2021 is a direct input: its automated measures include error- and exception-handling defects, so the rules below target the patterns those measures flag (paraphrased, not copied). The single most important rule: a caught error MUST be *handled, logged, or re-raised* — never silently discarded. A swallowed error is a bug that has been hidden rather than fixed.

| ID | Rule | Strength | Enforced by |
|---|---|---|---|
| RULE-ERR-1 | {{Use the language's idiomatic mechanism (raise/throw vs. return an error value) consistently; do not mix the two for the same kind of failure}} | MUST | {{Review}} |
| RULE-ERR-2 | A caught error MUST be handled, logged, or re-raised — never swallowed silently (no empty catch blocks) | MUST | {{Linter (empty catch) + review}} |
| RULE-ERR-3 | {{Retries use bounded backoff with a maximum attempt count; unbounded or tight-loop retries MUST NOT be used}} | MUST | {{Review}} |
| RULE-ERR-4 | Error logs include enough context to diagnose (operation, identifiers, cause) but MUST NOT log secrets or full sensitive payloads (cross-ref RULE-SEC-N) | MUST | {{Review (+ secret-scanner)}} |
| RULE-ERR-5 | {{Internal error detail is separated from user-facing messages; the user sees an actionable framing, not a raw stack trace or internal identifier}} | SHOULD | {{Review}} |

**User-facing messages (RULE-ERR-5):** {{If the product has a defined voice or an agent-mediated surface, the user reads the agent's framing, not raw substrate output. State that the user-facing message is composed by the product's surface layer; raw exceptions and stack traces are inputs to that layer, never shown to the user directly.}}

**Example (RULE-ERR-2):**

```
# Bad — error swallowed; failure becomes invisible
try: write_index(doc)
except Exception: pass

# Good — logged with context, then re-raised for the caller to decide
try:
    write_index(doc)
except IndexWriteError as e:
    log.error("index write failed for %s: %s", doc.id, e)
    raise
```

---

## 6. Security Rules

> Three primitives first, in plain English. **Input validation:** never trust data from outside the program (user, file, network) until you have checked it. **Output encoding:** escape data correctly for wherever it is going (HTML, SQL, a shell command) so it cannot be mis-read as a command — this is the root of injection bugs. **Secret handling:** passwords, API keys, and tokens never live in source code or logs. ISO/IEC 5055:2021's Security measures are a direct input here; the rules below are organized around its weakness categories (injection, improper input handling, and related) — described in our own words, with no normative text copied. For each rule, note whether a tool can catch it: some injection patterns are lint-detectable; authorization logic is review-only, because correctness depends on intent a tool cannot read.

| ID | Rule | Strength | Enforced by |
|---|---|---|---|
| RULE-SEC-1 | All data crossing a trust boundary (user input, file contents, network responses) MUST be validated before use | MUST | {{Review (+ some lint)}} |
| RULE-SEC-2 | Data interpolated into another language (SQL, HTML, shell, etc.) MUST be encoded/parameterized for that destination; never build such strings by concatenation | MUST | {{Linter (some patterns) + review}} |
| RULE-SEC-3 | {{Authentication: identity is established by the project's vetted mechanism only}} | MUST | {{Review}} |
| RULE-SEC-4 | {{Authorization: every privileged action checks the actor's permission at the point of action; "the UI hides it" is not authorization}} | MUST | {{Review only}} |
| RULE-SEC-5 | Secrets (keys, passwords, tokens) MUST NOT appear in source, comments, logs, or error messages; they come from {{the project's secret store / environment}} | MUST | {{Secret-scanner + review}} |
| RULE-SEC-6 | Cryptography uses vetted, current libraries; project code MUST NOT implement its own cryptographic primitives | MUST | {{Review}} |
| RULE-SEC-7 | Dependencies are pinned to exact versions, reviewed before adoption, and scanned for known vulnerabilities | MUST | {{Dependency scanner in CI + review}} |

**Where human judgment is mandatory:** RULE-SEC-4 (authorization) is review-only — a tool can confirm a check *exists* but not that it checks the *right* thing. RULE-SEC-2 (injection) is partly lint-detectable (string-built SQL, `eval` of dynamic input) but a clean scan does not prove safety; a reviewer still confirms trust boundaries. {{Tailor the validation/encoding rules to the project's actual inputs and sinks.}}

---

## 7. Resource Management

> The mental model in one line: **anything the program opens, it must close — including on the error path.** "Open implies a matching close" covers memory the language hands you to manage, open files and handles, network connections, locks, and database transactions. ISO/IEC 5055:2021's Reliability and Efficiency measures (resource leaks, unreleased handles) are an input for the rules below. The highest-value rule, and the most common leak in real code: **cleanup that only runs on the success path is a bug** — the failure path leaks. Prefer the language's scoped-cleanup construct (a *context manager* in Python, *RAII* in C++/Rust, *try-with-resources* in Java) over a manual close you have to remember to also call when something throws.

| ID | Rule | Strength | Enforced by |
|---|---|---|---|
| RULE-RES-1 | Files, sockets, and handles are acquired through the language's scoped-cleanup construct (context manager / RAII / try-with-resources); manual close MUST be paired with guaranteed cleanup on every exit path | MUST | {{Linter (some) + review}} |
| RULE-RES-2 | {{Memory ownership is explicit where the language is manual; every allocation has one clear owner responsible for release}} | MUST | {{Review}} |
| RULE-RES-3 | Network connections set timeouts, are pooled where appropriate, and are closed when done | MUST | {{Review}} |
| RULE-RES-4 | {{Shared mutable state accessed concurrently is guarded; locks are always acquired in a consistent global order to avoid deadlock}} | MUST | {{Review}} |
| RULE-RES-5 | Database transactions have explicit commit/rollback boundaries; a transaction MUST NOT be left open across an await/IO boundary or returned to the caller unclosed | MUST | {{Review}} |
| RULE-RES-6 | Cleanup runs on the failure path, not only on success | MUST | {{Review}} |

**Example (RULE-RES-1, RULE-RES-6):**

```
# Bad — leaks the handle if write() raises
f = open(path)
write(f)
f.close()

# Good — scoped cleanup closes on success AND on exception
with open(path) as f:
    write(f)
```

---

## 8. Testability Rules

> This section is about writing code *so that it can be tested* — which is different from writing the tests. Two enablers, in plain English. **Dependency isolation:** the code *receives* its collaborators (passed in) rather than reaching out and grabbing global ones, so a test can substitute fakes for the real database, clock, or network. **Determinism:** given the same input, the code produces the same output — no hidden dependence on the wall clock, randomness, or the network inside the unit under test. Code with these two properties can be tested fast and reliably; code without them forces slow, flaky tests or no tests at all. These rules trace to the verification approach in the SRS (§1.4) — they are how the project's V&V intent reaches the source.

| ID | Rule | Strength | Enforced by |
|---|---|---|---|
| RULE-TEST-1 | {{Units are small with clear inputs and outputs; avoid hidden global state that a test cannot set up or observe}} | SHOULD | {{Review}} |
| RULE-TEST-2 | Collaborators (I/O, time, randomness, network, config) are injected behind seams so a test can substitute fakes; code MUST NOT hard-reach global singletons for these | SHOULD | {{Review}} |
| RULE-TEST-3 | The unit under test is deterministic: same input → same output; no direct reads of the clock, RNG, or network inside pure logic | SHOULD | {{Review}} |
| RULE-TEST-4 | {{Test names follow a convention that states what is being tested and the expected outcome (e.g., `test_<unit>_<condition>_<expected>`), so a failing test name alone tells you what broke}} | MUST | {{Linter / review}} |

**Example (RULE-TEST-2, RULE-TEST-3):**

```
# Bad — reaches global clock; result changes with wall time; untestable in isolation
def is_expired(token): return token.created_at + TTL < datetime.now()

# Good — clock is injected; deterministic for a given `now`
def is_expired(token, now): return token.created_at + TTL < now
```

**Trace:** these rules realize the verification approach in {{`docs/srs.md` §5}}. If that document defines a V&V strategy (unit / integration / acceptance), the seams required here are what make it achievable.

---

## 9. Prohibited Practices

> A short, explicit list of "never do this here" is faster to apply at review time than a long list of "do this" — and it is where a project records its hard-won lessons. Each prohibition is a clear **MUST NOT** with a one-line reason, because the reason is what teaches. ISO/IEC 5055:2021's weakness lists are an input for the security and reliability prohibitions (paraphrased). Many prohibitions are simply the negative form of a rule stated positively elsewhere — those are cross-referenced, not duplicated; keep this section for prohibitions that have no positive home. Prohibited practices are prime candidates for linter rules: a "never" is exactly what a linter can mechanically block, so note which are machine-blocked versus review-caught.

| ID | Rule | Reason | Enforced by |
|---|---|---|---|
| RULE-PROHIB-1 | {{MUST NOT `eval`/execute untrusted input}} | {{arbitrary code execution}} | {{Linter}} |
| RULE-PROHIB-2 | {{MUST NOT deserialize untrusted data with an unsafe deserializer}} | {{remote code execution}} | {{Linter}} |
| RULE-PROHIB-3 | {{MUST NOT use deprecated/obsolete API `{{X}}`; use `{{Y}}` instead}} | {{removed in {{version}}; unsupported}} | {{Linter}} |
| RULE-PROHIB-4 | MUST NOT commit secrets to source | restates RULE-SEC-5 (cross-ref, not duplicated) | {{Secret-scanner}} |
| RULE-PROHIB-5 | MUST NOT swallow errors silently | restates RULE-ERR-2 (cross-ref) | {{Linter}} |
| RULE-PROHIB-6 | {{Organization-prohibited practice — e.g., MUST NOT log full request payloads}} | {{privacy / compliance}} | {{Review}} |

**Notes:** RULE-PROHIB-1..3 are typically machine-blocked (a linter rejects the merge). RULE-PROHIB-6 and other policy prohibitions are usually review-caught. {{Add the project's own "we learned this the hard way" prohibitions here — each with its one-line reason.}}

---

## 10. Compliance, Enforcement, and Waivers

> A standard is only real if it states *how it is enforced* and *what happens when a rule is broken*. Rules split into two kinds. **Machine-enforced** rules are checked by the formatter, linter, and static analysis in CI — they fail the build automatically, and they cost a reviewer nothing. **Review-enforced** rules need human judgment — naming quality, comment intent, authorization correctness — and a reviewer's attention should be spent here, not on what a tool already checks. The second half of this section defines the *waiver*: the documented, approved exception to a MUST rule. The principle to internalize: **an undocumented deviation is a defect; a documented waiver is a decision.** A standard with no waiver path is one people quietly ignore; a standard with a visible, accountable one stays credible.

### 10.1 Enforcement split

| Enforcement | Rule classes | Mechanism |
|---|---|---|
| Machine | {{RULE-FMT-* (formatter); RULE-NAME-1..3, RULE-PROHIB-1..3,5, some RULE-SEC-2/5 (linter, secret-scanner, static analysis); RULE-SEC-7 (dependency scanner)}} | {{Runs in CI on every change; failing checks block the merge}} |
| Review | {{RULE-NAME-5..7, RULE-DOC-2..3, RULE-ERR-*, RULE-SEC-4, RULE-RES-*, RULE-TEST-* and other judgment rules}} | {{The §11 checklist, walked at review time}} |

The machine-enforced measures map to automated source-code quality measures of the kind ISO/IEC 5055:2021 defines (reliability, security, efficiency, maintainability). {{Name the actual tools and the CI step that runs them.}}

### 10.2 Waivers

A MUST rule may be deviated from only with a recorded **waiver**. A waiver is a decision, logged where the team can see it ({{e.g., a `WAIVERS.md`, a tracker label, or an inline annotation the linter recognizes}}), containing:

| Field | Value |
|---|---|
| Waiver ID | {{WV-001}} |
| Rule | {{RULE-N being waived}} |
| Scope | {{File / function / module the waiver applies to}} |
| Reason | {{Why the rule cannot or should not be met here}} |
| Approved by | {{Approver — per the *Approved by* metadata row}} |
| Granted / Review-by | {{YYYY-MM-DD}} / {{YYYY-MM-DD or "permanent — revisit if X changes"}} |

An expired waiver is treated as no waiver. {{State whether waivers are required for SHOULD rules — typically no; a stated reason in review suffices for SHOULD.}}

---

## 11. Review Checklist

> The checklist is the standard turned into a pass/fail list a reviewer (or the rule author, reviewing their own change) walks at review time. It is how the *review-enforced* rules from §10 actually get applied — the machine-enforced ones are already green in CI before review begins. Each row references a `RULE-N` (or rule group) so the checklist traces directly back to the normative rules, and a column marks whether the row is machine-checked (skim it — CI already confirmed it) or human-checked (spend your attention here). Copy this table into your review tool or PR template, and **prune it to the rules that actually matter for the code under review** rather than ticking every box on every change.

| Check | Rule(s) | Checked by | Pass? |
|---|---|---|---|
| Names are domain-meaningful, not generic | RULE-NAME-5..7 | Human | {{☐}} |
| Casing/format conform | RULE-NAME-1..3, RULE-FMT-* | Machine (CI) | {{☐}} |
| Public APIs have a documented contract | RULE-DOC-1 | Human | {{☐}} |
| No commented-out code, no comments that just restate code | RULE-DOC-2, RULE-DOC-5 | Human | {{☐}} |
| No swallowed errors; retries bounded; no secrets in logs | RULE-ERR-2..4 | Mixed | {{☐}} |
| Trust-boundary input validated; output encoded; authz checked at action | RULE-SEC-1, RULE-SEC-2, RULE-SEC-4 | Human | {{☐}} |
| No secrets in source; deps pinned & scanned | RULE-SEC-5, RULE-SEC-7 | Machine (CI) | {{☐}} |
| Resources scoped-cleanup; cleanup on failure path; transactions bounded | RULE-RES-1, RULE-RES-5, RULE-RES-6 | Human | {{☐}} |
| Collaborators injected; unit deterministic; tests named to convention | RULE-TEST-2..4 | Human | {{☐}} |
| No prohibited constructs | RULE-PROHIB-* | Mixed | {{☐}} |
| Any MUST deviation has a recorded waiver | §10.2 | Human | {{☐}} |

{{Prune and extend per code area — a pure-data-model change needs few of these; a network-facing change needs all of §6 and §7.}}

---

## 12. Open Questions

> A living standard always has a few unsettled rules. Recording them keeps the team from re-litigating the same point in every review. Use two buckets. **Deferred with defaults** (`OQ-DEF-N`): the question *and* the default rule in force until it is decided — so work is never blocked waiting on the decision. **Resolved** (`OQ-N`): recorded with its resolution, so a future reader can see why a rule is the way it is. Migrate entries from the first bucket to the second as decisions land.

### 12.1 Deferred with defaults

- **OQ-DEF-1** {{Unsettled formatting choice pending tool support}} — *default: {{the current formatter profile stands until the tool ships the option}}.*
- **OQ-DEF-2** {{Which constructs the upcoming language-version migration prohibits}} — *default: {{existing RULE-PROHIB-N set applies; revisit on upgrade}}.*

### 12.2 Resolved (recorded for traceability)

- **OQ-1** {{Should we adopt a dependency-vulnerability scanner?}}: {{Resolved — yes; RULE-SEC-7 now requires it in CI as of v{{X}}.}}

---

## 13. Revision History

> Every substantive rule change gets a version bump and a row here — this is mandatory, not optional. Code review and CI cite `RULE-N` identifiers, so a reader needs to know *which version of a rule* was in force when a given commit was reviewed. When the meaning of a rule changes, say so in the Changes column and reference the rule ID.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):

- §1 Introduction (all subsections — purpose, scope, definitions, references)
- At least §2 Naming, §3 Formatting, and §4 Comments & Documentation (the construction baseline every codebase needs)
- §10 Compliance, Enforcement, and Waivers (a standard with no enforcement statement is advisory at best)
- §13 Revision History

**Optional sections** (include if relevant):

- §5 Error Handling, §6 Security Rules, §7 Resource Management, §8 Testability Rules — include each that applies to your code (a pure library with no I/O may not need §6/§7; almost everything benefits from §5 and §8).
- §9 Prohibited Practices (omit if you have no project-specific "never do this" lessons yet; add it the moment you do).
- §11 Review Checklist (highly recommended — it is how the human-enforced rules actually get applied; but you may keep it in your PR template instead of the standard).
- §12 Open Questions (track elsewhere if you prefer).

**Tailoring:**

- The SWEBOK Construction topics are a structure to organize against, not a checklist to certify against. Add, merge, or drop domain sections (§2–§9) to fit your languages and risk profile.
- Keep rules *atomic and numbered* — one rule per `RULE-N` so review and CI can cite them. A flat `RULE-1, RULE-2, …` numbering is acceptable for a very small standard, but the prefixed form (`RULE-NAME-1`, `RULE-ERR-2`, …) is recommended so each rule traces to the section that owns it.
- Push everything a tool can check into the tool. This document's value is the *judgment* rules and the *why*; let the formatter own formatting and the linter own the mechanical rules, and keep §3 a thin pointer rather than a hand-maintained rulebook.
- **Solo developer / small team:** collapse aggressively. A solo developer can drop the sign-off rows (Prepared/Reviewed/Approved collapse to one name), run §11 as a self-review before committing, and treat §10's waiver mechanism as a one-line note-to-self in the code. Keep §1 (so a future contributor — or future you — knows the rules), the few domain sections that match your code, and §13. Even solo, the standard pays for itself the first time you return to old code and the rules tell you what "good" looked like.

**Identifier conventions:**

- `RULE-NAME-N` naming · `RULE-FMT-N` formatting · `RULE-DOC-N` comments/documentation · `RULE-ERR-N` error handling · `RULE-SEC-N` security · `RULE-RES-N` resource management · `RULE-TEST-N` testability · `RULE-PROHIB-N` prohibited practices.
- `OQ-N` open questions · `OQ-DEF-N` open questions deferred with a stated default.
- These prefixes enable cross-document traceability — a `RULE-N` cited in a code-review comment or a CI rule points back to one place here; testability rules (`RULE-TEST-N`) trace forward to the SRS verification approach and back from the SDD.

**For regulated/safety-critical projects:** use the full ISO/IEC 5055:2021 standard (and any domain coding standard such as MISRA, CERT, or a sector-specific one), not this lightweight version. Verify the §5/§6/§7/§9 rule sets against the full ISO/IEC 5055:2021 measure definitions before relying on them in any regulated, safety-critical, or contractual context.
