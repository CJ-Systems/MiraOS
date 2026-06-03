# Software Construction Plan Template

> **Template purpose:** Lightweight Software Construction Plan structure aligned to the SWEBOK Guide v3.0 Software Construction Knowledge Area and the ISO/IEC/IEEE 12207:2017 software Construction (implementation) process. Use this template when you are about to start building a system whose requirements (SRS) and design (SDD) are settled and you need a written plan for HOW the code will be constructed, verified at the unit level, and integrated. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** After the SRS (WHAT) and SDD (HOW the design works) exist and before — or just as — coding begins. The Construction Plan is the bridge document between design and a running system: it does not contain the code, it describes the rules, environment, and process under which the code gets written.
>
> **Companion standard:** ISO/IEC/IEEE 12207:2017 (Systems and software engineering — Software life cycle processes), Software Construction process. Section structure additionally aligned to the SWEBOK Guide v3.0 Software Construction Knowledge Area.
>
> **Status of this template:** A lightweight skeleton derived from public sources — a construction-plan structure aligned to the SWEBOK Guide v3.0 Software Construction Knowledge Area and the ISO/IEC/IEEE 12207:2017 software Construction process. It is faithful to the SWEBOK KA outline but reduced for solo/small-team use. ISO/IEC/IEEE 12207:2017 is a PAYWALLED standard — the structure here is derived from the publicly described process names and the open SWEBOK KA, and reproduces NO normative text from the standard; verify section requirements against the full standard for enterprise/regulated/safety-critical/contractual contexts. Because the section set follows the SWEBOK Construction KA, this document names 12207 as a companion process standard but no single normative standard governs its full outline.

---

# Software Construction Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | CP-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 12207:2017 (Construction process) + SWEBOK v3.0 Software Construction KA (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Predecessor documents | SRS-{{PROJECT-ID}}-001, SDD-{{MODULE-ID}}-001 (the WHAT and the HOW this plan constructs) |
| Target environment | {{Primary language / runtime / platform — e.g., Python 3.x on Linux}} |
| Construction approach | {{Incremental / iterative / single-pass — e.g., incremental, mini-waterfall per work package}} |

---

## 1. Introduction

> This section orients the reader: why the document exists, what it covers, the words it uses, and what it depends on. It has four standard subsections. Delete this blockquote guidance once each subsection is filled in.

### 1.1 Purpose

> One paragraph stating what this document is for. The key idea for a true beginner: **software construction** is the SWEBOK Knowledge Area covering the detailed creation of working software — coding, verification, unit testing, integration, and debugging. It is the bridge between the design (the SDD, which says HOW the system is shaped) and an actual running system. This document is the *plan for* that construction, not the construction itself: it sets the rules and the process, while the code lives in the repository.

{{This document defines how {{Project Name}} will be constructed — built, coded, unit-verified, and integrated. It sits between the Software Design Description (SDD-{{MODULE-ID}}-001), which describes HOW the design is shaped, and the running code in the repository. It records the construction environment, the coding standards, the implementation and review process, and the traceability from each built unit back to the design and requirements it satisfies. It does not contain the code; it is the plan the code is built under.}}

### 1.2 Scope

> Define what this plan covers and what it explicitly excludes. Name the components or subsystems being constructed here, and state plainly what is constructed elsewhere, reused, or deferred — so the boundary is unambiguous.

In scope (constructed under this plan):
- {{Component / subsystem 1}}
- {{Component / subsystem 2}}
- {{...}}

Out of scope (constructed elsewhere, reused, or deferred):
- {{Reused third-party library}} — adopted as a dependency, not built here (see §2).
- {{Generated / vendor component}} — produced by {{tool / vendor}}, not hand-constructed.
- {{Deferred component}} — {{reason for deferral; e.g., out of scope for v1}}.

### 1.3 Definitions and Acronyms

> Define the terms a reader must understand before the rest of the document makes sense. The rows below seed the table with the construction concepts used throughout. Keep the ones that apply; add project-specific terms.

