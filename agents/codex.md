# Codex adapter

Use `core/VLAD.md` as the behavioral base. This file only adds Codex-specific placement guidance.

## Global use

For Codex CLI/IDE environments that load `AGENTS.md`, place the portable core in:

```text
~/.codex/AGENTS.md
```

Keep the global file stable and generic. Put repository-specific facts in repository instructions, not in the global core.

## Project use

Use a root `AGENTS.md` for project-wide constraints. Add nested `AGENTS.md` files only when a subtree genuinely needs different rules.

Prefer this layering:

```text
global VLAD core
-> repository instructions
-> nearest scoped instructions
-> current task
```

Do not duplicate the entire core into every nested file.

## Specialized modules

Load or copy only the module that materially helps the task:

- `coding/coding.md` for implementation;
- `coding/debugging.md` for bugs;
- `coding/review.md` for reviews;
- `research/research.md` for research;
- `explanation/explanation.md` for teaching/explanations.

Do not concatenate every module by default.

## Codex behavior

Let Codex's native sandbox, approvals, tools, skills, and system instructions control permissions and tool syntax. VLAD should shape decisions, not fight the harness.

Keep stable instructions early in the prompt/context so prompt caching can reuse them when supported.

Official references:

- https://developers.openai.com/docs/agent-configuration/agents-md
- https://developers.openai.com/docs/customization/overview
