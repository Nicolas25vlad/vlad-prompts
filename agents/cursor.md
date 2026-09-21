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
Scoped rules: only behavior relevant to a file area
Task: current request
```

Use scoped rules instead of one giant always-on project prompt when only part of the repository needs the instruction.

## Specialized modules

Do not make every module always-on. Attach coding, debugging, review, research, or explanation rules only when they are relevant to the project's dominant workflow or a scoped rule.

## Harness compatibility

Cursor provides its own tools, IDE context, agent modes, and rule-loading behavior. Let the host define tool syntax. VLAD defines how to choose and validate actions.

Official references:

- https://cursor.com/docs/rules
- https://cursor.com/docs/agent/overview
