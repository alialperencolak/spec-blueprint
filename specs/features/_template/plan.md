# Plan: [Feature Name]

> Skip this file for low-complexity features. Go directly to `tasks.md` when there are no significant architectural decisions, no new external dependencies, and a clear implementation path.

| Field | Value |
|-------|-------|
| Spec | [link to spec.md] |
| Status | Draft / Ready / Superseded |
| Author | — |
| Date | YYYY-MM-DD |

---

## Technical Approach

_How will this be built? Focus on the key structural decisions: what components change, what new components are introduced, and how they interact._

---

## Component Changes

| Component | Change Type | Notes |
|-----------|------------|-------|
| [Component] | New / Modified / Deleted | [Why and what changes] |

---

## Data Model

_Show new or modified schemas. Prefer plain text or SQL DDL over ERDs for version control friendliness._

```sql
-- Example
CREATE TABLE example (
  id UUID PRIMARY KEY,
  ...
);
```

---

## API / Event Contracts

_Define the interface before the implementation. Detailed contracts go in `contracts/`._

- New endpoints / events: [list with links to contract files]
- Breaking changes: [list with migration strategy]

---

## Key Trade-offs

_What did you choose NOT to do, and why? This prevents revisiting closed decisions._

| Alternative | Why Rejected |
|-------------|-------------|
| [Option A] | [Reason] |

---

## Risks & Spikes Needed

| Risk | Mitigation / Spike |
|------|-------------------|
| [Risk] | [Action to de-risk before implementation begins] |

---

## Validation Approach

_How will the plan be verified as correct after implementation? Link to spec acceptance criteria._

- All acceptance criteria in `spec.md` pass
- [Additional integration/performance/security checks]

---

## ADRs Raised

_Architectural decisions surfaced during planning. Create ADR files and link here._

- [ ] [ADR title] → [create ADR-XXXX]
