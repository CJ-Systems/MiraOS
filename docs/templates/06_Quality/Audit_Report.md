# Audit Report Template

> **Template purpose:** Lightweight Audit Report structure following IEEE 1028-2008 (with IEEE 828-2012 for configuration audits). Use this template to record the objective evidence, findings, and conclusion of a single software audit. Replace `{{placeholder}}` content with audit-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** After you have performed an audit — an independent, evidence-based check that some process, product, baseline, or supplier conforms to its plans, procedures, standards, or contract. This is a *record* document (the output of one audit event), so fill it in after the audit, in past tense ("the auditor examined..."), not as a plan. If you are reviewing a work product to improve it, that is a *review*, not an audit — use the review template instead.
>
> **Companion standard:** IEEE 1028-2008 — Standard for Software Reviews and Audits (the audit process: roles, audit procedure, evidence, findings); IEEE 828-2012 — Standard for Configuration Management in Systems and Software Engineering (configuration / baseline audits — functional and physical configuration audits).
>
> **Status of this template:** Lightweight, public, reusable structure for an IEEE 1028-2008 software audit (with IEEE 828-2012 for functional/physical configuration audits). Faithful to the IEEE 1028 audit-process outline (criteria → method → evidence → findings → corrective actions → conclusion) but reduced for solo/small-team use. WARNING: IEEE 1028-2008 and IEEE 828-2012 are paywalled standards — this template was authored from the publicly documented structure of the audit process and was NOT copied from the standards' text. Verify section requirements against the full purchased standards before relying on this for regulated, safety-critical, contractual, or certification audits, where the complete normative wording and any mandated forms apply. This is a record/instance document (the output of one audit event), so it intentionally runs leaner than the design/requirements templates and is not padded to a fixed section count.

---

# Audit Report — {{Project Name}}

