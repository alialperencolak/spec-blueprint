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
4. (Optional) Set up [Paperclip](https://github.com/paperclipai/paperclip) for multi-agent orchestration — see [Paperclip Integration](#paperclip-integration) below.
5. Start a feature with `/explore`, then follow the workflow.

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
    goal.md        /goal       Export spec as a Paperclip goal
    ticket.md      /ticket     Export tasks as Paperclip tickets

.paperclip/
  agent-roles.md                Org chart mapping specs-blueprint agents to Paperclip
  context-injection.md           What context Paperclip injects per agent role
  budgets.md                     Per-complexity budget caps and cost estimates
  agent-keys.env                 Local-only agent API keys (gitignored, not created by default)

CLAUDE.md                      AI assistant workflow rules
```

## Workflow Commands

| Command | When to use | Reports to Paperclip agent |
|---------|------------|------------------------------|
| `/explore <topic>` | Before writing any spec — understand constraints and options | — |
| `/specify <feature>` | Turn requirements into a testable spec with acceptance criteria | `spec-reviewer` |
| `/adr <decision title>` | Capture any architectural decision as a hypothesis | `architect` |
| `/plan <feature>` | Design the technical approach (skip for low-complexity features) | — |
| `/tasks <feature>` | Break the plan into ordered, verifiable tasks — auto-exports Paperclip `goal`/`tickets` | — |
| `/implement <feature>` | Delegates each task to `developer` for autonomous TDD (falls back to implementing directly if Paperclip isn't configured) | `developer`, per task |
| `/validate <feature>` | Verify every acceptance criterion is satisfied | `validator` |

Reporting to a Paperclip agent only happens if `.paperclip/agent-keys.env` exists locally; otherwise the step is skipped silently. See [Paperclip Integration](#paperclip-integration).

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

## Paperclip Integration

This repo optionally integrates with [Paperclip](https://github.com/paperclipai/paperclip) for multi-agent orchestration and a dashboard view of who's doing what. spec-blueprint owns *what* and *quality*; Paperclip owns *who*, *when*, and *cost*.

Setup:

1. Run `npx paperclipai onboard` to create/connect a company and register the 4 agents from `.paperclip/agent-roles.md`: `architect`, `spec-reviewer`, `developer`, `validator`.
2. Start the instance: `npx paperclipai run` (serves the dashboard, default `http://127.0.0.1:3100` for a local instance).
3. Create an API key per agent and save them locally:
   ```
   npx paperclipai token agent create -C <company-id> --agent architect --name spec-workflow --json
   ```
   Repeat for `spec-reviewer`, `developer`, `validator`. Store all 4 tokens in `.paperclip/agent-keys.env` (already gitignored — never commit these):
   ```
   PAPERCLIP_COMPANY_ID=...
   PAPERCLIP_API_BASE=http://127.0.0.1:3100
   PAPERCLIP_ARCHITECT_KEY=...
   PAPERCLIP_SPEC_REVIEWER_KEY=...
   PAPERCLIP_DEVELOPER_KEY=...
   PAPERCLIP_VALIDATOR_KEY=...
   ```
4. That's it — `/specify`, `/adr`, `/implement`, and `/validate` each report their activity to the matching agent automatically (see table above), and `/tasks` auto-exports `paperclip-goal.md` / `paperclip-tickets.md` for every feature.

If `.paperclip/agent-keys.env` doesn't exist, all reporting steps are skipped silently — the spec-driven workflow works standalone without Paperclip.

## Inspired By

- [OpenSpec](https://github.com/Fission-AI/openspec) — lightweight, fluid spec commands
- [Spec Kit](https://github.com/github/spec-kit) — executable specs as primary artifacts
- [BMad Method](https://github.com/bmad-code-org/bmad-method) — lifecycle coverage, complexity-adaptive depth
- [Manifesto for Agile Architecture](https://www.mhp.com/en/insights/blog/the-manifesto-for-agile-architecture) — architecture as hypothesis, continuous feedback
