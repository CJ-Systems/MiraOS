# Installation Guide Template

> **Template purpose:** Lightweight Installation Guide structure inspired by ISO/IEC/IEEE 26511:2018 (managing information for users) and ISO/IEC/IEEE 26514:2022 (designing and developing information for users), plus the SWEBOK Software Construction / User Documentation framing. Use this template when writing the procedure that takes a reader from a defined starting environment to a verified, running installation of {{System Name}}. Replace `{{placeholder}}` content with system-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once the software is installable and you need a repeatable procedure someone other than the author can follow — first install through verified running state, plus upgrade and rollback. The Installation Guide is the "how do I get this onto a machine and prove it works" document. It is distinct from the User Guide (day-to-day use) and the Operations/Admin Guide (ongoing running); see §1.2.
>
> **Companion standard:** ISO/IEC/IEEE 26511:2018 — Systems and software engineering — Requirements for managers of information for users of systems, software, and services; and ISO/IEC/IEEE 26514:2022 — Systems and software engineering — Design and development of information for users.
>
> **Status of this template:** Lightweight skeleton deepened to house depth for the Mira-OS templates pack; follows the SWEBOK Software Construction / User Documentation structure and the outline of ISO/IEC/IEEE 26511:2018 and 26514:2022. Faithful to those outlines but reduced for solo/small-team use. Both standards are paywalled ISO/IEC/IEEE publications — this template paraphrases their structure and quotes no normative text; VERIFY section requirements and any normative wording against the purchased standards before relying on this for regulated, contractual, or safety-critical contexts. Suitable for internal documentation, public build-in-public sharing, and early-stage products.

---

# Installation Guide — {{System Name}}

| Field | Value |
|---|---|
| Document ID | INST-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 26511:2018 + 26514:2022 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Applies to version(s) | {{Software version or version range this guide installs, e.g. 1.4.x}} |
| Target environment(s) | {{Supported OS / platform / architecture this procedure is written for}} |
| Install method | {{Package manager / archive / source build / scripted installer — which path this guide documents}} |
| Estimated install time | {{Rough wall-clock time for a clean install, so the reader can plan}} |
| Privileges required | {{e.g. root / sudo / standard user — the access level needed to complete the procedure}} |

---

## 1. Introduction

> This section orients the reader before any commands are run. It folds the usual Purpose, Scope, Definitions, and References subsections together — the same shape used by the Software Requirements Specification and Software Design Description templates in this pack — so a reader moving between documents finds a familiar layout.

### 1.1 Purpose

> One paragraph. State plainly that this guide enables a reader to install, configure, verify, upgrade, and roll back {{System Name}} — starting from a defined environment and ending at a working, verified installation. Name the audience (who you are writing for and what skills you assume) and what they will be able to do when finished. Beginner note: naming the audience here is not a formality — it sets the level you write at. If you assume "a new operator with standard sysadmin skills," you can say `sudo` without explaining it; if your audience is broader, you cannot.

{{This guide enables a reader to install, configure, verify, and (when needed) upgrade or roll back {{System Name}}, taking them from {{the defined starting environment — e.g. a clean supported OS install}} to a working, verified installation. It is written for {{audience — e.g. a new operator with standard system-administration skills}}. When finished, the reader will have {{System Name}} {{installed, configured for this deployment, and confirmed running via the checks in §6}}.}}

### 1.2 Scope

> State what this guide covers and what it deliberately excludes, then name the single install method and environment it targets. Beginner note — three documents are easy to confuse, and keeping them apart is what stops this one from sprawling into a manual:
> - **Installation Guide** (this document) — getting the system *onto a machine and running for the first time*: install, configure, verify, upgrade, roll back.
> - **User Guide** — *day-to-day use* of the running system.
> - **Operations / Admin Guide** — *ongoing running*: monitoring, backups, scaling, routine maintenance.
> Drawing this boundary is the single most useful thing this section does. When you are tempted to explain how to *use* a feature, that belongs in the User Guide; point there instead.

