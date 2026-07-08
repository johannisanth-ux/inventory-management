# GitHub Copilot Vibe Coding Tutorial

## Course theme

This tutorial teaches how to build a GitHub Copilot-native development workflow around an existing inventory management application.

The learner starts with a clean fork of:

```text
https://github.com/beck-source/inventory-management.git
```

The original repository may contain Claude-specific files. In this tutorial, those references are removed from the fork. The Claude-oriented ideas can be used only as reference material while creating GitHub Copilot-native equivalents.

The main focus is not generic vibe coding. The main focus is GitHub Copilot features:

- Agent mode
- Ask, Plan, and Agent workflows
- Repository instructions
- Path-specific instructions
- Prompt files as reusable slash commands
- Custom agents
- Agent skills
- Tools
- MCP servers
- Hooks
- Local plugin packaging
- Review and security agents
- Issue-to-PR workflow

I use the term **MCP server** instead of **map server**, because MCP, or Model Context Protocol, is the relevant Copilot and VS Code concept.

---

# Course length

Recommended format:

```text
20 videos x 5 minutes = 100 minutes
```

This keeps the tutorial between 1 and 2 hours.

---

# Final learner outcome

By the end of the tutorial, the learner will have:

1. Forked and cleaned the inventory-management repository.
2. Removed Claude-specific files and references.
3. Created GitHub Copilot repository instructions.
4. Created scoped instruction files for Vue, FastAPI, and testing.
5. Created reusable prompt files that behave like project commands.
6. Used Copilot Agent mode to implement a real feature.
7. Created specialist custom agents.
8. Converted a backend testing workflow into a Copilot skill.
9. Connected external tools through MCP.
10. Added deterministic guardrails with hooks.
11. Packaged the workflow as a local Copilot plugin.
12. Completed a capstone feature from issue to PR summary.

The capstone feature is:

```text
Low Stock & Reorder Recommendations
```

The learner will add backend and frontend support for identifying inventory items where quantity on hand is below reorder point, then display recommendations on the dashboard.

---

# Target final repository structure

By the end of the tutorial, the learner should have this structure:

```text
.github/
  copilot-instructions.md

  instructions/
    vue.instructions.md
    fastapi.instructions.md
    testing.instructions.md

  prompts/
    start-app.prompt.md
    stop-app.prompt.md
    feature-plan.prompt.md
    implement-backend.prompt.md
    implement-frontend.prompt.md
    test-and-fix.prompt.md
    optimize-codebase.prompt.md
    prepare-pr.prompt.md

  agents/
    planner.agent.md
    api-engineer.agent.md
    vue-expert.agent.md
    code-reviewer.agent.md
    security-reviewer.agent.md

  skills/
    backend-api-test/
      SKILL.md

  hooks/
    audit-log.json
    block-dangerous-commands.json

.vscode/
  mcp.json

scripts/
  copilot-audit-log.sh
  block-dangerous-command.sh

plugin.json
```

---

# Instructor preparation before recording

Do this before recording the tutorial. The learner should start from your clean fork, not from the original Claude-oriented repository.

Replace `<your-github-username>` with your GitHub username.

```bash
git clone https://github.com/<your-github-username>/inventory-management.git
cd inventory-management

git remote add upstream https://github.com/beck-source/inventory-management.git
git checkout -b tutorial/copilot-clean-start
```

Remove Claude-specific assets:

```bash
rm -rf .claude
rm -f CLAUDE.md
rm -f .mcp.json
```

Search for remaining Claude or Anthropic references:

```bash
grep -Rni "claude\|anthropic" . \
  --exclude-dir=.git \
  --exclude-dir=node_modules \
  --exclude-dir=.venv \
  --exclude-dir=dist
```

Create the Copilot folder structure:

```bash
mkdir -p .github/prompts
mkdir -p .github/agents
mkdir -p .github/instructions
mkdir -p .github/skills/backend-api-test
mkdir -p .github/hooks
mkdir -p .vscode
mkdir -p scripts
```

Commit the clean baseline:

```bash
git add -A
git commit -m "Create clean GitHub Copilot tutorial baseline"
```

---

# Claude-to-Copilot conversion map

Use the Claude files only as reference material. Do not keep Claude-specific names or paths in the final tutorial repository.

| Original Claude asset | Action | Copilot-native replacement |
|---|---|---|
| `CLAUDE.md` | Remove | `.github/copilot-instructions.md` |
| `.claude/commands/start.md` | Remove | `.github/prompts/start-app.prompt.md` |
| `.claude/commands/stop.md` | Remove | `.github/prompts/stop-app.prompt.md` |
| `.claude/commands/test.md` | Remove | `.github/prompts/test-and-fix.prompt.md` |
| `.claude/commands/optimize.md` | Remove | `.github/prompts/optimize-codebase.prompt.md` |
| `.claude/agents/vue-expert.md` | Remove | `.github/agents/vue-expert.agent.md` |
| `.claude/agents/code-reviewer.md` | Remove | `.github/agents/code-reviewer.agent.md` |
| `.claude/agents/security-auditor.md` | Remove | `.github/agents/security-reviewer.agent.md` |
| `.claude/skills/backend-api-test/SKILL.md` | Remove | `.github/skills/backend-api-test/SKILL.md` |
| `.mcp.json` | Replace | `.vscode/mcp.json` |
| `.claude/hooks/*` | Remove | `.github/hooks/*.json` and `scripts/*.sh` |