| Field | Value |
|---|---|
| Document ID | AUD-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | IEEE 1028-2008 (+ IEEE 828-2012 if configuration audit) (lightweight) |
| Owner | {{Project name or owner}} |
| Audit Type | {{Process audit / Functional Configuration Audit (FCA) / Physical Configuration Audit (PCA) / Supplier audit / Compliance audit}} |
| Audited Area | {{Process / product / baseline / records / supplier audited}} |
| Audit Date(s) | {{YYYY-MM-DD or range}} |
| Audit Criteria Baseline | {{Plans / procedures / baseline version the audit measured against}} |
| Distribution | {{Who receives this report — owner, audited area lead, CM authority}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> Fold the usual Purpose, Scope, Definitions, and References into four short subsections. Keep each tight — this is a record of a specific audit, not a standing reference document.
>
> Beginner note: an **audit** (formal sense) is an independent, evidence-based check that work conforms to its plans, procedures, standards, or contract. Unlike a *review* (which improves a work product) or a *test* (which exercises behavior), an audit asks "does the actual state match what was promised or required?" and produces objective evidence either way. IEEE 1028 is the standard that defines this process.

### 1.1 Purpose

> One paragraph: state why this report exists — that it records the objective evidence, findings, and conclusion of a specific audit performed under IEEE 1028, and that it is the authoritative record of that audit's result. Beginner note: a report is the *output* of an audit event, so write it after the audit, in past tense ("the auditor examined..."), not as a plan.

This report records the objective evidence, findings, and conclusion of the {{audit type}} audit of {{audited area}} for {{Project Name}}, performed under IEEE 1028-2008{{ and, for baseline/configuration audits, IEEE 828-2012}}. It is the authoritative record of that audit's result and the basis for any corrective actions in §9.

### 1.2 Scope

> State what this report covers and explicitly what it excludes. Beginner note: scope here is the *audit's* scope (which processes / products / baselines were examined) — anything not examined cannot be concluded on, so naming exclusions protects the reader from over-reading the conclusion.

Covered: {{processes / products / baselines / records / suppliers actually examined}}.

Not covered / excluded: {{areas deliberately left out — and why, e.g. "out of scope," "covered by a separate audit," "not yet baselined"}}.

### 1.3 Definitions, Acronyms, and Abbreviations

> Define audit-specific terms used in this report so a non-specialist reader is not gated out. At minimum define the finding classifications used (conformance, nonconformance, observation), the severity scale, and any FCA/PCA terms if this is a configuration audit.

| Term | Definition |
|---|---|
| Audit criteria | The yardstick measured against — the specific plans, procedures, requirements, acceptance criteria, standards, or contract clauses the audited area is supposed to satisfy. A finding only means something relative to a stated criterion. |
| Objective evidence | What was actually observed (a document, screenshot, interview answer, config value, log entry). Findings rest on objective evidence, not opinion. |
| Finding | A single recorded observation from the audit, tagged FND-N — a fact plus its classification and severity. One finding = one issue. |
| Conformance | A finding where the audited area meets the criterion. |
| Nonconformance | A finding where the audited area fails to meet a criterion (a real deviation that needs fixing). |
| Observation | A minor or improvement note that is not a strict failure against a criterion. |
| Corrective action | The agreed fix for a nonconformance: what changes, who owns it, when it is due, and how the fix will be verified (closed-loop). |
| Severity | How serious a finding is — e.g. {{Critical / Major / Minor}}. Independent of status. |
| Status | Where a finding or action stands — e.g. {{Open / In-progress / Closed / Waived}}. Independent of severity. |
| FCA — Functional Configuration Audit | (IEEE 828) Checks that the product actually does what its requirements say. |
| PCA — Physical Configuration Audit | (IEEE 828) Checks that the delivered items (files, versions, build artifacts) match the documented configuration list. |
| Baseline | A formally agreed, version-locked snapshot of work products that changes only through controlled change. Configuration audits verify a baseline. |
| {{Other term}} | {{Definition}} |

### 1.4 References

> List the audit criteria sources (plans, procedures, requirements, contract, standards) and any prior audit reports. Beginner note: these references ARE the yardstick — every finding points back to one of these. Categorize: criteria documents, baselines audited, applicable standards (IEEE 1028-2008; IEEE 828-2012 if configuration), prior reports.

Criteria documents (the yardstick):

| Ref | Document |
|---|---|
| R1 | {{Plan / procedure / requirement used as criterion — e.g. Configuration Management Plan §4.2}} |
| R2 | {{SRS / acceptance criteria / contract clause used as criterion}} |

Baselines audited (configuration audits):

| Ref | Document |
|---|---|
| R3 | {{Baseline ID and version — e.g. Release 1.2.0 configuration item list}} |

Applicable standards and prior reports:

| Ref | Document |
|---|---|
| R4 | IEEE 1028-2008 — Software Reviews and Audits |
| R5 | IEEE 828-2012 — Configuration Management in Systems and Software Engineering (if configuration audit) |
| R6 | {{Prior audit report — e.g. AUD-{{PROJECT-ID}}-000}} |

---

## 2. Audit Identification

> The "who / what / when" fingerprint of the audit, so a future reader can judge independence, recency, and type without reading the body.
>
> Beginner note: the Auditor field is load-bearing for trust. **Auditor independence** means the person auditing is not auditing their own work — that independence is what makes the evidence credible. IEEE 1028 calls this out. Record enough here that a reader can judge it (e.g. "auditor is from a different team than the auditee").

| Field | Value |
|---|---|
| Audit ID | AUD-{{PROJECT-ID}}-001 |
| Audit Type | {{Process / FCA / PCA / Supplier / Compliance}} |
| Audited Area | {{Process, product, baseline, records, or supplier}} |
| Baseline / Version audited | {{Baseline ID and version, if a configuration audit}} |
| Auditor(s) | {{Name / role — note independence from audited area}} |
| Auditee(s) / Area lead | {{Who represented the audited area}} |
| Audit Date(s) | {{YYYY-MM-DD or range}} |
| Report date | {{YYYY-MM-DD}} |

---

## 3. Audit Scope

> Describe precisely which processes, products, baselines, records, or suppliers were examined — and the boundaries (what was in the population but NOT examined, e.g. because of sampling).
>
> Beginner note: this differs from §1.2 in granularity — §1.2 is the report's framing; §3 is the concrete enumeration of what the auditor actually walked through. If **sampling** was used (examining a fraction of a larger population rather than every item), say what the full population was and what fraction was sampled, because a clean result on a sample is not the same as a clean result on everything.

Processes / products / baselines examined:

- {{Item}} — {{what about it was examined}}
- {{Item}} — {{what about it was examined}}

Sampling (if applicable): population of {{N}} {{items — e.g. change requests, source files, supplier deliverables}}, sampled {{n}} selected by {{method — random / risk-based / judgmental}}. Items NOT examined: {{remainder — and the implication: conformance is asserted only over the sample}}.

---

## 4. Audit Criteria

> List the specific plans, procedures, requirements, acceptance criteria, standards, and contract clauses the audited area was measured against. Each criterion should be referenceable (give it a Criterion ID) so findings can cite it.
>
> Beginner note: this is the most important section for making findings meaningful — a finding is always "X does not meet criterion Y." Without an explicit criterion, a "finding" is just an opinion. For a Functional Configuration Audit the criteria are the requirements; for a Physical Configuration Audit the criteria are the documented configuration item list.

| Criterion ID | Source (plan / procedure / requirement / standard clause) | What it requires |
|---|---|---|
| C1 | {{e.g. CM Plan §4.2}} | {{Every change must reference an approved change request}} |
| C2 | {{e.g. SRS REQ-12}} | {{The product must do X}} |
| C3 | {{e.g. Release 1.2.0 configuration item list}} | {{The delivered build must contain exactly the listed items at the listed versions}} |

---

## 5. Audit Method

> Describe how evidence was gathered: interviews, document/record inspection, observation of work in progress, tool or repository review, sampling approach, and any checklists used. State the audit procedure per IEEE 1028 (planning, opening, examination, recording, closing) at whatever depth fits.
>
> Beginner note: the method is what lets someone *repeat* or *trust* the audit — if two auditors followed this method they should reach the same findings. Name the techniques actually used; do not list techniques you did not use.

Methods used:

- {{Interviews — who, about what}}
- {{Document / record inspection — which records}}
- {{Observation / tool / repository review — which tools or repositories}}
- {{Checklist used — reference it if it exists}}

Audit procedure followed: {{planning → opening meeting → examination → recording of findings → closing meeting}} per IEEE 1028-2008.

---

## 6. Findings

> This is the heart of the report. Each row is one finding tagged FND-N, resting on objective evidence, classified by Type and Severity, with an owner and status. Keep one issue per row so findings can be tracked and closed individually.
>
> Beginner note: "Type" classifies the finding (Conformance / Nonconformance / Observation); "Severity" says how serious (Critical / Major / Minor); "Status" is where it stands (Open / In-progress / Closed / Waived). **Severity and status are independent axes** — a finding can be Major and Closed. Every finding's Evidence cell must point at something concrete (a doc ref, a config value, a log line) and its Criterion should trace to §4.

| ID | Finding | Criterion (§4) | Type | Severity | Evidence | Owner | Due Date | Status |
|---|---|---|---|---|---|---|---|---|
| FND-1 | {{Two of the sampled changes had no linked change request}} | C1 | Nonconformance | Major | {{Repo log: commits abc123, def456 reference no CR}} | {{owner}} | {{YYYY-MM-DD}} | Open |
| FND-2 | {{Build artifact list matches the documented CI list}} | C3 | Conformance | — | {{Release manifest vs. CI list, both attached}} | — | — | Closed |
| FND-3 | {{Procedure exists but is not yet linked from onboarding docs}} | C1 | Observation | Minor | {{Onboarding index has no link to the CM procedure}} | {{owner}} | {{YYYY-MM-DD}} | Open |

---

## 7. Positive Observations

> Record effective practices and conforming evidence worth preserving — not just what failed. These can be logged as FND-N rows with Type = Conformance, or listed here narratively.
>
> Beginner note: audits are not only about catching failures. Recording what was done well (a) gives a fair picture, (b) preserves good practice so it is repeated and not accidentally "reformed" away, and (c) keeps the report from reading as purely punitive, which improves the auditee's willingness to engage honestly next time.

- {{Effective practice / conforming evidence}} (ref FND-2 if logged as a finding)
- {{Effective practice / conforming evidence}}

---

## 8. Nonconformances

> Pull the subset of §6 findings whose Type = Nonconformance and describe each deviation in enough detail that the owner understands exactly what failed and why it matters. Reference the finding ID (FND-N) and the criterion it violated (§4).
>
> Beginner note: a **nonconformance** is a real failure-to-meet-criterion that requires a corrective action — distinct from an *observation* (a minor or improvement note that does not strictly fail a criterion). Each nonconformance here should map one-to-one to a corrective action in §9. State the impact / risk so the severity is justified, not just asserted.

- **FND-1** ({{Major}}) — failed criterion C1: {{two sampled changes had no linked change request}}. Impact: {{changes are untraceable to an approval, so unauthorized changes could ship undetected}}. → corrective action CA-1.
- **FND-N** ({{severity}}) — failed criterion {{C-id}}: {{what deviated}}. Impact: {{risk if not corrected}}. → corrective action CA-N.

---

## 9. Corrective Actions

> Each corrective action is tagged CA-N, names the finding(s) it resolves (FND-N), the owner, the due date, and — critically — the verification method that will confirm the fix actually closed the gap (closed-loop).
>
> Beginner note: "corrective" means it addresses an *existing* nonconformance (vs. "preventive," which guards against *future* ones). A corrective action is not done when the change is made — it is done when the change is *verified*. The Verification Method column is what closes the loop; without it, actions silently rot in "open."

| Action ID | Resolves (FND-N) | Action | Owner | Due Date | Verification Method | Status |
|---|---|---|---|---|---|---|
| CA-1 | FND-1 | {{Add a pre-merge check that rejects commits with no linked change request}} | {{owner}} | {{YYYY-MM-DD}} | {{Re-audit a fresh sample of 10 changes; all must link a CR}} | Open |
| CA-2 | FND-3 | {{Link the CM procedure from the onboarding index}} | {{owner}} | {{YYYY-MM-DD}} | {{Re-check onboarding index has the link}} | Open |

---

## 10. Conclusion

> Summarize the overall audit result (pass / pass-with-actions / fail, or conform / conform-with-nonconformances), the count and severity profile of findings, residual risk, and — for a configuration audit — an explicit statement of whether the baseline is accepted (FCA/PCA disposition per IEEE 828).
>
> Beginner note: the conclusion must be supportable only by the evidence in §6–§9 — do not conclude anything about areas that were not examined (§3). State the disposition plainly (is the audited area accepted, accepted with required corrective actions, or rejected?) and name the residual risk a reader is accepting if the open actions are not yet closed.

Overall result: {{disposition — e.g. "conform with nonconformances; accepted subject to CA-1 and CA-2"}}.

Findings: {{n}} nonconformances ({{by severity — e.g. 1 Major, 0 Critical}}), {{n}} observations, {{n}} positive observations.

Residual risk: {{what risk the reader accepts while open corrective actions remain unclosed}}.

Baseline disposition (if configuration audit): {{accepted / accepted with corrective actions / rejected}}.

---

## 11. Open Questions

> Items raised during the audit that are unresolved and not yet a finding — ambiguous criteria, evidence the auditor could not obtain, or scope the auditor and auditee did not agree on. Distinguish these from nonconformances: an open question is "we could not yet determine conformance," not "it failed."
>
> Beginner note: it is honest and useful to record what the audit could NOT settle. Hiding open questions makes the conclusion look stronger than the evidence supports. Resolve and remove (or promote to a finding) as they close.

- **OQ-1** {{question}} — {{what is blocking, who must decide, by when}}.
- **OQ-2** {{question}} — {{what is blocking, who must decide, by when}}.

---

## 12. Revision History

> MUST be the last body section. Track every substantive change to this report with a version bump, date, author, and description. Beginner note: an audit report is a record that others act on (corrective actions, sign-off), so changes after issue must be traceable — a silently edited audit report is not trustworthy. Re-issues (e.g. after corrective actions are verified) get their own row.

| Version | Date | Author | Description of Change | Approval |
|---|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft | {{pending}} |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (all subsections — the criteria references in §1.4 anchor every finding)
- §2 Audit Identification (the independence record)
- §4 Audit Criteria (without explicit criteria, findings are just opinions)
- §5 Audit Method
- §6 Findings
- §10 Conclusion
- §12 Revision History

**Optional sections** (include if relevant):
- §3 Audit Scope (fold into §1.2 for a very small audit, but keep it separate whenever sampling was used)
- §7 Positive Observations (recommended — keeps the report fair and non-punitive; omit only if nothing notable)
- §8 Nonconformances (omit if §6 had zero nonconformances; otherwise it must map one-to-one to §9)
- §9 Corrective Actions (omit only if there are no nonconformances to correct)
- §11 Open Questions (track elsewhere if you prefer; do not bury unresolved items inside the conclusion)

**Identifier conventions**:
- AUD-{{PROJECT-ID}}-NNN: the audit report document and the audit instance itself
- FND-N: individual findings — referenced from §8 Nonconformances and §7 Positive Observations, and traced back to evidence (§6) and criterion (§4)
- CA-N: corrective actions — each links to the finding(s) FND-N it resolves
- C-N: audit criteria in §4 — cited by each finding in §6
- OQ-N: open questions

These prefixes enable cross-document traceability: a criterion (C-N) often points at a requirement in the SRS (REQ-N) or a CM plan clause; a finding (FND-N) cites the criterion; a corrective action (CA-N) cites the finding. Following the chain backward — CA → FND → C → source — lets a reader confirm any conclusion rests on real evidence against a real requirement.

**Tailoring**:
- The section list from IEEE 1028 is guidance, not a fixed form. Add/remove subsections as the audit needs.
- **Solo developer / very small team:** collapse aggressively. Keep §4 (Criteria), §6 (Findings), §9 (Corrective Actions), §10 (Conclusion), and §12 (Revision History) — these are the irreducible core (what you measured against, what you found, what you'll fix, the verdict, and a change trail). Fold §1.2 Scope and §3 Audit Scope together; record §2 Audit Identification as a couple of lines rather than a table; drop §7/§8/§11 if empty. Even a one-person team should keep §4 and §6 distinct — separating the yardstick from the observations is what stops "I audited it and it's fine" from being unfalsifiable.
- **Auditing your own work (no independent auditor available):** record that plainly in §2 Auditor(s) ("self-audit — no independent auditor") so a reader can weight the evidence accordingly. A self-audit is better than no audit, but the independence caveat must be visible.
- Re-issue the report (new Revision History row, bumped version) when corrective actions are verified, rather than silently editing the original — the audit trail is the point.

**For regulated/safety-critical projects:** use the full IEEE 1028-2008 (and IEEE 828-2012 for configuration audits), not this lightweight version. Those standards specify the complete normative wording, roles, and any mandated forms required for contractual, certification, or safety-critical audits.
