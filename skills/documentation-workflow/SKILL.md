# Documentation workflow

Stages: (1) Discover source, tests, exports, package metadata, and existing docs. (2) Decide whether documentation needs changing and select the appropriate location. (3) Outline sections, audience, evidence needs, and unknowns. (4) Draft from the outline. (5) Verify links and code examples, iterating on failures. (6) Review technical and editorial quality.

Run autonomously by default. Support optional human approval checkpoints after any stage. Persist the outline and verification results even in autonomous mode. Each stage can be invoked independently. Do not invent missing implementation details; flag uncertainties. Verification and review may return work to drafting.

## Decide whether and where to document

A code change does **not** imply a README change, or even a documentation change. Before editing, ask:

1. Does existing documentation become inaccurate or incomplete for its intended audience?
2. Does the change affect a public contract, supported workflow, or important user-facing behavior? Internal-only changes and bug fixes that restore already-documented behavior often need no new user-facing documentation.
3. What is the narrowest useful location for the information, following the repository's established documentation structure?
4. Would a brief README mention or link materially improve discovery for someone evaluating or starting with the project?

Choose by reader need rather than by the file most convenient to edit:

- **README:** Project purpose, primary capabilities, first useful task, and navigation. Add material only when it changes what an arriving reader needs to understand or find.
- **How-to guide:** Steps to accomplish a specific task, including optional or advanced workflows.
- **Reference:** API signatures, options, configuration, defaults, and exhaustive behavior details.
- **Explanation or architecture:** Rationale, mental models, tradeoffs, and design decisions.
- **Migration guide or changelog:** Breaking changes, upgrade actions, and release history.
- **No user-facing change:** Internal refactors or changes that do not affect the documented contract.

Correct outdated documentation at its source; do not duplicate it in the README. Prefer linking from an entry point to detailed material over copying the detail. Respect existing repository conventions when they serve the reader.

If proposing a README edit, state why it belongs at the entry point rather than in a focused document. **No documentation change** is a valid outcome; record the decision briefly when the workflow is driven by a code change.
