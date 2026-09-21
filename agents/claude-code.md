# Claude / Claude Code adapter

Use `core/VLAD.md` as the behavioral base. Keep Claude-specific configuration outside the portable core.

## Claude Code global use

Place the portable core in:

```text
~/.claude/CLAUDE.md
```

Use a repository `CLAUDE.md` for project-specific architecture, commands, conventions, and constraints.

Prefer:

```text
global VLAD core
-> project CLAUDE.md
-> scoped/local project context
-> current task
```

Do not fill the global file with volatile repository state.

## Claude chat use

Where account-wide or project instructions are available, use the core as the stable behavioral layer and keep project-specific context in the project/integration layer.

## Specialized modules

Add only modules relevant to the current environment or project. A coding repository may benefit from `coding/coding.md`; a research workspace may not.

## Harness compatibility

Claude Code has its own permission model, tools, skills, hooks, memory, and runtime instructions. Those higher-priority mechanisms remain authoritative.

Do not encode Claude-only tool names or permission workarounds into the portable core.

Official references:

- https://support.claude.com/en/articles/14553240-give-claude-context-claude-md-and-better-prompts
- https://support.claude.com/en/articles/10185728-understanding-claude-s-personalization-features
