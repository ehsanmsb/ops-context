# OpsContext

Context-aware skills for safer, more focused DevOps and cloud AI agents.

OpsContext is an early-stage public Agent Plugin. It packages small, task-specific skills instead of loading one large instruction set into every request.

## Who it is for

- Software developers working with delivery and infrastructure workflows
- DevOps, SRE, platform, and cloud engineers
- Teams connecting AI agents to private engineering systems through MCP

## Included skills

### `git-workflow`

Guides branch naming, Conventional Commits, commit and push review gates, and removal of AI attribution from Git metadata.

Activation and behavior cases live in [`evals/git-workflow.json`](evals/git-workflow.json).

### `organization-context`

Resolves organization-specific source control, documentation, tickets, service catalogs, delivery systems, artifact registries, cloud accounts, Kubernetes clusters, observability, incidents, security, cost systems, and MCP capabilities without hardcoding private values into the public plugin.

Projects can copy [`examples/ops-context.yaml`](examples/ops-context.yaml) to `.ops-context.yaml` and replace the example values with non-secret organization context. See the [profile format](skills/organization-context/references/profile-format.md) for boundaries and field guidance.

Actual MCP endpoints, authentication, internal policies, and sensitive references belong in the agent host configuration or a private companion plugin maintained by the organization.

Activation and behavior cases live in [`evals/organization-context.json`](evals/organization-context.json).

### `terraform-opentofu`

Creates, reviews, debugs, and safely operates Terraform and OpenTofu configuration. It preserves repository conventions, reviews plan impact, protects state, and requires explicit approval before applies, destroys, imports, state mutations, force unlocks, or production operations.

Activation and behavior cases live in [`evals/terraform-opentofu.json`](evals/terraform-opentofu.json).

### `operational-safety`

Protects live systems from access lockout, outages, data loss, unsafe retries, and irreversible changes. It adds explicit safeguards for remote Linux administration, SSH and firewalls, networking, storage, cloud control planes, Kubernetes, databases, credentials, deployments, and incident operations.

Activation and behavior cases live in [`evals/operational-safety.json`](evals/operational-safety.json).

## Principles

- Load only the workflow relevant to the current request.
- Prefer repository conventions and existing tools.
- Keep changes small, reviewable, and validated.
- Require explicit approval before commits, pushes, or destructive operations.
- Never expose secrets or invent live infrastructure state.

## Status

Version `0.4.0` adds reviewed Git workflows, organization context, focused Terraform/OpenTofu operations, and shared operational safeguards for live systems. Additional infrastructure workflows will be added incrementally after their activation and output behavior can be evaluated.

## License

[MIT](LICENSE)
