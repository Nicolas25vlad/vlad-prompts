# vlad-prompts

A compact library of behavioral instructions for AI agents.

The main artifact is **[`core/VLAD.md`](core/VLAD.md)**: one portable prompt that can stand alone as a global/system instruction for coding agents, chat assistants, research agents, and custom LLM applications.

> **Understand precisely. Think compactly. Act minimally. Verify aggressively. Explain clearly.**

VLAD optimizes **quality per token**. It tries to remove wasted reasoning, code, tool calls, context, and prose without removing work required for correctness.

## Use it

### 1. Global instruction

Copy `core/VLAD.md` into the global/custom instruction surface of your agent.

The core is deliberately provider-agnostic and compact enough for common custom-instruction surfaces.

Host-specific placement notes:

- [Codex](agents/codex.md)
- [Claude / Claude Code](agents/claude-code.md)
- [Cursor](agents/cursor.md)
- [ChatGPT](agents/chatgpt.md)

### 2. Add one specialized module

Use the core alone by default. Add a module only when it materially helps:

- [Coding](coding/coding.md)
- [Debugging](coding/debugging.md)
- [Code review](coding/review.md)
- [Research](research/research.md)
- [Explanation](explanation/explanation.md)

Do **not** concatenate every file into one mega-prompt.

### 3. Use the repo as a prompt-design reference

The docs explain why the rules exist and how to build efficient agent instructions:

- [Principles](docs/principles.md)
- [Prompt design](docs/prompt-design.md)
- [Anti-patterns](docs/anti-patterns.md)
- [Research sources](docs/sources.md)
- [Behavioral evals](evals/scenarios.md)

## Architecture

```text
vlad-prompts/
├── core/
│   └── VLAD.md
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
│   ├── anti-patterns.md
│   └── sources.md
└── evals/
    └── scenarios.md
```

The architecture is intentionally small. A new file should represent a distinct behavior layer, not one paragraph that could live elsewhere.

## Behavioral model

For non-trivial work, VLAD uses one compact loop:

```text
normalize -> inspect -> decide -> act -> verify -> report
```

Important consequences:

- noisy human input is normalized without changing intent;
- reasoning is structured around decisions rather than conversational self-talk;
- tools replace guesses, but tool spam is avoided;
- coding starts from the existing architecture and patterns;
- debugging follows evidence and root cause;
- autonomy is preferred until ambiguity materially changes the result;
- verification is part of completion;
- output is proportional to the task.

## Prompt composition

A good default composition is:

```text
VLAD core
+ one relevant specialized module (optional)
+ host adapter/project instructions
+ current task and dynamic context
```

Keep stable instructions before volatile context when the host can reuse cached prompt prefixes.

## Evaluation

[`evals/scenarios.md`](evals/scenarios.md) contains provider-agnostic regression scenarios for coding, debugging, research, explanation, ambiguity, long context, scope discipline, and tool efficiency.

The goal is not to make every response shorter. The goal is to remove tokens and actions that do not improve the result.

## Research

The system was designed from behavioral patterns found across coding agents, public prompt research, official provider documentation, [i-have-adhd](https://github.com/ayghri/i-have-adhd), and [Ponytail](https://github.com/DietrichGebert/ponytail).

The third-party system-prompt collection used during research is treated as reverse-engineering material, not as authoritative provider documentation. See [sources](docs/sources.md).
