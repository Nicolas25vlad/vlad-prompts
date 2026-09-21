# Sources and research notes

VLAD is original work informed by public documentation and publicly available prompt research. Source material is used to extract patterns, not copied as a drop-in system prompt.

## System prompt research

### asgeirtj/system_prompts_leaks

Repository: https://github.com/asgeirtj/system_prompts_leaks

Reviewed material included examples attributed to Claude chat models, Claude Code, OpenAI Codex, ChatGPT agent-style prompts, and Cursor.

Useful recurring patterns:

- explicit instruction hierarchy;
- read/inspect before mutation;
- separate tool policy from communication style;
- distinguish diagnosis from authorized mutation;
- preserve user changes and avoid destructive operations;
- continue long tasks through context compaction instead of restarting;
- ask only when ambiguity materially changes the result;
- use specialized tools when they are safer or more precise;
- report verification honestly;
- keep host-specific mechanics outside portable behavior.

Important caveat: this is a third-party collection of claimed/extracted prompts. It is not treated as official documentation or proof of internal implementation.

## Clear communication

### ayghri/i-have-adhd

Repository: https://github.com/ayghri/i-have-adhd

Useful ideas adapted at the principle level:

- put the actionable answer early;
- keep multi-step work bounded and easy to scan;
- suppress tangents;
- make state and errors concrete;
- remove empty preambles and closing filler;
- optimize for an answer a reader can act on without rereading.

VLAD does not adopt every rule literally. Fixed list-size limits and mandatory time estimates, for example, are not portable enough for the core.

## Minimum sufficient action

### DietrichGebert/ponytail

Repository: https://github.com/DietrichGebert/ponytail

Useful ideas adapted at the principle level:

- understand the flow before optimizing implementation;
- search for existing project solutions first;
- prefer stdlib, native, and already-installed capabilities before adding code or dependencies;
- favor the smallest correct diff;
- do not confuse fewer lines with less responsibility;
- root-cause fixes beat repeated symptom patches.

VLAD generalizes this beyond code into **minimum sufficient action**: the fewest actions that completely and correctly solve the task.

## Official provider documentation

### OpenAI / ChatGPT / Codex

- Prompting: https://developers.openai.com/api/docs/guides/prompting
- Prompt caching: https://developers.openai.com/api/docs/guides/prompt-caching
- Codex customization: https://developers.openai.com/docs/customization/overview
- Codex AGENTS.md: https://developers.openai.com/docs/agent-configuration/agents-md
- ChatGPT Custom Instructions: https://help.openai.com/en/articles/8096356-custom-instructions-for-chatgpt

Relevant lessons:

- keep general instructions separate from task-specific details;
- stable prompt prefixes improve cache reuse;
- Codex supports layered project instructions through `AGENTS.md`;
- persistent project guidance should remain concise;
- custom-instruction surfaces have finite size, so the standalone core must stay compact.

### Anthropic / Claude

- Claude context, CLAUDE.md, and prompting: https://support.claude.com/en/articles/14553240-give-claude-context-claude-md-and-better-prompts
- Claude personalization features: https://support.claude.com/en/articles/10185728-understanding-claude-s-personalization-features

Relevant lessons:

- separate account/global behavior from project-specific context;
- use `CLAUDE.md` for durable Claude Code guidance;
- keep volatile repository state out of global instructions.

### Cursor

- Rules: https://cursor.com/docs/rules
- Agent overview: https://cursor.com/docs/agent/overview

Relevant lessons:

- keep persistent rules small and focused;
- use project-level rules for durable context;
- separate always-on instructions from specialized, scoped rules.

## Research policy

When extending this repository:

1. Prefer official documentation for product behavior.
2. Treat leaked or reverse-engineered prompts as research artifacts, not authority.
3. Extract reusable decision patterns rather than provider-specific wording.
4. Add a rule only when it improves observable behavior.
