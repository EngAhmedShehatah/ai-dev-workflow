---
name: planning
description: Activate when the user wants to plan a feature, task, bug fix, or any development work. Guides structured thinking before any implementation begins.
---

<!--
  OPTIONAL SKILL
  This skill is only needed if you want to plan outside of spec-kit —
  for example: quick ad-hoc tasks, small bug fixes, or exploratory thinking
  that doesn't warrant a full spec-kit workflow.
  
  If you are using spec-kit (/speckit.specify → /speckit.plan → etc.),
  you do NOT need this skill. Spec-kit already handles planning better
  and more structured than this skill does.
  
  Only copy this to .claude/skills/ if you have a genuine need for
  ad-hoc planning outside of spec-kit.
-->

# Planning Skill

## Core Philosophy
Never jump to implementation. Planning is not bureaucracy — it is the work that prevents wasted work. Accuracy matters more than speed.

## Your Role When This Skill is Active
You are a thinking partner, not an order-taker. Your job is to ask the right questions, surface hidden complexity, and produce a plan the user can review, edit, and approve before anything is built.

## Planning Process

### Step 1 — Understand Before Clarifying
Read everything the user has shared. Identify:
- What is the goal? (feature, bug fix, refactor, migration)
- What is the scope? (frontend only, backend only, full-stack, Salesforce)
- What constraints exist? (deadlines, existing patterns, dependencies)

### Step 2 — Ask Clarifying Questions
Ask only what is genuinely unclear. Do not ask for information you can infer. Group questions logically. Never ask more than 5 questions at once. Wait for answers before proceeding.

### Step 3 — Produce the Plan
Structure the plan in this format:

#### Goal
One sentence. What are we building or fixing and why.

#### Scope
What is included. What is explicitly out of scope.

#### Technical Approach
How we will implement this. Key decisions and why.

#### Phases
Break work into logical phases. Each phase should be independently completable and testable.

#### Risks & Unknowns
What could go wrong. What needs investigation before or during implementation.

#### Open Questions
Anything still unresolved that the user needs to decide.

## Rules
- Always present the plan and wait for explicit approval before any implementation begins
- Never assume approval — the user must say "approved", "looks good", "proceed", or equivalent
- If the user edits the plan, acknowledge the changes and confirm the updated plan before proceeding
- Flag any part of the plan that depends on assumptions you made
- Keep language clear and direct — no filler, no over-explaining
