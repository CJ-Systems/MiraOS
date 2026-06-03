# Test Incident / Defect Report Template

> **Template purpose:** Lightweight Test Incident / Defect Report structure inspired by ISO/IEC/IEEE 29119-3:2021 (test incident reporting) with anomaly classification per IEEE 1044-2009. Use this template to document a single thing that looked wrong during testing — from "something happened" through investigation to a decided outcome. Replace `{{placeholder}}` content with incident-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** The moment a test fails, a tester sees behavior that does not match the requirement or test case, or anyone observes something during testing that needs looking into. One report covers **one** incident (and, at most, the one defect it turns out to be). This report sits downstream of the Test Plan and the test runs it drives: the plan said HOW you would test, a test run produced a result, and this report captures the result that needs investigation. Open it as soon as the incident is noticed — fill in the later sections (Analysis, Resolution, Verification) as the investigation proceeds.
>
> **Companion standard:** ISO/IEC/IEEE 29119-3:2021 (test incident reporting) + IEEE 1044-2009 (anomaly classification). The 29119-3 part gives the incident-report structure; IEEE 1044 gives the vocabulary for classifying the anomaly once you know what it actually was (type, severity, lifecycle state).
>
> **Status of this template:** Lightweight, public, reusable structure faithful to the outline of ISO/IEC/IEEE 29119-3:2021 (test documentation — incident reporting) with anomaly classification per IEEE 1044-2009. Both companion standards are paywalled ISO/IEEE publications — this template paraphrases their section structure and concepts in original wording and reproduces NO normative text, tables, or figures from either standard. It is a tailored extract for solo/small-team and internal use; verify section completeness and field names against the purchased standards for regulated, safety-critical, or contractual contexts. Reduced from the full incident-report set: omit fields that do not apply to your project rather than padding empty ones.

---

# Test Incident / Defect Report — {{System Name}}

| Field | Value |
|---|---|
| Document ID | INC-{{PROJECT-ID}}-001 |
| Version | 0.1 (draft) |
| Date | {{YYYY-MM-DD}} |
| Status | Draft |
| Standard | ISO/IEC/IEEE 29119-3:2021 + IEEE 1044-2009 (lightweight) |
| Owner | {{Project name or owner}} |
| Incident ID | INC-{{PROJECT-ID}}-001 |
| Defect ID | DEF-{{PROJECT-ID}}-001 (assigned once confirmed a defect; "N/A — not a defect" if triage rejects it) |
| Reported by | {{Name / role}} (who observed and logged the incident) |
| Assigned to | {{Owner / role}} (current owner for investigation or fix) |
| Build / Version under test | {{build identifier where the incident was observed}} |
| Test environment | {{environment name / config — e.g. staging, OS, browser, data set}} |
| Current status | New / Triaged / Assigned / Fixed / In Retest / Closed / Rejected / Deferred / Duplicate |
| Severity | Critical / Major / Moderate / Minor / Cosmetic (impact axis) |
| Priority | P1 / P2 / P3 / P4 (scheduling axis) |
| Date reported | {{YYYY-MM-DD}} |
| Prepared by | {{Name / role}} |
| Reviewed by | {{Names / roles}} |
| Approved by | {{Approval authority}} |

---

## 1. Introduction

> Standard opener. This is a **record**, not a spec — keep the introduction short. Its job is to orient a reader once: what this report is, the one-report-equals-one-incident rule, the handful of terms that make the rest readable, and what it points back to. A beginner note on the load-bearing distinction up front: an **incident** is anything observed during testing that needs looking into; a **defect** (also called a fault or bug) is a confirmed flaw in the product itself. Not every incident is a defect — the cause might be a bad test case, a misconfigured environment, behavior the tester misread, or user error. This report walks one incident from "something looked wrong" to a decided outcome. Delete this blockquote once the section is filled.

### 1.1 Purpose

