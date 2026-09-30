---
title: "<procedure name>"
owner: "<team or service owner>"
last_reviewed: "YYYY-MM-DD"
environments:
  - "<environment>"
---

# Purpose

<What this procedure accomplishes and when to use it.>

## Scope and exclusions

- Applies to: <services, platforms, and environments>
- Does not apply to: <explicit exclusions>

## Preconditions

- Change or incident reference: `<reference>`
- Required access and tools: <requirements>
- Recovery access or backup: <verified recovery mechanism>
- Conflicting operations to check: <deployments, migrations, restores, locks>

## Preflight

1. Target: `<exact target identifier>`
   - Check: `<read-only command or observation>`
   - Expected: `<evidence that this runbook applies>`

## Risk and approvals

- Blast radius: <affected users, services, data, or access paths>
- Approval required before: <first state-changing step>
- Stop when: <failure, mismatch, or degradation signals>

## Procedure

1. Action: `<bounded action>`
   - Expected: `<result>`
   - Verify: `<health or state check>`
   - Stop when: `<unexpected result>`

## Rollback or recovery

1. Trigger: <condition requiring recovery>
2. Action: `<reviewed recovery step>`
3. Verify: `<restored health and access>`
4. Escalate when: <rollback is unsafe or fails>

## Completion

- Success criteria: <end-to-end signals>
- Evidence to record: <commands, timestamps, dashboards, tickets>
- Follow-up: <cleanup, review, or prevention work>
- Escalation contact: <team or approved channel>
