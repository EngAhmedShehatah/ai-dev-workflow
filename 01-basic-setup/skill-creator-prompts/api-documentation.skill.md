# Skill Creator Prompt — API Documentation Skill

## How to Use This File
Open Claude Code in your project root and run:

  /skill-creator

Then paste the prompt below exactly as written.
The skill-creator will analyze your codebase and ask you clarifying questions.
Answer them based on your specific project. The more detail you give, the better the skill.

---

## Prompt to Paste

Create an API documentation skill for this project. Before generating the skill, please:

1. Scan the project structure to understand how API endpoints are organized
2. Read a sample of existing endpoint files to understand current patterns
3. Identify the documentation format and tooling already in use
4. Identify how existing documentation files are structured and where they live
5. Identify how request and response schemas are currently defined
6. Identify how authentication and authorization are documented
7. Identify how error responses are structured and documented
8. Identify any existing conventions for example payloads and mock data

Then ask me any clarifying questions about:
- Documentation patterns you found but are unsure about
- Anything that appears inconsistent in the existing documentation
- Documentation tooling or format preferences not yet visible in the project
- Any documentation rules or standards the team has agreed on
- How detailed example payloads should be
- Whether mock data for interactive testing should be included

After I answer, generate an API documentation skill that captures:
- Where documentation files belong and how they are named
- Which documentation format and tooling to use
- How to structure documentation for each endpoint
- What must be documented per endpoint — method, path, parameters, headers, body, responses, errors
- How to write example request payloads including mock data for interactive testing
- How to write example response payloads for all possible status codes
- How to document authentication requirements per endpoint
- How to keep documentation in sync with implementation
- Any project-specific documentation patterns or conventions

The skill should be specific enough that any developer — human or AI —
following it would produce documentation indistinguishable from the existing project documentation.
