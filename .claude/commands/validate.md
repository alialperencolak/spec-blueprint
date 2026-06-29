---
name: validate
description: Verify that every acceptance criterion in the feature spec is satisfied by the implementation.
arguments: true
allowed-tools:
  - Read
  - Bash
  - Edit
context: fork
effort: high
---

Verify that the implementation satisfies the feature spec.

Arguments: $ARGUMENTS (feature name matching an existing specs/features/<name>/ directory)

Phase: validate (runs after all tasks in tasks.md are checked off)

Steps:
1. Read `specs/features/$ARGUMENTS/spec.md` — extract every acceptance criterion.
2. For each acceptance criterion:
   a. Identify the relevant code, test, or observable behavior.
   b. Confirm it satisfies the Given/When/Then scenario.
   c. Mark it PASS, FAIL, or PARTIAL with a one-line explanation.
3. Check non-functional requirements: performance targets, security requirements, accessibility.
4. Check contracts in `specs/features/$ARGUMENTS/contracts/` match the implemented interface.
5. Check that `specs/constitution.md` quality gates are satisfied.
6. Review any "Discovered During Implementation" entries in tasks.md — confirm each was addressed in the spec.

Outcome:
- All PASS → update spec.md status to "Validated". Prompt to run /archive.
- Any FAIL or PARTIAL → list failures with the exact gap between spec and implementation. Do NOT mark as validated. Fix the implementation, then re-run /validate.

After validation:
- Update any ADRs whose validation plan milestone has been reached — fill in the "Outcome" section with what was learned.

Output: AC-by-AC results table, final status (Validated / Not Validated), and any ADR outcomes to record.
