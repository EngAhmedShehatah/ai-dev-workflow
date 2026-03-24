# Skill Creator Prompt — Unit Testing Skill

## How to Use This File
Open Claude Code in your project root and run:

  /skill-creator

Then paste the prompt below exactly as written.
The skill-creator will analyze your codebase and ask you clarifying questions.
Answer them based on your specific project. The more detail you give, the better the skill.

---

## Prompt to Paste

Create a unit testing skill for this project. Before generating the skill, please:

1. Scan the project structure to understand how test files are organized
2. Read a sample of existing test files to understand current testing patterns
3. Identify the testing frameworks and libraries already in use
4. Identify how mocks, stubs, and spies are currently used
5. Identify how test data and fixtures are currently managed
6. Identify any existing test coverage thresholds or requirements
7. Identify naming conventions for test files and test cases

Then ask me any clarifying questions about:
- Testing patterns you found but are unsure about
- Anything that appears inconsistent in the existing test files
- Coverage expectations I have that are not yet visible in the codebase
- Any testing rules or anti-patterns the team has agreed on

After I answer, generate a unit testing skill that captures:
- Where test files belong and how they are named
- Which testing framework and assertion library to use
- How to structure a test file — describe blocks, it blocks, setup and teardown
- How to mock external dependencies, services, and modules
- How to handle async tests
- Coverage expectations per file type
- What must always be tested and what should never be tested
- Any project-specific testing patterns or conventions

The skill should be specific enough that any developer — human or AI —
following it would produce tests indistinguishable from the existing test suite.