| Term | Definition |
|---|---|
| Work package (WP) | One self-contained, assignable unit of construction (a component, feature, script, or data asset). Numbering work packages WP-1, WP-2, … is what makes progress trackable and lets each piece trace back to the requirement and design element it satisfies. |
| Coding standard | An agreed set of rules for how code is written (naming, formatting, comments, error handling, logging). Its purpose is not aesthetics — it is so any reader (human or agent) can predict the shape of the code, and so reviews catch real defects instead of arguing about style. |
| Static analysis | Automated tools that read source code WITHOUT running it and flag likely defects, style violations, or security issues. Contrast with dynamic testing (unit tests), which runs the code. "Static" literally means the program is not executing. |
| Unit test | A small automated check that exercises one piece of code (a function, a class) in isolation and asserts it behaves as expected. Stubs, mocks, and drivers are stand-in pieces used to isolate the unit from its neighbors so the test measures only the one thing. |
| Code coverage | The percentage of code lines or branches that unit tests actually execute. High coverage is a floor, not a ceiling: it tells you what was NOT tested, not that what ran was correct. |
| Build / integration | "Build" turns source into a runnable or installable artifact (compile, bundle, package). "Integration" is combining separately-constructed units and checking they work together. "Continuous integration (CI)" means doing this automatically and often, so breakage is caught the day it happens, not weeks later. |
| Traceability | An explicit, followable link from each implemented unit back to the design element and requirement it fulfills (and forward to the tests that verify it). It answers "why does this code exist?" and "if requirement X changes, what code is affected?" |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> List the documents this plan depends on or that inform it, grouped for readability. The predecessor SRS and SDD are the WHAT and HOW that this plan constructs; the coding-standard and external-standard references back up §4 and the document's framing.

Predecessor documents:
- SRS-{{PROJECT-ID}}-001 — {{path/to/srs.md}} — requirements (the WHAT) being constructed.
- SDD-{{MODULE-ID}}-001 — {{path/to/sdd.md}} — design (the HOW) being constructed.

Architecture Decision Records:
- ADR-NNNN — {{decision relevant to construction; e.g., language/runtime choice}}.
- {{...}}

Coding-standard / style documents:
- {{path/to/style-guide or linter config}} — {{e.g., the formatter/linter config this project adopts}}.

External standards:
- ISO/IEC/IEEE 12207:2017 — software life-cycle processes; this plan covers its Construction (implementation) process.
- SWEBOK Guide v3.0 — Software Construction Knowledge Area; the outline this plan's sections follow.

---

## 2. Construction Scope

> This is the spine of the document: the **work-package inventory**. A *work package* (WP) is one assignable unit of construction. Giving each a `WP-N` id is what lets every later section — review, testing, traceability — refer to a specific piece without ambiguity. The "Traces to" column is filled from the SDD's design ids (`PURP-`, `METH-`, `CON-`, `IF-`) and the SRS's requirement ids (`REQ-`, `FR-`, `NFR-`); every WP should trace UP to at least one of them, because a unit of construction with nothing above it is either scope creep or a missing requirement. Before the table, state in prose what is explicitly NOT being constructed here, so the boundary is unambiguous.

**Not constructed under this plan.** {{State plainly what is reused, generated, or vendor-supplied rather than built. Reused libraries, code generated by tooling, and vendor components are dependencies, not work packages — they appear in §3 (Development Environment) as part of the dependency set, not here. Example: {{Library X}} is consumed as a pinned dependency; {{generated client Y}} is regenerated from {{spec}}, never hand-edited.}}

**Work-package inventory.** Each row is one assignable unit of construction. Add rows as the design is decomposed; keep WP ids stable once assigned, because the rest of the plan references them.

| WP-ID | Item (component / feature / interface / script / data asset / supporting tool) | Type | Traces to (SDD ID / REQ ID) | Notes |
|---|---|---|---|---|
| WP-1 | {{e.g., {{module}} core service}} | Component | IF-1, FR-3 | {{primary build target}} |
| WP-2 | {{e.g., {{public}} API surface}} | Interface | IF-2, REQ-5 | {{exposes WP-1}} |
| WP-3 | {{e.g., config loader script}} | Script | CON-1 | {{supporting}} |
| WP-4 | {{e.g., seed taxonomy / fixture data}} | Data asset | PURP-2, FR-7 | {{shipped with build}} |
| WP-5 | {{e.g., build/CI tooling}} | Supporting tool | — | {{enables §9; may not trace to a requirement}} |
| ... | ... | ... | ... | ... |

---

## 3. Development Environment

