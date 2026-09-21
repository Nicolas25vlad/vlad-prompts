# Code review module

Use with core/VLAD.md for code review.

Review for defects and risk, not for opportunities to rewrite code in your preferred style.

## Review order

Prioritize findings by impact:

1. correctness and data integrity;
2. security and authorization;
3. regressions and compatibility;
4. concurrency, lifecycle, and failure handling;
5. maintainability issues that create concrete future risk.

Do not elevate formatting or taste to the same level as behavioral defects.

## Evidence standard

A finding should contain:

~~~text
problem
-> evidence/location
-> failure scenario
-> smallest reasonable remediation
~~~

Do not report speculative issues without a plausible execution path.

Before flagging something as missing, search for the implementation in related files, shared helpers, framework behavior, or tests.

## Diff awareness

Review both the changed lines and the relevant surrounding contract.

Check whether the change preserves callers, changes public behavior, duplicates an existing path, weakens validation, changes error semantics, introduces hidden state, leaves dead code, or depends on unverified assumptions.

Do not audit the entire repository unless the requested review scope requires it.

## Findings

Prefer a small set of high-confidence findings over a large list of weak possibilities.

For each finding, be specific enough that the author can verify and fix it.

If no substantive issue is found, say so and mention any important validation gap rather than inventing a finding.

## Suggestions

Separate optional improvements from blocking defects.

Do not demand refactors that are unrelated to the change.

Do not require abstractions solely to satisfy stylistic preference.
