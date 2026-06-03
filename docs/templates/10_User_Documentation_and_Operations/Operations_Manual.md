# Operations Manual Template

> **Template purpose:** Lightweight Operations Manual (a.k.a. runbook / ops guide) structure for the document an operator follows to *keep a deployed system running* day to day. An operations manual is distinct from an install guide (one-time setup) and from a user guide (how end-users use features) — it answers "it is deployed; now how do I run it, watch it, and fix it when it breaks?" Replace `{{placeholder}}` content with system-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once a system is (or is about to be) running in production and someone has to keep it alive. Write the first draft before go-live so the response to the first 3am failure is pre-decided rather than improvised, and keep it current as the running system changes. It sits downstream of the SRS/architecture/design docs (WHAT and HOW it was built) and downstream of the install/deployment guide (how it got there) — this manual is about the *ongoing operation* of what those produced.
>
> **Companion standard:** ISO/IEC/IEEE 26511:2018 (information for users — management of the user documentation process) + ISO/IEC/IEEE 12207:2017 §6.4.9 (Operation process).
>
> **Status of this template:** Lightweight, public, reusable extract aligned to ISO/IEC/IEEE 26511:2018 (information for users) and the Operation process of ISO/IEC/IEEE 12207:2017 (§6.4.9), and to SWEBOK's Software Maintenance / operational practice. Both companion standards are PAYWALLED ISO/IEEE publications — this template reproduces only the structural outline and plain-language concepts, contains no copyrighted text from the standards, and has NOT been line-checked against the purchased standards. Verify section coverage against the full standards before relying on this in a regulated, safety-critical, or contractual context. Suitable as-is for solo / small-team and internal or public operational documentation. The SWEBOK-aligned domain sections (System Overview, Roles, Startup/Shutdown, Monitoring, Routine Operations, Incident Handling, Backup and Recovery, Security Operations, Known Problems) follow SWEBOK operational structure and are not governed by any single normative standard; 26511/12207 are named as the closest companion standards for document management and the operation life-cycle process respectively.

---

# Operations Manual — {{System Name}}

| Field | Value |
|---|---|
| Document ID | OPS-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 26511:2018 + 12207:2017 §6.4.9 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Operated system version(s) | {{Which release(s) of the system this manual applies to — ops procedures drift as the system changes}} |
| Operating environment | {{Production / staging / single-host / cloud region — where these procedures are valid}} |
| On-call / contact | {{Who to reach, and how, when the system is down — even a single name and channel, e.g. "<name>, <chat app>"}} |
| Review cadence | {{How often this manual is re-checked against reality, e.g. quarterly or after every incident}} |

---

## 1. Introduction

> This is the **Operations Manual** — the runbook for keeping a *deployed* {{System Name}} running day to day. It is **not** the install guide (one-time setup) and **not** the end-user guide (how to use features). It assumes the system already exists and is running, and it tells whoever keeps it alive how to start it, watch it, maintain it, and recover it when something breaks.
>
> Keep the four subsections below. They establish *why this document exists*, *what slice of operations it covers*, *the vocabulary a true beginner needs*, and *what other documents it depends on*. The guidance blockquotes can be deleted once each subsection is written.

### 1.1 Purpose

> One paragraph: why this document exists and who it is for. Name the **operator** role — the person who keeps the system alive in production — even on a solo project. (On a solo project the operator, owner, and end-user can all be the same person; naming the role still matters, because future-you reading this at 3am during an outage genuinely *is* a different person than present-you who currently holds all the context in their head. Write for that future reader.)

{{This document tells the operator how to run {{System Name}} in production: how to start and stop it, how to know it is healthy, what routine work keeps it healthy, what to do when it breaks, and how to recover it from failure or data loss. It is written for the **operator** — whoever is responsible for keeping {{System Name}} alive — which on this project is {{operator name / role, e.g. "the maintainer wearing the operator hat"}}.}}

### 1.2 Scope

> Define the operational surface this manual covers and what it explicitly excludes. Be specific about *which version(s)* of the system and *which environment* the procedures are valid for — ops procedures drift as the system changes, and a procedure that was right two releases ago can be actively wrong now. If operations differ between phases (e.g. a single-host prototype vs. a future multi-host deployment), note the phase split here.

**This manual covers** the day-to-day operation of {{System Name}} version(s) {{X.Y}} running in {{environment, e.g. "a single WSL2 host"}}: startup/shutdown, monitoring, routine maintenance, incident response, backup/recovery, and security operations.

**This manual explicitly excludes:**
- **Initial provisioning / install** — see {{install / deployment guide reference}}. (One-time setup is a different document.)
- **Feature usage** — see {{user guide reference}}. (How end-users *use* the system is a different document.)
- **Source-level debugging / development** — see {{architecture / design docs}}. (Fixing the code is development work, not operation.)

