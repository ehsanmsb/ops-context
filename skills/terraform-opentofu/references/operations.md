# Terraform and OpenTofu operations

Read this reference only for plan execution, imports, moves, state operations, drift, or production targets.

## Classify the operation

Usually local or read-only:

- Formatting and formatting checks
- Configuration validation
- Existing repository lint, security, policy, and test commands
- State listing or showing, provided output will not expose secrets
- Planning after confirming the environment, backend, and credentials

Mutating or high risk:

- Apply and destroy
- Import through CLI or configuration-driven import followed by apply
- State move, remove, push, replace-provider, or manual repair
- Force unlock
- Refresh commands that write state
- Taint, replacement, or any production operation

Require explicit approval immediately before mutating or high-risk operations.

## Review a plan

Report:

- Target environment, account, region, workspace, and backend
- Counts and identities of creates, updates, replacements, and destroys
- IAM, network exposure, encryption, data retention, availability, and state changes
- Provider or module version changes
- Values that remain unknown until apply
- Potential cost or quota impact when supported by evidence
- Recovery or rollback constraints

Do not reduce a plan review to its resource counts. A single replacement, permission expansion, route change, database update, or state move can carry most of the risk.

Saved plans and plan JSON may contain sensitive values. Do not commit them, publish them, or paste their full contents into chat. Applying a saved plan executes without an interactive approval prompt; obtain approval before running it.

## Imports and moves

- Prefer configuration-driven `import` and `moved` blocks when the project's selected version supports them because they are reviewable in normal plan workflows.
- Confirm the resource address, provider, environment, and remote identifier before import.
- Ensure configuration exists and matches the real resource before applying an import.
- Use `moved` blocks for address refactors when possible instead of ad hoc state moves.
- Inspect every module caller before moving shared resources or changing module addresses.

## State and locking

- Treat state as sensitive and preserve backend locking.
- Never edit state JSON manually.
- Before state mutation, verify the backend, workspace, target address, current lock owner, and recovery path.
- Do not use `-lock=false` to work around contention.
- Force-unlock only after confirming the original operation is no longer running and the lock identifier belongs to the intended backend and workspace.
- Use backend-supported versioning or a protected backup before a state repair when available.

OpenTofu can encrypt state and plan data at rest, but enabling or changing encryption without a recoverable key strategy can make them unreadable. Treat encryption changes as a separate reviewed migration.

## Failure handling

Stop after an unexpected partial apply, state write failure, provider authentication failure, or ambiguous target. Preserve logs without secrets, inspect live and state data read-only, and propose the smallest recovery step. Do not retry mutation commands blindly.
