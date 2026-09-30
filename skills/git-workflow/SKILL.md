---
name: git-workflow
description: Manage Git branches, commits, pushes, and history with clean branch names, Conventional Commits, review gates, and no AI attribution. Use when creating or naming branches, preparing or making commits, pushing changes, rebasing, or rewriting Git history.
---

# Git Workflow

Preserve the user's intent and the repository's existing conventions. A request to edit code is not permission to create a branch, commit, push, or rewrite history.

## Branches

Before creating a branch, inspect repository guidance and existing branch names. Follow an established convention when one exists; otherwise use `<type>/<short-description>` in lowercase kebab-case.

Do not include AI attribution in new branch names. Avoid standalone terms such as `ai`, `bot`, `agent`, `codex`, `chatgpt`, `claude`, `copilot`, or model names. Do not rename an existing user branch unless requested.

Examples:

- `feat/add-health-check`
- `fix/terraform-state-lock`
- `chore/update-ci-image`

## Commits

Follow the repository's existing commit convention. If none exists, use Conventional Commits:

```text
<type>(<optional-scope>): <imperative summary>
```

Keep each commit focused on one logical change. Do not add AI attribution, generated-by text, or AI co-authors to commit messages or metadata.

Before every commit:

1. Inspect the working tree and relevant diff.
2. Run the smallest meaningful validation for the changed files.
3. Show the user the changed files, a concise diff summary, validation results, and the exact proposed commit message.
4. Request explicit approval after presenting that review.
5. Commit only after approval.

Do not treat an earlier request to implement or edit as approval of the final commit.

## Pushes

Before every push:

1. Confirm the destination remote and branch.
2. Show the commits that will be pushed.
3. Report the latest validation results and any known risks.
4. Request explicit approval after presenting that review.
5. Push only after approval.

Never force-push, bypass hooks, amend commits, rebase, squash, or otherwise rewrite history unless the user explicitly requests that exact operation after seeing its impact.
