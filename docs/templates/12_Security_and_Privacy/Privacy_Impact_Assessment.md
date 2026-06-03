# Privacy Impact Assessment Template

> **Template purpose:** Lightweight Privacy Impact Assessment / Data Protection Impact Assessment (PIA / DPIA) structure for recording how a system handles personal data, what risks that handling creates for the people the data is about, what safeguards bring those risks down, and what must be disclosed to those people. A PIA answers a deceptively simple question — "whose data are we touching, why, and what could that do to them?" — and writes down the answer before the system goes live. This one template also doubles as scaffolding for two adjacent compliance deliverables: the GDPR Article 30 *Record of Processing Activities* (a standing inventory of what you process) and the public *privacy notice* (what you must tell people). Replace `{{placeholder}}` content with project-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** Before deploying — or substantially changing — any system that collects, stores, reads, combines, shares, or deletes personal data about living people. Start one as soon as the intended processing is clear, not after launch. Under GDPR a DPIA is *mandatory* whenever processing is "likely to result in a high risk" to people (large-scale profiling, special-category data, systematic monitoring, new technologies, automated decisions with legal effect, and similar triggers); for everything else it is still strongly recommended as good practice. A PIA is the broader, jurisdiction-neutral equivalent and is good hygiene even where no single law forces it. Treat it as a living document: re-run it on any material change to processing and on a periodic cadence.
>
> **Companion standard:** GDPR (EU 2016/679) Art. 35 (DPIA) and Art. 30 (records of processing activities); CCPA / CPRA; informed by the OWASP AI Security & Privacy Guide and NIST SP 800-53 Rev. 5 privacy controls.
>
> **Status of this template:** Lightweight, public skeleton assembled from publicly available summaries of GDPR Articles 35 and 30 and the CCPA/CPRA, informed by the openly published OWASP AI Security & Privacy Guide and NIST SP 800-53 Rev. 5 (NIST publications are US-government public-domain works). GDPR and CPRA statutory text is itself public law; this template paraphrases obligations and reproduces no normative text. It is suitable for solo/small-team and early-stage use — for regulated, high-risk, or legally binding assessments, verify against the full regulation text and obtain qualified data-protection / legal review.

---

# Privacy Impact Assessment (Data Protection Impact Assessment) — {{System Name}}

