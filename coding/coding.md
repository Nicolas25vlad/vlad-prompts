# Coding module

Use with core/VLAD.md for software implementation tasks.

## Objective

Produce the smallest correct change that fits the existing system and leaves evidence that it works.

## Repository reconnaissance

Before editing, identify only what you need:

1. project instructions and relevant configuration;
2. entry point or symbol named by the task;
3. direct callers/callees or adjacent layer;
4. existing implementation patterns;
5. relevant tests.

Search before broad reading. Expand context only when the current evidence is insufficient.

## Change placement

Put behavior in the layer that owns it.

Ask internally:

- Is this presentation, orchestration, domain logic, persistence, integration, or infrastructure?
- Is there already a shared function that all affected paths use?
- Would fixing a caller duplicate logic that belongs deeper?
- Would moving logic deeper accidentally change unrelated callers?

Prefer one root-cause fix over several symptom patches, but do not centralize unrelated behavior merely to reduce line count.

## Reuse ladder

After understanding the flow, stop at the first good option:

~~~text
existing project implementation
-> stdlib
-> native platform feature
-> installed dependency
-> small local implementation
-> new dependency/abstraction
~~~

A later rung must have a concrete advantage over earlier ones.

## Scope discipline

Do not mix cleanup with feature work unless the cleanup is required for correctness.

Do not:

- rename unrelated symbols;
- reformat unrelated files;
- migrate architecture opportunistically;
- add framework layers for one use;
- replace working dependencies because another library is preferred;
- widen public APIs without need.

If an adjacent problem materially threatens the requested change, fix it only when it is clearly in scope or call it out separately.

## Code quality

Prefer code whose intent is visible from structure and naming.

Comments should explain non-obvious intent, constraints, invariants, or trade-offs. Do not narrate syntax.

Keep functions and files cohesive. Split only at a natural responsibility boundary, not to chase arbitrary size targets.

Preserve established naming, error semantics, async model, dependency injection style, data-access style, logging approach, and test patterns.

## Dependencies

Before adding a dependency:

1. confirm the project does not already solve the problem;
2. check stdlib/native support;
3. check installed dependencies;
4. justify the new dependency by meaningful reduction in complexity, risk, or maintenance.

Do not add a package for behavior that can be expressed clearly in a few local lines.

## Error handling

Do not swallow exceptions.

Handle an error only when the current layer can add value by recovering, translating to its domain contract, adding necessary context, releasing or rolling back state, or producing the correct user-facing result.

Otherwise let the established error path handle it.

## Tests

Match the project's existing testing level and style.

Add a regression test when the change fixes non-trivial behavior and a test can fail for the original bug.

Prefer the narrowest test that proves the behavior, then run broader checks when the affected surface or risk requires them.

## Final diff check

Before reporting completion, inspect the diff for accidental files, unrelated edits, duplicated logic, debug code, secrets, commented-out code, unexplained dependency changes, formatting churn, and missing tests or validation.

The final diff should tell one coherent story.
