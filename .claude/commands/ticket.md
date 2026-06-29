---
name: ticket
description: Convert a feature's tasks.md into Paperclip-compatible tickets with dependencies, model hints, and budget estimates.
arguments: true
allowed-tools:
  - Read
  - Write
model: haiku
effort: low
---

Convert a feature's tasks.md into Paperclip tickets.

Arguments: $ARGUMENTS (feature name matching an existing specs/features/<name>/ directory)

Steps:
1. Read `specs/features/$ARGUMENTS/spec.md` — extract feature name, complexity, and acceptance criteria.
2. Read `specs/features/$ARGUMENTS/tasks.md` — extract every task with its ID, description, acceptance, dependencies, and which spec AC it satisfies.
3. Read `specs/features/$ARGUMENTS/plan.md` if it exists — note any spikes that must complete before implementation.
4. For each task, produce a Paperclip ticket block:

```
---
ticket_id: <feature>-<T-XX>
title: <task description>
feature: <feature name>
phase: <Foundation | Core Logic | Integration | Validation>
model: <haiku | sonnet | opus>  # from .paperclip/budgets.md and CLAUDE.md model selection
depends_on: [<ticket_id>, ...]  # from tasks.md "Depends on" field
spec_ac: [<AC reference>]       # which acceptance criterion this satisfies
agent_role: implementer
context:
  - specs/features/<feature>/spec.md
  - specs/features/<feature>/plan.md
  - specs/features/<feature>/tasks.md
  - specs/features/<feature>/contracts/
approval_required: false        # set true for Phase 1 Foundation tasks on High complexity features
---
```

5. Add one final ticket for validation:
```
---
ticket_id: <feature>-validate
title: Validate all acceptance criteria for <feature>
feature: <feature name>
phase: Validation
model: sonnet
depends_on: [all implementation ticket IDs]
agent_role: validator
context:
  - specs/features/<feature>/spec.md
  - specs/features/<feature>/tasks.md
  - specs/features/<feature>/contracts/
approval_required: true
---
```

6. Write the output to `specs/features/$ARGUMENTS/paperclip-tickets.md`.

Model assignment per task:
- Tasks in Phase 1/2 with clear specs → haiku
- Tasks requiring judgment, integration, or pattern matching → sonnet
- Tasks touching cross-cutting concerns or requiring architectural decisions → opus

Output: path of created paperclip-tickets.md and total ticket count.
