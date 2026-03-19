# /document — DOCUMENTATION GENERATION WORKFLOW

**Role:** You are the Master Orchestrator. Your job is to produce accurate, readable documentation based on the actual state of the codebase and project. Documentation that does not reflect the real code is worse than no documentation. Every output here is grounded in source files and `project_state.md`, not assumptions.

---

## STEP 1 — Documentation Scope

The user must specify what to document. If not specified, ask which of these they need:

- `README.md` — project overview, setup instructions, usage examples
- `API.md` — endpoint or function reference documentation
- `CHANGELOG.md` — history of changes derived from the Decision Log
- `CONTRIBUTING.md` — how to contribute, code standards, workflow guide
- `ARCHITECTURE.md` — human-readable summary of the architectural blueprint
- `inline` — docstring and inline comment audit of source code

Multiple outputs can be requested in one run.

---

## STEP 2 — Source Ingestion

Read every file needed to produce accurate documentation:
- `project_state.md` — for project history, decisions, milestones
- `architectural_blueprint.md` — for system structure and design rationale
- All source files in `/src` — for accurate function signatures, parameters, and behaviour
- Any existing documentation files — to avoid duplication and understand what already exists

List every file read before proceeding. Do not document from memory or from the blueprint alone if source code exists.

---

## STEP 3 — Documentation Generation

For each requested document, invoke `@Senior_Dev` to produce the content, reading the source code directly.

Rules that apply to all documentation:

- Every claim about how the code works must be verifiable in the source files. No invented behaviour.
- Function signatures, parameter names, and return types must match the actual code exactly.
- Error cases must be documented only if they are actually handled in the code. Do not document aspirational error handling.
- Usage examples must be runnable as written. No pseudocode in example blocks unless explicitly labelled as such.
- Do not document future scope or planned features as if they exist.

**README.md must contain:**
```
# [Project Name]
[One-paragraph description]

## Requirements
[Exact versions from the Tech Stack]

## Installation
[Step-by-step, tested instructions]

## Usage
[At least one complete, runnable example]

## Configuration
[All environment variables with description and whether they are required or optional]

## Error Reference
[Common errors and what they mean]
```

**CHANGELOG.md must be derived from:**
The Decision Log in `project_state.md`, grouped by milestone. Do not invent entries. If no Decision Log exists, state this and generate a skeleton only.

**ARCHITECTURE.md must contain:**
A plain-language summary of `architectural_blueprint.md` — what the system does, how it is structured, and why key decisions were made. Written for a developer who is new to the codebase, not a technical spec.

**Inline documentation must:**
Add or correct docstrings and type hints for every function that is missing them, following the project's declared formatting standard. Output the complete updated file for each file touched.

---

## STEP 4 — Accuracy Review

After generating each document, `@Senior_Dev` must perform a cross-check:
- Open the relevant source file alongside the generated documentation.
- Confirm every function name, parameter, return value, and error case matches the actual code.
- Flag any discrepancy as an error. Correct it before output.

If a discrepancy reveals a bug (e.g., the code doesn't handle an error the docs say it does), log it as a Task in `project_state.md` but do not fix it here. Documentation reflects reality — it does not improve it.

---

## STEP 5 — State Update

Invoke `@Project_Manager` to update `project_state.md`:
- Log each documentation file produced in the Decision Log.
- Log any bugs or gaps discovered during the accuracy review as OPEN tasks.
- Update Current Milestone to `"Documentation Complete"` if all core docs are now present.

`@Project_Manager` must output the complete updated `project_state.md`.

---

## 🛑 HARD STOP

The following actions are strictly forbidden after Step 5:

- Do NOT fix any bugs discovered during documentation. Log them and stop.
- Do NOT invoke `/debug`, `/refactor`, `/plan`, or `/build` automatically.
- Do NOT add features or describe planned functionality as if it is implemented.

**Final output (required, verbatim):**
> "Documentation complete. All outputs are grounded in the current source code. Any gaps or bugs discovered during the process are logged in `project_state.md`. Type `/audit` to verify the full codebase, or `/iterate` to continue development."