---

# Recommended video structure

Use the same structure for each five-minute video:

```text
0:00-0:30  What this video adds
0:30-1:15  GitHub Copilot feature explanation
1:15-3:45  Live repo demo
3:45-4:30  Validation step
4:30-5:00  Recap and next step
```

---

# Full tutorial outline

| Section | Video | Title | Copilot feature focus | Repo task |
|---|---:|---|---|---|
| 1 | 1 | Start from the clean fork | Repo preparation | Remove Claude references and inspect app |
| 1 | 2 | Run the baseline app | Copilot as codebase reader | Start frontend and backend |
| 1 | 3 | Ask vs Plan vs Agent mode | Copilot modes | Plan the capstone feature |
| 2 | 4 | Create repo instructions | `.github/copilot-instructions.md` | Teach Copilot the project rules |
| 2 | 5 | Add Vue instructions | Scoped instructions | Add `vue.instructions.md` |
| 2 | 6 | Add FastAPI and testing instructions | Scoped instructions | Add backend and test rules |
| 3 | 7 | Create start and stop commands | Prompt files | Add reusable app lifecycle prompts |
| 3 | 8 | Create feature planning command | Prompt files | Add `/feature-plan` |
| 3 | 9 | Create test-and-fix command | Prompt files | Add `/test-and-fix` |
| 4 | 10 | Use tool control | Agent tools | Limit tools before coding |
| 4 | 11 | Implement backend endpoint | Agent mode | Add reorder recommendations API |
| 4 | 12 | Implement frontend UI | Agent mode | Add dashboard section |
| 4 | 13 | Fix integration issues | Agent iteration | Align API and UI |
| 5 | 14 | Create Planner agent | Custom agents | Add read-only planning agent |
| 5 | 15 | Create Vue Expert agent | Custom agents | Add frontend specialist |
| 5 | 16 | Create review agents | Custom agents | Add code and security reviewers |
| 6 | 17 | Add backend testing skill | Agent Skills | Add reusable testing skill |
| 6 | 18 | Add MCP servers | MCP tools | Add GitHub and Playwright MCP |
| 6 | 19 | Add hooks and plugin | Hooks and plugin | Add guardrails and package workflow |
| 7 | 20 | Capstone issue to PR | Full Copilot workflow | Complete and review the feature |

---

# Section 1: Clean repo and Copilot mental model

## Video 1: Start from the clean fork

### Goal

Show the learner the cleaned fork and prove there are no Claude references.

### Steps to record

Check the repository status:

```bash
git status
```

Search for remaining Claude references:

```bash
grep -Rni "claude\|anthropic" . \
  --exclude-dir=.git \
  --exclude-dir=node_modules \
  --exclude-dir=.venv \
  --exclude-dir=dist
```

Show the main app structure:

```text
client/
server/
tests/
scripts/
README.md
```

### Copilot prompt

Use this in Ask mode:

```text
Inspect this repository and explain the application architecture.

Focus on:
- frontend framework
- backend framework
- data storage approach
- startup commands
- key API endpoints
- where I should make changes for a new inventory feature

Do not edit files yet.
```

### Expected result

Copilot explains the app architecture without changing files.

The learner understands:

- Where the frontend lives.
- Where the backend lives.
- Where tests live.
- Where feature changes will likely happen.

---

## Video 2: Run the baseline app

### Goal

Validate the repo before using Copilot to modify it.

### Steps to record

Try the repo start script first:

```bash
./scripts/start.sh
```

If you want to show manual startup, run the backend in one terminal:

```bash
cd server
uv venv
uv sync
uv run python main.py
```

Run the frontend in another terminal:

```bash
cd client
npm install
npm run dev
```

Open these URLs:

```text
Frontend: http://localhost:3000
Backend:  http://localhost:8001
API docs: http://localhost:8001/docs
```

### Copilot prompt

```text
Based on the repository files, explain how the frontend calls the backend.
Identify the API client file, the main FastAPI file, and the mock data loading file.
Do not edit anything.
```

### Expected result

The learner sees the app running before any AI-generated changes are made.

---

## Video 3: Ask mode vs Plan mode vs Agent mode

### Goal

Introduce the vibe coding loop without letting Copilot edit too early.

### Teaching point

Good Copilot workflow is:

```text
Ask -> Plan -> Constrain -> Implement -> Validate -> Review
```

### Steps to record

1. Use Ask mode to understand the code.
2. Use Plan mode to design the capstone feature.
3. Use Agent mode only after the plan is clear.

### Copilot prompt

Use this in Plan mode:

