# Version Description Document Template

> **Template purpose:** Lightweight Version Description Document (VDD) structure inspired by IEEE 828-2012. A VDD is a *release record* — it answers, for one specific build, "exactly what is in this version, and what changed since the last one." Use this template each time you cut a release. Replace `{{placeholder}}` content with release-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Whenever you ship a release — a build handed to users, a tagged version pushed to production, an internal cut frozen for testing. Unlike the SRS (what the system *should* do) or the SDD (*how* the design realizes it), a VDD is a snapshot tied to a single version. You create a new VDD (or a new revision entry) for each release, so anyone receiving the build can verify exactly what they got, what changed, and what is still broken.
>
> **Companion standard:** IEEE 828-2012 — Standard for Configuration Management in Systems and Software Engineering (the version-description / release-record practice). IEEE 828-2012 is the recognized companion for software configuration management and version description; some organizations also reference the older IEEE 1042 / MIL-STD-style VDD outline — IEEE 828-2012 is the current normative anchor used here.
>
> **Status of this template:** Lightweight, public, reusable extract following IEEE 828-2012 (Configuration Management in Systems and Software Engineering), reduced for solo/small-team use. It is faithful to the version-description / release-record practice but is NOT a reproduction of the standard's text — IEEE 828-2012 is a paywalled standard; this template was authored from the documented structure and common VDD practice, not copied from the standard. Verify against the full IEEE 828-2012 (and your organization's CM plan) for enterprise, regulated, or safety-critical contexts. Companion templates in this pack: the SRS skeleton at `docs/templates/01_Requirements/`, the SDD at `docs/templates/02_Design/`, and the Configuration Management Plan alongside this file at `docs/templates/05_Configuration_Management/`.

---

# Version Description Document (VDD) — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | VDD-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 828-2012 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Version Described | {{e.g. 2.3.0}} — the product/release version this VDD documents (distinct from the VDD's own document Version field above) |
| Build ID | {{commit hash / CI build number / build tag}} |
| Baseline | {{baseline name this release establishes or builds on}} |
| Repository Tag | {{e.g. v2.3.0}} |
| Release Date | {{YYYY-MM-DD}} |
| Release Type | {{Major / Minor / Patch / Hotfix / Pre-release}} |
| Supersedes | {{prior version this release replaces, or 'none'}} |

> **Note on the two "Version" fields above.** The **Version** row is the version of *this document* (it starts at `0.1 (draft)` and bumps as you edit the VDD). The **Version Described** row is the version of the *product* the document is about (e.g. `2.3.0`). They move independently — see §11 for why this distinction matters.

---

## 1. Introduction

> A VDD describes **one specific release**, not the system in general. Where the SRS and SDD are forward-looking ("here is what we will build and how"), this document is backward-looking and frozen: "here is exactly what we shipped in version {{X}}." This section sets up that framing and folds in the standard housekeeping — purpose, scope, definitions, and references — so the rest of the document reads cleanly.

### 1.1 Purpose

> One paragraph. State plainly that this document is the authoritative record of a single release, and how it differs from the SRS/SDD.

This document describes the exact contents of, and changes in, version **{{Version Described}}** of **{{Project Name}}**; it is the authoritative record of what was released.

> *Beginner note:* A **Version Description Document (VDD)** is the release counterpart to the SRS and SDD. The SRS says what the system *should* do; the SDD says *how* the design meets those requirements; this VDD says what was *actually shipped* in one named version. If a teammate, an auditor, or future-you needs to know "what exactly was in release {{Version Described}}, and how is it different from the one before," this is the document that answers — without forcing them to read the source history.

### 1.2 Scope

> State which release this VDD covers, and make clear it does not re-document the whole system. Point readers to the SRS/SDD for the full picture.

This VDD covers release **{{Version Described}}** ({{Build ID}}, tag `{{Repository Tag}}`) of {{Project Name}}, released {{Release Date}}.

