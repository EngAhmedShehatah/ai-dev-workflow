# Setup Instructions

Step-by-step guide for setting up the AI Dev Workflow in any project.
Follow this file exactly, in order, every time you initialize a new project.

---

## Prerequisites

Make sure the following are installed globally before starting:

- [ ] Node.js 18+
- [ ] Claude Code CLI (`npm install -g @anthropic-ai/claude-code`)
- [ ] Salesforce CLI (`npm install -g @salesforce/cli`) — only for Salesforce projects
- [ ] Python 3.11+ — required by spec-kit
- [ ] uv (`pip install uv`) — required by spec-kit
- [ ] Git

---

## Phase 1 — Initialize the Project Foundations

### Step 1 — Install spec-kit
Open your terminal, navigate to your project root, and run:
```bash
specify init --here --ai claude
```
This creates the `.specify/` folder with all spec-kit templates inside your project.

### Step 2 — Initialize Claude Code
Inside Claude Code, run:
```
/init
```
This creates `CLAUDE.md` at your project root. Fill it in with your project's always-on context — tech stack, folder structure, team conventions, anything Claude should always know.

### Step 3 — Create the spec-kit Constitution
Inside Claude Code, run:
```
/speckit.constitution
```
Answer all questions thoroughly. This creates `constitution.md` which every future spec and plan will reference. Take your time here — the better the constitution, the better every plan that follows.

---

## Phase 2 — Set Up Claude Code Folder Structure

### Step 4 — Create the .claude folders
In your terminal, run:
```bash
mkdir -p .claude/agents
mkdir -p .claude/skills
```

### Step 5 — Copy Agent Files
Copy all agent files from this repository into `.claude/agents/`:
```
.claude/agents/planner.md
.claude/agents/implementer.md
.claude/agents/unit-tester.md
.claude/agents/e2e-tester.md
.claude/agents/api-documenter.md
```
These are generic — copy them as-is. Do not modify them per project.

### Step 6 — Copy Planning Skill (Optional)
Only do this step if you need ad-hoc planning outside of spec-kit.
Copy `skills/planning.md` from this repository into `.claude/skills/`:
```
.claude/skills/planning.md
```

---

## Phase 3 — Generate Project-Specific Skills

These skills must be generated inside your actual project — do not copy them from another project.

### Step 7 — Install the Skill Creator Plugin
Inside Claude Code, run:
```
/plugin install skill-creator@claude-plugins-official
```

### Step 8 — Generate the Implementation Skill
Inside Claude Code, run:
```
/skill-creator
```
Then paste the full contents of `skill-creator-prompts/implementation.md` from this repository.
Answer all clarifying questions the skill-creator asks.
The skill will be saved automatically to `.claude/skills/implementation.md`.

### Step 9 — Generate the Unit Testing Skill
Inside Claude Code, run:
```
/skill-creator
```
Then paste the full contents of `skill-creator-prompts/unit-testing.md` from this repository.
Answer all clarifying questions the skill-creator asks.
The skill will be saved automatically to `.claude/skills/unit-testing.md`.

### Step 10 — Generate the E2E Testing Skill
Inside Claude Code, run:
```
/skill-creator
```
Then paste the full contents of `skill-creator-prompts/e2e-testing.md` from this repository.
Answer all clarifying questions the skill-creator asks.
The skill will be saved automatically to `.claude/skills/e2e-testing.md`.

### Step 11 — Generate the API Documentation Skill
Inside Claude Code, run:
```
/skill-creator
```
Then paste the full contents of `skill-creator-prompts/api-documentation.md` from this repository.
Answer all clarifying questions the skill-creator asks.
The skill will be saved automatically to `.claude/skills/api-documentation.md`.

---

## Phase 4 — Modify Spec-kit Templates

These modifications are done once per project and prevent spec-kit from interfering with your git workflow.

