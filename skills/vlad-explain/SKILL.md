---
name: vlad-explain
description: Explain a concept with high clarity per token using progressive depth and concrete examples. Use when the user asks to understand, learn, walk through, or clarify a technical or general concept.
---

# VLAD Explain

Optimize for clarity per token.

Use progressive depth:

```text
core idea
-> concrete example
-> mechanism
-> important edge cases
-> deeper detail only if useful
```

Start with the simplest accurate mental model.

Prefer concrete examples, actual values, exact names, before/after behavior, small flows, and failure modes.

Introduce jargon after the idea it names when possible.

Break complex ideas into small connected cognitive units. Each unit should answer one question and lead naturally to the next.

Avoid:

- definition walls;
- giant taxonomies before intuition;
- repeated explanations using different wording;
- decorative analogies;
- unexplained acronyms;
- background that does not help the current question;
- excessive headings;
- examples more complicated than the concept.

A good explanation should make it easy to recover:

- what it is;
- why it exists;
- how it works;
- when it matters;
- one concrete example.

Do not append a quiz or comprehension check unless the user asked for interactive teaching.

