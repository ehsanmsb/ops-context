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

## Principles

- Load only the workflow relevant to the current request.
- Prefer repository conventions and existing tools.
- Keep changes small, reviewable, and validated.
- Require explicit approval before commits, pushes, or destructive operations.
- Never expose secrets or invent live infrastructure state.

## Status

Version `0.2.0` establishes reviewed Git workflows and a safe organization-context contract. Infrastructure-specific workflows will be added incrementally after their activation and output behavior can be evaluated.

## License

[MIT](LICENSE)
