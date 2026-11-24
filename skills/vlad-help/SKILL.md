---
name: vlad-help
description: Show the available VLAD task skills and choose the smallest one that matches the current workflow. Use when the user asks what VLAD skills exist, how to invoke them, or which VLAD workflow fits a task.
---

# VLAD Help

Available task skills:

- `vlad-discuss`: collaboratively challenge and refine ideas, architecture, trade-offs and implementation plans without changing code.
- `vlad-code`: implement or modify software.
- `vlad-doomscroll`: stay focused on an authorized coding task without unnecessary questions or premature stopping; interrupt only for material blockers.
- `vlad-debug`: diagnose and fix a bug from evidence.
- `vlad-review`: focused defect/risk review of code, a diff, commit, or PR.
- `vlad-codebase-audit`: audit repository health, complexity, debt, security, maintainability and Git history with a quality score.
- `vlad-pr-audit`: score a proposed PR/branch/diff before human review, including attributable findings and minimal fixes.
- `vlad-research`: investigate a question using current evidence and sources.
- `vlad-explain`: explain a concept progressively and clearly.

Choose the smallest skill that fully matches the user's current goal.

Do not activate several skills merely because they are available. Combine skills only when the task genuinely spans workflows, such as researching an API and then implementing against it.

VLAD core behavior remains the general behavioral layer. These skills add task-specific procedure.
