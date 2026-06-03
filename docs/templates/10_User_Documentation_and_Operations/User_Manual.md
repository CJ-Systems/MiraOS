# User Manual Template

> **Template purpose:** Lightweight, task-oriented User Manual structure following ISO/IEC/IEEE 26514:2022 (Design and development of information for users). Use this template when writing the manual that ships to the people who *use* a product. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Once a feature set is stable enough that real user goals can be documented end-to-end. The User Manual is the highest-level "how do I get my thing done with this system" document for end users. It sits downstream of the SRS (which use cases / requirements exist) and is planned and scheduled by the companion User Documentation Plan in this same pack. Operator/admin runbooks and developer docs live in separate documents — this manual does not.
>
> **Companion standard:** ISO/IEC/IEEE 26514:2022 — Systems and software engineering — Design and development of information for users — primary. ISO/IEC/IEEE 26515:2018 — Developing information for users in an agile environment — companion for the production/lifecycle side, owned mainly by the User Documentation Plan in this same pack.
>
> **Status of this template:** Lightweight, public, reusable extract for the Mira-OS docs pack, following the task-oriented structure of ISO/IEC/IEEE 26514:2022 (with 26515:2018 as the agile-production companion, mainly owned by the sibling User Documentation Plan). Faithful to the 26514 content outline but reduced for solo/small-team use. Both standards are paywalled ISO/IEEE publications — this template paraphrases their section structure and contains no copied normative text; verify against the purchased standards for regulated, safety-critical, or contractual contexts. The pack-skeleton domain sections (Getting Started, User Tasks, Features, Messages and Errors, Troubleshooting, Security and Privacy Guidance, Glossary, Support) are preserved and deepened, not replaced.

---

# User Manual — {{System Name}}

| Field | Value |
|---|---|
| Document ID | UM-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 26514:2022 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Audience | {{Primary user role(s) — e.g., end user / power user / administrator}} |
| Applies to (system version) | {{Product/version this manual documents — e.g., v2.x}} |
| Assumed prior knowledge | {{What the reader is assumed to already know}} |
| Delivery format | {{Online help / PDF / in-product / printed}} |
| Companion documents | User Documentation Plan; Operations/Admin Guide; SRS (use cases) |

---

## 1. Introduction

> This section sets up who the manual is for and what it does and does not cover. It folds the usual Purpose / Scope / Definitions / References subsections into one place.
>
> **Beginner note — user documentation vs. system documentation.** *User documentation* is written for the people who **use** the system to get real work done. *System documentation* (operator runbooks, admin guides, developer docs) is written for the people who run or build it. This manual is user documentation only. Naming that split up front is the single most effective way to stop a manual from quietly drifting into internals the reader doesn't need — when in doubt, ask "does an end user trying to finish a job need this?" If not, it belongs in the Operations/Admin Guide, not here.

### 1.1 Purpose

> One paragraph: what this manual is and who it is for. State explicitly that it is *user* documentation.

{{This manual explains how to use {{System Name}} to accomplish real goals. It is written for {{primary user role(s)}} — the people who use the system — not for the people who operate or build it. Operator and administrator runbooks live in the Operations/Admin Guide; developer and internal-design documents live with the engineering specs. This manual documents {{System Name}} version {{x.y}}.}}

### 1.2 Scope

> What the manual covers and excludes; the system version it applies to; the user roles it serves; anything intentionally deferred.

**This manual covers:** {{the day-to-day tasks, features, messages, and self-service troubleshooting for {{System Name}} {{version}} as used by {{role(s)}}.}}

**This manual does not cover:** {{installation/deployment (see {{install/setup doc}}), administration and operations (see Operations/Admin Guide), and developer/API integration (see {{developer doc}}).}}

**Intentionally deferred:** {{tasks/features documented in a later revision — list, or "none".}}

#### 1.2.1 Audience and prerequisites