**In scope:**
- {{First install from {{starting environment}} through a verified running state}}
- {{Configuration required to make the install usable (§5)}}
- {{Verification that the install succeeded (§6)}}
- {{Upgrade from a supported earlier version (§7) and rollback when an install/upgrade fails (§8)}}

**Out of scope (and where to look instead):**
- {{Day-to-day usage}} → User Guide ({{ref}})
- {{Ongoing operation, monitoring, backups}} → Operations / Admin Guide ({{ref}})
- {{Why the system is built the way it is}} → Software Design Description ({{ref}})

**This guide documents one path:** install method **{{e.g. the official package manager}}** on **{{target environment}}**. If other install methods exist (e.g. {{archive, source build}}), they are documented separately at {{ref}} — do not mix methods within one install.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define any term a reader could misread, including the beginner-facing terms this document leans on. Each is also defined plainly at its first real use in a later section; this table is the quick-reference. Add system-specific names, service names, and ports.

| Term | Definition |
|---|---|
| Prerequisite | A condition that must already be true before installation can succeed (hardware capacity, an OS version, an account, a license, an open network port). Listed up front so a failed install does not strand the reader halfway through. |
| Checksum / hash | A short fingerprint (e.g. SHA-256) computed from a file. If the fingerprint you compute matches the one the project published, the file arrived intact and untampered — you installed the real package, not a corrupted or substituted one. |
| Environment variable | A named value the operating system holds and hands to a program when it starts (e.g. `DATABASE_URL`). Software often reads configuration from these instead of from a file. "Setting an environment variable" just means giving that named value before the program runs. |
| Secret | A credential that must stay confidential (password, API key, private key, token). Secrets are configuration too, but their *values* must never appear in this document, in version control, or in logs — record WHERE a secret goes, never WHAT it is. |
| Smoke test | A quick, shallow check run right after install to confirm the system is alive and basically working (it starts, it answers a health check, the version is correct) before any heavier testing. The name comes from hardware: power it on and see if it smokes. |
| Health check | An endpoint or command the system provides that reports whether it is up and ready (e.g. a `/health` URL returning `OK`, or a `status` command). Used both at install-time verification and in ongoing operation. |
| Idempotent | An operation that produces the same end state whether you run it once or many times. A good install/upgrade step is ideally idempotent: re-running it after a partial failure is safe and does not double-apply changes. |
| Rollback | Returning the system to its previous known-good state when an install or upgrade fails. A real rollback covers both the software AND the data — not just removing the new files. |
| Data migration | Transforming existing data so it matches what a new version expects (e.g. adding a column, reshaping records). Migrations are often one-way, which is exactly why upgrade and rollback must be planned together. |
| Acceptance criteria | The explicit, checkable conditions that define "the install succeeded." With them, verification is yes/no per criterion instead of a matter of opinion. |
| {{Service name}} | {{What this named service/process is and the role it plays}} |
| {{Port number}} | {{What listens on this port and whether it is inbound or outbound}} |

### 1.4 References

> List what this guide depends on or points at, categorized for readability (same approach as the SRS template). Include where to obtain the package, the release notes for the target version, the SRS/Design Description if public, any platform-vendor documentation relied on, and the companion standards.

Package and release:
- {{Download / package source location}} — {{where the artifacts in §3 are obtained}}
- {{Release notes for {{target version}}}} — {{breaking changes, known issues}}

Project documents:
- {{SRS-PROJECT-ID-001}} — {{Software Requirements Specification, if public}}
- {{SDD / Design Description}} — {{design rationale, if public}}
- {{User Guide / Operations Guide}} — {{where out-of-scope topics live}}

Platform / vendor:
- {{OS or platform vendor doc relied on — e.g. firewall, service manager}}

