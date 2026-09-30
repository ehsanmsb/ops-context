# Linux and network guardrails

## SSH and host firewalls

When connected remotely, assume firewall, route, interface, SSH daemon, key, user, PAM, and sudo changes can permanently lock out the operator.

Before changing UFW, firewalld, nftables, iptables, or another host firewall:

1. Detect whether the current session is remote and record its source, destination, address family, and SSH port.
2. Identify the active firewall manager and its persistent configuration. Do not mix managers casually.
3. Inspect the effective SSH listener and all management paths instead of assuming port 22.
4. Add and verify the replacement allow rule before removing or narrowing the current rule.
5. Preserve the existing session. Verify a second independent login through the intended final path before removing the old path.
6. Use a verified out-of-band console or scheduled automatic rollback when a mistake could sever all remote access.
7. Recheck firewall state, SSH access, service health, and persistence after the change.

Never enable a default-deny policy, flush a ruleset, replace the active table, close the current SSH port, or remove the operator's source address while SSH is the only verified management path. Never assume a successful rule command proves a new connection works.

## Routing, DNS, VPN, and interfaces

- Record the current management route, gateway, DNS resolution, interface addresses, and VPN dependency.
- Add and test a new route, resolver, interface, or tunnel before removing the old one.
- Avoid restarting the entire network stack remotely when a scoped reload or staged change exists.
- Keep a timed rollback or out-of-band path for default route, DNS, VPN, MTU, bonding, bridge, and interface changes.
- Verify both IPv4 and IPv6 when either can carry management or production traffic.

## Services, packages, and reboots

- Validate configuration with the service's native test command before reload or restart.
- Prefer reload over restart when it safely applies the change.
- Check active sessions, dependent services, workload redundancy, maintenance windows, and restart policy.
- Do not stop or disable SSH, sudo access, the firewall manager, or a recovery agent until replacement access is verified.
- Drain or fail over workloads before rebooting or replacing a live node when availability requires it.
- Require approval immediately before a reboot, shutdown, kernel change, or package operation that restarts critical services.

## Storage, files, and permissions

- Resolve the exact device, mount, filesystem, path, and owning workload before mutation.
- Verify backups or snapshots and their restore path before formatting, partitioning, shrinking, wiping, detaching, or deleting storage.
- Never run broad recursive deletion or permission changes against an unresolved variable, wildcard, repository root, filesystem root, home directory, or mounted data path.
- Do not use `mkfs`, `wipefs`, `dd`, destructive filesystem repair, or partition-table writes without exact-device review and approval.
- When changing SSH keys, users, sudoers, ownership, or permissions, preserve the current authorized path until a second session verifies the replacement.

## Destructive shell operations

Expand variables and targets using read-only inspection before execution. Prefer explicit paths and bounded selectors. Reject commands whose safety depends on an empty variable, broad glob, unverified current directory, ambiguous device name, or command substitution that can change between review and execution.