> One sentence. State that this report documents a single incident, its investigation, and its outcome, and names the standards it follows.

{{This report documents a single test incident, its investigation, and its outcome, in conformance with ISO/IEC/IEEE 29119-3 and IEEE 1044-2009.}}

### 1.2 Scope

> State the one-report-one-incident rule plainly so the report does not become a junk drawer.

This report covers **one** incident, INC-{{PROJECT-ID}}-001, and at most the **one** defect it resolves to (DEF-{{PROJECT-ID}}-001). {{Multiple unrelated incidents get separate reports. If this incident turns out to be the same as one already filed, it is linked as a duplicate of the surviving report — not merged into it (see §9 Resolution).}}

### 1.3 Definitions, Acronyms, and Abbreviations

> Seed the table with the load-bearing pairs a beginner needs so the rest of the report reads cleanly. Add project-specific terms as needed; delete any you do not use.

| Term | Definition |
|---|---|
| Incident | Anything observed during testing that needs investigation — a failed test, a crash, a result that looked wrong. Not yet known to be a product flaw. |
| Defect (fault, bug) | A confirmed flaw in the product itself. A defect exists where actual behavior diverges from expected behavior in a way the product is responsible for. |
| Severity | How bad the impact is **if** the defect occurs — an objective property of the defect (data loss outranks a cosmetic typo). The impact axis. |
| Priority | How soon the defect should be fixed relative to other work — a business/scheduling decision, set by different people for different reasons than severity. The scheduling axis. |
| Reproducibility | Whether following the same steps reliably produces the same failure (Always / Intermittent / Once / Unable to reproduce). |
| Root cause | The underlying reason for the failure in code, data, or config — as opposed to the *symptom*, which is what the tester observed on screen. |
| Triage | The process where new incidents are reviewed, confirmed as defects (or not), assigned severity and priority, and routed to an owner. This report is what triage reads from and writes to. |
| {{Project term}} | {{Definition}} |

### 1.4 References

> List what was being tested and what informs this report, so the incident traces back to its sources. Use the upstream IDs already in play (REQ-N, TC-N, TR-N) so the chain is intact.

| Ref | Document / item |
|---|---|
| R1 | {{TC-N}} — test case under test |
| R2 | {{REQ-N}} — requirement / acceptance criterion under test |
| R3 | {{TP-PROJECT-ID-001 or path}} — governing Test Plan |
| R4 | {{Build / release notes for the version under test}} |
| R5 | ISO/IEC/IEEE 29119-3:2021 — test documentation (incident reporting) |
| R6 | IEEE 1044-2009 — classification for software anomalies |

---

## 2. Identification

> This is the most important section of a record document — it is what triage scans first. It answers **what, where, who, when** so anyone picking up the report cold has the coordinates and does not have to ask. Keep it a field/value table. One field deserves a beginner note: **Detected-in phase** matters because a defect found in production costs far more to fix than one found in unit test, and capturing the phase here feeds *defect-escape* metrics later (how many defects slipped past each test level). Delete this blockquote once filled.

| Field | Value |
|---|---|
| Incident ID | INC-{{PROJECT-ID}}-001 |
| Defect ID | DEF-{{PROJECT-ID}}-001 (or "N/A — not a defect") |
| Title / one-line summary | {{e.g. "Checkout total ignores applied promo code"}} |
| Reported by | {{Name / role}} |
| Date reported | {{YYYY-MM-DD}} |
| Assigned to | {{Owner / role}} |
| Build / version under test | {{build identifier}} |
| Test environment | {{OS / browser / config / data set — e.g. "staging, Ubuntu 24.04, Firefox 128, seed-data v3"}} |
| Related requirement | {{REQ-N}} |
| Related test case | {{TC-N}} |
| Related test run | {{TR-N}} |
| Reproducibility | Always / Intermittent / Once / Unable to reproduce |
| Detected-in phase | Unit / Integration / System / Acceptance / Production |
| Duplicate of / related to | {{INC-N or DEF-N, or "none"}} |

