# Concept of Operations Template

> **Template purpose:** Lightweight Concept of Operations (ConOps / Operational Concept) structure following ISO/IEC/IEEE 29148 and IEEE 1362. A ConOps describes a system from the *user's point of view* — what the world looks like today, why a change is needed, and how people will actually live with and operate the new system day to day. It is written in plain prose before requirements are pinned down, so everyone shares one picture of "what we're building and why" before any "what must it do" gets formalized. Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** At the very start of a project or major change — *before* the SRS, sometimes before you're even sure the project should happen. The ConOps is the document you write to align stakeholders on the problem, the proposed change, and a vision of the system in use. Once it's agreed, the requirements (SRS) say WHAT the system must do, the design (SDD) says HOW. The ConOps stays the readable "why and for whom" anchor underneath them.
>
> **Companion standard:** ISO/IEC/IEEE 29148 (which folds in the Concept of Operations / Operational Concept Description, "ConOps"/"OpsCon") and IEEE 1362 — Standard for a Concept of Operations (ConOps) Document.
>
> **Status of this template:** Lightweight skeleton derived from public sources describing the ISO/IEC/IEEE 29148 and IEEE 1362 outlines. Because the underlying standards are likely paywalled, this template paraphrases their intent and follows their section *organization* only — it reproduces no normative text. Verify against the full standard when you have access, especially for enterprise/regulated/safety-critical contexts.

---