```text
Create a plan for a Low Stock & Reorder Recommendations feature.

The feature should:
- use the existing inventory data
- identify items where quantity_on_hand is below reorder_point
- calculate a recommended order quantity
- expose the result from the FastAPI backend
- display it on the Vue dashboard
- include backend tests
- avoid adding a database

Do not edit files yet.
```

### Expected result

The learner sees that vibe coding is not random prompting. It is structured collaboration with Copilot.

---

# Section 2: Instructions

## Video 4: Create `.github/copilot-instructions.md`

### Goal

Create repository-wide instructions so Copilot follows the project rules.

### Why this matters

Instructions tell Copilot what this repository expects, such as the app stack, coding rules, and how to handle common patterns. We need them because repeating the same guidance in every prompt is slow and easy to forget. They are helpful because they make Copilot responses more consistent, reduce extra back-and-forth, and keep the tutorial focused on the actual task instead of re-explaining project basics.

### Steps to record

Create the file:

```bash
touch .github/copilot-instructions.md
```

### Copilot prompt

```text
Create repository-wide Copilot instructions for this inventory-management app.

Use these facts:
- Frontend: Vue 3 Composition API with Vite on port 3000
- Backend: Python FastAPI on port 8001
- Data: JSON files loaded into memory, no database
- API client: client/src/api.js
- Backend entry point: server/main.py
- Mock data loader: server/mock_data.py
- Views: client/src/views/*.vue
- Do not use emojis in business UI
- Use loading and error states in Vue views
- Use unique keys in v-for, never index
- Validate dates before date operations
- Inventory supports warehouse and category filters, not month
- Update Pydantic models when changing response structures

Create concise instructions only. Do not mention Claude.
```

### Suggested final file

```md
# GitHub Copilot instructions for inventory-management

This repository contains a full-stack inventory management application.

## Stack

- Frontend: Vue 3 Composition API with Vite in `client/`.
- Backend: Python FastAPI in `server/`.
- Data: JSON files loaded into memory. Do not add a database unless explicitly requested.
- API client: `client/src/api.js`.
- Backend entry point: `server/main.py`.
- Mock data loader: `server/mock_data.py`.
- Views: `client/src/views/*.vue`.

## General rules

- Keep changes small, focused, and testable.
- Match existing project patterns before introducing new patterns.
- Do not use emojis in business UI.
- Prefer clear business language over decorative UI elements.
- Do not introduce new frameworks unless explicitly requested.

## Frontend rules

- Use Vue 3 Composition API.
- Store raw async data in `ref` values.
- Use `computed` for derived data.
- Always include loading and error states for API-driven views.
- Use stable unique keys in `v-for`; never use array index.
- Validate dates before calling date methods.
- Match existing style conventions.

## Backend rules

- Follow existing FastAPI endpoint patterns.
- Keep mock data JSON/in-memory.
- Use or update Pydantic response models when response structures change.
- Keep filters consistent with existing behavior.
- Inventory supports warehouse and category filters, not month.
- Return clear HTTP errors for missing records.

## Testing rules

- Add or update tests for changed backend behavior.
- Use pytest for backend tests.
- Validate response structure, data types, filters, and business calculations.
- Run backend tests and frontend build before completing feature work.
```

### Expected result

Copilot now has durable project context.

---

## Video 5: Add Vue-specific instructions

### Goal

Create scoped instructions that apply only to frontend files.

### Steps to record

Create the file:

```bash
touch .github/instructions/vue.instructions.md
```

### Copilot prompt

```text
Create a Vue-specific instruction file for this project.

The file should apply to:
client/src/**/*.vue
client/src/**/*.js

Rules:
- Use Vue 3 Composition API.
- Use ref for raw async data and computed for derived data.
- Always include loading and error states for API-driven views.
- Use unique stable keys in v-for, such as sku, id, month, or order_number.
- Never use index as a key.
- Never use emojis in the business UI.
- Match existing CSS patterns from client/src/App.vue.
- Do not modify backend files from a frontend-only task.
- If a backend contract is needed, state the required API shape instead of inventing server changes.

Return the complete .instructions.md file with YAML frontmatter.
```

### Suggested final file

```md
---
name: Vue Frontend Instructions
description: Vue 3 and frontend conventions for the inventory app
applyTo: "client/src/**/*.vue,client/src/**/*.js"
---

# Vue frontend conventions

- Use Vue 3 Composition API.
- Store raw API data in `ref` values.
- Use `computed` for derived values instead of methods in templates.
- Always include loading and error states for API-driven views.
- Use stable unique keys in `v-for`; never use array index.
- Validate dates before calling date methods.
- Match existing layout and style conventions in `client/src/App.vue`.
- Do not use emojis in the business UI.
- Do not modify backend files during frontend-only tasks. State required API contract changes instead.
```

### Expected result

Frontend requests now get Vue-specific guidance automatically.

---

## Video 6: Add FastAPI and testing instructions

### Goal

Create scoped instructions for backend and test files.

### Steps to record

Create the files:

```bash
touch .github/instructions/fastapi.instructions.md
touch .github/instructions/testing.instructions.md
```

### Copilot prompt

```text
Create two Copilot instruction files.

