# 🛸 ANTIGRAVITY MASTER CONTROL

A multi-agent orchestration framework for automating the software development lifecycle through specialised AI personas, strict workflow boundaries, and physical file artifacts.

---

## ⚡ WORKFLOWS

Each workflow is a slash command that moves the project through one defined phase. They are sequential by default but can be run independently when the state file is valid.

### Core Workflows

| Command  | Purpose                                   | Input                        | Output                                            |
| :------- | :---------------------------------------- | :--------------------------- | :------------------------------------------------ |
| `/setup` | Initialise the project environment        | `project_overview.md`        | `project_state.md`, `/project_agents`             |
| `/plan`  | Design the architecture                   | `project_state.md`           | `architectural_blueprint.md`, `security_audit.md` |
| `/build` | Implement and verify the code             | `architectural_blueprint.md` | Production code, QA reports                       |
| `/audit` | Full codebase security and quality review | `/src`, `project_state.md`   | `security_audit.md`, updated `project_state.md`   |

### Iteration Workflows

| Command     | Purpose                               | Input                                             | Output                                               |
| :---------- | :------------------------------------ | :------------------------------------------------ | :--------------------------------------------------- |
| `/iterate`  | Add features to an existing codebase  | Feature description, `architectural_blueprint.md` | `iteration_blueprint.md`, updated code               |
| `/debug`    | Isolate and fix a specific bug        | Bug report, `/src`                                | Surgical fix, updated `project_state.md`             |
| `/refactor` | Clean up code based on audit findings | `project_state.md` with open quality tasks        | Refactored source files                              |
| `/document` | Generate docs from actual source code | `/src`, `project_state.md`                        | `README.md`, `CHANGELOG.md`, `ARCHITECTURE.md`, etc. |

---

## 🤖 THE AI TEAM

### Core Agents (`/agents_library`)

These are the production agents hydrated by `@Team_Assembler` during `/setup` and saved to `/project_agents`.

| Agent                   | Role                                                                | Primary Output                          |
| :---------------------- | :------------------------------------------------------------------ | :-------------------------------------- |
| `@Architect`            | Designs system structure, module boundaries, and data flow          | `architectural_blueprint.md`            |
| `@Senior_Dev`           | Translates blueprints into production code                          | Source files                            |
| `@Security_Lead`        | Audits for vulnerabilities and enforces secure-by-default practices | `security_audit.md`                     |
| `@QA_Specialist`        | Tests happy paths, sad paths, and edge cases                        | `qa_report.md`                          |
| `@Project_Manager`      | Owns `project_state.md` and controls agent handoffs                 | Updated `project_state.md`              |
| `@Debugger`             | Isolates root causes and applies surgical fixes                     | Fixed source files                      |
| `@Custom_Agent_Builder` | Interviews the user and produces new agent templates                | New `_Template.md` in `/agents_library` |

### Setup Agents (`/setup_agents`)

These run once during `/setup` and are not hydrated into project agents.

| Agent                  | Role                                                                                                                       |
| :--------------------- | :------------------------------------------------------------------------------------------------------------------------- |
| `@Project_Initializer` | Validates `project_overview.md`, scaffolds the folder structure, and bootstraps `project_state.md`                         |
| `@Team_Assembler`      | Selects templates from `/agents_library`, hydrates them with project-specific content, and saves them to `/project_agents` |

---

## 📜 THE THREE LAWS

### 1. The State is Truth

No turn ends without `@Project_Manager` updating `project_state.md`. The state file is the long-term memory of the project. Every decision, blocker, and task lives there. If it is not in the state, it did not happen.

### 2. Physical Artifacts Only

Every phase produces a physical file. `architectural_blueprint.md`, `security_audit.md`, `qa_report.md`, `iteration_blueprint.md` — these are the save points that require your review before the next phase begins. Abstract "plans" or "implementation summaries" are not acceptable outputs.

### 3. Hard Stops are Mandatory

Every workflow ends with a Hard Stop. The Orchestrator is forbidden from auto-proceeding. You review the artifact, then you trigger the next command. This is not optional.

---

## 🗂️ PROJECT STRUCTURE

