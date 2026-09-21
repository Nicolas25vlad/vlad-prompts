---
name: vlad-code
description: Implement or modify software with VLAD's minimal, evidence-first workflow. Use for feature work, requested refactors, configuration changes, repository edits, and other coding tasks where the user wants changes made.
---

# VLAD Code

Treat the user's current request as the implementation target.

Apply the active global/system instructions first. Then use this workflow:

```text
understand -> locate -> trace -> reuse -> implement -> verify -> diff
```

1. **Understand**
   - Extract the concrete goal, constraints, and success criteria.
   - Do not invent extra features or cleanup.

2. **Locate**
   - Search for the smallest relevant code surface before broad reading.
   - Read the files you will change and the nearest relevant tests/config.
   - Look for existing implementations or project patterns before creating new ones.

3. **Trace**
   - Understand the real data/control flow through the affected layers.
   - Put the change in the layer that owns the responsibility.

4. **Reuse**
   Prefer, in order:
   ```text
   existing project solution
   -> standard library
   -> native platform capability
   -> installed dependency
   -> small local implementation
   -> new dependency/abstraction
   ```

5. **Implement**
   - Make the smallest complete change.
   - Match existing naming, architecture, error semantics, async style, data access, logging, and tests.
   - Avoid unrelated refactors, premature abstractions, dependency reflex, obvious comments, silent hacks, and swallowed exceptions.
   - Preserve unrelated user changes.

6. **Verify**
   - Run the smallest check that can falsify the success claim.
   - Expand verification with risk: focused test, typecheck/lint, integration test, build, runtime check, CI, migration check.
   - If verification is unavailable, state that instead of implying success.

7. **Diff**
   - Inspect the final diff for accidental files, unrelated churn, debug code, secrets, duplicate logic, and missing validation.

Report:
```text
result
important changes
verification
remaining limitation only if material
```

For the extended policy, consult `coding/coding.md` when it is available and relevant.
