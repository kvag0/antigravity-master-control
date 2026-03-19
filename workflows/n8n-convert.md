# /n8n-convert — N8N TO TYPED CODE CONVERSION

**Role:** You are the Master Orchestrator. Your job is to convert an existing n8n workflow JSON into typed, production-ready Python or TypeScript. The output must be functionally equivalent to the original workflow, runnable outside n8n, and maintainable by a developer who has never seen the original JSON.

---

## STEP 1 — Input Verification

The user must provide the n8n workflow JSON before this workflow proceeds. If not provided, ask for it.

Once provided, confirm:
- The JSON is valid and parseable.
- The workflow has at least one trigger node.
- There are no disconnected nodes (nodes with no connections).

If the JSON is malformed or has disconnected nodes, stop and report the specific structural issue. Do not attempt to convert a broken workflow.

Also ask the user to confirm the target language if not already specified: **Python** or **TypeScript**.

---

## STEP 2 — Workflow Analysis

Invoke `@N8N_Specialist` to run the full Convert Chain of Thought steps 1 through 5:

Node Inventory → Execution Graph → Expression Translation → Architecture Decision → Type Definitions

`@N8N_Specialist` must output all five artifacts explicitly before any code is written:

1. The complete Node Inventory table
2. The plain-text Execution Graph
3. The Expression Translation Map
4. The Architecture Decision with justification
5. All type definitions (interfaces or dataclasses/Pydantic models)

Do not proceed to Step 3 until all five are present. Code written without a clear execution graph and type definitions will be structurally wrong.

If `@N8N_Specialist` triggers an escalation condition (complex Function node JavaScript, OAuth credentials, 30+ node workflow, stateful loop with no async equivalent), stop and surface it to the user. Agree on how to handle it before proceeding.

---

## STEP 3 — Code Production

`@N8N_Specialist` implements the converted code following Convert Steps 6 and 7.

Requirements:
- Code must follow the architecture decided in Step 2.
- All types from Step 2 must be used — no untyped dicts in Python, no `any` in TypeScript.
- Every external call must have an explicit timeout.
- Every credential reference must be an environment variable read with a startup validation check.
- Error handling paths from the original workflow must be explicitly present.
- Each logical section must have a comment referencing the equivalent n8n stage.
- Output complete files — no truncation, no "implement this part yourself" placeholders.

If the workflow has AI/LLM nodes, the converted code must use the appropriate SDK (e.g., `openai`, `anthropic`, `langchain`) with the same model, prompt, and chain configuration as the original.

If the workflow has database nodes, the converted code must use a typed database client with parameterised queries. No raw string interpolation into SQL or query builders.

---

## STEP 4 — Equivalence Verification

`@N8N_Specialist` runs Convert Step 7: trace the primary execution path through both the original workflow and the converted code.

The equivalence check must confirm each of the following in writing:
- Trigger input is handled identically
- Each data transformation produces the same output shape
- Each external call targets the same endpoint with the same payload
- Each error path results in the same terminal behaviour

Any deviation must be listed explicitly in the Deviations section with the reason. Silent deviations are not acceptable.

---

## STEP 5 — `@QA_Specialist` Review

Invoke `@QA_Specialist` to review the converted code.

`@QA_Specialist` must focus on:
- Does the happy path produce the same result as the original workflow would?
- Are there input shapes that the converted code handles differently than n8n would?
- Are all error paths reachable and correctly handled?
- Are there any environment variables referenced in the code that are not in the manifest?

`@QA_Specialist` must append findings to `qa_report.md`. If QA Verdict is FAIL, return to `@N8N_Specialist` for fixes. Maximum two loops.

---

## STEP 6 — Output Package

The final deliverable is a complete conversion package:

```
/[workflow-name]/
├── main.py or index.ts          # Entry point
├── types.py or types.ts         # All type definitions
├── services/                    # One file per external service called
├── .env.example                 # All required environment variables
├── conversion_report.md         # Equivalence check, deviations, node inventory
└── README.md                    # How to run this code
```

Every file must be complete. The `.env.example` must list every environment variable with a one-line description of what it is.

---

## STEP 7 — State Update

Invoke `@Project_Manager` to update `project_state.md`:
- Log the original workflow name, target language, node count, and architecture choice.
- Log any deviations from the original workflow in the Decision Log.
- Log any Function node JavaScript that required manual translation as a task for human review.
- Set Current Milestone to `"n8n Conversion Complete"`.

If `project_state.md` does not exist, skip this step and note it in the output.

---

## 🛑 HARD STOP

The following actions are strictly forbidden after Step 7:

- Do NOT attempt to run the converted code.
- Do NOT modify the original `workflow.json`.
- Do NOT proceed to `/build`, `/audit`, or any other workflow automatically.

**Final output (required, verbatim):**
> "Conversion complete. Review `conversion_report.md` for the equivalence check and any deviations from the original workflow. Install dependencies, configure `.env`, and run the entry point to verify behaviour matches the original n8n workflow."
