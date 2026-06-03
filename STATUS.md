# MiraOS Status

Last updated: 2026-06-02

MiraOS is in its public-documentation setup phase: turning private working
material into a clean public repository. The focus right now is **legibility
from the outside** — making the existing project work understandable to a
newcomer — not implementation packaging.

For the project thesis and framing, start with `README.md`. This file is a
point-in-time snapshot.

## Templates

The active work centers on a documentation template system, kept in two layers:

- **Source catalog** (`docs/templates/`) — the full generated template pack,
  preserved intact as a source/reference catalog.
- **Active set** (`docs/active-templates/`) — the smaller, MiraOS-specific set
  adapted for actual use.

**Ready / active now:**

- Code Review Record

**Drafted / under review:**

- Research Note
- Routing Guide
- Spike Report
- Standard Note
- Topic Map

The Code Review Record is intentionally structured because it serves two jobs:
agent handoff and audit trail, and a learning artifact for people new to
programming, new to AI-assisted development, or studying a change worth reviewing.

**Still being adapted:**

- Glossary
- Software Requirements Specification
- Architecture Decision Record
- Software Design Description
- Status Report
- Change Request
- Version Description Document

## Open Work

Active, near-term:

- Decide which parts of `docs/` are ready to commit publicly.
- Review and settle the drafted active templates listed above.
- Refine and maintain `project-map.md` as the public orientation layer.
- Rewrite selected private architecture notes into public docs.

## Not Ready Yet

Explicitly out of scope for now, so nothing here is implied or promised:

- packaged install instructions
- a stable public runtime
- user-facing demos
- complete public architecture docs
- finalized requirements
- a threat model
- AI governance docs

## Boundary

Private MiraOS working material stays separate from this public repository.
Public docs are rewritten from the ideas, not copied raw from the private archive.

Copyrighted reference material (IEEE/ISO standards PDFs) is kept locally for
reference only and is fenced out of the repository via `.gitignore`.
