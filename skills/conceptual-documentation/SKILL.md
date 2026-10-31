---
name: conceptual-documentation
description: Write, revise, or review conceptual developer documentation that explains a system's mental model, key ideas, and relationships without duplicating API reference or how-to guides.
---

# Conceptual documentation

Explain the ideas a developer needs to understand a library, application, or system. Focus on **how to think about it**: the roles of its concepts, how they relate, and the consequences of those relationships. Conceptual documentation is an explanation, not a tutorial, task procedure, API catalog, or implementation inventory.

Apply [technical-writing](../technical-writing/SKILL.md) and [markdown-authoring](../markdown-authoring/SKILL.md). Use [api-research](../api-research/SKILL.md) to ground claims in real contracts and usage, [documentation-workflow](../documentation-workflow/SKILL.md) to determine whether and where the document belongs, and [documentation-review](../documentation-review/SKILL.md) to review the result. Use [code-examples](../code-examples/SKILL.md) for executable illustrations.

## Decide whether an explanation is needed

1. Identify the reader and the **conceptual question** they cannot readily answer from existing documentation. Examples include how components cooperate, why a boundary exists, or how to choose among related concepts.
2. Inspect existing README, guides, API docs, and conceptual material. If a short clarification or link in an existing document would suffice, prefer that to creating another page.
3. State the **central conceptual insight** in one sentence before drafting: what should the reader understand afterward that a catalog of APIs would not teach? Organize the explanation to develop that insight. If no distinct insight emerges, reconsider whether a separate document is needed.
4. Define one coherent scope. Do not create a separate page for every class, concept, or pattern by default.
5. Use the documentation-workflow skill to choose placement **and a discoverable entry point** (such as an existing README or docs index); do not prescribe a directory structure or require conceptual documentation for every repository.

## Establish an evidence-based mental model

- Investigate public contracts, usage examples, call sites, tests, and existing explanations before assigning responsibilities. Treat names and familiar design-pattern vocabulary as clues, not proof.
- Establish terminology from the project. A term may name a callable contract, a component implementing it, and a role in a larger composition. Explain the distinction when it matters rather than forcing one universal definition.
- Identify the essential concepts and **relationships between them**: who supplies what, how information or control flows, which component owns a decision, and where responsibilities begin and end.
- Separate what the public design promises from what happens to be true of the current implementation. Avoid narrating source files, inheritance trees, or development history as a substitute for explaining the model.
- Verify meaningful assertions against evidence. When behavior or intent is ambiguous, flag the uncertainty for human review instead of inventing a coherent-sounding architecture.

## Write the explanation

- Open with the question or mental model the document answers and why understanding it matters to the reader.
- Organize around the central insight, ideas, and relationships, not a parade of exported classes. Explain how the parts work together and what choices or expectations follow from that arrangement.
- Use a small illustrative scenario or diagram when it makes a relationship clearer. Illustrations should clarify the model rather than become a runnable walkthrough or a complete implementation.
- Explain tradeoffs, boundaries, and consequences when they help the reader reason about usage. Avoid unverified design rationales or retrospective claims about why authors chose an approach.
- Link to relevant public declarations, how-to guides, and references for exact APIs and procedures. Do not duplicate signatures, option tables, event lists, or step-by-step instructions.
- Favor precise, consumer-relevant statements over exhaustive lists of what the system does not do. Document negative guarantees when they materially affect the mental model.
- Keep the explanation useful independently of a specific version's internal organization where possible; never conceal genuine version-specific constraints.

## Verify and deliver

- Check each significant concept, relationship, and guarantee against the inspected evidence; note unresolved questions explicitly.
- Review for plausible but unsupported architectural claims, misleading conventional terminology, redundancy with existing docs, and unexplained leaps between concepts.
- Check whether previous review findings or memorable edge cases have been overemphasized at the expense of the reader's actual question. Use past mistakes to improve verification, not as mandatory topics for every new explanation.
- Verify relative links from the document's actual directory, confirm that targets exist, and check that readers can discover the explanation from an appropriate entry point. Inspect diagrams and examples where tooling permits. Do not claim that a conceptual explanation is verified solely because code compiles or lint passes.
- Report the intended reader and conceptual question, where the document belongs, what evidence supports it, and any uncertainties needing a human decision.
