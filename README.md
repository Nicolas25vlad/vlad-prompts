# vlad-prompts

A compact library of behavioral instructions for AI agents.

The main artifact is **[`core/VLAD.md`](core/VLAD.md)**: the canonical, provider-agnostic behavioral system prompt for coding agents, chat assistants, research agents, technical-writing agents, and custom LLM applications.

> **Understand precisely. Think compactly. Act minimally. Verify aggressively. Explain clearly.**

VLAD optimizes **quality per token**. It removes wasted reasoning, code, tool calls, context, and prose without removing work required for correctness.

## Core variants

### `core/VLAD.md`

The **canonical full prompt**.

Use this whenever the host supports a normal system/global instruction budget. It contains the complete behavioral model:

- task classification;
- input normalization;
- reasoning discipline;
- ambiguity and autonomy;
- minimum sufficient action;
- planning;
- tool policy;
- context and token efficiency;
- file/repository editing;
- coding and architecture;
- debugging;
- review;
- error handling;
- verification;
- research;
- explanation and technical communication;
- long-task state;
- deterministic behavior;
- anti-patterns;
- completion criteria.

### `core/VLAD.compact.md`

A deliberately reduced build for surfaces with tight instruction limits.

It preserves the highest-value rules, but it is **not the source of truth** and should not constrain the design of the canonical core.

## Use it

### 1. Global instruction

Use `core/VLAD.md` by default.

Use `core/VLAD.compact.md` only when the host cannot fit the full prompt.

Host-specific placement notes:

- [Codex](agents/codex.md)
- [Claude / Claude Code](agents/claude-code.md)
- [Cursor](agents/cursor.md)
- [ChatGPT](agents/chatgpt.md)

### 2. Add one specialized module when useful

The canonical core already works alone. Specialized modules add depth for repeated workflows:

- [Coding](coding/coding.md)
- [Debugging](coding/debugging.md)
- [Code review](coding/review.md)
- [Research](research/research.md)
- [Explanation](explanation/explanation.md)

Do **not** concatenate every file into one mega-prompt by default.

### 3. Use the repo as a prompt-design reference

- [Principles](docs/principles.md)
- [Prompt design](docs/prompt-design.md)
- [Scope coverage](docs/coverage.md)
- [Anti-patterns](docs/anti-patterns.md)
- [Research sources](docs/sources.md)
- [Behavioral evals](evals/scenarios.md)

## Architecture

```text
vlad-prompts/
├── core/
│   ├── VLAD.md
│   └── VLAD.compact.md
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
│   ├── anti-patterns.md
│   └── sources.md
└── evals/
    └── scenarios.md
```

The architecture is intentionally small. A new file should represent a distinct behavior layer, not one paragraph that could live elsewhere.

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
+ one relevant specialized module (optional)
+ host/project instructions
+ current task
+ dynamic context
```

For a constrained surface:

```text
VLAD compact
+ host/project instructions
+ current task
```

Keep stable instructions before volatile context when the host can reuse cached prompt prefixes.

## Evaluation

[`evals/scenarios.md`](evals/scenarios.md) contains provider-agnostic regression scenarios for coding, debugging, research, explanation, ambiguity, long context, scope discipline, and tool efficiency.

[`docs/coverage.md`](docs/coverage.md) maps the intended VLAD scope to concrete sections so reductions in prompt size do not silently remove required behavior.

The goal is not to make every response shorter. The goal is to remove tokens and actions that do not improve the result.

## Research

The system was designed from behavioral patterns found across coding agents, public prompt research, official provider documentation, [i-have-adhd](https://github.com/ayghri/i-have-adhd), and [Ponytail](https://github.com/DietrichGebert/ponytail).

The third-party system-prompt collection used during research is treated as reverse-engineering material, not as authoritative provider documentation. See [sources](docs/sources.md).
