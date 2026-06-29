# Spec-Driven Development — Project Instructions

## Workflow

Every change follows this cycle:

```
explore → specify → plan → tasks → implement → validate → (archive)
```

Use the slash commands in `.claude/commands/` to move through each phase.

## Rules

1. **Specs before code.** Never implement a feature without a `specs/features/<name>/spec.md`. If one doesn't exist, run `/explore` then `/specify` first.
2. **Architecture decisions are hypotheses.** Capture them in `specs/architecture/decisions/` as ADRs. Update the ADR with observed outcomes — decisions that prove wrong should say so explicitly.
3. **Specs are living documents.** When implementation reveals a constraint that contradicts the spec, update the spec first, then proceed. The spec is always the source of truth.
4. **Right amount of architecture.** Simple CRUD features can skip `plan.md` and go straight to `tasks.md`. Complex, distributed, or cross-cutting changes require all phases. Let complexity drive depth, not habit.
5. **Validate before closing.** After implementing, run `/validate` against the spec's acceptance criteria. A feature is not done until it passes its own spec.

## Directory Map

```
specs/
  constitution.md          — non-negotiable project principles
  architecture/
    overview.md            — system context (update as architecture evolves)
    principles.md          — architectural principles & trade-off rules
    decisions/             — ADRs (Architecture Decision Records)
  features/
    <feature-name>/
      spec.md              — what to build (requirements, AC, edge cases)
      plan.md              — how to build it (technical design)
      tasks.md             — ordered task checklist
      contracts/           — API schemas, event contracts, data models
```

## Architecture Role

Choose the architecture model appropriate to your team (see `specs/architecture/principles.md`):
- **No explicit role** — small, self-directed team, low complexity
- **Architecture owner** — distributed teams or high coordination needs
- **Architecture champions** — specific technical domain challenges
- **Classic architecture role** — hierarchical orgs or very high complexity

## Complexity Calibration

Before starting any feature, assess complexity drivers:
- High quality / non-functional requirements
- Tight time or budget constraints
- Large or distributed team
- New/unfamiliar technology
- External dependencies
- Existing conflicting goals

More drivers → more architecture work. Fewer drivers → skip phases and ship faster.
