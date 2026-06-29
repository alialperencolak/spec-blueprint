---
name: plan
description: Generate a technical implementation plan from a ready feature spec.
arguments: true
allowed-tools:
  - Read
  - Write
  - Edit
model: opus
effort: high
---

Generate a technical implementation plan from a ready spec.

Arguments: $ARGUMENTS (feature name matching an existing specs/features/<name>/ directory)

Phase: plan (runs after /specify with status=Ready, before /tasks)

Prerequisite check:
1. Read `specs/features/$ARGUMENTS/spec.md`.
2. Confirm status is "Ready" (not Draft). If Draft, list open questions and stop.
3. Confirm no open questions remain. If any exist, stop and ask the user to resolve them first.

Steps:
1. Read `specs/constitution.md` and `specs/architecture/principles.md` to apply the right constraints.
2. Read `specs/architecture/overview.md` to understand the current system context.
3. Fill in `specs/features/$ARGUMENTS/plan.md`:
   - Technical approach: which components change, what is new, how they interact
   - Component changes table
   - Data model (SQL DDL or schema, not ERDs)
   - API/event contracts: list endpoints/events, create stubs in `contracts/` for each
   - Key trade-offs: alternatives rejected and why
   - Risks and spikes: any unknowns that must be de-risked before implementation begins
   - Validation approach: how implementation will be verified against spec AC
4. For each significant architectural decision surfaced, create an ADR via /adr.

Complexity calibration (from `specs/architecture/principles.md`):
- Low complexity: skip plan.md entirely, proceed to /tasks
- Medium: fill core sections, skip data model if no schema changes
- High: fill all sections, require spike completion before tasks

Output: path of created/updated plan.md, list of ADRs created or needed, list of spikes to complete before implementation.
