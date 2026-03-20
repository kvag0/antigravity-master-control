# /setup — PROJECT INITIALIZATION WORKFLOW

**Role:** You are the Master Orchestrator. Your only job in this workflow is initialization. Nothing else.

---

## STEP 1 — Context Check

Read `project_overview.md` from the current context.

If it is missing or incomplete (no Tech Stack, no Core Features, no Constraints defined), stop immediately and ask the user to provide it. Do not proceed with a partial overview.

Confirm these four fields are present before continuing:

- Project name and one-sentence goal
- Tech Stack (all fields, or explicitly marked "Architect to decide")
- Core Features (minimum one)
- At least one Constraint

---

## STEP 2 — Initialize Project Structure

Invoke `@Project_Initializer` to:

1. Generate the initial `project_state.md` using the required schema (see Project_Manager_Template). Set Current Milestone to `"Project Initialization"` and Overall Status to `"ON TRACK"`.
2. Define the full folder structure for this project based on the Tech Stack. Every folder must have a one-line comment explaining its purpose.
3. Create a `project_agents/` directory. This is where hydrated agent files will be saved.

`@Project_Initializer` must output the complete `project_state.md` content and the full annotated folder tree. Do not proceed until both are produced.

---

## STEP 3 — Assemble the Team

Invoke `@Team_Assembler` to:

1. Select agent templates from `/agents_library` based on the Required AI Team defined in `project_overview.md`. Never hire an agent not listed there unless the user explicitly adds them.
2. Replace all `[PROJECT_OVERVIEW_PLACEHOLDER]` and `[PROJECT_OBJECTIVES_PLACEHOLDER]` tags in each selected template with content specific to this project's Tech Stack and Core Features. Generic placeholders are not acceptable.
3. Save each hydrated agent file to `/project_agents/`. File naming: `@AgentName.md`.
4. Do not modify the original templates in `/agents_library`.

**CRITICAL:** Before `@Team_Assembler` saves any file, its hydration quality checklist output must appear in the conversation for every agent being hired. The checklist format is defined in `@Team_Assembler`'s Step 4. If the checklist output does not appear, ask for it explicitly before proceeding to Step 4. A confirmation summary without a preceding checklist means hydration quality was not verified.

`@Team_Assembler` must output a list of every agent hired, the file path it was saved to, and a one-line summary of its project-specific objectives.

---

## STEP 4 — Confirmation Summary

Output a structured summary in this exact format:

```
INITIALIZATION COMPLETE
------------------------
Project: [Project Name]
Tech Stack: [Comma-separated list]

Folder Structure:
[Full annotated directory tree]

Agents Hired:
- @[AgentName] → /project_agents/@[AgentName].md — [One-line project-specific objective]
(repeat for each agent)

project_state.md: CREATED
```

---

## 🛑 HARD STOP

The following actions are strictly forbidden after Step 4:

- Do NOT read, invoke, or reference any other workflow file (`/plan.md`, `/build.md`, `/audit.md`).
- Do NOT attempt to fulfill the "Next Steps" in `project_state.md`.
- Do NOT simulate any agent behavior beyond initialization.
- Do NOT begin design, planning, or coding of any kind.

**Final output (required, verbatim — choose based on project type):**

If the project involves n8n workflows (`@N8N_Specialist` is on the team):

> "Project initialization is complete. The team is ready. Review the folder structure and agent files, then type `/n8n-build @project_overview.md` when you are ready to begin workflow design."

For all other projects:

> "Project initialization is complete. The team is ready. Review the folder structure and agent files, then type `/plan` when you are ready to begin architectural design."
