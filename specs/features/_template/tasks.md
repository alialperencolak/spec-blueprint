# Tasks: [Feature Name]

| Field | Value |
|-------|-------|
| Spec | [link to spec.md] |
| Plan | [link to plan.md or "N/A — low complexity"] |
| Started | YYYY-MM-DD |
| Target | YYYY-MM-DD |

---

## Pre-Implementation Checklist

- [ ] All open questions in `spec.md` are resolved
- [ ] All spikes in `plan.md` are completed
- [ ] Contracts in `contracts/` are finalized
- [ ] Team has reviewed spec acceptance criteria

---

## Tasks

> Tasks are ordered by dependency. Complete prerequisites before starting dependents.
> Mark each `[x]` when done. Add notes inline if the task revealed a spec change.

### Phase 1: Foundation

- [ ] T-01: [Task description — specific and verifiable]
  - Acceptance: [how to verify this task is done]
  - Spec AC: [which acceptance criterion this satisfies]

- [ ] T-02: [Task description]
  - Acceptance: ...
  - Depends on: T-01

### Phase 2: Core Logic

- [ ] T-03: ...
- [ ] T-04: ...

### Phase 3: Integration & Contracts

- [ ] T-05: Implement/connect to contracts defined in `contracts/`
- [ ] T-06: Integration tests against spec acceptance criteria

### Phase 4: Validation

- [ ] T-07: Run `/validate` — verify all spec AC pass
- [ ] T-08: Update spec status to "Validated"
- [ ] T-09: Update ADRs with outcomes (if any architectural decisions were tested)

---

## Discovered During Implementation

_Issues or spec contradictions found while implementing. Don't silently fix — document here and update `spec.md`._

| Task | Discovery | Spec Updated? |
|------|-----------|--------------|
| — | — | — |
