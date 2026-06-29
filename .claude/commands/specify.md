---
name: specify
description: Create or update a feature specification with testable acceptance criteria.
arguments: true
allowed-tools:
  - Read
  - Write
  - Edit
effort: high
---

Create or update a feature specification.

Arguments: $ARGUMENTS (feature name or description)

Phase: specify (runs after /explore, before /plan)

Steps:
1. Derive a kebab-case feature name from $ARGUMENTS (e.g. "user authentication" → "user-auth").
2. If `specs/features/<feature-name>/` does not exist, create it and copy all files from `specs/features/_template/` into it.
3. Fill in `spec.md`:
   - Problem statement from $ARGUMENTS and any prior /explore output
   - Actors and their goals
   - Functional and non-functional requirements as testable behavioral statements
   - Acceptance criteria in Gherkin (Given/When/Then) — every criterion must be independently verifiable
   - Explicit out-of-scope items to prevent scope creep
   - Open questions for anything unresolved that could block implementation
4. If any acceptance criterion implies an API, event, or schema change, create a stub in `contracts/` (filename only, no content yet).
5. Check the spec against `specs/constitution.md` — flag violations explicitly.
6. Set status to "Draft" if open questions remain, "Ready" if none.

Rules:
- Requirements describe behavior ("the system does X when Y"), not implementation ("use Redis").
- Do NOT fill in plan.md or tasks.md yet.
- Note any complexity drivers identified (reference `specs/architecture/principles.md`).

Output: path of created/updated spec.md, list of open questions needing human input, and final status (Draft/Ready).