---

## 3. Summary

> A one-paragraph abstract a triage lead can read in ten seconds and route correctly. State the observed problem, the feature/component affected, and the user-visible impact, in plain language — **without** yet diving into reproduction steps or analysis (those have their own sections). Beginner tip: write the summary **last**, even though it appears near the front. You will only know the real story after Description and Analysis. A good summary is the report's "subject line" — specific enough to tell it apart from every other incident. "Checkout total ignores promo code" beats "Checkout broken." Delete this blockquote once filled.

{{One paragraph. What happened, where (which feature/component), and who it affects and how badly — at a glance. Example: "When a valid promo code is applied at checkout, the displayed order total does not reflect the discount, though the confirmation email shows the correct discounted amount. Affects all users of the checkout flow; customers are shown a higher total than they are charged, eroding trust."}}

---

## 4. Description

> This is where most reports fail a beginner, so the section is structured to force the parts that matter. The heart of every defect description is **expected vs. actual**: *expected* is what should have happened per the requirement or test case; *actual* is what did happen. A defect only exists where these two diverge in a way the product is responsible for. A report that says only "it broke" cannot be triaged — always state **both** halves. Keep the narrative tight; supporting artifacts (logs, screenshots) go in §6 Evidence, not here. Delete this blockquote once filled.

**Expected result:** {{What should have happened, citing the requirement or acceptance criterion. E.g. "Per REQ-N, applying a valid promo code reduces the displayed order total by the discount amount before checkout."}}

**Actual result:** {{What actually happened — quote exact error text or observed values. E.g. "The displayed total remained $48.00 (full price); no discount line appeared. Confirmation email charged $43.20." Do not paraphrase error messages — copy them.}}

**Impact:** {{Who is affected and how badly, tied to the user or business function. E.g. "Every customer applying a promo code sees a total higher than they are charged; support tickets and chargebacks likely."}}

**Context / preconditions:** {{Anything that had to be true for the incident to occur — account state, data set, feature flags, timing. E.g. "Logged-in account with an active cart of 2+ items; promo code FALL20 enabled; checkout-v2 feature flag on."}}

---

## 5. Steps to Reproduce

> A reproducibility-grade procedure. The test of a good repro is that **someone who has never seen the bug can follow the steps and watch it happen.** Number every step; one action per step; do not skip the "obvious" step — the obvious step is often exactly where the bug hides. Start from a stated clean state and end with the reproducibility rating. If the incident is **not** reproducible, say so plainly and point to §6 Evidence — for an intermittent or once-only failure, the captured artifacts are the only proof it occurred. Delete this blockquote once filled.

**Starting preconditions:** {{Clean state, logged-in user, specific data set — e.g. "Fresh browser session; logged in as standard customer; cart contains SKU-1001 ×2; promo code FALL20 valid and unused."}}

| Step | Action | Observed result at this step |
|---|---|---|
| 1 | {{Add SKU-1001 ×2 to the cart}} | {{Cart subtotal shows $48.00 — as expected}} |
| 2 | {{Proceed to checkout}} | {{Order summary shows $48.00 — as expected}} |
| 3 | {{Enter promo code FALL20 and click Apply}} | {{"Code applied" toast appears, but total still shows $48.00 — DIVERGES HERE}} |
| 4 | {{Complete the order}} | {{Confirmation email charges $43.20 (discount applied), contradicting the displayed total}} |

**Reproducibility:** {{Always / Intermittent / Once-only / Unable to reproduce.}} {{If intermittent, state observed frequency — e.g. "~1 in 5 runs; appears tied to a slow discount-service response."}}

---

## 6. Evidence

