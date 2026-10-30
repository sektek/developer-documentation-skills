---
name: api-research
description: Investigate a software project's public APIs, intended usage patterns, defaults, and behavioral contracts before documenting or demonstrating them.
---

# API research

Establish how a public API is intended to be used, not merely whether a possible usage compiles. Use this skill when selecting APIs for examples, documenting behavior, or resolving uncertainty about supported usage. Skip full research for editorial changes that do not alter technical claims.

## Establish the task and evidence

1. Identify the user's goal, expected audience, and relevant public surface. Limit investigation to the APIs needed for that goal.
2. Inspect public exports, types, implementation, tests, package metadata, existing examples, and repository guidance. Prefer evidence from the actual version being documented.
3. Compare plausible entry points. Distinguish recommended convenience APIs from lower-level integration and extension points; don't assume that the first working or most visible example is the preferred usage.
4. Follow the dependency path. Determine what the high-level API constructs or manages by default, what callers must provide, and when explicit injection is warranted for sharing, customization, or lifecycle control.
5. Check meaningful behavioral contracts: defaults, resource ownership, shutdown, errors, retries, concurrency, and relevant guarantees. Investigate only those that affect the task.
6. Reconcile conflicts between implementation, tests, and documentation. Treat implementation as evidence of behavior, not automatic proof of intended usage. Flag ambiguous intent for maintainer review.

## Recommend a usage path

- Prefer the simplest supported public API that preserves the project's intended behavior and minimizes unnecessary caller-managed setup.
- Avoid manually constructing a default dependency when the parent component already creates it, unless the task benefits from sharing or configuring that dependency.
- Avoid lower-level integration APIs merely because they are flexible or easier to discover.
- Identify tradeoffs and exceptions when another usage path is appropriate.
- Do not invent API signatures, defaults, guarantees, or maintainer intent.

## Hand off findings

Provide a concise record for the consuming documentation skill:

- **Recommended usage:** Public entry point and minimal setup for the task.
- **Alternatives:** When a different API or explicit dependency is appropriate.
- **Contract:** Relevant defaults, lifecycle, and behavior.
- **Evidence:** Source paths, tests, and documentation supporting the recommendation.
- **Uncertainty:** What is inferred, unresolved, or needs verification.

This is research, not code execution or documentation placement. Use the code-examples skill for executable verification and documentation-workflow for deciding what to write and where.
