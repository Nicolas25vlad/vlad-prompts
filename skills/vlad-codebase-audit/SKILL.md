---
name: vlad-codebase-audit
description: Audit a repository or codebase for actionable technical debt, dead code, YAGNI violations, overengineering, security risks, outdated code/dependencies, maintainability, and a scored remediation plan. Use for whole-codebase health checks, not PR-only reviews.
---

# VLAD Codebase Audit

Perform a **read-only, evidence-led codebase audit**. Find real engineering cost and risk, especially avoidable complexity. Apply YAGNI and Ponytail's minimum-sufficient-action approach: understand the flow, reuse what exists, remove what has no demonstrated job, and prefer small root-cause fixes. Smaller code is not inherently better.

## Audit workflow

1. **Establish scope.** Identify the repository revision, languages, runtime, entry points, architecture, test setup, CI, dependency manifests, and the modules included. Exclude generated, vendored, and build artifacts from source-quality scoring; inspect manifests/lockfiles when checking dependencies. Respect user-specified paths or time budgets.
2. **Map before judging.** Search symbols, references, callers, configuration, tests, and recent change hotspots. Trace representative execution and data flows. Prioritize high-impact code, boundaries, churn, and duplication instead of opening every file indiscriminately.
3. **Inspect risks, in order:** security and authorization; correctness/data integrity; obsolete or unsafe dependencies and deprecated APIs; error/concurrency/resource handling; hard-to-change coupling; repeated patches, duplicate paths, dead code, unnecessary layers, indirection, speculative interfaces, and unused dependencies. For each proposed deletion, check dynamic imports, reflection, configuration, exports, scripts, and external consumers before concluding it is unused.
4. **Validate every candidate.** Cross-check related implementation, test coverage, contract, and framework behavior. Demonstrate an actual failure scenario or concrete maintenance cost. Verify version/deprecation/security-advisory claims against available authoritative evidence; otherwise label them unverified and **do not score** them as findings. Do not treat personal style, age of code, file length, or number of abstractions alone as a defect.
5. **Trace Git history per finding.** Prefer `git blame -L <start>,<end> -- <path>` and `git show --format=fuller <sha>`; use `git log --follow -- <path>` or line history when a move/rename makes blame misleading. Record the **last relevant change** commit, author, and authored date. Distinguish last-touch attribution from the commit that originally introduced the defect; only claim the latter when history supports it. If history is missing/shallow/ambiguous, use `unknown`. Never present authorship as personal fault.
6. **Prioritize fixes.** Favor deletions/simplifications that preserve behavior, removal of confirmed dead paths, existing utilities over new wrappers, and tests that protect the change. Suggest the smallest safe plan (up to three actions per finding); include targeted verification and compatibility/migration safeguards when relevant.
7. **Report only.** Do not change, remove, install, or update code unless the user explicitly asks for implementation. Never print secrets or exploit payloads.

## Severity and score (0–100)

Severity: **P0** critical exploitable/data-loss issue; **P1** major concrete risk; **P2** meaningful maintainability/complexity defect; **P3** minor but verifiable cost. Include confidence (high/medium/low); score only supported findings.

Start at **100 points**, divided into: correctness **25**, security **25**, simplicity/YAGNI **20**, maintainability **20**, verification **10**. Deduct once per distinct root cause from its primary dimension: P0 = 25, P1 = 12, P2 = 5, P3 = 2; cap deductions at that dimension's budget. Cap overall score at **39** if any P0, **79** if any P1. Do not deduct for an unrun test merely because it could not be run; a demonstrated missing safety net can be a finding. Show the five dimension subtotals and deductions so the number is reproducible.

The score is an **estimate of inspected code health**, not a probability of safety. State scope, coverage, checked commands/tests, blind spots, and confidence. Mark the score **provisional** when coverage or verification is limited. If no meaningful code could be inspected, report **score unavailable** rather than inventing one. Zero findings does not prove absence of defects.

## Output contract

Lead with: **revision | audited scope/coverage | quality score /100 (confidence, provisional?) | main risk and fastest win**.

List findings by severity then impact/effort, using this compact record for each:

- **ID · P0–P3 · dimension · confidence · summary**
- **Where/evidence:** `path:start-end`, concrete trace or checked observation, and consequence.
- **Git:** last relevant author, authored date (ISO), abbreviated SHA and commit URL when available; introduction commit separately **only if verified**. Otherwise `unknown (why)`.
- **Attack plan:** 1–3 minimal actions, verification step, effort (S/M/L) and risk of change.

Finish with a short prioritized sequence (now/next/later), dimension score breakdown, checks run/not run, and excluded areas. Avoid giant lists of speculative smells or automatic refactor proposals. If nothing material is found, report that directly.

