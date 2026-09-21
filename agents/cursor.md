# Cursor adapter

Use `core/VLAD.md` as the stable behavioral base.

## Global use

Put the core in Cursor User Rules when you want VLAD to apply across projects.

Keep global rules provider- and repository-agnostic.

## Project use

Use `AGENTS.md` or `.cursor/rules` for project-specific instructions.

A useful split is:

```text
User Rules: VLAD core
Project rules: architecture + conventions + commands
Skills: task-specific workflows
Task: current request
```

Use scoped rules instead of one giant always-on project prompt when only part of the repository needs the instruction.

## Skills and slash invocation

Cursor discovers Agent Skills and exposes them in the `/` menu.

Invoke:

```text
/vlad-code
/vlad-debug
/vlad-review
/vlad-research
/vlad-explain
/vlad-help
```

A skill can also be used as a Custom Mode when you want that workflow to remain active across multiple turns.

For project-local use, place skills under:

```text
.cursor/skills/<name>/SKILL.md
```

The root `plugin.json` also packages the repository as a portable Agent Plugin that Cursor can consume.

## Harness compatibility

Cursor provides its own tools, IDE context, agent modes, and rule-loading behavior. Let the host define tool syntax. VLAD defines how to choose and validate actions.

Official references:

- https://cursor.com/docs/rules
- https://cursor.com/docs/agent/overview
- https://cursor.com/docs/skills
- https://cursor.com/docs/plugins
