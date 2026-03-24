# Skill Creator Prompt — E2E Testing Skill

## How to Use This File
Open Claude Code in your project root and run:

  /skill-creator

Then paste the prompt below exactly as written.
The skill-creator will analyze your codebase and ask you clarifying questions.
Answer them based on your specific project. The more detail you give, the better the skill.

---

## Prompt to Paste

Create an end-to-end testing skill for this project. Before generating the skill, please:

1. Scan the project structure to understand how E2E test files are organized
2. Read a sample of existing E2E test files to understand current testing patterns
3. Identify the E2E testing framework and libraries already in use
4. Identify how test environments are configured and managed
5. Identify how test data is seeded, managed, and cleaned up
6. Identify how authentication and session management is handled in tests
7. Identify how selectors and element targeting are currently approached
8. Identify any existing conventions for test organization and naming

Then ask me any clarifying questions about:
- E2E patterns you found but are unsure about
- Anything that appears inconsistent in the existing E2E test files
- Environment setup or teardown requirements I have
- Any E2E rules or anti-patterns the team has agreed on
- Which user journeys are considered critical and must always be covered

After I answer, generate an E2E testing skill that captures:
- Where E2E test files belong and how they are named
- Which framework and libraries to use
- How to structure test files and group related journeys
- How to handle authentication and protected routes in tests
- How to manage and isolate test data
- How to target elements reliably without brittle selectors
- How to handle async operations, animations, and loading states
- Which user journeys must always have E2E coverage
- Any project-specific E2E patterns or conventions

The skill should be specific enough that any developer — human or AI —
following it would produce E2E tests indistinguishable from the existing test suite.