**Phases (if applicable):**
- **Phase 1** (current): {{e.g. single-host prototype — one operator, one machine}}
- **Phase 2** (future): {{e.g. multi-host — procedures here may not yet cover this; revisit before that phase}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Seed the operational vocabulary a true beginner needs so the rest of the manual reads cleanly. Define each formal term plainly the first time it would otherwise be assumed. Add system-specific terms (component names, service-manager unit names, paths) as needed.

| Term | Definition |
|---|---|
| Operations Manual (runbook / ops guide) | The document an operator follows to *keep a running system running*. Distinct from an install guide (one-time setup) and a user guide (feature usage). |
| Operator | Whoever keeps the system alive in production. May be the same solo person who built it. This manual is written **for** the operator. |
| Procedure (OPS-N) | A numbered, step-by-step sequence an operator runs. Each step is copy-pasteable or unambiguous, states its expected result, and says what to do if the result is wrong. Numbered so it can be cited from alerts, incident playbooks, and logs ("run OPS-4"). |
| Logging | Recording what happened, after the fact, for later reading. |
| Monitoring | Continuously watching metrics/health — *is it OK right now?* |
| Alerting | Firing a notification when a monitored value crosses a threshold — *wake someone up.* |
| Threshold | The value at which "normal" becomes "a problem worth acting on" (e.g. disk >90% full). A threshold without a defined response is just a number. |
| Incident | An unplanned event that degrades or stops service. Has a **severity** (how bad) that drives **escalation** (who to wake, how fast). |
| Triage | First-response assessment of an incident — what is broken, how bad, what is the fastest safe action — before attempting a full fix. (Term borrowed from emergency medicine.) |
| Escalation | The defined path for handing an incident to someone with more authority/access when first response cannot resolve it. |
| Post-incident review (postmortem) | A blameless write-up after an incident: what happened, why, what we change so it cannot recur. |
| RTO (Recovery Time Objective) | The maximum acceptable *time* to restore service after a failure ("back within 4 hours"). About **downtime**. |
| RPO (Recovery Point Objective) | The maximum acceptable amount of *data loss* measured in time ("lose at most the last 1 hour"). About **data freshness**. |
| Backup verification (restore test) | Periodically performing the restore to *prove* the backup actually works. A backup never restored is a hope, not a backup. |
| Secret / credential | A sensitive value (API key, password, token, private key) that grants access. Never committed to the repo; handled differently from ordinary config. |
| Rotation | Periodically replacing a secret with a new one so an old, possibly-leaked credential stops working. Pairs with **revocation** (killing a credential immediately on suspected compromise). |
| Maintenance window | A pre-announced period during which the system may be down or degraded for planned work, so the impact is expected rather than surprising. |
| Known problem + workaround | A bug or limitation you have *chosen not to fix yet*, paired with the interim steps that keep operations going. |
| {{System-specific term}} | {{Definition}} |

### 1.4 References

> List the documents this manual depends on or that the operator may need to reach for. Categorize for readability. Include the system's own design lineage, the install/deployment guide, vendor/runtime docs, and the companion standards.

System documents:
- {{path/to/srs.md}} — Software Requirements Specification (WHAT the system does)
- {{path/to/architecture.md}} — Architecture Description (HOW it is structured)
- {{path/to/design/*.md}} — module/subsystem design (SDD) documents
- {{path/to/install-or-deployment-guide.md}} — initial provisioning (the one-time setup this manual assumes is already done)

Vendor / runtime documents:
- {{runtime / model provider docs}} — {{relevance, e.g. status page, API limits}}
- {{service-manager / OS docs}} — {{relevance}}

Companion standards:
- ISO/IEC/IEEE 26511:2018 — Information for users: management of the user documentation process
- ISO/IEC/IEEE 12207:2017 §6.4.9 — Operation process (software life cycle)

---

## 2. System Overview (operational view)

> This is **not** the design document. It is the design *as seen by someone who has to restart it at 3am* — the answer to "what am I actually keeping alive, and what does it depend on?" Keep it to what an operator needs: what runs, where it runs, what data it holds, what it talks to, and what breaks if a dependency goes away.
>
> Tie each component to the **OPS-N** procedures (§4) that start, stop, and check it, so this overview doubles as an index into the rest of the manual.

{{One-paragraph plain-language picture of the running system: what {{System Name}} is, at the level of "a process that does X, talking to Y, storing Z."}}

**Running components**

| Component | Where it runs | Depends on | Health check | Related OPS-N |
|---|---|---|---|---|
| {{e.g. main service}} | {{host / path / port / service-manager unit}} | {{e.g. local datastore, model provider API}} | {{how you confirm it is up}} | OPS-{{N}} (start), OPS-{{N}} (check) |
| {{e.g. background worker}} | {{host / path / unit}} | {{main service}} | {{health check}} | OPS-{{N}} |
| {{e.g. local datastore}} | {{host / path}} | {{disk}} | {{health check}} | OPS-{{N}} |

> Note: if this system runs **without containers** — components are native processes managed by {{service manager, e.g. systemd user units / a supervisor script}}, not images — the procedures below assume native installs the operator can inspect directly. Adjust this note if the system is containerized.

**Data stores (the things backups must protect — cross-reference §8)**

| Data store | Location | What it holds | Backed up by |
|---|---|---|---|
| {{e.g. database file}} | {{absolute path}} | {{what would be lost if this vanished}} | OPS-{{N}} (§6) |
| {{e.g. config / state dir}} | {{absolute path}} | {{...}} | OPS-{{N}} (§6) |

**External dependencies and integrations**

| Dependency | What it provides | If unavailable, {{System Name}} ... |
|---|---|---|
| {{e.g. runtime / model provider}} | {{the capability it provides}} | {{degrades how? fails how? for how long is that tolerable?}} |
| {{e.g. message relay / API}} | {{...}} | {{...}} |

**Component + dependency sketch** (ASCII is fine):

```
{{[ user / caller ]
        |
        v
[ main service ] --uses--> [ runtime/model provider ]  (external)
        |
        v
[ local datastore ]  <-- backed up by OPS-N (§6)}}
```

---

## 3. Roles and Responsibilities

> Who is responsible for what, in operational terms. On a solo project this can read as "all me" — write it anyway. The value is making explicit **which hat you are wearing** for a given task (operator vs. owner vs. end-user vs. external vendor support), and ensuring the manual survives the project gaining a second person without a rewrite.
>
> Use **ROLE-N** ids so other sections (and incident logs) can cite a role. Cross-reference the **On-call / contact** row in the metadata block at the top.

| ROLE-N | Role | Filled by | Operational responsibilities | Authority | Contact |
|---|---|---|---|---|---|
| ROLE-1 | Operator | {{name / role or "TBD"}} | Runs startup/shutdown (§4), watches monitoring (§5), performs routine ops (§6), first-responds to incidents (§7) | May restart/stop the system; may execute any OPS-N procedure | {{how reached during an incident}} |
| ROLE-2 | Owner | {{name / role or "TBD"}} | Decides operational policy, RTO/RPO targets, what is in scope | Approves restore-from-backup, secret rotation, and maintenance windows | {{contact}} |
| ROLE-3 | End-user | {{who, or "general public"}} | Uses the system; may report incidents | None operational | {{how they report problems}} |
| ROLE-4 | External vendor support | {{e.g. runtime / model provider support}} | Resolves issues in dependencies outside our control | Per vendor contract/plan | {{support channel / ticket URL}} |

> On a solo project, ROLE-1, ROLE-2, and ROLE-3 may all be one person. The split still tells future-you *which authority you are exercising* — e.g. "as Owner I am approving this restore," so the Operator step that follows is sanctioned.

---

## 4. Startup and Shutdown

> The first place the **OPS-N** convention earns its keep — model it well; the rest of the manual copies this shape. A *procedure* is a numbered sequence where each step states the exact action **and its expected result**, plus what to do if the result is wrong. "Expected result + what to do if wrong" is exactly what separates a real procedure from a vague memory.
>
> Cover three modes: **normal** startup/shutdown, **emergency** (fast/forced) shutdown, and **scheduled** (planned restart, e.g. after an upgrade or inside a maintenance window). **Startup order matters** when components depend on each other — cross-reference §2 and bring up dependencies first.
>
> Honor the substrate-output principle: tell the operator what success and failure **look like in plain language**, not just "run this and read the output." Raw command output is the operator's *input*, not the operator's instruction.

### OPS-1 — Normal startup

**Preconditions:** {{host is up; no maintenance in progress; dependencies in §2 are reachable}}.

| # | Action | Expected result | If wrong |
|---|---|---|---|
| 1 | Start the datastore: `{{command}}` | {{e.g. "status shows active; no error lines"}} | {{go to OPS-? / check §5 logs}} |
| 2 | Start the main service: `{{command}}` | {{e.g. "process is listening on port {{port}}"}} | {{check it did not start before its dependency; re-run step 1}} |
| 3 | Start background worker(s): `{{command}}` | {{expected result}} | {{...}} |

**Verification (how I know it actually came up):** {{e.g. "run OPS-3; the health check for every §2 component returns healthy, and a test request returns a normal response."}}

**Rollback / if a step fails:** {{e.g. "stop everything via OPS-2, fix the failing dependency, restart from step 1." Do not leave components half-started.}}

### OPS-2 — Normal shutdown

**Preconditions:** {{no critical job mid-run; users notified if user-facing}}.

| # | Action | Expected result | If wrong |
|---|---|---|---|
| 1 | Stop the main service: `{{command}}` | {{process exits cleanly; no orphaned children}} | {{check for stuck process; see OPS-{{N}}}} |
| 2 | Stop background worker(s): `{{command}}` | {{...}} | {{...}} |
| 3 | Stop the datastore last: `{{command}}` | {{clean shutdown; no corruption warning in logs}} | {{do NOT force-kill the datastore mid-write — see OPS-3 emergency}} |

**Verification:** {{no relevant processes remain; ports freed.}}

### OPS-3 — Emergency (fast/forced) shutdown

> Use only when normal shutdown is unsafe or unresponsive — e.g. the host is about to lose power, or a runaway process is causing harm. Forced shutdown trades cleanliness for speed; expect to verify data integrity on the next startup.

| # | Action | Expected result | If wrong |
|---|---|---|---|
| 1 | Force-stop the main service: `{{command}}` | {{process gone immediately}} | {{escalate per §7}} |
| 2 | Force-stop remaining components | {{all stopped}} | {{...}} |
| 3 | Note the time and reason | {{recorded for the §7 post-incident review}} | {{—}} |

**Verification / aftermath:** {{on next startup, run the datastore integrity check {{command}} before serving traffic; if it reports damage, go to §8 recovery.}}

### OPS-4 — Scheduled restart (planned, e.g. after upgrade / in a maintenance window)

> A planned restart announced in advance (see §6 maintenance windows). The difference from OPS-1/OPS-2 is *coordination*: users are told, the work is bounded, and there is a rollback plan if the new version misbehaves.

| # | Action | Expected result | If wrong |
|---|---|---|---|
| 1 | Announce the maintenance window (§6) | {{users / stakeholders informed}} | {{postpone if not announced}} |
| 2 | Take a pre-change backup (OPS-{{N}}, §6) | {{verified backup exists}} | {{do not proceed without it}} |
| 3 | Normal shutdown (OPS-2) | {{system down cleanly}} | {{OPS-3}} |
| 4 | Apply the planned change: `{{command / steps}}` | {{change applied; expected version reported}} | {{roll back to pre-change backup, restart old version}} |
| 5 | Normal startup (OPS-1) + verify | {{system healthy on new version}} | {{roll back; restore from step 2}} |

**Rollback:** {{restore the OPS-{{N}} backup from step 2 and start the previous version; record the failure for §8/§10.}}

---

## 5. Monitoring

> The operator's daily-awareness section. Keep the three things distinct — beginners conflate them constantly:
> - **Logging** records *what happened* (after the fact, for reading).
> - **Monitoring** continuously watches *is it OK right now?*
> - **Alerting** fires a notification when a monitored value crosses a **threshold** (wake someone).
>
> The goal of all three is to learn about a problem from **your monitoring, not from a user**. A threshold with no paired response is just a number — every alert below names the **OPS-N** procedure (or §7 incident path) to run when it trips.

### 5.1 Logs (what happened)

| Component | Log location | How to read/tail | Retention |
|---|---|---|---|
| {{main service}} | {{path / journalctl unit}} | `{{tail command}}` | {{e.g. 14 days, then rotated}} |
| {{worker}} | {{path}} | `{{command}}` | {{...}} |

> Cold-store note (if relevant): older logs/notes that are still valid but not needed in routine awareness can live in a cold store ({{e.g. an archive dir}}) — reachable on demand, not loaded every glance.

### 5.2 Metrics / health signals (is it OK right now?)

> What "healthy" looks like for each component. Cross-reference the §2 health-check column.

| Component | Healthy looks like | How to check |
|---|---|---|
| {{main service}} | {{e.g. "responds to health endpoint within 1s; error rate near zero"}} | {{command / endpoint}} |
| {{datastore}} | {{e.g. "accepts a test query; disk usage under threshold"}} | {{command}} |

### 5.3 Alerts (wake someone)

| ALERT-N | Signal | Threshold | Severity | Response (OPS-N / §7) |
|---|---|---|---|---|
| ALERT-1 | Disk usage on {{path}} | > 90% full | {{SEV-2}} | OPS-{{N}} (clear space, §6) |
| ALERT-2 | Main-service error rate | > 1% over 5 min | {{SEV-2}} | Triage per §7; likely OPS-1 restart |
| ALERT-3 | Health endpoint unreachable | any failure for > 2 min | {{SEV-1}} | §7 incident; OPS-1 / OPS-3 |
| ALERT-4 | {{dependency}} unavailable | {{e.g. 3 consecutive failures}} | {{SEV-2}} | {{degrade gracefully; §7}} |

### 5.4 Dashboards / at-a-glance checks (if any)

{{Where the operator looks for a single-glance health picture, if such a place exists — a status page, a one-line script, a `systemctl status` of all units. If there is none yet, say so and consider it an §11 open question.}}

### 5.5 Daily / periodic glance checklist

> A short routine so awareness is a habit, not a reaction.

- [ ] {{All §2 components report healthy (run the §5.2 checks)}}
- [ ] {{Disk usage under ALERT-1 threshold}}
- [ ] {{No new error spikes in §5.1 logs since last glance}}
- [ ] {{Most recent backup (§6/§8) is present and recent}}

---

## 6. Routine Operations

> The catalog of scheduled and recurring work that keeps the system healthy. "Routine" work is exactly the work that silently rots when undone — a written **cadence** matters more than it feels like it should. Each recurring task is an **OPS-N** procedure with a stated cadence and a way to confirm it ran.
>
> A **maintenance window** is a pre-announced period during which the system may be down or degraded for planned work. Announcing planned downtime beats surprising people: the impact becomes *expected*. Note that **taking** backups lives here; **restoring** them lives in §8.

**Recurring schedule (scannable index)**

| OPS-N | Task | Cadence | Last verified |
|---|---|---|---|
| OPS-5 | Take a backup | {{daily}} | {{YYYY-MM-DD}} |
| OPS-6 | Log review | {{weekly}} | {{YYYY-MM-DD}} |
| OPS-7 | Disk/space check | {{weekly}} | {{YYYY-MM-DD}} |
| OPS-8 | Dependency / credential expiry check | {{monthly}} | {{YYYY-MM-DD}} |
| OPS-9 | Planned upgrade (maintenance window) | {{on-event}} | {{YYYY-MM-DD}} |

### OPS-5 — Take a backup

**Cadence:** {{daily}}.

| # | Action | Expected result |
|---|---|---|
| 1 | Run the backup of each §2 data store: `{{command}}` | {{a timestamped backup artifact appears at {{location}}}} |
| 2 | Confirm size/age looks sane | {{not zero bytes; newer than the last one}} |

**Confirm it ran:** {{e.g. "the latest file under {{backup location}} is dated today." Verification that the backup can actually be *restored* is a separate task — see §8.}}

### OPS-6 — Log review

**Cadence:** {{weekly}}. Steps: {{tail the §5.1 logs for the period; note any repeated warnings; file new recurring issues into §10 Known Problems.}}

### OPS-7 — Disk / space check

**Cadence:** {{weekly}}. Steps: {{check usage on {{paths}}; if approaching ALERT-1 threshold, clear {{what is safe to clear}}.}}

### OPS-8 — Dependency / credential expiry check

**Cadence:** {{monthly}}. Steps: {{check for available updates to the runtime and dependencies (cross-reference §9); check expiry dates on any time-limited credentials (cross-reference §9 rotation).}}

### OPS-9 — Planned upgrade (uses a maintenance window)

**Cadence:** {{on-event}}. Steps: {{announce the window; perform OPS-4 scheduled restart with the upgrade as the planned change.}}

---

## 7. Incident Handling

> A pre-written playbook for when something breaks unexpectedly. The whole point is that you **pre-decide the response now, calmly**, so you are not improvising mid-outage.
>
> Definitions for a beginner:
> - **Incident** — an unplanned event that degrades or stops service.
> - **Severity** — how bad it is; drives how fast and to whom you escalate.
> - **Triage** — the first-response assessment (what is broken, how bad, fastest safe action) *before* a full fix.
> - **Escalation** — handing the incident to someone with more authority/access when first response cannot resolve it.
> - **Post-incident review (postmortem)** — a blameless write-up afterward: what happened, why, what we change so it cannot recur.
>
> Reference real **OPS-N** procedures rather than restating their steps here.

### 7.1 Severity scale

| INC-N | Severity | Means | Target response time |
|---|---|---|---|
| INC-1 | SEV-1 (critical) | {{service down / data at risk}} | {{respond immediately}} |
| INC-2 | SEV-2 (major) | {{degraded but usable, or trending toward down}} | {{within {{30 min}}}} |
| INC-3 | SEV-3 (minor) | {{cosmetic / single-feature / has a workaround}} | {{next routine window}} |

### 7.2 Escalation path

> Be honest about the solo case — the "escalation path" may be "restore from backup and walk away" or "open a vendor ticket." Write it down anyway; the value is having decided it in advance.

| Severity | First response | If unresolved, escalate to ... |
|---|---|---|
| SEV-1 | {{ROLE-1 operator triages immediately}} | {{ROLE-2 owner authorizes restore-from-backup (§8); or open a SEV-1 vendor ticket with ROLE-4}} |
| SEV-2 | {{ROLE-1 triages}} | {{ROLE-2; vendor support if dependency-caused}} |
| SEV-3 | {{log as §10 Known Problem with a workaround}} | {{schedule a fix; no wake-up needed}} |

### 7.3 Triage checklist

> First questions, in order:

1. **What is broken?** {{which §2 component / which user-visible symptom — confirm via §5 monitoring, not a guess}}
2. **How bad?** {{assign a severity from §7.1}}
3. **What is the fastest *safe* action?** {{often an OPS-1 restart, or a §8 restore; "safe" means it will not make data loss worse}}
4. **Is it us or a dependency?** {{check §2 external dependencies / vendor status page before deep-diving our own code}}

### 7.4 Communication

> Who to tell, and where. State note + affected users.

- **Internal:** {{notify ROLE-2 owner per the escalation path}}
- **Users:** {{where a status note goes — e.g. a status page, a pinned message; what it should say}}

### 7.5 Resolution

> The immediate fix restores service. The *durable* fix is process: a recurring incident's fix usually becomes a **new OPS-N procedure** (so next time it is routine) or a **§10 Known Problem** entry (if you are choosing not to fully fix it yet).

{{Describe how resolution is recorded and what gets promoted into §4/§6 (a new procedure) or §10 (a known problem).}}

### 7.6 Post-incident review (template)

> Fill out after any SEV-1/SEV-2. Blameless — the target is the system, not the person.

| Field | Entry |
|---|---|
| Incident ID / date | {{INC-N / YYYY-MM-DD}} |
| Severity | {{SEV-?}} |
| What happened | {{plain-language timeline}} |
| Why (root cause) | {{the underlying cause, not just the symptom}} |
| Detection | {{how we found out — ideally §5 monitoring, not a user}} |
| Resolution | {{what restored service; which OPS-N used}} |
| What we change | {{new OPS-N? new §10 entry? new §5 alert? new §11 open question?}} |

---

## 8. Backup and Recovery

> The section that proves the system can come back from data loss. Two distinct, **both-required** claims live here:
> 1. *"We take backups."* (§6 OPS-5 covers the taking.)
> 2. *"We have proven we can restore."* (This section — an unverified backup is a hope, not a backup.)
>
> Two recovery objectives, kept distinct (beginners mix these up constantly):
> - **RTO (Recovery Time Objective)** — max acceptable **downtime** ("back within 4 hours").
> - **RPO (Recovery Point Objective)** — max acceptable **data loss** in time ("lose at most the last 1 hour").
>
> Make the restore procedure detailed enough to follow under stress — it is the one people skip writing and later regret.

### 8.1 What is backed up

> Cross-reference the §2 data stores. Note off-host / offsite copies if any — a backup on the same disk that just died is no backup.

| Data store (§2) | Schedule | Location | Retention | Off-host? |
|---|---|---|---|---|
| {{database file}} | {{daily, OPS-5}} | {{path / target}} | {{e.g. 14 dailies + 4 weeklies}} | {{yes/no — where}} |
| {{config/state dir}} | {{daily}} | {{path}} | {{...}} | {{...}} |

### 8.2 OPS-10 — Restore procedure

**Preconditions:** {{ROLE-2 owner has authorized the restore; the cause of loss is understood enough not to immediately re-corrupt; system is stopped (OPS-2/OPS-3)}}.

| # | Action | Expected result | If wrong |
|---|---|---|---|
| 1 | Identify the backup to restore (newest good one) | {{a specific dated artifact chosen}} | {{if newest is suspect, step back to the prior one}} |
| 2 | Stop the system (OPS-2, or OPS-3 if needed) | {{nothing is writing the data store}} | {{do NOT restore over a live store}} |
| 3 | Move the damaged data aside (do not delete) | {{damaged copy preserved for diagnosis}} | {{—}} |
| 4 | Restore from the chosen backup: `{{command}}` | {{data store reconstructed at {{path}}}} | {{try the prior backup; if all fail, go to §8.5}} |
| 5 | Start the system (OPS-1) and verify | {{healthy; data is the expected version}} | {{stop; escalate per §7}} |

**Verification:** {{run a known-data check — e.g. a record you know should exist is present. Record the restore (date, which backup, outcome) per §8.4.}}

### 8.3 Backup verification (restore test)

> The periodic proof that backups actually restore. Without this, §8.1 is just a hope.

- **Cadence:** {{e.g. monthly, or before any major upgrade}}.
- **How:** {{restore the latest backup into a scratch/staging location and confirm it loads and the known-data check passes — without touching production}}.
- **Where the result is recorded:** {{e.g. a row in §12 revision history or a verification log at {{path}} — date, backup tested, pass/fail}}.

### 8.4 RTO / RPO targets — and whether we actually meet them

| Objective | Target | Do current backups meet it? |
|---|---|---|
| RTO (max downtime) | {{e.g. 4 hours}} | {{honest answer — "yes, OPS-10 takes ~30 min" / "unknown, never timed — see §11"}} |
| RPO (max data loss) | {{e.g. 24 hours, since backups are daily}} | {{"yes if daily backup holds" / "RPO is effectively 24h because backups are daily — tighten cadence to reduce"}} |

### 8.5 Disaster recovery — total host loss

> Rebuild-from-scratch outline for when the whole machine is gone, not just the data.

{{Ordered outline: provision a new host (install/deployment guide) → restore data from the off-host backup (OPS-10) → bring up components (OPS-1) → verify. Name the off-host backup location explicitly; if there is none yet, that is a §11 open question and a real risk.}}

---

## 9. Security Operations

> The operator's *recurring* security duties — distinct from one-time hardening, which belongs in the install/deployment docs. Beginner framing:
> - A **secret / credential** is a sensitive value (API key, password, token, private key) that grants access. Secrets are **never committed to the repo** and are handled differently from ordinary config.
> - **Rotation** is periodically replacing a secret so an old, possibly-leaked one stops working.
> - **Revocation** is killing a credential *immediately* on suspected compromise.
>
> This is a public template: the example content below records **names and locations only, never values** — and never implies leaking a real secret. Cross-reference §7 for when a security event becomes an incident.

### 9.1 Account / access management

| Who | Access to what | Review cadence |
|---|---|---|
| {{ROLE-1 operator}} | {{host login, service controls}} | {{quarterly}} |
| {{ROLE-4 vendor}} | {{their API only}} | {{on plan change}} |

> Review cadence: {{e.g. quarterly, confirm each access is still needed and remove any that is not.}}

### 9.2 Secret / credential handling

**Secret inventory (names and locations only — NEVER values):**

| Secret name | Where it lives | Rotated by | Rotation cadence |
|---|---|---|---|
| {{e.g. PROVIDER_API_KEY}} | {{e.g. a secrets file outside the repo / the OS keyring}} | OPS-11 | {{e.g. every 90 days}} |
| {{e.g. signing key}} | {{e.g. local keyring; never in the repo}} | OPS-11 | {{annually}} |

**OPS-11 — Rotate a secret**

| # | Action | Expected result |
|---|---|---|
| 1 | Generate/obtain the new secret | {{new value created at the provider}} |
| 2 | Place it where the component reads it (NOT the repo) | {{component picks up the new value}} |
| 3 | Restart the component (OPS-1) | {{component authenticates with the new secret}} |
| 4 | Revoke the old secret at the provider | {{old value no longer works}} |

**OPS-12 — Immediate revocation (suspected leak)**

> Run the moment a secret may be exposed. Speed beats tidiness.

| # | Action | Expected result |
|---|---|---|
| 1 | Revoke the exposed secret at the provider | {{it stops working immediately}} |
| 2 | Issue a replacement (OPS-11) | {{service restored with a fresh secret}} |
| 3 | Open a §7 incident; assess what the leak exposed | {{recorded for post-incident review}} |

### 9.3 Audit-log review

> What to look at and how often: {{e.g. review access/auth logs {{weekly}} for unexpected logins or unusual API usage; anything anomalous becomes a §7 incident.}}

### 9.4 Vulnerability response

> How updates/patches to the runtime and dependencies are tracked and applied. Cross-reference §6 OPS-8 (the periodic check) and §4 OPS-4 (the restart that applies them).

{{Where advisories are watched ({{source}}); how severity is judged; the path from "patch available" → OPS-8 noted → OPS-4 applied in a maintenance window. A security event in the wild that affects us promotes to a §7 incident.}}

---

## 10. Known Problems and Workarounds

> A structured register so the *same issue is not re-diagnosed from scratch every time it recurs*. A **known problem** is a bug or limitation you have consciously chosen **not to fix yet**, paired with the interim steps that keep operations going. Use **KP-N** ids.
>
> This register is fed by §7 post-incident reviews. When a known problem is finally resolved, **move it to the revision history (§12)** rather than silently deleting it — the operational history stays legible, and "this used to break, here is what we changed" is itself useful knowledge.

| KP-N | Symptom (what the operator observes) | Cause (if known) | Workaround (OPS-N) | Status |
|---|---|---|---|---|
| KP-1 | {{e.g. service hangs after ~7 days uptime}} | {{e.g. a slow resource leak; root cause not yet found}} | {{restart weekly — OPS-1; scheduled in §6}} | open |
| KP-2 | {{e.g. occasional 1% error spike under a dependency hiccup}} | {{upstream provider rate-limit}} | {{retry automatically; no action needed unless ALERT-2 sustained}} | accepted-permanently |
| KP-3 | {{symptom}} | {{cause}} | {{workaround / cross-ref OPS-N}} | planned fix |

---

## 11. Open Questions

> Where operational decisions that are still unresolved are parked so they are not forgotten. Distinct from §10 Known Problems: §10 is about the *running system's* behavior; §11 is about this **manual / process itself** being incomplete (e.g. "no offsite backup target chosen yet," "RTO not yet validated by a real restore test," "no second on-call person").
>
> Use **OQ-N** ids. Optionally split *deferred-with-defaults* from *resolved-for-traceability* if the project wants it (matching the SDD pattern). Resolve and remove — or migrate to §12 — as work progresses.

### 11.1 Open

| OQ-N | Question | Blocked on | Who decides |
|---|---|---|---|
| OQ-1 | {{e.g. no off-host backup target chosen — §8.5 disaster recovery is incomplete}} | {{deciding where off-host copies go}} | {{ROLE-2 owner}} |
| OQ-2 | {{e.g. RTO is stated but never validated by a real restore test}} | {{running a timed OPS-10 in staging}} | {{ROLE-1 operator}} |
| OQ-3 | {{e.g. single on-call person — no coverage if they are unreachable}} | {{whether a second person joins the project}} | {{ROLE-2 owner}} |

### 11.2 Deferred with defaults (optional)

- **OQ-DEF-1** {{Question}} — *default: {{the interim default in effect; revisit if it proves inadequate}}.*

### 11.3 Resolved (recorded for traceability) (optional)

- **OQ-{{N}}** {{Question}}: {{resolution and date}}.

---

## 12. Revision History

> Mandatory. Every substantive change to an operational procedure gets a version bump here — and **retired §10 Known Problems and resolved §11 Open Questions land here** rather than vanishing. For an operations manual, *why a procedure changed* is itself operational knowledge: a procedure that changed after an incident is more trustworthy when the reader can see that lineage (e.g. "OPS-1 gained a verification step after INC-1").

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 System Overview (operational view) — the operator must know what they are keeping alive
- §4 Startup and Shutdown — at minimum normal start (OPS-1) and stop (OPS-2)
- §5 Monitoring — at minimum where the logs are and what "healthy" looks like
- §7 Incident Handling — at minimum a severity scale and a triage checklist
- §8 Backup and Recovery — at minimum the restore procedure (OPS-10) and stated RTO/RPO
- §12 Revision History

**Optional sections** (include if relevant):
- §3 Roles and Responsibilities (collapses to a couple of rows on a solo project — but keep it)
- §6 Routine Operations (include once anything recurs on a schedule)
- §9 Security Operations (include the moment the system holds any secret)
- §10 Known Problems and Workarounds (grows from §7 reviews; empty at first is fine)
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (use these so the manual cross-references cleanly with itself, with logs, and with sibling documents):
- **OPS-N** — operational procedures. The load-bearing prefix: every runnable procedure gets one, so an operator can be told "run OPS-4" and a log entry or alert can cite it.
- **ROLE-N** — roles and responsibilities (§3)
- **ALERT-N** — monitoring alerts/thresholds (§5)
- **INC-N** / SEV-1..n — incident types/severities (§7)
- **RTO / RPO** — recovery objectives (§8; standard ops terms, not invented here)
- **KP-N** — known problems and workarounds (§10)
- **OQ-N** — open questions (§11)

**Tailoring**:
- The section list above is guidance, not a contract. Add/remove subsections as the system needs. Mark deviations explicitly ("skipping §9 because the system holds no secrets yet").
- **Solo developer / small team:** the manual collapses without losing its value. §3 Roles becomes a few rows where one person wears every hat — keep it, because it tells future-you *which authority* you are exercising. The escalation path (§7) may legitimately read "restore from backup (OPS-10) and open a vendor ticket." The point of the whole document on a solo project is that present-you, who holds all the context, writes down the calm decision so that 3am-future-you, who holds none of it, can execute it without re-deriving everything.
- Keep procedures *runnable*: every OPS-N step states its expected result and what to do if the result is wrong. A procedure you cannot follow under stress is not yet finished.
- Revision history is mandatory, and for an ops manual it doubles as the graveyard for resolved Known Problems and Open Questions — move them there, do not delete them.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 26511:2018 and ISO/IEC/IEEE 12207:2017 standards, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
