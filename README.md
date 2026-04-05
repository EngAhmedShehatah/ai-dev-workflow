# AI Dev Workflow

A complete, professional AI-powered development workflow for full-stack developers using Claude Code.

Initially Built for: **Angular + TypeScript  + Node.js/Express + Salesforce (Apex, LWC, Agentforce)**

---

## What This Is

This repository contains the files you need to set up a structured, agent-driven development workflow using Claude Code. It combines:

- **spec-kit** — for structured planning (specify → clarify → plan → tasks → implement)
- **Skills** — project-specific knowledge files that guide how Claude works
- **Agents** — specialized workers that handle implementation, testing, and documentation
- **MCPs & Plugins** — tools that give Claude hands to interact with GitHub, Salesforce, browsers, and more

The result is a workflow where you stay in control at every checkpoint, nothing gets implemented without a reviewed plan, and every piece of work is tested and documented consistently.

---

## Repository Structure

```
ai-dev-workflow/
├── README.md                          ← This file
├── 01-basic-setup/
│   ├── setup-instructions.md          ← Start here
│   ├── agents/
│   │   ├── implementer.md             ← Implements tasks from tasks.md
│   │   ├── unit-tester.md             ← Writes unit tests after each task
│   │   ├── e2e-tester.md              ← Writes e2e tests after all tasks
│   │   ├── api-documenter.md          ← Documents REST API endpoints
│   │   └── planner.md                 ← Ad-hoc planning outside spec-kit
│   ├── skills/
│   │   └── planning.md                ← Generic planning skill (reuse everywhere)
│   └── skill-creator-prompts/
│       ├── implementation.md          ← Paste into skill-creator for impl skill
│       ├── unit-testing.md            ← Paste into skill-creator for test skill
│       ├── e2e-testing.md             ← Paste into skill-creator for e2e skill
│       └── api-documentation.md      ← Paste into skill-creator for docs skill
└── 02-custom-commands/
    ├── jira.md                        ← /jira command: fetch Jira ticket with all context
    └── git.md                         ← /ship command: branch, commit, push & PR
```

---

## Quick Start

Read [`setup-instructions.md`](./01-basic-setup/setup-instructions.md) for the complete step-by-step setup guide.

The short version:

```
1.  specify init --here --ai claude     → install spec-kit
2.  /init                               → create CLAUDE.md
3.  /speckit.constitution               → create constitution.md
4.  Copy 01-basic-setup/agents/ → .claude/agents/
5.  Install skill-creator plugin
6.  Run skill-creator × 4              → generate project-specific skills
7.  Copy 01-basic-setup/skills/planning.md → .claude/skills/
8.  Modify .specify/templates to remove branch auto-creation
9.  Modify implement.md to delegate to agents
10. Install plugins and MCPs
11. Copy 02-custom-commands/*.md → ~/.claude/commands/   (optional)
```

---

## The Daily Workflow

For every feature, bug, or task:

```
Create git branch manually
        ↓
/speckit.specify       → spec.md (what & why)
        ↓
/speckit.clarify       → refined spec.md
        ↓
/speckit.checklist     → validated spec.md
        ↓
/speckit.plan          → plan.md (how, technically)
        ↓
/speckit.tasks         → tasks.md (step-by-step)
        ↓
/speckit.analyze       → quality gate
        ↓
Review manually        ← never skip this
        ↓
/speckit.implement     → agents take over
        ↓
code-simplifier        → cleanup pass
        ↓
Final review → merge
```

---

## Key Concepts

| Concept | What it is |
|---|---|
| **Skill** | Reusable instructions auto-loaded by relevance |
| **Agent** | Isolated Claude worker with its own context |
| **MCP** | Tool giving Claude access to external systems |
| **Plugin** | Bundled package of skills + agents + MCPs |
| **CLAUDE.md** | Always-on project context (created by `/init`) |
| **constitution.md** | Spec-kit's always-on project DNA |

---

## Tools Stack

**Anthropic Official Plugins**
- `feature-dev` — structured feature workflow
- `frontend-design` — intentional UI design
- `code-review` — structured code review
- `security-guidance` — security issue detection
- `commit-commands` — structured commit messages

**Partner MCPs**
- GitHub MCP — repo, issues, PRs
- Playwright MCP — browser automation and testing
- Figma MCP — design-to-code (when working with designers)
- Sentry MCP — production error context

**Salesforce Official**
- `@salesforce/mcp` — Apex, LWC, metadata, org management

**Community**
- Context7 — live library documentation

---

## Related Articles

- [Basic Setup — AI Dev Workflow](https://medium.com/@engahmedshehatah/basic-setup-ai-dev-workflow-33724218fc2a)
- [Custom Commands — Claude Code](link here once published)

---

## Author

**Ahmed Shehatah** — Senior Angular Developer  
[GitHub](https://github.com/EngAhmedShehatah)