> Name the reader (audience/persona) and what they are assumed to already know (prerequisite knowledge).
>
> **Beginner note — audience / persona and prerequisite knowledge.** A *persona* is a short, named description of the reader you are writing for. *Prerequisite knowledge* is what you assume the reader already has (e.g., "comfortable with spreadsheets"). This single choice sets the reading level for the entire manual — pitch every later section to this reader. If you find yourself explaining something below this reader's level, or assuming something above it, the fix is here.

- **Primary audience:** {{persona — e.g., "an office user who manages records day to day"}}
- **Secondary audience (if any):** {{e.g., power users / occasional administrators}}
- **Assumed prior knowledge:** {{e.g., "familiar with web forms and basic file management; no technical/admin background assumed"}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Only the user-facing terms a reader needs to get *through the introduction*. The fuller alphabetical list lives in §8 Glossary.

| Term | Definition |
|---|---|
| {{Term 1}} | {{Plain-language definition in the user's vocabulary}} |
| {{Term 2}} | {{Definition}} |
| ... | ... |

### 1.4 References

> Documents this manual depends on or points at. Crucially, point at the SRS/use cases the tasks trace to, the companion User Documentation Plan, and the Operations guide.

Project and source documents:
- {{SRS-PROJECT-ID-001}} — Software Requirements Specification; the use cases / functional requirements that the §3 tasks trace back to.
- {{DOC-PROJECT-ID-001}} — User Documentation Plan; governs this manual's lifecycle, schedule, and status.
- {{path/to/operations-guide.md}} — Operations/Admin Guide; the home for operator/admin procedures excluded from this manual.
- {{path/to/install-setup.md}} — Installation/setup guide referenced from §2 Getting Started.

Standards:
- ISO/IEC/IEEE 26514:2022 — Design and development of information for users (the structure this manual follows).
- ISO/IEC/IEEE 26515:2018 — Developing information for users in an agile environment (production/lifecycle companion, owned by the User Documentation Plan).

---

## 2. Getting Started

> This section gives the reader their first successful end-to-end experience and the small mental model everything else builds on.
>
> **Beginner note — Getting Started is deliberately thin.** Its job is *one quick win* plus the handful of concepts a user must hold to make sense of the rest — not completeness. The depth lives in §3 User Tasks. If this section starts growing into a full procedure for everything, those procedures belong in §3 instead. Resist the urge to be exhaustive here; aim for "in five minutes the reader has done one real thing and understands the layout."

### 2.1 Before you begin

> Prerequisites the reader must satisfy before the first task will work. This mirrors the *precondition* idea used throughout §3 — what must be true before you start.
>
> **Beginner note — precondition.** A *precondition* is something that must already be true before a step can succeed (you're signed in, you have permission, a record is selected). Stating preconditions up front prevents the most common manual failure: steps that silently assume a setup the reader doesn't have.

You will need:
- {{An account / who provisions it}}
- {{Required permission(s) or role}}
- {{Supported browser / OS / device}}
- {{Network access / any other prerequisite}}

### 2.2 Accessing the system

> How to reach the system — URL, app, or install pointer. Do not duplicate the install guide; point to it.

{{Open {{System Name}} at {{URL}} / launch the {{app}}. If the system is not yet installed, see {{install/setup doc}} — this manual assumes it is already available.}}

### 2.3 Signing in

> The first task most users hit. Keep it short; if sign-in is itself complex, promote it to a full TASK-N in §3 and link here.

1. {{Go to {{sign-in location}}.}}
2. {{Enter your {{credential}}.}}
3. {{Complete {{second factor, if any}}.}}

Expected result: {{you land on {{main screen}}.}} If sign-in fails, see {{MSG-1}} in §5 or {{TRBL-1}} in §6.

### 2.4 A tour of the main screen

> A labelled walkthrough of the primary screen and how to move around. A simple labelled list or table is usually enough.

| Area | What it is | What you do here |
|---|---|---|
| {{Navigation / sidebar}} | {{Plain description}} | {{e.g., switch between sections}} |
| {{Main work area}} | {{Description}} | {{Description}} |
| {{Status / account menu}} | {{Description}} | {{Description}} |

### 2.5 Core concepts

> The few ideas a user must hold to understand everything after. Keep to a short list; full definitions go in §8 Glossary.

- **{{Concept 1}}** — {{one-line plain explanation}}
- **{{Concept 2}}** — {{one-line plain explanation}}

### 2.6 Guided / conversational setup (if applicable)

> If the system itself walks the user through setup (for example, an in-product flow that asks questions and configures things for them), describe what that experience looks like rather than listing raw configuration steps.

{{Where {{System Name}} guides you through setup itself, the system asks you {{what it asks}} and configures {{what it configures}} for you; you do not edit configuration by hand. Follow the prompts; this manual describes what you will be asked and why, not the underlying settings.}}

---

## 3. User Tasks

> This is the heart of the manual and its deepest section. A *task* is one real-world goal the reader wants to accomplish, written as a repeating, copy-per-task structure.
>
> **Beginner note — task-oriented (task-based) documentation.** The organizing idea of 26514 is to structure the manual around the goals a user is trying to accomplish ("send an invoice", "reset a password"), **not** around a tour of menus or screens. Each goal becomes a numbered **TASK-N** with the same repeating shape. This is *why* tasks lead and theory is trimmed — it follows from the *minimalism* principle (after John Carroll's minimalist-documentation work): give users exactly enough to act and to learn by doing, and cut conceptual padding. Minimalism is the reason to be lean, never an excuse to be vague.
>
> **Beginner note — preconditions and traceability.** Each task lists its *preconditions* (see §2.1) so steps never assume setup the reader doesn't have. Each task also carries a TASK-N id that *traces back* to a use case / functional requirement in the SRS. **Traceability** here simply means: when the system changes, you can follow the link from a requirement to the task(s) that document it, and know exactly which manual sections to update. The TASK-N id is what makes that link possible.

### 3.0 How tasks are organized

> A short orientation note for the reader before the task list. Explain the repeating shape so they know what to expect in every task.

Every task below uses the same six-part shape, so once you've read one you can navigate any of them:

1. **Purpose** — what the task accomplishes and why you'd do it.
2. **Preconditions** — what must already be true before you start.
3. **Steps** — numbered actions, written as plain imperatives ("Click Save").
4. **Expected result** — what you should see when it worked.
5. **Errors and recovery** — what can go wrong and how to get back on track (links to §5 and §6).
6. **Related tasks** — nearby goals you might want next.

### 3.1 Task index

> A navigable, traceable index of every documented task. The "Traces to" column is the traceability link back to the SRS.

| Task ID | Task name | Who it's for | Traces to (SRS) |
|---|---|---|---|
| TASK-1 | {{e.g., Sign in to {{System Name}}}} | {{End user}} | {{UC-1 / FR-3.1}} |
| TASK-2 | {{e.g., Create a new {{record}}}} | {{End user}} | {{UC-2 / FR-3.2}} |
| TASK-3 | {{e.g., Find last month's {{records}}}} | {{Power user}} | {{UC-5 / FR-3.4}} |
| TASK-N | {{Task name}} | {{Role}} | {{UC-N / FR-N}} |

### 3.2 TASK-1 — {{Task name}}

> Copy this subsection once per task, incrementing the TASK-N id and the §3.N number together. Keep the six headings in this order in every task.

**Purpose.** {{One or two plain sentences: what this accomplishes and when you'd reach for it.}}

**Preconditions.**
- {{e.g., You are signed in (see TASK-... / §2.3).}}
- {{e.g., You have the {{permission/role}}.}}
- {{e.g., A {{record}} is selected.}}

**Steps.**
1. {{Imperative action — "Open the {{section}}".}}
2. {{Imperative action — "Click {{button}}".}}
3. {{Imperative action — "Enter {{field}} and click {{Save}}".}}

**Expected result.** {{State it concretely — what the reader actually sees, e.g., "A confirmation 'Saved' appears and the new {{record}} shows in the list."}}

**Errors and recovery.**
- {{If you see {{MSG-2}} → {{plain recovery action}}; see §5.}}
- {{If {{symptom}} → see {{TRBL-2}} in §6.}}
- {{If you cannot recover → see §7 Support.}}

**Related tasks.** {{TASK-3 ({{name}}), TASK-...}}

### 3.3 TASK-2 — {{Task name}}

{{Repeat the six-part shape...}}

---

## 4. Features

> A *feature* is a user-visible capability described from the user's point of view — what it's for, when you'd reach for it, and its limits. This is distinct from §3, which is step-by-step procedures.
>
> **Beginner note — feature vs. task.** A **feature** answers *"what can the system do?"* (for example, "saved searches"). A **task** answers *"how do I get my thing done?"* (for example, "find last month's invoices", which *uses* saved searches). We separate them on purpose: mixing them produces the classic manual that tours every menu and never actually helps anyone finish a job. Describe the capability here; put the goal-driven procedure in §3 and cross-reference between the two.

### 4.1 {{Feature name}}

- **What it's for:** {{the user-facing purpose}}
- **When you'd use it:** {{the situation that makes a user reach for it}}
- **Limits / edge behavior:** {{caps, known limitations, surprising behavior worth flagging}}
- **Tasks that use it:** {{TASK-2, TASK-3}}

### 4.2 {{Feature name}}

{{Repeat per feature, cross-referencing the TASK-N entries that exercise it...}}

---

## 5. Messages and Errors

> A reference catalogue of the messages a user will see — not only errors, but confirmations and warnings too — with what each means in plain language and exactly what to do next.
>
> **Beginner note — what a good message entry does.** It tells the reader three things: *what happened*, *why*, and *exactly what to do next*. It never just restates the raw message text. Write the meaning in the user's language, not in the system's. Where the system surfaces messages in a friendly, mediated voice rather than as raw system output, document the actual user-facing wording the reader will see, so they can match what's on their screen to this table. Each message gets an **MSG-N** id so task recovery steps (§3) and troubleshooting entries (§6) can point straight at it.

| ID | Message (as the user sees it) | Type | Meaning (plain language) | What to do |
|---|---|---|---|---|
| MSG-1 | {{"Sign-in failed"}} | Error | {{Your {{credential}} wasn't accepted, or your account is locked.}} | {{Re-enter your {{credential}}; if it keeps failing see TRBL-1, then §7 Support.}} |
| MSG-2 | {{"Saved"}} | Confirmation | {{Your changes were stored successfully.}} | {{Nothing — you can continue.}} |
| MSG-3 | {{"This will permanently delete {{item}}"}} | Warning | {{The next step cannot be undone.}} | {{Confirm only if you're sure; otherwise cancel.}} |
| MSG-N | {{message}} | {{Error/Warning/Confirmation}} | {{meaning}} | {{action; escalate to §7 if not self-recoverable}} |

---

## 6. Troubleshooting

> Structured self-service entries organized by what the user *observes*, because the symptom is all they have when something breaks.
>
> **Beginner note — organize by symptom, not by cause.** When something goes wrong, the user can only describe what they *see* — they can't search by a cause they don't yet know. So each entry leads with a **Symptom**, then offers the **Likely cause**, then the **Resolution**. Order entries by how likely or severe they are. Link each entry back to the relevant MSG-N message and/or TASK-N task, and when self-service runs out, point to §7 Support. Each entry gets a **TRBL-N** id.

| ID | Symptom (what you see) | Likely cause | Resolution | Related |
|---|---|---|---|---|
| TRBL-1 | {{Can't sign in even with the right {{credential}}}} | {{Account locked after repeated attempts, or session expired}} | {{Wait {{n}} minutes and retry; if still locked, contact §7 Support}} | {{MSG-1, TASK-1}} |
| TRBL-2 | {{Changes don't appear after saving}} | {{Stale view / not refreshed}} | {{Refresh the {{section}}; if still missing, see §7 Support}} | {{MSG-2, TASK-2}} |
| TRBL-N | {{symptom}} | {{cause}} | {{resolution}} | {{MSG-N / TASK-N}} |

**Still stuck?** If none of the above resolves the problem, see §7 Support and bring the information listed there.

---

## 7. Security and Privacy Guidance

> The user's own responsibilities and safe-use practices. This is about the human in the loop, distinct from the system's built-in controls.
>
> **Beginner note — this section is about the human, not the machine.** Even a well-secured system depends on the user: not sharing credentials, not pasting secrets where they don't belong, knowing what the system stores about them, and knowing how to report a problem. The system's *own* controls (encryption, access enforcement, retention policy) belong in the security/privacy and operations documents — cross-reference them here, don't restate them. Keep this section short and actionable, not a policy essay.

### 7.1 Protecting your account

- {{Keep your {{credential}} private; never share it.}}
- {{Use {{second factor}} if offered, and keep your recovery method current.}}
- {{Sign out on shared devices.}}

### 7.2 Sharing and access

- {{Share {{items}} only with people who need them; review access periodically.}}
- {{Understand what each sharing/permission level grants before using it.}}

### 7.3 Handling sensitive and personal data

- {{Don't enter secrets (passwords, tokens) into {{free-text fields}} where they aren't expected.}}
- {{Treat {{personal/sensitive data}} per {{your organization's policy}}.}}

### 7.4 What the system stores about you

> Plain summary; point at the formal privacy notice rather than restating it.

{{In short, {{System Name}} stores {{what}} for {{why}}, kept {{where / how long}}. For the full details, see {{privacy notice / data-handling doc}}.}}

### 7.5 Reporting a security or privacy concern

- {{If you suspect a security or privacy problem, report it via {{channel}} as soon as possible.}}
- {{Do not investigate by sharing the issue or credentials more widely.}}

---

## 8. Glossary

> The fuller alphabetical list of user-facing terms, distinct from §1.3 (which holds only the terms needed to read the introduction).
>
> **Beginner note — write for the reader who jumped straight to a task.** A glossary entry should let someone who skipped to §3 understand a term without reading the whole manual. Define terms in the user's everyday vocabulary; prefer the plain word over internal/system jargon. Keep a technical term only when the user has actively opted into it (a named workflow concept) or must type it literally. Cross-link the first hard use of a term in the body to its entry here.

| Term | Definition |
|---|---|
| {{Term A}} | {{Plain-language definition; note if it's a term the user must type literally}} |
| {{Term B}} | {{Definition}} |
| {{Term C}} | {{Definition}} |
| ... | ... |

---

## 9. Support

> Where to get help, what to have ready, and how things escalate. This is the terminal node that §5 and §6 escalate into.
>
> **Beginner note — the manual does triage on support's behalf.** Telling the reader up front exactly what to gather turns a vague first contact into one that's resolvable immediately, instead of a slow back-and-forth. List the channels, the response shape to expect, and the precise information to bring — then state the escalation path for when first-line support can't resolve it.

### 9.1 How to get help

| Channel | How to reach it | What to expect |
|---|---|---|
| {{Help desk / email}} | {{address / link}} | {{e.g., response within {{n}} business hours}} |
| {{In-product help}} | {{where}} | {{e.g., self-service articles + chat}} |
| {{Community / forum}} | {{link}} | {{best-effort peer help}} |

### 9.2 What to have ready

Before contacting support, gather:
- **System version** — {{from the front-matter "Applies to (system version)" of this manual}}
- **What you were doing** — the {{TASK-N}} you were attempting
- **What you saw** — the {{MSG-N}} message (exact wording) and/or {{TRBL-N}} symptom
- **Steps to reproduce** — what you did, in order, so support can see it too
- {{Account / environment details if relevant}}

### 9.3 Escalation

{{If first-line support can't resolve it, your issue is escalated to {{tier 2 / engineering / on-call}} via {{path}}. Expect {{what}}.}}

---

## 10. Open Questions

> Unresolved documentation decisions, parked on purpose so they aren't silently asserted as fact in the body.
>
> **Beginner note — uncertainty goes here, not into a task.** An explicit open-questions list keeps half-known things out of the procedures, where a reader would otherwise take them as fact. Anything not yet confirmed — a task not yet documented, behavior the author couldn't verify, terminology still in flux, audience scope still being settled — is parked here with an **OQ-N** id, what's blocking it, and who needs to decide. Resolve and remove each as the manual matures.

- **OQ-1**: {{e.g., TASK-4 behavior under {{condition}} not yet confirmed}} — {{what's blocking; who decides}}
- **OQ-2**: {{e.g., terminology "{{term}}" vs "{{alt term}}" not settled}} — {{blocking; decider}}
- **OQ-N**: {{question}} — {{blocking; decider}}

---

## 11. Revision History

> The change log for the manual itself.
>
> **Beginner note — how a reader judges whether to trust this manual.** Every substantive change gets a row here and a version bump, so a reader can tell which system version the manual matches and whether it has been approved. The **Status line** in the front matter (Draft / In Review / Approved / Retired — governed by the companion User Documentation Plan) and this table together are what tell a reader whether the manual can be trusted yet. This section stays last so the body reads start-to-finish and the change log lives at the back.

| Version | Date | Author | Description of Change | Approval |
|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft | {{Pending}} |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections, including 1.2.1 Audience and prerequisites)
- §2 Getting Started (at minimum: Before you begin, Accessing the system, Signing in)
- §3 User Tasks (the core — at least the §3.0 orientation, the §3.1 task index, and one full TASK-N)
- §5 Messages and Errors
- §9 Support
- §11 Revision History

**Optional sections** (include if relevant):
- §4 Features (omit only if every capability is already obvious from the tasks)
- §6 Troubleshooting (fold into §5 if the system is very simple)
- §7 Security and Privacy Guidance (include for anything handling accounts or personal data; cross-reference rather than restate the formal policy)
- §8 Glossary (omit if §1.3 already covers every term; otherwise keep)
- §10 Open Questions (track elsewhere if you prefer)
- §2.6 Guided / conversational setup (omit if the system has no in-product guided setup)

**Identifier conventions**:
- TASK-N: each documented user task — the headline traceability handle. A TASK-N traces back to a use case / functional requirement in the SRS and forward to the feature(s) it uses.
- MSG-N: catalogued user-facing messages, warnings, and confirmations (§5), referenced from task recovery and troubleshooting.
- TRBL-N: troubleshooting entries (§6), keyed by symptom, linking to MSG-N / TASK-N.
- OQ-N: open documentation questions (§10).

TASK-N is the headline prefix; MSG-N, TRBL-N, and OQ-N are lightweight and optional. These prefixes enable cross-document traceability — a use case in the SRS can be traced to the task(s) that document it here, so when the system changes you can find which manual sections need updating.

**Tailoring**:
- The 26514 section structure is guidance, not law. Add or merge subsections as the product needs.
- Keep the manual *task-oriented and minimalist* — lead with goals, cut conceptual padding, never pad with menu tours. Minimalism means lean, not vague.
- Keep user documentation separate from operator/admin runbooks and developer docs; cross-reference them instead of absorbing them.
- **Solo developer / small team:** collapse the manual to the four load-bearing sections — §2 Getting Started, §3 User Tasks (with the task index), §5 Messages and Errors, and §9 Support — plus §11 Revision History. Document tasks as you actually build features, one TASK-N at a time, and grow the rest only when a real user need appears. The MSG-N / TRBL-N / OQ-N ids can stay informal until the manual is big enough to need cross-references.
- The Status line and Revision History are mandatory regardless of size — they are how a reader decides whether to trust the document.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 26514:2022 (with 26515:2018 for the agile-production lifecycle), not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
