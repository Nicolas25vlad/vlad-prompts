# VLAD scope coverage

This file is a regression guard for the intended behavioral scope.

The canonical `core/VLAD.md` should continue to cover every category below. A future optimization that removes one of these areas must be deliberate, justified, and reflected here.

| Required behavior | Canonical section |
|---|---|
| Clear behavioral hierarchy | 1. Behavioral hierarchy |
| General task loop | 2. Operating model |
| Answer / explain / research / diagnose / implement / review distinction | 3. Classify the task before acting |
| Input normalization | 4. Input normalization |
| Efficient, non-conversational reasoning | 5. Reasoning discipline |
| Autonomy and material ambiguity policy | 6. Ambiguity and autonomy |
| Minimum sufficient action | 7. Minimum sufficient action |
| Avoid overplanning | 8. Planning |
| Tool grounding and tool-spam prevention | 9. Tool use |
| Context efficiency and selective retrieval | 10. Context efficiency |
| Prompt/token caching layout | 10. Context efficiency |
| Quality-per-token optimization | 11. Token efficiency |
| Read before edit / preserve user work | 12. File and repository work |
| Coding-agent workflow | 13. Coding |
| Existing-pattern reuse / no premature abstractions | 13. Coding |
| Correct architectural layer | 14. Change placement and architecture |
| Evidence-driven debugging | 15. Debugging |
| Code-review behavior | 16. Code review |
| Error propagation / no swallowed failures | 17. Error handling |
| Verification proportional to risk | 18. Verification |
| Honest completion claims | 18. Verification |
| Research source quality and freshness | 19. Research and factual work |
| Progressive, clear explanations | 20. Explanation and technical communication |
| Technical writing clarity | 20. Explanation and technical communication |
| Proportional response shape | 21. User-visible response shape |
| Long-task state and context compaction | 22. Long tasks |
| Matter-of-fact failure handling | 23. Errors and corrections |
| Deterministic decision rules | 24. Determinism and predictability |
| Explicit anti-pattern suppression | 25. Anti-patterns |
| Final behavioral self-check | 26. Completion criteria |

## Specialized modules

The full core must be useful alone.

Modules are allowed to deepen behavior, but the fundamental behavior cannot exist only in a module.

Examples:

- `coding/coding.md` deepens repository reconnaissance, dependencies, testing, and diff discipline.
- `coding/debugging.md` deepens reproduction, hypothesis testing, and regression behavior.
- `coding/review.md` deepens review-specific evidence standards.
- `research/research.md` deepens search and source synthesis.
- `explanation/explanation.md` deepens progressive explanation.

## Compact build

`core/VLAD.compact.md` is intentionally not expected to reproduce this entire matrix.

Its job is to preserve the highest-leverage behavior when instruction space is constrained.

When the compact build and full core differ, the full core defines VLAD.
