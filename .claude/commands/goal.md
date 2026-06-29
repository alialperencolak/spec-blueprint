---
name: goal
description: Convert a feature spec into a Paperclip goal definition with done conditions, agent assignments, and budget envelope.
arguments: true
allowed-tools:
  - Read
  - Write
model: haiku
effort: low
---

Convert a feature spec into a Paperclip goal definition.

Arguments: $ARGUMENTS (feature name matching an existing specs/features/<name>/ directory)

Steps:
1. Read `specs/features/$ARGUMENTS/spec.md` — extract problem statement, actors, requirements, acceptance criteria, and complexity.
2. Read `.paperclip/budgets.md` — determine budget envelope for this complexity level.
3. Read `.paperclip/agent-roles.md` — determine which agents are involved.
4. Produce a Paperclip goal block:

```
---
goal_id: <feature-name>
title: <problem statement, one sentence>
description: |
  <feature spec problem statement>
actors: [<list from spec actors section>]
complexity: <Low | Medium | High>

done_conditions:
  # Each acceptance criterion from spec.md becomes a done condition
  - id: AC-1
    description: <Given/When/Then scenario summary>
  - id: AC-2
    description: ...

agents:
  - role: spec-reviewer
    trigger: on_spec_ready
    model: claude-haiku-4-5-20251001
  - role: architect
    trigger: manual
    required_if: complexity == High
    model: claude-opus-4-8
  - role: implementer
    trigger: ticket_checkout
    model: see_ticket
  - role: validator
    trigger: all_tickets_complete
    model: claude-sonnet-4-6

budget:
  complexity: <Low | Medium | High>
  estimated_tickets: <count from tasks.md if exists, else estimate>
  monthly_cap_usd: <from .paperclip/budgets.md>

approval_gates:
  - after: spec-reviewer  # spec must pass review before tickets created
  - after: validator      # validation must pass before goal marked done

context_bundle:
  - CLAUDE.md
  - .claude/rules/spec-workflow.md
  - specs/constitution.md
  - specs/features/<feature>/
---
```

5. Write output to `specs/features/$ARGUMENTS/paperclip-goal.md`.

Output: path of created paperclip-goal.md and a summary of done conditions and agent assignments.
