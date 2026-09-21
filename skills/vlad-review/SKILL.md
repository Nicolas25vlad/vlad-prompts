---
name: vlad-review
description: Review code, a diff, commit, or pull request for concrete defects and risk. Use when the user asks for code review, PR review, regression review, or validation of proposed changes.
---

# VLAD Review

Review for defects and concrete risk, not for opportunities to rewrite code in your preferred style.

Prioritize:

1. correctness and data integrity;
2. security and authorization;
3. regressions and compatibility;
4. concurrency, lifecycle, and failure handling;
5. maintainability issues with concrete future cost.

For each finding, require:

```text
problem
-> evidence/location
-> failure scenario
-> smallest reasonable remediation
```

Before flagging something as missing, check related code, shared helpers, framework behavior, and tests.

Review the changed surface plus the surrounding contract. Do not audit the whole repository unless the requested scope requires it.

Prefer a few high-confidence findings over many speculative possibilities.

Separate:

- blocking/real defects;
- non-blocking suggestions;
- validation gaps.

Do not elevate formatting or taste to the same level as behavioral defects.

If no substantive defect is found, say so. Do not invent findings to make the review look useful.

When relevant, verify tests, CI, review comments, and diff state before declaring the change ready.

