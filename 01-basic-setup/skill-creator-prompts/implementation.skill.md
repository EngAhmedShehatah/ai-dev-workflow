# Skill Creator Prompt — Implementation Skill

## How to Use This File
Open Claude Code in your project root and run:

  /skill-creator

Then paste the prompt below exactly as written.
The skill-creator will analyze your codebase and ask you clarifying questions.
Answer them based on your specific project. The more detail you give, the better the skill.

---

## Prompt to Paste

Create an implementation skill for this project. Before generating the skill, please:

1. Scan the project structure to understand the folder organization
2. Read a sample of existing files to understand current coding patterns
3. Identify the frameworks, libraries, and tools already in use
4. Identify naming conventions already being followed
5. Identify how errors are currently handled
6. Identify how state is managed
7. Identify how services and dependencies are injected
8. Identify any existing linting or formatting rules

Then ask me any clarifying questions about:
- Patterns or conventions you found but are unsure about
- Anything that appears inconsistent in the existing code
- Preferences I have that are not yet visible in the codebase

After I answer, generate an implementation skill that captures:
- Folder structure and where new files belong
- Naming conventions for files, classes, functions, and variables
- Component and service patterns
- Error handling approach
- State management approach
- Dependency injection approach
- Code style and formatting rules
- Anything else critical to writing consistent code in this project

The skill should be specific enough that any developer — human or AI —
following it would produce code indistinguishable from the existing codebase.
