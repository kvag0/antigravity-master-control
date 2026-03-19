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
| `/build` | Implement and verify the code             | `architectural_blueprint.md` | Production code, `qa_report.md`                   |
| `/audit` | Full codebase security and quality review | `/src`, `project_state.md`   | `security_audit.md`, updated `project_state.md`   |

### Iteration Workflows

| Command        | Purpose                                               | Input                                             | Output                                               |
| :------------- | :---------------------------------------------------- | :------------------------------------------------ | :--------------------------------------------------- |
| `/iterate`     | Add features to an existing codebase                  | Feature description, `architectural_blueprint.md` | `iteration_blueprint.md`, updated code               |
| `/debug`       | Isolate and fix a specific bug                        | Bug report, `/src`                                | Surgical fix, updated `project_state.md`             |
| `/refactor`    | Clean up code based on audit findings                 | `project_state.md` with open quality tasks        | Refactored source files, updated `qa_report.md`      |
| `/document`    | Generate docs from actual source code                 | `/src`, `project_state.md`                        | `README.md`, `CHANGELOG.md`, `ARCHITECTURE.md`, etc. |
| `/n8n-build`   | Build a new n8n workflow from a brief                 | Workflow brief                                    | `workflow.json`, credential manifest, test cases     |
| `/n8n-convert` | Convert an n8n workflow to typed Python or TypeScript | `workflow.json`, target language                  | Converted code package, `conversion_report.md`       |

---

## 🤖 THE AI TEAM

### Core Agents (`/agents_library`)

These are the production agents hydrated by `@Team_Assembler` during `/setup` and saved to `/project_agents`.

| Agent                   | Role                                                                      | Primary Output                                         |
| :---------------------- | :------------------------------------------------------------------------ | :----------------------------------------------------- |
| `@Architect`            | Designs system structure, module boundaries, data flow, and API contract  | `architectural_blueprint.md`                           |
| `@Senior_Dev`           | Translates blueprints into production code                                | Source files                                           |
| `@Security_Lead`        | Audits for vulnerabilities, verifies blockers, enforces secure-by-default | `security_audit.md`                                    |
| `@QA_Specialist`        | Tests happy paths, sad paths, and edge cases                              | `qa_report.md`                                         |
| `@Project_Manager`      | Owns `project_state.md`, controls agent handoffs, verifies QA artifacts   | Updated `project_state.md`                             |
| `@Debugger`             | Isolates root causes and applies surgical fixes                           | Fixed source files                                     |
| `@N8N_Specialist`       | Designs, analyses, and converts n8n workflows                             | `workflow.json` or converted Python/TypeScript package |
| `@Custom_Agent_Builder` | Interviews the user and produces new agent templates                      | New `_Template.md` in `/agents_library`                |

### Setup Agents (`/setup_agents`)

These run once during `/setup` and are not hydrated into project agents.

| Agent                  | Role                                                                                                     |
| :--------------------- | :------------------------------------------------------------------------------------------------------- |
| `@Project_Initializer` | Validates `project_overview.md`, scaffolds the annotated folder structure, bootstraps `project_state.md` |
| `@Team_Assembler`      | Selects templates, hydrates them with project-specific objectives, runs quality gate before saving       |

---

## 📜 THE THREE LAWS

### 1. The State is Truth

No turn ends without `@Project_Manager` updating `project_state.md`. The state file is the long-term memory of the project. Every decision, blocker, and task lives there. If it is not in the state, it did not happen.

### 2. Physical Artifacts Only

Every phase produces a physical file. `architectural_blueprint.md`, `security_audit.md`, `qa_report.md`, `iteration_blueprint.md` — these are the save points that require your review before the next phase begins. Abstract "plans" or "implementation summaries" are not acceptable outputs. A workflow that claims completion without producing its required artifact has not completed.

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
│   ├── N8N_Specialist_Template.md
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
│   ├── document.md
│   ├── n8n-build.md
│   └── n8n-convert.md
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
├── security_audit.md            # Latest security audit output
└── qa_report.md                 # QA results — must exist before /build or /refactor completes
```

---

## 🛠️ HOW TO USE THIS

### Starting a new project

1. Copy `project_overview_template.md` and fill it out completely. Every blank field causes an agent to make an assumption you did not approve.
2. Run `/setup`. Review the annotated folder structure and agent files. Check that `@Team_Assembler` output a passing hydration quality checklist for each agent.
3. Run `/plan`. Review `architectural_blueprint.md` — confirm the API Contract section is present if your project has a backend. This is your last checkpoint before code is written.
4. Run `/build @architectural_blueprint.md`. Verify `qa_report.md` is produced before the build completes.
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

n8n workflows:
/n8n-build → import and configure in n8n
/n8n-convert → review conversion_report.md → run converted code
```

---

## 🚦 TROUBLESHOOTING

**Agent is not stopping at the Hard Stop?**
Check that the workflow file is loaded in full context and that the Hard Stop section is present at the end. Re-paste the workflow if necessary.

**Agents producing generic or vague output?**
The hydration quality gate in `@Team_Assembler` is the first thing to check. It must output an explicit pass/fail checklist for each agent before saving any file. If it skipped the checklist, the hydration is likely too generic. Re-run `/setup` with a more detailed `project_overview.md`.