File 1: .github/instructions/fastapi.instructions.md
Apply to:
server/**/*.py

Rules:
- Follow existing FastAPI endpoint patterns.
- Keep data in JSON/in-memory mock data.
- Do not introduce a database.
- Use Pydantic response models when response shape changes.
- Keep filter behavior consistent with existing endpoints.
- Return clear HTTP errors for missing records.

File 2: .github/instructions/testing.instructions.md
Apply to:
tests/**/*.py

Rules:
- Use pytest.
- Use the existing FastAPI TestClient fixture.
- Test happy path, filters, data structure, types, and error cases.
- Keep tests independent.
- Use case-insensitive comparisons for status/category values.
- For money calculations, allow small floating point tolerance.

Return complete file contents for both files.
```

### Suggested `fastapi.instructions.md`

```md
---
name: FastAPI Backend Instructions
description: Backend conventions for FastAPI code in the inventory app
applyTo: "server/**/*.py"
---

# FastAPI backend conventions

- Follow existing FastAPI endpoint patterns.
- Keep data in JSON/in-memory mock data.
- Do not introduce a database unless explicitly requested.
- Use Pydantic response models when response shape changes.
- Keep filter behavior consistent with existing endpoints.
- Inventory filters support warehouse and category, not month.
- Return clear HTTP errors for missing records.
- Keep endpoint logic simple and testable.
- Update tests when endpoint behavior changes.
```

### Suggested `testing.instructions.md`

```md
---
name: Backend Testing Instructions
description: Testing conventions for the inventory app
applyTo: "tests/**/*.py"
---

# Testing conventions

- Use pytest.
- Use the existing FastAPI TestClient fixture.
- Test happy path first.
- Test filters and combinations of filters where relevant.
- Validate response structure and data types.
- Test error cases for missing or invalid records.
- Keep tests independent.
- Use case-insensitive comparisons for status and category values.
- For money calculations, allow small floating point tolerance.
```

### Expected checkpoint

```bash
ls .github/instructions
```

---

# Section 3: Prompt files as Copilot slash commands

## Video 7: Create `/start-app` and `/stop-app`

### Goal

Turn repeated startup and shutdown tasks into reusable prompt files.

### Steps to record

Create the files:

```bash
touch .github/prompts/start-app.prompt.md
touch .github/prompts/stop-app.prompt.md
```

### Suggested `start-app.prompt.md`

```md
---
name: start-app
description: Start the FastAPI backend and Vue frontend
agent: agent
---

Start the inventory-management application.

Steps:
1. Check whether ports 3000 and 8001 are already in use.
2. If the repo script exists, run `./scripts/start.sh`.
3. If the script fails, start manually:
   - Backend: `cd server && uv run python main.py`
   - Frontend: `cd client && npm install && npm run dev`
4. Confirm:
   - Frontend is available at http://localhost:3000
   - Backend is available at http://localhost:8001
   - API docs are available at http://localhost:8001/docs

Do not modify source files.
```

### Suggested `stop-app.prompt.md`

```md
---
name: stop-app
description: Stop local frontend and backend servers
agent: agent
---

Stop the local development servers.

Steps:
1. Find processes using ports 3000 and 8001.
2. On macOS/Linux, use `lsof -ti:3000,8001 | xargs kill 2>/dev/null || true`.
3. On Windows, explain how to use `netstat -aon | findstr :3000` and `taskkill /F /PID <pid>`.
4. Confirm the ports are no longer in use.

Do not modify source files.
```

### Demo prompt

```text
/start-app
```

### Expected result

Copilot starts or explains how to start the local app without editing files.

---

## Video 8: Create `/feature-plan`

### Goal

Create a reusable planning command before editing files.

### Steps to record

Create the file:

```bash
touch .github/prompts/feature-plan.prompt.md
```

### Suggested `feature-plan.prompt.md`

```md
---
name: feature-plan
description: Plan a feature before editing files
agent: plan
argument-hint: "<feature request>"
---

Create an implementation plan for this feature:

${input:feature request}

Rules:
- Do not edit files.
- Inspect relevant files first.
- Identify frontend files, backend files, test files, and data files that may be affected.
- Keep the app architecture unchanged: Vue 3 frontend, FastAPI backend, JSON/in-memory data.
- State API contract changes explicitly.
- Include acceptance criteria.
- Include validation commands.
- Include risks and edge cases.
```

### Demo prompt

```text
/feature-plan Add Low Stock & Reorder Recommendations to the dashboard.
```

### Expected result

Copilot returns a feature plan without editing files.

---

## Video 9: Create `/test-and-fix`

### Goal

Create a reusable validation and repair command.

### Steps to record

Create the file:

```bash
touch .github/prompts/test-and-fix.prompt.md
```

### Suggested `test-and-fix.prompt.md`

```md
---
name: test-and-fix
description: Run tests, diagnose failures, and fix them
agent: agent
---

