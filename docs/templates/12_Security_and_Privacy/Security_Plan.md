# Information Security Plan and Statement of Applicability Template

> **Template purpose:** Lightweight Information Security Plan and Statement of Applicability (SoA) structure inspired by ISO/IEC 27001:2022 and ISO/IEC 27002:2022, with control selection drawing on the publicly available NIST SP 800-53 Rev. 5 catalog and ISO/IEC 27034 (the application-security series) for app/agent-specific controls. Use this template when you need one documented place that records what a system protects, the risks it faces, and the security controls it actually runs. Replace `{{placeholder}}` content with system-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Any system holding data, credentials, or behavior worth protecting — even a solo-operated one. Start a plan as soon as the system has enough shape to name its assets and likely threats. The plan pairs with the SRS (which states what the system does) and the SDD/Architecture (which states how) — this document states how the system stays *secure* while doing it. Revisit it on a cadence and after every major change or incident.
>
> **Companion standard:** ISO/IEC 27001:2022 + ISO/IEC 27002:2022 + NIST SP 800-53 Rev. 5; ISO/IEC 27034 (series) for application-security controls (lightweight).
>
> **Status of this template:** Lightweight skeleton assembled from public summaries of the companion standards (ISO/IEC 27001:2022, ISO/IEC 27002:2022, ISO/IEC 27034 series) and the publicly available NIST SP 800-53 Rev. 5 control catalog. The ISO/IEC standards are paywalled and not reproduced here — section names and intent are paraphrased from public sources, so verify the SoA structure, clause references, and Annex A control set against the full purchased standard before relying on this for certification or any regulated/audited context. NIST SP 800-53 Rev. 5 is U.S. public-domain and may be cited and quoted directly. Suitable for solo/small-team and internal use; not a substitute for the normative standards in a certification effort.

---

# Information Security Plan and Statement of Applicability — {{System Name}}

