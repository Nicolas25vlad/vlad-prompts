# Codex adapter

Use `core/VLAD.md` as the behavioral base.

## Global use

For Codex CLI/IDE environments that load `AGENTS.md`, place the portable core in:

```text
~/.codex/AGENTS.md
```

Keep the global file stable and generic. Put repository-specific facts in repository instructions, not in the global core.

## Project use

Use a root `AGENTS.md` for project-wide constraints. Add nested `AGENTS.md` files only when a subtree genuinely needs different rules.

Prefer:

```text
global VLAD core
-> repository instructions
-> nearest scoped instructions
-> selected skill
-> current task
```

## Skills

This repository exposes task workflows under `skills/`.

Explicit Codex invocation:

```text
$vlad-code
$vlad-debug
$vlad-review
$vlad-research
$vlad-explain
$vlad-help
```

Codex can also select a skill automatically when its description matches the request.

For project-local skills, Codex can load skills from `.agents/skills`. The repository also ships `.codex-plugin/plugin.json` for plugin packaging.

Use one task skill by default. Compose several only when the task genuinely spans workflows.

## Codex behavior

Let Codex's native sandbox, approvals, tools, skills, and system instructions control permissions and tool syntax. VLAD shapes decisions, not the harness.

Keep stable instructions early in the prompt/context so prompt caching can reuse them when supported.

Official references:

- https://developers.openai.com/docs/agent-configuration/agents-md
- https://developers.openai.com/docs/customization/overview
- https://developers.openai.com/docs/build-skills