External standards:
- ISO/IEC/IEEE 26511:2018 — managing information for users (companion)
- ISO/IEC/IEEE 26514:2022 — designing and developing information for users (companion)

---

## 2. Prerequisites

> A prerequisite is a condition that must already be true before installation can begin. This section turns that idea into a checkable inventory: every prerequisite gets an ID (**PRE-N**) so installation steps and troubleshooting entries can reference it precisely — e.g. "STEP-4 fails → check PRE-3." Group prerequisites by category, and for each give a concrete, verifiable bar *and* a one-line way to check it. Beginner note: confirming every PRE-N up front is what prevents a half-finished install — the worst kind, because a partial install is harder to back out of than no install at all. End the section with a pre-flight checklist the reader can tick off before STEP-1.

| ID | Category | Requirement | How to verify |
|---|---|---|---|
| PRE-1 | Hardware / capacity | CPU: min {{n}} cores / rec {{n}}; RAM: min {{n}} GB / rec {{n}}; Disk: min {{n}} GB free; Architecture: {{e.g. x86-64 / arm64}} | {{`nproc`, `free -h`, `df -h <path>`, `uname -m`}} |
| PRE-2 | Operating system | {{OS name}} version {{supported range, e.g. 22.04–24.04}}. Unsupported: {{explicitly list versions known not to work}} | {{`cat /etc/os-release` or platform equivalent}} |
| PRE-3 | Software dependency | {{Runtime/library/service, e.g. a database}} version {{required range}} present and reachable | {{one-line command, e.g. `<dep> --version`}} |
| PRE-4 | Network — outbound | Outbound access to {{package source host(s) / port(s)}} to fetch artifacts | {{`curl -sI <url>` returns a response}} |
| PRE-5 | Network — inbound | Port {{n}} open for {{purpose}}; {{DNS name resolves / proxy configured if required}} | {{`ss -ltn 'sport = :<n>'`; `getent hosts <name>`}} |
| PRE-6 | Accounts / privileges | {{Access level — ties to the "Privileges required" metadata row, e.g. sudo}}; account {{name/role}} exists | {{`id`, `sudo -v`}} |
| PRE-7 | License / entitlement / API key | {{License key / entitlement / API key}} obtained and available (value handled in §5, not here) | {{confirm you possess it; do NOT paste the value}} |

**Pre-flight checklist** (tick every box before starting §4):

- [ ] PRE-1 capacity meets at least the minimum bar
- [ ] PRE-2 OS is a supported version
- [ ] PRE-3 dependencies present at required versions
- [ ] PRE-4 / PRE-5 network access confirmed (outbound fetch + inbound ports)
- [ ] PRE-6 you have the required privilege level
- [ ] PRE-7 license/entitlement/API key in hand (value kept for §5)

---

## 3. Package Contents

> This section is the manifest: exactly which artifacts the reader will obtain, and how to prove each one arrived intact. A **checksum** (or hash) is a short fingerprint computed from a file — for example with SHA-256. The project publishes the expected fingerprint; you compute the fingerprint of the file you downloaded and compare. A **match** means the file is intact and authentic; a **mismatch** means STOP — do not install a file whose fingerprint is wrong, as it may be corrupted or substituted. Note where to verify a cryptographic signature if the project signs releases. Secrets and license keys are NOT shipped in the package — they are handled in §5 Configuration.

| Item | Version | Description | Source / URL | Checksum (algorithm + value) |
|---|---|---|---|---|
| {{package-name}} | {{x.y.z}} | {{The main installable artifact}} | {{download URL}} | SHA-256: {{published value}} |
| {{checksums file}} | — | {{Published list of expected checksums}} | {{download URL}} | {{signed? see below}} |
| {{signature file (if signed)}} | — | {{Detached signature for the package}} | {{download URL}} | — |

**Verifying integrity (run before installing):**

```
{{# compute the fingerprint of the file you downloaded
sha256sum <downloaded-file>
# then compare its output, character for character, against the published value above}}
```

