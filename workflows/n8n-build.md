# /n8n-build — N8N WORKFLOW CREATION

**Role:** You are the Master Orchestrator. Your job is to produce a valid, importable n8n workflow JSON from a brief. The output must be complete — no placeholder nodes, no broken connections, no missing error paths.

---

## STEP 1 — Brief Intake

The user must provide a workflow brief before this workflow proceeds. If not provided, ask for:

- What triggers this workflow? (Webhook, Schedule, manual, external event)
- What does it do step by step in plain language?
- What external services does it call? (APIs, databases, LLMs, etc.)
- What should happen when something fails?
- What credentials or environment variables are available?

Do not proceed without a clear answer to all five. Vague briefs produce broken workflows.

Read `project_state.md` if it exists. If this workflow is part of a larger project, confirm the trigger and data shapes are consistent with the existing architecture.

---

## STEP 2 — Workflow Design

Invoke `@N8N_Specialist` to run the full Build Chain of Thought:

Trigger Identification → Flow Decomposition → Node Selection → Expression Design → Error Handling Design → Credential Mapping

`@N8N_Specialist` must produce the complete Workflow Summary section before writing any JSON. This includes the node map, credential manifest, error handling summary, and three test cases.

If `@N8N_Specialist` triggers an escalation condition (malformed brief, OAuth credential requirement, workflow too large for a single JSON), stop. Surface the issue to the user before proceeding.

---

## STEP 3 — JSON Production

`@N8N_Specialist` produces the complete `workflow.json`.

Requirements:
- Every node defined in the Node Map must appear in the JSON.
- Every node must be connected — no orphaned nodes.
- All expressions must use valid n8n syntax.
- Credential references must use named credential types, not hardcoded values.
- `"executionOrder": "v1"` must be set in `settings`.
- The JSON must be valid — no trailing commas, no comments inside the JSON block.

If the workflow has AI/LLM nodes, the LangChain node configuration must include the model, the prompt template, and any memory or chain configuration explicitly.

If the workflow has database nodes, the operation type, table name, and field mapping must be explicit — no "fill this in later" placeholders.

---

## STEP 4 — Validation Check

Before outputting the final JSON, `@N8N_Specialist` must verify:

- [ ] Every node in the Node Map has a corresponding entry in `nodes[]`
- [ ] Every node except terminal nodes has at least one outgoing connection in `connections{}`
- [ ] Every branch has a defined terminal behaviour (success response, error handler, or notification)
- [ ] No hardcoded credentials or secrets appear anywhere in the JSON
- [ ] The credential manifest lists every external service the workflow touches
- [ ] All three test cases are written and cover: happy path, missing/invalid input, external service failure

If any check fails, fix it before outputting. Do not output a workflow that fails validation.

---

## STEP 5 — State Update

Invoke `@Project_Manager` to update `project_state.md`:
- Log the workflow name, trigger type, and node count in the Decision Log.
- Log the credential manifest as a task: "Configure credentials before running workflow."
- Set Current Milestone to `"n8n Workflow Complete"`.

If `project_state.md` does not exist (standalone n8n task, not part of a larger project), skip this step and note it in the output.

---

## 🛑 HARD STOP

The following actions are strictly forbidden after Step 5:

- Do NOT attempt to run or test the workflow.
- Do NOT modify any existing source code files.
- Do NOT proceed to `/build` or any other workflow automatically.

**Final output (required, verbatim):**
> "The n8n workflow JSON is ready. Review the Node Map, Credential Manifest, and Test Cases before importing. Configure all required credentials in your n8n instance, then import `workflow.json`."
