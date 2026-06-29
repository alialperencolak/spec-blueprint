---
name: adr
description: Capture an architecture decision as a testable hypothesis with a validation plan.
arguments: true
allowed-tools:
  - Read
  - Write
  - Edit
model: opus
effort: medium
---

Create an Architecture Decision Record.

Arguments: $ARGUMENTS (short decision title, e.g. "use postgres for primary storage")

Phase: any (ADRs can be created during explore, specify, plan, or implement)

Steps:
1. Count existing ADRs in `specs/architecture/decisions/` and assign the next number (zero-padded to 4 digits).
2. Create `specs/architecture/decisions/ADR-<number>-<kebab-title>.md` from the template at `specs/architecture/decisions/ADR-0000-template.md`.
3. Fill in:
   - Context: the situation forcing a decision, constraints, quality attributes at stake — no solution bias
   - Decision drivers: specific measurable requirements driving the choice
   - Options considered: at least 2 alternatives with pros/cons
   - Decision: chosen option with one sentence linking back to drivers
   - Key consequences: positive outcomes, trade-offs accepted, downstream decisions needed
   - Validation plan: how and when we'll know if this was correct
4. Leave "Outcome" blank — it is filled in after real-world feedback.
5. Add a row to the Decision Index table in `specs/architecture/overview.md`.

Rules:
- Status starts as "Proposed". Change to "Accepted" once the team agrees, "Deprecated" if superseded.
- The "Outcome" section is the most important part — schedule a reminder to fill it in after the next relevant milestone.
- If this decision conflicts with `specs/constitution.md`, flag it before creating the ADR.

Output: path of the created ADR file and the updated overview.md decision index row.
