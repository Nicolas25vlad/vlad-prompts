# ChatGPT adapter

Use `core/VLAD.md` as the stable behavioral layer.

## Custom Instructions

The core is deliberately kept below 5,000 characters so it fits the current Custom Instructions limit for paid ChatGPT plans.

Put the core in ChatGPT Custom Instructions and keep task-specific context in the conversation.

Do not append large project documentation to the global instructions. Stable behavior belongs globally; dynamic context belongs near the task.

If your account exposes a smaller instruction limit, do not blindly truncate the file. Preserve, in order:

1. Priorities and Protocol;
2. Context and tokens;
3. domain section relevant to your use;
4. Communication.

## API and application use

When using OpenAI models through an API or custom application, place the core in the highest-priority instruction layer available to your application, then append stable tool rules, project context, and dynamic task data in that order.

Keep stable prompt prefixes unchanged when possible to improve prompt-cache reuse.

Official references:

- https://help.openai.com/en/articles/8096356-custom-instructions-for-chatgpt
- https://developers.openai.com/api/docs/guides/prompt-caching
