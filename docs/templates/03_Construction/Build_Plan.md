# Build Plan Template

> **Template purpose:** Lightweight Build Plan structure for documenting how a software system is turned from its source inputs into deliverable, runnable artifacts — repeatably, by someone other than the original author. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When a project has source code that must be compiled, packaged, or assembled into something you ship or run (a binary, a package, a container image, a deployable bundle), and you need that transformation written down so it can be re-run on a clean machine or by a continuous-integration (CI) server. The Build Plan sits after the SRS (WHAT) and SDD (HOW the design is structured) — it documents how the realized design is TRANSFORMED into an artifact, and stops once that artifact has been produced and verified.
>
> **Companion standard:** ISO/IEC/IEEE 12207:2017 — Systems and software engineering — Software life cycle processes (construction & integration processes); continuous-integration practice (industry convention, no single normative standard).
>
> **Status of this template:** Lightweight extract aligned to the construction and integration processes of ISO/IEC/IEEE 12207:2017, plus common continuous-integration practice (industry convention, not a single normative standard). Faithful to the standard's intent but reduced for solo/small-team use. **Author note:** ISO/IEC/IEEE 12207:2017 is a paywalled standard — this template was built to its publicly-described process structure, NOT by quoting its text; verify section coverage against the purchased standard for enterprise/regulated/safety-critical contexts. The continuous-integration portions follow widely-held practice and name no single normative standard. No copyrighted standard text is reproduced here.

---

# Build Plan — {{System Name}}

