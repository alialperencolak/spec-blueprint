# Paperclip Agent Roles

Maps spec-blueprint agents to a Paperclip org chart. Use this as the reference when onboarding into Paperclip via `npx paperclipai onboard`.

---

## Org Chart

```
Architecture Owner
  └── Architect Agent         (specs/architecture, ADRs)
        └── Spec Reviewer     (spec quality gate before implementation)
              └── Implementer (feature implementation, one task at a time)
                    └── Validator (post-implementation AC verification)
```

---

## Agent Definitions

### architect
| Field | Value |
|-------|-------|
| Role | Architecture Owner |
| Model | `claude-opus-4-8` |
| Budget cap | Medium (ADRs are high-value, low-frequency) |
| Triggers | Manual / on new feature spec reaching "Ready" status |
| Deliverables | ADR files in `specs/architecture/decisions/`, updates to `overview.md` |
| Context inject | `CLAUDE.md`, `.claude/rules/spec-workflow.md`, `specs/constitution.md`, `specs/architecture/` |

### spec-reviewer
| Field | Value |
|-------|-------|
| Role | QA / Spec Gatekeeper |
| Model | `claude-haiku-4-5-20251001` |
| Budget cap | Low (read-only, fast) |
| Triggers | Automatic — when a spec.md status changes to "Draft" or "Ready" |
| Deliverables | Review report (pass/fail per section) |
| Context inject | `specs/constitution.md`, target `spec.md` |
| Approval gate | Spec must pass review before `/plan` or `/tasks` can proceed |

### developer (Claude Code)
| Field | Value |
|-------|-------|
| Role | TDD Developer |
| Agent file | `.claude/agents/developer.md` |
| Model | `claude-haiku-4-5-20251001` (simple tasks) / `claude-sonnet-4-6` (normal) / `claude-opus-4-8` (complex) |
| Budget cap | Per ticket — see `budgets.md` |
| Triggers | Ticket checkout (atomic — only one agent per task) |
| Deliverables | Passing test + implementation, checked-off task in `tasks.md` |
| Context inject | `CLAUDE.md`, `.claude/rules/spec-workflow.md`, feature `spec.md`, `plan.md`, `tasks.md` |
| TDD cycle | Red (failing test from AC) → Green (min code to pass) → Refactor |

### validator (Claude Code)
| Field | Value |
|-------|-------|
| Role | QA / Release Gate |
| Model | `claude-sonnet-4-6` |
| Budget cap | Medium |
| Triggers | All tasks in `tasks.md` checked off |
| Deliverables | Validation report, spec status updated to "Validated" |
| Context inject | `CLAUDE.md`, feature `spec.md`, `tasks.md`, `contracts/` |

---

## Reporting Lines

Paperclip approval gates to configure:
1. `spec-reviewer` must PASS before any implementation ticket is created
2. `architect` must create at least one ADR before implementation if feature is High complexity
3. `validator` result must be PASS before spec is archived or feature is shipped
