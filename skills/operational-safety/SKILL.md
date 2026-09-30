---
name: operational-safety
description: Protect live systems from lockout, outages, data loss, and irreversible changes. Use before mutations to Linux hosts, SSH, firewalls, networking, storage, databases, cloud resources, Kubernetes clusters, production services, credentials, or recovery controls. Do not use for read-only analysis, documentation, or local code edits.
---

# Operational Safety

Never trade away the current access path, recovery path, or last known-good state merely to complete a change. A successful command is not a successful operation unless access, health, and recoverability remain verified.

## Classify risk

Classify the intended action before execution:

- **Read-only:** observes state without changing it.
- **Reversible:** has a tested, immediately available rollback.
- **Destructive:** deletes, overwrites, rotates, expires, or permanently transforms state.
- **Access-affecting:** can change SSH, firewall, routing, DNS, IAM, credentials, certificates, or administrative access.
- **Availability-affecting:** can restart, drain, scale, deploy, migrate, or disrupt a live workload.

Use the highest applicable risk level. Treat an unknown target, blast radius, rollback, or access path as a blocker for mutation, not as permission to guess.

## Safety gate

Before a non-read-only action:

1. Identify the exact host, account, region, cluster, namespace, database, service, environment, and current session path that apply.
2. Inspect current state and concurrent operations using read-only commands.
3. Define success signals, failure signals, blast radius, rollback steps, and the access method needed to perform recovery.
4. Confirm that backup, versioning, redundancy, out-of-band access, or another recovery mechanism actually exists when the change could require it.
5. Prefer a dry run, plan, diff, config test, canary, or single-target change.
6. Present the exact mutation and rollback plan, then require explicit approval immediately before execution.
7. Execute one bounded step, verify health and access, and stop on unexpected output before continuing.

Do not combine unrelated risky actions into one command. Do not weaken safety controls, use force flags, disable locking, skip validation, bypass approvals, or broaden targets merely to make an operation succeed.

## Domain guardrails

- For SSH, host firewalls, routing, DNS, VPN, Linux services, reboots, storage, permissions, or destructive shell commands, read [references/linux-network.md](references/linux-network.md).
- For cloud, Kubernetes, databases, deployments, secrets, certificates, CI/CD, or observability changes, read [references/platforms.md](references/platforms.md).

## Stop conditions

Stop mutation and report the blocker when:

- The target or environment is ambiguous.
- The current access path may be removed without verified alternate access.
- A required backup, rollback, or recovery credential is unavailable.
- The observed state differs materially from the reviewed plan.
- Another deployment, migration, restore, incident action, or state lock conflicts with the change.
- Verification fails or monitoring indicates degradation.

After execution, report the exact action, target, observed result, health checks, remaining risk, and rollback status. Never claim success from command exit status alone.