| Field | Value |
|---|---|
| Document ID | BLD-{{SYSTEM-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 12207:2017 (construction & integration, lightweight) + CI practice |
| Owner | {{Project name or owner}} |
| Build type | {{One-off / Manual / CI-automated / Release}} |
| Target environment(s) | {{Local dev / CI / Staging / Production target(s) this plan builds for}} |
| Reproducibility goal | {{Best-effort / Pinned-inputs / Bit-for-bit deterministic}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: what this document is for and what it specifies.
>
> Beginner note: a **build** is the act of turning source code and other source inputs into a runnable or shippable thing — a binary, a package, a container image, a deployable bundle. A **Build Plan** is the *executable recipe* for that transformation. The test of a good Build Plan is simple: if a fresh machine (or a CI runner) followed only this document, it should produce the same artifact the author gets. State the document's place in the life cycle so the reader knows where it fits relative to its siblings.

This document specifies how **{{System Name}}** is built from its source inputs into deliverable artifacts, repeatably, by someone other than the original author. It sits in the project's document life cycle as follows: the Software Requirements Specification (SRS) says *what* the system must do; the Software Design Description (SDD) says *how* the design is structured; this Build Plan says how the realized design is *transformed* into a runnable or shippable artifact. {{One or two sentences naming the system and the kind of artifact it produces — e.g. "a single console binary," "a Python wheel," "a container image."}}

### 1.2 Scope

> Define what this plan covers and what it explicitly does NOT cover. Drawing this boundary up front stops the document from sprawling into testing or deployment, which have their own plans.
>
> Beginner note: state the **reproducibility goal** here in plain prose. A *reproducible* (or *deterministic*) build is one where building the same pinned inputs produces the same outputs every time, no matter who runs it or when. The opposite — "it builds on my machine" — is the failure this whole document exists to prevent.

In scope:
- {{Which system / repositories / components this plan builds}}
- {{Which build types are covered — local developer build, CI build, release build}}
- Producing the artifact(s) listed in §6 and verifying them per §7

Out of scope (covered elsewhere):
- **Test design and the full test campaign** — see the Test Plan ({{04_Testing_and_VV}}). This plan includes only fast post-build *smoke* checks (§7), not the full test suite.
- **Deployment and release** — see the Release / Deployment Plan. This document stops once the artifact has been produced and verified; it does not push, deploy, or promote to production.
- {{Anything else deliberately excluded}}

**Reproducibility goal (prose):** {{State the goal and why — e.g. "This plan targets pinned-inputs reproducibility: every dependency is version-locked so a build re-run from the same baseline pulls identical inputs. Bit-for-bit determinism is a future goal, deferred until the release stage (see OQ-DEF-1)."}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Define terms that, if undefined, would lead to misreading the rest of the document. Beginner-facing rows are pre-seeded below so a reader new to formal build practice is not blocked; add project-specific tooling terms.

| Term | Definition |
|---|---|
| Build | The act of turning source code and other source inputs (the contents of the source tree) into a runnable or shippable artifact — a binary, package, container image, or bundle. |
| Artifact | The concrete thing a build produces and that later life-cycle stages consume: an executable, a wheel / jar / npm package, a container image, or a signed bundle. The standards-vocabulary word for "the build's output you actually ship or run." |
| Build input | Anything consumed to produce the result: source, locked dependency versions, config, secrets, base images. |
| Build output | Anything the build emits: the artifact, logs, checksums, a manifest. Listing inputs and outputs explicitly is what makes a build *auditable*. |
| Reproducible / deterministic build | The property that building the same pinned inputs produces the same outputs every time, regardless of who runs it or when. |
| Pinning / version locking | Recording the exact version of every dependency (a lockfile, a pinned tag, a digest) so a future build pulls the same thing rather than "whatever is latest today." Unpinned inputs are the most common reason a build that worked last month fails this month. |
| Checksum / hash | A short fingerprint (e.g. SHA-256) computed from a file's bytes. Recording it next to an output lets anyone later confirm the artifact they have is byte-for-byte the one this build produced, and was not tampered with or corrupted. |
| Continuous integration (CI) | The practice of running the build (and its verification checks) automatically on every change, on a shared server, rather than only by hand on a developer's laptop. CI is where a build plan most often gets executed; the plan is the spec the CI configuration implements. |
| Smoke test | A tiny, fast check run right after a build that answers only "did the thing come out alive?" (e.g. the binary launches, prints its version, exits 0). Not full testing; it catches gross breakage before more expensive steps run. |
| Baseline / labeling | A *baseline* is a named, frozen snapshot of inputs + outputs (often tied to a version tag) that you can return to exactly. *Labeling* is attaching that human-readable name / version to the artifact so it can be tracked through later stages. |
| {{Tooling term}} | {{Project-specific build tool / runtime / package-manager term}} |
| ... | ... |

### 1.4 References

> List the documents this build consumes or corresponds to, categorized for readability. Use the `| Ref | Document |` form consistent with the SDD.

| Ref | Document |
|---|---|
| R1 | {{path/to/srs.md}} — Software Requirements Specification (the WHAT this build realizes) |
| R2 | {{path/to/sdd.md}} — Software Design Description (component decomposition this build assembles) |
| R3 | ADR-NNNN — {{relevant build / packaging / dependency decision}} |
| R4 | {{path/to/build/tool/docs}} — build tooling documentation (compiler, build tool, package manager) |
| R5 | {{path/to/ci/config}} — CI configuration file(s) this plan corresponds to (e.g. the pipeline that automates §5) |
| R6 | ISO/IEC/IEEE 12207:2017 — software life cycle processes (construction & integration) — companion standard |
| ... | ... |

---

## 2. Build Scope

> This is the inventory of everything that is part of THIS build. It draws the boundary so the reader knows exactly what is in and what is out.
>
> Beginner note: a **configuration item (CI ID)** is a configuration-management identifier — a stable label given to each thing under version / configuration control, so it can be referenced consistently across documents (here it ties to §9 Configuration Management). Do not confuse "CI ID" (a configuration item's identifier) with "CI" meaning continuous integration — both abbreviations are common; this column means the former.

Inventory of items in this build:

| CI ID | Item | Type | Source location | In this build? |
|---|---|---|---|---|
| {{CM-001}} | {{Main application repo}} | repository | {{git URL / path}} | Yes |
| {{CM-002}} | {{Core module}} | component/module | {{path within repo}} | Yes |
| {{CM-003}} | {{Third-party library X}} | external dependency | {{registry + locked version}} | Yes |
| {{CM-004}} | {{Generated client / docs}} | generated artifact | {{generator + output path}} | Yes |
| {{CM-005}} | {{Runtime config bundle}} | configuration item | {{path / config store}} | Yes |
| {{CM-006}} | {{Experimental component Y}} | component/module | {{path}} | No — {{reason excluded}} |

(Type ∈ {repository, component/module, external dependency, generated artifact, configuration item}.)

**Build topology:** {{Describe which components build together vs. separately. If components depend on one another, state the build order — e.g. "core module builds first; the CLI links against it; the docs are generated last from the built binary." If everything builds as one unit, say so.}}

**Deliberate exclusions:** {{List any items left out of this build and why — e.g. "the experimental component Y is excluded until its dependency is pinned (see §10)."}}

**Component decomposition:** This plan does not restate the system's component breakdown — see the SDD (R2) for the authoritative decomposition. This section names only what each component contributes *as a build input or product*.

---

## 3. Build Environment

> This describes the exact conditions the build needs. It is the single biggest source of "works on my machine" failures, so write it precisely enough that someone with a clean machine could recreate these conditions exactly.
>
> Beginner note: an **environment variable** is a named value the operating system hands to a running program (e.g. a path, a flag, or a credential). Builds often read configuration from environment variables rather than hard-coding it. A **secret** is a sensitive value (token, key, password) the build needs but that must never be written into source or logs.

### 3.1 Tools and runtimes

| Tool / Runtime | Pinned version | Install / source | Required for steps |
|---|---|---|---|
| {{Language runtime}} | {{e.g. 3.12.x}} | {{install method / source}} | STEP-1, STEP-2 |
| {{Build tool}} | {{pinned version}} | {{source}} | STEP-2 |
| {{Package manager}} | {{pinned version}} | {{source}} | STEP-1 |
| {{Compiler / linker}} | {{pinned version}} | {{source}} | STEP-2 |
| {{Packaging / build engine}} | {{pinned version}} | {{source}} | STEP-3 |
| ... | ... | ... | ... |

### 3.2 Operating system / platform

- **Build host OS:** {{e.g. WSL2 Ubuntu 24.04 — state the project's actual environment}}
- **Cross-platform targets (if any):** {{e.g. "build produces a Linux x86-64 binary only; macOS/Windows out of scope for v1"}}
- **Containerized build environments:** {{State the project policy. If the project forbids containerized builds, say so explicitly here so no reviewer proposes a container-based build by default — e.g. "This project does not use container-based build environments; builds run natively on the host. Do not introduce a containerized build step."}}
- **CI runner image / spec (if the build runs in CI):** {{name the runner image and its pinned tag/digest, or "n/a — manual build only"}}

### 3.3 Environment variables

| Variable | Purpose | Example / default | Secret? |
|---|---|---|---|
| {{BUILD_PROFILE}} | {{selects debug vs. release flags}} | {{release}} | No |
| {{OUTPUT_DIR}} | {{where artifacts are written}} | {{./dist}} | No |
| {{REGISTRY_TOKEN}} | {{auth to pull private dependencies}} | {{(injected by CI)}} | Yes |
| ... | ... | ... | ... |

### 3.4 Credentials and secrets

> Name WHAT secrets the build needs and HOW they are supplied. Never embed actual values anywhere in this document, in source, or in logs.

The build requires the following secrets:

- **{{Secret name}}** — {{what it authorizes, e.g. "pull access to the private package registry"}}. Supplied via {{how — e.g. "an environment variable injected by the CI secret store at run time; never committed to the repository"}}.
- {{Additional secrets...}}

If no secrets are required, state: {{"This build requires no secrets — all inputs are public."}}

---

## 4. Build Inputs

> This is the heart of reproducibility. Every input must be pinned to an exact version and traceable to a controlled source — otherwise the build is not repeatable.
>
> Beginner note: the **Controlled?** column asks whether the input is under version / configuration control such that we can get *this exact version* back later. "Yes" means it is pinned via a lockfile, a tag, or a digest. "No" means it floats ("latest") — which is a reproducibility risk and must be flagged. The **Pin mechanism** names *how* the version is locked (the lockfile, tag, digest, or hash).

| Input | Type | Pinned version / digest | Source | Controlled? | Pin mechanism |
|---|---|---|---|---|---|
| {{Application source tree}} | source tree | {{git commit SHA / tag}} | {{repo}} | Yes | git tag / commit |
| {{Third-party library X}} | locked dependency | {{1.4.2}} | {{registry}} | Yes | lockfile |
| {{Base image / toolchain image}} | base image | {{sha256:...}} | {{registry}} | Yes | digest |
| {{Runtime config}} | config | {{config version / hash}} | {{config store}} | Yes | hash |
| {{Build script}} | build script | {{committed at SHA}} | {{repo path}} | Yes | git commit |
| {{Registry token}} | secret reference | {{n/a — referenced, not pinned}} | {{CI secret store}} | n/a | reference only |
| {{Some-tool@latest}} | locked dependency | {{FLOATING — "latest"}} | {{registry}} | **No — flag** | none yet |

(Type ∈ {source tree, locked dependency, base image, config, build script, secret reference}.)

**Pinning policy:**
- **No floating versions in a release build.** Any input marked "No" in the Controlled? column above must be pinned before a release build is permitted; record unresolved ones in §10.
- **Keeping lockfiles current:** {{Describe how dependency lockfiles are regenerated and reviewed — e.g. "the lockfile is regenerated only on a dedicated dependency-update change, reviewed, and committed; routine builds never regenerate it."}}

**Baseline linkage:** The complete set of inputs above is what §9 (Configuration Management) captures as part of a baseline, so that the exact input set for any past build can be recovered.

---

## 5. Build Procedure

> This is the executable spine of the document: a numbered, ordered, literal sequence of steps that, run top to bottom on the §3 environment with the §4 inputs, produces the §6 outputs. No prose hand-waving — give the actual commands, or an actual reference to the script / CI job that runs them.
>
> Beginner note: each step is numbered STEP-N so it can be referenced from logs, from failure handling (§8), and from the CI configuration. An **idempotent** step is one that is safe to run again with the same result (e.g. "ensure the output directory exists"); a **destructive** step changes or removes state (e.g. "delete the previous build output"). A **clean build** starts from nothing (no leftover artifacts); an **incremental build** reuses prior outputs to go faster — useful locally, but a release build should always be clean so nothing stale leaks in.

Run the following steps in order on the §3 environment with the §4 inputs:

| Step | Action (command / script) | Produces | Success signal |
|---|---|---|---|
| STEP-1 | {{`<package-manager> install --frozen-lockfile`}} | {{resolved dependency tree}} | {{exits 0; lockfile unchanged}} |
| STEP-2 | {{`<build-tool> build --profile release`}} | {{primary artifact in OUTPUT_DIR}} | {{exits 0; artifact present}} |
| STEP-3 | {{`<packager> package`}} | {{distributable package / image}} | {{exits 0; package well-formed}} |
| STEP-4 | {{`<checksum-tool> sha256 <artifact> > <artifact>.sha256`}} | {{checksum file}} | {{checksum file written}} |
| STEP-5 | {{`<manifest-generator>`}} | {{build manifest}} | {{manifest lists all outputs}} |

**Per-step notes:**
- **Idempotent vs. destructive:** {{e.g. "STEP-1 is idempotent. STEP-2 is destructive in clean mode (it first removes OUTPUT_DIR). STEP-4–5 are idempotent."}}
- **Resumability:** {{Where the build can safely be resumed after a failure — e.g. "after a failure in STEP-3, re-run from STEP-3; STEP-1–2 outputs are still valid."}}
- **Clean vs. incremental:** {{State the default and when each applies — e.g. "Local developer builds default to incremental. CI and release builds always run clean (full removal of prior outputs before STEP-2)."}}

**CI mapping (single source of truth):** The CI pipeline ({{R5}}) is the automated executor of these same steps — STEP-1…STEP-N map one-to-one to the pipeline's build job. **Keep the two in sync:** when a step changes here, change the CI config in the same change, and vice versa. This document and the CI config describe the *same* procedure; neither is allowed to drift from the other.

---

## 6. Build Outputs

> This is the complete manifest of everything the build emits, where each lands, and its fingerprint — so a later stage can pick up exactly the right artifact and confirm it is intact.
>
> Beginner note: not every output is shippable. The **primary artifact** (and any packages/images) are what you ship or run; build logs and manifests are diagnostic byproducts. The **checksum** column records each output's fingerprint so a downstream stage can verify it byte-for-byte.

| Output | Type | Location / artifact store | Version / label | Checksum (algo) | Consumed by |
|---|---|---|---|---|---|
| {{app binary}} | primary artifact | {{OUTPUT_DIR/app}} | {{v0.1.0}} | {{sha256:...}} | test, release, deploy |
| {{distributable package}} | package | {{artifact store URL}} | {{v0.1.0}} | {{sha256:...}} | release |
| {{container image (if used)}} | container image | {{registry/repo:tag}} | {{v0.1.0}} | {{sha256:... (digest)}} | deploy |
| {{build log}} | build log | {{logs/build-<run>.log}} | {{run ID}} | {{sha256:...}} | failure triage (§8) |
| {{build manifest}} | manifest | {{OUTPUT_DIR/manifest.json}} | {{v0.1.0}} | {{sha256:...}} | configuration management (§9) |
| {{SBOM}} | SBOM | {{OUTPUT_DIR/sbom.json}} | {{v0.1.0}} | {{sha256:...}} | dependency / license audit (§7) |

(Type ∈ {primary artifact, package, container image, build log, manifest, SBOM}. "SBOM" = software bill of materials — a list of every component that went into the artifact.)

**Labeling / versioning:** {{How outputs are labeled — tie to the Version in the metadata block and to §9 baselining. E.g. "the version label is derived from the git tag at build time and stamped into the artifact, the manifest, and the checksum filenames, so all outputs of one build carry the same label."}}

**Storage and retention:** {{Where artifacts are stored and for how long — e.g. "release artifacts retained indefinitely in the artifact store; CI build logs retained 90 days; local builds not retained."}}

**Shippable vs. diagnostic:** The shippable outputs are {{the primary artifact and package/image}}; the rest ({{build log, manifest, SBOM}}) are diagnostic byproducts used for triage, audit, and configuration management, not for release.

**Checksums:** Recorded using {{SHA-256}}. Each checksum is written to {{a sidecar `.sha256` file next to the output and into the build manifest}}, so the value can be reconstructed and compared later (see §9 reproducibility evidence).

---

## 7. Build Verification

> These are the fast, automatic checks that confirm the build is plausibly good BEFORE it is handed downstream. This is the build's own quality gate — distinct from the full test campaign, which lives in the Test Plan (cross-reference it; do not duplicate it here).
>
> Beginner note: a **blocking** check rejects the build if it fails (the artifact does not proceed). An **advisory** check reports a problem but does not stop the build (someone decides whether it matters). Decide each check's status deliberately — making everything blocking can stall the build on noise; making nothing blocking lets broken artifacts through.

| Check | Type | What it confirms | Pass criterion | Blocking? |
|---|---|---|---|---|
| {{Smoke test}} | smoke test | artifact launches / responds / reports version | {{`app --version` exits 0 and prints expected version}} | Yes |
| {{Static analysis & lint}} | static check | source has no flagged defects / style violations | {{linter exits 0, no errors}} | {{Yes / advisory}} |
| {{Dependency / vulnerability scan}} | security check | no known-vulnerable pinned dependencies | {{no findings at/above {{severity}}}} | {{Yes / advisory}} |
| {{License check}} | compliance check | all dependencies have allowed licenses | {{no disallowed licenses in SBOM}} | {{Yes / advisory}} |
| {{Packaging / integrity check}} | packaging check | artifact is well-formed and checksum matches | {{package validates; recomputed checksum == recorded}} | Yes |
| {{Reproducibility check}} | reproducibility check | a second clean build yields identical outputs | {{checksums of re-built outputs match}} | {{only if reproducibility goal is bit-for-bit; else advisory}} |

**Blocking policy:** {{State which checks reject the build. E.g. "Smoke test and packaging/integrity check are blocking — a failure stops promotion. Static analysis and license checks are blocking on a release build, advisory on a developer build. The reproducibility check is advisory until the reproducibility goal is raised to bit-for-bit (see §10)."}}

**CI gating:** In CI, these checks run as gates on the §5 build step — the build is not considered successful, and outputs are not promoted, until the blocking checks pass.

**Results reporting:** {{Where verification results are reported — e.g. "results are summarized in the CI run output and attached to the build manifest; failures are surfaced per §8."}}

**Relationship to full testing:** This section is *not* the test campaign. Functional, integration, and acceptance testing are specified in the Test Plan ({{04_Testing_and_VV}}); this section only confirms the build is intact enough to hand to that campaign.

---

## 8. Build Failure Handling

> Builds will fail; this section says what happens automatically and who does what, so a failure is a defined process rather than a panic. This is where the build plan meets operational reality.
>
> Beginner note: **triage** is the disciplined first look at a failure — figuring out *what category* the failure is before diving into fixes. The cheapest things to check first are environmental: what changed, what else is running, what input floated. A **rollback** here means a failed build must never replace a known-good artifact or baseline; promotion happens only after verification (§7) passes.

**Logs.** Build logs are written to {{logs/build-<run>.log}} (see §6). Each log entry is tagged with the STEP-N it belongs to, so a failure points directly at the failing step in §5. To read a failure: {{find the first failing STEP-N, read its log section, then check that step's inputs (§4) and environment (§3).}}

**Notifications.** {{Who / what is alerted and via what channel — e.g. "CI posts a failure summary to {{channel}} naming the failing STEP-N and the first error."}} Following the house principle that the system mediates user-facing surfaces, **raw build stderr is not dumped at the user** — it is translated into a clear, plain-language failure message ("the build failed at STEP-3 while packaging; the most likely cause is an unpinned dependency that changed") with the raw log available on demand for whoever debugs it.

**Triage order (check the environment first, before reading source):**
1. **What changed?** Compare inputs (§4) and environment (§3) against the last good build — a floated dependency or a tool-version bump is the most common cause.
2. **What else is running / interfering?** {{e.g. another build on the same runner, a stale cache, a held lockfile.}}
3. **Which STEP-N failed,** and is its failure consistent with #1 or #2?
4. **Only then** read the source / build script for the failing step.

**Retry / rebuild rules:**
- **Safe automatic retry:** {{transient failures only — e.g. network timeout pulling a dependency. Retry up to {{N}} times.}}
- **Clean rebuild required:** {{when partial/corrupt state is suspected — e.g. an interrupted STEP-2. Discard outputs and re-run from STEP-1.}}
- **No retry — fail fast:** {{deterministic failures — a compile error, a failed blocking check. Do not retry; fix the cause.}}

**Rollback / promotion guard:** A failed build **must not** replace a known-good artifact or baseline. The previous good artifact remains the current one until a new build passes §7 verification. Promotion to the next stage happens *only* after all blocking checks pass.

**Quick reference:**

| Failure class | Likely cause | First action |
|---|---|---|
| Dependency fetch failure | network / registry down; unpinned version moved | check §4 Controlled? column; retry if transient |
| Compile / build error | source change; tool-version mismatch | check what changed in source and §3 tool versions |
| Packaging failure | misconfigured packager; missing input | check STEP-3 inputs and config |
| Verification gate failure | smoke/static/security check failed | read the failing check in §7; do not promote |
| Non-reproducible output | floated input; non-deterministic tool | check §4 for unpinned inputs |

---

## 9. Configuration Management

> This is how a specific build is frozen, named, and stored so it can be returned to exactly — the difference between "we think this is what we shipped" and "here is the labeled baseline, byte-for-byte." It is the ISO/IEC/IEEE 12207 configuration-management touchpoint for the build.
>
> Beginner note: a **baseline** is a named, frozen snapshot you can recover exactly. For a build, the baseline is the *pinned input set* (§4) + the *outputs* (§6) + the *version of this plan* that produced them, captured together. **Labeling** is attaching a human-readable version (often a tag) to those outputs so they can be tracked through later stages.

**Labeling / versioning scheme.** {{How the metadata-block Version is derived and applied — e.g. "the version is taken from the git tag (e.g. `v0.1.0`); the build stamps that label onto every output in §6 and records it in the manifest, so all outputs of one build share one label."}}

**Baselining.** A baseline for a given build comprises, captured together:
- the pinned input set from §4 (with each input's Controlled? status and Pin mechanism),
- the outputs from §6 (with their recorded checksums), and
- the version of this Build Plan that governed the build.

These three together define the baseline. Cross-reference: the CI ID column in §2 identifies the configuration items, and the Controlled? column in §4 records that each input is recoverable.

**Archival / retention.** {{Where baselines and build logs are kept and for how long — e.g. "baselines (manifest + checksums + input pins) are stored in {{store}} indefinitely for released versions; build logs retained {{90 days}}."}}

**Reproducibility evidence.** To re-run a past baseline and confirm identical outputs:
1. Recover the exact inputs from the baseline's pinned input set (§4).
2. Recreate the §3 environment at its pinned versions.
3. Run the §5 procedure.
4. Recompute checksums of the new outputs and compare to the baseline's recorded checksums.
{{State the expected result given the reproducibility goal — e.g. "Under the pinned-inputs goal, the input set and tool versions match exactly; checksum equality is expected for deterministic outputs and is the bit-for-bit goal at the release stage."}}

**Signed baselines (if applicable).** {{If the project signs commits / tags, note it here — e.g. "release baselines are tied to a signed git tag; the signature is part of the baseline's provenance."}} If signing is not used, state: {{"baselines are not cryptographically signed in v1."}}

---

## 10. Open Questions

> Unresolved build decisions are tracked here rather than lost in chat. Resolve and remove them as work progresses.
>
> Beginner note: split open questions into two kinds. **Deferred with defaults** have a working default the build currently uses but may revisit. **Load-bearing / unresolved** genuinely block or risk the build and need a decision.

### 10.1 Deferred with defaults

- **OQ-DEF-1** {{Question}} — *default: {{the default the build currently uses}}.* {{e.g. "Reproducibility goal is best-effort (pinned inputs), not bit-for-bit. Default acceptable until the release stage; revisit before first release."}}
- **OQ-DEF-2** {{Question}} — *default: {{default}}.*
- ...

### 10.2 Load-bearing / unresolved

- **OQ-1** {{Question}} — {{what is blocking, and who / what must decide. e.g. "Dependency {{X}} is still floating ('latest') — must be pinned before any release build. Owner: {{role}}."}}
- **OQ-2** {{Question}} — {{e.g. "Secret-delivery mechanism for {{REGISTRY_TOKEN}} in CI is not yet decided. Blocking the first CI build. Owner: {{role}}."}}
- ...

---

## 11. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §3 Build Environment
- §4 Build Inputs
- §5 Build Procedure
- §6 Build Outputs
- §11 Revision History

**Optional sections** (include if relevant):
- §2 Build Scope (fold into §4 for a single-component build with no separate inventory)
- §7 Build Verification (keep at least a smoke-test row; expand as checks are added)
- §8 Build Failure Handling (a one-off manual build can keep this to the triage-order list)
- §9 Configuration Management (omit baselining detail for a throwaway local build; required for any release build)
- §10 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- BLD-N: the document and document-level statements (e.g. BLD-{{SYSTEM-ID}}-001)
- STEP-N: individual build steps in §5, referenceable from logs, failure-handling rules, and CI configuration
- CI-NNN: configuration items in §2 (configuration-management identifiers; the "CI ID" column)
- OQ-N / OQ-DEF-N: open questions (load-bearing / deferred-with-defaults)

These prefixes enable cross-document traceability — a step (STEP-N) referenced from a CI log or a §8 failure rule points back to one place; an SRS requirement or SDD component traces forward into the inputs (§4) and outputs (§6) this build assembles.

**Tailoring**:
- The 12207 construction/integration process and CI practice are guidance, not requirements. Add/remove subsections as the project needs; keep the spine (§3 environment, §4 inputs, §5 procedure, §6 outputs).
- **Single source of truth:** if the build runs in CI, the CI config and §5 describe the same procedure — change them together, never let them drift.
- **Solo developer / small-team collapse:** for a solo project, the Build Plan can shrink to §3 (environment), §4 (inputs), §5 (procedure), §6 (outputs), and a smoke-test row in §7 — written as a single page. The sign-off block in the metadata table collapses to one name in all three rows (Prepared / Reviewed / Approved by the same person). §2 (scope inventory) and §9 (baselining) can be deferred until there is more than one component or the first release, but the moment a build produces something you ship to someone else, fill in §6 checksums and §9 labeling so you can prove what you shipped.
- Keep the plan executable: prefer real commands and a reference to the script/CI job over prose descriptions of what the build "should" do.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 12207:2017, not this lightweight version. This template was built to the standard's publicly-described construction and integration process structure and does not reproduce its normative text; verify section coverage against the purchased standard for enterprise, regulated, or safety-critical contexts. The continuous-integration portions follow widely-held industry practice and name no single normative standard.
