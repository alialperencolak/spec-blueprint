# Spec: [Feature Name]

| Field | Value |
|-------|-------|
| Status | Draft / Ready / In Progress / Validated / Archived |
| Complexity | Low / Medium / High |
| Created | YYYY-MM-DD |
| Last updated | YYYY-MM-DD |

---

## Problem Statement

_What user or system problem does this feature solve? One paragraph. No solution yet._

---

## Users / Actors

- **[Actor]** — [what they need and why]

---

## Requirements

### Functional

- [ ] FR-1: [Requirement stated as a testable behavior, not as an implementation]
- [ ] FR-2: ...

### Non-Functional

- [ ] NFR-1: [Performance / security / reliability requirement with measurable target]
- [ ] NFR-2: ...

---

## Acceptance Criteria

_These are the definition of done. Each criterion must be independently verifiable._

```gherkin
Scenario: [Happy path]
  Given [precondition]
  When  [action]
  Then  [observable outcome]

Scenario: [Edge case]
  Given ...
  When  ...
  Then  ...

Scenario: [Error case]
  Given ...
  When  ...
  Then  ...
```

---

## Out of Scope

_Explicitly state what this feature will NOT do to prevent scope creep._

- ...

---

## Open Questions

_Unresolved decisions that block or risk the spec. Each should be resolved before `tasks.md` is created._

- [ ] Q1: [Question] → Owner: [name]

---

## Related

- ADRs: [links to relevant Architecture Decision Records]
- Upstream features: [links]
- Downstream features: [links]
- Contracts: [`contracts/` directory]
