# Debugging module

Use with core/VLAD.md when the task is to diagnose or fix a bug.

## Evidence loop

Use this loop:

~~~text
symptom
-> reproduction/evidence
-> execution path
-> hypothesis
-> discriminating check
-> root cause
-> minimal fix
-> regression verification
~~~

Do not skip from symptom directly to edit unless the cause is already demonstrated.

## Reproduction

Prefer the smallest deterministic reproduction available: one failing test, one request, one command, one input fixture, one stack trace, or one minimal sequence of user actions.

Record the exact observed behavior and expected behavior.

If reproduction is impossible, identify the strongest available evidence and state the limitation.

## Trace the path

Follow data and control flow through only the relevant layers.

For an API bug this may be:

~~~text
request -> controller -> validation -> service -> repository/query -> response
~~~

For each layer, ask where the observed state first diverges from the expected state.

## Hypotheses

Keep the active hypothesis set small.

A useful hypothesis predicts an observable result.

Example:

Hypothesis: userId reaches the service but is omitted from the repository predicate.

Check: inspect the service call and generated query or test spy. If the service forwards userId but the predicate lacks it, the hypothesis is supported.

Do not make several unrelated edits as one experiment.

## Root cause

Fix the earliest responsible layer that can correct the behavior without changing valid callers.

Distinguish root cause, contributing factor, symptom, and unrelated defect.

Do not label a symptom as root cause merely because changing it hides the failure.

## Debug spirals

If multiple fixes fail, stop adding edits.

Re-check whether the reproduction matches the real bug, whether the edited code path actually executes, stale build/cache/process state, hidden configuration or environment differences, and incorrect assumptions about data shape or ownership.

New edits require new evidence.

## Regression

A bug is not complete when the symptom disappears once.

Verify:

1. the original reproduction now passes;
2. the closest sibling behavior still works;
3. existing relevant tests pass;
4. the fix does not rely on test-only mocks that bypass the real failure path.

Report the actual root cause and the verification performed.
