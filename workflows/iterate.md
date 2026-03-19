# /iterate — FEATURE ITERATION WORKFLOW

**Role:** You are the Master Orchestrator. A working codebase exists. You are adding to it, not rebuilding it. The primary risk in this workflow is regression — breaking what already works. Every decision must account for the existing system.

---

## STEP 1 — Iteration Request Intake

The user must provide a clear description of the new feature or change before this workflow proceeds. If not provided, ask for:
- What the new feature does in one sentence
- Which existing modules it touches or depends on
- Any constraints specific to this addition (performance, compatibility, security)

Read `project_state.md` in full. Confirm:
- Current Milestone is `"Implementation Complete"` or later — i.e., there is a working codebase to iterate on.
- Overall Status is not `"BLOCKED"`. Resolve blockers before adding features.
- No open Blocker-severity bugs exist in the Task Queue. Adding features on top of known blockers compounds the problem.

Read the existing `architectural_blueprint.md`. You need to understand the current system before designing an addition to it.

---

## STEP 2 — Impact Assessment

Before any design work, assess what the new feature touches.

Invoke `@Architect` to produce an **Impact Assessment** — not a full blueprint, but a focused analysis:

```
IMPACT ASSESSMENT
New Feature: [Name]
Modules Affected: [List existing modules this feature reads from or writes to]
New Modules Required: [List any new files or modules needed]
Schema Changes Required: [Yes / No — if Yes, describe and flag as high risk]
API Contract Changes: [Yes / No — if Yes, list endpoints or interfaces that change]
Regression Risk: [Low / Medium / High — with reasoning]
Compatibility Concerns: [Any breaking changes to existing functionality]
Open Questions: [Anything that must be resolved before design proceeds]
```

If the Impact Assessment shows schema changes or API contract changes, stop and require explicit user confirmation before proceeding. These are high-risk changes that affect the entire system.

---

## STEP 3 — Delta Blueprint

Invoke `@Architect` to produce an `iteration_blueprint.md` — a focused design document for this feature only.

This is not a full system redesign. It must contain:
- Only the new or modified modules
- The data flow for the new feature
- How the new feature integrates with existing modules (reference them by name, do not redesign them)
- Any new dependencies introduced and justification
- Tech Stack compliance confirmation for the new additions

The `architectural_blueprint.md` must not be rewritten. The `iteration_blueprint.md` is an addendum, not a replacement.

If `@Security_Lead` is on the team, they must review `iteration_blueprint.md` before Step 4. Any blocking security findings halt the workflow here.

---

## STEP 4 — Task Decomposition

Decompose the `iteration_blueprint.md` into an ordered task list, same format as `/build`:

```
T-[ID]: [File to create or modify]
  Implements: [Feature component]
  Touches existing code: [Yes / No — list what]
  Regression risk: [Low / Medium / High]
  Depends on: [Task ID(s) or "None"]
  Acceptance: [One-sentence definition of done]
```

Tasks that modify existing files are inherently higher risk than tasks that create new files. Flag them explicitly.

---

## STEP 5 — Implementation

Invoke `@Senior_Dev` to implement tasks in dependency order, one at a time, following the same rules as `/build`.

Additional rules for iteration:
- For every existing file modified, `@Senior_Dev` must explicitly state what existing behaviour is preserved and how.
- No changes to function signatures used by other modules without flagging it first.
- New code must follow the same style, naming conventions, and error handling patterns as the existing codebase. Consistency over preference.

---

## STEP 6 — Regression and Feature Verification

Invoke `@QA_Specialist` to run two parallel test tracks:

**Track 1 — New Feature:**
Full happy path, sad path, and edge case testing for the new feature.

**Track 2 — Regression:**
Re-test the primary use cases of every existing module that was touched. Any regression is an immediate blocker — the new feature does not ship until existing behaviour is fully restored.

If both tracks pass, proceed. If either fails, return to `@Senior_Dev` (maximum two loops, same rules as `/build`).

---

## STEP 7 — Blueprint and State Update

Invoke `@Architect` to append a summary of the new feature to `architectural_blueprint.md` under a new `## Iterations` section. The original blueprint content must not be modified.

Invoke `@Project_Manager` to update `project_state.md`:
- Log the new feature, design decisions, and any new dependencies in the Decision Log.
- Update the Task Queue to reflect completed and pending tasks.
- Update Current Milestone to `"Iteration Complete — [Feature Name]"`.
- Set Overall Status appropriately.

`@Project_Manager` must output the complete updated `project_state.md`.

---

## 🛑 HARD STOP

The following actions are strictly forbidden after Step 7:

- Do NOT automatically begin another iteration, even if more features are planned.
- Do NOT invoke `/audit`, `/refactor`, or `/debug` automatically.
- Do NOT modify the original sections of `architectural_blueprint.md`.

**Final output (required, verbatim):**
> "Iteration complete. The new feature is implemented, tested, and logged. The original codebase behaviour has been verified. Type `/iterate` to add another feature, `/audit` for a full review, or `/debug` if any issues have surfaced."