| Field | Value |
|---|---|
| Document ID | PIA-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | GDPR Art. 35 + Art. 30 + CCPA/CPRA (lightweight) |
| Owner | {{Project name or accountable owner}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |
| Data Controller | {{Legal entity / individual acting as controller}} |
| Data Protection Officer (DPO) | {{Name / contact, or 'N/A — DPO not required'}} |
| Assessment Trigger | {{New system / major change / periodic review — why this PIA is being run now}} |
| Risk Level (overall) | {{Low / Medium / High — set after §6}} |
| Prior-Consultation Required | {{Yes (residual high risk) / No}} |

---

## 1. Introduction

> This section sets up everything that follows: why the document exists, exactly what it covers, the vocabulary a reader needs, and which laws this builds on. Read the definitions first — the rest of the document leans on them.
>
> One framing to internalize up front: **a privacy impact assessment is about risks to people, not risks to the organisation.** A security review asks "what threatens our system?" A PIA asks "what does our system threaten about the people whose data it holds?" Those are different questions, and the second one is the one teams most often skip. Everywhere this document says "risk," it means risk *to the data subjects* unless it says otherwise.

### 1.1 Purpose

> One-paragraph statement of what this document is for and what it produces. Establish that it is the single place where this system's personal-data handling, the privacy risks that handling creates, the safeguards that address them, and the disclosures owed to people are recorded.

{{This document assesses the privacy risks of processing personal data in {{System Name}} and records the safeguards and disclosures that bring residual risk down to an acceptable level. It produces three linked artefacts at once: the DPIA / PIA itself (the risk assessment), the Record of Processing Activities (the data inventory in §3), and the privacy-notice scaffolding (what data subjects must be told, in §8). The goal is not zero data collection — a working system needs data — but to make the personal-data handling visible, justified, minimised, and deliberately protected before the system reaches the people it affects.}}

### 1.2 Scope

> Be concrete about which system, which version, and which processing activities this assessment covers, and state plainly what is out of scope. A PIA for "the app, generally" is not actionable; a PIA for "the v2 account system and its analytics pipeline, covering signup through deletion" is. Name the life-cycle stages covered (collection, storage, use, sharing, retention, deletion) so a reader knows the assessment traces data from entry to end-of-life.

In scope:
- System / version: {{name and version of the system being assessed}}
- Processing activities: {{collection, storage, use, sharing, retention, deletion — list the ones covered}}
- Life-cycle stages: {{from first collection through final deletion / anonymisation}}

Out of scope:
- {{Processing handled by a separate assessment — name where}}
- {{Components, integrations, or third-party services assessed elsewhere}}
- {{Anonymous / aggregate data that contains no personal data — but verify it is genuinely non-identifiable; see §6}}

### 1.3 Definitions

> Define the core vocabulary plainly. The terms below are the load-bearing ones — keep their definitions even if you trim the rest. A reader who understands these can read the whole document. Add project-specific terms in the empty rows.

| Term | Definition |
|---|---|
| DPIA / PIA | A written assessment of how a system processes personal data and what risks that creates for the people the data is about. GDPR Art. 35 *requires* one when processing is "likely to result in high risk" to those people; a PIA is the broader US/general equivalent and is good practice everywhere. |
| Personal data (PII) | Any information relating to an identified or identifiable living person — a name, email, location, an ID number, an online identifier, a device fingerprint, and so on. If a piece of data can be tied back to a specific person, directly or in combination with other data, it is personal data. |
| Special-category data | The sensitive subset of personal data with stricter rules: health, biometrics, genetic data, racial/ethnic origin, religious or political beliefs, sex life or orientation, trade-union membership. Processing it usually needs a stronger justification and stronger safeguards. |
| Data subject | The living person the personal data is about. (CPRA calls them a "consumer.") The risks this document assesses are risks to data subjects, *not* to the company. |
| Data controller | The party that decides *why* and *how* personal data is processed. The controller carries primary legal responsibility. |
| Data processor | A party that handles personal data *on the controller's behalf* (e.g., a hosting provider, an email service). The role determines who carries which obligations; a processor acts only on documented instructions. |
| Processing | Almost anything done with personal data — collecting, storing, reading, organising, combining, sharing, exporting, deleting. Even merely *holding* data is processing. |
| Lawful basis | Under GDPR you need a specific legal justification to process personal data *at all* — e.g., consent, performance of a contract, legal obligation, vital interests, public task, or legitimate interests. You pick one per processing purpose. "We wanted to" is not a lawful basis. |
| Records of Processing Activities (RoPA) | The GDPR Art. 30 inventory of what data you process, why, who you share it with, where it goes, and how long you keep it. §3 of this template *is* a RoPA; keeping it current is itself a compliance deliverable. |
| Data subject rights | What people can demand of you: access (a copy of their data), correction, deletion ("right to be forgotten"), portability (their data in a reusable format), objection to processing, and — under CPRA — opting out of the "sale" or "sharing" of their data. The system must be able to honour these. |
| Data minimisation | The principle that you collect only the personal data the purpose actually needs — no "nice to have" fields, no hoarding. |
| Retention | How long you keep data. The principle: keep it only as long as the purpose needs, then delete or anonymise it. |
| Inherent vs. residual risk | *Inherent* risk is the risk before any safeguards. *Residual* risk is what is left *after* safeguards are in place. Reviewers and regulators care most about the residual number. |
| Cross-border transfer | Moving personal data to a jurisdiction outside the one it was collected in (e.g., EU → US). Often needs an extra legal mechanism (an adequacy decision, standard contractual clauses, etc.). |
| {{Project term}} | {{Definition}} |

### 1.4 References

> List the external obligations this assessment is measured against and the internal documents it builds on. Categorise for readability. The external list drives the compliance mapping in §9; the internal list (SRS, SDD, security policy) supplies the system facts the rest of the PIA relies on.

External standards and regulations:
- GDPR (Regulation (EU) 2016/679), Art. 35 — Data Protection Impact Assessment.
- GDPR (Regulation (EU) 2016/679), Art. 30 — Records of Processing Activities.
- CCPA / CPRA (California Consumer Privacy Act, as amended by the California Privacy Rights Act) — consumer rights and notice duties.
- OWASP AI Security & Privacy Guide — model-specific privacy risks (training-data leakage, membership-inference, model inversion).
- NIST SP 800-53 Rev. 5 — privacy control families used as a control catalogue in §7.
- {{Sector rule, if any — e.g., HIPAA, FERPA, GLBA, PIPEDA, UK GDPR}}

Internal documents:
- {{path/to/SRS.md}} — system requirements, including what data the system must handle.
- {{path/to/SDD.md}} — design, including where data is stored and how it flows.
- {{path/to/security-policy.md}} — organisational safeguards this PIA references.
- {{path/to/data-retention-policy.md}} — retention rules referenced in §5.

---

## 2. System Overview and Data Flows

> Describe what {{System Name}} does and, in plain language, *how personal data moves through it*. A reader should be able to trace one person's data end to end before they reach any risk section. Cover four things: where data **enters** (collection points — signup forms, imports, sensors, cookies), where it is **stored** (databases, files, caches, backups, logs), what **processes** touch it (services, jobs, analytics, the model if it is an AI system), and where it **leaves** (sharing with third parties, exports, deletion). A simple numbered flow or a small diagram is ideal; the point is that the data journey is legible, not buried in architecture.

### 2.1 What the System Does

{{One or two paragraphs in plain language: what {{System Name}} is for and what it does with people's data at a high level. Avoid implementation detail here — that lives in the SDD. Focus on the personal-data story.}}

### 2.2 Data Flow

> Number each step so later sections can cross-reference it. Trace a single data subject's data from first contact to deletion.

1. **Collection** — {{e.g., the data subject submits a signup form; PD-1, PD-2 enter here}}.
2. **Transport** — {{e.g., sent over TLS to the application server}}.
3. **Storage** — {{e.g., written to the `users` table in the primary database; backed up nightly}}.
4. **Use / processing** — {{e.g., used to authenticate the user and personalise content}}.
5. **Sharing** — {{e.g., email shared with the transactional email provider (processor); analytics events sent to {{provider}}}}.
6. **Retention / deletion** — {{e.g., retained while the account is active, deleted 30 days after account closure}}.

### 2.3 Data Flow Diagram (optional)

> A small diagram makes the flow legible at a glance. ASCII, Mermaid, or a linked image are all fine for a lightweight assessment.

```
{{Data subject}} ──▶ [ Collection point ] ──▶ [ {{System Name}} ] ──┬──▶ [ Datastore ]
                                                                    ├──▶ [ Processor: {{name}} ]
                                                                    └──▶ [ Third party: {{name}} ]
```

### 2.4 Actors and Roles

> Name who is the controller, who are processors, and any third parties, so §3 and §4 can reference them consistently.

| Actor | Role | Notes |
|---|---|---|
| {{Your entity}} | Controller | Decides why and how data is processed. |
| {{Hosting / email / analytics provider}} | Processor | Acts on documented instructions; covered by a data-processing agreement. |
| {{Third party receiving data}} | {{Controller / Processor / Recipient}} | {{What they receive and why}} |

---

## 3. Personal Data Inventory (RoPA)

> Tabulate **every category of personal data the system handles**, one row per category. This table is the GDPR Art. 30 *Record of Processing Activities* — keeping it current is itself a compliance deliverable, not just input to the rest of this document. Each row gets an ID (PD-N) so the risk, lawful-basis, and safeguard sections can point at exactly which data they mean.
>
> For each category record: what it is, whether it is special-category/sensitive, where it came from, where it is stored, who can access it, how long it is kept, and whether it crosses a border. If a row is special-category, flag it loudly — those rows usually drive the highest-risk findings in §6 and need a stronger lawful basis in §4.

| ID | Data category | Special category? | Source | Stored where | Who can access | Retention | Cross-border transfer? |
|---|---|---|---|---|---|---|---|
| PD-1 | {{e.g., Email address}} | No | {{Signup form}} | {{`users` table; nightly backup}} | {{App service; support staff}} | {{Life of account + 30 days}} | {{No / Yes → {{country}} via {{mechanism}}}} |
| PD-2 | {{e.g., IP address / device identifier}} | No | {{Automatically on request}} | {{Access logs}} | {{Ops / on-call}} | {{90 days}} | {{No}} |
| PD-3 | {{e.g., Health information}} | **Yes** | {{User-provided}} | {{Encrypted `health` table}} | {{Restricted role only}} | {{Until withdrawal of consent}} | {{No}} |
| PD-N | {{...}} | {{Yes / No}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

> **Keep this table alive.** Whenever a new field is collected, a new datastore added, or a new third party brought in, add or amend a PD-N row and bump the version in §12. A stale inventory is a compliance gap, not a documentation nicety.

---

## 4. Processing Purposes and Lawful Basis

> For each distinct *reason* the system processes data, give a purpose (PURP-N) and tie it to a lawful basis (LB-N), referencing the PD-N categories it uses. The discipline here is **one lawful basis per purpose**, and **no data used beyond the purpose it was collected for** (this is "purpose limitation" — data collected to log you in should not silently become marketing data).
>
> Under GDPR the lawful basis must be one of: consent, performance of a contract, legal obligation, vital interests, public task, or legitimate interests. If you rely on *consent*, the system must be able to record it and let people withdraw it. If you rely on *legitimate interests*, you should be able to show you weighed your interest against the data subject's rights (a "legitimate interests assessment").
>
> Under CPRA, also note whether the activity counts as a **"sale"** or **"sharing"** of personal information (these have broad legal meanings — sharing for cross-context behavioural advertising counts), and how the data subject's **opt-out** is honoured.

### 4.1 Purposes and Bases

| ID | Processing purpose | Data used (PD-N) | Lawful basis (LB-N) | Basis type | CPRA: sale/share? | Opt-out path |
|---|---|---|---|---|---|---|
| PURP-1 | {{e.g., Authenticate users / run the account}} | PD-1, PD-3 | LB-1 | {{Contract}} | No | n/a |
| PURP-2 | {{e.g., Send transactional email}} | PD-1 | LB-2 | {{Legitimate interests}} | No | {{Unsubscribe link}} |
| PURP-3 | {{e.g., Product analytics}} | PD-2 | LB-3 | {{Consent}} | {{Yes (sharing) / No}} | {{Cookie banner / "Do Not Sell or Share" link}} |
| PURP-N | {{...}} | {{PD-N}} | {{LB-N}} | {{Consent / Contract / Legal obligation / Vital interests / Public task / Legitimate interests}} | {{Yes / No}} | {{...}} |

### 4.2 Lawful-Basis Notes

> For any basis that needs justification, record it here. Consent needs a record + withdrawal path; legitimate interests needs a balancing note.

- **LB-3 (Consent)** — {{How consent is captured, recorded, and withdrawn. Where the record lives.}}
- **LB-2 (Legitimate interests)** — {{Brief balancing test: our interest vs. the data subject's reasonable expectations and rights, and why ours does not override theirs.}}
- **LB-N** — {{...}}

---

## 5. Necessity, Proportionality, and Data Minimisation

> This is where you show the processing is *justified* — the question GDPR Art. 35 expects a DPIA to answer head-on. For each purpose, demonstrate two things: **necessity** (you genuinely need this data to achieve the purpose — could you do it with less, or with anonymised/aggregated data instead?) and **proportionality** (the privacy intrusion is in proportion to the benefit; you are not using a sledgehammer for a nail).
>
> Then state the **retention rule per data category** and exactly **how data is deleted or anonymised** at end of life. "We'll delete it eventually" is not a retention rule; "deleted 30 days after account closure by the nightly purge job, including from backups within the backup-rotation window" is. Anonymisation only counts if the result genuinely cannot be re-identified — see the re-identification risk in §6.

### 5.1 Necessity and Proportionality

| Purpose (PURP-N) | Data used (PD-N) | Why this data is necessary | Could less / anonymised data work? | Proportionate? |
|---|---|---|---|---|
| PURP-1 | PD-1, PD-3 | {{Needed to identify and serve the account holder}} | {{No — identity is intrinsic to the purpose}} | {{Yes}} |
| PURP-3 | PD-2 | {{Used to understand feature usage}} | {{Partly — could aggregate / truncate IPs}} | {{Yes, after minimisation}} |
| PURP-N | {{PD-N}} | {{...}} | {{...}} | {{Yes / No — if No, narrow the data}} |

### 5.2 Retention and Deletion

| Data (PD-N) | Retention period | Trigger for deletion | Deletion / anonymisation method | Covers backups? |
|---|---|---|---|---|
| PD-1 | {{Life of account + 30 days}} | {{Account closure}} | {{Hard delete via purge job}} | {{Yes — within backup rotation}} |
| PD-2 | {{90 days}} | {{Age}} | {{Log rotation / truncation}} | {{Yes}} |
| PD-N | {{...}} | {{...}} | {{Delete / anonymise — describe}} | {{Yes / No}} |

---

## 6. Risks to Data Subjects

> Assess harms to **the people**, not to the organisation. List each risk with an ID (PR-N), a plain-language description of *what could happen to a person*, the PD-N categories involved, and a **likelihood × severity** rating that gives an overall level. Rate the *inherent* risk here (before safeguards); §7 records what is left after safeguards.
>
> Common risk categories to walk through (a checklist, not a limit):
> - **Unauthorised access / breach** — data exposed to people who should not see it.
> - **Re-identification** — "anonymised" data turns out to be tie-able back to individuals, often by combining datasets.
> - **Profiling / discrimination** — inferences about a person lead to unfair or harmful treatment.
> - **Function creep** — data collected for one purpose quietly gets used for another (the purpose-limitation failure from §4).
> - **Inability to exercise rights** — the system cannot actually honour access/deletion/opt-out requests.
> - **Excessive retention** — data kept long after it was needed, enlarging the blast radius of any breach.
>
> **If this is an AI / ML system** (e.g., a personal-data-heavy assistant that learns from user data), draw on the OWASP AI Security & Privacy Guide for model-specific risks: **training-data leakage** (the model regurgitates personal data it was trained on), **membership-inference** (an attacker infers that a specific person's data was in the training set), and **model inversion** (reconstructing personal data from the model's outputs). Treat these as first-class PR-N rows, not footnotes.

### 6.1 Likelihood and Severity Scales

> Define the scales in words so two people scoring the same risk land in roughly the same place.

| Level | Likelihood | Severity (to the data subject) |
|---|---|---|
| Low | {{Unlikely under normal operation}} | {{Minor, reversible inconvenience}} |
| Medium | {{Plausible over the system's lifetime}} | {{Material harm — distress, financial loss, reputational damage}} |
| High | {{Expected unless actively prevented}} | {{Severe / irreversible — identity theft, discrimination, exposure of special-category data}} |

### 6.2 Risk Register

| ID | Risk to data subjects | Data involved (PD-N) | Likelihood | Severity | Inherent level |
|---|---|---|---|---|---|
| PR-1 | {{Unauthorised access to account data via credential leak}} | PD-1, PD-3 | {{Medium}} | {{High}} | {{High}} |
| PR-2 | {{Re-identification of "anonymised" analytics by joining IP + timestamps}} | PD-2 | {{Medium}} | {{Medium}} | {{Medium}} |
| PR-3 | {{Function creep — analytics data reused for marketing without basis}} | PD-2 | {{Medium}} | {{Medium}} | {{Medium}} |
| PR-4 | {{(AI) Training-data leakage — model echoes a user's private input to another user}} | PD-3 | {{Low}} | {{High}} | {{Medium}} |
| PR-5 | {{Inability to honour deletion requests because data persists in backups}} | PD-1, PD-3 | {{Medium}} | {{Medium}} | {{Medium}} |
| PR-N | {{...}} | {{PD-N}} | {{L/M/H}} | {{L/M/H}} | {{L/M/H}} |

---

## 7. Safeguards and Mitigations

> For each risk PR-N, list the controls that reduce it, each with an ID (SAFE-N). Cover both **technical** safeguards (encryption at rest and in transit, access control / least privilege, pseudonymisation, retention limits, rate-limiting, audit logging) and **organisational** ones (policies, staff training, data-processing agreements with processors, breach-response procedures). Where it helps a reviewer, **map each control to a NIST SP 800-53 Rev. 5 privacy control** (e.g., the AC access-control family, SC system-and-communications protection, the privacy-specific controls) — the mapping is optional but makes the assessment auditable.
>
> Then record the **residual risk** after the safeguards are in place. This is the number reviewers care about most. **If any residual risk stays "High," GDPR may require *prior consultation* with the supervisory authority before you proceed** — flag that in the metadata table (Prior-Consultation Required) and in §11.

### 7.1 Controls per Risk

| ID | Mitigates (PR-N) | Control | Type | NIST 800-53 (optional) | Residual risk |
|---|---|---|---|---|---|
| SAFE-1 | PR-1 | {{Encryption at rest + TLS in transit; MFA on accounts}} | Technical | {{SC-28, SC-8, IA-2}} | {{Low / Medium}} |
| SAFE-2 | PR-1 | {{Role-based access control; least privilege; access logging}} | Technical | {{AC-2, AC-6, AU-2}} | {{Low}} |
| SAFE-3 | PR-2 | {{IP truncation + aggregation before storage}} | Technical | {{—}} | {{Low}} |
| SAFE-4 | PR-3 | {{Purpose-limitation policy + review gate before any new data use}} | Organisational | {{—}} | {{Low}} |
| SAFE-5 | PR-4 | {{Exclude special-category inputs from training; output filtering; tenant isolation}} | Technical | {{—}} | {{Low / Medium}} |
| SAFE-6 | PR-5 | {{Deletion job covers backups within rotation window; documented in retention policy}} | Technical + Organisational | {{—}} | {{Low}} |
| SAFE-N | {{PR-N}} | {{...}} | {{Technical / Organisational}} | {{control ID}} | {{L/M/H}} |

### 7.2 Residual-Risk Summary

> Roll up the residual levels and state the overall position. This drives the Risk Level (overall) and Prior-Consultation fields in the metadata.

- Highest residual risk after safeguards: {{Low / Medium / High}}.
- Any residual **High** risks: {{list PR-N, or "none"}}.
- Prior consultation with a supervisory authority required: {{Yes — because PR-N remains High / No}}.

---

## 8. Data Subject Rights and Transparency

> Two jobs in one section. First, describe **how the system lets people exercise their rights** — access (a copy of their data), correction, deletion, portability, objection, and the CPRA opt-out of sale/sharing. For each, record *how a request arrives*, *how the requester's identity is verified* (so you do not hand one person's data to another), and *the deadline to respond* (GDPR generally one month; CPRA generally 45 days — confirm the current figures for your regime).
>
> Second, capture the **privacy-notice scaffolding**: the things you must *tell* data subjects — who you are, the purposes and lawful bases, what you collect, who you share it with, how long you keep it, their rights, and how to contact you or complain. This content is the source for the public-facing privacy notice, so writing it here means you write it once.

### 8.1 Rights Handling

| Right | How requests arrive | Identity verification | Response deadline | Notes / limits |
|---|---|---|---|---|
| Access | {{Account settings / email to privacy@}} | {{Logged-in session / verified email}} | {{e.g., 30 days}} | {{Provide PD-1..PD-N held}} |
| Correction | {{Self-service / request}} | {{...}} | {{e.g., 30 days}} | {{...}} |
| Deletion ("erasure") | {{Self-service / request}} | {{...}} | {{e.g., 30 days}} | {{Exceptions: legal-hold data}} |
| Portability | {{Request}} | {{...}} | {{e.g., 30 days}} | {{Machine-readable export}} |
| Objection / restriction | {{Request}} | {{...}} | {{e.g., 30 days}} | {{...}} |
| CPRA opt-out of sale/sharing | {{"Do Not Sell or Share" link / GPC signal}} | {{Not required for opt-out}} | {{e.g., 15 days for GPC}} | {{Honour browser opt-out signals}} |

### 8.2 Privacy-Notice Content (source for the public notice)

> Fill these once; they become the public privacy notice.

- **Who we are (controller):** {{name + contact}}.
- **What we collect:** {{summary referencing PD-1..PD-N}}.
- **Why (purposes & bases):** {{summary referencing PURP-N / LB-N}}.
- **Who we share with:** {{processors and third parties from §2.4}}.
- **How long we keep it:** {{summary referencing §5.2}}.
- **Your rights and how to exercise them:** {{summary referencing §8.1}}.
- **International transfers:** {{any cross-border transfers + mechanism, or "none"}}.
- **How to contact us / complain:** {{contact; right to lodge a complaint with a supervisory authority}}.

---

## 9. Compliance Mapping

> A traceability table showing how this assessment satisfies each external obligation. Map each requirement to the **section, table, or PD-N / PR-N / SAFE-N IDs** that address it, so a reviewer can confirm nothing was skipped. This is the section an auditor reads first; treat any "Gap" entry as an open question for §10.

| Requirement | Source | Addressed in | IDs | Status |
|---|---|---|---|---|
| Systematic description of processing | GDPR Art. 35(7)(a) | §2, §4 | PURP-N | {{Done / Gap}} |
| Necessity & proportionality assessment | GDPR Art. 35(7)(b) | §5 | PURP-N, PD-N | {{Done / Gap}} |
| Assessment of risks to data subjects | GDPR Art. 35(7)(c) | §6 | PR-N | {{Done / Gap}} |
| Measures to address the risks | GDPR Art. 35(7)(d) | §7 | SAFE-N | {{Done / Gap}} |
| Record of processing activities | GDPR Art. 30 | §3 | PD-1..PD-N | {{Done / Gap}} |
| Lawful basis recorded per purpose | GDPR Art. 6 | §4 | LB-N | {{Done / Gap}} |
| Notice / right to know | CPRA | §8.2 | — | {{Done / Gap}} |
| Consumer rights (access/delete/correct/opt-out) | CPRA | §8.1 | — | {{Done / Gap}} |
| {{Sector rule requirement}} | {{HIPAA / FERPA / …}} | {{§N}} | {{IDs}} | {{Done / Gap}} |

---

## 10. Open Questions

> Track unresolved items — undecided lawful bases, processing awaiting legal review, a cross-border transfer waiting on an adequacy decision, controls not yet implemented. One row each (OQ-N) with what is blocking and who must decide. Resolve and remove as work progresses.
>
> **An unresolved item tied to a High residual risk means the PIA is not yet complete** — you cannot sign off (§11) while a blocking question on a high-risk activity is still open.

| ID | Open question | Blocking | Owner / decider | Linked to | Target date |
|---|---|---|---|---|---|
| OQ-1 | {{Is legitimate interests or consent the right basis for PURP-3?}} | {{Legal review}} | {{DPO / counsel}} | LB-3, PURP-3 | {{YYYY-MM-DD}} |
| OQ-2 | {{Transfer to {{country}} pending adequacy / SCCs}} | {{Awaiting mechanism}} | {{Owner}} | PD-1 | {{YYYY-MM-DD}} |
| OQ-N | {{...}} | {{...}} | {{...}} | {{PD-N / PR-N / SAFE-N}} | {{YYYY-MM-DD}} |

---

## 11. Sign-Off and Review Schedule

> Record who reviewed and approved this assessment and when. At minimum: the **system owner** (accountable for the processing) and the **DPO / privacy lead** (or the person playing that role on a small team). If §7 left a residual **High** risk, record the outcome of the required **prior consultation** with the supervisory authority before deployment proceeds.
>
> Then state when the PIA must be **re-run**. A PIA is a living document, not a one-time gate: re-assess on any material change to the processing (new data, new purpose, new processor, new model) *and* on a periodic cadence even if nothing obvious changed.

### 11.1 Approvals

| Role | Name | Decision | Date |
|---|---|---|---|
| System owner | {{Name}} | {{Approved / Approved with conditions / Rejected}} | {{YYYY-MM-DD}} |
| DPO / privacy lead | {{Name or "N/A — DPO not required"}} | {{Approved / …}} | {{YYYY-MM-DD}} |
| Supervisory authority (if prior consultation) | {{Authority}} | {{Outcome}} | {{YYYY-MM-DD}} |

### 11.2 Review Schedule

- **Trigger-based review:** re-run this PIA on {{any new data category, new purpose, new processor/third party, new model, or change of lawful basis}}.
- **Periodic review:** at least every {{6 / 12}} months regardless of change.
- **Next scheduled review:** {{YYYY-MM-DD}}.

---

## 12. Revision History

> Standard version/date/author/changes table. Bump the version on **every substantive change** — especially any change to the data inventory (§3), the processing purposes (§4), or the residual-risk ratings (§7), since those are exactly what drives the compliance obligations.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — the definitions carry the rest of the document)
- §2 System Overview and Data Flows
- §3 Personal Data Inventory (RoPA) — also your Art. 30 record
- §4 Processing Purposes and Lawful Basis
- §6 Risks to Data Subjects
- §7 Safeguards and Mitigations (including the residual-risk summary)
- §11 Sign-Off and Review Schedule
- §12 Revision History

**Optional sections** (include if relevant):
- §2.3 Data Flow Diagram (omit if the numbered flow is clear enough)
- §5 Necessity, Proportionality, and Data Minimisation (strongly recommended; GDPR Art. 35 expects it — omit only for a true early prototype with placeholder data)
- §8 Data Subject Rights and Transparency (required wherever GDPR or CPRA applies; optional only if no real personal data is in play yet)
- §9 Compliance Mapping (omit if no external regime applies; keep it the moment one does)
- §10 Open Questions (track elsewhere if you prefer — but do not lose blocking high-risk items)

**Identifier conventions**:
- PD-N: personal-data categories (the §3 inventory rows)
- PURP-N: processing purposes
- LB-N: lawful-basis entries
- PR-N: privacy risks to data subjects
- SAFE-N: safeguards / mitigations
- OQ-N: open questions

These prefixes enable cross-document and intra-document traceability — a purpose (PURP-N) cites the data it uses (PD-N), a risk (PR-N) cites the data involved, a safeguard (SAFE-N) cites the risk it reduces, and the compliance map (§9) cites all of them so a reviewer can confirm nothing was skipped.

**Tailoring**:
- The section order loosely follows the GDPR Art. 35 elements (describe → justify → assess risk → mitigate) plus the Art. 30 inventory and the notice content. Add or drop subsections as the system needs.
- Keep §3 (the RoPA) current independently of the rest — it is a standing deliverable, not a one-time artefact.
- One lawful basis per purpose, and no data used beyond the purpose it was collected for: if a single PURP-N seems to need two bases, it is probably two purposes.
- The risk levels in the examples are illustrative — set your own scales in §6.1 and apply them consistently.

**For regulated/safety-critical projects:** use the full GDPR (and CCPA/CPRA) text and obtain qualified data-protection / legal review, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products; it is a starting skeleton, not legal advice, and a residual "High" risk should go to a qualified reviewer (and, where required, to prior consultation with the supervisory authority) before deployment.
