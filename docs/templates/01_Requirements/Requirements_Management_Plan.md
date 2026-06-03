# Requirements Management Plan Template

> **Template purpose:** Lightweight Requirements Management Plan (RMP) structure aligned to ISO/IEC/IEEE 29148:2018 (requirements management) with ISO/IEC/IEEE 12207:2017 for the change-control / configuration-management process context. Use this template to define HOW a project will source, analyze, specify, validate, attribute, trace, baseline, change, and measure its requirements over the project's life. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Early in a project, alongside the first draft of the Software Requirements Specification (SRS). The SRS holds the requirements *themselves*; this plan describes the *discipline* applied to them. A solo developer benefits too — the plan is the written answer to "how do I keep my requirements from drifting into chaos six weeks from now."
>
> **Companion standard:** ISO/IEC/IEEE 29148:2018 — Systems and software engineering — Life cycle processes — Requirements engineering (primary, for requirements management); ISO/IEC/IEEE 12207:2017 — Systems and software engineering — Software life cycle processes (companion, for the change-control / configuration-management process context).
>
> **Status of this template:** Lightweight skeleton derived from public sources, aligned to ISO/IEC/IEEE 29148:2018 (requirements management) with ISO/IEC/IEEE 12207:2017 for the change-control/configuration-management process context. It follows the 29148 requirements-management outline and a SWEBOK-aligned section set (Requirements Sources, Elicitation/Analysis/Specification/Validation Approach, Requirement Attributes, Traceability, Change Control, Requirements Metrics), reduced for solo/small-team use. It paraphrases and reproduces NO normative text from these paywalled ISO/IEEE standards and is NOT a substitute for them; verify section content against the full standards for enterprise, regulated, safety-critical, or contractual contexts.

---

