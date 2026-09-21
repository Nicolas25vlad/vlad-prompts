# Prompt design

This repository treats prompts as executable behavioral specifications.

## Canonical core vs compact builds

`core/VLAD.md` is the canonical source of behavioral truth.

It should contain every rule that is important enough to change general agent behavior across providers. Do **not** constrain the canonical design to the smallest instruction limit of one host.

`core/VLAD.compact.md` is a compatibility build for tight instruction surfaces. It may omit depth, examples, and lower-priority rules, but it must preserve the core philosophy and priority order.

When compacting:

1. start from the canonical core;
2. preserve decision hierarchy;
3. preserve normalization, autonomy, tool grounding, minimal action, verification, context efficiency, and communication;
4. remove examples and duplicated elaboration before removing behavior;
5. document any intentionally lost behavior.

The compact build never becomes the design target for the full core.

## Keep the core provider-agnostic

Provider-specific syntax, tool names, permission models, file locations, and harness mechanics belong in `agents/`.

Domain-specific operating procedures belong in focused modules such as `coding/`, `research/`, and `explanation/`.

The core should describe **what behavior to choose**, not how one vendor names a tool.

## Prefer behavior over adjectives

Do not spend tokens saying the agent is "expert", "smart", "careful", or "senior" unless the role itself changes behavior.

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
+ host/project instructions
+ task
+ dynamic context
```

Use the compact build only when required by the host.

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
- Avoid new dependencies, unless existing alternatives are materially more complex or fragile.

## Anti-bloat test

Before adding or keeping an instruction, ask:

- Does it change behavior?
- Is it already implied elsewhere?
- Can it be written with fewer words without losing the decision rule?
- Is it concrete enough to apply?
- Is it portable across providers?
- Does it improve quality, predictability, or efficiency?
- Does it reduce ambiguity?
- Does it belong in the full core, compact build, a module, or an adapter?

If not, delete it.