> Supporting artifacts. For intermittent or once-only defects, **the evidence IS the report** — without it there is nothing for a fixer to work from. Three habits make evidence usable: (1) capture it at the moment of failure — logs pulled after a restart are often useless; (2) **redact secrets and PII before attaching** (tokens, customer data, credentials) — this is non-negotiable for a shared or public report; (3) for a performance incident, record the measured number **and** the threshold it violated, not "felt slow." The evidence-store path below is a placeholder — attachments must never embed credentials. Delete this blockquote once filled.

| Artifact | Type | Location / link | What it shows |
|---|---|---|---|
| {{checkout-total.png}} | Screenshot | {{<evidence-store>/INC-PROJECT-ID-001/}} | {{Displayed total $48.00 after promo applied}} |
| {{app-2026-06-01.log}} | Log | {{<evidence-store>/INC-PROJECT-ID-001/}} | {{Discount computed server-side but not returned to the cart view}} |
| {{latency-trace.json}} | Trace / measurement | {{<evidence-store>/INC-PROJECT-ID-001/}} | {{Discount-service response 1.8s vs. 500ms timeout threshold}} |
| {{...}} | {{log / screenshot / video / trace / data file / measurement}} | {{link}} | {{what it demonstrates}} |

---

## 7. Severity and Priority

> This is where IEEE 1044 earns its place: classifying the anomaly. The two axes below are constantly conflated — keep them strictly separate. **Severity** = how bad the impact is if it occurs (objective, a property of the defect). **Priority** = how soon to fix it relative to other work (a business decision). They are independent. The canonical mismatches prove it: a *high-severity, low-priority* defect (data loss in a feature nobody uses yet) and a *low-severity, high-priority* defect (a typo on the login screen everyone sees). They are set by different people for different reasons. Delete this blockquote once filled.

### 7.1 Severity

> The impact axis. Pick one level and justify it against the actual impact and the scope of affected users/functions.

| Field | Value |
|---|---|
| Severity | Critical / Major / Moderate / Minor / Cosmetic |
| Rationale | {{Why this level — e.g. "Major: customers are mischarged relative to the displayed price; no data loss but direct trust and billing-correctness impact."}} |
| Scope of impact | {{Which users / functions — e.g. "All checkout users applying any promo code."}} |

### 7.2 Priority

> The scheduling axis. Record **who** set it and **why** — priority is a business call, not the tester's.

| Field | Value |
|---|---|
| Priority | P1 / P2 / P3 / P4 |
| Set by | {{Name / role — e.g. PM, triage lead}} |
| Rationale | {{Why this priority relative to other work — e.g. "P1: revenue-facing and customer-visible; fix targeted for the next hotfix build."}} |

### 7.3 Anomaly classification (optional, IEEE 1044)

> Optional sub-note carrying the IEEE 1044 attributes useful for trend analysis. Fill **Type** at triage; finalize **Mode** and **Insertion activity** once §8 Analysis is done. Delete if you are not tracking anomaly trends.

| Attribute | Value |
|---|---|
| Type | Logic / Data / Interface / Documentation / Standards |
| Mode (once analyzed) | {{e.g. wrong, missing, extra}} |
| Insertion activity (once analyzed) | {{phase where the flaw was introduced — e.g. requirements, design, coding}} |

---

## 8. Analysis

> The investigation record — this is what turns an **INC**ident into a confirmed **DEF**ect (or rejects it). The beginner anchor here is **root cause vs. symptom**: the *symptom* is what the tester saw (the wrong number on screen); the *root cause* is the underlying reason in code/data/config. Fixing the symptom without the root cause is exactly how a defect comes back. If analysis is not yet done, mark this section "under investigation" rather than leaving it blank — an empty Analysis on a report marked "Closed" is a process smell. Delete this blockquote once filled.

**Findings:** {{What the investigation revealed. E.g. "The discount is computed correctly in the pricing service but the cart-view component reads a cached pre-discount total when the discount-service response arrives after render."}}

**Root cause:** {{The underlying reason in code/data/config — distinct from the symptom in §4. E.g. "Race condition: cart total is rendered before the asynchronous discount response resolves, and there is no re-render on late arrival."}}