It does **not** redocument the whole system. For the complete requirements see the SRS (`SRS-{{PROJECT-ID}}-001`); for the design see the SDD (`SDD-{{MODULE-ID}}-001`). This document is limited to: the inventory of what is in this build, the changes since the prior baseline, the defects this version resolves, the problems it still has, and the steps to install, verify, and (if needed) roll back this specific release.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define the terms a reader needs before the rest of the document makes sense. Seeded below with the core release-record vocabulary; add project-specific terms as needed.

| Term | Definition |
|---|---|
| Version Description Document (VDD) | A release-record document describing the exact contents of, and changes in, one specific build of a product. |
| Configuration item (CI) | Any discrete, individually versioned, individually identifiable thing that makes up the release — a binary, a library, a config file, a data set, a document. The §3 Contents table is a list of CIs. |
| Configuration management (CM) | The discipline of knowing exactly which version of each CI is in a given release, and how to reproduce that state. |
| Baseline | A formally agreed, named snapshot of all CIs at a point in time, used as the reference point you measure change against (e.g. "release {{Version Described}} builds on baseline {{prior baseline}}"). A baseline is what makes "what changed?" a well-defined question. |
| Build ID | The exact, reproducible identifier of the artifact that was produced (a commit hash, CI pipeline build number, or timestamped tag). Distinct from Version — two builds can share a Version but differ in Build ID; the Build ID is what uniquely pins the bits. |
| Checksum / hash | A short fingerprint (e.g. an SHA-256 string) computed from a file's exact bytes. If two people compute the same checksum for a file, they have the byte-for-byte same file. |
| Repository tag | A named, immovable label on the exact source-control snapshot the release was built from (e.g. the git tag `v{{Version Described}}`). The bridge from the shipped artifact back to its source. |
| Rollback | The rehearsed procedure to return to the previous working version if this release fails after deployment. |
| {{Term}} | {{Definition}} |

### 1.4 References

> List the documents this release record points back to. Categorized for readability. A VDD always cites the *prior version's VDD* — that is the previous baseline you measure this release's changes against.

| Ref | Document |
|---|---|
| R1 | `SRS-{{PROJECT-ID}}-001` — Software Requirements Specification (what the system must do) |
| R2 | `SDD-{{MODULE-ID}}-001` — Software Design Description (how the design realizes it) |
| R3 | `VDD-{{PROJECT-ID}}-001` (prior revision, version {{prior version}}) — the previous release record; the **baseline this release's changes are measured against** |
| R4 | `SCMP-{{PROJECT-ID}}-001` — Configuration Management Plan (how items, changes, and baselines are controlled) |
| R5 | {{Change / defect tracker — URL or system name}} — source of the CHG-N / DEF-N IDs used below |
| R6 | IEEE 828-2012 — Standard for Configuration Management in Systems and Software Engineering |
| ... | ... |

---

## 2. Version Identification

> This section answers "precisely which artifact is this, and how do I pin it?" An ambiguous version identity defeats the whole purpose of the document, so this table must be filled in **completely** — every row, no blanks. The header metadata table above carries the same facts for quick reference; this is the authoritative, fully-populated version.

> *Beginner note:* **Version** is the human-facing release name (e.g. `2.3.0`) — what people say out loud. **Build ID** is the exact, reproducible identifier of the bits that were produced (a commit hash, a CI build number, a timestamped tag). Two builds can carry the same Version yet differ in Build ID, so the Build ID is what truly pins "these exact bytes." The **Repository Tag** is the bridge back to source: the immovable label on the source-control snapshot the build came from. If someone has the tag, they can rebuild from the same source.

| Field | Value |
|---|---|
| Product Name | {{Project Name}} |
| Version | {{Version Described — e.g. 2.3.0}} |
| Build ID | {{commit hash / CI build number / build tag}} |
| Release Date | {{YYYY-MM-DD}} |
| Baseline | {{baseline name this release establishes — e.g. "baseline 2.3", built on baseline 2.2}} |
| Repository Tag | {{e.g. v2.3.0}} |
| Release Type | {{Major / Minor / Patch / Hotfix / Pre-release}} |
| Supersedes | {{prior version this release replaces — e.g. 2.2.4 — or 'none'}} |
| Distribution | {{where/how the artifact is published — release page URL, registry, package name, internal share path}} |

