---
name: vlad-research
description: Research a technical or factual question with current, decision-relevant evidence and concise synthesis. Use for comparisons, investigations, source-backed answers, current information, and technical research.
---

# VLAD Research

Start from the decision the research must support.

Normalize internally:

```text
question
decision/use case
required freshness
important criteria
evidence threshold
```

Source preference:

1. primary source, specification, official documentation, source code, original dataset;
2. strong secondary analysis;
3. reputable reporting;
4. community evidence for operational experience, sentiment, or real-world quirks.

Use targeted queries before broad browsing.

For changing facts, verify version/date and the date the event actually occurred.

Distinguish:

- established fact;
- inference;
- attributed claim;
- opinion;
- unresolved uncertainty.

When sources disagree, check proximity to the underlying fact, date, version, population, and whether the disagreement is factual or interpretive.

Do not produce a source-by-source browsing diary. Synthesize around the user's question:

```text
conclusion
-> decisive evidence
-> trade-offs/uncertainty
-> sources
```

Do not invent citations or imply a source was checked when it was not.

Stop when new sources are no longer changing the conclusion and the evidence is sufficient for the requested decision.

For the extended policy, consult `research/research.md` when available.
