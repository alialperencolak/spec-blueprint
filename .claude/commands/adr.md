---
name: adr
description: Capture an architecture decision as a testable hypothesis with a validation plan.
arguments: true
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
model: opus
effort: medium
---

Create an Architecture Decision Record.

Arguments: $ARGUMENTS (short decision title, e.g. "use postgres for primary storage")

Phase: any (ADRs can be created during explore, specify, plan, or implement)

## Delegate or write directly

If `.paperclip/agent-keys.env` exists, **delegate ADR authoring to the `architect` agent** (below) instead of writing it yourself — per `.paperclip/agent-roles.md`, ADR files are `architect`'s own deliverable, not something to write yourself and merely notify it about afterward. If the file doesn't exist, fall back to **Direct ADR Creation** further down.

### Delegate to architect

a. Send an **actionable** handoff — ask for the ADR to be authored, don't describe one that already exists:
   ```
   source .paperclip/agent-keys.env && npx paperclipai agent-prompt architect "$PAPERCLIP_ARCHITECT_KEY" \
     --title "ADR: <decision title>" \
     "Create an Architecture Decision Record for: <decision title>. Count existing ADRs in specs/architecture/decisions/ and assign the next number (zero-padded to 4 digits). Create specs/architecture/decisions/ADR-<number>-<kebab-title>.md from the template at specs/architecture/decisions/ADR-0000-template.md. Fill in Context (situation forcing the decision, constraints, quality attributes — no solution bias), Decision drivers (specific measurable requirements), Options considered (at least 2 alternatives with pros/cons), Decision (chosen option linked to drivers), Key consequences (outcomes, trade-offs, downstream decisions), and Validation plan (how/when we will know if this was correct). Leave Outcome blank. Status starts Proposed. Flag before creating if this conflicts with specs/constitution.md. Add a row to the Decision Index table in specs/architecture/overview.md." \
     --json
   ```
   Capture the created issue's `id` from the JSON response.

b. Poll `npx paperclipai issue get <issueId> --json` for its `status`, roughly every 10 seconds. Stop polling once status is `done`, `blocked`, `in_review`, or `cancelled`.

c. **Independently verify — never trust the agent's comment alone:**
   - Confirm the ADR file actually exists at the path it reported, with Context, Decision drivers, Options considered (≥2), Decision, Key consequences, and Validation plan all filled in (not template placeholders).
   - Confirm Status is "Proposed" and Outcome is blank.
   - Confirm `specs/architecture/overview.md` actually has a new Decision Index row pointing to it.

d. If status is `blocked`, or verification fails (file missing, sections still templated, overview.md not updated): **stop** and report the discrepancy. Do not fill in the gaps yourself — that defeats the point of delegating.

e. On confirmed success, report: path of the created ADR file and the updated overview.md decision index row.

### Direct ADR Creation (fallback — only when `.paperclip/agent-keys.env` doesn't exist)

Steps:
1. Count existing ADRs in `specs/architecture/decisions/` and assign the next number (zero-padded to 4 digits).
2. Create `specs/architecture/decisions/ADR-<number>-<kebab-title>.md` from the template at `specs/architecture/decisions/ADR-0000-template.md`.
3. Fill in:
   - Context: the situation forcing a decision, constraints, quality attributes at stake — no solution bias
   - Decision drivers: specific measurable requirements driving the choice
   - Options considered: at least 2 alternatives with pros/cons
   - Decision: chosen option with one sentence linking back to drivers
   - Key consequences: positive outcomes, trade-offs accepted, downstream decisions needed
   - Validation plan: how and when we'll know if this was correct
4. Leave "Outcome" blank — it is filled in after real-world feedback.
5. Add a row to the Decision Index table in `specs/architecture/overview.md`.

Rules (either path):
- Status starts as "Proposed". Change to "Accepted" once the team agrees, "Deprecated" if superseded.
- The "Outcome" section is the most important part — schedule a reminder to fill it in after the next relevant milestone.
- If this decision conflicts with `specs/constitution.md`, flag it before creating the ADR.

Output: path of the created ADR file and the updated overview.md decision index row.