# Concept of Operations — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | CONOPS-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29148 + IEEE 1362 (lightweight) |
| Owner | {{Project name or owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Audience | {{Stakeholders / users / sponsors who must agree on this concept}} |
| Supersedes | {{Prior ConOps version, or "none — first concept"}} |

---

## 1. Introduction

### 1.1 Purpose

> One paragraph: what this document is for and who should read it. A ConOps exists to get every stakeholder — sponsors, users, builders — looking at the *same* picture of the problem and the proposed system before detailed requirements are written. Say plainly that this is the user's-eye view, not a technical spec.

{{This document describes the concept of operations for {{Project Name}}: the situation today, why a change is needed, and how people will use and operate the proposed system. It is written from the user's point of view to align stakeholders on the problem and the vision before requirements are formalized. The Software Requirements Specification (SRS) will say WHAT the system must do; the design documents say HOW. This ConOps says WHY, FOR WHOM, and WHAT IT LOOKS LIKE IN USE.}}

### 1.2 Scope

> Define what this concept covers and what it deliberately leaves out. Name the system, and note any phases (e.g., a first release versus a later vision). Distinguish the system from neighboring things it might be confused with.

**{{Project Name}} is** {{a short, plain description of the system in user terms}}.

**{{Project Name}} is NOT** {{things it is commonly mistaken for / out of scope}}.

**Phase 1** (current concept): {{what this version of the concept covers}}.

**Phase 2** (future vision): {{later ambitions, or "out of scope for this concept"}}.

### 1.3 Definitions and Acronyms

> Define every project-specific term and acronym a reader would need to follow the rest of the document. Include ordinary words used in a special way here. If leaving a term undefined would let two readers picture different things, define it.

| Term | Definition |
|---|---|
| {{Term 1}} | {{Definition}} |
| {{Term 2}} | {{Definition}} |
| ... | ... |

### 1.4 References

> List the documents this concept depends on or that inform it — prior notes, related specs, decision records, and external standards. Categorizing them makes the list easier to scan.

Background and prior work:
- {{path/to/doc.md}} — {{brief description}}
- ...

Related specifications and decisions:
- {{path/to/spec.md}} — {{brief description}}
- ADR-NNNN — {{decision relevant to this concept}}
- ...

External standards:
- ISO/IEC/IEEE 29148 — {{requirements engineering; defines the ConOps/OpsCon}}
- IEEE 1362 — {{Concept of Operations document standard}}
- {{Other standard with version}} — {{relevance}}

---

## 2. Current Situation / Background

> This section paints the world as it is *today*, before the proposed system exists. Describe how people currently get the job done — even if "the current system" is just manual effort, a spreadsheet, or nothing at all. Be honest about what hurts. A reader should finish this section understanding the status quo and why it is not good enough. If you skip this, the justification in §3 has nothing to push against.

### 2.1 The World Today

> Narrative description of how things work now: who is involved, what they do, what tools or processes (if any) exist. Keep it concrete and plain.

{{Describe the current situation in plain prose...}}

### 2.2 Existing System (if any)

> If there is a current system being replaced or extended, describe it: what it does, its main parts, who operates it. If there is no existing system, say so explicitly — "the work is done manually / not done at all" is a valid current state.

{{Description of the existing system, or a statement that none exists...}}

### 2.3 Problems and Limitations

> The concrete pain points with the status quo. What is slow, error-prone, costly, frustrating, or impossible today? These problems are what the proposed system must address, so be specific — vague complaints make for vague requirements later.

- {{Problem 1}} — {{who it affects and how}}
- {{Problem 2}} — {{...}}
- ...

---

## 3. Justification for and Nature of Changes

> Having shown the problems in §2, this section makes the case for change and outlines *what* will change at a high level. "Justification" = why doing nothing is unacceptable and why this change is the right response. "Nature of changes" = the broad strokes of what's new or different — not detailed requirements, just the shape of the change. A reader should finish here convinced the change is worth making and roughly aware of what it entails.

### 3.1 Justification for Change

> Why change now? What is the cost of the status quo, the opportunity, or the trigger (new need, new technology, a deadline)? Tie each reason back to a problem from §2.3.

{{The case for change, in plain prose...}}

### 3.2 Nature of the Changes

> The high-level description of what will change: new capabilities, retired processes, shifts in who does what. Keep it at the "concept" altitude — these become requirements later, they are not requirements yet.

- {{Change 1}} — {{what becomes possible / different}}
- {{Change 2}} — {{...}}
- ...

### 3.3 Priorities Among Changes

> Not all changes matter equally. Note which are essential ("must change for this to be worth doing") versus desirable versus nice-to-have. This helps scope later phases.

| Change | Priority | Notes |
|---|---|---|
| {{Change}} | {{Essential / Desirable / Optional}} | {{rationale}} |
| ... | ... | ... |

---

## 4. Concept for the Proposed System

> This is the heart of the ConOps: a description of the proposed system as people will experience it. Stay in user terms — what the system does for people, the different ways it can run (its "modes"), and the kinds of people who use it ("user classes"). Avoid internal design detail; that belongs in the SDD. A reader should come away able to picture the system in use and to recognize which kind of user they are.

### 4.1 Operational Overview

> A plain-language summary of the proposed system in operation: what it does, the main pieces a user would notice, and the overall flow of a typical use. A diagram or simple sketch helps here if you have one.

{{High-level description of the proposed system in use...}}

### 4.2 Modes of Operation

> A "mode" is a distinct way the system can be running — for example normal/everyday use, a setup or onboarding mode, an offline or degraded mode, a maintenance mode. Different modes can offer different capabilities. List the modes and what each is for, so no one assumes the system only ever behaves one way.

| Mode | Purpose | Available capabilities |
|---|---|---|
| {{Normal operation}} | {{everyday use}} | {{what users can do}} |
| {{Setup / onboarding}} | {{first-run configuration}} | {{...}} |
| {{Degraded / offline}} | {{when a dependency is unavailable}} | {{reduced capabilities}} |
| ... | ... | ... |

### 4.3 User Classes

> A "user class" is a category of person who interacts with the system, grouped by what they need from it and what they're allowed to do — for example an everyday user, an administrator, a first-time visitor, an external integrator. Give each a UC-N identifier so scenarios in §5 and requirements in the SRS can refer back to them. Describe who they are, what they want, and roughly what access or responsibility they have.

- **UC-1 {{User class name}}** — {{who they are; what they need from the system; their level of access or responsibility}}.
- **UC-2 {{User class name}}** — {{...}}.
- **UC-3 {{User class name}}** — {{...}}.
- ...

### 4.4 How User Classes Interact with the System

> For each user class, summarize the main ways they touch the system — what they do, how often, and through what surface (a CLI, a chat interface, a config file, an API). This bridges the abstract user classes into the concrete scenarios that follow.

| User class | Interacts via | Main activities |
|---|---|---|
| UC-1 {{name}} | {{interface}} | {{what they do}} |
| UC-2 {{name}} | {{interface}} | {{...}} |
| ... | ... | ... |

---

## 5. Operational Scenarios

> Scenarios are short "day in the life" stories that walk through the system in use, step by step, in plain prose. Each one names a user (by their UC-N class), a goal, and the sequence of what happens — including what the system does and how the person responds. Good scenarios are concrete enough that a reader can almost watch them happen, and they surface needs that abstract descriptions miss. Give each a SCN-N identifier. Cover the common "happy path" cases first, then add at least one where something goes wrong (an error, a missing dependency, a wrong input) so the concept accounts for trouble, not just success.

### 5.1 SCN-1 — {{Scenario name, e.g., "First-time setup"}}

> **Actor(s):** {{UC-N}} · **Goal:** {{what the user is trying to accomplish}} · **Mode:** {{which mode of operation from §4.2}}

{{Tell the story step by step in plain prose:
1. {{The user does X...}}
2. {{The system responds with Y...}}
3. {{The user then...}}
4. {{...and the goal is achieved when Z.}}}}

**Outcome:** {{what success looks like at the end of this scenario}}.

### 5.2 SCN-2 — {{Scenario name, e.g., "Everyday use"}}

> **Actor(s):** {{UC-N}} · **Goal:** {{...}} · **Mode:** {{...}}

{{Step-by-step narrative...}}

**Outcome:** {{...}}.

### 5.3 SCN-3 — {{Scenario name, e.g., "Something goes wrong"}}

> **Actor(s):** {{UC-N}} · **Goal:** {{...}} · **Mode:** {{e.g., degraded / offline}}
>
> At least one scenario should show the system under trouble: an error, an unavailable dependency, bad input, or an interruption. Show how the user notices, what the system tells them, and how they recover. This is where the concept proves it has thought about the unhappy path.

{{Step-by-step narrative of the failure and recovery...}}

**Outcome:** {{how the user ends up — recovered, blocked, or escalated}}.

---

## 6. Operational Environment

> Describe *where and how* the system runs and the assumptions you're making about that setting. This includes the platform it runs on, what it depends on (network, other services, hardware), who installs and maintains it, and any constraints of the deployment context. Calling these out early prevents nasty surprises — a concept that quietly assumes always-on internet or a powerful machine should say so here so that assumption can be challenged.

### 6.1 Deployment Context

> Where does the system live and run? A single user's laptop, a server, a phone, an embedded device, a cloud account? Who installs it and who keeps it running?

{{Description of where and how the system is deployed...}}

### 6.2 Dependencies and Resources

> What does the system rely on to work — operating systems, runtimes, network access, third-party services, hardware capabilities, storage? Note minimums where they matter.

- {{Dependency 1}} — {{why it's needed / minimum version or capability}}
- {{Dependency 2}} — {{...}}
- ...

### 6.3 Assumptions about the Environment

> Things you are taking for granted about the deployment setting. Each assumption is a risk if it turns out to be false, so state them plainly so they can be reviewed.

- {{Assumption 1}}
- {{Assumption 2}}
- ...

---

## 7. Operational Impacts

> No system arrives without ripples. This section describes how introducing the proposed system changes things for the people and the operation around it — new tasks, retired tasks, retraining, changed responsibilities, transition steps. Listing impacts honestly helps stakeholders prepare and prevents the "nobody told us we'd have to do X" problem after launch.

### 7.1 Impact on Users

> What changes for the people who use the system day to day? New skills to learn, new habits, things they no longer have to do.

- {{Impact on users 1}}
- ...

### 7.2 Impact on Operations and Support

> What changes for whoever keeps the system running — installation, maintenance, monitoring, backups, support? If the system is solo/self-operated, say what the one operator now has to keep an eye on.

- {{Operational impact 1}}
- ...

### 7.3 Impact on the Organization (if applicable)

> Broader effects: changed roles, new responsibilities, cost or budget shifts, policy changes. Omit or shorten for solo/small-team projects where there is no wider organization.

- {{Organizational impact 1}}
- ...

### 7.4 Transition and Migration

> How do people get *from* the current situation (§2) *to* the proposed system? Note any data migration, parallel-running period, cutover, or rollback plan. Even a small project benefits from a one-line "how we switch over" note.

{{Description of how the transition happens, or "not applicable — greenfield project"...}}

---

## 8. Open Questions

> Aspects of the concept still unresolved. For each, state the question and what is blocking its resolution or who needs to decide. Resolve and remove these as the concept firms up; unresolved ones should flow into the SRS as things to nail down.

- **OQ-1**: {{question}} — {{what's blocking, who needs to decide}}
- **OQ-2**: {{question}} — {{...}}
- ...

---

## 9. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections)
- §2 Current Situation / Background
- §3 Justification for and Nature of Changes
- §4 Concept for the Proposed System (especially user classes and modes)
- §5 Operational Scenarios (at least one happy-path and one trouble scenario)
- §9 Revision History

**Optional sections** (include if relevant):
- §6 Operational Environment (omit only if truly environment-agnostic, which is rare)
- §7 Operational Impacts (trim §7.3 Organization for solo/small-team projects; keep §7.1 and §7.2)
- §8 Open Questions (track elsewhere if you prefer)

**Tailoring**:
- Section headers from 29148/1362 are guidance, not requirements. Add or remove subsections as the project needs.
- Keep the ConOps in *user terms* and plain prose. Internal design and data structures belong in the SDD; testable "must" statements belong in the SRS.
- Write scenarios (§5) as stories, not bullet specs. Their value is that a reader can picture the system in use — that's what catches missing needs early.
- Revision history is mandatory. Track every substantive change with version bumps.

**Identifier conventions**:
- SCN-N: operational scenarios (§5)
- UC-N: user classes (§4.3)

These prefixes enable cross-document traceability — user classes and scenarios named here can be referenced by requirements in the SRS and by design decisions in the SDD.

**For regulated/safety-critical projects:** use the full standard, not this lightweight version.