Run validation for this repository.

Steps:
1. Inspect package and test configuration.
2. Run backend tests if available.
3. Run frontend build or tests if available.
4. Report failures clearly.
5. Fix only failures related to the current change.
6. Re-run the failing command after each fix.
7. Stop when backend tests and frontend build pass.

Preferred commands:
- Backend: `pytest tests/backend/ -v`
- Frontend: `cd client && npm run build`

If a command is unavailable, explain what is missing and suggest the smallest setup fix.
```

### Demo prompt

```text
/test-and-fix
```

### Expected result

Copilot runs validation, identifies failures, makes focused fixes, and reruns checks.

---

# Section 4: Agent mode, tools, and implementation

## Video 10: Use tool control

### Goal

Teach learners how to control which tools Copilot can use.

### Steps to record

1. Open GitHub Copilot Chat in VS Code.
2. Switch to Agent mode.
3. Open the tool picker.
4. Show read/search tools, file edit tools, terminal tools, problems tools, and MCP tools if available.
5. Explain that the available tools should match the risk level of the task.

### Copilot prompt

```text
Using only read/search tools, inspect the inventory-related backend and frontend files.
List the files that will likely change for Low Stock & Reorder Recommendations.
Do not edit files.
```

### Expected result

The learner sees that Agent mode is powerful but should be constrained intentionally.

---

## Video 11: Implement backend endpoint with Agent mode

### Goal

Create the backend part of the Low Stock & Reorder Recommendations feature.

### Steps to record

Create a backend implementation prompt file:

```bash
touch .github/prompts/implement-backend.prompt.md
```

### Suggested `implement-backend.prompt.md`

```md
---
name: implement-backend
description: Implement backend changes for an approved feature plan
agent: agent
---

Implement only the backend portion of the approved feature.

Rules:
- Read the plan and relevant backend files first.
- Modify only backend and backend test files unless explicitly needed.
- Keep data in JSON/in-memory mock data.
- Follow existing FastAPI endpoint patterns.
- Add or update Pydantic models if the response shape changes.
- Add pytest coverage under tests/backend.
- Run backend tests after changes.
- Report changed files and validation results.

Feature:
${input:feature}
```

### Demo prompt

```text
/implement-backend Add a reorder recommendations endpoint.

Acceptance criteria:
- Use existing inventory data.
- Return items where quantity_on_hand < reorder_point.
- Include sku, name, warehouse, category, quantity_on_hand, reorder_point, and recommended_order_quantity.
- recommended_order_quantity should be at least reorder_point - quantity_on_hand.
- Add backend tests.
```

### Expected validation command

```bash
pytest tests/backend/ -v
```

### Expected result

The backend exposes a reorder recommendations endpoint and backend tests are added or updated.

---

## Video 12: Implement frontend UI with Agent mode

### Goal

Create the dashboard UI for reorder recommendations.

### Steps to record

Create a frontend implementation prompt file:

```bash
touch .github/prompts/implement-frontend.prompt.md
```

### Suggested `implement-frontend.prompt.md`

```md
---
name: implement-frontend
description: Implement frontend changes for an approved feature plan
agent: agent
---

Implement only the frontend portion of the approved feature.

Rules:
- Read the relevant Vue view and API client files first.
- Follow Vue 3 Composition API.
- Add loading and error states.
- Use computed properties for derived values.
- Use stable unique keys in v-for.
- Match existing business UI styling.
- Do not use emojis.
- Do not modify backend files unless explicitly requested.
- Run frontend build after changes.

Feature:
${input:feature}
```

### Demo prompt

```text
/implement-frontend Add a dashboard section for reorder recommendations.

