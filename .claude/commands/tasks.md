---
name: tasks
description: Break a feature plan into an ordered, verifiable task checklist ready for implementation.
arguments: true
allowed-tools:
  - Read
  - Write
  - Edit
model: haiku
effort: medium
---

Generate an ordered task breakdown from a feature plan.

Arguments: $ARGUMENTS (feature name matching an existing specs/features/<name>/ directory)

Phase: tasks (runs after /plan or directly after /specify for low-complexity features)

Prerequisite check:
1. Read `specs/features/$ARGUMENTS/spec.md` — confirm status is "Ready".
2. Read `specs/features/$ARGUMENTS/plan.md` if it exists.
3. Confirm no open spikes remain in plan.md. If spikes are incomplete, list them and stop.

Steps:
1. Fill in `specs/features/$ARGUMENTS/tasks.md`:
   - Pre-implementation checklist (verify all spec open questions resolved, contracts finalized)
   - Phased task list, ordered by dependency:
     - Phase 1: Foundation (data model, schema migrations, base types)
     - Phase 2: Core Logic (business logic, services, domain code)
     - Phase 3: Integration & Contracts (API handlers, event producers/consumers, glue)
     - Phase 4: Validation (run /validate against spec AC, update statuses)
   - Each task includes: description, acceptance (how to verify), which spec AC it satisfies, dependencies
2. Tasks must be atomic: one task = one verifiable unit of work.
3. Do not include tasks for things already done in the codebase.

Rules:
- Tasks are implementation steps, not re-statements of requirements.
- If a task is ambiguous, break it down further rather than leaving it vague.
- Every spec acceptance criterion must map to at least one task.

Output: path of created/updated tasks.md, count of tasks created, and which spec acceptance criteria are covered.
