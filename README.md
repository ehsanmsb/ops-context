# OpsContext

Context-aware skills for safer, more focused DevOps and cloud AI agents.

OpsContext is an early-stage public Agent Plugin. It packages small, task-specific skills instead of loading one large instruction set into every request.

## Included skills

### `git-workflow`

Guides branch naming, Conventional Commits, commit and push review gates, and removal of AI attribution from Git metadata.

Activation and behavior cases live in [`evals/git-workflow.json`](evals/git-workflow.json).

## Principles

- Load only the workflow relevant to the current request.
- Prefer repository conventions and existing tools.
- Keep changes small, reviewable, and validated.
- Require explicit approval before commits, pushes, or destructive operations.
- Never expose secrets or invent live infrastructure state.

## Status

Version `0.1.0` starts with the Git workflow shared by future DevOps and cloud skills. Infrastructure-specific workflows will be added incrementally after their activation and output behavior can be evaluated.

## License

[MIT](LICENSE)