> Document the concrete machinery so a new contributor — or an agent — can reproduce the build from scratch. The central beginner idea is **reproducibility**: "works on my machine" is the failure this section prevents. Pinning exact tool and dependency versions, and recording them in a *lockfile* (a generated file that records the exact resolved version of every dependency, transitive ones included), is what makes one person's working build reproducible on another machine and next month. Record the languages and versions, the package manager and lockfile policy, the build system, the repository layout and branching convention, and any environment constraints. Respect project constraints: if this project forbids containers, state native install here — do not default to Docker.

**Version / tool matrix.** Pin versions; record the lockfile that captures the full resolved dependency set.

| Concern | Choice | Version / pin | Notes |
|---|---|---|---|
| Primary language | {{e.g., Python}} | {{e.g., 3.x}} | {{required; pinned because …}} |
| Runtime / platform | {{e.g., Linux x86_64}} | {{e.g., kernel 6.x}} | {{target environment}} |
| Package / dependency manager | {{e.g., the project's package manager}} | {{version}} | Lockfile: {{lockfile name}}, committed to the repo |
| Build system | {{e.g., the project's build tool}} | {{version}} | {{entry point / command}} |
| Editor / toolchain assumptions | {{e.g., any editor honoring the formatter config}} | — | {{e.g., format-on-save expected}} |
| {{Other tool}} | {{choice}} | {{version}} | {{notes}} |

**Lockfile policy.** {{State that the lockfile is committed and is the source of truth for dependency versions; describe when and how it is regenerated, and the rule that no one installs dependencies outside the locked set.}}

**Repository layout and workflow.** {{Describe where source, tests, build config, and assets live in the repository. Describe the branching/workflow convention — e.g., the integration branch, how feature work branches off and merges back.}}

**Environment constraints.** {{State hard constraints — e.g., no containers (native install only); offline build requirement; specific OS. If the project forbids Docker/containers, native install is documented here and containerization is not used.}}

---

## 4. Coding Standards

> State the concrete rules — or, better, point at the authoritative config the project adopts — for how code is written. A *coding standard* exists so that reviews catch real defects rather than litigate style, and so any reader can predict the shape of the code. The strongest form of a coding standard is an auto-formatter plus a linter whose config is committed to the repository: machine-enforced rules don't drift and don't need arguing. List rules by hand only where no tool covers them. For prose-native / Software-3.0 artifacts, the "code" may be structured prose (skill specs, agent instructions, documents) — in that case the standard governs document structure, voice, and section conventions rather than syntax; adapt the rows accordingly. Tag individual rules `CS-N` if review checklists (§6) will cite them.

**Authoritative tooling (preferred over hand-listing).**

| Concern | Tool / config | Where it lives | Enforced how |
|---|---|---|---|
| Formatting | {{auto-formatter}} | {{config path}} | {{format-on-save / CI check}} |
| Linting | {{linter}} | {{config path}} | {{CI gate / pre-commit}} |
| {{Other}} | {{tool}} | {{path}} | {{how}} |

**Rules not covered by tooling** (cite as `CS-N` where review checklists reference them):

- **CS-1 Naming.** {{Naming conventions for files, functions, types, constants.}}
- **CS-2 Commenting / documentation.** {{When and how code is commented; docstring/API-doc expectations.}}
- **CS-3 Error handling.** {{How errors are raised, caught, and surfaced; what must never be silently swallowed.}}
- **CS-4 Logging.** {{What is logged, at what level, and what must never be logged — e.g., secrets or personal data.}}
- **CS-5 Security practices.** {{Input validation, secrets handling, dependency-trust rules.}}
- **CS-6 Maintainability.** {{Function size / complexity limits, duplication rules, structure conventions.}}
- **CS-N {{Prose-native rule, if applicable}}.** {{For structured-prose artifacts: document section order, voice, placeholder conventions.}}

---

## 5. Implementation Approach

> Describe HOW units actually get built, not just the rules they follow. The key beginner distinction is **incremental construction** versus big-bang. Incremental means: build a thin slice end-to-end first (one feature working from input to output), confirm it works, then widen — adding the next slice on a foundation that already runs. Big-bang means building every part separately and only assembling at the end, where all the integration surprises arrive at once. Incremental construction surfaces integration problems early and small. Pair it with the **smallest-safe-change** discipline: prefer the minimal edit that achieves the goal over a sweeping rewrite, because a small change is easier to verify and less likely to break code that already works. If the project runs a per-unit mini-waterfall, document that cadence here and say what moves a work package to "done."

**Ordering.** {{Incremental vs. single-pass. If incremental, name the thin first slice and the order in which WPs from §2 are built.}}

**Prototyping / spikes.** {{When throwaway prototypes or time-boxed spikes are used to reduce uncertainty before committing to a build, and the rule that spike code is not promoted to production without proper construction.}}

**Reuse before build.** {{The rule that an existing library or prior unit is preferred over writing new code; how reuse candidates are checked before a WP starts.}}

**Refactoring discipline.** {{Smallest-safe-change-first; when refactoring is allowed (with tests green before and after); the rule against mixing a refactor with a behavior change in the same step.}}

**Integrating partial work.** {{How incomplete WPs are integrated safely — e.g., behind a flag, as a stub, or kept on a branch until the slice is whole.}}

**Per-work-package lifecycle.** Each WP from §2 moves through this cadence; the WP is "done" only when the final gate is met.

| Step | What happens | Gate to advance |
|---|---|---|
| Requirements | {{Confirm which SRS/SDD ids this WP satisfies}} | {{Traces-to filled in §2}} |
| Design | {{Confirm the SDD element is detailed enough to build}} | {{No open design question blocks the WP}} |
| Implement | {{Write the code per §4}} | {{Compiles / runs; lint clean}} |
| Verify | {{Unit tests per §8}} | {{Tests pass; coverage target met}} |
| Capture | {{Update traceability §10; note decisions}} | {{Matrix row complete; review passed §6}} |

---

## 6. Code Review Approach

> Define the review gate. A *code review* is a second set of eyes confirming that code is correct, readable, and matches the design BEFORE it merges into the integration branch. The two concepts that turn "looks good to me" into a repeatable gate are **entry criteria** (what must already be true for a work package to *enter* review) and **exit criteria** (what "approved" concretely means). In a solo or human-plus-agent setup, name who plays the reviewer role — and note that the agent surfacing its reasoning (explaining *why* it built something a certain way) is part of the review input, not a substitute for the human approval gate.

**Who reviews.** {{Reviewer role(s). In a solo setup, state the self-review discipline — e.g., review on a separate pass / next session. In a human+agent setup, the agent surfaces reasoning and proposes; the human holds the approval gate.}}

**Entry criteria** (a WP may enter review only when all hold):
- Compiles / runs without error.
- Unit tests for the WP pass (§8).
- Static analysis is clean to threshold (§7).
- Traceability row for the WP is filled (§10).

**Review checklist** (what the reviewer confirms):
- Correctness — the code does what the WP's requirement/design says (cite `REQ-`/`IF-` ids).
- Readability — matches the coding standard (§4); cite `CS-N` rules where relevant.
- Design fit — does not contradict the SDD; no undesigned scope added.
- Tests — the unit tests actually exercise the behavior, not just inflate coverage.
- Safety — no secrets, no swallowed errors, no insecure pattern introduced.

**Exit criteria** ("approved" means):
- {{All checklist items satisfied or each exception recorded with justification.}}
- {{Reviewer (human) sign-off recorded; the WP may merge / integrate.}}

---

## 7. Static Analysis

> Specify the automated tools that read the code WITHOUT running it. To restate plainly: *static analysis* inspects source as text/structure and catches a different class of defect than tests do — unused variables, possible null dereferences, insecure patterns, dead code — things a unit test might never exercise. A documented **blocking threshold** matters because it makes the gate objective: a finding at or above the threshold stops the build; below it, it warns. Without a written threshold, every finding becomes a fresh judgment call. Also document the workflow for handling findings: fix, suppress with a written justification, or accept.

**Tools and thresholds.**

| Tool | Scope (what it checks) | Blocking threshold |
|---|---|---|
| {{Linter}} | {{style + likely-bug rules}} | {{e.g., any error-level finding blocks; warnings allowed}} |
| {{Type checker}} | {{type correctness}} | {{e.g., any type error blocks}} |
| {{Security scanner}} | {{insecure patterns, vulnerable deps}} | {{e.g., high/critical blocks; medium warns}} |
| {{Other}} | {{scope}} | {{threshold}} |

**Finding disposition workflow.** Every finding is resolved one of three ways, and the resolution is recorded:
- **Fix** — change the code so the finding no longer fires (default).
- **Suppress with justification** — silence a specific finding inline or in config WITH a written reason; suppressions are reviewed in §6.
- **Accept** — a category-wide decision (recorded here or in an ADR) that a class of finding does not apply to this project.

{{Note where the static-analysis config lives in the repository and whether it runs locally, in CI (§9), or both.}}

---

## 8. Unit Verification

> Cover testing at the **unit** level only — one piece of code in isolation. Define the terms plainly. A *unit test* exercises a single function or class and asserts the result. *Isolation* means you replace the unit's neighbors with stand-ins — *stubs* (return canned values), *mocks* (also record how they were called), *drivers* (call the unit for you) — so the test measures only the one unit, not its dependencies. And the *coverage caveat*: code coverage is a floor, not a proof. 90% coverage means 10% was never executed by any test; it does NOT mean the 90% is correct, only that it ran. Keep this section's scope tight: integration-level and system-level verification live in the verification / SRS documents, not here. Tie each WP's acceptance criteria back to its `WP-N` id from §2.

**Framework and conventions.** {{Unit-test framework; where tests live; naming convention (e.g., one test file per source file); how tests are run.}}

**Test data strategy.** {{How test data/fixtures are created and kept; whether fixtures are checked in; rule against tests depending on live external state.}}

**Stubs / mocks / drivers.** {{Which isolation approach is used and when; the rule that a unit test must not silently reach a real network, database, or filesystem unless that is the unit under test.}}

**Coverage expectation.** Target: {{e.g., ≥ 80% line coverage on constructed WPs}}. **Caveat:** this is a floor that flags untested code; it is not evidence the covered code is correct. Reviewers (§6) confirm the tests assert *meaningful behavior*, not just execute lines.

**Per-WP acceptance criteria.** A work package is unit-verified when:

| WP-ID | Acceptance criterion (unit level) | Coverage met? |
|---|---|---|
| WP-1 | {{Tests for {{behavior}} pass; edge cases {{…}} covered}} | {{yes/no}} |
| WP-2 | {{…}} | {{…}} |
| ... | ... | ... |

> Integration verification (do WP-1 and WP-2 work together?) and system verification (does the whole thing meet the SRS?) are out of scope here — see §9 for integration build behavior and the verification / SRS documents for the levels above unit.

---

## 9. Build and Integration

> Document how source becomes a runnable artifact and how separately-built units come together. Keep two ideas distinct: **build** is source → runnable/installable artifact (compile, bundle, package); **integration** is combining units and checking they work together. **Continuous integration (CI)** is simply "do the build and the integration automatically and often, so breakage surfaces the same day it is introduced rather than weeks later when no one remembers the change." Record the pipeline steps, how dependencies are resolved (from the locked set in §3), what the release artifact is, how often integration happens, and what happens when integration fails. Respect the no-container constraint if the project has one.

**Build pipeline (source → artifact).**

| Step | Action | Produces |
|---|---|---|
| 1 | {{Resolve dependencies from lockfile (§3)}} | {{installed/locked deps}} |
| 2 | {{Run static analysis (§7) + unit tests (§8)}} | {{pass/fail gate}} |
| 3 | {{Compile / bundle / package}} | {{runnable or installable artifact}} |
| 4 | {{Version / tag the artifact}} | {{release artifact}} |

**Dependency resolution.** {{All dependencies come from the locked set (§3); no unlocked installs in the build. State how a new dependency is added and re-locked.}}

**Release artifact.** {{What ships — e.g., an installable package, a bundle, a container-free native install. If the project forbids containers, the artifact is a native package/bundle, not an image.}}

**Integration frequency.** {{Continuous (per change) vs. scheduled. If CI: each change to the integration branch triggers steps 1–2 automatically.}}

**Integration-failure handling.** {{What happens when the build or integration breaks — e.g., the change does not merge; the break is fixed before any new work proceeds; who is notified.}}

**Where build/CI config lives.** {{Path in the repository to the build/CI configuration.}}

---

## 10. Traceability

> This is the section that makes the whole plan auditable. *Traceability* answers two questions: "why does this code exist?" — trace a work package UP to the design element and requirement it satisfies — and "if this requirement changes, what breaks?" — trace DOWN from the requirement to the code and the tests that verify it. Keeping the matrix current is what prevents two silent failures: **orphan code** (a unit that satisfies no requirement — either scope creep or an undocumented need) and **untested requirements** (a requirement with no verifying test). If the project maintains a dedicated Requirements Traceability Matrix document, this section references it instead of duplicating it.

**Trace matrix.** Each work package links up to design + requirement and forward to the test that verifies it.

| Work Package (WP-N) | Implements design element (SDD `IF-`/`PURP-` id) | Satisfies requirement (SRS `REQ-`/`FR-` id) | Verified by (test id) | Status |
|---|---|---|---|---|
| WP-1 | IF-1 | FR-3 | {{TEST-1}} | {{Not started / In progress / Done}} |
| WP-2 | IF-2 | REQ-5 | {{TEST-2}} | {{…}} |
| WP-3 | CON-1 | {{—}} | {{TEST-3}} | {{…}} |
| WP-4 | PURP-2 | FR-7 | {{TEST-4}} | {{…}} |
| ... | ... | ... | ... | ... |

> If a dedicated Requirements Traceability Matrix exists, replace the table above with: "Traceability is maintained in {{RTM document id / path}}; this plan defers to it." Keep the matrix current as WPs are built — a stale matrix is worse than none, because it implies coverage that no longer exists.

---

## 11. Open Questions

> This is where honest uncertainty is recorded rather than hidden. Each entry names the question and what is blocking resolution or who decides. Two kinds: load-bearing questions that actually block construction (`OQ-N`), and questions deferred with a stated default that lets work continue (`OQ-DEF-N`) — the default is the working answer until someone proves it inadequate. Resolved questions may be kept with their resolution noted, so the reasoning is auditable later.

### 11.1 Load-bearing (block construction)

- **OQ-1** {{Question}} — {{what's blocking resolution; who decides}}.
- **OQ-2** {{Question}} — {{blocker; decider}}.

### 11.2 Deferred with defaults

- **OQ-DEF-1** {{Question}} — *default: {{the working answer until revisited}}.* Revisit if {{the default proves inadequate because …}}.
- **OQ-DEF-2** {{Question}} — *default: {{default}}.*

### 11.3 Resolved (recorded for traceability)

- **OQ-N** {{Question}}: {{Resolution and date / ADR reference}}.

---

## 12. Revision History

> Every substantive change to this plan gets a version bump and a row here, so the document's own history is auditable the same way the code's history is. Treat the plan as a living document: when the work-package inventory, the environment, or the process changes, record it.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Construction Scope (the work-package inventory is the spine)
- §3 Development Environment
- §4 Coding Standards
- §5 Implementation Approach
- §10 Traceability
- §12 Revision History

**Optional sections** (include if relevant):
- §6 Code Review Approach (keep even solo — self-review counts; collapse the "who reviews" prose)
- §7 Static Analysis (omit only if no static tooling is used yet; recommend keeping)
- §8 Unit Verification (defer detail if construction has not begun, but state the intended framework)
- §9 Build and Integration (collapse to a single build command for a tiny project)
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- CP-{{PROJECT-ID}}-001: this document's id.
- WP-N: work packages — one assignable unit of construction each (§2).
- CS-N: individual coding-standard rules, where review checklists cite them (§4, §6).
- OQ-N / OQ-DEF-N: open questions (load-bearing / deferred-with-defaults) (§11).
- Cross-document: work packages trace UP to SDD design ids (`PURP-`, `METH-`, `CON-`, `IF-`) and SRS requirement ids (`REQ-`, `FR-`, `NFR-`), and forward to test ids. These prefixes are what let the SRS, SDD, and this plan cross-reference cleanly.

**Tailoring**:
- The section set follows the SWEBOK Construction KA; treat it as guidance, not obligation. Add or merge sections as the project needs, but state deviations explicitly.
- **Solo developer / small team:** the document collapses substantially. The work-package inventory (§2) and traceability (§10) earn their keep even for one person — they are how you answer "where am I?" and "why does this exist?" across sessions. §6 becomes a self-review discipline (review on a later pass), the reviewer in §6 and the approval authority in the sign-off block may be the same person, and §9 may shrink to a single build command. Keep §1, §2, §4, and §10; compress the rest to a few lines each.
- For prose-native / Software-3.0 artifacts, "construction" is writing structured prose. The coding standard (§4) governs document structure and voice; work packages (§2) are documents or skills; "tests" (§8) become structural/consistency checks. Adapt rather than discard.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 12207:2017 Construction process (and the complete SWEBOK Construction KA), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
