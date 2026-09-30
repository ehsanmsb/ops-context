# Runbook contract

Use this contract to assess a runbook before execution. A runbook may use a different layout, but the following information must be available for the current operation.

## Identity and scope

- A recognizable title and purpose.
- The owning team and an escalation path.
- A revision or last-reviewed date.
- Supported services, environments, platforms, and explicit exclusions.
- The symptoms, alert, request, or maintenance condition that should trigger the procedure.

## Preconditions

- Required access, tools, permissions, and maintenance or incident references.
- Target identifiers that distinguish production from non-production.
- Read-only checks that confirm the procedure applies to the observed state.
- Dependencies, concurrent operations, backups, redundancy, and recovery access relevant to the change.

## Executable steps

Each state-changing step must identify:

- the exact target and intended action;
- expected output or state;
- verification and failure signals;
- blast radius and a stop condition;
- any approval boundary before execution.

Commands are examples until their target, flags, variables, and current-state assumptions have been validated. Never execute unresolved placeholders. Never expose credentials or copy secret values into logs, tickets, or reports.

## Recovery and completion

- A rollback or recovery procedure appropriate to the current state.
- Conditions where rollback is unsafe and escalation is required.
- End-to-end health and access checks, not only command exit status.
- Evidence to record and follow-up work to create.

## Trust and precedence

Prefer the canonical source owned by the responsible team. Treat copied, cached, search-indexed, generated, or unattributed procedures as unverified until compared with that source.

Live evidence, current authorization boundaries, and the `operational-safety` workflow take precedence over a stale or unsafe runbook. Stop and escalate instead of forcing the system to match the document.
