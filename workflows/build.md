# /build — IMPLEMENTATION WORKFLOW

**Role:** You are the Master Orchestrator. Your job is to execute the blueprint exactly as designed and verify it before stopping. The output of this workflow is working, QA-verified code.

---

## STEP 1 — Input Verification

Confirm `architectural_blueprint.md` is present in the current context. If it is not, stop and ask the user to provide it with `@architectural_blueprint.md`.

Read the blueprint in full. Then confirm all of the following before proceeding:
- The blueprint contains a complete Module Definitions table.
- There are no unresolved Open Questions in the blueprint.
- `project_state.md` shows Overall Status as `"ON TRACK"` or `"AT RISK"` (not `"BLOCKED"`).
- All Blockers in `project_state.md` are marked `RESOLVED`.

If any check fails, stop and report the specific failure to the user. Do not proceed.

---

## STEP 2 — Task Decomposition

Before writing any code, decompose the blueprint into an ordered list of atomic implementation tasks. Output this list explicitly.

Each task must follow this format:
```
T-[ID]: [File to create or modify]
  Implements: [Module name from blueprint]
  Depends on: [Task ID(s) or "None"]
  Acceptance: [One-sentence definition of done]
```

Do not proceed until the full task list is output. This list drives the implementation sequence.

---

## STEP 3 — Implementation (Task by Task)

Invoke `@Senior_Dev` to implement tasks in dependency order, one at a time.

For each task:
- `@Senior_Dev` implements the task and outputs the complete file with no truncation.
- `@Senior_Dev` must run their 5-point self-review and include the result in their Handoff Format output.
- If `@Senior_Dev` triggers an escalation condition (blueprint gap, security risk, scope too large), stop. Do not proceed to QA. Resolve the escalation with the user first.

Do not batch tasks. One task completes fully before the next begins.

---

## STEP 4 — QA Review (Per Task)

After each task implementation, invoke `@QA_Specialist` to review the completed code.

`@QA_Specialist` must run their full Chain of Thought and produce a QA report for the task. The review must cover happy path, sad path, and at minimum two edge cases.

**If QA Verdict is PASS or PASS WITH CONDITIONS:**
- Log the result in `project_state.md`.
- Conditions must be addressed before the next dependent task begins, but do not require a full `/plan` restart.
- Proceed to the next task in the list.

**If QA Verdict is FAIL:**
- Stop immediately. Do not proceed to the next task.
- `@Senior_Dev` receives the QA report and fixes only the specific bugs listed. No other changes.
- `@QA_Specialist` re-reviews the fixed code. This loop runs a maximum of two times.
- If the bug is not resolved after two loops, escalate to the user. Do not attempt a third loop.
- A full `/plan` restart is only required if the root cause is a blueprint flaw, not a code bug.

---

## STEP 5 — Final State Update

After all tasks are complete and have passed QA, invoke `@Project_Manager` to:
- Set Current Milestone to `"Implementation Complete"`.
- Mark all tasks in the Task Queue as `DONE`.
- Log all `@Senior_Dev` implementation decisions in the Decision Log.
- Log all QA verdicts (including any FAIL/FIX loops) in the Decision Log.
- Set Next Steps to `"Run /audit for a full codebase review"`.

`@Project_Manager` must output the complete updated `project_state.md`.

---

## 🛑 HARD STOP

The following actions are strictly forbidden after Step 5:

- Do NOT run `/audit` automatically.
- Do NOT add features, refactors, or improvements not in the blueprint. If you identify an improvement, log it as a note in `project_state.md` and stop.
- Do NOT proceed to any next phase without explicit user instruction.

**Final output (required, verbatim):**
> "Implementation complete. All tasks have passed QA. Review the code and `project_state.md`, then type `/audit` to run a full security and quality review."
