---
description: Fetch a Jira ticket with all fields and comments. Accepts a ticket ID (e.g. PROJ-123) or a full Jira URL.
args: ticketIdOrUrl
---

# /jira — Fetch Jira Ticket

You are fetching a Jira ticket and presenting a full summary to the user.

## Input parsing

`$ARGUMENTS` is required. If empty or missing, respond with:
> Usage: `/jira PROJ-123` or `/jira https://yourcompany.atlassian.net/browse/PROJ-123`

Do not prompt or ask — just show the usage and stop.

The argument can be:
- A **ticket ID** like `PROJ-123`
- A **full URL** like `https://yourcompany.atlassian.net/browse/PROJ-123`

Extract the ticket key (e.g. `PROJ-123`) from whatever format is provided.

## Auth Preflight

Call `getAccessibleAtlassianResources` first. If not authenticated, stop and tell the user:
> "Atlassian MCP is not authenticated. Run `/mcp` to authenticate, then try again."

Extract the `cloudId` from the response — do NOT hardcode it.

## Fetching

### Step 1: Fetch the issue with all fields
Use the Atlassian MCP `getJiraIssue` tool with:
- `cloudId`: the value from auth preflight
- `issueIdOrKey`: the extracted ticket key
- `fields`: `["*all*"]`
- `responseContentFormat`: `markdown`

### Step 2: Fetch comments
Use the Atlassian MCP `getJiraIssue` tool with:
- `cloudId`: the value from auth preflight
- `issueIdOrKey`: the extracted ticket key
- `fields`: `["comment"]`
- `responseContentFormat`: `markdown`

Run both calls in parallel if possible.

## Output

Present a clean summary including:

### Core fields
- **Summary** (title)
- **Type** (Bug, Story, Task, etc.)
- **Status**
- **Priority**
- **Assignee**
- **Reporter**
- **Sprint**
- **Story Points**
- **Scrum Team**
- **Fix Version(s)**
- **Labels**
- **Created / Updated dates**
- **Linked issues** (clones, blocks, etc.)

### Description
Full description text.

### Custom fields
Show any non-empty custom fields that are not already covered above. Skip internal/system fields that have no user value.

### Figma Links
- Scan the ticket fields for URLs containing `figma.com`. List any found.
- If found, use Figma MCP to fetch all details and summarize these details for user.
- If none, state: "No Figma links found."

### Attachments
List any attachments on the ticket (filename, size, author). These may contain screenshots, reports, or supporting documents relevant to the work.

### Comments
For each comment show:
- **Author** and **date**
- **Full body text** — do not truncate, comments often contain critical security reports, requirements, or context

## Important rules
- Always use `fields: ["*all*"]` — never skip custom fields
- Always fetch comments separately — they contain important context
- If the ticket is not found, inform the user clearly
- Do not summarize or truncate comment bodies — present them in full
- If no arguments provided, show usage and stop — do not prompt
