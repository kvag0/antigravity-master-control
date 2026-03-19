# 🛸 ANTIGRAVITY MASTER CONTROL

Welcome to the **Master Control** workspace. This is a high-performance, multi-agent orchestration framework designed to automate the software development lifecycle (SDLC) through specialized AI personas and rigid workflow boundaries.

---

## ⚡ THE CORE WORKFLOWS

Use these slash commands to move a project from a single idea to a verified codebase.

| Command      | Purpose           | Primary Input                | Primary Output                         |
| :----------- | :---------------- | :--------------------------- | :------------------------------------- |
| **`/setup`** | **The Factory**   | `project_overview.md`        | `project_state.md` & `/project_agents` |
| **`/plan`**  | **The Blueprint** | `project_state.md`           | `architectural_blueprint.md`           |
| **`/build`** | **The Engine**    | `architectural_blueprint.md` | Production Code & QA Audit             |
| **`/audit`** | **The Guard**     | Source Code (`/src`)         | `audit_report.md`                      |

---

## 🤖 THE AI TEAM (ROSTER)

Your project agents are hydrated from templates in the `/agents_library` during the setup phase:

- **`@Architect`**: Designs system structure and logic flow.
- **`@Senior_Dev`**: Writes clean, PEP 8 compliant, production-ready code.
- **`@Security_Lead`**: Identifies vulnerabilities and enforces safety constraints.
- **`@QA_Specialist`**: Performs edge-case testing and logic verification.
- **`@Project_Manager`**: Maintains the `project_state.md` and manages handoffs.

---

## 📜 THE CORE PRINCIPLES (LAWS)

To keep the "Runaway AI" behavior at bay, this framework follows three strict laws:

### 1. The State is Truth

No agent is allowed to finish a turn without the `@Project_Manager` updating the `project_state.md`. This file is the "Long-Term Memory" of the project. If it isn't in the state, the team doesn't know it happened.

### 2. Physical Artifacts Only

We do not use abstract "Implementation Plans." We use physical files (`architectural_blueprint.md`, `audit_report.md`). This creates a "Save Point" that requires user approval before the next phase begins.

### 3. Hard Stops are Mandatory

Every workflow ends with a **Nuclear Hard Stop**. The Orchestrator is forbidden from "auto-proceeding" to the next command. You must manually review the artifact and trigger the next command yourself.

---

## 🛠️ HOW TO USE THIS WORKSPACE

1.  **Define the Goal:** Create a `project_overview.md` in the root.
2.  **Initialize:** Run `/setup`. This builds your folder structure and "hires" your project-specific agents.
3.  **Design:** Run `/plan`. Review the `architectural_blueprint.md` once generated.
4.  **Execute:** Run `/build @architectural_blueprint.md`.
5.  **Verify:** Run `/audit` to find vulnerabilities or refactor opportunities.

---

## 🚦 TROUBLESHOOTING

- **AI won't stop coding?** Check the "Hard Stop" section in your `plan.md` or `build.md` workflow settings.
- **Agents are hallucinating?** Update the templates in `/agents_library` and re-run `/setup` to refresh the project agents.
- **Missing Context?** Ensure you are @mentioning the relevant blueprint or state file when calling a command.

---

**Status:** SYSTEM ONLINE | **Version:** 1.0.0
