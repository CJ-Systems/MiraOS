# Architecture Decision Record Template

> **Template purpose:** Lightweight Architecture Decision Record (ADR) structure following Michael Nygard's ADR pattern. Use this template to capture a single architecturally-significant decision. Replace `{{placeholder}}` content with decision-specific text. Section guidance (in blockquotes) can be deleted once the section is written.
>
> **When to use:** When you make a choice that will need explaining later, would be costly to reverse, rules out alternatives a reasonable person might pick, or has consequences that aren't obvious from the decision alone. One ADR captures one decision. Trivial choices (naming a variable, picking a field order) do not get an ADR.
>
> **Companion standard:** Michael Nygard's Architecture Decision Record pattern (informed by ISO/IEC/IEEE 42010:2022). There is no formal IEEE standard for ADRs themselves; ISO/IEC/IEEE 42010:2022 (architecture description) and ISO/IEC/IEEE 42030:2019 (architecture evaluation) are the adjacent standards that touch how decisions relate to architecture.
>
> **Status of this template:** Lightweight pattern suited to solo/small-team use. Faithful to the Nygard shape (Context → Decision → Consequences) with Alternatives and Related-decisions sections added for traceability. For large or regulated systems, pair ADRs with a fuller architecture description per ISO/IEC/IEEE 42010.

---

# ADR-{{NNNN}}: {{Short Decision Title}}

> The title states the decision, not the topic. Prefer "Use PostgreSQL for the primary store" over "Database choice." Number `{{NNNN}}` is the next sequential 4-digit value; numbers are never reused or renumbered.

| Field | Value |
|---|---|
| Status | {{Proposed \| Accepted \| Deprecated \| Superseded}} |
| Date | {{YYYY-MM-DD}} |
| Deciders | {{Who made / signed off on this decision}} |
| Supersedes | {{ADR-NNNN, or — if none}} |
| Superseded-by | {{ADR-NNNN, or — if none}} |

---

## 1. Context

> This is the heart of an ADR and the part future readers value most. Describe the **forces** at play — the problem, the constraints, the requirements, the technical and organizational pressures — that make a decision necessary. Write it **neutrally and without the decision**: a reader should be able to reach the section's end and not yet know which way you went. State facts and tensions, not the conclusion. Capture what was true *at the time of writing*; this is a historical record, so do not edit it later to reflect what you learned afterward. If the decision supersedes an earlier one, name the earlier ADR here and explain what changed.

{{Describe the problem and the forces driving it. What needs deciding, and why now? List the relevant constraints, requirements, and pressures — functional, technical, operational, and organizational. Quantify where you can ("~10,000 concurrent users," "must respond within 200 ms"). Name any decision this one supersedes and what changed. End before stating the choice itself.}}

---

## 2. Decision

> State the choice **plainly, in active voice, as something the team is committing to**: "We will...". One decision per ADR. Be specific enough that someone could act on it — name the actual technology, pattern, version, or rule, not a vague direction. Keep this section short; the *why* lives in Context and the *so-what* lives in Consequences. If the decision has a few concrete parts, a short numbered list is fine.

We will {{state the decision in one or two sentences, active voice}}.

{{Optional: a short numbered list of the concrete parts of the decision, if it has more than one.}}

1. {{Decision part one}}
2. {{Decision part two}}

---

## 3. Consequences