Acceptance criteria:
- Call the backend reorder recommendations endpoint.
- Show SKU, item name, warehouse, current quantity, reorder point, and recommended order quantity.
- Show a helpful empty state when there are no low-stock items.
- Include loading and error states.
- Match the existing dashboard styling.
```

### Expected validation command

```bash
cd client
npm run build
```

### Expected result

The Vue dashboard displays reorder recommendations from the backend.

---

## Video 13: Fix integration issues

### Goal

Show Copilot iterating across backend and frontend after real validation feedback.

### Demo prompt

```text
/test-and-fix
```

Then ask:

```text
Review the current backend and frontend changes together.
Find mismatches between the frontend API call and the backend response shape.
Fix only integration issues.
Run backend tests and frontend build again.
```

### Expected validation commands

```bash
pytest tests/backend/ -v
cd client && npm run build
```

### Expected result

The learner sees Copilot diagnose mismatches, patch focused issues, and rerun checks.

---

# Section 5: Custom agents

## Understanding agent tools

Custom agents can be limited to specific tools through the `tools:` array in the YAML frontmatter. This helps you control what the agent can do, keeps planning agents read-only, and makes each agent fit a clear job.

Tool types you will see in custom agents:

- Built-in aliases:
  - `read`: reads files and notebooks. Use it when the agent needs context before deciding what to do.
  - `search`: searches files or text in the codebase. Use it when the agent needs to locate relevant code or docs.
  - `edit`: modifies files. Use it only for agents that are allowed to make changes.
  - `execute`: runs shell commands such as bash or PowerShell. Use it when the agent needs to build, test, inspect output, or run scripts.
  - `agent`: invokes another custom agent. Use it when you want delegation to a specialized agent.
  - `web`: fetches URLs and searches the web. The docs say this is currently not applicable for the cloud agent.
  - `todo`: creates and manages structured task lists. The docs say this is currently not applicable for the cloud agent, though it is supported in VS Code.
- Out-of-the-box MCP tools:
  - `github/*`: exposes GitHub's read-only tools. Use it when the agent needs repository-hosted GitHub data.
  - `playwright/*`: exposes Playwright tools. Use it when the agent needs browser automation, with localhost access only.
- Custom MCP tools:
  - `server-name/tool-name`: enables a specific tool from a custom MCP server.
  - `server-name/*`: enables all tools from that MCP server.

Tool selection rules:

- Omit `tools` or use `tools: ["*"]` to enable all available tools.
- Provide a specific list, such as `tools: ["read", "search", "edit"]`, to enable only those tools.
- Use `tools: []` to disable all tools.
- Unrecognized tool names are ignored, which lets product-specific tool names appear safely in a profile.

The rest of this section shows how those tools change the behavior of different agents, from read-only planners to editing specialists.

## Video 14: Create a read-only Planner agent

### Goal

Create a custom agent that plans without editing files.

### Steps to record

Create the file:

```bash
touch .github/agents/planner.agent.md
```

### Suggested `planner.agent.md`

```md
---
name: planner
description: Read-only planning agent for feature design and task breakdown
tools: ['search/codebase', 'vscode/askQuestions']
---

# Planner Agent

You create implementation plans only.

Rules:
- Do not edit files.
- Do not run destructive commands.
- Inspect relevant files before planning.
- Identify frontend, backend, test, and data impacts.
- Produce acceptance criteria.
- Produce validation commands.
- Call out risks and assumptions.
- Keep plans short and actionable.

For this project:
- Frontend is Vue 3 + Vite in `client/`.
- Backend is FastAPI in `server/`.
- Data is JSON/in-memory mock data.
- Inventory filters support warehouse and category, not month.
```

### Demo prompt

```text
Using the planner agent, plan a small improvement to the reorder recommendations feature.
Do not edit files.
```

### Expected result

The planner agent produces a focused plan and does not modify files.

---

## Video 15: Create `vue-expert.agent.md`

### Goal

Create a frontend specialist agent.

### Steps to record

Create the file:

```bash
touch .github/agents/vue-expert.agent.md
```

### Suggested `vue-expert.agent.md`

```md
---
name: vue-expert
description: Vue 3 frontend specialist for the inventory-management app
tools: ['search/codebase', 'editFiles', 'runCommands', 'problems']
---

# Vue Expert Agent

You are a Vue 3 frontend specialist for this inventory-management app.

Scope:
- You may edit `client/src/**/*.vue`.
- You may edit `client/src/**/*.js`.
- You may edit `client/src/App.vue`.
- Do not edit `server/` files unless the user explicitly asks.
- Do not change API contracts silently. State required backend changes clearly.

Frontend rules:
- Use Vue 3 Composition API.
- Use `ref` for raw API data.
- Use `computed` for derived values.
- Use `onMounted` or watchers consistently with existing views.
- Always include loading and error states.
- Use stable unique keys in `v-for`; never use array index.
- Validate dates before date methods.
- Match existing styles.
- Do not use emojis in the UI.

Validation:
- Run `cd client && npm run build` after meaningful changes.
- If Playwright MCP is available, validate the page in the browser.
```

### Demo prompt

```text
Using the vue-expert agent, review the dashboard reorder recommendations UI.
Suggest any frontend-only improvements.
Do not edit backend files.
```

### Expected result

The custom agent behaves like a focused frontend specialist instead of a generic assistant.

---

## Video 16: Create reviewer and security agents

### Goal

Create specialist agents for review and security checks.

### Steps to record

Create the files:

```bash
touch .github/agents/code-reviewer.agent.md
touch .github/agents/security-reviewer.agent.md
```

### Suggested `code-reviewer.agent.md`

```md
---
name: code-reviewer
description: Reviews changed files for correctness, maintainability, Vue/FastAPI patterns, and project conventions
tools: ['search/codebase', 'runCommands']
---

# Code Reviewer Agent

Review recently changed files only.

Review priorities:
1. Correctness and edge cases.
2. Vue 3 Composition API usage.
3. FastAPI and Pydantic consistency.
4. Project-specific filter and data-flow rules.
5. Maintainability and duplication.
6. Performance issues such as unnecessary recomputation.

Project-specific checks:
- Use stable keys in `v-for`; never use index.
- Validate dates before date operations.
- Inventory supports warehouse/category filters, not month.
- Pydantic models must match JSON and response structures.
- Vue API calls should go through `client/src/api.js`.
- Backend data should remain JSON/in-memory.

Output format:
- Files reviewed
- Critical issues
- Recommended improvements
- Good patterns
- Final action: Approve / Request changes
```

