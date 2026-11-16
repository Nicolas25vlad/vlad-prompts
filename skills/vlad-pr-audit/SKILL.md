---
name: vlad-pr-audit
description: Pre-review a pull request, branch, staged changes, or diff for YAGNI/overengineering, code quality, security, regressions, unnecessary changes, maintainability, and a 0-100 score with Git-attributed findings and small fix plans. Use before requesting human PR review.
---

# VLAD PR Audit

Perform a **read-only, pre-submission quality gate** on the proposed change, not a full repository audit. Focus on YAGNI, Ponytail's minimal-correct-change approach, clean maintainable code, and proven security/correctness risks. Do not reward deleting necessary safeguards, splitting code into ornamental abstractions, or blindly minimizing line count.

## Review workflow

1. **Pin the comparison.** Determine the PR base/head SHA from PR metadata, or the explicit target branch and `git merge-base` for a local branch. For staged/uncommitted review use the actual requested index/worktree diff and label it. Record refs and whether worktree changes are included; never silently compare against an assumed base.
2. **Read the complete diff** (including added, modified, deleted, renamed files) and locate impacted entry points, callers, types, tests, config, migrations, and interfaces. Read just enough surrounding code to understand contracts and check whether a shared implementation already exists. Treat generated files and lockfile churn separately.
3. **Evaluate newly introduced or worsened concerns:** authorization/data exposure, correctness/regressions, failure handling, new dependencies or obsolete APIs, needless wrappers/interfaces/config toggles, speculative extensibility, duplicated logic, dead branches, over-broad change scope, hard-to-maintain coupling, and missing tests for risky behavior. Prefer existing project solutions -> standard library -> native feature -> installed dependency -> new abstraction. Suggest deletion only after checking consumers and compatibility.
4. **Verify with evidence.** Check relevant tests, type/lint/build and CI if accessible; distinguish passed, failed, and not run. For each finding, cite the changed `path:line` (or base line for deletion), a concrete failure or future maintenance cost, and the smallest fix. Check authoritative docs/advisories before claiming a version/dependency is insecure or obsolete. Do not score speculative smells, formatting preferences, or unrelated pre-existing debt.
5. **Trace the responsible change.** Use PR commits and `git blame` on head for added/modified lines; inspect `git log <base>..<head> -- <path>` and `git show` to corroborate. For removed lines, inspect base history and the removing commit. Record **change commit, author, authored date**, and link when verifiable. When a rebase, squash, dirty worktree, rename, or shallow history prevents attribution, write `unknown` instead of guessing. Last-touch does not establish fault or introduction.
6. **Decide readiness.** Only mark **ready for human review** when no blockers are found and essential checks are satisfactory. Otherwise label **fix before review** or **needs verification** with concrete conditions. Do not auto-approve, merge, push, or change files.

## Severity and score (0–100)

Use **P0** critical exploitable/data-loss issue; **P1** major concrete risk; **P2** meaningful maintainability/complexity defect; **P3** minor but demonstrated cost. Attach evidence confidence; score supported findings only.

Start at **100** for the **proposed change**, across correctness **25**, security **25**, simplicity/YAGNI **20**, maintainability **20**, verification **10**. Deduct once per distinct root cause in its main dimension: P0 = 25, P1 = 12, P2 = 5, P3 = 2; cap deductions by dimension. Cap overall score at **39** when any P0 exists or **79** with any P1. Show dimension subtotals and each deduction. Do not deduct merely because unavailable tools prevented running tests, but mark the result provisional; verified risky missing coverage can be scored.

Rate **what the PR adds or makes worse**, not all legacy code it touches. A clean diff can earn a high score even in a troubled codebase. Always state coverage, checks, confidence, and whether score is **provisional**. If the relevant diff is unavailable, **score unavailable**, not 100. The percentage is a transparent heuristic, not a probability that the PR is bug-free.

## Output contract

Open with: **PR/branch + base...head | changed files/scope | score /100 (confidence/provisional) | READY / FIX BEFORE REVIEW / NEEDS VERIFICATION**.

For each finding (blockers first), include:

- **ID · P0–P3 · dimension · confidence · one-line summary**
- **Diff evidence:** `path:head-line` or `path:base-line (deleted)`, factual effect and reproducible failure/maintenance scenario.
- **Git:** relevant PR commit abbreviated SHA/link, author, authored date (ISO), or `unknown` with reason; separately note historical context when useful.
- **Attack plan:** up to three minimal edits, focused test/check, effort S/M/L.

End with **must fix**, **optional simplifications**, **checks passed/failed/not run**, **dimension-score breakdown**, and any unreviewed portions. If no real findings exist, explicitly state that rather than manufacturing recommendations.

