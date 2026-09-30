# Organization profile format

Use `.ops-context.yaml` at a repository root to describe non-secret organization context relevant to that project. Every section is optional. Omit unknown or unused values instead of adding placeholders.

```yaml
version: 1

organization:
  name: Example Corp

source_control:
  provider: gitlab
  base_url: https://gitlab.example.com
  group: platform

documentation:
  repositories:
    - https://gitlab.example.com/platform/docs

runbooks:
  repositories:
    - name: platform-runbooks
      url: https://gitlab.example.com/platform/runbooks
      path: runbooks
  knowledge_bases:
    - name: operations
      url: https://docs.example.com/operations/runbooks

knowledge:
  provider: confluence
  base_url: https://docs.example.com
  spaces:
    - PLATFORM

tickets:
  provider: jira
  base_url: https://tickets.example.com
  projects:
    - OPS

cloud:
  accounts:
    - name: production
      provider: aws
      account_id: "123456789012"
      regions:
        - eu-west-1
      environment: production

kubernetes:
  clusters:
    - name: production
      context: production
      environment: production
      default_namespace: platform

observability:
  metrics: https://grafana.example.com
  logs: https://logs.example.com
  traces: https://traces.example.com

systems:
  - capability: developer-portal
    name: backstage
    url: https://developer.example.com
  - capability: ci
    name: gitlab-ci
    url: https://gitlab.example.com
  - capability: gitops
    name: argocd
    url: https://argocd.example.com
  - capability: container-registry
    name: harbor
    url: https://registry.example.com
  - capability: secrets-management
    name: vault
    url: https://vault.example.com
  - capability: on-call
    name: pagerduty
    url: https://oncall.example.com
  - capability: security-findings
    name: security-center
    url: https://security.example.com
  - capability: cost-management
    name: finops
    url: https://cost.example.com

mcp_tools:
  source_control: gitlab
  knowledge: confluence
  tickets: jira
  cloud: aws
  kubernetes: kubernetes
  observability: grafana
  service_catalog: backstage
  delivery: argocd
  artifacts: harbor
  secrets: vault
  incidents: pagerduty
  security: security-center
  cost: finops
  runbooks: knowledge
```

## Recommended system capabilities

Add only capabilities the organization actually uses:

- `developer-portal` and `service-catalog` for service ownership, dependencies, and self-service workflows.
- `ci`, `cd`, and `gitops` for builds, deployments, promotion, and rollback state.
- `infrastructure-as-code` for Terraform, OpenTofu, Pulumi, state, plans, and policy checks.
- `container-registry` and `package-registry` for images, packages, provenance, and promotion.
- `secrets-management` and `identity-access` for access workflows and secret metadata, never secret values.
- `on-call`, `status-page`, and `postmortems` for incident coordination and operational history.
- `security-findings`, `siem`, and `policy` for vulnerabilities, events, compliance, and guardrails.
- `cost-management` for budgets, allocation, usage, and optimization.
- `dns`, `cdn`, `vpn`, and `network-management` for network control planes.
- `backup-recovery` for backup inventory, restore workflows, and disaster-recovery status.
- `communication` for the approved incident or engineering collaboration channel.

Each `systems` item uses a stable capability plus the organization's recognizable tool name and discovery URL. Optional entries may also include `environments`, `projects`, or `mcp_tool` when they materially narrow selection.

Use `runbooks.repositories` for version-controlled procedures and `runbooks.knowledge_bases` for canonical procedures maintained in documentation systems. Each entry needs a recognizable `name` and discovery `url`; add `path`, `environments`, or `services` only when they narrow selection. A logical `mcp_tools.runbooks` mapping may point to the configured knowledge or source-control capability, but it does not prove that the connection is available.

## Rules

- Store identifiers and discovery URLs only.
- Never store tokens, passwords, cookies, private keys, kubeconfigs, connection strings, or secret values.
- Treat `mcp_tools` and per-system `mcp_tool` values as logical capability mappings, not proof that a connection exists.
- Configure MCP endpoints and authentication in the agent host or a private organization plugin.
- Keep production and non-production targets distinguishable.
- Prefer stable names over environment-specific aliases that users cannot recognize.
- Keep company-specific profiles in repositories and systems authorized for that information.

For organization-wide context, publish a private companion plugin that uses this format and declares the organization's authenticated MCP dependencies. Keep the portable OpsContext plugin free of internal endpoints and credentials.
