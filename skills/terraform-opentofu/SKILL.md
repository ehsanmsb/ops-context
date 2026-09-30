---
name: terraform-opentofu
description: Create, review, debug, and safely operate Terraform or OpenTofu configurations, modules, plans, imports, moves, and state workflows. Use for .tf or .tfvars files, provider and module changes, plan analysis, drift, imports, or state operations. Do not use for CloudFormation, Pulumi, Ansible, or generic cloud architecture.
---

# Terraform and OpenTofu

Make the smallest reviewable infrastructure change that follows the repository's existing workflow. Never silently switch a project between Terraform and OpenTofu.

## Discover the execution context

Before changing or running anything:

1. Read repository guidance and inspect existing configuration, lock files, automation, and CI commands.
2. Identify the expected CLI and version, root module, environment, workspace, backend, providers, and affected resources.
3. When internal accounts, clusters, repositories, or MCP tools matter, use the `organization-context` workflow.
4. For a shared module change, inspect its callers before changing inputs, outputs, or behavior.

Ask only for context that blocks safe progress. Do not infer a production target, backend, workspace, account, region, resource address, or import identifier.

## Author configuration

- Preserve the repository's file layout, naming, version constraints, and module boundaries.
- Prefer direct resources and existing modules over speculative wrappers or new abstractions.
- Add variables only when callers need variation; include useful types and descriptions.
- Mark sensitive outputs appropriately and never place credentials or secret defaults in configuration or committed variable files.
- Do not add lifecycle suppression, broad IAM access, public network exposure, or destructive replacements merely to make a plan pass.
- Keep provider or module upgrades separate from unrelated infrastructure changes when practical.

## Validate and review

Use the repository's existing commands first. Otherwise:

1. Format or check formatting with the selected CLI.
2. Validate configuration when initialized dependencies are available.
3. Run configured linters, security scanners, policy checks, or tests only when the project already uses them.
4. Generate a plan only after confirming the target environment and backend.
5. Summarize creates, updates, replacements, destroys, sensitive changes, and unresolved unknowns.

Treat validation without a plan as incomplete evidence for runtime behavior. If credentials, initialization, or live access are unavailable, report the exact unverified layer.

## Mutation gate

Read [references/operations.md](references/operations.md) before imports, moves, state repair, force unlocks, applies, destroys, or production work.

Present the exact target, plan summary, validation results, and rollback or recovery considerations before mutation. Require explicit approval immediately before any apply, destroy, import, state mutation, force unlock, or production action. A saved plan can execute without another CLI prompt, so never treat its existence as approval.

Apply the `operational-safety` workflow whenever the operation can affect a live system, access path, availability, durable data, or recovery controls.

Do not use `-auto-approve`, bypass locking, edit state manually, expose plan or state contents, or commit generated plan and state files unless the user explicitly requests a safe, reviewed exception.

Finish with a concise list of changed files, validation performed, plan impact, remaining risks, and any action still awaiting approval.
