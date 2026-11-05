---
name: api-research
description: Research a software project's public APIs, terminology, component responsibilities, relationships, intended usage, and behavioral contracts before documenting them.
---

# API research

Establish evidence for how public APIs are used and how related concepts fit together, not merely whether a possible usage compiles. Use this skill when selecting APIs for examples, explaining component relationships, documenting behavior, or resolving uncertainty about supported usage. Skip full research for editorial changes that do not alter technical claims.

## Establish the task and evidence

1. Identify the user's goal, expected audience, and relevant public surface. Limit investigation to the APIs needed for that goal.
2. Inspect public exports, types, implementation, tests, package metadata, existing examples, and repository guidance. Prefer evidence from the actual version being documented.
3. Establish project terminology and component roles from public contracts, usage, and surrounding context. A name may describe a callable contract, an implementation, or a downstream role; distinguish these where relevant. Treat names and familiar patterns as clues rather than proof.
4. Identify relevant relationships and boundaries: who supplies what, where data and control flow, which component owns a responsibility, and what compatibility constraints apply. Distinguish public contracts from incidental implementation structure.
5. Compare plausible entry points. Distinguish recommended convenience APIs from lower-level integration and extension points; don't assume that the first working or most visible example is the preferred usage.
6. Follow the dependency path. Determine what the high-level API constructs or manages by default, what callers must provide, and when explicit injection is warranted for sharing, customization, or lifecycle control.
7. Check meaningful behavioral contracts: defaults, resource ownership, shutdown, errors, retries, concurrency, and relevant guarantees. Investigate only those that affect the task.
8. Reconcile conflicts between implementation, tests, and documentation. Treat implementation as evidence of behavior, not automatic proof of intended usage. Flag ambiguous intent for maintainer review.

## Recommend a usage path (when applicable)

- Prefer the simplest supported public API that preserves the project's intended behavior and minimizes unnecessary caller-managed setup.
- Avoid manually constructing a default dependency when the parent component already creates it, unless the task benefits from sharing or configuring that dependency.
- Avoid lower-level integration APIs merely because they are flexible or easier to discover.
- Identify tradeoffs and exceptions when another usage path is appropriate.
- Do not invent API signatures, defaults, guarantees, or maintainer intent.

## Hand off findings

Provide a concise record of findings relevant to the consuming documentation skill; omit categories that do not apply:

- **Recommended usage:** Public entry point and minimal setup for the task.
- **Alternatives:** When a different API or explicit dependency is appropriate.
- **Contract:** Relevant defaults, lifecycle, and behavior.
- **Concepts and relationships:** Relevant roles, established terminology, interactions, boundaries, and compatibility constraints.
- **Evidence:** Source paths, tests, and documentation supporting the recommendation.
- **Uncertainty:** What is inferred, unresolved, or needs verification.

This is research, not code execution or documentation placement. Use the code-examples skill for executable verification and documentation-workflow for deciding what to write and where.
