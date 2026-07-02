---
name: validate
description: Verify that every acceptance criterion in the feature spec is satisfied by the implementation.
arguments: true
allowed-tools:
  - Read
  - Bash
  - Edit
context: fork
model: sonnet
effort: high
---

Verify that the implementation satisfies the feature spec.

Arguments: $ARGUMENTS (feature name matching an existing specs/features/<name>/ directory)

Phase: validate (runs after all tasks in tasks.md are checked off)

## Delegate or validate directly

If `.paperclip/agent-keys.env` exists, **delegate validation to the `validator` agent** (below) instead of checking the AC yourself — the same reasoning as `/implement`: doing it yourself and then notifying `validator` afterward just logs a decision it never made. If the file doesn't exist, fall back to the **Direct Validation** steps further down.

### Delegate to validator

a. Send an **actionable** handoff — ask for the validation to be done, not a pre-computed verdict:
   ```
   source .paperclip/agent-keys.env && npx paperclipai agent-prompt validator "$PAPERCLIP_VALIDATOR_KEY" \
     --title "Validate <feature-name>" \
     "Validate specs/features/<feature-name>/spec.md against its implementation. For every acceptance criterion, identify the relevant code/test/behavior and mark PASS, FAIL, or PARTIAL with a one-line explanation. Check non-functional requirements, check contracts/ match the implemented interface, check specs/constitution.md quality gates are satisfied, and review any 'Discovered During Implementation' entries in tasks.md. If all PASS, update spec.md status to Validated. If any FAIL or PARTIAL, do not mark Validated — list the exact gap instead." \
     --json
   ```
   Capture the created issue's `id` from the JSON response.

b. Poll `npx paperclipai issue get <issueId> --json` for its `status`, roughly every 10 seconds. Stop polling once status is `done`, `blocked`, `in_review`, or `cancelled`.

c. **Independently verify — never trust the agent's comment alone:**
   - Read the AC-by-AC results in its comment against `spec.md` — every acceptance criterion must actually be addressed, not skipped.
   - Run the project's test suite (`Bash`) yourself and cross-check its PASS/FAIL claims.
   - Confirm `spec.md` status was actually changed to "Validated" if and only if the agent reported all-PASS.

d. If status is `blocked`, or verification surfaces a mismatch (agent claims PASS but a test actually fails, or an AC was silently skipped): **stop** and report the discrepancy. Do not mark the feature validated yourself.

e. On confirmed success, report: AC-by-AC results table (as validated), final status (Validated / Not Validated), any ADR outcomes to record.

### Direct Validation (fallback — only when `.paperclip/agent-keys.env` doesn't exist)

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

After validation (either path):
- Update any ADRs whose validation plan milestone has been reached — fill in the "Outcome" section with what was learned.

Output: AC-by-AC results table, final status (Validated / Not Validated), and any ADR outcomes to record.
