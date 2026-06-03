# Code Review Record

> Use this for meaningful code changes, AI-assisted development handoffs, or changes worth studying. This is both a review record and a learning artifact.

## Review Header

| Field | Value |
|---|---|
| Review ID | CRR-YYYYMMDD-001 |
| Date | YYYY-MM-DD |
| Status | Draft |
| Work product | PR / commit range / file set / module |
| Version / Commit | exact hash, branch@commit, or snapshot |
| Risk level | Routine / Elevated / High |
| Author / Implementing agent |  |
| Reviewer |  |
| Recorder |  |
| Review decision | Accepted / Accepted with rework / Re-review required / Rejected |

## Reader Context

This record should help both experienced reviewers and newer programmers understand the change.

Use this section to say how the reader should approach the review. If the change touches high-risk areas such as core runtime, memory, permissions, agent orchestration, gateway/session behavior, persistence, or system integration, name that clearly and explain what concepts matter.

- Expected background:
- Concepts to understand before reviewing:
- Good first questions for a newer reader:
- Areas that require extra care:

## 1. What Changed

Summarize the change in plain engineering language.

- 

## 2. Why This Pattern Was Chosen

Explain the implementation strategy. Name the pattern, local convention, or tradeoff where possible.

- 

## 3. Alternatives Considered

List reasonable alternatives and why they were not chosen.

| Alternative | Why not chosen |
|---|---|
|  |  |

## 4. Files Worth Reading First

Give the reader an ordered path through the change.

| Order | File / section | Why read it |
|---|---|---|
| 1 |  |  |
| 2 |  |  |
| 3 |  |  |

## 5. Things To Trace In The Code

Concrete paths to follow while reading.

- Entry point:
- State flow:
- Data model:
- Error path:
- Test path:

## 6. Concepts Used

Terms, language concepts, framework concepts, tooling concepts, or design ideas this change demonstrates.

- 

## 7. Review Criteria

| Criterion | Result | Notes |
|---|---|---|
| Correctness | Pass / Concern / N/A |  |
| Maintainability | Pass / Concern / N/A |  |
| Testability | Pass / Concern / N/A |  |
| Error handling | Pass / Concern / N/A |  |
| Security / privacy | Pass / Concern / N/A |  |
| Fits project architecture | Pass / Concern / N/A |  |
| Learning value is clear | Pass / Concern / N/A |  |

## 8. Findings

| ID | Finding | Severity | Location | Owner | Disposition | Status |
|---|---|---|---|---|---|---|
| FND-1 |  | Blocker / Major / Minor / Info |  |  | Fix now / Fix later / Won't fix / Not a defect / Deferred | Open / Resolved / Verified |

## 9. Questions For The Reader

Prompts for critical reading, not homework for its own sake.

- Is this logic living in the right place?
- Is the naming honest?
- What happens when this fails?
- Is this easy to test?
- Does this duplicate a pattern elsewhere?
- Would this still make sense in six months?

## 10. Follow-Up Actions

| Action | Owner | Due / trigger | Status |
|---|---|---|---|
|  |  |  |  |

## 11. Final Decision

Decision:

Rationale:

Sign-off:
