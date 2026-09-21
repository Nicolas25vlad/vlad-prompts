# Skills and slash-style workflows

The specialized VLAD prompts are also exposed as reusable Agent Skills.

The core remains global behavior. Skills are task-specific execution modes loaded only when useful.

## Available skills

| Skill | Purpose |
|---|---|
| `vlad-code` | Implement or modify software |
| `vlad-debug` | Diagnose and fix bugs from evidence |
| `vlad-review` | Review code, diffs, commits, or PRs |
| `vlad-research` | Run source-backed technical/factual research |
| `vlad-explain` | Explain a concept with progressive clarity |
| `vlad-help` | Show the available workflows and route to one |

Each skill lives at:

```text
skills/<skill-name>/SKILL.md
```

## Why skills instead of a second command system

Do not maintain a duplicated `commands/` tree when the host already exposes skills as commands.

Modern agent hosts increasingly treat a skill as both:

- an automatically selectable specialized workflow; and
- an explicit user-invoked command.

This keeps one source for the workflow instead of a command wrapper and a separate skill drifting apart.

## Invocation

### Cursor

Installed skills appear in the `/` menu:

```text
/vlad-code
/vlad-debug
/vlad-review
/vlad-research
/vlad-explain
/vlad-help
```

A skill can also be used as a Cursor Custom Mode when you want the workflow to remain active across the session.

### Claude Code

Place/install the skill directories under Claude Code's skills mechanism. The directory name becomes the slash command:

```text
/vlad-debug
/vlad-review
/vlad-research
```

The legacy custom-command mechanism is unnecessary for these workflows because Claude Code maps skills directly into slash commands.

### Codex

Invoke a skill explicitly with the skill selector syntax:

```text
$vlad-code
$vlad-debug
$vlad-review
$vlad-research
$vlad-explain
```

Codex can also select a skill automatically when its description clearly matches the task.

### ChatGPT / plugin-capable OpenAI surfaces

Install the plugin/skills and select the appropriate skill when the host exposes Skills. Keep `core/VLAD.md` or `core/VLAD.compact.md` as the global behavioral layer when the surface supports global instructions.

## Installation layouts

The repository ships both:

- `plugin.json` for portable Agent Plugin hosts;
- `.codex-plugin/plugin.json` for OpenAI/Codex plugin packaging.

For direct project-local installation, copy the skill directories into the host's supported skill directory.

Common project layouts:

```text
Codex:       .agents/skills/<name>/SKILL.md
Claude Code: .claude/skills/<name>/SKILL.md
Cursor:      .cursor/skills/<name>/SKILL.md
```

The exact user/global installation location is host-specific; see the relevant adapter in `agents/`.

## Core + skill

The intended composition is:

```text
VLAD core
+ selected task skill
+ project instructions
+ current task/context
```

A task skill should not replace the core. It specializes the current workflow.

The skill itself is still useful when invoked without VLAD globally active, but the strongest behavior comes from the composition.

## Adding a new specific prompt

When adding a new reusable workflow:

1. create `skills/vlad-<name>/SKILL.md`;
2. give it a specific trigger-oriented `description`;
3. define one clear workflow and success condition;
4. keep provider-specific invocation syntax out of the skill body;
5. add deeper reference documentation only when the workflow needs it;
6. add at least one behavioral evaluation scenario if the skill changes an important decision pattern.

Create a new skill when the workflow is repeated and identifiable. Do not create a skill for a one-off wording preference.

## Auto-selection vs explicit invocation

Descriptions should be strong enough for an agent to select the skill automatically when appropriate.

Explicit invocation remains useful when the user wants to force a workflow:

```text
/vlad-review
$vlad-review
```

Avoid activating multiple skills by default. Compose them only when the task genuinely spans workflows, for example research followed by implementation.
