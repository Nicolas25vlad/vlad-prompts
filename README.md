# vlad-prompts

A compact library of behavioral instructions and reusable Agent Skills for AI agents.

The main artifact is **[`core/VLAD.md`](core/VLAD.md)**: the canonical, provider-agnostic behavioral system prompt for coding agents, chat assistants, research agents, technical-writing agents, and custom LLM applications.

> **Understand precisely. Think compactly. Act minimally. Verify aggressively. Explain clearly.**

VLAD optimizes **quality per token**. It removes wasted reasoning, code, tool calls, context, and prose without removing work required for correctness.

## Core variants

### `core/VLAD.md`

The **canonical full prompt**.

Use this whenever the host supports a normal system/global instruction budget.

### `core/VLAD.compact.md`

A deliberately reduced build for surfaces with tight instruction limits.

It preserves the highest-value rules, but it is **not the source of truth** and should not constrain the design of the canonical core.

## Skills

The specialized workflows are executable Agent Skills:

- [`vlad-code`](skills/vlad-code/SKILL.md): implementation and repository changes;
- [`vlad-debug`](skills/vlad-debug/SKILL.md): evidence-driven debugging;
- [`vlad-review`](skills/vlad-review/SKILL.md): focused defect/PR review;
- [`vlad-codebase-audit`](skills/vlad-codebase-audit/SKILL.md): repository-wide maintainability, simplicity, security, debt, Git history, and quality score;
- [`vlad-pr-audit`](skills/vlad-pr-audit/SKILL.md): pre-review PR/diff audit with YAGNI findings, commit attribution, fix plan, and quality score;
- [`vlad-research`](skills/vlad-research/SKILL.md): source-backed research;
- [`vlad-explain`](skills/vlad-explain/SKILL.md): progressive explanation;
- [`vlad-help`](skills/vlad-help/SKILL.md): workflow discovery/routing.

Both audit skills use an explainable 0–100 heuristic, evidence-backed findings, severity, fix plans, and Git attribution when available. The codebase audit scores inspected repository health; the PR audit scores only introduced or worsened issues. Scores may be provisional when coverage is limited.

The same skill gives a slash-command-style UX on hosts that expose skills through `/`.

Typical invocation:

```text
Cursor / Claude Code: /vlad-debug  or /vlad-codebase-audit
Codex:               $vlad-debug or $vlad-pr-audit
```

See [Skills and slash-style workflows](docs/skills.md).

## Use it

### 1. Global instruction

Use `core/VLAD.md` by default.

Use `core/VLAD.compact.md` only when the host cannot fit the full prompt.

Host-specific placement notes:

- [Codex](agents/codex.md)
- [Claude / Claude Code](agents/claude-code.md)
- [Cursor](agents/cursor.md)
- [ChatGPT](agents/chatgpt.md)

### 2. Invoke a task skill

Keep the core global, then load one task workflow only when needed.

```text
VLAD core
+ selected skill
+ project instructions
+ current task/context
```

Do not activate every skill by default.

### 3. Use the long modules as reference/depth

The skills are the executable interface. The deeper modules remain useful as reference material and for direct prompt composition:

- [Coding](coding/coding.md)
- [Debugging](coding/debugging.md)
- [Code review](coding/review.md)
- [Research](research/research.md)
- [Explanation](explanation/explanation.md)

### 4. Use the repo as a prompt-design reference

- [Principles](docs/principles.md)
- [Prompt design](docs/prompt-design.md)
- [Scope coverage](docs/coverage.md)
- [Skills](docs/skills.md)
- [Anti-patterns](docs/anti-patterns.md)
- [Research sources](docs/sources.md)
- [Behavioral evals](evals/scenarios.md)

## Plugin packaging

The repository ships reusable plugin manifests:

```text
plugin.json
.codex-plugin/plugin.json
```

The portable plugin exposes the `skills/` collection. Host adapters document the preferred installation surface.

## Architecture

```text
vlad-prompts/
├── core/
│   ├── VLAD.md
│   └── VLAD.compact.md
├── skills/
│   ├── vlad-code/SKILL.md
│   ├── vlad-debug/SKILL.md
│   ├── vlad-review/SKILL.md
│   ├── vlad-codebase-audit/SKILL.md
│   ├── vlad-pr-audit/SKILL.md
│   ├── vlad-research/SKILL.md
│   ├── vlad-explain/SKILL.md
│   └── vlad-help/SKILL.md
├── coding/
│   ├── coding.md
│   ├── debugging.md
│   └── review.md
├── research/
│   └── research.md
├── explanation/
│   └── explanation.md
├── agents/
│   ├── codex.md
│   ├── claude-code.md
│   ├── cursor.md
│   └── chatgpt.md
├── docs/
│   ├── principles.md
│   ├── prompt-design.md
│   ├── coverage.md
│   ├── skills.md
│   ├── anti-patterns.md
│   └── sources.md
├── evals/
│   └── scenarios.md
├── plugin.json
└── .codex-plugin/
    └── plugin.json
```

The architecture stays intentionally small. Skills are the executable workflow layer; long modules are reference/depth; adapters contain provider-specific placement.

## Behavioral model

For non-trivial work:

```text
normalize -> inspect -> decide -> act -> verify -> report
```

This produces several concrete behaviors:

- noisy human input is normalized without changing intent;
- reasoning is structured around decisions rather than conversational self-talk;
- tools replace guesses, but tool spam is avoided;
- coding starts from the existing architecture and patterns;
- debugging follows evidence and root cause;
- autonomy is preferred until ambiguity materially changes the result;
- verification is part of completion;
- context is treated as a limited working set;
- output is proportional to the task.

## Prompt composition

A strong default is:

```text
VLAD full core
+ one relevant skill (optional)
+ host/project instructions
+ current task
+ dynamic context
```

For a constrained surface:

```text
VLAD compact
+ selected skill when needed
+ host/project instructions
+ current task
```

Keep stable instructions before volatile context when the host can reuse cached prompt prefixes.

## Evaluation

[`evals/scenarios.md`](evals/scenarios.md) contains provider-agnostic regression scenarios.

[`docs/coverage.md`](docs/coverage.md) maps the intended VLAD scope to concrete sections so reductions in prompt size do not silently remove required behavior.

The goal is not to make every response shorter. The goal is to remove tokens and actions that do not improve the result.

## Research

The system was designed from behavioral patterns found across coding agents, public prompt research, official provider documentation, [i-have-adhd](https://github.com/ayghri/i-have-adhd), and [Ponytail](https://github.com/DietrichGebert/ponytail).

The third-party system-prompt collection used during research is treated as reverse-engineering material, not as authoritative provider documentation. See [sources](docs/sources.md).
