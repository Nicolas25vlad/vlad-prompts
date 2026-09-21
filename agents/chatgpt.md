# ChatGPT adapter

VLAD has two core builds:

- `core/VLAD.md`: canonical full behavior;
- `core/VLAD.compact.md`: reduced compatibility build.

## Custom Instructions

For ChatGPT surfaces with a tight Custom Instructions character limit, use `core/VLAD.compact.md`.

Do not shrink the canonical `VLAD.md` merely to satisfy this surface.

Keep project-specific or volatile context in the conversation or project layer instead of consuming the global instruction budget.

## Skills

OpenAI skill-capable surfaces can use the reusable workflows under `skills/`.

Available skills:

```text
vlad-code
vlad-debug
vlad-review
vlad-research
vlad-explain
vlad-help
```

The repository ships plugin packaging so the specialized workflows can be installed without pasting each prompt repeatedly.

Keep the core as the stable behavioral layer and load the task skill on demand.

## Larger system/project instruction surfaces

If the ChatGPT/OpenAI surface supports a larger system, developer, workspace, or project instruction layer, prefer the full `core/VLAD.md`.

A useful order is:

```text
VLAD full core
-> stable tool/application rules
-> stable project context
-> selected skill
-> task
-> dynamic data
```

## API and custom applications

When using OpenAI models through an API or custom application, place the full core in the highest-priority instruction layer your application controls unless the total prompt budget makes that impractical.

Keep stable prompt prefixes unchanged when possible to improve prompt-cache reuse.

Use the compact build only when latency, cost, context budget, or host limits make the full core materially unsuitable.

Official references:

- https://help.openai.com/en/articles/8096356-custom-instructions-for-chatgpt
- https://developers.openai.com/api/docs/guides/prompt-caching
- https://developers.openai.com/docs/build-skills
