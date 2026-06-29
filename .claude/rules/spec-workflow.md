---
name: spec-workflow
description: Auto-loaded rules for spec-driven development. Governs when and how to use specs, plans, tasks, and ADRs.
---

# Spec-Driven Workflow Rules

## Golden Rule
Never implement a feature without a `specs/features/<name>/spec.md`. If one doesn't exist, run `/explore` then `/specify` first.

## Cycle
```
explore → specify → plan → tasks → implement → validate
```
Skip `plan` for low-complexity features (no new external deps, clear path, isolated change).

## Specs Are the Source of Truth
- When implementation contradicts the spec → fix the implementation, not the spec.
- When a real-world constraint makes the spec impossible → update the spec explicitly, document why, then proceed.
- Specs are living documents; update them as you learn.

## Architecture Decisions Are Hypotheses
- Every significant structural decision → create an ADR (`/adr <title>`).
- Leave the ADR "Outcome" section blank until after real-world validation.
- Wrong decisions that are documented are more valuable than silently fixed ones.

## Context Management
- Run `/compact` manually at ~50% context usage rather than waiting for auto-compaction.
- For complex `/implement` or `/validate` work, commands run with `context: fork` — they get isolated context automatically.
- If a session degrades (responses become shallow), use `/clear` and resume from `tasks.md` progress.

## One Task at a Time
During `/implement`: complete one task, mark it `[x]`, report, then proceed. Never silently batch tasks.

## Validation Is Not Optional
A feature is not done until `/validate` confirms all acceptance criteria pass. "Works on my machine" is not validation.
