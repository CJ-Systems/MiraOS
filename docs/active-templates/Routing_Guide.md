# Documentation Routing Guide

> Use this before creating or filing a MiraOS project document. The goal is low-friction capture first, then correct routing once enough context exists.

## Quick Decision

Ask: what kind of thing is this?

| If it is... | Use... |
|---|---|
| Important, but not ready to classify | Quick Capture |
| A decision we made that future-us may question | Architecture Decision Record |
| Intended behavior or a stable "must do" statement | Requirements Document |
| How a subsystem/module works | Software Design Description |
| Learning from articles, papers, docs, conversations, or outside systems | Research Note |
| A companion note for one standard or formal guide | Standard Note |
| A bounded technical experiment | Spike Report |
| A meaningful code change or agent handoff | Code Review Record |
| Current project truth | Status Report |
| A release/tag/build snapshot | Version Description Document |
| A vocabulary decision | Glossary |
| A proposed change to a controlled baseline | Change Request |
| Cross-topic navigation across docs/code/standards/questions | Topic Map |

## Capture First

When the right route is unclear:

1. Capture the thought quickly using `docs/active-templates/Quick_Capture.md`.
2. Preserve source, context, date, and why it mattered.
3. Leave it in a low-friction holding place.
4. Classify it later using this guide.
5. Promote it only when it becomes a real artifact.

Do not make the user manually file everything perfectly at capture time. MiraOS needs both classification and associative re-finding.

## Routes

### Quick Capture

Use when:

- A thought, source, observation, or question seems worth preserving.
- The correct destination is not obvious yet.
- Stopping to choose a formal artifact would interrupt flow.
- The content may later become an ADR, requirement, research note, topic map, spike, status report, or glossary entry.

Do not use for:

- Finished decisions; write an ADR.
- Source-grounded learning that is already coherent; write a Research Note or Standard Note.
- Stable project state; write a Status Report.
- Random noise that does not need to be recovered later.

Active template: `docs/active-templates/Quick_Capture.md`

### Architecture Decision Record

Use when:

- A decision has been made.
- Reasonable alternatives were rejected.
- The choice has consequences that are not obvious from code.
- Reversing the choice later would be costly.

Do not use for:

- Research summaries.
- Open questions.
- General thoughts that feel important.
- "We should think about..." notes.

Source: `docs/templates/02_Design/Architecture_Decision_Record.md`

### Requirements Document

Use when:

- MiraOS must do something.
- Behavior needs to be separated from implementation.
- Requirements need stable IDs for later design or tests.

Do not use for:

- Implementation design.
- Exploratory ideas that have not become intended behavior.
- Philosophy unless it constrains behavior.

Source: `docs/templates/01_Requirements/Software_Requirements_Specification.md`

### Software Design Description

Use when:

- A subsystem needs a design record.
- State, interfaces, data structures, lifecycle, coupling, or instrumentation need explanation.
- An agent or human should understand the module without reverse-engineering code.

Do not use for:

- One-off decisions better captured by ADRs.
- Open-ended research.
- Implementation notes obvious from code.

Source: `docs/templates/02_Design/Software_Design_Description.md`

### Research Note

Use when:

- The primary content is learning from a source.
- The note should separate what the source says from what Mira infers.
- No project decision has been made yet.

Do not use for:

- Formal standards; use Standard Note.
- Decisions; write an ADR after the decision exists.
- Unbounded personal reflection; use memory or journal space.

Active template: `docs/active-templates/Research_Note.md`

### Standard Note

Use when:

- The source is one IEEE, ISO, IEC, NIST, OWASP, SWEBOK, or regulatory standard/guide.
- A local PDF needs a markdown companion map.
- We need key clauses, concepts, definitions, and relevance without copying the standard.

Do not use for:

- Full-text conversion of copyrighted standards.
- General article summaries.
- Project decisions.

Active template: `docs/active-templates/Standard_Note.md`

### Topic Map

Use when:

- A subject crosses multiple docs, standards, ADRs, code areas, and open questions.
- The artifact should help navigation more than declare new truth.
- Associative re-finding matters.

Do not use for:

- A single source summary.
- A single decision.
- A single module design.

Active template: `docs/active-templates/Topic_Map.md`

### Spike Report

Use when:

- We run a bounded technical experiment.
- The goal is to answer a question, not ship a feature.
- We need approach, evidence, result, and recommendation.

Do not use for:

- Production design after the approach is chosen.
- Open-ended research without a bounded question.
- Full milestone retrospectives; use Lessons Learned.

Active template: `docs/active-templates/Spike_Report.md`

### Code Review Record

Use when:

- An agent makes a meaningful code change.
- Implementation context needs handoff to another reviewer.
- A human reviewer wants to study the change.
- The change touches architecture, persistence, memory, tools, safety, tests, or user-visible behavior.

Do not require for:

- Typo fixes.
- One-line config changes.
- Small documentation cleanup.
- Disposable experiments already covered by a Spike Report.

Active template: `docs/active-templates/Code_Review_Record.md`

### Status Report

Use when:

- The question is "where are we right now?"
- We need progress, blockers, decisions needed, and next actions.
- A point-in-time project snapshot would help future continuation.

Do not use for:

- Every casual update.
- Historical lessons; use Lessons Learned.
- Detailed project management ceremony before it is useful.

Source: `docs/templates/08_Management/Status_Report.md`

### Change Request

Use when:

- A controlled baseline exists.
- A proposed change needs evaluation before implementation.
- Impact analysis is needed across requirements, design, code, tests, docs, risk, or schedule.

Do not use for:

- Ordinary exploratory edits.
- Changes before a baseline exists.
- Direction decisions better captured by ADRs.

Source: `docs/templates/05_Configuration_Management/Change_Request.md`

### Version Description Document

Use when:

- We cut a release, tag, internal build, or distributable package.
- We need a frozen record of exactly what shipped.

Do not use for:

- Ongoing status.
- Planning a release.
- General changelog notes without a real version/snapshot.

Source: `docs/templates/05_Configuration_Management/Version_Description_Document.md`

### Glossary

Use when:

- A term appears across multiple documents.
- A word is used in a MiraOS-specific way.
- Two readers might reasonably interpret the term differently.

Do not use for:

- Ordinary English.
- Long essays about concepts.
- Copying definitions from standards.

Source: `docs/templates/00_Index/Glossary.md`

## Anti-Patterns

- Do not turn research into ADRs before a decision exists.
- Do not put important thoughts in `docs/adrs/` just because they feel important.
- Do not require a full formal template for every small edit.
- Do not use the full generated template catalog as the daily working system.
- Do not convert standards PDFs into full-text markdown unless there is a clear legal and practical reason.