- **Match** → the file is intact and authentic; proceed.
- **Mismatch** → STOP. Do not install. Re-download from the official source (§1.4); if it still mismatches, treat it as a security concern and see TS-2 in §9.

**Signature verification (if the project signs releases):** {{verify the detached signature against the project's published public key, e.g. `gpg --verify <sig> <file>` — a good signature proves the file came from the holder of that key. Where to obtain and trust the key: {{ref}}.}}

**Not in this package:** secrets and license keys (API keys, passwords, tokens) are never shipped in the artifacts above — you supply them during Configuration (§5). If a secret appears in a package, treat that as a defect, not a feature.

---

## 4. Installation Procedure

> This is the core of the guide: the authoritative ordered procedure. Every step is numbered **STEP-N** and states three things — the **action** (an exact, copy-pasteable command or UI action), the **expected result** (the observable confirmation that the step worked), and **what to do if it differs** (a cross-reference to a Troubleshooting entry, TS-N).
>
> Beginner notes that make the procedure work:
> - Follow the steps **in order** and do not skip ahead. The whole value of a numbered procedure is that you always know which STEP-N you are on, so a failure points at exactly one step.
> - Confirm each **Expected result** before moving on. If a step's result differs, stop and follow its TS-N link rather than pressing forward on a broken foundation.
> - Keep each step **atomic** — one action per STEP-N — so a failure isolates to a single step.
> - Where possible, write steps to be **idempotent**: an idempotent operation reaches the same end state whether you run it once or several times, so re-running it after a partial failure is safe and does not double-apply changes. For each step, note whether re-running is safe.
> - Flag any step that needs **elevated privileges**, and flag clearly — *before* the reader runs it — any step that is **destructive or hard to reverse**.
> - Where the path **branches** by environment or method, make the branch explicit rather than hiding alternatives in prose.

**STEP-0 — Re-confirm prerequisites.** Before anything else, re-run the §2 pre-flight checklist (PRE-1…PRE-7). Do not start mid-air.
- *Action:* re-verify each PRE-N (see §2 "How to verify" column).
- *Expected result:* every checklist box ticked.
- *If different:* resolve the failing PRE-N before continuing; an unmet prerequisite here will surface as a confusing failure later.

| Step | Action (exact command / UI action) | Expected result | Re-run safe? | If different |
|---|---|---|---|---|
| STEP-1 | {{Obtain and verify the package — `sha256sum <file>` per §3}} | {{Checksum matches published value}} | {{Yes — read-only check}} | {{→ TS-2}} |
| STEP-2 | {{Install the package, e.g. `sudo <pkg-mgr> install <package>`}} ⚠ elevated privileges (PRE-6) | {{Installer reports success; binary on PATH: `<cmd> --version`}} | {{Yes — re-install reaches same state}} | {{→ TS-3 (permissions), TS-5 (network)}} |
| STEP-3 | {{Create the service account / directories, e.g. `sudo useradd …` / `mkdir -p <data-dir>`}} | {{Account and directories exist with expected ownership}} | {{Yes — guarded create}} | {{→ TS-3}} |
| STEP-4 | {{Apply configuration — see §5; e.g. write `<config-file>` / export env vars}} | {{Config file present and parses; required CFG-N values set}} | {{Yes — overwrite}} | {{→ TS-6}} |
| STEP-5 | {{Initialize state, e.g. `<cmd> init-db`}} ⚠ may be **destructive** if run against existing data — confirm target is empty first | {{Initialization completes; schema/version recorded}} | {{No — see warning}} | {{→ TS-4, §8 Rollback}} |
| STEP-6 | {{Start the service, e.g. `sudo systemctl enable --now <service>`}} | {{Service active/running; listening on port {{n}} (PRE-5)}} | {{Yes}} | {{→ TS-4, TS-5}} |

> **Branch example (delete if single-path).** If the install differs by environment, split the branch explicitly:
> - **Branch A — {{environment / method A}}:** {{steps or deltas}}
> - **Branch B — {{environment / method B}}:** {{steps or deltas}}
> Re-converge at: {{the STEP-N where both branches rejoin}}.

When all steps report their Expected result, the software is installed and running. **It is not yet verified** — proceed to §6 before declaring the install complete.

---

## 5. Configuration

> Configuration is what turns a generic install into THIS deployment. Getting it wrong is the most common cause of an install that "completes" but does not work. This section is a structured parameter reference: each parameter gets an ID (**CFG-N**) so steps and troubleshooting can point at it precisely.
>
> Two beginner terms used here on first real use:
> - **Environment variable** — a named value the operating system hands to a program when it starts (e.g. `DATABASE_URL`). Many programs read configuration from these instead of a file; "setting" one just means providing that named value before the program runs.
> - **Secret** — a credential that must stay confidential (password, API key, private key, token). Secrets are configuration, but their VALUES must never be written into this document, committed to version control, or printed to logs. Record only WHERE each secret goes.
>
> After configuring, write down the chosen **non-secret** values somewhere durable — you will need them for the upgrade and rollback procedures (§7, §8).

| ID | Name | Where it's set | Required? | Default | Allowed values / format | Description |
|---|---|---|---|---|---|---|
| CFG-1 | {{LISTEN_PORT}} | {{env var / `<config-file>` key}} | {{Yes}} | {{8080}} | {{integer 1–65535}} | {{Port the service listens on (must match PRE-5)}} |
| CFG-2 | {{DATA_DIR}} | {{`<config-file>` key}} | {{Yes}} | {{/var/lib/{{system}}}} | {{absolute path, writable by service account}} | {{Where persistent data lives (back this up — §7/§8)}} |
| CFG-3 | {{LOG_LEVEL}} | {{env var}} | {{No}} | {{info}} | {{debug \| info \| warn \| error}} | {{Verbosity of startup and runtime logs}} |
| CFG-4 | {{DATABASE_URL}} | {{env var}} | {{Yes}} | {{none}} | {{connection string}} | {{Where the system finds its database (PRE-3)}} |

**Secrets (record WHERE, never WHAT):**

| Secret needed | Goes into | NOT into |
|---|---|---|
| {{Database password}} | {{secret store / env var injected at start / file mode 600}} | this document, version control, logs |
| {{API key (PRE-7)}} | {{secret store / env var}} | this document, version control, logs |

> If a "completed" install does not work, suspect a wrong CFG-N value first (most common cause), then a missing secret, then a prerequisite. Verify with §6 before troubleshooting blindly.

---

## 6. Installation Verification

> "Is it installed?" should be answered by a set of yes/no checks, not by a feeling. This section lists the **acceptance criteria** — the explicit, checkable conditions that define a successful install — as numbered **VER-N** checks. Three beginner terms: a **smoke test** is a quick, shallow "does it even turn on?" check run right after install; a **health check** is an endpoint or command the system provides that reports whether it is up and ready; **acceptance criteria** are exactly these yes/no conditions. **Every VER-N must pass before the install is declared complete.** If a VER-N fails, do not declare success — go to §9 Troubleshooting, and if it cannot be resolved, §8 Rollback.

| ID | Check | Exact command / action | Pass condition |
|---|---|---|---|
| VER-1 | Smoke test — does it start? | {{`sudo systemctl status <service>` / `<cmd> status`}} | {{Service is `active (running)` with no restart loop}} |
| VER-2 | Health check — is it ready? | {{`curl -fsS http://localhost:{{port}}/health`}} | {{Returns `OK` / HTTP 200}} |
| VER-3 | Version check — right version? | {{`<cmd> --version`}} | {{Matches "Applies to version(s)" / the version installed in STEP-2}} |
| VER-4 | Log inspection — clean startup? | {{`journalctl -u <service> --since "5 min ago"` / `tail <log>`}} | {{No `ERROR`/`FATAL` lines at startup}} |
| VER-5 | End-to-end — one real operation | {{One minimal real action, e.g. create then read a test record, then delete it}} | {{Operation succeeds and returns expected result}} |

**Acceptance:** the install is complete only when **VER-1 through VER-5 all pass**. Record the result:

| VER-N | Result (Pass/Fail) | Notes |
|---|---|---|
| VER-1 | {{ }} | {{ }} |
| ... | {{ }} | {{ }} |

**If any VER-N fails:** match the symptom to a §9 TS-N entry and resolve it, then re-run the failed VER-N. If it cannot be made to pass, the install has not succeeded — follow §8 Rollback to return to the previous known-good state.

---

## 7. Upgrade Procedure

> Upgrading is installing a newer version over an existing one. The hard part is **data migration** — transforming existing data so it matches what the new version expects (adding a column, reshaping records). Migrations are often **one-way**, which is the whole reason upgrade and rollback are planned together: if you migrate before backing up, there may be nothing to roll back to. The **pre-upgrade backup is non-skippable** — it is what makes §8 Rollback possible. Reuse the §6 VER-N checks for post-upgrade verification, and follow the same STEP-N discipline as §4.

**Supported upgrade paths:**

| From version | To version | Notes (intermediate version required?) |
|---|---|---|
| {{1.3.x}} | {{1.4.x}} | {{Direct}} |
| {{1.2.x}} | {{1.4.x}} | {{Must upgrade to {{1.3.x}} first, then to {{1.4.x}}}} |

**Compatibility / breaking changes:** {{list config keys removed/renamed (which CFG-N), behavior changes, dropped platform support — link release notes from §1.4}}.

**Upgrade steps** (same discipline as §4 — STEP-N, expected result, re-run safety):

| Step | Action | Expected result | Re-run safe? | If different |
|---|---|---|---|---|
| STEP-U1 | {{**Take the backup FIRST** — software artifacts + all data (CFG-2 DATA_DIR + database)}} ⚠ do not skip | {{Backup exists, is complete, and is restorable (test-list it)}} | {{Yes}} | {{Stop — do not upgrade without a verified backup}} |
| STEP-U2 | {{Stop the service, e.g. `sudo systemctl stop <service>`}} | {{Service stopped; nothing writing to data}} | {{Yes}} | {{→ TS-4}} |
| STEP-U3 | {{Install the new version (as in STEP-2, new artifact)}} | {{New version on PATH: `<cmd> --version`}} | {{Yes}} | {{→ TS-3, TS-5}} |
| STEP-U4 | {{Run data migration, e.g. `<cmd> migrate`}} ⚠ often **one-way** | {{Migration completes; new schema/version recorded; duration ≈ {{estimate}}}} | {{No — one-way}} | {{→ §8 Rollback}} |
| STEP-U5 | {{Start the service (as in STEP-6)}} | {{Service running on new version}} | {{Yes}} | {{→ TS-4}} |

**Post-upgrade verification:** re-run VER-1 through VER-5 (§6). The upgrade is complete only when all pass on the new version.

---

## 8. Rollback

> **Rollback** is returning the system to its previous known-good state when an install or upgrade fails. The central point — and the one beginners miss — is that a real rollback covers **both software AND data**. Uninstalling the new binaries is not enough if STEP-U4's migration already changed the data: you must also restore the data from the backup. That is why §4/§7 insist on taking the backup *before* migrating — **rollback is only as good as that backup.** Note also that there may be a window after which rollback is no longer clean (once new data has accumulated under the new version), so decide quickly.

**Rollback triggers — when to roll back instead of continuing to troubleshoot:**
- {{VER-2 (health) or VER-5 (end-to-end) fails after install/upgrade and the cause is not a quick CFG-N fix}}
- {{Data corruption or migration error observed after STEP-U4}}
- {{The service will not stay up (restart loop) and §9 has no matching TS-N}}

**Rollback steps:**

| Step | Action | Expected result | If different |
|---|---|---|---|
| STEP-R1 | {{Stop the service}} | {{Service stopped; nothing writing to data}} | {{→ TS-4}} |
| STEP-R2 | {{Restore software — reinstall the previous version's artifacts}} | {{Previous version on PATH: `<cmd> --version`}} | {{→ TS-3}} |
| STEP-R3 | {{Restore data from the pre-install / pre-upgrade backup (STEP-U1)}} | {{Data matches the pre-upgrade state}} | {{If no/incomplete backup, rollback is not possible — escalate (§9)}} |
| STEP-R4 | {{Start the service}} | {{Service running on previous version}} | {{→ TS-4}} |

**Post-rollback verification:** re-run VER-1 through VER-5 (§6) and confirm they pass as they did before the failed change — this proves you are back to the previous known-good state.

**Point of no clean return:** {{after {{condition — e.g. the new version has accepted live writes for more than {{duration}}}}, rolling back would discard data created since the upgrade. Past this point, prefer fixing forward over rolling back, and consult {{escalation path}}.}}

---

## 9. Troubleshooting

> This is a diagnosable reference, not a list of complaints. Each entry is a **TS-N**: the symptom the reader actually observes, its likely cause, the resolution, and a back-reference to the PRE-N / STEP-N / VER-N it relates to. Beginner habit to build: **match the symptom you actually see to a TS-N entry and follow its resolution** — do not guess and thrash. Because each entry points back at the step that produced it, you can resume the procedure from exactly the right place. If no entry matches, gather diagnostics (logs, version, environment) and escalate per the note below.

| ID | Symptom (what you observe) | Likely cause | Resolution | Related |
|---|---|---|---|---|
| TS-1 | {{An early step fails for no obvious reason}} | {{Unmet prerequisite}} | {{Re-run the §2 checklist; fix the failing PRE-N, then resume}} | PRE-1…PRE-7, STEP-0 |
| TS-2 | {{Checksum/signature does not match}} | {{Corrupted or substituted download}} | {{Do NOT install. Re-download from §1.4 source; if it still mismatches, treat as a security concern and escalate}} | §3, STEP-1 |
| TS-3 | {{"Permission denied" / cannot write}} | {{Insufficient privileges or wrong ownership}} | {{Run the step with the privilege level in PRE-6; check directory ownership from STEP-3}} | PRE-6, STEP-2/3, STEP-R2 |
| TS-4 | {{Service will not start / "address already in use"}} | {{Port in use, or bad config}} | {{Check CFG-1 port vs PRE-5; `ss -ltn`; free the port or change CFG-1; inspect logs (VER-4)}} | PRE-5, CFG-1, STEP-6, VER-1/4 |
| TS-5 | {{Download/fetch times out}} | {{Outbound network or proxy/DNS issue}} | {{Verify PRE-4; configure proxy/DNS; retry the step (idempotent)}} | PRE-4/5, STEP-2 |
| TS-6 | {{Install "completes" but health check (VER-2) fails}} | {{Wrong CFG-N value or missing secret}} | {{Re-check required CFG-N (§5) and that each secret reached its destination; correct and restart}} | §5 CFG-N, VER-2/5 |

**Where to find logs / gather diagnostics:** {{log location(s); `<cmd> version`; how to dump effective config (with secrets redacted)}}.

**If no TS-N matches / how to escalate:** {{collect the failing VER-N, the relevant log excerpt, `<cmd> --version`, and OS/platform info; file a report at {{issue tracker / support channel}} with that bundle attached. Never paste secret values into a report.}}

---

## 10. Open Questions

> An honest Installation Guide names what it has NOT yet verified, so a reader knows which parts of the procedure are solid and which are provisional. Track unresolved items about the procedure itself with **OQ-N**: an environment not yet validated, an install method still being decided, a prerequisite range not yet confirmed, a rollback path not yet tested. For each, note what is blocking resolution and who must decide. Resolve and remove entries as they close (record the resolution in the Revision History).

- **OQ-1:** {{Question about the procedure — e.g. "Has the upgrade path 1.2.x → 1.4.x been tested end-to-end?"}} — {{what's blocking; who must decide/test}}
- **OQ-2:** {{e.g. "Is the rollback in §8 verified, or written-but-untested?"}} — {{blocker; owner}}
- **OQ-3:** {{e.g. "Confirm PRE-2 supported OS range on {{new platform}}"}} — {{blocker; owner}}

---

## 11. Revision History

> Mandatory final section, same discipline as the SRS and SDD templates. Record every substantive change with a version bump. Beginner note: for an Installation Guide this is especially load-bearing — the guide is tied to the software versions it installs, so a change to supported versions (the "Applies to version(s)" metadata row), to prerequisites, or to the steps each gets its own row. The Approval column records who signed the change off (ties to the sign-off block in the metadata table).

| Version | Date | Author | Description of Change | Approval |
|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft | {{Approver}} |
| {{0.2}} | {{YYYY-MM-DD}} | {{Author}} | {{e.g. Added support for {{version}}; updated PRE-3 dependency range}} | {{Approver}} |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — purpose, scope boundary, definitions, references)
- §2 Prerequisites (the PRE-N inventory + pre-flight checklist)
- §3 Package Contents (with checksum verification)
- §4 Installation Procedure (the STEP-N procedure)
- §5 Configuration (at minimum the required CFG-N parameters and where secrets go)
- §6 Installation Verification (the VER-N acceptance criteria)
- §11 Revision History

**Optional sections** (include if relevant):
- §7 Upgrade Procedure (omit for a first release with no prior version to upgrade from; add it the moment a second version exists)
- §8 Rollback (strongly recommended whenever §5 STEP-5 / §7 STEP-U4 touch data; omit only for trivially reinstallable, stateless software)
- §9 Troubleshooting (start small — seed it with the failures you hit while writing §4 — and grow it from real reports)
- §10 Open Questions (track elsewhere if you prefer, but do track them — see the honesty note in the section)

**Tailoring:**
- The section list is guidance, not a contract. Add a §-level branch for each distinct install method if you genuinely support several, or split them into separate guides (preferred — §1.2 documents one path per guide).
- **Identifier conventions** (use these so this guide cross-references cleanly with sibling documents): **PRE-N** prerequisites, **STEP-N** installation/upgrade/rollback steps (STEP-U*/STEP-R* for the upgrade/rollback variants), **CFG-N** configuration parameters, **VER-N** verification checks, **TS-N** troubleshooting entries, **OQ-N** open questions. These let a step, its inputs, and its checks be traced to one another — and let the procedure trace back to requirements (SRS) and design (SDD) via their IDs.
- **Solo developer / small team collapse:** keep §2 (PRE-N), §4 (STEP-N), §6 (VER-N), and §11 — these are the irreducible core (what must be true, what to do, how to know it worked, what changed). The sign-off block collapses to one name: "Prepared / reviewed / approved by {{you}}." §7 and §8 can start as a single line each ("no prior version yet" / "to restore: reinstall {{x.y.z}} and restore the {{DATA_DIR}} backup") and grow into full procedures when a second version ships. §9 grows from real failures rather than being written up front. Keeping the IDs even at this scale costs little and pays off the first time you need to point at "the step that failed."
- Keep this guide focused on getting the system installed and verified. Day-to-day usage belongs in the User Guide; ongoing operation in the Operations/Admin Guide; design rationale in the Software Design Description.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 26511:2018 and 26514:2022 (purchased copies), not this lightweight version. This template paraphrases their structure and reproduces no normative text; verify section requirements and any normative wording against the standards before relying on this for regulated, contractual, or safety-critical contexts.
