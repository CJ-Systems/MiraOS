# Configuration Management Plan Template

> **Template purpose:** Lightweight Configuration Management Plan (SCMP) structure inspired by IEEE 828-2012. Use this template when you need to write down how a project tracks what's under version control, how changes get proposed and approved, and how releases are frozen and recorded. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once a project has more than a handful of files worth controlling — source, specs, configs, release artifacts — and you want a single document that says "here is what we track, here is how we change it, here is how we know what state we're in." Especially useful for solo or small-team projects that have outgrown ad-hoc commit habits but don't want heavyweight process.
>
> **Companion standard:** IEEE 828-2012 — Standard for Configuration Management in Systems and Software Engineering.
>
> **Status of this template:** Lightweight, plain-English derivation inspired by the IEEE 828-2012 outline. It paraphrases the standard's section organization for solo/small-team use and does NOT reproduce normative text. Verify against the full standard for enterprise/regulated contexts.

---

# Configuration Management Plan — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | SCMP-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 828-2012 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Version control system | {{git / other}} |
| Repository | {{URL or path}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph stating what this document is for. Configuration Management (CM) is the discipline of keeping track of what files and artifacts make up the project, how they change over time, and how to reproduce any past state. This document records the project's CM approach so anyone (including future-you) can answer "what's under control, how do changes happen, and what state are we in right now?"

{{This document describes how {{Project Name}} manages its configuration: which items are placed under version control, how changes to those items are proposed and approved, how known-good reference points (baselines) are defined, and how the state of the project is tracked and audited.}}

### 1.2 Scope

> Define what this plan covers and what it does not. For a small project this is usually "everything in the repository plus released artifacts." Note anything deliberately excluded (e.g., local developer scratch files, generated build output that isn't tracked).

In scope:
- {{e.g., all source, specs, and configuration in the project repository}}
- {{e.g., tagged releases and their artifacts}}

Out of scope:
- {{e.g., transient build output regenerated from source}}
- {{e.g., personal/local config not shared with the team}}

### 1.3 Definitions and Acronyms

> Define CM terms plainly so a reader new to formal practice isn't lost. The three core ideas below are worth keeping verbatim — they are the vocabulary the rest of the document relies on.

| Term | Definition |
|---|---|
| Configuration Item (CI) | Anything placed under version control whose changes are tracked deliberately — a source file, a spec, a config file, a release artifact. The "things we keep an eye on." |
| Baseline | A known, frozen reference point: a specific state of the project everyone agrees on and can return to. In git, a baseline is typically a tagged release (e.g., `v1.0.0`). |
| Configuration control | The change-request process that governs how a CI is modified — how a change is proposed, reviewed, approved, and recorded. The "rules for changing the tracked things." |
| Status accounting | Keeping and reporting the record of what changed, when, by whom, and what state each item is in. |
| Configuration audit | A check that what was built/released actually matches the records (the right files, the right versions). |
| {{Other term}} | {{Definition}} |

### 1.4 References

> List the documents this plan depends on or relates to — the project's SRS/SDD, relevant ADRs, the external standard, and any contributing guidelines.

| Ref | Document |
|---|---|
| R1 | {{path/to/srs.md}} — requirements specification |
| R2 | {{path/to/sdd.md}} — design description |
| R3 | {{CONTRIBUTING.md / branching guide}} |
| R4 | IEEE 828-2012 — Configuration Management in Systems and Software Engineering |
| ... | ... |

---

## 2. CM Organization and Responsibilities

> Who is responsible for which CM activities? Large organizations split this across a CM manager, a Change Control Board (CCB), developers, and reviewers. For a **solo developer or small team, these roles collapse onto one or two people** — but it's still worth naming them, because the roles describe *activities* that happen regardless of how many people perform them. Write down who currently wears each hat; if it's all you, say so plainly.

| Role | Responsibility | Who holds it |
|---|---|---|
| CM owner | Maintains this plan; defines naming/tagging conventions | {{name / "the maintainer (solo)"}} |
| Change control authority | Approves or rejects proposed changes (the CCB, however small) | {{name / "the maintainer (solo)"}} |
| Contributor | Proposes changes via the agreed workflow | {{names / "anyone with repo access"}} |
| Reviewer | Reviews proposed changes before they're accepted | {{name / "self-review + CI for solo"}} |
| Release manager | Cuts and tags releases (baselines) | {{name}} |

> **Solo/small-team collapse:** {{e.g., "All roles are held by the maintainer. 'Approval' means the maintainer's own review plus passing CI before merge to the default branch. The plan is kept honest by the tooling (branch protection, required checks) rather than by separate people."}}

---

## 3. Configuration Identification

> This section answers "what exactly is under control, and how do we name and freeze it?" Identification is the foundation — you can't control or audit what you haven't first identified. Use **CI-N** identifiers so other documents (and this one) can refer to specific item classes.

### 3.1 Configuration Items

> List the classes of items under version control. You don't have to enumerate every file — group them sensibly (e.g., "all Markdown specs under `docs/`"). Each class gets a CI-N id.

| ID | Configuration item (class) | Location | Notes |
|---|---|---|---|
| CI-1 | {{Source code}} | {{`dna/` or `src/`}} | {{language, package layout}} |
| CI-2 | {{Specifications & docs}} | {{`docs/`}} | {{Markdown specs, ADRs}} |
| CI-3 | {{Build & config files}} | {{repo root}} | {{e.g., `pyproject.toml`, CI workflows}} |
| CI-4 | {{Release artifacts}} | {{tags / releases}} | {{what a release bundles}} |
| ... | ... | ... | ... |

### 3.2 Naming Conventions

> How are items, branches, and versions named so they're unambiguous and sortable? Consistency here is what makes status accounting and audits possible later.

- **Files / modules:** {{e.g., kebab-case Markdown; package-name for code modules}}
- **Branches:** {{e.g., `feature/<short-desc>`, `fix/<short-desc>`, `release/<version>` — a git-flow style scheme, or trunk-based with short-lived branches}}
- **Versions:** {{e.g., Semantic Versioning `MAJOR.MINOR.PATCH`}}
- **Tags:** {{e.g., `v1.2.0` annotated tags}}

### 3.3 Baselines

> A baseline is a frozen, named reference point. **In git, the natural baseline is an annotated, tagged release** — `git tag -a v1.0.0 -m "..."` marks an exact commit everyone can return to. Define what events create a baseline and what each baseline must satisfy before it's declared.

| Baseline | Definition | How it's created | Entry criteria |
|---|---|---|---|
| {{Release baseline}} | {{A shipped version}} | {{annotated git tag `vX.Y.Z` on the default branch}} | {{all checks green; CHANGELOG updated; version bumped}} |
| {{Milestone baseline}} | {{An internal checkpoint}} | {{tag or long-lived branch}} | {{criteria}} |
| ... | ... | ... | ... |

> **Note:** Once a baseline (tag) is published, treat it as immutable. Fixes happen as *new* commits and a *new* baseline, never by moving an existing tag.

---

## 4. Configuration Control

> This is the heart of the plan: the **change process**. Configuration control is the agreed procedure for modifying a CI — how a change is proposed, reviewed, approved, and recorded. The point is that changes to controlled items don't happen by accident or by direct edits to the baseline; they go through a known path. **In a git workflow, this maps cleanly onto branches and pull/merge requests.**

### 4.1 Change Process

> Describe the path a change takes from idea to accepted. Keep it as light as the project warrants — even "open a branch, open a PR, pass CI, merge" is a valid, real change-control process.

1. **Propose** — {{e.g., open an issue, or create a `feature/`/`fix/` branch off the default branch}}
2. **Develop** — {{make the change on the branch; commit with clear messages}}
3. **Review** — {{open a pull/merge request; self-review or peer review; CI runs}}
4. **Approve** — {{change control authority (see §2) approves; required checks pass}}
5. **Integrate** — {{merge to the default branch; delete the working branch}}
6. **Record** — {{the merge + PR are the record; update CHANGELOG / status accounting per §5}}

### 4.2 Change Control Authority

> Who has the authority to approve a change into a baseline? For a solo project this is you (plus the gate of passing CI). For a small team it might be "any maintainer" or "the area owner." State it explicitly so there's no ambiguity about who can say yes.

{{e.g., "Merges to `main`/`develop` require an approving review from a maintainer and all required CI checks passing. For the solo phase, the maintainer's own review plus green CI constitutes approval. Direct pushes to the default branch are disabled via branch protection."}}

### 4.3 Emergency / Hotfix Changes

> Sometimes a change can't wait for the normal path (a production-breaking bug). Describe the abbreviated path and how it gets reconciled with the normal process afterward.

{{e.g., "`hotfix/` branch off the latest release tag; expedited review; merged to both the release line and the default branch; a patch baseline `vX.Y.(Z+1)` is tagged immediately."}}

---

## 5. Configuration Status Accounting

> Status accounting is simply **keeping and reporting the record**: what items exist, what version each is at, what changes are open/approved/merged, and what's in each baseline. The goal is that at any moment you can answer "what's the current state, and how did we get here?" Most of this is *already produced for free by git* — the job is to point at it and add the small human-readable layer on top.

### 5.1 What We Track

| Information | Source / where it lives |
|---|---|
| History of every change | {{git commit history}} |
| Open / in-review changes | {{open pull requests, issue tracker}} |
| What's in each release | {{CHANGELOG, git tag annotations, release notes}} |
| Current version | {{version file / latest tag}} |
| Known open issues | {{issue tracker}} |

### 5.2 Reporting

> How and when is project state reported, and to whom? For a small project a maintained CHANGELOG plus the tag/release list may be the entire status-accounting report.

{{e.g., "A `CHANGELOG.md` follows Keep-a-Changelog format and is updated as part of every release baseline. `git log` and the releases page serve as the on-demand status report. No separate periodic report is produced at this scale."}}

---

## 6. Configuration Audits and Reviews

> An audit answers "does what we actually shipped match what the records say we shipped?" Two classic checks: a **functional** check (does the release do what the requirements/specs say) and a **physical** check (does the release contain exactly the right files at the right versions — the tag points at the commit it claims, the artifact was built from that commit). For a small project this can be a short release checklist rather than a formal audit.

### 6.1 Audit Types

| Audit | Question it answers | How performed |
|---|---|---|
| Functional | Does the baseline satisfy its requirements/specs? | {{run test suite; check acceptance criteria}} |
| Physical | Does the baseline contain the right items at the right versions? | {{verify tag → commit → built artifact chain; checksum artifacts}} |

### 6.2 Release Checklist

> A lightweight stand-in for formal audits. The list a maintainer walks before declaring a baseline.

- [ ] {{All tests pass on the commit being tagged}}
- [ ] {{Version number bumped and consistent across files}}
- [ ] {{CHANGELOG updated with the changes since the last baseline}}
- [ ] {{Tag is annotated and points at the reviewed commit on the default branch}}
- [ ] {{Released artifact builds reproducibly from the tagged commit}}
- [ ] {{...}}

---

## 7. Tools and Environment

> Name the concrete tools that implement the policy above. The plan stays useful only if it reflects the tools actually in use. Most modern small teams use git, so the examples below are git-flavored — adapt if your project differs.

### 7.1 Version Control System

{{e.g., "git, hosted at {{URL}}. Default branch: `main` (or `develop`). Branch protection enabled: no direct pushes, required passing checks, required review."}}

### 7.2 Branching Strategy

> Describe the branching model and link it back to the change process in §4.1. State it so contributors know where to branch from and merge to.

{{e.g., "Trunk-based: short-lived `feature/`/`fix/` branches off `main`, merged via PR, branch deleted on merge." OR "git-flow: `feature/` → `develop`, `release/` → `main` + `develop`, `hotfix/` → `main` + `develop`."}}

### 7.3 Release and Tagging Conventions

> How versions are assigned and how releases are frozen as baselines (ties to §3.3).

- **Versioning scheme:** {{Semantic Versioning}}
- **Tag format:** {{annotated `vX.Y.Z`}}
- **Release procedure:** {{e.g., "bump version → update CHANGELOG → merge release branch → `git tag -a vX.Y.Z` → push tag → publish release notes"}}
- **Signing (optional):** {{e.g., signed tags/commits, if used}}

---

## 8. Open Questions

> CM decisions still being resolved. Resolve and remove as the project matures.

- **OQ-1**: {{question}} — {{what's blocking, who needs to decide}}
- ...

---

## 9. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — the definitions especially)
- §3 Configuration Identification (you must know what's under control)
- §4 Configuration Control (the change process is the core of CM)
- §9 Revision History

**Optional sections** (include if relevant):
- §2 CM Organization (for a solo project this can be a single sentence in §4.2; expand as the team grows)
- §5 Configuration Status Accounting (omit the formal version if git history + CHANGELOG already serve; still worth one paragraph pointing at them)
- §6 Configuration Audits (a release checklist is enough for most small projects; full functional/physical audits are for regulated work)
- §7 Tools and Environment (omit only if documented elsewhere, e.g., a CONTRIBUTING guide — but link to it)
- §8 Open Questions (track elsewhere if you prefer)

**Identifier conventions**:
- CI-N: configuration items (classes of controlled items) — enables traceability from this plan to specific items and from other documents back to them
- OQ-N: open questions

**Tailoring**:
- The whole point of a lightweight SCMP is that the *tooling enforces the policy*. Prefer "branch protection requires review + green CI" over prose nobody reads. Write down what the tools already do.
- For a solo developer, most roles in §2 collapse to one person and most of §5 is "git already records this." That's fine — name it explicitly rather than pretending a board exists.
- Keep baselines = tagged releases. Don't invent a parallel freezing mechanism if git tags already do the job.

**For regulated/enterprise projects:** use the full IEEE 828-2012, not this lightweight version.