**`/build` completed but no `qa_report.md` exists?**
The build did not complete correctly. QA was skipped. Do not proceed to `/audit`. Invoke `@QA_Specialist` manually with the source files and ask it to produce `qa_report.md` before continuing.

**`@Security_Lead` issued APPROVED but a blocker was marked resolved without verification?**
The Blocker Verification step (Step 2b) was skipped or failed silently. Re-run `/audit` and confirm `@Security_Lead` explicitly cites the file and line that resolves each blocker before issuing approval.

**`@Architect` blueprint is missing the API Contract section?**
The blueprint is incomplete. Add the API Contract table manually before running `/build`. Without it, `@Senior_Dev` will invent data shapes independently for each route, which causes drift that `@QA_Specialist` cannot catch without a spec.

**`@Debugger` cannot reproduce the bug?**
The bug report is likely missing the exact trigger condition. Provide the specific input, environment, and sequence of actions that causes the failure. "It crashes sometimes" is not a bug report.

**`/iterate` flagged schema or API contract changes?**
This is a deliberate hard gate. Schema and contract changes affect the entire system. Confirm you understand the impact before proceeding — the gate exists because these changes are the most common source of regressions.

**Need a specialist agent that does not exist?**
Run `@Custom_Agent_Builder`. Do not improvise a template from scratch — the builder enforces the framework structure and integration checks that a hand-written template will likely miss.

**`project_state.md` is out of sync with reality?**
Invoke `@Project_Manager` directly with a summary of the current state and ask it to reconcile and rewrite the file using its output schema. This is a valid manual recovery step.

**n8n JSON produces broken connections after import?**
The workflow failed the Step 4 validation check or the check was skipped. Open the JSON and verify every node in `nodes[]` has a corresponding entry in `connections{}`. Orphaned nodes are the most common cause of import failures.

**n8n conversion produces code that behaves differently than the original workflow?**
Check the Deviations section of `conversion_report.md` first — intentional differences are documented there. If the behaviour difference is not listed, it is an equivalence bug. Run `/debug` against the converted code with the specific input that produces the wrong result.

**Function nodes couldn't be converted cleanly?**
Complex custom JavaScript in n8n Function nodes is the hardest conversion case. If `@N8N_Specialist` flagged a Function node as a deviation, review the original JavaScript manually and decide whether to rewrite it in the target language or keep it as an inline comment with a `TODO`.

---

## 📋 CHANGELOG

### v2.2.0

- **`@N8N_Specialist`** — New agent with dual Chain of Thought: one for building workflows from a brief, one for converting existing n8n JSON to typed Python or TypeScript. Handles LangChain/LLM nodes, database nodes, webhook triggers, and error path mapping.
- **`/n8n-build`** — New workflow for creating valid, importable n8n JSON from a brief. Produces workflow JSON, credential manifest, node map, and three test cases.
- **`/n8n-convert`** — New workflow for converting n8n JSON to typed Python or TypeScript. Produces a full conversion package including type definitions, service modules, `.env.example`, `conversion_report.md`, and a `README.md`.

### v2.1.0

- **`/build`** — Added mandatory `qa_report.md` artifact gate before Hard Stop. Added required `@Senior_Dev` handoff block before QA begins per task. Added Module Definitions cross-reference during task decomposition.
- **`/refactor`** — Added mandatory `qa_report.md` update before Hard Stop.
- **`@Architect`** — Added `## API Contract` as a required output schema section for all projects with a backend API. Added server initialisation order rule to Known Risks.
- **`@Security_Lead`** — Added Blocker Verification as Step 2b in Chain of Thought. Added nested array element validation guidance to OWASP scan step. Clarified Critical finding handling for blueprint reviews vs code reviews.
- **`@Project_Manager`** — Added QA artifact verification to Handoff Intake step. Agent now checks for `qa_report.md` before logging any QA pass.
- **`@Team_Assembler`** — Added hard output gate to Step 4. Hydration quality checklist must be explicitly output with pass/fail per agent before any file is created.
- **`@Project_Initializer`** — Made annotated folder tree mandatory in confirmation output.

### v2.0.0

- Added `/iterate`, `/debug`, `/refactor`, `/document` workflows.
- Added `@Debugger` and `@Custom_Agent_Builder` to agents library.
- Rewrote all five core agent templates with role-specific Chain of Thought, defined output schemas, and explicit escalation conditions.
- Rewrote all four core workflows with structured steps, artifact requirements, and Hard Stop enforcement.
- Rewrote `@Project_Initializer` and `@Team_Assembler` with validation checklists and output schemas.
- Rewrote `project_overview_template.md` with Pre-Existing Decisions, Known Anti-Patterns, and Success Criteria sections.

### v1.0.0

- Initial release. Core workflows: `/setup`, `/plan`, `/build`, `/audit`. Core agents: `@Architect`, `@Senior_Dev`, `@Security_Lead`, `@QA_Specialist`, `@Project_Manager`.

---

**Status:** SYSTEM ONLINE | **Version:** 2.2.0
