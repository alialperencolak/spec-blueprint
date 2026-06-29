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