| Field | Value |
|---|---|
| Document ID | SP-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC 27001:2022 + ISO/IEC 27002:2022 + NIST SP 800-53 Rev. 5 (lightweight) |
| Owner | {{Project name or security owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Classification | {{Public / Internal / Confidential}} (this plan often references sensitive controls; mark appropriately) |
| ISMS Scope | {{One-line boundary: which systems, data, and locations this plan covers}} |
| Risk Owner | {{Person/role accountable for accepting residual risk}} |
| Review Cadence | {{e.g., Reviewed quarterly + after any major change or incident}} |
| Control Baseline | {{ISO/IEC 27002:2022 Annex A / NIST 800-53 Low/Moderate/High / custom}} |

---

## 1. Introduction

> This section frames the whole document: why it exists, what it covers, the vocabulary a beginner needs, and what other documents it leans on. Keep it to about a page — this is the setup, not the substance.
>
> A few formal terms appear throughout this plan; define them once here so the rest reads cleanly:
> - **ISMS (Information Security Management System):** the documented set of policies, processes, and controls a project uses to manage information-security risk in a *repeatable* way — not security done by reflex each time, but security done the same way every time and written down. ISO/IEC 27001 defines what an ISMS must contain.
> - **Statement of Applicability (SoA):** the central ISO 27001 artifact — a list of every candidate control, whether you applied it, why, and its current status. It is the bridge between your risk assessment (what could go wrong) and the controls you actually run (what you do about it).
> - **Control:** a safeguard or countermeasure — technical, procedural, or organizational — that reduces a risk. ISO/IEC 27002 and NIST SP 800-53 are *catalogs* of pre-named controls you select from rather than inventing your own.
> - **CIA triad:** the three properties security protects — **Confidentiality** (only authorized parties see data), **Integrity** (data is not altered improperly), **Availability** (data and systems are usable when needed). Almost every security requirement traces back to one of these three.
> - **Asset:** anything worth protecting — data, credentials, code, hardware, services, or reputation. Controls protect assets; you cannot pick controls sensibly until you know what the assets are.
> - **Residual risk:** the risk that remains *after* controls are applied. It is never zero; the risk owner formally accepts whatever is left.

### 1.1 Purpose

> One paragraph. Establish that this is the single place that defines the security plan and Statement of Applicability for {{System Name}}: what is protected, the risks faced, and the controls run.

{{This document defines the information-security management plan and the Statement of Applicability for {{System Name}}. It records the assets we protect, the risks they face, the controls we have selected to manage those risks, and the status of each control. It is the security companion to the system's SRS (what the system does) and SDD/Architecture (how it is built).}}

### 1.2 Scope

> Define what is covered and what is explicitly excluded. Name the systems, data, environments, and boundaries inside scope, and call out anything deliberately left out so a reader is never unsure whether a thing is "in" or "out."

In scope:
- {{Systems / services covered — e.g., the {{System Name}} application and its single host}}
- {{Data covered — e.g., user data, credentials, configuration, backups}}
- {{Environments covered — e.g., production host only / dev + prod}}

Out of scope (handled elsewhere or deliberately excluded):
- {{What is out — e.g., the upstream LLM provider's own security posture (covered by their compliance), end-user devices, physical premises security}}

### 1.3 Definitions and Acronyms

> Define every term a beginner needs to read the rest without guessing. The core terms below are load-bearing — keep them even if you trim the rest. A reader who understands these can read the whole document.

| Term | Definition |
|---|---|
| ISMS | Information Security Management System — the documented, repeatable set of policies, processes, and controls used to manage information-security risk. |
| SoA | Statement of Applicability — the list of every candidate control, whether it applies, why, and its status (see §7). |
| Control | A safeguard (technical, procedural, or organizational) that reduces a risk; selected from a catalog such as ISO/IEC 27002 or NIST SP 800-53. |
| CIA triad | Confidentiality, Integrity, Availability — the three properties security protects. |
| Asset | Anything worth protecting: data, credentials, code, hardware, services, reputation. |
| Threat | Who or what could cause harm — an attacker, a bug, a disk failure. |
| Vulnerability | A weakness a threat could exploit. Risk exists where a threat can reach a vulnerability that affects an asset. |
| Risk | The chance that a threat exploits a vulnerability and harms an asset; ranked as **likelihood × impact**. |
| Residual risk | The risk left over after controls are applied; never zero, and formally accepted by the risk owner. |
| {{Project-specific term}} | {{Definition}} |

### 1.4 References

> List the standards, related specs, decision records, and policies this plan depends on or points to. Categorize for readability so a reader can find the right thing fast.

Companion standards:
- ISO/IEC 27001:2022 — Information security management systems — Requirements (the ISMS + SoA requirements).
- ISO/IEC 27002:2022 — Information security controls (the control catalog / Annex A reference).
- ISO/IEC 27034 (series) — Application security.
- NIST SP 800-53 Rev. 5 — Security and Privacy Controls for Information Systems and Organizations (public-domain control catalog).

Related project documents:
- {{path/to/srs.md}} — Software Requirements Specification (security requirements may originate here).
- {{path/to/architecture.md}} or {{path/to/sdd.md}} — design context for what is being secured.
- ADR-NNNN — {{security-relevant architecture decision}}.

Policies this plan depends on:
- {{path/to/policy}} — {{e.g., access-control policy, backup policy, acceptable-use}}

---

## 2. Security Objectives and Policy

> This section states, in plain language, what "secure" means for {{System Name}} and the standing commitments the system operates under. Frame the objectives against the CIA triad — Confidentiality, Integrity, Availability — so each one names which property it protects. These objectives are the "why" that every later control should be able to trace back to. A control with no objective behind it is probably ceremony; an objective with no control behind it is probably a gap.

### 2.1 Security Objectives

> State the high-level goals. Keep them outcome-shaped ("X stays Y"), not control-shaped (controls come later in the SoA). Tag each with the CIA property it serves.

| ID | Objective | CIA property |
|---|---|---|
| OBJ-1 | {{e.g., User and conversation data is readable only by the owner and the system itself.}} | Confidentiality |
| OBJ-2 | {{e.g., System state and configuration cannot be silently tampered with.}} | Integrity |
| OBJ-3 | {{e.g., The system recovers to a known-good state within {{N}} after a host failure.}} | Availability |
| OBJ-N | {{Objective}} | {{C / I / A}} |

### 2.2 Policy Commitments

> The guiding commitments the system operates under — the rules that hold regardless of which specific control is in play. Phrase them as durable principles. Use SR-N here if a commitment is also a testable security requirement that later controls must satisfy.

- **{{Least privilege}}** — {{every identity, process, and credential gets the minimum access needed and no more.}}
- **{{Secrets never in source}}** — {{credentials, tokens, and keys live outside version control; the repository is assumed to be readable by others.}}
- **{{State isolation}}** — {{state belonging to one identity/tenant is not readable or writable by another.}}
- **SR-1** {{Security requirement phrased as a commitment, e.g., "All access to {{asset}} requires authentication."}} — traces to OBJ-{{N}}.
- **{{Commitment}}** — {{description}}

---

## 3. ISMS Scope and Context

> ISO 27001 Clause 4 asks you to draw the management boundary precisely and to understand the world the system lives in. This section does both. The boundary matters because the SoA only has to cover what is *inside* it — drawing it too wide creates obligations you cannot meet; drawing it too narrow leaves real assets unprotected. "Interested parties" is just the standard's phrase for everyone who cares about the system's security — users, the operator, any third parties. "Context" is the set of external and internal conditions that make some controls realistic and others not.

### 3.1 Boundary

> Name what is inside the management scope and what is outside, concretely. Systems, services, repositories, data stores, hosts, and people — list them so there is no ambiguity at audit time.

| Inside scope | Outside scope |
|---|---|
| {{e.g., the {{System Name}} app process}} | {{e.g., the OS vendor's update infrastructure}} |
| {{e.g., the production host {{hostname}}}} | {{e.g., the upstream model provider's servers}} |
| {{e.g., the project repository and its backups}} | {{e.g., third-party libraries' own development}} |
| {{e.g., the operator (one person)}} | {{e.g., end-user personal devices}} |

### 3.2 Interested Parties

> Everyone who has a stake in the system's security and what they expect of it. For a solo system this is short; name it anyway.

| Party | What they expect |
|---|---|
| {{Owner / operator}} | {{e.g., the system does not leak their data or get hijacked}} |
| {{Users}} | {{e.g., their data is private and the service is available}} |
| {{Third parties / providers}} | {{e.g., the system respects their API terms and rate limits}} |

### 3.3 External and Internal Context

> The conditions that shape what controls are realistic. Regulatory expectations, the deployment environment, and hard constraints all belong here. Be honest about constraints — a control you cannot actually run should be marked Not Applicable in the SoA with this context as the reason, not pretended into existence.

- **Regulatory / contractual:** {{e.g., no formal regulation; provider API terms apply; no PII of EU residents → GDPR not triggered (confirm).}}
- **Deployment environment:** {{e.g., single headless host, no GUI; no containerization; remote SSH administration only.}}
- **Operating constraints:** {{e.g., solo-operated — no separation-of-duties possible; backups are local + one offsite copy; limited budget for paid security tooling.}}

---

## 4. Assets and Data Classification

> You cannot select controls sensibly until you know what you are protecting and how sensitive it is — so this section lists the assets and grades each one. An **asset** is anything worth protecting: data, credentials, code, hardware, services, or reputation. **Classification** is a sensitivity label (e.g., Public / Internal / Confidential) that tells you how much protection an asset warrants — a public landing page and a private API key both matter, but not equally. For each asset, note which CIA properties matter most: a backup's *availability* is paramount; a credential's *confidentiality* is. This table feeds directly into the risk assessment in §5 — every risk should attach to an asset listed here.

| Asset ID | Asset | Classification | Primary CIA concern | Notes / location |
|---|---|---|---|---|
| AST-1 | {{e.g., API tokens / credentials}} | Confidential | Confidentiality | {{e.g., stored in {{secrets file/manager}}, never in repo}} |
| AST-2 | {{e.g., system state / config files}} | Confidential | Integrity, Confidentiality | {{e.g., on host at {{path}}}} |
| AST-3 | {{e.g., source code}} | Internal | Integrity | {{e.g., version-controlled; repo may be public}} |
| AST-4 | {{e.g., user / conversation data}} | Confidential | Confidentiality | {{e.g., {{datastore}}}} |
| AST-5 | {{e.g., embeddings / derived data}} | Internal | Confidentiality | {{e.g., reconstructable from source data}} |
| AST-6 | {{e.g., backups}} | Confidential | Availability, Integrity | {{e.g., local + {{offsite}}}} |
| AST-7 | {{e.g., the host / infrastructure}} | Internal | Availability | {{e.g., single host {{hostname}}}} |
| AST-N | {{Asset}} | {{Public / Internal / Confidential}} | {{C / I / A}} | {{Notes}} |

> **Classification key (tailor to your needs):**
> - **Public** — disclosure causes no harm; may already be published.
> - **Internal** — disclosure is undesirable but not damaging; not for outsiders by default.
> - **Confidential** — disclosure, loss, or tampering causes real harm to the owner or users.

---

## 5. Risk Assessment

> This section is the evidence base for every control you later select — it identifies what could actually go wrong with the assets in §4. The method below is **qualitative**, which simply means it ranks risks by judgment (Low / Medium / High) rather than by precise numbers; that is fine and normal for a lightweight plan, as long as the scoring is *reproducible* — another person should reach roughly the same ranking from the same facts.
>
> For each risk, name four things:
> - the **threat** (who or what could cause harm — an attacker, a bug, a disk failure),
> - the **vulnerability** it would exploit (the weakness — an unpatched library, a reused password, no backup),
> - the **affected asset(s)** from §4, and
> - the **likelihood** and **impact**, whose product (likelihood × impact) gives a simple ranking so risks can be compared on one axis.
>
> A risk only exists where a threat can reach a vulnerability that affects an asset — if any of the three is missing, it is not a risk for this system.

### 5.1 Scoring Method

> State the scale you use so the scoring is reproducible. The simple 3×3 below is enough for most small systems.

- **Likelihood:** Low (unlikely this year) / Medium (plausible) / High (expected without action).
- **Impact:** Low (minor inconvenience) / Medium (real harm, recoverable) / High (severe or unrecoverable harm to owner/users).
- **Exposure = Likelihood × Impact**, banded: e.g., High×High and High×Medium → **High**; Medium×Medium → **Medium**; anything ×Low or Low× → **Low**. Tailor the bands to taste, but write them down.

### 5.2 Identified Risks

| Risk ID | Threat | Vulnerability | Affected asset(s) | Likelihood | Impact | Exposure |
|---|---|---|---|---|---|---|
| RISK-1 | {{e.g., credential theft via leaked repo}} | {{e.g., secret accidentally committed}} | AST-1 | {{Med}} | {{High}} | {{High}} |
| RISK-2 | {{e.g., dependency supply-chain compromise}} | {{e.g., unpinned/unaudited package}} | AST-3, AST-7 | {{Low}} | {{High}} | {{Med}} |
| RISK-3 | {{e.g., host disk failure}} | {{e.g., single copy of state}} | AST-2, AST-6 | {{Med}} | {{Med}} | {{Med}} |
| RISK-4 | {{e.g., prompt injection / untrusted input}} | {{e.g., agent acts on attacker-controlled text}} | AST-4 | {{Med}} | {{Med}} | {{Med}} |
| RISK-5 | {{e.g., unauthorized remote access}} | {{e.g., weak/exposed SSH config}} | AST-7 | {{Low}} | {{High}} | {{Med}} |
| RISK-N | {{Threat}} | {{Vulnerability}} | {{AST-N}} | {{L/M/H}} | {{L/M/H}} | {{L/M/H}} |

---

## 6. Risk Treatment Plan

> A risk assessment that does not lead to decisions is just a worry list. This section is the explicit decision log that turns each RISK-N into action, recorded as a treatment TR-N. There are four standard treatment choices:
> - **Reduce (mitigate)** — apply controls that lower the likelihood or impact. This is the common case; point at the CTRL-N rows in §7 that do the reducing.
> - **Accept** — decide the residual risk is tolerable and live with it. Record *who* accepts it (the risk owner) and *why* — acceptance is a deliberate, owned decision, not an oversight.
> - **Avoid** — change the system so the risk no longer applies (e.g., stop collecting the data that was at risk).
> - **Transfer / share** — shift some of the risk to another party (e.g., insurance, or relying on a provider's certified controls). Note that transfer rarely removes accountability — you still own the outcome to your users.

| Treatment ID | Risk | Decision | Rationale | Controls (if reduce) | Residual accepted by |
|---|---|---|---|---|---|
| TR-1 | RISK-1 | Reduce | {{e.g., keep secrets out of repo + scan history}} | CTRL-1, CTRL-2 | — |
| TR-2 | RISK-2 | Reduce | {{e.g., pin + periodically audit dependencies}} | CTRL-3 | — |
| TR-3 | RISK-3 | Reduce | {{e.g., automated offsite backups + restore test}} | CTRL-4 | — |
| TR-4 | RISK-4 | Reduce | {{e.g., treat all external text as untrusted; constrain tool permissions}} | CTRL-5, CTRL-8 | — |
| TR-5 | RISK-5 | Accept | {{e.g., key-only SSH on a non-standard port is judged sufficient; full bastion is out of budget}} | — | {{Risk Owner, {{YYYY-MM-DD}}}} |
| TR-N | RISK-N | {{Reduce / Accept / Avoid / Transfer}} | {{Rationale}} | {{CTRL-N or —}} | {{Owner + date, if accepted}} |

---

## 7. Statement of Applicability (Selected Controls)

> This is the heart of the plan and the one artifact ISO 27001 most cares about. The **Statement of Applicability** is a table with one row per candidate control, recording for each: where the control comes from, whether you apply it, *why*, how it is implemented here, and its current status. It is the bridge from the risk assessment (§5–6) to what the system actually runs.
>
> Two beginner notes that matter:
> - **Cite the source, do not reinvent.** Each control should reference its catalog entry — an ISO/IEC 27002:2022 clause (e.g., 5.x organizational, 6.x people, 7.x physical, 8.x technological) *or* a NIST SP 800-53 Rev. 5 identifier (e.g., AC-3, AU-2, CP-9, SI-3). NIST IDs are public and may be quoted directly; ISO clause text is paywalled, so reference the clause *number* and paraphrase its intent rather than copying the standard's wording.
> - **Record what you did NOT do, too.** Include the Not-Applicable rows with reasons. An auditor — and future-you — needs to see that you *considered* a control and made a deliberate choice, not that you forgot it. "Not applicable: no physical premises; host is a cloud VM" is a perfectly good SoA entry.
>
> Justify each Applicable control by tracing it to a RISK-N (the risk it reduces) or an SR-N (the requirement it satisfies). Status moves Planned → Implemented → Verified as work proceeds; the "Verified" status only earns its name once §9 confirms it.

| Control ID | Source reference | Control (short name) | Applicable? | Justification | Implementation notes for {{System Name}} | Status |
|---|---|---|---|---|---|---|
| CTRL-1 | NIST 800-53 SC-12 / ISO 27002 §8.24 | Cryptographic key & secret management | Yes | RISK-1, SR-1 | {{Secrets in {{secrets manager/file}} outside repo; least-privilege scopes; rotation per §9}} | {{Implemented}} |
| CTRL-2 | NIST 800-53 SI-7 / ISO 27002 §8.x | Secret scanning / integrity check on commits | Yes | RISK-1 | {{Pre-commit + history scan with {{tool}}}} | {{Planned}} |
| CTRL-3 | NIST 800-53 SA-12 / ISO 27002 §8.x | Supply-chain / dependency hygiene | Yes | RISK-2 | {{Pin versions; periodic audit with {{tool}}}} | {{Planned}} |
| CTRL-4 | NIST 800-53 CP-9 / ISO 27002 §8.13 | Backup & restore | Yes | RISK-3 | {{Automated daily backup; offsite copy; quarterly restore test}} | {{Implemented}} |
| CTRL-5 | NIST 800-53 SI-10 / ISO 27034 | Input validation / untrusted-input handling | Yes | RISK-4, SR-2 | {{All external text treated as untrusted; see §8}} | {{Planned}} |
| CTRL-6 | NIST 800-53 AC-3 / ISO 27002 §5.15 | Access control / least privilege | Yes | OBJ-1, RISK-5 | {{Key-only auth; per-identity scopes}} | {{Implemented}} |
| CTRL-7 | NIST 800-53 AU-2 / ISO 27002 §8.15 | Logging | Yes | §9 | {{Security-relevant events logged to {{location}}}} | {{Planned}} |
| CTRL-8 | ISO 27034 / NIST 800-53 CM-7 | Least-functionality / tool-permission scoping (agent) | Yes | RISK-4 | {{Agent tool permissions explicitly allow-listed; see §8}} | {{Planned}} |
| CTRL-N | {{Catalog ref}} | {{Control}} | No | {{Why not applicable}} | {{e.g., "No physical premises — host is a managed VM; physical controls are the provider's"}} | N/A |

---

## 8. Application Security Controls

> §7 covers security in general; this section zooms into the controls specific to the *application or agent itself* — the surface that custom code and AI behavior create. It draws on ISO/IEC 27034 (the application-security series), which is about building security into the software rather than bolting it on around the edges. For an AI-agent system there are extra surfaces a generic plan misses: what tools the agent may call, what state it can read or write, and how identities are kept apart.
>
> Any *new* security requirement this section introduces gets an SR-N identifier and should be traced to a control row in §7, so the SoA stays the single source of truth for "what we run."

### 8.1 Secure Development Practices

> How security enters the build, not just the running system. Code review, dependency control, and keeping secrets out of source all belong here.

- **SR-2** {{e.g., All external/user-supplied text is treated as untrusted input and never executed as instructions.}} → CTRL-5
- {{Code review before merge to the main branch / for security-relevant changes.}}
- {{Dependencies pinned and audited; see CTRL-3.}}
- {{Secrets kept out of source; see CTRL-1, CTRL-2.}}

### 8.2 Input, Prompt Handling, and Trust Boundaries

> Name the trust boundaries explicitly — the lines across which data goes from "trusted" to "untrusted." For an agent, the big one is anything the agent reads from the outside world (web content, user messages, file contents) versus its own instructions.

- {{Trust boundary 1: {{e.g., user message → agent reasoning — user text is data, not commands}}.}}
- {{Trust boundary 2: {{e.g., fetched web/file content → agent — never followed as instructions}}.}}
- {{Mitigation: {{e.g., prompt-injection-resistant framing; tool calls gated by §8.4 permissions}}.}}

### 8.3 Dependency and Supply-Chain Hygiene

> The packages and models you pull in are part of your attack surface. Record how you control them.

- {{Versions pinned; lockfile committed.}}
- {{Periodic audit / advisory check via {{tool}}.}}
- {{Provenance / source trust for any model artifacts or non-package downloads.}}

### 8.4 Secrets Handling

> Where secrets live, who can read them, and how they rotate. Cross-reference CTRL-1.

- {{Storage: {{secrets file / manager / env}}, never in repo.}}
- {{Scope: least-privilege tokens; one credential per purpose where feasible.}}
- {{Rotation cadence and trigger (see §9).}}

### 8.5 Agent-Specific Surfaces (if applicable)

> The controls that only exist because there is an autonomous agent. Omit if {{System Name}} has no agent.

| Surface | Control | Trace |
|---|---|---|
| Tool permissions | {{Explicit allow-list of callable tools; deny by default}} | CTRL-8 |
| State read/write | {{Agent may read {{X}}, may write {{Y}}; everything else denied}} | CTRL-6 |
| Identity isolation | {{State of one identity is not reachable by another}} | OBJ-1, {{policy in §2.2}} |
| {{Surface}} | {{Control}} | {{CTRL-N / OBJ-N}} |

---

## 9. Operational Security and Incident Response

> Security is not a one-time setup — most of it happens in day-to-day operation. This section covers the running disciplines (access, logging, backup, patching, change management) and then the incident-response basics. For a solo or small-team system, keep this *runnable* rather than enterprise-heavyweight — a plan you will actually follow beats a perfect plan you will not. The one thing not to skip is naming the **detect → respond → recover** loop: how you would *notice* an incident, what you would *do*, and how you would get back to a known-good state.

### 9.1 Day-to-Day Operations

| Area | Practice | Cadence / trigger | Trace |
|---|---|---|---|
| Access control | {{Key-only auth; review accounts/keys}} | {{Quarterly}} | CTRL-6 |
| Credential rotation | {{Rotate {{which credentials}}}} | {{Every {{N}} / on suspected exposure}} | CTRL-1 |
| Logging & monitoring | {{What is logged; how reviewed}} | {{Reviewed {{cadence}}}} | CTRL-7 |
| Backup & recovery | {{Backup target; restore test}} | {{Daily backup / quarterly restore test}} | CTRL-4 |
| Patching | {{OS + dependency updates}} | {{Monthly / on critical advisory}} | CTRL-3 |
| Change management | {{How changes are reviewed before they reach prod}} | {{Per change}} | §8.1 |

### 9.2 Incident Response

> The detect–respond–recover loop, written so you could follow it at 3am. Keep the steps concrete and the contacts current.

- **Detect:** {{How an incident becomes known — alert, log anomaly, provider notice, user report.}}
- **Notify:** {{Who is told and how — for solo systems this is "the operator," but name any third party that must be informed, e.g., affected users or a provider.}}
- **Contain:** {{First actions to stop the bleeding — e.g., revoke the exposed credential, take the host offline, disable the affected tool.}}
- **Recover:** {{Restore to known-good — e.g., rotate all secrets, restore from CTRL-4 backup, redeploy from a clean source.}}
- **Learn:** {{Capture what happened and what changes — feed new risks back into §5 and new controls into §7. A repeat incident with no plan change is the real failure.}}

---

## 10. Verification and Audit

> A control you have not checked is a control you only *hope* works. This section states how you confirm controls actually work and keep working — so the "Verified" status in the SoA means something. ISO 27001 Clauses 9–10 are about exactly this: monitoring whether the ISMS is effective and continually improving it. For a lightweight plan, that means a periodic self-assessment, not a formal external audit.
>
> Pick a **verification method** appropriate to each control:
> - **Review** — read the config/code/policy and confirm it matches intent.
> - **Test** — exercise the control and observe it behaving (e.g., attempt access that should be denied).
> - **Scan** — run an automated tool (secret scanner, dependency audit, vulnerability scan).
> - **Demonstration** — show the control working end-to-end (e.g., perform a real restore from backup).

### 10.1 Verification per Control

| Control | Method | Evidence retained | Last verified | Next due |
|---|---|---|---|---|
| CTRL-1 | Review + Scan | {{Scan report; config screenshot}} | {{YYYY-MM-DD}} | {{YYYY-MM-DD}} |
| CTRL-4 | Demonstration | {{Restore-test log}} | {{YYYY-MM-DD}} | {{YYYY-MM-DD}} |
| CTRL-6 | Test | {{Denied-access test result}} | {{YYYY-MM-DD}} | {{YYYY-MM-DD}} |
| CTRL-N | {{Review / Test / Scan / Demo}} | {{Evidence}} | {{YYYY-MM-DD}} | {{YYYY-MM-DD}} |

### 10.2 Audit and Continual Improvement

> The routine that keeps the whole plan honest. Cross-reference the **Review Cadence** in the metadata header.

- **Self-assessment cadence:** {{e.g., quarterly walk-through of the SoA + risk table; full review after any major change or incident — see metadata Review Cadence.}}
- **What is reviewed:** {{scope still accurate? new assets/risks? control statuses current? accepted residual risks still tolerable?}}
- **Improvement loop (Clauses 9–10):** {{findings become new RISK-N / CTRL-N / OQ-N entries; nothing is "noted and forgotten."}}

---

## 11. Open Questions

> Security decisions that are not yet settled. Tracking them openly is healthier than pretending they are resolved — an unowned open question is how gaps survive. Use OQ-N, and for each note what is blocking resolution and who must decide. Resolve and remove entries as the plan matures; a provisionally-accepted risk lives here until the risk owner makes it a TR-N in §6.

- **OQ-1** {{Question — e.g., "Do we need at-rest encryption for AST-4, or is host-level disk encryption sufficient?"}} — {{blocked on: {{what}}}}; {{decider: {{who}}}}.
- **OQ-2** {{Question}} — {{blocking}}; {{decider}}.
- **OQ-N** {{Question}} — {{blocking}}; {{decider}}.

---

## 12. Revision History

> Record every substantive change with a version bump, date, author, and summary. Security plans must show their evolution — auditors and future maintainers need to see when scope, risks, or control selections changed, and why. A plan with a single "Initial draft" row that is two years old tells its own story.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Security Objectives and Policy
- §3 ISMS Scope and Context
- §4 Assets and Data Classification
- §5 Risk Assessment
- §6 Risk Treatment Plan
- §7 Statement of Applicability — this is the artifact that makes the document an SoA; without it you have notes, not a plan.
- §12 Revision History

**Optional sections** (include if relevant):
- §8 Application Security Controls (include for any custom application or agent; omit only if {{System Name}} is pure off-the-shelf infrastructure).
- §9 Operational Security and Incident Response (strongly recommended; at minimum keep the detect–respond–recover loop in §9.2).
- §10 Verification and Audit (defer the per-control table if very early, but keep the cadence).
- §11 Open Questions (track elsewhere if you prefer).

**Tailoring**:
- **Identifier conventions** — keep these consistent so documents cross-reference cleanly:
  - SP-N: this document's ID prefix.
  - SR-N: security requirements (may originate in the SRS and be referenced here).
  - CTRL-N: selected controls (the SoA rows in §7).
  - RISK-N: identified risks (§5).
  - TR-N: risk-treatment decisions (§6).
  - OBJ-N: security objectives (§2).
  - OQ-N: open questions (§11).
- Pick **one** control baseline (ISO 27002 Annex A *or* a NIST 800-53 baseline) as the spine of the SoA and map the other to it as needed — running two full catalogs in parallel is more bookkeeping than a small system needs.
- The qualitative Low/Medium/High scoring in §5 is enough for most solo/small-team systems. Move to numeric scoring only if you genuinely need finer ranking.
- A public-by-design repository changes the threat model — assume the repo's contents are readable by anyone and let that drive the secrets controls (CTRL-1, CTRL-2). Mark the document's own Classification accordingly.
- Keep the SoA the single source of truth for "what we run." If a control is added anywhere (§8, §9), it earns a CTRL-N row in §7.

**For regulated/safety-critical projects:** use the full ISO/IEC 27001:2022 + ISO/IEC 27002:2022 (and ISO/IEC 27034 for application security), verified against the purchased normative text, not this lightweight version. This template paraphrases publicly available summaries and the public-domain NIST SP 800-53 Rev. 5 catalog; it is suitable for solo/small-team and internal use but is not a substitute for the normative standards in a certification or audited context.
