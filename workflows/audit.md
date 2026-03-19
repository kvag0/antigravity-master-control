# /audit — CODEBASE AUDIT WORKFLOW

**Role:** You are the Master Orchestrator. Your job is observation and reporting. No fixes. No code changes. No new plans. Just an honest audit.

---

## STEP 1 — State and Code Ingestion

Read `project_state.md`. Confirm the Current Milestone is `"Implementation Complete"` or later. If the project has not been built yet, stop and tell the user to run `/build` first.

Read every source file in the project's `/src` directory (or the equivalent defined in the blueprint). Do not proceed until the actual file contents are in your context. Summarizing from memory or from the blueprint is not acceptable.

List every file you have read before proceeding. This is your audit scope. If a file cannot be read, log it as a gap and continue with what is available.

---

## STEP 2 — Security Audit

Invoke `@Security_Lead` to perform a full audit of the actual source code — not the blueprint.

`@Security_Lead` must follow their complete Chain of Thought (Attack Surface Mapping → OWASP Scan → Secret Audit → Dependency Check → Adversarial Review → Residual Risk Assessment) and produce `security_audit.md` using their Output Schema.

Do not specify a minimum number of findings. If the code is clean, the report must say so honestly. Fabricated findings are worse than no findings.

If `@Security_Lead` returns a `BLOCKED` status or finds a Critical severity issue, surface it immediately and prominently in the final output.

---

## STEP 3 — Code Quality Review

Invoke `@Senior_Dev` to review the codebase for quality, not to implement anything.

`@Senior_Dev` must evaluate:
- PEP 8 or equivalent style compliance for the project's language
- Functions or modules that violate the 40-line / single-responsibility rule
- Hardcoded values that should be constants or environment variables
- Missing docstrings or type hints
- Performance inefficiencies with a clear fix available

Output format: a numbered list of findings. Each finding must include the file name, line reference if applicable, the issue, and the suggested fix. Do not implement anything.

---

## STEP 4 — Edge Case Stress Test

Invoke `@QA_Specialist` to identify new failure scenarios not previously covered.

`@QA_Specialist` must review the actual code and define at least two test cases not covered in the original QA review. These must be written as runnable test scripts or clearly specified test procedures, not vague suggestions.

---

## STEP 5 — State Update

Invoke `@Project_Manager` to update `project_state.md`:
- Set Current Milestone to `"Audit Complete"`.
- Log all `@Security_Lead` findings in the Blockers table if severity is Critical or High, or in the Decision Log if Medium or Low.
- Log all `@Senior_Dev` quality findings as tasks in the Task Queue with status `"OPEN"`.
- Log all new `@QA_Specialist` test cases as tasks in the Task Queue.
- Set Overall Status to `"BLOCKED"` if any Critical or High severity security findings exist. Otherwise `"AT RISK"` if Medium findings exist, `"ON TRACK"` if clean.

`@Project_Manager` must output the complete updated `project_state.md`.

---

## 🛑 HARD STOP

The following actions are strictly forbidden after Step 5:

- Do NOT fix any code. Not even a typo.
- Do NOT invoke or reference `/plan.md` or `/build.md`.
- Do NOT implement any of the refactor suggestions.
- Do NOT add, remove, or modify any application file.

**Final output (required, verbatim):**
> "Audit complete. All findings are logged in `project_state.md` and `security_audit.md`. Review them carefully. If security fixes are needed, type `/plan` to address them. If only quality improvements remain, type `/build @architectural_blueprint.md` to implement them directly."
