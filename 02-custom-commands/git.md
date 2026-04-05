---
description: Create a branch, commit, push, and output the PR creation URL for the current changes.
---

# /git — Branch, Commit, Push & PR

You are executing a git workflow. Follow these steps precisely, stopping on any failure.

## Inputs

Ask the user for:

- **Jira ticket ID** (e.g. PROJ-123) — used for branch name, commit message, and to derive the base branch
- **Commit message summary** — one-line description of the change

## Step 0: Pre-flight check

Run `git status` to check if there are any changes (staged, unstaged, or untracked).
If there are **no changes at all**, stop and inform the user — there is nothing to ship.

## Step 1: Derive base branch from Jira fix version

Fetch the Jira ticket using the same approach defined in `/jira` command (see `~/.claude/commands/jira.md` for configuration and fetching details) if you did not do that already.

From the result, look at the **fix version** field. It will contain a version string.

- Extract the version and derive the corresponding base branch name according to your team's branching convention (e.g. `rel/1.2` from version `1.2.3`)
- Verify the branch exists on the remote: `git ls-remote --heads origin <base-branch>`

**If you cannot determine the base branch**, stop and ask the user. This happens when:

- fix version is empty or missing
- The version contains "tbd", "TBD", or is otherwise ambiguous
- The derived branch doesn't exist on the remote

## Step 2: Stash current changes

```
git stash
```

## Step 3: Checkout base branch, fetch and pull latest

```
git checkout <base-branch>
git fetch origin
git pull origin <base-branch>
```

If pull fails (e.g. merge conflicts), stop and inform the user.

## Step 4: Create a new branch from origin

```
git checkout -b <new-branch> origin/<base-branch>
```

- Use kebab-case for the short description derived from the commit message
- Keep all meaningful words — do not truncate or drop words that would make the title ambiguous or meaningless. Prefer a slightly longer branch name over a vague one.

## Step 5: Pop stashed changes

```
git stash pop
```

If pop fails due to conflicts, stop and inform the user.

## Step 6: Stage only related files

- Run `git status` to see all changes
- **Only stage files that are related to the ticket fix** — never add logs, reports, test output, `.csv`, `.gz`, `.txt` artifacts, or unrelated files
- Show the user which files you're staging and confirm before proceeding

## Step 7: Commit with tee logging

Run the commit piped through `tee` so the full pre-commit hook output (lint, tests, etc.) is captured:

```
git commit -m "<message>" 2>&1 | tee /tmp/git-commit-output.txt
```

After the command:

- Read `/tmp/git-commit-output.txt` to check for errors or test failures
- If pre-commit hooks failed, read the log, diagnose the issue, and inform the user — do NOT retry blindly
- If pre-commit hooks failed, output the failure errors/messages exactly as is from the log to the user
- If commit succeeded, confirm and continue

## Step 8: Push and set upstream

```
git push -u origin <new-branch>
```

## Step 9: Output the PR creation URL

Construct the PR URL for your team's git hosting platform (GitHub, GitLab, Bitbucket, etc.) with the source branch and destination branch pre-filled, then output it for the user.

## Important rules

- Stop on any failure and inform the user — never force-push, reset, or skip hooks
- The `tee` log at `/tmp/git-commit-output.txt` is critical — always read it after commit to verify success
- Never stage artifact files (`.csv`, `.gz`, `.log`, `.txt` test outputs)
