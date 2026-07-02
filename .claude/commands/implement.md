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

## Pick the task

1. Read `specs/features/$ARGUMENTS/spec.md` — find the AC the task satisfies (Given/When/Then).
2. Read `specs/features/$ARGUMENTS/tasks.md` — use the given task ID, or the first unchecked `[ ]` task if none was given. Confirm its dependencies are already `[x]`.
3. Read relevant contracts in `specs/features/$ARGUMENTS/contracts/` before touching any interface.

## Delegate or implement directly

If `.paperclip/agent-keys.env` exists, **delegate the task to the `developer` agent** (below) instead of writing the code yourself — Paperclip's local instance runs a real Claude adapter capable of autonomous TDD work, and doing the work yourself would just duplicate/bypass it. If the file doesn't exist, fall back to the **Direct TDD Cycle** further down.

### Delegate to developer

a. Send an **actionable** handoff — describe the task to be done, never a task already marked complete (a pre-completed description gives the agent nothing to do and it will just close the issue):
   ```
   source .paperclip/agent-keys.env && npx paperclipai agent-prompt developer "$PAPERCLIP_DEVELOPER_KEY" \
     --title "<feature-name> <task-id>: <task description>" \
     "Implement task <task-id> from specs/features/<feature-name>/tasks.md using TDD (Red-Green-Refactor), per .claude/commands/implement.md and .claude/rules/spec-workflow.md. <task description and the spec AC it satisfies>. Write the failing test first, confirm it fails, implement the minimum code, confirm it passes, then mark <task-id> [x] in tasks.md with the test file noted." \
     --json
   ```
   Capture the created issue's `id` from the JSON response.

b. Poll `npx paperclipai issue get <issueId> --json` for its `status`, roughly every 10 seconds. Stop polling once status is `done`, `blocked`, `in_review`, or `cancelled`.

c. **Independently verify — never trust the agent's comment alone:**
   - Run the project's test suite (`Bash`) and confirm the relevant test(s) actually pass.
   - Confirm the task is actually marked `[x]` in `tasks.md` with a test file noted.
   - Read the new/changed test file(s) and confirm they genuinely exercise the task's spec AC (not a trivial/no-op test).

d. If status is `blocked`, or verification fails (tests don't pass, task not marked, or the test doesn't cover the AC): **stop** and report the discrepancy to the user. Do not mark the task done yourself, do not proceed to the next task, do not silently "fix" the agent's work — that defeats the point of delegating.

e. If status is `in_review`: report what's pending and who owns the next step. Do not proceed automatically.

f. On confirmed success, report: task ID, agent, test file, spec AC covered, next task ID.

### Direct TDD Cycle (fallback — only when `.paperclip/agent-keys.env` doesn't exist)

For each task, follow Red → Green → Refactor strictly in order.

**Red — write the failing test first:**
1. Translate the task's AC (Given/When/Then) into a test case using the project's test framework.
   - Given → test setup / preconditions
   - When → the action under test
   - Then → the assertion
2. Run the test: `Bash` the test runner against only this new test.
3. Confirm it **fails** with an assertion error (not a syntax/import error). If it passes immediately, the test is wrong — fix it before proceeding.

**Green — minimum implementation:**
4. Write the smallest code that makes the test pass. No extra logic.
5. Run the test again. Confirm it **passes**.

**Refactor — clean without breaking:**
6. If the code is messy, refactor it. Re-run the test after each change.
7. Test must stay green throughout refactor.

**Close the task:**
8. Mark the task `[x]` in `tasks.md`. Add inline note: which test file covers it.
9. If implementation reveals a contradiction with the spec, STOP. Document in the "Discovered During Implementation" table in `tasks.md`, update `spec.md`, then continue.
10. Report: task ID, test file created/updated, spec AC covered, next task ID.

## Rules
- A task is NOT done if no passing test exists for it — whether implemented directly or delegated.
- Never delete or skip a test to make a task pass — fix the implementation.
- One task per turn, delegated or direct. Never batch tasks silently.
- Never modify `spec.md` or `plan.md` to match broken implementation.
- If a task needs an architectural decision not in an ADR, pause and run `/adr` first.
- When delegating, always independently verify — a closed issue and a nice comment are not proof of working code.

## After all tasks complete
Run `/validate` — the validation phase reruns all tests and checks every spec AC end-to-end.
