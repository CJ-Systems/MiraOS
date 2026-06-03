# Migration Plan Template

> **Template purpose:** Lightweight Migration Plan structure following ISO/IEC/IEEE 14764:2022 (the software-maintenance standard's migration and software-retirement activities). Use this template to plan moving a system, its data, and its users from a current environment to a target one. Replace `{{placeholder}}` content with system-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Whenever you are moving an existing system — its software, its data, and the people who depend on it — from a current ("source") setup to a new ("target") one: a re-platform, a database swap, a cloud move, a major version jump, or retiring an old system in favor of a new one. Write this plan *before* you touch production. The plan is the controlled procedure; the migration is the execution of the plan.
>
> **Companion standard:** ISO/IEC/IEEE 14764:2022 — Software engineering — Software life cycle processes — Maintenance (migration and software retirement activities).
>
> **Status of this template:** A lightweight skeleton derived from public sources, following ISO/IEC/IEEE 14764:2022 (Software maintenance — migration and software retirement activities). It is original house-authored prose that follows the standard's section topics; it paraphrases the standard's structure and reproduces NO normative text. ISO/IEC/IEEE 14764:2022 is a paywalled standard — VERIFY this outline against the full standard before relying on it for regulated, contractual, or safety-critical migrations, as this lightweight extract may omit normative requirements.

---

# Migration Plan — {{System Name}}

| Field | Value |
|---|---|
| Document ID | MIG-{{SYSTEM-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 14764:2022 (lightweight) |
| Owner | {{Project name or owner}} |
| Source environment | {{Current system / version / platform being migrated FROM}} |
| Target environment | {{Destination system / version / platform being migrated TO}} |
| Migration strategy | {{Big-bang / Phased / Parallel-run / Pilot — name the chosen pattern}} |
| Planned cutover window | {{Date/time window, or 'TBD'}} |
| Rollback decision authority | {{Role/name with authority to trigger rollback}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> A **Migration Plan** is the controlled, written procedure for moving {{System Name}}, its data, and its users from a current environment to a target one. Under ISO/IEC/IEEE 14764:2022 — the standard that defines how software is *maintained* over its life — migration is a planned maintenance activity, not improvisation: you write the procedure first, get it reviewed, then execute it. This section orients any reader to why the document exists and what it covers, folding in the classic Purpose / Scope / Definitions / References preamble as numbered subsections.

### 1.1 Purpose

> One paragraph: state which migration this plan governs and what "success" concretely means. Make clear that once approved, this plan is the *authoritative* procedure — if reality diverges from it, you revise the plan (with a version bump), you don't quietly improvise around it.

{{This Migration Plan governs the migration of {{System Name}} from {{source environment}} to {{target environment}}. Success means {{define it concretely — e.g., "all production data migrated and reconciled, all acceptance criteria in §7 met, users working in the target system, and the source system safely decommissioned"}}. Once approved (see sign-off block above), this document is the authoritative procedure for the migration; any deviation is handled by revising this plan, not by undocumented ad-hoc changes.}}

### 1.2 Scope

> Define what this migration includes and — just as important — what it explicitly excludes. Name which systems, which data, and which users are in vs. out. Say whether this is a single-phase move or one phase of a larger multi-phase program. Vagueness here turns into argument at cutover.

**In scope:**
- {{System / subsystem being migrated, e.g., "the {{System Name}} application and its primary {{datastore}}"}}
- {{Data in scope, e.g., "all active customer records from {{date}} onward"}}
- {{Users in scope, e.g., "all {{role}} users in the {{region}} tenant"}}

**Explicitly out of scope:**
- {{Excluded system/data, e.g., "the legacy reporting warehouse — migrated separately under MIG-{{OTHER-ID}}-001"}}
- {{Excluded data, e.g., "archived records older than {{retention period}} — handled by §9 archival, not migrated live"}}
- {{Excluded users, e.g., "third-party API integrators — covered by §6 communications, not relocated"}}

**Phasing:** {{Single-phase / Phase {{N}} of a {{M}}-phase program — name the relationship to any larger effort.}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Define migration-specific terms plainly so a first-time reader is not gated out. The terms below recur throughout the plan; keep their definitions in everyday language.

| Term | Definition |
|---|---|
| Migration | Moving a system, its data, and its users from a current ("source") environment to a target ("destination") environment without losing data or breaking service. A defined maintenance activity in ISO/IEC/IEEE 14764. |
| Cutover | The moment the target system becomes the live, system-of-record and the source stops being authoritative. The plan's most delicate point: everything before is preparation, everything after is stabilization. |
| ETL (Extract, Transform, Load) | The three jobs of moving data: pull it out of the old store (extract), reshape it to fit the new schema (transform), write it into the new store (load). |
| Reconciliation | Proving the data landed correctly by comparing source and target (row counts, checksums, totals, spot-checks) — so you can *assert* nothing was lost or corrupted, rather than hope. |
| Rollback (fallback) | The pre-planned way to abandon the migration and return to a known-good prior state if something goes wrong. Written *before* cutover, it turns a crisis into a procedure. |
| Decommission (retirement) | Formally and safely shutting down the source system after a successful, accepted migration: archiving data, revoking access, releasing licenses and infrastructure, recording it is no longer authoritative. |
| {{Domain term}} | {{Definition}} |

### 1.4 References

> List the documents that this plan depends on or that constrain it. Categorize for readability. ISO/IEC/IEEE 14764:2022 belongs here as the companion standard.

Project / system documents:
- {{path/to/architecture.md}} — {{target architecture this migration realizes}}
- {{path/to/srs.md}} — {{requirements the migrated system must continue to meet}}
- {{path/to/runbook.md}} — {{operational runbook for the source and/or target system}}

Organizational / contractual:
- {{Data-retention policy / SLA / contract clause governing downtime or data handling}}

Regulatory / compliance:
- {{Applicable regulation, e.g., data-privacy obligations affecting what data may be copied or must be masked}}

Standards:
- ISO/IEC/IEEE 14764:2022 — Software maintenance; migration and software-retirement activities (companion standard for this plan).
- {{Other applicable standard with version}} — {{relevance}}

---

## 2. Current State (Source)

> You cannot plan a safe move without an honest inventory of what exists today. This section describes the system you are migrating **FROM** in enough detail that a stranger could understand what is at stake. Be specific — vagueness here becomes surprises at cutover. Cover the existing system and platform, its data stores (and their rough size/shape), the interfaces and integrations that depend on it, current operational constraints, and the known weaknesses that motivate or complicate the move.

**System and platform:** {{Current software name, version, runtime, hosting platform, and how it is deployed today.}}

**Data stores:** {{What data lives where, in what kind of store, and roughly how much — e.g., "{{N}} GB across {{M}} tables in {{datastore}}; {{K}} rows in the largest table." Include file/blob storage, caches, and queues if they hold state that matters.}}

**Interfaces and integrations (who depends on the source):**

| Component | Type | Owner | Notes |
|---|---|---|---|
| {{Component / store / interface}} | {{App / DB / queue / API / file share}} | {{Team or role}} | {{Size, criticality, who calls it / who it calls}} |
| {{e.g., Billing API consumer}} | {{Inbound API}} | {{Finance}} | {{Calls source nightly; breaks if endpoint moves}} |
| {{...}} | {{...}} | {{...}} | {{...}} |

**Current constraints:** {{Uptime requirements, allowed maintenance windows, peak-usage periods to avoid, compliance obligations on the data, contractual SLAs.}}

**Known weaknesses / risks motivating or complicating migration:** {{Aging platform, unsupported version, data-quality issues that transformation must handle, undocumented behavior, brittle integrations. Each item here likely reappears in §10 Risks.}}

---

## 3. Target State (Destination)

> This is the "after" picture — what "done and working" actually looks like. Describe the system you are migrating **TO**: the target software and version, its data model and schema, its infrastructure, its operational model, and the support model after go-live. Where the target differs *structurally* from the source — renamed fields, changed schema, dropped or merged features — call those **deltas** out explicitly, because they drive the transformation work in §5 Data Migration.

**Target software and platform:** {{Destination software name, version, runtime, hosting, deployment model.}}

**Data model and schema:** {{The target schema/structure. Note where it differs from the source structure.}}

**Infrastructure:** {{Hosting, storage, network, scaling, and any new dependencies the target introduces.}}

**Operational model:** {{Who runs the target, how it is monitored, backup/restore approach, on-call ownership.}}

**Support model after go-live:** {{Who supports users and operations once the target is live; escalation paths.}}

**Source → target deltas (what changes structurally):**

| Source element | Target element | Delta | Drives which DM task |
|---|---|---|---|
| {{source.field_a}} | {{target.fieldA}} | {{Renamed}} | {{DM-1}} |
| {{source.status (free text)}} | {{target.status (enum)}} | {{Normalized; needs mapping table}} | {{DM-2}} |
| {{source.legacy_flag}} | {{— (dropped)}} | {{Removed; confirm no consumer depends on it}} | {{DM-3}} |
| {{...}} | {{...}} | {{...}} | {{...}} |

---

## 4. Migration Strategy

> State and justify the **pattern** you have chosen, then lay out the ordered steps that execute it. Define each pattern in one line the first time it appears:
> - **Big-bang** — switch everything at once in a single cutover.
> - **Phased / incremental** — move slices (by module, region, or user group) over time.
> - **Parallel-run** — run both systems live simultaneously and reconcile until you trust the target.
> - **Pilot** — a small group goes first to de-risk before the rest follow.
>
> Each trades risk against complexity and duration differently; pick one deliberately and say *why* it fits this migration's constraints. Then lay out the ordered migration steps as **STEP-1, STEP-2, …** — each a discrete, verifiable action with an owner and a clear "done when" condition. This numbered STEP-N list is the spine that §7 (Verification) and §8 (Rollback) trace back to.

**Chosen pattern:** {{Big-bang / Phased / Parallel-run / Pilot}}.

**Why this pattern fits:** {{Justify against the constraints from §2 — e.g., "Parallel-run chosen because the contractual SLA forbids more than {{X}} minutes of downtime, and reconciling both systems for {{N}} days lets us prove correctness before cutting over."}}

**Sequencing, dependencies, and freeze windows:** {{Note which steps must precede which; the planned cutover window; and any code-freeze, data-freeze, or blackout periods during which no other changes are allowed.}}

**Migration steps:**

| ID | Step | Owner | Done when |
|---|---|---|---|
| STEP-1 | {{Provision and configure target environment}} | {{Role}} | {{Target reachable, smoke-tested, monitored}} |
| STEP-2 | {{Dry-run the full data migration against a copy}} | {{Role}} | {{Reconciliation (DM-N) passes on the copy}} |
| STEP-3 | {{Freeze source writes / enter cutover window}} | {{Role}} | {{Source confirmed read-only; STEP-2 signed off}} |
| STEP-4 | {{Execute production data migration (see §5)}} | {{Role}} | {{All DM-N tasks complete and reconciled}} |
| STEP-5 | {{Repoint integrations and switch system-of-record}} | {{Role}} | {{Cutover complete; target is authoritative}} |
| STEP-6 | {{Run post-cutover verification (see §7)}} | {{Role}} | {{All AC-N met}} |
| STEP-N | {{...}} | {{...}} | {{...}} |

---

## 5. Data Migration

> This is usually the highest-risk part of any migration, so be concrete. **ETL** names the three jobs of moving data: **Extract** (pull from the source store), **Transform** (reshape to fit the target schema), **Load** (write into the target). The single most important sub-activity here is **reconciliation** — proving, not hoping, that nothing was lost or corrupted in transit. Capture the work as **DM-N** tasks. Note any data-privacy or retention obligations that affect what may be copied or must be masked.

**DM-N data-migration tasks:**

| ID | Task | ETL phase | Approach / tooling | Owner | Per-task rollback |
|---|---|---|---|---|---|
| DM-1 | {{Extract customer records}} | Extract | {{Tool / query}} | {{Role}} | {{Re-run; idempotent}} |
| DM-2 | {{Map free-text status → enum}} | Transform | {{Mapping table; defaults for unknown values}} | {{Role}} | {{Drop staging table; re-transform}} |
| DM-3 | {{Load records into target}} | Load | {{Batch / streaming; load order}} | {{Role}} | {{Truncate target table; reload from staging}} |
| DM-N | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

**Transformation / mapping rules:** {{How renamed, merged, defaulted, or dropped fields are handled (tie back to the §3 deltas table). State the rule for records that fail to transform — quarantine, default, or abort.}}

**Load procedure and ordering:** {{The order tables/entities must be loaded so foreign keys and dependencies are satisfied; batch sizes; how failures mid-load are handled.}}

**Validation and reconciliation (how we prove nothing was lost):**
- Row counts: {{compare source vs. target counts per entity; tolerance = {{0 / stated allowance}}.}}
- Checksums / hashes: {{checksum key fields or whole records and compare.}}
- Totals: {{sum financial or quantity columns on both sides and compare.}}
- Spot-checks: {{manually compare {{N}} sampled records end-to-end.}}
- {{Define what counts as a reconciliation PASS vs. FAIL — a FAIL is a candidate rollback trigger in §8.}}

**In-flight / changing data:** {{If the source stays live during migration (e.g., parallel-run), describe how changes made after extraction are captured and applied — change-data-capture, delta sync, or a final freeze-and-catch-up at cutover.}}

**Data-privacy / retention obligations:** {{What data must be masked, anonymized, excluded, or specially handled per regulation or policy; what must be retained vs. what must not be copied.}}

---

## 6. User Transition

> A migration is **not done when the data moves — it is done when people are working in the new system.** Name who is affected and what changes for them, in plain terms. A migration that is technically perfect but leaves users stranded has failed its purpose. Cover communications, training, cutover-day support, and any temporary dual-access or read-only period.

**Affected stakeholders and what changes for them:**

| Stakeholder group | What changes | What they must do |
|---|---|---|
| {{End users in {{region}}}} | {{New URL; updated UI}} | {{Re-bookmark; complete short training}} |
| {{Integrators / API consumers}} | {{New endpoint after STEP-5}} | {{Update endpoint config by {{date}}}} |
| {{Support / ops team}} | {{New monitoring and runbook}} | {{Complete handover; be on standby at cutover}} |
| {{...}} | {{...}} | {{...}} |

**Communication plan (tied to the STEP-N sequence):**

| When | Audience | Message | Channel | Owner |
|---|---|---|---|---|
| {{T-{{N}} days (before STEP-3)}} | {{All users}} | {{Heads-up: migration window and what to expect}} | {{Email / banner}} | {{Role}} |
| {{T-1 day}} | {{All users}} | {{Reminder; downtime window; where to get help}} | {{Email}} | {{Role}} |
| {{Cutover (STEP-5)}} | {{All users}} | {{We are live on the new system; here's how to log in}} | {{Email / banner}} | {{Role}} |
| {{T+{{N}} days}} | {{All users}} | {{Stabilization complete; old system retiring}} | {{Email}} | {{Role}} |

**Training and documentation:** {{What training is provided, in what form, by when; where the updated user docs live.}}

**Cutover-day support:** {{Who is on standby, for how long, and how users reach help during and immediately after cutover.}}

**Temporary dual-access / read-only period:** {{If users can read the old system (read-only) for a grace period after cutover, state the window and when it closes — note this interacts with §9 decommissioning.}}

---

## 7. Verification and Acceptance

> Define how you *prove* the migration succeeded. Two distinct questions:
> - **Verification** — "did the migration execute correctly *per the plan*?" (the data moved, the steps ran as written).
> - **Validation** — "does the migrated system actually *do what users need*?" (it behaves right in real use).
>
> 14764 treats both as part of transition. **Acceptance criteria** are the explicit, testable conditions that must hold before anyone signs off — without them, "done" is just an opinion. List them as **AC-N**, each tied where possible to a STEP-N or DM-N. State who performs each check and who holds sign-off authority. Then define the post-cutover stabilization window and the threshold at which the migration is *declared formally accepted*.

**AC-N acceptance criteria:**

| ID | Acceptance criterion | Type | Traces to | Verified by | How verified |
|---|---|---|---|---|---|
| AC-1 | {{Row counts and checksums match between source and target}} | Verification | {{DM-1, DM-3}} | {{Role}} | {{Reconciliation report}} |
| AC-2 | {{All ordered steps completed within the cutover window}} | Verification | {{STEP-1..STEP-6}} | {{Role}} | {{Runbook checklist}} |
| AC-3 | {{Users can complete {{key workflow}} end-to-end in the target}} | Validation | {{STEP-5}} | {{Role / pilot users}} | {{Scripted user acceptance test}} |
| AC-4 | {{All critical integrations send/receive correctly}} | Validation | {{STEP-5}} | {{Role}} | {{Integration smoke test}} |
| AC-N | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

**Sign-off authority:** {{Role/name who declares the acceptance criteria met. Distinct from, or the same as, the rollback decision authority — state which.}}

**Stabilization / monitoring period:** {{How long the team actively monitors after cutover (e.g., {{N}} days), what metrics are watched, and what would re-open a rollback decision during this window.}}

**Formal acceptance threshold:** {{The migration is declared formally accepted when {{all AC-N pass AND the stabilization window completes with no rollback-triggering defect}}. Formal acceptance is the gate that unlocks §9 decommissioning.}}

---

## 8. Rollback Plan

> A **rollback** (or **fallback**) is the pre-planned way to abandon the migration and return to a known-good prior state if something goes wrong. Written *before* cutover, it turns a crisis into a procedure rather than a panic. Capture it as **RB-N** items: the triggers that cause a rollback decision, the step-by-step procedure, how source state is restored (and how any data written to the target during the attempt is reconciled or discarded), the point-of-no-return after which rollback is no longer feasible, and the decision authority empowered to call it. Ground the triggers in a stated **maximum tolerable downtime**.

**Maximum tolerable downtime:** {{The longest outage the business/SLA can absorb — e.g., "{{X}} minutes." Trigger thresholds below are calibrated to this.}}

**RB-N rollback triggers (conditions that cause a rollback decision):**

| ID | Trigger | Threshold | Decision authority |
|---|---|---|---|
| RB-1 | {{Reconciliation failure}} | {{Any AC-1 / DM-N mismatch beyond tolerance}} | {{Rollback authority}} |
| RB-2 | {{Acceptance criteria not met by deadline}} | {{AC-N still failing at {{cutover window + X}}}} | {{Rollback authority}} |
| RB-3 | {{Critical defect in target}} | {{Severity-1 with no fix within {{Y}} minutes}} | {{Rollback authority}} |
| RB-4 | {{Downtime exceeds tolerance}} | {{Outage > maximum tolerable downtime}} | {{Rollback authority}} |
| RB-N | {{...}} | {{...}} | {{...}} |

**Rollback procedure (step-by-step):**
1. {{Halt the migration / cutover immediately; freeze target writes.}}
2. {{Restore source to its known-good pre-cutover state (see "data restoration" below).}}
3. {{Repoint integrations back to the source.}}
4. {{Reconcile or discard any data written to the target during the attempt.}}
5. {{Re-open the source as system-of-record; notify users per §6.}}
6. {{Conduct a post-mortem; revise this plan before any retry.}}

**Data restoration:** {{How the source's data and state are restored — backup/snapshot taken at STEP-3, transaction logs, etc. State explicitly how any writes that hit the target during the attempt are handled: reconciled back to source, or safely discarded.}}

**Point-of-no-return:** {{The step after which rollback is no longer feasible and why — e.g., "After STEP-5, once integrations have written to the target and the source backup window has lapsed, rollback is no longer safe; from this point the team must drive forward to a fix." Place this deliberately and call it out, because it is the moment the safety net is removed.}}

**Decision authority:** {{Role/name — must match the "Rollback decision authority" row in the front-matter metadata table.}}

---

## 9. Decommissioning the Source System

> After a successful, accepted migration, the old system must be **deliberately and safely shut down — not just abandoned.** Decommissioning (retirement) is part of 14764's transition scope. Crucially, it happens **only after §7 formal acceptance and the stabilization window pass**, so that a rollback (§8) remains possible until then. Cover data archival, access revocation, license/infrastructure release, integration shutdown, and recording the date the source ceased to be authoritative.

**Precondition (do not start until met):** {{Decommissioning begins only after §7 acceptance is signed off AND the stabilization/monitoring window has completed with no rollback-triggering defect. Until then the source stays warm so §8 rollback remains available.}}

**Decommissioning tasks:**

| Task | Detail | Owner | Done when |
|---|---|---|---|
| {{Data archival / retention}} | {{What is kept, where, for how long, per which policy/regulation}} | {{Role}} | {{Archive verified and catalogued}} |
| {{Revoke access and credentials}} | {{Disable accounts, rotate/retire secrets, remove permissions}} | {{Role}} | {{No live credentials remain}} |
| {{Release licenses, infrastructure, cost}} | {{Cancel licenses; deprovision servers/storage; stop billing}} | {{Role}} | {{Resources released; cost confirmed stopped}} |
| {{Redirect / shut down integrations}} | {{Repoint or disable integrations that pointed at the source}} | {{Role}} | {{No integration still calls the source}} |
| {{Record retirement}} | {{Log the date the source ceased to be authoritative}} | {{Role}} | {{Date recorded: {{YYYY-MM-DD}}}} |

**Date source ceased to be authoritative:** {{YYYY-MM-DD}}.

---

## 10. Risks

> A **risk register** is a plain list of what could go wrong, how likely it is, how bad it would be, and who is watching it. Naming risks ahead of time is how a team stays *ahead* of them instead of reacting. Use the table below and link each mitigation back to a concrete STEP-N, DM-N, or RB-N item where one exists — so the register is actionable, not decorative. Include the migration-specific classics: data loss/corruption, extended downtime, reconciliation mismatch, user-readiness gaps, and integration breakage.

| ID | Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| RISK-1 | {{Data loss or corruption during transfer}} | {{Med}} | {{High}} | {{Reconciliation per §5 (DM-N); rollback RB-1}} | {{Role}} |
| RISK-2 | {{Downtime exceeds tolerance}} | {{Low}} | {{High}} | {{Dry-run STEP-2 to size the window; trigger RB-4}} | {{Role}} |
| RISK-3 | {{Reconciliation mismatch at cutover}} | {{Med}} | {{High}} | {{Checksums + totals in §5; RB-1 trigger}} | {{Role}} |
| RISK-4 | {{Users not ready / not trained}} | {{Med}} | {{Med}} | {{Training and comms per §6}} | {{Role}} |
| RISK-5 | {{Integration breaks after repoint}} | {{Med}} | {{High}} | {{Integration smoke test AC-4; repoint in STEP-5}} | {{Role}} |
| RISK-N | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

---

## 11. Open Questions

> Capture decisions still unresolved so they are *tracked rather than forgotten*, and resolve/remove them as the plan firms up. List as **OQ-N**, each with the question, what is blocking resolution, and who must decide. A migration plan with open questions in load-bearing places (cutover window, schema-mapping edge cases, the rollback point-of-no-return) is not ready to execute — this section makes that visible.

- **OQ-1**: {{Undecided cutover window}} — {{blocked on: {{e.g., business calendar confirmation}}; decision owner: {{role}}}}
- **OQ-2**: {{Unresolved schema-mapping edge case for {{field}}}} — {{blocked on: {{e.g., data-owner ruling on legacy values}}; decision owner: {{role}}}}
- **OQ-3**: {{Sign-off pending on the rollback point-of-no-return}} — {{blocked on: {{e.g., backup-window confirmation}}; decision owner: {{rollback authority}}}}
- **OQ-N**: {{...}}

---

## 12. Revision History

> Track every substantive change with a version bump so the plan's evolution is auditable — important for a migration that may be reviewed and re-approved before execution. Keep the optional Approval column if your process requires recorded approval per revision.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Current State (Source)
- §3 Target State (Destination)
- §4 Migration Strategy (the STEP-N list is the spine)
- §5 Data Migration (almost always the highest-risk part)
- §7 Verification and Acceptance
- §8 Rollback Plan
- §12 Revision History

**Optional sections** (include if relevant):
- §6 User Transition (omit only if the migration genuinely has no human users — e.g., a back-end batch system with no interactive users; even then, keep the integrator-communication parts)
- §9 Decommissioning the Source System (omit only if the source must remain live indefinitely; otherwise keep it — abandoned-but-still-running systems are a real risk)
- §10 Risks (strongly recommended; track elsewhere only if you maintain a separate program-level risk register)
- §11 Open Questions (track elsewhere if you prefer, but don't lose load-bearing unknowns)

**Traceability ID conventions** (so this plan cross-references cleanly with itself and sibling documents):
- STEP-N — ordered, discrete, verifiable migration steps (§4)
- DM-N — data-migration tasks (§5)
- AC-N — acceptance criteria (§7), each tied where possible to a STEP-N or DM-N
- RB-N — rollback triggers and procedures (§8)
- RISK-N — risks (§10), with mitigations linking back to STEP-N / DM-N / RB-N
- OQ-N — open questions (§11)

**Tailoring:**
- The 14764 topic set is guidance, not a mandate. Add or remove subsections as the migration needs.
- Keep §4's STEP-N list the single source of truth for *what happens in what order*; let §7 and §8 reference it rather than restating it.
- **Solo developer / small team collapse:** for a small migration (e.g., one developer moving a personal project's database), you can collapse this dramatically — keep §2/§3 as a few bullets each, §4 as a short numbered checklist, §5's reconciliation as "compare row counts and a sample by hand," §7 as a one-line "I can log in and the data's all there," and §8 as "I have a backup and the restore command is `{{command}}`." The *shape* still protects you: even a one-person migration benefits from a written rollback line and a reconciliation check before deleting the old data. Don't skip §8 just because you're working alone — that's exactly when an unplanned rollback hurts most.
- Revision history is mandatory. A migration plan is frequently reviewed and re-approved before execution; version every substantive change.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 14764:2022, not this lightweight version. This template is suitable for solo/small-team projects, internal tooling, and routine migrations; it does not reproduce the standard's normative requirements and may omit obligations that a regulated or contractual migration must satisfy.
