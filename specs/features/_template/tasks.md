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
- [ ] Test framework is set up and runnable (`Bash` the test runner to confirm)

---

## Tasks

> TDD order per task: **Red** (write failing test from AC) → **Green** (minimum code to pass) → **Refactor** (clean while green).
> Mark `[x]` only after the test passes. Record the test file inline.

### Phase 1: Foundation

- [ ] T-01: [Task description — specific and verifiable]
  - Spec AC: [which Given/When/Then scenario this satisfies]
  - Test: [test file path once written, e.g. `tests/unit/feature.test.ts`]
  - Depends on: —

- [ ] T-02: [Task description]
  - Spec AC: ...
  - Test: ...
  - Depends on: T-01

### Phase 2: Core Logic

- [ ] T-03: ...
  - Spec AC: ...
  - Test: ...
  - Depends on: T-01, T-02

- [ ] T-04: ...
  - Spec AC: ...
  - Test: ...

### Phase 3: Integration & Contracts

- [ ] T-05: Implement against contracts in `contracts/`
  - Spec AC: ...
  - Test: integration test covering the contract interface
  - Depends on: T-03, T-04

- [ ] T-06: Integration tests — all contract endpoints/events covered
  - Spec AC: all AC that touch external interfaces
  - Test: `tests/integration/`

### Phase 4: Validation

- [ ] T-07: Run `/validate` — all spec AC must pass end-to-end
- [ ] T-08: Update spec status to "Validated"
- [ ] T-09: Update ADRs with outcomes (fill in "Outcome" sections)

---

## Test Coverage Map

_Filled in as tasks complete. Every spec AC must have a corresponding test._

| Spec AC | Test file | Status |
|---------|-----------|--------|
| AC-1: [scenario name] | — | — |
| AC-2: [scenario name] | — | — |

---

## Discovered During Implementation

_Spec contradictions or new constraints found while implementing. Never silently fix — document here and update `spec.md`._

| Task | Discovery | Spec Updated? |
|------|-----------|--------------|
| — | — | — |
