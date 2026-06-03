# MiraOS Engineering Document Templates

A complete, SWEBOK-organized set of **56 lightweight, reusable document templates** for software-engineering projects — each derived from a companion ISO/IEC/IEEE (or widely-used community / regulatory) standard, and written for solo developers and small teams who want the *structure* and *discipline* of formal practice without the weight of the full normative standards.

The templates are organized by **SWEBOK Knowledge Area** (the folders `01`–`11`, the way the Software Engineering Body of Knowledge maps the field), with two extra areas — `12_Security_and_Privacy` and `13_AI_Governance` — for cross-cutting modern concerns that SWEBOK V3 underserves and SWEBOK V4 has begun to formalize.

## House style

Every template follows the same shape:

- A front-matter blockquote stating **purpose**, **when to use**, the **companion standard**, and the template's **status**.
- A metadata table (document ID, version, date, status, standard, owner) including a **sign-off block** (Prepared by / Reviewed by / Approved by) for formal review chains. *(ADRs use their native Deciders row instead.)*
- Numbered sections, each opening with plain-English guidance written for someone new to formal software-engineering practice.
- `{{double-brace}}` placeholders to replace.
- A closing **Template usage notes** section (required vs. optional sections, tailoring advice including how the document collapses for a solo developer, and when to reach for the full standard instead).

## Maturity tiers

Each template carries an indicative tier — *why it exists yet*, not how finished it is (all are usable now):

- **now** — supports practice an active solo/small project does today.
- **planned** — expected in the near term as the project matures.
- **eventual** — scaffolding for product / enterprise / regulatory needs that arrive with real users (security, privacy, AI governance, operations, certification, retirement). Present so the set is complete, not because the work is due.

## The set — by Knowledge Area

### 00_Index
| Template | Companion standard | Tier |
|---|---|---|
| `Glossary.md` | ISO/IEC/IEEE 24765 (SEVOCAB) style | planned |

### 01_Requirements
| Template | Companion standard | Tier |
|---|---|---|
| `Concept_of_Operations.md` | ISO/IEC/IEEE 29148 / IEEE 1362 | planned |
| `Stakeholder_Requirements_Specification.md` | ISO/IEC/IEEE 29148:2018 | planned |
| `System_Requirements_Specification.md` | ISO/IEC/IEEE 29148:2018 | planned |
| `Software_Requirements_Specification.md` | ISO/IEC/IEEE 29148:2018 | now |
| `Interface_Requirements_Specification.md` | ISO/IEC/IEEE 29148:2018 | planned |
| `Requirements_Management_Plan.md` | ISO/IEC/IEEE 29148 + 12207 | planned |
| `Requirements_Traceability_Matrix.md` | ISO/IEC/IEEE 29148 (traceability) | planned |

### 02_Design
| Template | Companion standard | Tier |
|---|---|---|
| `Software_Architecture_Description.md` | ISO/IEC/IEEE 42010:2022 | planned |
| `Architecture_Evaluation_Report.md` | ISO/IEC/IEEE 42030:2019 | planned |
| `Architecture_Decision_Record.md` | Nygard pattern (informed by 42010) | now |
| `Software_Design_Description.md` | IEEE 1016-2009 | now |
| `Data_Design_Description.md` | IEEE 1016-2009 + ISO/IEC 25012 | planned |
| `Interface_Design_Description.md` | IEEE 1016-2009 (interface viewpoint) | planned |

### 03_Construction
| Template | Companion standard | Tier |
|---|---|---|
| `Build_Plan.md` | ISO/IEC/IEEE 12207 + CI practice | now |
| `Code_Review_Record.md` | IEEE 1028-2008 | now |
| `Coding_Standard.md` | SWEBOK Construction + ISO/IEC 5055 | now |
| `Software_Construction_Plan.md` | ISO/IEC/IEEE 12207 (construction) | now |

