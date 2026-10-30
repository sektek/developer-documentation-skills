---
name: technical-writing
description: Apply consistent editorial conventions to developer-facing documentation, including READMEs, guides, explanations, and API reference material.
---

# Technical writing

Write accurate, usable documentation for software developers. Apply the editorial policy in [style decisions](../../references/style-decisions.md). Adapt the presentation to the document type and reader's task; do not impose a single structure on every document.

## Before writing

1. Identify the reader, their likely prior knowledge, and what they need to accomplish.
2. Identify the document's purpose: decision support, task completion, conceptual understanding, or lookup.
3. Ground technical claims in the implementation, tests, package metadata, or authoritative project documentation.
4. Record unresolved questions rather than filling gaps with plausible-sounding details.

## Writing conventions

- Lead with the information the reader needs. Use short paragraphs and descriptive headings.
- Prefer direct, active sentences and concrete subjects. Use passive voice when the actor is unknown or unimportant.
- Address the reader as "you" for instructions when natural. Use imperative verbs for steps.
- Prefer familiar words over jargon, but preserve established domain and API terminology.
- Name interfaces, methods, options, and errors exactly as they appear in the source. Do not paraphrase identifiers.
- Use one term for one concept. Explain ambiguous or project-specific terms at first use.
- State prerequisites and consequences before actions when they affect safety or success.
- Distinguish facts, requirements, recommendations, and examples. Do not use "must" for preferences.
- Avoid promotional claims, filler, unnecessary apologies, and unsupported performance or compatibility claims.
- Prefer positive instructions when they are clearer; use explicit prohibitions for important constraints.
- Use examples to clarify a behavior, not as a substitute for explaining necessary conditions.

## Technical accuracy

- Never invent commands, output, supported versions, configuration defaults, or behavior.
- Do not infer runtime guarantees from TypeScript types alone.
- Explain meaningful failure modes and side effects when relevant to the task.
- Keep examples aligned with the public API. Delegate executable example checks to the code-examples skill.
- When a claim cannot be verified, flag it for confirmation or omit it if nonessential.

## Review

Check that a reader can find the answer, distinguish required actions from optional advice, and follow instructions without hidden prerequisites. Check consistent terminology and source-backed technical claims. Use the documentation-review skill for a full review.

Do not silently rewrite the author's technical position merely to satisfy a stylistic preference.
