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
-> selected skill
-> current task
```

## Skills as slash commands

Claude Code maps custom skills to slash commands.

Install/copy the relevant skill directories under the Claude skills location, for example project-local:

```text
.claude/skills/vlad-debug/SKILL.md
```

Then invoke:

```text
/vlad-code
/vlad-debug
/vlad-review
/vlad-research
/vlad-explain
/vlad-help
```

Skills may also be selected automatically when relevant.

Prefer skills over maintaining a duplicate legacy `.claude/commands/` tree.

## Claude chat use

Where account-wide or project instructions are available, use the core as the stable behavioral layer and keep project-specific context in the project/integration layer.

## Harness compatibility

Claude Code has its own permission model, tools, skills, hooks, memory, and runtime instructions. Those higher-priority mechanisms remain authoritative.

Do not encode Claude-only tool names or permission workarounds into the portable core.

Official references:

- https://support.claude.com/en/articles/14553240-give-claude-context-claude-md-and-better-prompts
- https://support.claude.com/en/articles/14553413-claude-code-cheatsheet
- https://support.claude.com/en/articles/12512198-how-to-create-custom-skills