# Requirements Management Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | RMP-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29148:2018 (lightweight) |
| Owner | {{Project name or owner}} |
| Companion standard | ISO/IEC/IEEE 29148:2018 + 12207:2017 (lightweight) |
| Governs (artifacts) | {{e.g., SRS-{{PROJECT-ID}}, StRS, module specs}} |
| Current baseline | {{BL-N — date / status, or "none frozen yet"}} |
| Change authority | {{Role/person who approves requirement changes}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph stating what this document is for. The key idea a beginner must grasp here: there are two related-but-different activities. **Requirements *engineering*** is the act of discovering and writing the requirements. **Requirements *management*** is the ongoing discipline of keeping those requirements organized, traced, baselined, and under change control over the whole life of the project. This document is the *management* plan — it describes the *process*, not the requirements. The requirements themselves live in the SRS (and any Stakeholder Requirements Specification, StRS). State that distinction plainly so no one looks here expecting to find the actual requirements.

{{This document defines how requirements for {{Project Name}} are sourced, analyzed, specified, validated, attributed, traced, baselined, changed, and measured across the project's life. It is the requirements *management* plan: it governs the **process** by which requirements are handled. The requirements **themselves** are recorded in the Software Requirements Specification (`SRS-{{PROJECT-ID}}`) and, where applicable, a Stakeholder Requirements Specification. If you are looking for "what the system must do," read the SRS; if you are looking for "how we keep those statements trustworthy over time," you are in the right place.}}

### 1.2 Scope

> State plainly what this plan covers and what it deliberately leaves out. Beginners often expect a "plan" to cover everything; be explicit that this plan is scoped to requirements, not the whole project. Name the artifacts it governs (the SRS, stakeholder requirements, module specs), the life-cycle phases it spans, and the things that are someone else's plan (project scheduling, test *execution*, deployment).

This plan **covers**:
- The requirements artifacts it governs: {{e.g., the SRS (`SRS-{{PROJECT-ID}}`), the Stakeholder Requirements Specification (StRS), module specifications}}.
- The life-cycle phases it spans: {{e.g., from initial elicitation through development, into maintenance, until project retirement}}.
- The process activities: sourcing, elicitation, analysis, specification, validation, attribution, traceability, baselining, change control, and metrics.

This plan **does NOT cover** (out of scope):
- {{Project management — schedule, budget, staffing (see the Project Management Plan)}}.
- {{Test *execution* — running and reporting tests (see the Test Plan). This plan only governs how a *verification method* is assigned to each requirement, not the act of testing.}}
- {{Detailed design and implementation decisions (see the Software Design Description, SDD).}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Define the formal vocabulary the rest of the document leans on, so the plan is readable without prior formal software-engineering training. Pre-seed the load-bearing concepts (baseline, elicitation, traceability, verification vs. validation, change control) here, then the later sections can use the words freely. Aim for terms that, if undefined, would cause a reader to misread the rest of the document.

| Term | Definition |
|---|---|
| Requirements engineering | The act of *discovering and writing* requirements. Distinct from requirements management (below). |
| Requirements management | The ongoing discipline of keeping requirements organized, traced, baselined, and under change control over the project's life. The subject of this document. |
| Baseline (`BL-N`) | A snapshot of an agreed set of requirements, frozen at a point in time and given an identifier. After baselining, a requirement changes only through change control. A baseline is what makes "we agreed on X back in {{month}}" provable rather than a memory. |
| Elicitation | The act of drawing requirements out of stakeholders and sources (interviews, observation, document analysis, prototyping). It is *discovery*, not *collection* — many real requirements are never stated until you go looking. |
| Bidirectional traceability | The ability to follow any requirement *forward* (need → requirement → design → code → test) and *backward* (test → requirement → originating need). Forward proves nothing was dropped; backward proves nothing was built that no one asked for. |
| Verification | "Did we build the thing right?" — does the product meet the *written* requirement. |
| Validation | "Did we build the right thing?" — does the *requirement* actually serve the real need. A requirement can pass verification and still fail validation. |
| Requirement attribute | A piece of metadata attached to a requirement (its ID, source, priority, status, rationale, verification method, trace links). Attributes turn a flat list of sentences into something sortable, filterable, and traceable. |
| Change control | The defined path a proposed requirement change must travel: submitted → impact-analyzed → approved/rejected → implemented → recorded. It exists to prevent silent scope growth ("scope creep"). |
| Requirements metric | A countable health indicator about the requirement set itself (e.g., how many are unverified, how many changed this period). Metrics make requirement quality observable instead of a gut feeling. |
| SRS / StRS | Software Requirements Specification / Stakeholder Requirements Specification — the documents that hold the actual requirements this plan governs. |
| {{Other project-specific term}} | {{Definition}} |

### 1.4 References

> List the documents this plan depends on or governs, plus the external standards behind it. Categorize for readability, the way the SRS does. A beginner should be able to tell, from the categories alone, which documents this plan *governs* (the requirements artifacts) and which it *answers to* (organizational, contractual, regulatory, and standards references).

Governed artifacts (the requirements this plan manages):
- `SRS-{{PROJECT-ID}}` — {{Software Requirements Specification: the software requirements themselves}}
- {{StRS-{{PROJECT-ID}} — Stakeholder Requirements Specification, if used}}
- {{path/to/module/spec.md — module specification(s), if used}}

Organizational, contractual, and regulatory references:
- {{Organizational policy / quality manual — relevance}}
- {{Contract / statement of work clause — relevance}}
- {{Regulation or compliance regime — relevance, or "none applicable"}}

External standards:
- ISO/IEC/IEEE 29148:2018 — Requirements engineering (primary; this plan follows its requirements-management outline).
- ISO/IEC/IEEE 12207:2017 — Software life cycle processes (companion; supplies the change-control / configuration-management process context for §9).

---

## 2. Requirements Sources

> A "source" is any origin a requirement can legitimately come from: a named stakeholder, a regulation, a contract, an existing system, an operational scenario, or market/competitive analysis. Give each source an identifier (`SRC-N`) so a requirement can record *where it came from* — this is the first link in the traceability chain. The **Authority** column is load-bearing: it records *whose say-so settles a conflict* involving that source, which §4 (Analysis) uses to resolve contradictions. Watch for the asymmetry that bites small teams: a source with high authority but low availability (e.g., a busy executive sponsor, an external regulator) is a project risk — flag it here, because requirements that depend on a slow-to-respond authority will stall.

| ID | Source | Description | Contact / availability | Authority |
|---|---|---|---|---|
| SRC-1 | {{Primary stakeholder / product owner}} | {{What requirements this source originates}} | {{Name or role; how reachable}} | {{High — final say on product scope}} |
| SRC-2 | {{Regulation / standard}} | {{Compliance requirements it imposes}} | {{Published text / regulator}} | {{High — non-negotiable; settles conflicts in its domain}} |
| SRC-3 | {{Existing system being replaced}} | {{Behaviors that must be preserved}} | {{System docs / its maintainer}} | {{Medium — informs but does not override product owner}} |
| SRC-4 | {{Operational scenario / field observation}} | {{Tacit needs surfaced by watching real use}} | {{Whoever performs the work}} | {{Medium}} |
| SRC-5 | {{Market / competitive analysis}} | {{Differentiators, table-stakes features}} | {{Analyst / public sources}} | {{Low — advisory}} |

**Availability risks:** {{e.g., "SRC-2 (regulator) responds in weeks, not days — any requirement that hinges on its interpretation is a schedule risk; raise such items early."}}

---

## 3. Elicitation Approach

> Elicitation is *discovery*, not *collection*. The mistake a beginner makes is treating requirements like items on a shelf to be gathered up — but the most important requirements are often the ones no one says out loud because "everybody knows that." Name the techniques you will use, and — the part that actually matters — say *when each is appropriate*, because the technique determines which kinds of requirement you can find. Tie each technique back to the `SRC-N` sources from §2. Finally, say where elicited-but-not-yet-written items wait until §5 turns them into real requirements.

| Technique | What it surfaces | When to use it | Sources (§2) |
|---|---|---|---|
| Interviews | Stated needs, priorities, rationale | One-on-one with a knowledgeable stakeholder | SRC-1 |
| Workshops | Shared agreement, conflict between stakeholders | Several stakeholders must reconcile views | SRC-1, SRC-3 |
| Observation / contextual inquiry | **Tacit** requirements users never articulate | Watching real work in its real setting | SRC-4 |
| Document analysis | Constraints embedded in existing material | Reading regulations, contracts, legacy docs | SRC-2, SRC-3 |
| Prototyping | Requirements that only become visible once something is concrete | The need is vague until people can react to a mock-up | SRC-1, SRC-4 |
| Surveys | Breadth across many users; rough priorities | Many stakeholders, shallow input acceptable | SRC-5 |
| Operational scenarios | End-to-end "a day in the life" needs | Tracing a real task start-to-finish | SRC-4 |

**Why technique choice matters:** {{e.g., "observation surfaces tacit requirements users never think to state; prototypes surface requirements that only appear once something is concrete to react to. Relying on interviews alone systematically misses both."}}

**Parking lot:** {{Where elicited-but-not-yet-specified items are recorded (e.g., a "raw needs" list or backlog) until §5 turns them into written, attributed requirements. Nothing elicited is lost; it simply waits in the parking lot until specified.}}

---

## 4. Analysis Approach

> Analysis is where the raw, messy output of elicitation is turned into a coherent, non-contradictory, prioritized set. This is the gate a requirement must pass through *before* it is eligible to enter a baseline (§9). Cover five things: **prioritization** (which requirements matter most), **conflict resolution** (what happens when two requirements contradict), **feasibility** (can it actually be built within constraints), **dependency analysis** (which requirements presuppose others), and **per-requirement risk**. Name a concrete prioritization scheme and define it plainly the first time — beginners should not have to already know what "MoSCoW" means.

**Prioritization — MoSCoW.** {{We prioritize each requirement as one of:}}
- **Must** — the product fails without it.
- **Should** — important but the product still works (painfully) without it.
- **Could** — desirable; included only if effort allows.
- **Won't** (this release) — explicitly excluded now; recorded so it is not silently dropped.

{{(MoSCoW is one common scheme; substitute your own — e.g., High/Medium/Low — but define it here and use the same scheme as the Priority attribute in §7.)}}

**Conflict resolution.** {{When two requirements contradict, resolution follows the Authority column from §2: the higher-authority source prevails. If two equal-authority sources conflict, escalate to the change authority named in the metadata. Record the resolution as a requirement's rationale attribute (§7) so the decision is not re-litigated.}}

**Feasibility.** {{Each requirement is checked against project constraints (technical, schedule, budget). An infeasible requirement is either renegotiated with its source or marked Won't with a recorded reason — it does not silently survive into a baseline.}}

**Dependency analysis.** {{Identify which requirements presuppose others (e.g., "REQ-12 cannot be verified until REQ-3 exists"). Dependencies are recorded as Trace Links (§7) and inform implementation order.}}

**Per-requirement risk.** {{Each requirement gets a risk note (the Risk attribute, §7): volatility, technical uncertainty, or dependence on a low-availability source (§2). High-risk requirements are flagged for earlier attention.}}

**Gate:** {{A requirement is eligible to enter a baseline (§9) only after it has been prioritized, checked for conflicts, judged feasible, and had its dependencies and risk recorded.}}

---

## 5. Specification Approach

> Specification is writing the requirement down so it is **unambiguous, atomic, and testable**. This is the bridge to §7 (Attributes) and §8 (Traceability): a well-specified requirement is one you can attach metadata to and trace. State the writing format, the identifier scheme, the mandatory attributes, and the quality checklist. One subtlety for beginners: this plan *governs* the requirement IDs but does not *own* them — the SRS assigns the actual `REQ-` / `SR-` identifiers. This plan defines the discipline; the SRS is the register.

**Format.** {{One requirement per statement (atomic). Use "shall" phrasing — "The system shall …" — or the project's chosen convention. No statement should contain "and" joining two separable obligations; split them.}}

**Identifier scheme.** {{This plan governs how requirements are managed but does not invent requirement IDs. The SRS assigns the actual identifiers (`REQ-N` for software requirements, `SR-N` for stakeholder/system requirements). This plan's own internal prefixes (`SRC-`, `ATTR-`, `MET-`, `OQ-`) name *process* items, never requirements.}}

**Mandatory attributes.** {{Every specified requirement carries the attribute set defined in §7 (at minimum: ID, Source, Priority, Status, Rationale, Verification Method, Trace Links). See §7 for which are mandatory for baseline eligibility.}}

**Quality criteria — characteristics of a good requirement.** {{Adapted from the 29148 characteristics, each requirement should be:}}

| Characteristic | Plain-language meaning |
|---|---|
| Necessary | Removing it leaves a gap; it earns its place. |
| Unambiguous | Has exactly one reasonable reading. |
| Complete | States everything needed to act on it — no "TBD" left dangling. |
| Singular (atomic) | Describes exactly one thing. |
| Feasible | Can be built within the project's constraints. |
| Verifiable | You can define a concrete test or check that proves it was met. |
| Traceable | Can be linked back to a source and forward to design/code/test. |

{{A statement failing any of these is sent back for rework before it counts as specified.}}

---

## 6. Validation Approach

> First, re-anchor the verification-vs-validation distinction, because this section is primarily about **validation** — "are these the *right* requirements?" — even though it also describes how a *verification* method ("did we build it right?") gets assigned to each requirement. Name the techniques. Then state the exit criterion crisply: a requirement is *validated* when its source stakeholder has confirmed it AND a verification method has been assigned. That dual condition is a *precondition* for entering a baseline (§9) — an unvalidated requirement cannot be frozen.

**Techniques.** {{We validate requirements using:}}
- **Peer review** — another team member reads the requirement for clarity and correctness.
- **Formal inspection / walkthrough** — a structured group read for higher-stakes requirements.
- **Prototyping / simulation** — let the stakeholder react to something concrete.
- **Acceptance-test derivation** — write the test that would prove the requirement met; if you cannot, the requirement is not verifiable (§5) and needs rework.
- **Explicit stakeholder confirmation / sign-off** — the originating source (§2) confirms "yes, this is what I meant."

**Assigning a verification method.** {{For each requirement, record *how it will be verified* (test / demonstration / inspection / analysis) as the Verification Method attribute (§7). Assigning the method is part of validation — a requirement nobody knows how to check is not yet ready.}}

**Exit criterion.** {{A requirement is *validated* when (a) its source stakeholder (§2) has confirmed it AND (b) a verification method (§7) has been assigned. Both conditions are required before the requirement is eligible for a baseline (§9).}}

---

## 7. Requirement Attributes

> Attributes are the columns that turn a flat list of requirement sentences into a queryable, sortable, traceable set. Without them, "show me every unverified Must-have requirement that changed since the last baseline" is impossible; with them, it is a filter. Define the schema your project actually uses, with **allowed values** for each attribute (not just a name). Tag each schema row `ATTR-N` for reference. State which attributes are mandatory for a requirement to be **baseline-eligible** versus optional — this connects directly to the §9 entry criteria.

| ID | Attribute | Allowed values / meaning | Mandatory for baseline? |
|---|---|---|---|
| ATTR-1 | ID | The SRS-assigned identifier (`REQ-N` / `SR-N`). Unique, never reused. | Yes |
| ATTR-2 | Source | The `SRC-N` origin from §2. Records where the requirement came from. | Yes |
| ATTR-3 | Priority | The §4 scheme — `Must` / `Should` / `Could` / `Won't`. | Yes |
| ATTR-4 | Status | Lifecycle (see below): `Proposed` → `Analyzed` → `Validated` → `Baselined` → `Implemented` → `Verified` → `Retired`. | Yes |
| ATTR-5 | Rationale | Why this requirement exists; records conflict resolutions (§4). | Yes |
| ATTR-6 | Verification Method | How it will be checked — `Test` / `Demonstration` / `Inspection` / `Analysis`. | Yes |
| ATTR-7 | Trace Links | Forward/backward links (§8): to source, design (`PURP-`/`IF-`), code, test. | Yes |
| ATTR-8 | Risk | Volatility / technical-uncertainty note from §4. | Optional |

**Status lifecycle (ATTR-4).** {{A requirement moves through these states; each transition has a gate from an earlier section:}}
- **Proposed** — captured, not yet analyzed.
- **Analyzed** — passed the §4 gate (prioritized, feasible, conflicts resolved).
- **Validated** — passed the §6 exit criterion (stakeholder-confirmed + verification method assigned).
- **Baselined** — frozen into a baseline (§9).
- **Implemented** — built in design/code.
- **Verified** — its verification method passed.
- **Retired** — superseded or removed (via change control, §9); kept for traceability, never deleted.

**Baseline eligibility:** {{A requirement is baseline-eligible only when ATTR-1 through ATTR-7 are complete. ATTR-8 (Risk) is recommended but optional.}}

---

## 8. Traceability

> Lead with the bidirectional idea: every requirement can be followed **forward** (need → requirement → design → code → test) and **backward** (test → requirement → originating need). Forward traceability proves nothing was dropped on the way to implementation; backward traceability proves nothing was built that no one asked for (work with no backward link is "gold-plating" — effort spent on something no requirement justifies). Describe the concrete trace chain *for this project*, say *how* traces are recorded and *who* maintains them, and explain coverage analysis (what a gap in each direction means). Cross-reference any separate traceability matrix the plan governs.

**The trace chain for {{Project Name}}:**

```
stakeholder need (SRC-N)
  → software requirement (SRS REQ-N / SR-N)
    → design element (SDD PURP-N / IF-N)
      → code ({{module / file}})
        → test ({{test ID}})
          → defect ({{tracker ID, if any}})
            → release ({{version}})
```

**How traceability is recorded.** {{Via the Trace Links attribute (ATTR-7, §7), consolidated into a Requirements Traceability Matrix (RTM). The RTM is {{a markdown table at `path/to/rtm.md` / a spreadsheet / managed in tooling — see OQ-DEF-1}}.}}

**Who maintains it.** {{The {{role}} updates trace links whenever a requirement, design element, or test changes. Stale traces are caught by the traceability-coverage metric (MET-3, §10).}}

**Coverage analysis.**
- **Forward gap** — a requirement with no design/code/test link downstream = an *unimplemented requirement*. Investigate: is it dropped, or just not built yet?
- **Backward gap** — code or a test with no requirement upstream = *orphaned work / gold-plating*. Investigate: should there be a requirement, or should the work be removed?

**Related artifact:** {{Requirements Traceability Matrix `RTM-{{PROJECT-ID}}`, governed by this plan (if maintained separately from the requirement attributes).}}

---

## 9. Baselines and Change Control

> A baseline and its change control are inseparable, so they live in one section: a baseline only *means* something if changes to it are controlled. A **baseline (`BL-N`)** is a frozen, agreed snapshot of requirements; after freezing, a requirement changes only through the controlled path described here. First define how a baseline is established (its entry criteria come from §4 and §6), how it is identified and recorded, and what it locks. Then walk the lifecycle of a single change request, step by step. This is the project's structural defense against **scope creep** — the slow, unnoticed growth of scope through changes that were never explicitly approved. This section is also the concrete link to the ISO/IEC/IEEE 12207:2017 configuration-management process.

### 9.1 Establishing a baseline

**Entry criteria.** {{A requirement may enter baseline `BL-N` only if it is Analyzed (§4 gate passed), Validated (§6 exit criterion met), and has attributes ATTR-1..ATTR-7 complete (§7).}}

**Identification and recording.** {{Each baseline gets a sequential ID (`BL-1`, `BL-2`, …), a freeze date, and a recorded list of exactly which requirement IDs (and their versions) it contains. The Current baseline field in the metadata table names the latest.}}

| Baseline | Date | Contents | Status |
|---|---|---|---|
| BL-1 | {{YYYY-MM-DD}} | {{REQ-1 … REQ-N at v{{x}}}} | {{Frozen / Superseded}} |
| BL-2 | {{YYYY-MM-DD}} | {{BL-1 + REQ-N+1 … ; REQ-3 revised}} | {{Frozen}} |

**What a baseline locks.** {{Once frozen, the listed requirements cannot be edited in place. Any change goes through §9.2 and produces either a baseline revision or a new baseline.}}

### 9.2 Change-control lifecycle

> A proposed change to a baselined requirement travels a fixed path. Each step has an owner and leaves a record, so every change has a visible justification.

1. **Submitted** — {{anyone records a change request (CR): what requirement(s), what change, why. Give it a CR ID.}}
2. **Impact-analyzed** — {{determine what is affected: which requirements, designs (SDD), code, tests, and baselines. This uses the traceability chain (§8) — that is what makes impact analysis possible rather than guesswork.}}
3. **Approved / rejected** — {{the change authority named in the metadata decides. Rejections are recorded with a reason, not silently dropped.}}
4. **Implemented** — {{approved changes are applied to the requirement(s) and their attributes; Status (ATTR-4) updated.}}
5. **Audited / recorded** — {{the change is logged, and a new baseline or baseline revision is created (§9.1) so the frozen set always reflects reality.}}

**Configuration-management link.** {{This change-control lifecycle is this project's lightweight instance of the ISO/IEC/IEEE 12207:2017 configuration-management / change-management process. Baselines are the configuration items; the CR log is the change record.}}

**Scope-creep defense.** {{Because every change to a frozen requirement must be submitted, impact-analyzed, and approved, scope cannot grow invisibly. The volatility metric (MET-1, §10) makes the *rate* of change visible too.}}

---

## 10. Requirements Metrics

> Metrics make the *health* of the requirement set observable instead of a feeling. For a solo or small-team project, pick a few low-effort, countable indicators — the goal is a number you can glance at, not a measurement program. Tag each `MET-N`. For each metric give its definition, how often you collect it, who owns it, and — most important for a beginner — *what action a bad reading should trigger*. A metric with no associated action is decoration, not a decision input.

| ID | Metric | Definition | Frequency | Owner | A bad reading triggers… |
|---|---|---|---|---|---|
| MET-1 | Requirements volatility | Number of requirement changes (added/modified/removed via §9.2) per baseline per period | {{Per baseline / monthly}} | {{Role}} | {{High volatility late in the project → pause and stabilize scope before more build; investigate the source.}} |
| MET-2 | Verification coverage | % of requirements with an assigned **and passing** verification method (ATTR-6) | {{Per baseline / sprint}} | {{Role}} | {{Below target → identify unverified requirements and assign/run verification before release.}} |
| MET-3 | Traceability coverage | % of requirements with complete forward **and** backward trace links (§8) | {{Per baseline}} | {{Role}} | {{Gaps → run coverage analysis (§8): forward gap = unimplemented requirement; backward gap = orphaned work.}} |
| MET-4 | Open defects against requirements | Count of open defects linked to a requirement | {{Weekly}} | {{Role}} | {{Rising count → triage; a requirement with many defects may be ambiguous (§5) and need rework.}} |

{{Add or drop metrics to fit team size. For a true solo project, MET-2 and MET-3 alone are often enough.}}

---

## 11. Open Questions

> Where genuinely-undecided *process* choices live, so they are tracked rather than silently forgotten. Following the SDD pattern, split into **deferred-with-defaults** (`OQ-DEF-N`: a question with the default in force until revisited — work proceeds under the default) and **resolved** (`OQ-N`: recorded for traceability so the decision is not re-litigated). These are questions about how the *plan* works, not about the requirements themselves. Resolve and migrate items out as the plan matures.

### 11.1 Deferred with defaults

- **OQ-DEF-1** {{Which tool holds the traceability matrix — a markdown table in the repo, a spreadsheet, or external tooling?}} — *default: {{a markdown table committed alongside the SRS, until volume makes it unwieldy}}.*
- **OQ-DEF-2** {{How formal should change-request submission be for a solo developer?}} — *default: {{a dated entry in a `CHANGES.md` log; promote to a tracker if a second contributor joins}}.*

### 11.2 Resolved (recorded for traceability)

- **OQ-1** {{Question}}: {{Resolution and date}}.

---

## 12. Revision History

> Mandatory final section. Every substantive change to this plan gets a version bump and a row. Because this plan *governs baselines*, a revision that changes the change-control process (§9) or the attribute schema (§7) is itself significant — call such changes out explicitly in the Changes column, since they affect how every requirement is handled going forward.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Requirements Sources
- §5 Specification Approach
- §7 Requirement Attributes
- §9 Baselines and Change Control
- §12 Revision History

**Optional sections** (include if relevant):
- §3 Elicitation Approach (can be brief if requirements come from a single obvious source)
- §4 Analysis Approach (can be brief on a small project, but keep the prioritization scheme)
- §6 Validation Approach (defer detail if too early, but keep the exit criterion)
- §8 Traceability (keep at least the trace chain; full RTM optional for small projects)
- §10 Requirements Metrics (a solo project may keep only MET-2 and MET-3)
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (compose with sibling SRS/SDD prefixes):
- `BL-N` — requirement baselines (frozen sets)
- `SRC-N` — requirements sources (§2)
- `ATTR-N` — requirement attributes / schema rows (§7)
- `MET-N` — requirements metrics (§10)
- `OQ-N` / `OQ-DEF-N` — open questions (resolved / deferred-with-defaults)
- This plan does **not** invent requirement IDs — the SRS supplies the actual `REQ-N` / `SR-N` identifiers; the SDD supplies `PURP-N` / `IF-N` design IDs. This plan's prefixes name *process* items so the whole document set cross-references cleanly.

**Tailoring**:
- Section headers are guidance, not mandates. Merge or shorten sections the project does not need — just don't drop the Required set.
- **Solo developer / small team collapse:** keep §1 (purpose + a short definitions table), §5 (how you write requirements), §7 (the attribute columns you actually use — often just ID, Priority, Status, Verification Method, Trace Links), §9 (even a one-line "baselines are git tags; changes go in `CHANGES.md`" counts), and §12. §2–§4, §6, §8, §10, §11 can each collapse to a paragraph or be folded into §1. The discipline matters more than the page count — a one-page RMP that you actually follow beats a ten-page one you don't.
- This plan governs the *process*; the requirements themselves stay in the SRS. Don't copy requirements into this document.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29148:2018 (with ISO/IEC/IEEE 12207:2017 for the configuration-management process), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
