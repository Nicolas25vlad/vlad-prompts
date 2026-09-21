# Sources and research notes

VLAD is original work informed by public documentation and publicly available prompt research. Source material is used to extract patterns, not copied as a drop-in system prompt.

## System prompt research

### asgeirtj/system_prompts_leaks

Repository: https://github.com/asgeirtj/system_prompts_leaks

Reviewed material included examples attributed to:

- Claude chat models across multiple versions;
- Claude Code;
- OpenAI Codex;
- ChatGPT agent-style prompts;
- Cursor.

Useful recurring patterns:

- explicit instruction hierarchy;
- read/inspect before mutation;
- separate tool policy from communication style;
- distinguish read-only diagnosis from authorized mutation;
- preserve user changes and avoid destructive operations;
- continue long tasks through context compaction instead of restarting;
- ask only when ambiguity materially changes the result;
- use specialized tools when they are better than generic shell operations;
- report verification honestly;
- keep provider-specific harness behavior outside portable behavioral principles.

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

VLAD does not adopt every rule literally. For example, fixed list-size limits and mandatory time estimates are not part of the portable core because they can reduce correctness in some tasks.

## Minimum sufficient action

### DietrichGebert/ponytail

Repository: https://github.com/DietrichGebert/ponytail

Useful ideas adapted at the principle level:

- understand the flow before optimizing the implementation;
- search for existing project solutions first;
- prefer standard-library, native, and already-installed capabilities before adding code or dependencies;
- favor the smallest correct diff;
- do not confuse fewer lines with less responsibility;
- root-cause fixes beat repeated symptom patches.

VLAD generalizes this beyond code into "minimum sufficient action": the fewest actions that completely and correctly solve the task.

## Official provider documentation

### OpenAI

- Prompting: https://developers.openai.com/api/docs/guides/prompting
- Prompt caching: https://developers.openai.com/api/docs/guides/prompt-caching
- Codex customization overview: https://developers.openai.com/docs/customization/overview
- AGENTS.md guidance: https://developers.openai.com/docs/agent-configuration/agents-md

Relevant design lessons:

- keep general instructions separate from task-specific details;
- stable prompt prefixes improve cache reuse;
- Codex supports layered project instructions through `AGENTS.md`;
- persistent project guidance should remain concise.

### Cursor

- Rules: https://cursor.com/docs/rules
- Agent overview: https://cursor.com/docs/agent/overview

Relevant design lessons:

- keep persistent rules small and focused;
- use project-level rules for durable context;
- separate always-on instructions from specialized, scoped rules.

## Research policy

When extending this repository:

1. Prefer official documentation for product behavior.
2. Treat leaked or reverse-engineered prompts as research artifacts, not authority.
3. Extract reusable decision patterns rather than provider-specific wording.
4. Add a rule only when it improves observable behavior.
