# Platform guardrails

## Cloud control planes

- Verify identity, role, account or subscription, region, project, environment, and selected profile before mutation.
- Inspect dependencies, deletion protection, backups, replicas, locks, policy constraints, and organization guardrails.
- Preserve management connectivity when changing security groups, routes, gateways, load balancers, DNS, IAM, or identity providers.
- Do not delete or disable the last administrator, recovery role, encryption key, audit trail, log archive, state backend, or break-glass path.
- Stage changes narrowly and verify telemetry before expanding scope.

## Kubernetes

- Verify current context, cluster identity, namespace, resource names, selectors, and environment.
- Prefer server-side dry run and diff before mutation when supported.
- Inspect owners, replicas, readiness, disruption budgets, storage, finalizers, and active rollouts.
- Drain one node at a time unless reviewed availability and disruption budgets support more.
- Do not bypass disruption budgets, force-delete workloads, remove finalizers, or delete namespaces, CRDs, persistent volumes, admission controls, or control-plane resources merely to clear an error.
- Define and verify rollback for deployments, configuration, and node maintenance before proceeding.

## Databases and durable data

- Verify the database, schema, tenant, replica role, transaction boundaries, locks, migration state, and active traffic.
- Confirm a recent recoverable backup or snapshot and the actual restore procedure before destructive schema or data changes.
- Prefer expand-and-contract migrations, bounded batches, transactions where appropriate, and tested rollback or forward-fix procedures.
- Do not run unbounded updates or deletes, destructive migrations, failovers, restores, or replication changes without impact review and approval.
- Stop on unexpected row counts, lag, lock duration, error rate, or data validation failure.

## Secrets, keys, and certificates

- Never expose secret material in commands, logs, diffs, tickets, or chat.
- Rotate by overlapping old and new credentials until consumers verify the new path; revoke the old value only after verification.
- Confirm recovery and dependency impact before disabling identity providers, root credentials, KMS keys, certificate authorities, or signing keys.
- Verify certificate names, chain, expiry, private-key match, reload behavior, and rollback before replacement.

## Deployments and automation

- Preserve branch protections, reviews, policy checks, deployment locks, and audit trails.
- Prefer canary, staged, or single-target rollout with explicit health and rollback criteria.
- Do not use force push, skip CI, disable tests, suppress policy, or bypass change controls to unblock a release.
- Ensure the rollback artifact and configuration are available before production rollout.
- Stop expansion when error rate, latency, saturation, availability, or business signals regress.

## Monitoring and incidents

- Do not silence broad alert groups or disable monitoring to make a change appear healthy.
- Make silences scoped, owned, justified, and time-limited.
- Preserve logs, traces, events, timestamps, and audit evidence during incidents.
- Avoid simultaneous speculative changes. Make one measurable intervention at a time and record its outcome.