### 04_Testing_and_VV
| Template | Companion standard | Tier |
|---|---|---|
| `Master_Test_Plan.md` | ISO/IEC/IEEE 29119-3 | planned |
| `Verification_and_Validation_Plan.md` | IEEE 1012-2016 | planned |
| `Test_Case_Specification.md` | ISO/IEC/IEEE 29119-3 | planned |
| `Test_Procedure_Specification.md` | ISO/IEC/IEEE 29119-3 | planned |
| `Test_Log.md` | ISO/IEC/IEEE 29119-3 | planned |
| `Test_Incident_Defect_Report.md` | ISO/IEC/IEEE 29119-3 + IEEE 1044 | planned |
| `Test_Summary_Report.md` | ISO/IEC/IEEE 29119-3 | planned |

### 05_Configuration_Management
| Template | Companion standard | Tier |
|---|---|---|
| `Software_Configuration_Management_Plan.md` | IEEE 828-2012 | now |
| `Change_Request.md` | IEEE 828-2012 + 12207 | now |
| `Configuration_Status_Accounting_Report.md` | IEEE 828-2012 | planned |
| `Version_Description_Document.md` | IEEE 828-2012 | now |

### 06_Quality
| Template | Companion standard | Tier |
|---|---|---|
| `Quality_Requirements_Specification.md` | ISO/IEC 25010:2023 (SQuaRE) | planned |
| `Software_Quality_Assurance_Plan.md` | IEEE 730-2014 | planned |
| `Review_and_Inspection_Plan.md` | IEEE 1028-2008 | planned |
| `Audit_Report.md` | IEEE 1028-2008 + 828 | planned |

### 07_Maintenance
| Template | Companion standard | Tier |
|---|---|---|
| `Software_Maintenance_Plan.md` | ISO/IEC/IEEE 14764:2022 | planned |
| `Problem_Report.md` | IEEE 1044-2009 + 14764 | planned |
| `Migration_Plan.md` | ISO/IEC/IEEE 14764:2022 | eventual |

### 08_Management
| Template | Companion standard | Tier |
|---|---|---|
| `Software_Project_Management_Plan.md` | ISO/IEC/IEEE 16326:2019 | eventual |
| `Risk_Management_Plan.md` | ISO/IEC/IEEE 16085 + NIST AI RMF | planned |
| `Measurement_Plan.md` | ISO/IEC/IEEE 15939 + ISO/IEC 25023 | planned |
| `Status_Report.md` | ISO/IEC/IEEE 16326:2019 | planned |

### 09_Process
| Template | Companion standard | Tier |
|---|---|---|
| `Software_Development_Plan.md` | ISO/IEC/IEEE 15288 / 12207 / 24748 | now |
| `Process_Improvement_Plan.md` | ISO/IEC 33001/33002 (ex-SPICE), CMMI | planned |

### 10_User_Documentation_and_Operations
| Template | Companion standard | Tier |
|---|---|---|
| `User_Documentation_Plan.md` | ISO/IEC/IEEE 26515:2018 | eventual |
| `Documentation_Management_Plan.md` | ISO/IEC/IEEE 26511 / 26512 / 26513 | eventual |
| `Installation_Guide.md` | ISO/IEC/IEEE 26511 / 26514 | eventual |
| `Operations_Manual.md` | ISO/IEC/IEEE 26511 + 12207 (operation) | eventual |
| `User_Manual.md` | ISO/IEC/IEEE 26514 / 26515 | eventual |

### 11_Economics_and_Closeout
| Template | Companion standard | Tier |
|---|---|---|
| `Business_Case.md` | SWEBOK Economics; ISO/IEC/IEEE 16326 | planned |
| `Software_Cost_Estimate.md` | SWEBOK Economics; COCOMO II, ISO/IEC 20926 | planned |
| `Lessons_Learned_Report.md` | SWEBOK; retrospective practice | now |

### 12_Security_and_Privacy
| Template | Companion standard | Tier |
|---|---|---|
| `Security_Plan.md` | ISO/IEC 27001 / 27002 / 27034, NIST SP 800-53 | eventual |
| `Threat_Model.md` | ISO/IEC 27034, OWASP Top 10, OWASP AI Guide | eventual |
| `Privacy_Impact_Assessment.md` | GDPR (DPIA), CCPA / CPRA | eventual |

### 13_AI_Governance
| Template | Companion standard | Tier |
|---|---|---|
| `AI_System_Description.md` | ISO/IEC 23053 / 22989, TR 24028 | planned |
| `AI_Impact_Assessment.md` | ISO/IEC 23894, NIST AI RMF, EU & Colorado AI Acts | eventual |
| `AI_Management_System.md` | ISO/IEC 42001:2023 | eventual |

