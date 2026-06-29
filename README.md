# project-blueprint

A spec-driven development starter for any project type. Specifications are the primary artifact — code follows from them, not the other way around.

## Core Idea

Architectural designs are **hypotheses**. Validate them early with real feedback. The right amount of architecture depends entirely on your project's complexity — not on convention.

```
explore → specify → plan → tasks → implement → validate
    ↑_________________________feedback_________________________|
```

## Quick Start

1. Clone this repo as the foundation for a new project.
2. Fill in `specs/constitution.md` with your project's non-negotiable principles.
3. Update `specs/architecture/overview.md` with your system context.
4. Start a feature with `/explore`, then follow the workflow.

## Directory Structure

```
specs/
  constitution.md              Non-negotiable project principles
  architecture/
    overview.md                System context (C4 Level 1) + ADR index
    principles.md              Architectural principles & trade-off rules
    decisions/
      ADR-0000-template.md     Copy this for each architecture decision
  features/
    _template/                 Copy this for each new feature
      spec.md                  What to build (requirements + acceptance criteria)
      plan.md                  How to build it (technical design)
      tasks.md                 Ordered implementation checklist
      contracts/               API specs, event schemas, data contracts

.claude/
  commands/                    Slash commands for Claude Code
    explore.md     /explore    Investigate before speccing
    specify.md     /specify    Write a feature spec
    adr.md         /adr        Capture an architecture decision
    plan.md        /plan       Generate a technical plan
    tasks.md       /tasks      Break plan into ordered tasks
    implement.md   /implement  Implement tasks one at a time
    validate.md    /validate   Verify implementation vs spec

CLAUDE.md                      AI assistant workflow rules
```

## Workflow Commands

| Command | When to use |
|---------|------------|
| `/explore <topic>` | Before writing any spec — understand constraints and options |
| `/specify <feature>` | Turn requirements into a testable spec with acceptance criteria |
| `/adr <decision title>` | Capture any architectural decision as a hypothesis |
| `/plan <feature>` | Design the technical approach (skip for low-complexity features) |
| `/tasks <feature>` | Break the plan into ordered, verifiable tasks |
| `/implement <feature>` | Implement tasks one at a time, staying inside the spec |
| `/validate <feature>` | Verify every acceptance criterion is satisfied |

## Complexity Calibration

Not every feature needs every phase. Use complexity drivers to decide:

| Complexity | Phases needed |
|---|---|
| Low (simple CRUD, isolated change) | specify → tasks → implement → validate |
| Medium (new subsystem, external dep) | explore → specify → plan → tasks → implement → validate |
| High (cross-cutting, distributed, new tech) | All phases + ADRs + spikes before tasks |

## Architecture Roles

Choose the model that fits your team (see `specs/architecture/principles.md`):

- **No explicit role** — small, self-directed team, low complexity
- **Architecture owner** — distributed teams or high coordination needs  
- **Architecture champions** — specific technical domain challenges
- **Classic architecture role** — hierarchical orgs or very high complexity

## Inspired By

- [OpenSpec](https://github.com/Fission-AI/openspec) — lightweight, fluid spec commands
- [Spec Kit](https://github.com/github/spec-kit) — executable specs as primary artifacts
- [BMad Method](https://github.com/bmad-code-org/bmad-method) — lifecycle coverage, complexity-adaptive depth
- [Manifesto for Agile Architecture](https://www.mhp.com/en/insights/blog/the-manifesto-for-agile-architecture) — architecture as hypothesis, continuous feedback