```
/
├── agents_library/              # Master template library — never modified during a project
│   ├── Architect_Template.md
│   ├── Senior_Dev_Template.md
│   ├── Security_Lead_Template.md
│   ├── QA_Specialist_Template.md
│   ├── Project_Manager_Template.md
│   ├── Debugger_Template.md
│   └── Custom_Agent_Builder_Template.md
│
├── setup_agents/                # One-time initialisation agents
│   ├── Project_Initializer.md
│   └── Team_Assembler.md
│
├── workflows/                   # Slash command definitions
│   ├── setup.md
│   ├── plan.md
│   ├── build.md
│   ├── audit.md
│   ├── iterate.md
│   ├── debug.md
│   ├── refactor.md
│   └── document.md
│
├── project_overview_template.md # Fill this out to start a new project
├── project_overview.md          # Your completed project brief (created by you)
└── README.md
```

Once `/setup` runs, each project gets its own workspace:

```
your-project/
├── project_agents/              # Hydrated agents for this project only
├── src/                         # Application source code
├── tests/                       # Test files mirroring src/ structure
├── docs/                        # Documentation and architectural artifacts
├── .env.example                 # Environment variable template
├── project_state.md             # Live project state — the single source of truth
├── architectural_blueprint.md   # System design artifact
├── iteration_blueprint.md       # Addendum for each feature iteration (created by /iterate)
└── security_audit.md            # Latest security audit output
```

---

## 🛠️ HOW TO USE THIS

### Starting a new project

1. Copy `project_overview_template.md` and fill it out completely. Every blank field causes an agent to make an assumption you did not approve.
2. Run `/setup`. Review the folder structure and agent files it produces.
3. Run `/plan`. Review `architectural_blueprint.md` before proceeding. This is your last checkpoint before code is written.
4. Run `/build @architectural_blueprint.md`. Review the code and QA reports.
5. Run `/audit` to verify security and quality before shipping.

### Iterating on an existing project

1. Run `/iterate` with a description of the new feature.
2. Review `iteration_blueprint.md` before implementation begins.
3. Run `/audit` after each significant iteration.

### Fixing bugs

Run `/debug` with a clear description of the failure. One bug per run. Additional bugs discovered during the session are logged to the Task Queue for the next `/debug` call.

### Cleaning up after an audit

Run `/refactor` to address quality findings. `/refactor` will not run if unresolved Critical or High security findings exist — those go through `/plan` first.

### Adding a new specialist agent

Run `@Custom_Agent_Builder`. It will interview you, check for overlap with existing agents, and produce a complete template ready to drop into `/agents_library`.

---

## 🔄 WORKFLOW SEQUENCE MAP

```
New project:
/setup → /plan → /build → /audit
                              ↓
                         /refactor  (quality issues)
                         /plan      (security issues)

Ongoing development:
/iterate → /build → /audit → /refactor (repeat)

Bug resolution:
/debug → (back to current milestone)

Documentation:
/document (can run at any milestone after /build)
```

---

## 🚦 TROUBLESHOOTING

**Agent is not stopping at the Hard Stop?**
Check that the workflow file is loaded in full context and that the Hard Stop section is present at the end. Re-paste the workflow if necessary.

**Agents producing generic or vague output?**
The hydration quality in `@Team_Assembler` is the usual cause. Re-run `/setup` with a more detailed `project_overview.md`. Vague input produces vague agents.

**`@Debugger` cannot reproduce the bug?**
The bug report is likely missing the exact trigger condition. Provide the specific input, environment, and sequence of actions that causes the failure. "It crashes sometimes" is not a bug report.

**`/iterate` flagged schema or API contract changes?**
This is a deliberate hard gate. Schema and contract changes affect the entire system. Confirm you understand the impact before proceeding — the gate exists because these changes are the most common source of regressions.

**Need a specialist agent that does not exist?**
Run `@Custom_Agent_Builder`. Do not improvise a template from scratch — the builder enforces the framework structure and integration checks that a hand-written template will likely miss.

**`project_state.md` is out of sync with reality?**
Invoke `@Project_Manager` directly with a summary of the current state and ask it to reconcile and rewrite the file using its output schema. This is a valid manual recovery step.

---

**Status:** SYSTEM ONLINE | **Version:** 2.0.0
