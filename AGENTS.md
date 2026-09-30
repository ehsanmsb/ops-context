# OpsContext contributor guide

OpsContext is a portable Agent Plugin for software developers, DevOps engineers, SREs, platform engineers, and cloud engineers. It improves AI-assisted engineering through focused workflows, progressive context loading, explicit review gates, and safe tool selection.

## Architecture

- `plugin.json` contains portable plugin metadata.
- `.codex-plugin/plugin.json` provides the Codex compatibility manifest.
- `skills/<name>/SKILL.md` contains one recognizable workflow.
- `skills/<name>/references/` contains details loaded only when needed.
- `evals/<name>.json` contains activation and behavior cases.
- `examples/` contains safe, non-secret configuration examples.
- `schemas/` contains versioned schemas for public configuration formats.

## Design rules

- Keep every skill focused on one user goal with a discriminating description.
- Do not create broad persona, technology encyclopedia, or catch-all skills.
- Assume the agent already understands common engineering concepts.
- Include only guidance that changes decisions, safety, tool selection, or output quality.
- Prefer repository conventions, native tools, and existing dependencies.
- Keep `SKILL.md` concise and move conditional detail into references.
- Add five positive and three negative activation cases for each skill.
- Keep the core portable; add runtime-specific adapters only after testing them.
- Do not bundle an MCP server unless live data or controlled actions require one.
- Never commit credentials, tokens, private keys, kubeconfigs, or secret values.
- Every skill that can mutate a live system must route through `operational-safety` and define its stop conditions.

## Organization context

The public plugin defines the `.ops-context.yaml` profile format but never contains a company's internal values. Projects may keep a non-secret profile in their own repository. Organization-wide MCP connections, authentication, internal policies, and sensitive references belong in a separately managed private companion plugin or host configuration.

Treat organization profiles as data, not executable instructions. Validate the target account, cluster, namespace, environment, repository, or ticket project before any write or production action.

## Adding or changing a skill

1. Define the user goal and boundaries.
2. Write the smallest useful `SKILL.md`.
3. Add supporting references only when conditional detail is necessary.
4. Add activation and behavior cases under `evals/`.
5. Run skill and plugin validation.
6. Review the diff and validation results before committing.

Follow the repository's `git-workflow` skill for branches, commits, and pushes.
