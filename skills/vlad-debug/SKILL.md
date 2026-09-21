---
name: vlad-debug
description: Diagnose and fix bugs using evidence, a small hypothesis set, root-cause analysis, and regression verification. Use when behavior is broken, tests fail, an error occurs, or the user asks why something is not working.
---

# VLAD Debug

Treat the user's report as a symptom, not automatically as the root cause.

Use:

```text
symptom
-> reproduction/evidence
-> relevant path
-> hypothesis
-> discriminating check
-> root cause
-> minimal fix
-> regression verification
```

1. Establish the exact observed and expected behavior.
2. Prefer the smallest deterministic reproduction: one failing test, request, command, input, stack trace, or UI sequence.
3. Trace only the relevant execution path and find where actual state first diverges from expected state.
4. Keep the active hypothesis set small. A useful hypothesis predicts an observable result.
5. Verify the hypothesis before editing when practical.
6. Fix the earliest responsible layer that corrects the behavior without breaking valid callers.
7. Re-run the original reproduction and the closest sibling behavior.

Do not:

- shotgun-debug;
- change several unrelated things in one experiment;
- patch a client symptom when the server/shared layer owns the bug;
- hide a failure with mocks, broad catches, fallbacks, or retries;
- keep trying variants of the same failed fix without new evidence.

If repeated attempts fail, stop editing and challenge the assumptions: wrong execution path, stale process/build/cache, configuration/environment difference, unexpected data shape, framework behavior, or incorrect reproduction.

If the user asked only for diagnosis, stop after a supported root cause unless implementation is clearly included in scope.

Report:
```text
root cause
evidence
fix, if requested
verification
```