## Lifecycle reading order

The KA folders are a *reference* organization, not a workflow. If you're starting a project and want "what do I write, roughly in what order," read across the areas like this:

1. **Frame it** — `Business_Case` → `Concept_of_Operations`
2. **Specify it** — `Stakeholder_Requirements` → `System_Requirements` → `Software_Requirements` → `Interface_Requirements`; manage with `Requirements_Management_Plan` + `Requirements_Traceability_Matrix`
3. **Plan it** — `Software_Development_Plan`, `Software_Project_Management_Plan`, `Risk_Management_Plan`, `Software_Configuration_Management_Plan`, `Software_Quality_Assurance_Plan`, `Measurement_Plan`
4. **Design it** — `Software_Architecture_Description` (+ `ADR`s), `Software_Design_Description`, `Data_Design_Description`, `Interface_Design_Description`; judge it with `Architecture_Evaluation_Report`; set targets with `Quality_Requirements_Specification`
5. **Build it** — `Software_Construction_Plan`, `Coding_Standard`, `Build_Plan`, `Code_Review_Record`
6. **Verify it** — `Master_Test_Plan` + `V&V_Plan` → `Test_Case` / `Test_Procedure` / `Test_Log` / `Test_Incident_Defect_Report` / `Test_Summary_Report`; `Review_and_Inspection_Plan`, `Audit_Report`
7. **Govern AI & secure it** — `AI_System_Description`, `AI_Impact_Assessment`, `AI_Management_System`; `Security_Plan`, `Threat_Model`, `Privacy_Impact_Assessment`
8. **Ship & run it** — `Version_Description_Document`, `Installation_Guide`, `User_Manual`, `Operations_Manual`, `User_Documentation_Plan`, `Documentation_Management_Plan`
9. **Keep it alive** — `Change_Request`, `Configuration_Status_Accounting_Report`, `Software_Maintenance_Plan`, `Problem_Report`, `Migration_Plan`, `Process_Improvement_Plan`, `Status_Report`
10. **Close it out** — `Software_Cost_Estimate` (revisit actuals), `Lessons_Learned_Report`

Throughout, `Glossary` fixes shared vocabulary.

## How to use a template

1. Copy the template to your target location (e.g. `docs/srs.md`, `docs/adrs/NNNN-<title>.md`).
2. Replace every `{{placeholder}}` with project-specific content.
3. Read each section's guidance blockquote, then delete the guidance once the section is written.
4. Follow the **Template usage notes** at the bottom of each template to decide which sections are required, which are optional, and when to step up to the full standard.

Documents reference each other through ID prefixes — a need `StR-3` (Stakeholder Requirements) → `SyR-F-7` (System Requirements) → realized by an `ADR` → evaluated by `EC-2` (Architecture Evaluation) → verified by `TC-12` (Test Case), traced in the `Requirements_Traceability_Matrix`. Keeping IDs stable is what makes traceability across the set work.

## On copyright

These templates are *inspired by* their companion standards but do **not** reproduce normative text. Field names, section ordering, and structural conventions are paraphrased or derived independently from publicly available sources. Where a standard sits behind a paywall (most ISO documents), the template is a lightweight skeleton built from public summaries and is marked as such — verify it against the authoritative text before relying on it for regulated, safety-critical, contractual, or enterprise contexts.

Standards content remains the property of its publishers (ISO, IEC, IEEE, NIST, OWASP, and the relevant regulators). The regulatory templates (AI Impact Assessment, Privacy Impact Assessment, Security Plan) are engineering scaffolding, **not legal advice** — confirm obligations for your jurisdiction with qualified counsel. These templates are released under the repository's license; the *standards and regulations* they reference are not.

## Status

`Software_Requirements_Specification` and `Software_Design_Description` were extracted from documents already in active use, so their structure is battle-tested. The rest are derived from public sources and standard outlines; the IEEE-accessible, NIST, and OWASP-based ones sit closer to their source than the paywalled-ISO ones. Treat any ISO-derived template as a faithful skeleton pending verification against the full standard. Together the 56 templates span the full SWEBOK knowledge-area map plus security, privacy, and AI governance.
