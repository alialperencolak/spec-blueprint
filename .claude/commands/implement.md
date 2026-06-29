---
name: implement
description: Implement tasks from a feature's tasks.md one at a time using TDD — Red (failing test) → Green (pass) → Refactor.
arguments: true
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
context: fork
model: sonnet
effort: high
---

Implement tasks from a feature's tasks.md using Test-Driven Development.

Arguments: $ARGUMENTS (feature name, and optionally a task ID e.g. "user-auth T-03")

Phase: implement (runs after /tasks)

## Per-task TDD cycle

For each task, follow Red → Green → Refactor strictly in order.

**Before writing any code:**
1. Read `specs/features/$ARGUMENTS/spec.md` — find the AC this task satisfies (Given/When/Then).
2. Read `specs/features/$ARGUMENTS/tasks.md` — confirm the task ID and its dependencies are done.
3. Read relevant contracts in `specs/features/$ARGUMENTS/contracts/` before touching any interface.

**Red — write the failing test first:**
4. Translate the task's AC (Given/When/Then) into a test case using the project's test framework.
   - Given → test setup / preconditions
   - When → the action under test
   - Then → the assertion
5. Run the test: `Bash` the test runner against only this new test.
6. Confirm it **fails** with an assertion error (not a syntax/import error). If it passes immediately, the test is wrong — fix it before proceeding.

**Green — minimum implementation:**
7. Write the smallest code that makes the test pass. No extra logic.
8. Run the test again. Confirm it **passes**.

**Refactor — clean without breaking:**
9. If the code is messy, refactor it. Re-run the test after each change.
10. Test must stay green throughout refactor.

**Close the task:**
11. Mark the task `[x]` in `tasks.md`. Add inline note: which test file covers it.
12. If implementation reveals a contradiction with the spec, STOP. Document in the "Discovered During Implementation" table in `tasks.md`, update `spec.md`, then continue.
13. Report: task ID, test file created/updated, spec AC covered, next task ID.

## Rules
- A task is NOT done if no passing test exists for it.
- Never delete or skip a test to make a task pass — fix the implementation.
- One task per turn. Never batch tasks silently.
- Never modify `spec.md` or `plan.md` to match broken implementation.
- If a task needs an architectural decision not in an ADR, pause and run `/adr` first.

## After all tasks complete
Run `/validate` — the validation phase reruns all tests and checks every spec AC end-to-end.