### Suggested `security-reviewer.agent.md`

```md
---
name: security-reviewer
description: Fast security review for changed files only
tools: ['search/codebase', 'runCommands']
---

# Security Reviewer Agent

Review changed files only.

Priority checks:
1. Hardcoded secrets, API keys, tokens, passwords, private keys.
2. Vue XSS risks such as `v-html` or `innerHTML`.
3. New API endpoints with missing input validation.
4. Unsafe shell commands.
5. Accidental exposure of local environment values.

Commands you may use:
- `git diff --name-only`
- `git diff`
- `grep -Rni "api_key\\|API_KEY\\|secret\\|password\\|token\\|BEGIN.*PRIVATE" <changed files>`
- `grep -Rni "v-html\\|innerHTML" <changed files>`

Report only concrete, exploitable issues.
Do not perform a full-codebase audit unless asked.
```

### Demo prompt for code reviewer

```text
Using the code-reviewer agent, review the current changed files.
Focus on correctness, maintainability, and project conventions.
```

### Demo prompt for security reviewer

```text
Using the security-reviewer agent, review the current changed files for hardcoded secrets, XSS risks, unsafe commands, and validation issues.
```

### Expected result

The learner sees a realistic review workflow using Copilot custom agents.

---

# Section 6: Skills, MCP, hooks, and plugin

## Video 17: Add backend API testing skill

### Goal

Create a reusable skill for backend API test work.

### Steps to record

Create the file:

```bash
touch .github/skills/backend-api-test/SKILL.md
```

### Suggested `SKILL.md`

```md
---
name: backend-api-test
description: Guidelines for writing backend API tests using pytest and FastAPI TestClient.
---

# Backend API Testing Skill

Use this skill when writing or modifying tests under `tests/backend`.

## Test location

Place backend API tests in:

```text
tests/backend/
```

## Required patterns

- Use pytest.
- Use the existing `client` fixture for FastAPI TestClient requests.
- Test happy path first.
- Test each query parameter separately.
- Test combinations of filters when relevant.
- Validate response structure.
- Validate data types and numeric ranges.
- Test business calculations.
- Test 404 or error cases for missing resources.
- Keep tests independent.

## Common checks

Inventory:
- `quantity_on_hand` is an integer.
- `reorder_point` is an integer.
- Numeric values are non-negative.
- Warehouse and category filters behave correctly.

Orders:
- Status values are valid.
- Date strings are valid before date operations.
- Totals are reasonable and allow small floating point tolerance.

Dashboard:
- Aggregated values should match raw endpoint data where possible.

## Commands

```bash
pytest tests/backend/ -v
pytest tests/backend/test_inventory.py -v
pytest tests/backend/ --cov=server
```

## Reminder

When the API response shape changes, update:
- Pydantic models
- endpoint logic
- backend tests
- frontend API expectations if needed
```

### Demo prompt

```text
Use the backend-api-test skill to add tests for the reorder recommendations endpoint.
```

### Expected result

Copilot uses the skill as task-specific knowledge when working on backend tests.

---

## Video 18: Add MCP servers

### Goal

Connect external tools to Copilot using MCP.

### Steps to record

Create the file:

```bash
touch .vscode/mcp.json
```

### Suggested `.vscode/mcp.json`

```json
{
  "servers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp"
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@microsoft/mcp-server-playwright"]
    }
  }
}
```

### Important note

Do not hardcode secrets in MCP configuration. Use environment variables, VS Code inputs, or secure local configuration for tokens.

### Demo prompt

```text
Use the Playwright MCP tools to open http://localhost:3000.
Verify that the dashboard loads.
Then check whether the reorder recommendations section appears.
Do not edit files.
```

### Expected result

Copilot uses browser automation tools to validate the running app.

---

## Video 19: Add hooks and package as plugin

### Goal

Add deterministic guardrails and package the workflow.

### Part A: Add a dangerous-command hook

Create files:

```bash
touch .github/hooks/block-dangerous-commands.json
touch scripts/block-dangerous-command.sh
chmod +x scripts/block-dangerous-command.sh
```

### Suggested `.github/hooks/block-dangerous-commands.json`

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "./scripts/block-dangerous-command.sh",
        "timeout": 10
      }
    ]
  }
}
```

### Suggested `scripts/block-dangerous-command.sh`

```bash
#!/usr/bin/env bash

input="$(cat)"

if echo "$input" | grep -E "rm -rf /|git reset --hard|git clean -fd|DROP TABLE|DELETE FROM" >/dev/null; then
  echo "Blocked potentially destructive command." >&2
  exit 2
fi

exit 0
```

### Part B: Add an audit log hook

Create files:

```bash
touch .github/hooks/audit-log.json
touch scripts/copilot-audit-log.sh
chmod +x scripts/copilot-audit-log.sh
```

### Suggested `.github/hooks/audit-log.json`

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "./scripts/copilot-audit-log.sh",
        "timeout": 10
      }
    ]
  }
}
```

