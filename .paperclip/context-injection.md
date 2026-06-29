# Paperclip Context Injection

Defines what Paperclip should inject into each agent's context window at runtime. Configure these in the Paperclip agent settings under "Context" or "Prompt injection".

---

## Global (all agents)

Always inject:
- `CLAUDE.md` — workflow rules and model selection
- `.claude/rules/spec-workflow.md` — auto-loaded spec-driven rules
- `specs/constitution.md` — non-negotiable project principles

---

## Per-Agent Context

### architect
```
specs/constitution.md
specs/architecture/principles.md
specs/architecture/overview.md
specs/architecture/decisions/          (all ADR files)
```
Task-scoped addition: the feature's `spec.md` when creating a feature ADR.

### spec-reviewer
```
specs/constitution.md
specs/features/<feature>/spec.md       (target spec only)
```
Keep minimal — reviewer needs spec + principles, nothing else.

### implementer
```
specs/features/<feature>/spec.md
specs/features/<feature>/plan.md
specs/features/<feature>/tasks.md
specs/features/<feature>/contracts/    (all contract files)
```
Do NOT inject: other features' specs, ADRs unrelated to this feature, architecture overview (noise).

### validator
```
specs/features/<feature>/spec.md
specs/features/<feature>/tasks.md
specs/features/<feature>/contracts/
```

---

## Why This Matters

Paperclip injects context at agent startup without retraining. The spec-blueprint structure is designed for this:
- One feature = one directory = one context bundle
- `spec.md` is the single source of truth the agent always gets
- `contracts/` gives agents the interface contract before they touch code
- Global rules in `CLAUDE.md` + `rules/` ensure consistent behavior across all agents
