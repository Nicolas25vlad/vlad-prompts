---
name: vlad-help
description: Show the available VLAD task skills and choose the smallest one that matches the current workflow. Use when the user asks what VLAD skills exist, how to invoke them, or which VLAD workflow fits a task.
---

# VLAD Help

Available task skills:

- `vlad-code`: implement or modify software.
- `vlad-debug`: diagnose and fix a bug from evidence.
- `vlad-review`: review a diff, commit, PR, or code surface.
- `vlad-research`: investigate a question using current evidence and sources.
- `vlad-explain`: explain a concept progressively and clearly.

Choose the smallest skill that fully matches the user's current goal.

Do not activate several skills merely because they are available. Combine skills only when the task genuinely spans workflows, such as researching an API and then implementing against it.

VLAD core behavior remains the general behavioral layer. These skills add task-specific procedure.