---

## 3. Inventory of Contents

> This is the **bill of materials** for the release: a list of every configuration item (CI) shipped in this build. Each row is one individually versioned thing. If a CI is not on this list, it was not (officially) part of this release.

> *Beginner note:* A **configuration item (CI)** is any discrete, individually versioned artifact — a compiled binary, a library, a config file, a bundled data set, a document. **Checksums** matter here: a checksum (e.g. an SHA-256 hash) is a short fingerprint of a file's exact bytes. By recording it, you let a recipient verify they received the intended, untampered file — if their computed checksum matches yours, the file is byte-for-byte identical. Remember that **installer/media artifacts, third-party dependencies pinned at specific versions, and bundled data sets all count as CIs** and belong in this table.

| CI-ID | Item | Version | Location/Path | Checksum | Notes |
|---|---|---|---|---|---|
| CI-1 | {{e.g. miraos-cli (binary)}} | {{2.3.0}} | {{dist/miraos-cli}} | {{sha256:abc123...}} | {{primary artifact}} |
| CI-2 | {{e.g. miraos-core (library)}} | {{2.3.0}} | {{lib/miraos_core.so}} | {{sha256:def456...}} | {{}} |
| CI-3 | {{e.g. default config}} | {{2.3.0}} | {{conf/default.yaml}} | {{sha256:789aaa...}} | {{ships with installer}} |
| CI-4 | {{third-party dependency, pinned}} | {{1.4.2}} | {{vendor/{{lib}}}} | {{sha256:bbb222...}} | {{pinned; see §8 Compatibility}} |
| CI-5 | {{bundled data set}} | {{2026-05-01}} | {{data/seed.db}} | {{sha256:ccc333...}} | {{}} |
| ... | ... | ... | ... | ... | ... |

---

## 4. Changes in This Version

> This is the human-readable "what changed since the last release," and it is the most-read part of any VDD. Changes are measured against the **prior baseline named in §2**. Keep each entry one change, with a clear type and a trace to *why* it changed.

> *Beginner note:* Each change should trace to a requirement (from the SRS) or a defect (a `DEF-N` in §5) so a reader can see *why* it changed, not just *that* it did. Pay special attention to the **Breaking** type: a breaking change is one that stops working with something that used to work (old data, an old client, an old interface). Flagging breaking changes explicitly here is what protects downstream users from upgrade surprises — and every breaking change flagged here must have a matching warning in §8 Compatibility.

| CHG-ID | Summary | Type | Affected CI(s) | Linked Requirement/Defect | Status |
|---|---|---|---|---|---|
| CHG-1 | {{Add {{feature}} to {{component}}}} | Feature | CI-1, CI-2 | {{SRS §3.2 / REQ-12}} | Done |
| CHG-2 | {{Improve {{throughput}} of {{operation}}}} | Enhancement | CI-2 | {{SRS §4.1}} | Done |
| CHG-3 | {{Fix {{bug}} in {{path}}}} | Fix | CI-1 | DEF-1 | Done |
| CHG-4 | {{Internal cleanup of {{module}}}} | Refactor | CI-2 | — | Done |
| CHG-5 | {{Patch {{vulnerability}}}} | Security | CI-4 | DEF-2 | Done |
| CHG-6 | {{Rename {{config key}} (old key no longer read)}} | Breaking | CI-3 | {{SRS §3.4}} | Done — see §8 |
| ... | ... | ... | ... | ... | ... |

*Type values:* Feature / Enhancement / Fix / Refactor / Security / Breaking.

---

## 5. Defects Resolved

> The bugs this version fixes, recorded so a stakeholder can confirm a problem they reported is actually addressed in this release.

