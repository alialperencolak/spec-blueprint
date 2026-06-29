---
name: implement
description: Implement tasks from a feature's tasks.md one at a time, staying strictly inside the spec.
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

Implement tasks from a feature's tasks.md, one at a time.

Arguments: $ARGUMENTS (feature name, and optionally a task ID e.g. "user-auth T-03")

Phase: implement (runs after /tasks)

Steps:
1. Read `specs/features/$ARGUMENTS/spec.md` to keep acceptance criteria in view.
2. Read `specs/features/$ARGUMENTS/tasks.md` to find the next unchecked task (or the specific task given in $ARGUMENTS).
3. Read relevant contracts in `specs/features/$ARGUMENTS/contracts/` before implementing any interface.
4. Implement the task:
   - Write the minimum code to satisfy the task's acceptance criteria.
   - Match existing code style, patterns, and abstractions in the codebase.
   - Do not implement adjacent tasks or "while I'm here" improvements.
5. After implementing, verify the task's acceptance criterion is met.
6. Mark the task `[x]` in tasks.md.
7. If implementation reveals a contradiction with the spec, STOP. Document the discovery in the "Discovered During Implementation" table in tasks.md, update spec.md, then continue.
8. After all tasks in a phase are complete, report phase summary before proceeding.

Rules:
- One task per implementation turn. Do not batch tasks silently.
- Never modify spec.md or plan.md to match broken implementation — fix the implementation.
- If a task requires an architectural decision not covered by an existing ADR, pause and run /adr first.

Output after each task: task ID completed, files changed, which spec AC it satisfies, and the next task ID to implement.