### Suggested `scripts/copilot-audit-log.sh`

```bash
#!/usr/bin/env bash

mkdir -p .copilot-audit
cat >> .copilot-audit/tool-use.log
printf '\n---\n' >> .copilot-audit/tool-use.log
exit 0
```

Add the audit folder to `.gitignore`:

```bash
printf '\n.copilot-audit/\n' >> .gitignore
```

### Part C: Package as plugin

Create the plugin manifest:

```bash
touch plugin.json
```

### Suggested `plugin.json`

```json
{
  "name": "inventory-copilot-workflow",
  "description": "GitHub Copilot workflow customizations for the inventory-management tutorial",
  "version": "1.0.0",
  "author": {
    "name": "Tutorial Author"
  },
  "skills": ".github/skills",
  "agents": ".github/agents",
  "hooks": ".github/hooks/block-dangerous-commands.json",
  "mcpServers": ".vscode/mcp.json"
}
```

### Demo prompt

```text
Explain what this local plugin packages for the inventory-management workflow.
Do not edit files.
```

### Expected result

The learner understands how prompts, agents, skills, hooks, and MCP config can be bundled as a reusable workflow.

---

# Section 7: Capstone

## Video 20: Full issue-to-PR workflow

### Goal

Use the complete GitHub Copilot workflow to finish the capstone feature.

### Capstone issue text

Use this as the issue or task description:

```text
Add Low Stock & Reorder Recommendations to the inventory dashboard.

Acceptance criteria:
- Backend exposes reorder recommendation data.
- Recommendation is based on existing inventory data.
- Items qualify when quantity_on_hand < reorder_point.
- Frontend displays recommendations on the dashboard.
- UI includes loading, error, and empty states.
- Backend tests pass.
- Frontend build passes.
- Browser validation confirms the UI renders.
- Code reviewer and security reviewer agents approve or list fixes.
```

### Complete workflow

Run the workflow in this order:

```text
1. /feature-plan Add Low Stock & Reorder Recommendations
2. Switch to planner agent and confirm the plan.
3. /implement-backend Add the backend endpoint and tests.
4. /implement-frontend Add the dashboard UI.
5. /test-and-fix
6. Use Playwright MCP to validate the browser.
7. Switch to code-reviewer agent.
8. Switch to security-reviewer agent.
9. Fix issues.
10. Generate a PR summary.
```

### Create final PR prompt

Create the file:

```bash
touch .github/prompts/prepare-pr.prompt.md
```

### Suggested `prepare-pr.prompt.md`

```md
---
name: prepare-pr
description: Summarize current changes for a pull request
agent: agent
---

Prepare a pull request summary for the current branch.

Steps:
1. Run `git status`.
2. Run `git diff --stat`.
3. Review changed files.
4. Summarize the feature in plain English.
5. List validation commands that were run.
6. List risks or follow-up work.
7. Do not commit or push unless explicitly asked.

Output format:
## Summary
## Changes
## Validation
## Risks / Follow-up
```

### Demo prompt

```text
/prepare-pr
```

### Expected final result

The learner has completed a feature and created a repeatable Copilot workflow system around the repository.

---

# Optional 60-minute cut

If you want a shorter version, use 12 videos:

```text
1. Start from the clean fork
2. Run the baseline app
3. Ask vs Plan vs Agent mode
4. Create repo instructions
5. Add Vue-specific instructions
6. Create prompt files for planning and testing
7. Use tool control
8. Implement backend endpoint
9. Implement frontend UI
10. Create custom agents
11. Add skill and MCP
12. Capstone issue to PR
```

This shorter version keeps the essential flow:

```text
Repo -> Copilot modes -> Instructions -> Prompt files -> Agent implementation -> Custom agents -> Skill/MCP -> Capstone
```

---

# Recommended section names for course platform

Use these as learner-facing module names:

```text
1. Start Clean: Prepare the Inventory App for Copilot
2. Teach Copilot the Project with Instructions
3. Turn Repeated Workflows into Prompt Commands
4. Use Agent Mode with Tools Safely
5. Build a Feature with Backend and Frontend Agents
6. Add Specialist Agents for Planning, Vue, Review, and Security
7. Add Skills for Repeatable Testing
8. Connect External Tools with MCP
9. Add Hooks and Package the Workflow as a Plugin
10. Capstone: Issue to PR with GitHub Copilot
```

---

# Final teaching emphasis

The tutorial should repeatedly reinforce this idea:

```text
Vibe coding is the interaction style.
GitHub Copilot customization is the professional workflow.
```

The learner should finish with more than one generated feature. They should finish with a reusable Copilot development system:

- Instructions provide durable project context.
- Prompt files provide repeatable commands.
- Custom agents provide specialist roles.
- Skills provide reusable task knowledge.
- Tools and MCP provide controlled external capabilities.
- Hooks provide deterministic guardrails.
- Plugins package the workflow for reuse.