### Step 12 — Disable Auto Branch Creation
Open this file in your editor:
```
.specify/templates/commands/specify.md
```
Find any instruction mentioning `git checkout`, `git branch`, or branch creation.
Replace it with:
```
Do NOT create a git branch. The user manages all git branching manually.
```
Save the file.

### Step 13 — Wire Implement Template to Your Agents
Open this file in your editor:
```
.specify/templates/commands/implement.md
```
Add the following delegation instructions:
```
- For each task in tasks.md, invoke the implementer agent
- After each task implementation, invoke the unit-tester agent
- After all tasks are complete, invoke the e2e-tester agent
- For any new endpoints, invoke the api-documenter agent
- Each agent will use its respective skills automatically
```
Save the file.

---

## Phase 5 — Install MCPs and Plugins

### Step 14 — Install Anthropic Official Plugins
Inside Claude Code, run each of the following:
```
/plugin install feature-dev@claude-plugins-official
/plugin install frontend-design@claude-plugins-official
/plugin install code-review@claude-plugins-official
/plugin install security-guidance@claude-plugins-official
/plugin install commit-commands@claude-plugins-official
```

### Step 15 — Install Context7
Follow the installation instructions at:
```
https://github.com/upstash/context7
```

### Step 16 — Install GitHub MCP
Follow the installation instructions at:
```
https://github.com/github/github-mcp-server
```

### Step 17 — Install Playwright MCP (if applicable)
Only if your project uses Playwright for E2E testing.
Follow the installation instructions at:
```
https://github.com/microsoft/playwright-mcp
```

### Step 18 — Install Figma MCP (if applicable)
Only if your project works with Figma designs.
Follow the installation instructions at:
```
https://github.com/figma/figma-developer-mcp
```

### Step 19 — Install Sentry MCP (if applicable)
Only if your project uses Sentry for error tracking.
Follow the installation instructions at:
```
https://github.com/getsentry/sentry-mcp
```

### Step 20 — Install Salesforce DX MCP (Salesforce projects only)
Add the following to your `.mcp.json` at the project root:
```json
{
  "mcpServers": {
    "Salesforce DX": {
      "command": "npx",
      "args": [
        "-y", "@salesforce/mcp",
        "--orgs", "YOUR_ORG_ALIAS",
        "--toolsets", "orgs,metadata,lwc-experts,apex"
      ]
    }
  }
}
```
Replace `YOUR_ORG_ALIAS` with your authenticated Salesforce org alias.

---

## Phase 6 — Verify Everything is in Place

Before starting your first task, confirm your project structure looks like this:
```
your-project/
├── .claude/
│   ├── agents/
│   │   ├── planner.md
│   │   ├── implementer.md
│   │   ├── unit-tester.md
│   │   ├── e2e-tester.md
│   │   └── api-documenter.md
│   └── skills/
│       ├── implementation.md       ← generated by skill-creator
│       ├── unit-testing.md         ← generated by skill-creator
│       ├── e2e-testing.md          ← generated by skill-creator
│       ├── api-documentation.md    ← generated by skill-creator
│       └── planning.md             ← optional, only if needed
├── .specify/
│   └── templates/
│       └── commands/
│           ├── specify.md          ← modified (no branch creation)
│           └── implement.md        ← modified (delegates to agents)
├── .mcp.json                       ← MCP configurations
├── CLAUDE.md                       ← Claude Code foundation
└── constitution.md                 ← spec-kit foundation
```

If everything is in place — you are ready to start your first task.

---

## You Are Ready

From this point, every feature, bug fix, or task follows this workflow:
```
You create your git branch manually
        ↓
/speckit.specify       → spec.md
        ↓
/speckit.clarify       → refined spec.md
        ↓
/speckit.checklist     → validated spec.md
        ↓
/speckit.plan          → plan.md
        ↓
/speckit.tasks         → tasks.md
        ↓
/speckit.analyze       → findings table → fix issues
        ↓
YOU REVIEW MANUALLY    → never skip this
        ↓
/speckit.implement     → agents take over
        ↓
code-simplifier        → after tests are green
        ↓
Your final review → merge
```