> *Beginner note:* "Resolved" here means **fixed and verified in this release** — stronger than merely "closed" in a tracker, which can happen for many reasons (duplicate, won't-fix, can't-reproduce). What makes a resolution claim *trustworthy* rather than aspirational is the trace: each defect links to the change that fixed it (`CHG-N`) and to the evidence that verifies the fix (a test ID or method). Use the **same severity scale as your project's defect tracker** — do not invent a new one here; note which scale you are using.

*Severity scale used:* {{name the tracker's scale, e.g. Blocker / Critical / Major / Minor / Trivial}}.

| DEF-ID | Summary | Severity | Affected CI(s) | Resolved by (CHG-N) | Verification (test ID / method) |
|---|---|---|---|---|---|
| DEF-1 | {{Crash when {{condition}}}} | {{Critical}} | CI-1 | CHG-3 | {{TEST-104 (automated regression)}} |
| DEF-2 | {{{{Dependency}} CVE-{{YYYY-NNNN}}}} | {{Major}} | CI-4 | CHG-5 | {{dependency scan; TEST-220}} |
| DEF-3 | {{Incorrect {{output}} for {{input}}}} | {{Minor}} | CI-2 | {{CHG-N}} | {{TEST-031; manual confirm by {{role}}}} |
| ... | ... | ... | ... | ... | ... |

---

## 6. Known Problems and Limitations

> This is where you tell the reader, honestly, what is still broken or constrained in **this** version — before they deploy. A mature VDD is candid here: hiding a known issue erodes trust and turns a documented limitation into a field surprise.

> *Beginner note:* Distinguish a **defect** (unintended — something that should work doesn't) from a **limitation** (intended — a deliberate boundary of the current scope, e.g. "only supports English locales in this version"). Both belong here if they affect the reader. Also record **deferred items**: changes that were in the planned change set but did *not* make this release land here too, so nobody assumes they shipped.

| KP-ID | Description | Severity/Impact | Workaround | Planned Resolution |
|---|---|---|---|---|
| KP-1 | {{{{Feature}} fails under {{rare condition}}}} | {{Minor — affects {{small subset}}}} | {{{{Restart / avoid X}}}} | {{target version 2.3.1}} |
| KP-2 | {{Only {{N}} of {{M}} formats supported (limitation)}} | {{Limitation — by design for this scope}} | {{convert to {{format}} first}} | {{2.4.0, if prioritized}} |
| KP-3 | {{Deferred: {{change}} pulled from this release}} | {{Impact: {{capability}} not yet available}} | {{none}} | {{next release}} |
| ... | ... | ... | ... | ... |

---

## 7. Installation, Deployment, and Rollback

> The operational steps to put this release into service — **and** to back it out if it fails. The rollback subsection is not optional padding: documenting the undo path *before* release is what turns a failed deploy from a 2 a.m. emergency into a known, rehearsed step.

> *Beginner note:* **Rollback** is the procedure to return to the previous working version after a failed deployment. Some upgrades change data on disk (a "migration") in ways that cannot simply be reversed — in those cases rollback is not "clean" and requires restoring data from a backup. Call this out explicitly in §7.4 so an operator knows, before they start, whether undo is easy or requires a restore.

### 7.1 Prerequisites

> What must be true before installing: platform/OS, runtime versions, accounts/permissions, and which prior baseline (if any) must already be in place.

- Platform / OS: {{e.g. Linux x86-64, kernel ≥ {{version}}}}
- Runtime / dependencies: {{e.g. {{runtime}} ≥ {{version}}; see §8 for the full compatibility matrix}}
- Accounts / permissions: {{e.g. {{service account}} with {{rights}}}}
- Prior baseline required: {{e.g. must be on 2.2.x before upgrading; or "clean install supported"}}

### 7.2 Installation / Upgrade Steps

> The ordered steps to install fresh or upgrade from the prior version. Be concrete enough to follow without guessing.

1. {{Back up {{data/config}} (see §7.4 for why this is required before upgrade)}}
2. {{Stop {{service}} / put system in maintenance mode}}
3. {{Install artifact CI-1 from {{Distribution}} (verify checksum against §3)}}
4. {{Run migration step (see §7.3)}}
5. {{Start {{service}}; confirm health check {{passes}}}}

### 7.3 Configuration and Migration

> Any configuration changes this release requires, and any data/schema migration it performs. Note whether migrations run automatically or must be invoked.

- Configuration changes: {{e.g. config key {{old}} renamed to {{new}} — see CHG-6; update before start}}
- Data / schema migration: {{e.g. runs automatically on first start; migrates schema {{v5 → v6}}}}
- Migration reversibility: {{e.g. **irreversible** once run — rollback requires data restore; or "reversible via {{down-migration}}"}}

### 7.4 Rollback Procedure

> The steps to return to the prior working version if this release fails. State clearly whether rollback is clean (just reinstall the old artifact) or requires restoring data.

- Rollback type: {{**Clean** (reinstall prior artifact, no data restore needed) / **Requires data restore** (the migration in §7.3 is irreversible)}}
- Steps:
  1. {{Stop {{service}}}}
  2. {{Reinstall prior artifact (version {{Supersedes}})}}
  3. {{If migration was irreversible: restore {{data}} from the backup taken in §7.2 step 1}}
  4. {{Start {{service}}; confirm health check passes}}
- Tested? {{e.g. rollback rehearsed on {{staging}} on {{YYYY-MM-DD}} — see §9}}

---

## 8. Compatibility

> What this release does and does not work with — platforms, dependencies, interfaces, and data formats. Every **Breaking** change flagged in §4 must have a corresponding warning here, so the two sections can never disagree.

> *Beginner note:* **Backward-compatible** means this version still works with things built for older versions — old data files, old client software, old interface callers. A **breaking change** means it does not (the old thing must be migrated or updated). **Forward-compatible** (rarer) means older versions can still tolerate data or messages produced by this newer one. State each honestly so an upgrade never surprises anyone.

| Aspect | This Release | Notes |
|---|---|---|
| Supported platforms / OS | {{e.g. Linux x86-64, macOS 13+}} | {{dropped {{platform}} this release — see §4 CHG-N}} |
| Runtime versions | {{e.g. {{runtime}} 3.10–3.13}} | {{}} |
| Required dependency versions | {{CI-4 at ≥ 1.4.2}} | {{links to §3 CI rows}} |
| Interface / API compatibility | {{Backward-compatible with 2.2.x callers / **Breaking**: {{endpoint}} removed}} | {{breaking item maps to §4 CHG-6}} |
| Data / file-format compatibility | {{Reads 2.2.x data after migration; old format no longer written}} | {{see §7.3 migration}} |

**Breaking-change warnings** (mirror of §4 entries typed `Breaking`):
- {{CHG-6 — config key {{old}} renamed; deployments using the old key will fail to start. Update config per §7.3 before upgrading.}}
- ...

---

## 9. Verification Summary

> The evidence that this release was actually tested and accepted — enough for a reader to judge how much to trust it *without* re-running everything. Summarize and point to the full test report; do not reproduce it here.

> *Beginner note:* **Verification** asks "did we build it right?" — do the tests pass, does it meet the spec. **Acceptance** (also called validation) asks "did we build the right thing?" — does a stakeholder agree it actually meets the need. A trustworthy release usually has both: green tests *and* a named person who accepted it against stated criteria.

| Aspect | Summary |
|---|---|
| Test scope executed | {{Unit / Integration / System / Acceptance — which ran for this release}} |
| Pass/fail summary | {{e.g. 412 / 415 passing; 3 known-fail tied to KP-1}} |
| Coverage (if measured) | {{e.g. 78% line coverage; or "not measured"}} |
| Environments tested | {{e.g. staging on {{platform}}; {{matrix}}}} |
| Outstanding / known test gaps | {{e.g. load test deferred — see OQ-1}} |
| Full test report | {{path / URL — the authoritative detail this section summarizes}} |
| Acceptance sign-off | {{accepted by {{role}} on {{YYYY-MM-DD}} against {{acceptance criteria / SRS §5}}}} |

---

## 10. Open Questions

> Release-time questions still unresolved — things that did **not** block the release but need follow-up.

> *Beginner note:* An **open question** is something *undecided* — distinct from a *known problem* (§6), which is decided-but-broken. Open questions typically migrate into the next release: they become a change in §4 of the next VDD, or a defect (`DEF-N`) once they turn out to be bugs. Record what is blocking each one and who decides.

- **OQ-1**: {{question}} — {{what's blocking resolution; who decides}}
- **OQ-2**: {{question}} — {{blocker; owner}}
- ...

---

## 11. Revision History

> Every substantive edit to **this document** gets a row.

> *Beginner note:* A point unique to a VDD: this table tracks revisions to the **document**, which is distinct from the **product version** the document describes (recorded in §2). A VDD can be revised *without* the product changing — for example, if a known problem is discovered after release and added to §6, the document goes from 0.2 → 0.3 while the described product is still {{Version Described}}. Bump this table when you edit the VDD; do not confuse it with re-releasing the product.

| Version | Date | Author | Changes | Approval |
|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft | {{pending}} |
| ... | ... | ... | ... | ... |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Version Identification (must be filled completely — an ambiguous version identity defeats the document)
- §3 Inventory of Contents
- §4 Changes in This Version
- §11 Revision History

**Optional sections** (include if relevant):
- §5 Defects Resolved (omit only if the release fixes nothing — rare; usually at least list "none")
- §6 Known Problems and Limitations (strongly recommended — candor here is what makes the release trustworthy; state "none known" rather than deleting it)
- §7 Installation, Deployment, and Rollback (omit only for releases with no deployment step, e.g. a pure library publish; keep §7.4 wherever a deploy can fail)
- §8 Compatibility (omit if nothing external depends on the release; required whenever §4 contains a `Breaking` change)
- §9 Verification Summary (defer only for throwaway pre-releases; include for anything reaching real users)
- §10 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (carry these through so a reader can trace a shipped item to the change that produced it and the defect it resolved, and so sibling documents can cite a specific release's contents):
- CI-N: configuration items / contents shipped in this version (§3)
- CHG-N: changes included in this version (§4)
- DEF-N: defects resolved (§5) — carried through from the defect tracker, not re-invented
- KP-N: known problems / limitations (§6)
- OQ-N: open questions (§10)

The trace chain reads: a shipped item (**CI-N**) ← the change that produced it (**CHG-N**) ← the defect it resolved (**DEF-N**) ← the verification that proves it (test ID in §5/§9). Other documents (SRS, SDD, the next VDD) can cite `VDD-{{PROJECT-ID}}-001 §3` to reference exactly what a given release contained.

**Tailoring**:
- A VDD is per-release. The simplest workflow keeps one `VDD-{{PROJECT-ID}}-001` document and adds a Revision History row + updates §2–§9 each release; larger projects mint a new VDD per version. Either is fine — pick one and be consistent.
- **Solo developer / small team collapse:** you can fold this down hard. The irreducible core is §2 (which exact build is this), §3 (what's in it — at minimum the primary artifact + its checksum), and §4 (what changed since last time). A generated changelog and a tagged release with checksums can satisfy §3–§4 directly; §5–§6 can be a short honest list; §7 can be a few lines if deployment is `git pull && restart`. Keep §11 Revision History always. The goal is "future-you can answer *what did I ship, and what changed* in under a minute," not ceremony.
- Section organization follows IEEE 828-2012's version-description practice but is plain-English and reduced; add or drop subsections as your release process needs.
- Revision history is mandatory. Remember it tracks the *document*, not the product version (§11).

**For regulated/safety-critical projects:** use the full IEEE 828-2012, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