**Affected components:** {{Modules/files/services, traceable to the design (SDD). E.g. "cart-view component; discount-service client; no change needed in pricing service."}}

**Anomaly type (IEEE 1044, finalized):** {{Logic / Data / Interface / Documentation / Standards — e.g. "Logic (timing/concurrency)."}}

**Related / duplicate defects:** {{DEF-N links, or "none."}}

**Triage outcome:**
- [ ] **Confirmed a defect** → assign {{DEF-{{PROJECT-ID}}-NNN}}
- [ ] **Not a defect** → reason: {{test error / environment misconfiguration / works-as-designed / cannot reproduce}} — {{explain why}}

---

## 9. Resolution

> The decision-and-action record. Capture the chosen disposition **explicitly** — and note this beginner rule: every disposition except a plain "Fixed" still needs a paper trail. "Won't fix" is a legitimate, documented decision, not a silent drop. A deferred defect with no re-open condition is a defect that quietly disappears. Record the build/version any fix lands in. Delete this blockquote once filled.

**Disposition:** {{choose one}}

| Disposition | Details |
|---|---|
| Fixed | {{Describe the change; reference the commit/PR/change ID and the build/version it lands in — e.g. "PR #482; re-render cart total on late discount response; lands in build 2.4.1."}} |
| Workaround provided | {{What users do meanwhile — e.g. "Refresh the checkout page after applying a code to force a re-render."}} |
| Deferred | {{Reason + the condition that would re-open it — e.g. "Deferred to next sprint; re-open if customer support tickets exceed 5/week."}} |
| Rejected | {{Not a defect / won't fix, with rationale — e.g. "Works as designed: promo codes do not stack with member pricing; clarified in REQ-N."}} |
| Duplicate | {{Link to the surviving DEF-N this duplicates.}} |

---

## 10. Verification

> The close-out gate. State the **closure criteria** (what must be true to call this Closed) and record the **retest** that proves it. The beginner rule that matters most: **"Closed" means verified-fixed**, ideally by someone other than the fixer — a developer saying "done" is not verification. If the retest still fails, the report **re-opens**; record that loop here rather than silently editing Status. Delete this blockquote once filled.

**Closure criteria:** {{What must be true. Typically: the original §5 repro steps no longer produce the failure on the fixed build, AND a regression check confirms nothing adjacent broke. E.g. "Promo code applied → displayed total matches charged total on build 2.4.1; existing checkout regression suite passes."}}

**Retest record:**

| Field | Value |
|---|---|
| Retested by | {{Name / role — ideally not the fixer}} |
| Build retested | {{build identifier}} |
| Steps followed | {{Reference §5 Steps to Reproduce}} |
| Evidence | {{Link to the passing test run — TR-N}} |
| Result | Pass (proceed to Closed) / Fail (re-open — see §12 Status History) |

---

## 11. Open Questions

> House-standard Open Questions, placed before the audit trail. For a record document this is short and incident-specific — not a project-wide tracker. List anything still unresolved that blocks **closing this report**; each item names what is blocking and who must decide. Resolve and delete items as the incident moves toward Closed. Beginner note: an open question on a report still in New/Triaged is normal; an open question on a report marked "Closed" means it was closed prematurely. Delete this blockquote once filled.

- **OQ-1**: {{e.g. "Root cause not yet confirmed, awaiting production logs from ops."}} — {{what is blocking, who must decide}}
- **OQ-2**: {{e.g. "Severity disputed between tester and PM; needs triage decision."}} — {{who decides}}

---

## 12. Status History

> The **defect-lifecycle audit trail** — distinct from §13 Revision History, which tracks edits to the *document*. This table tracks the state of the *defect*. The canonical flow is **New → Triaged → Assigned → Fixed → In Retest → Closed**, with side-exits **Rejected / Deferred / Duplicate**. Every status transition gets a row: the date, the owner at that moment, and a one-line note on why it moved. This table is **append-only** — never edit a past row. A status that jumps straight from New to Closed with no intermediate rows is a red flag that triage and verification were skipped. Delete this blockquote once filled.

| Date | Status | Owner | Notes |
|---|---|---|---|
| {{YYYY-MM-DD}} | New | {{Reporter}} | {{Incident logged from test run TR-N}} |
| {{YYYY-MM-DD}} | Triaged | {{Triage lead}} | {{Confirmed defect; severity Major, priority P1; assigned DEF-PROJECT-ID-001}} |
| {{YYYY-MM-DD}} | Assigned | {{Owner}} | {{Routed to owning developer}} |
| {{YYYY-MM-DD}} | Fixed | {{Developer}} | {{PR #482 merged into build 2.4.1}} |
| {{YYYY-MM-DD}} | In Retest | {{Tester}} | {{Retesting on build 2.4.1}} |
| {{YYYY-MM-DD}} | Closed | {{Tester}} | {{Verified fixed; regression suite green}} |

---

## 13. Revision History

> House-standard final section, mandatory. This records changes to **this document** (added evidence, corrected steps, reworded analysis) — distinct from §12 Status History, which records changes to the **defect's state**. Both are append-only audit trails serving different audiences: Revision History serves whoever maintains the report; Status History serves whoever tracks the defect. Delete this blockquote once filled.

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial report |

---

## Template usage notes

**Required sections** (don't omit):
- §1 Introduction (at least Purpose, Scope, and the seeded Definitions)
- §2 Identification (the triage header — the load-bearing section of a record)
- §3 Summary
- §4 Description (both Expected and Actual results are mandatory)
- §5 Steps to Reproduce (or an explicit statement that the incident is not reproducible, pointing to §6)
- §7 Severity and Priority
- §12 Status History
- §13 Revision History

**Optional sections** (include if relevant):
- §6 Evidence (omit only if there is genuinely nothing to attach — rare; for intermittent defects it is mandatory)
- §7.3 Anomaly classification (omit if you are not tracking IEEE 1044 anomaly trends)
- §8 Analysis (mark "under investigation" rather than omitting on an open report; required before Closed)
- §9 Resolution (filled once a disposition is decided)
- §10 Verification (filled at close-out; required to reach "Closed")
- §11 Open Questions (track elsewhere if you prefer)

**Identifier conventions** (for cross-document traceability):
- INC-N: test incidents (the report's own ID) — an event observed during testing that requires investigation
- DEF-N: defects — a confirmed flaw, traced from the incident that surfaced it
- REQ-N: requirement under test (from the SRS)
- TC-N: test case under test (from the Test Plan / test design)
- TR-N: test run / execution that produced the result

One report instance documents one incident and, if confirmed, the one defect it resolves to. These prefixes let the report trace back to exactly what was being tested.

**Tailoring**:
- One incident per report. Multiple unrelated incidents get separate reports; duplicates are linked, not merged.
- **Solo developer / small team:** this collapses to a few lines. You can keep §2 Identification, §4 Description (expected/actual), §5 Steps, and §12 Status History in a single issue-tracker ticket, and skip the formal sign-off block (you are reporter, fixer, and verifier — note that honestly rather than pretending three roles). Keep expected-vs-actual and a status trail even at the smallest scale; those two are what make a report usable later. Severity/priority can collapse to a single "how urgent" field when one person sets both.
- Fill the later sections (Analysis, Resolution, Verification) as the investigation proceeds — the report is a living record, not a one-shot form.
- Omit fields that do not apply rather than padding empty ones. A short, honest report beats a long, half-blank one.

**For regulated/safety-critical projects:** use the full ISO/IEC/IEEE 29119-3:2021 and IEEE 1044-2009, not this lightweight version. This template is suitable for solo/small-team projects, internal documentation, and early-stage products.
