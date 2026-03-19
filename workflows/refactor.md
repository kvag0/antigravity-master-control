# /refactor — TARGETED CODE CLEANUP WORKFLOW

**Role:** You are the Master Orchestrator. Your job is to implement code quality improvements identified by `/audit`. No new features. No architectural changes. No scope expansion. Cleaner code that does exactly what it did before, better.

---

## STEP 1 — Audit Findings Intake

Read `project_state.md`. Confirm:

- Current Milestone is `"Audit Complete"` or later.
- There are quality-related tasks in the Task Queue with status `"OPEN"`.
- Overall Status is not `"BLOCKED"` due to a Critical or High security finding — those must go through `/plan` first, not `/refactor`.

If no audit findings exist in the Task Queue, stop. Tell the user to run `/audit` first.

Read `security_audit.md` if it exists. Confirm there are no unresolved Critical or High severity findings. If there are, stop and tell the user these must be addressed via `/plan` before refactoring.

---

## STEP 2 — Refactor Scope Definition

Extract all open quality tasks from the Task Queue. Group them by type:

```
STYLE — PEP 8, formatting, naming conventions
STRUCTURE — functions over 40 lines, missing decomposition, circular imports
DOCUMENTATION — missing docstrings, type hints, inline comments
CONSTANTS — hardcoded values that should be environment variables or constants
PERFORMANCE — identified inefficiencies with a clear, safe fix available
```

Present the grouped list to confirm scope before any code is changed. The user may choose to exclude certain groups.

Do not include any item that is not already in the Task Queue from a prior `/audit`. New improvements identified during this workflow go into the Task Queue for the next cycle — they are not implemented now.

---

## STEP 3 — Refactor Implementation

Invoke `@Senior_Dev` to implement the refactor tasks, grouped by file.

Rules for this step:

- Work file by file. Complete and verify one file before moving to the next.
- For each change, `@Senior_Dev` must state: what changed, why, and confirmation that the external behaviour is identical.
- No function signature changes that would break callers in other modules without explicit user approval.
- No dependency additions or removals.
- Output the complete refactored file for each file touched. No diffs, no snippets.

`@Senior_Dev` must run their 5-point self-review for each file and include the result in the handoff.

If `@Senior_Dev` identifies an improvement not in the audit findings, they must log it in the Task Queue and continue. They must not implement unscoped changes.

---

## STEP 4 — Regression Verification

Invoke `@QA_Specialist` to confirm the refactored code behaves identically to the pre-refactor version.

`@QA_Specialist` must:

- Re-run the original happy path test for every file touched.
- Confirm all previously passing test cases still pass.
- Flag any behavioural difference, however small, as a regression blocker.
- Append the regression verification results to `qa_report.md`. This file must exist and contain the regression results before the Hard Stop message is permitted. If `qa_report.md` does not exist or has not been updated, the workflow has not completed.

If a regression is found, `@Senior_Dev` fixes only that regression before QA re-verifies. This is not a full debug loop — it is a revert-and-redo of the specific change that caused the regression.

---

## STEP 5 — State Update

Invoke `@Project_Manager` to update `project_state.md`:

- Mark all completed refactor tasks as `DONE` in the Task Queue.
- Log each refactor change in the Decision Log with the reason.
- Log any newly identified improvements as `OPEN` tasks for the next cycle.
- Update Current Milestone to `"Refactor Complete"`.
- Set Overall Status based on remaining open items.

`@Project_Manager` must output the complete updated `project_state.md`.

---

## 🛑 HARD STOP

The following actions are strictly forbidden after Step 5:

- Do NOT add features, change behaviour, or expand scope.
- Do NOT invoke `/plan`, `/build`, or `/audit` automatically.
- Do NOT implement any improvements identified during this workflow that were not in the original audit findings.

**Final output (required, verbatim):**

> "Refactor complete. All changes are logged in `project_state.md`. The codebase behaviour is unchanged. Type `/audit` to verify the full codebase, or `/iterate` to begin adding new features."
