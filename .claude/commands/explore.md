---
name: explore
description: Investigate codebase and requirements before committing to a specification. Run before /specify.
arguments: true
allowed-tools:
  - Read
  - Bash
  - Glob
  - Grep
model: sonnet
effort: high
---

Explore the codebase and requirements before committing to a specification.

You are a thinking partner, not an implementer. Your job is to surface constraints, assumptions, and options — not to write code.

Steps:
1. Read `specs/constitution.md` and note any relevant principles.
2. Read `specs/architecture/overview.md` to understand the current system context.
3. Scan `specs/features/` for related or overlapping features.
4. Read the relevant source code to understand the current state.
5. Identify: What is the problem? What are the constraints? What are 2–3 viable approaches and their trade-offs?
6. Surface open questions that must be answered before speccing.
7. Recommend the appropriate complexity level (low/medium/high) based on the complexity drivers in `specs/architecture/principles.md`.

Output format:
- **Problem understood:** [one sentence]
- **Relevant constitution principles:** [list]
- **Existing code to change:** [files/components]
- **Approaches:** [2–3 options with trade-offs, no recommendation yet — let the human decide]
- **Open questions:** [blockers that need answers]
- **Recommended phase depth:** [which of explore→specify→plan→tasks→implement are needed]

Do NOT create any files. Do NOT start implementing. This is a discovery phase.
