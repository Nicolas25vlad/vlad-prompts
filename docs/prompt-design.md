# Prompt design

This repository treats prompts as executable behavioral specifications.

## Keep the core stable

`core/VLAD.md` is intentionally provider-agnostic. It contains rules that should remain useful across coding agents, chat assistants, research agents, and custom LLM applications.

Provider-specific syntax, tool names, permission models, and file locations belong in `agents/`.

Domain-specific operating procedures belong in focused modules such as `coding/`, `research/`, and `explanation/`.

## Prefer behavior over adjectives

Do not spend tokens saying the agent is "expert", "smart", "careful", or "senior" unless the role itself changes what it should do.

Describe observable behavior instead:

- search before creating;
- trace the relevant flow before editing;
- verify claims with available tools;
- ask only when ambiguity is material;
- inspect the final diff.

A rule earns its place when it changes a decision.

## Stable prefix, dynamic suffix

For systems that support prompt caching, organize context in this order when possible:

1. global principles;
2. stable tool rules and schemas;
3. relatively stable project context;
4. task-specific instructions;
5. highly dynamic retrieved data or user input.

Do not rewrite large static blocks on every request. Append changing context after stable instructions.

## Layering

A practical composition is:

```text
core/VLAD.md
+ optional capability module
+ optional host adapter
+ project-specific instructions
+ task
```

Avoid blindly concatenating every file. Specialized modules should be loaded only when their rules materially help.

## Input normalization

Normalization is an internal representation, not a user-visible ceremony.

For a complex request:

```text
Goal:
Fix filtering by userId.

Facts:
The endpoint currently returns unfiltered data when userId is present.

Constraints:
Preserve other filters.
Avoid regressions.

Unknowns:
Where the filter is lost.

Likely path:
controller -> service -> repository/query -> tests

Success:
userId constrains results and existing filters still pass.
```

For a simple request such as "rename this variable", normalization may be no more than identifying the target and desired name.

## Reasoning

Reasoning should compute a solution, not imitate a spoken internal monologue.

Useful internal primitives:

```text
goal
facts
constraints
unknowns
dependencies
options
decision
action
verification
```

Do not require chain-of-thought disclosure. User-facing explanations should expose conclusions, evidence, assumptions, and short decision rationale when useful.

## Instructions should contain escape conditions

Rigid rules fail when they ignore context. State when a rule yields.

Examples:

- Be concise, unless completeness is required.
- Avoid questions, unless different interpretations produce materially different work.
- Prefer the smallest diff, unless the root cause is in a shared layer.
- Avoid new dependencies, unless the existing alternatives are materially more complex or fragile.

## Anti-bloat test

Before adding or keeping an instruction, ask:

- Does it change behavior?
- Is it already implied elsewhere?
- Can it be written with fewer words?
- Is it concrete enough to apply?
- Is it portable across providers?
- Does it improve quality, predictability, or efficiency?
- Does it reduce ambiguity?
- Does it belong in the core, a module, or an adapter?

If not, delete it.
