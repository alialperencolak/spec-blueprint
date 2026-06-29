# Spec-Driven Development

## Workflow
```
explore → specify → plan → tasks → implement → validate
```
Full rules auto-load from `.claude/rules/spec-workflow.md`.

## Commands
| `/explore <topic>` | Investigate before speccing |
| `/specify <feature>` | Write spec with Gherkin AC |
| `/adr <title>` | Capture architecture decision |
| `/plan <feature>` | Technical design (skip if low complexity) |
| `/tasks <feature>` | Ordered implementation checklist |
| `/implement <feature>` | One task at a time |
| `/validate <feature>` | Verify every AC passes |
| `/goal <feature>` | Export spec as a Paperclip goal definition |
| `/ticket <feature>` | Export tasks as Paperclip tickets with model + budget hints |

## Paperclip Integration

This repo integrates with [Paperclip](https://github.com/paperclipai/paperclip) for multi-agent orchestration.

- `.paperclip/agent-roles.md` — org chart mapping (architect, spec-reviewer, implementer, validator)
- `.paperclip/context-injection.md` — what context Paperclip injects per agent role
- `.paperclip/budgets.md` — per-complexity budget caps and per-ticket cost estimates

**Layer split:** spec-blueprint owns *what* and *quality*. Paperclip owns *who*, *when*, and *cost*.

## Model Selection

Match model to task complexity. Pass the model flag when invoking Claude Code subagents or spawning agents explicitly.

| Task type | Examples | Model |
|-----------|----------|-------|
| **Simple** | Marking tasks complete, renaming files, updating a status field, `.gitignore` edits | `claude-haiku-4-5-20251001` |
| **Normal** | Writing a spec, generating tasks, implementing a single CRUD task, updating an ADR | `claude-sonnet-4-6` |
| **Complex** | Architectural planning, cross-cutting refactors, security review, multi-system design, `/validate` on a high-complexity feature | `claude-opus-4-8` |

### Per-command defaults

| Command | Default model | Override when |
|---------|--------------|---------------|
| `/explore` | sonnet | High architectural uncertainty → opus |
| `/specify` | sonnet | Simple feature → haiku |
| `/adr` | opus | Low-stakes decision → sonnet |
| `/plan` | opus | Low-complexity feature → sonnet |
| `/tasks` | haiku | Tasks depend on complex plan → sonnet |
| `/implement` | haiku (simple task) / sonnet (normal) | Architectural judgment needed → opus |
| `/validate` | sonnet | High-complexity feature with many AC → opus |

## Agents
- `spec-reviewer` — checks spec quality and constitution alignment
- `architect` — ADR creation, complexity assessment, trade-off analysis

## Directory Map
```
specs/
  constitution.md        non-negotiable principles
  architecture/
    overview.md          system context + ADR index
    principles.md        fit-for-purpose rules
    decisions/           ADR-XXXX-*.md files
  features/
    <name>/
      spec.md            what (requirements + AC)
      plan.md            how (technical design)
      tasks.md           ordered checklist
      contracts/         API / event / schema contracts
```

## Context Tips
- Compact manually at ~50% context (`/compact`) — don't wait for auto-compact.
- If responses degrade, `/clear` and resume from `tasks.md` progress.
- `implement` and `validate` commands run forked — they get isolated context automatically.