> Every decision has results — good, bad, and neutral. This section makes them visible so nobody is surprised later. Split them three ways so the trade-offs are honest: **Positive** (what gets better), **Negative** (what gets worse or harder, the price you're paying), and **Neutral / Trade-offs** (things that simply change, or two-edged effects). A consequence is *any* outcome of the decision — new work created, options foreclosed, risks introduced, capabilities gained. Where a negative consequence has a mitigation, name it. Listing the negatives is not a sign of a bad decision; an ADR with no negatives is usually one that hasn't been thought through.

### 3.1 Positive

- {{Good outcome of the decision}}
- {{Another benefit}}

### 3.2 Negative

- {{Cost, drawback, or new burden}} — {{mitigation, if any}}
- {{Risk introduced}} — {{mitigation, if any}}

### 3.3 Neutral / Trade-offs

- {{Something that simply changes, or a two-edged effect}}
- {{An option this decision forecloses or defers}}

---

## 4. Alternatives Considered

> Record the other options that were genuinely on the table and **why each was not chosen**. This is what stops a future reader from re-litigating a settled decision: "Why didn't they just use X?" — because X is right here, with the reason it lost. Be fair to the alternatives; describe their real strengths, not strawmen. The strongest rejected option (the "close second") deserves the most attention, because that's the one someone is most likely to second-guess. If an alternative was rejected for a reason that may later stop being true, say so — that tells a future reader when this ADR is worth revisiting.

### 4.1 {{Alternative 1 name}}

- **What it is:** {{brief description}}
- **Why not chosen:** {{the specific reason it lost — and, if relevant, what would have to change for it to win}}

### 4.2 {{Alternative 2 name}}

- **What it is:** {{brief description}}
- **Why not chosen:** {{reason}}

### 4.3 Do nothing / status quo

> Almost always worth recording: what happens if no decision is made? Sometimes "do nothing" is the right answer; when it isn't, naming it shows the decision was necessary.

- **What it is:** {{the current state if no change is made}}
- **Why not chosen:** {{why the status quo was inadequate}}

---

## 5. Related Decisions and References

> Wire this ADR into the wider record so a reader can navigate outward. **Related decisions** are other ADRs in this project — ones this depends on, complements, supersedes, or is superseded by. **References** are external or internal sources that informed the decision: specs, tool/library docs, standards, benchmarks, articles. Keeping these split (project decisions vs. outside sources) matches how readers look things up.

**Related decisions:**

- ADR-{{NNNN}} — {{how it relates: depends on / complements / superseded by}}
- {{path/to/spec-or-doc.md}} — {{relationship}}

**References:**

- {{External source — tool docs, standard, paper, benchmark, with a link}}
- {{Internal source — e.g., `docs/benchmarks/comparison.md`}}

---

## Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | {{YYYY-MM-DD}} | {{Author}} | Initial draft |

---

## Template usage notes

**Required sections** (don't omit):

- Title with `ADR-{{NNNN}}` number
- Metadata table (Status, Date, Deciders at minimum)
- §1 Context
- §2 Decision
- §3 Consequences
- Revision History

**Optional sections** (include when relevant):

- §4 Alternatives Considered — strongly recommended whenever the decision ruled out options a reasonable person might pick. Omit only for decisions where there was genuinely no alternative.
- §5 Related Decisions and References — omit if the ADR truly stands alone, but most don't.
- The `Supersedes` / `Superseded-by` metadata rows — leave as `—` until they apply.

**Tailoring:**

- **Numbering and storage.** Store ADRs together in one directory (e.g., `docs/adrs/`). Filename pattern `NNNN-kebab-case-title.md` (e.g., `0007-event-sourced-orders.md`). Numbers are 4-digit zero-padded for sortability, assigned sequentially, and **never reused or renumbered** — even after an ADR is superseded. The history is the point.
- **Lifecycle.** An ADR moves through `Proposed → Accepted`, and from `Accepted` either to `Deprecated` (no longer applies, no replacement exists yet — avoid leaving an ADR here long-term) or `Superseded` (replaced by a newer ADR). When superseding: write the new ADR with the next number, name the old one in the new ADR's §1 Context and explain what changed, and update the old ADR's `Status` to `Superseded` and its `Superseded-by` row to point at the new number. **Leave the old ADR's body otherwise intact** — the reasoning at the time of writing is part of the record.
- **One decision per ADR.** If you find two decisions in one draft, split it. Cross-link the pair via §5.
- **Keep a project index.** A `README.md` listing ADRs by number, title, status, and a one-line hook makes the decision history navigable as it grows.

A full architecture-evaluation process (e.g., ISO/IEC/IEEE 42030:2019, or a structured method such as ATAM) is warranted when a decision affects multiple quality attributes with competing stakeholders, carries high reversal cost across the whole system, or must be defended to auditors or external reviewers. For everyday architecturally-significant choices on a solo or small-team project, this lightweight ADR is enough.
