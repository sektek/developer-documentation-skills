---
name: readme
description: Create, revise, or review README files for software projects, libraries, and repositories.
---

# README authoring

Create a README that helps a developer decide whether the project meets their needs, accomplish a first useful task, and find the next level of documentation. Treat it as an entry point, not an exhaustive manual.

Before updating a README in response to a code change, apply the placement decision in [documentation-workflow](../documentation-workflow/SKILL.md). A change does not automatically warrant a README edit; prefer focused documentation and a link when needed for discovery.

Apply the [technical-writing](../technical-writing/SKILL.md), [markdown-authoring](../markdown-authoring/SKILL.md), and [code-examples](../code-examples/SKILL.md) skills as needed. Follow the repository's existing documentation conventions where they do not conflict with accuracy.

## Discover before drafting

Inspect available evidence, including:

- Package metadata, exports, supported runtimes, installation and build instructions.
- Existing README and linked documentation, examples, tests, and public APIs.
- The project's actual purpose, supported use cases, and meaningful limitations.
- Existing terminology and intended developer audience.

Identify unknowns explicitly. Do not invent capabilities, installation commands, compatibility claims, or working examples. For an existing README, preserve correct, useful content and links unless there is a reason to change them.

## Plan the reader's path

Create a short outline before drafting. Decide which questions the README must answer and in what order. Usually:

1. **What is this?** Describe the project and its practical purpose in one or two short paragraphs.
2. **When would I use it?** Show the problem it addresses and, when helpful, what it deliberately does not address.
3. **How do I start?** State prerequisites and installation, then provide the shortest useful working example.
4. **What else can it do?** Highlight a small set of meaningful capabilities, ideally with links or compact examples.
5. **Where do I go next?** Link to guides, reference documentation, examples, contributing information, and other relevant resources.

This is a decision framework, not a mandatory section template. Omit irrelevant sections and adapt ordering to the project. For an application, emphasize setup and running it; for a library, emphasize its public API and use cases; for a monorepo, help readers find the appropriate packages.

## Write the README

- Lead with a concrete value proposition rather than marketing language or an abstract architecture tour.
- Explain the minimum mental model needed to understand the first example. Introduce additional concepts when they become useful.
- Prefer a complete, realistic first example over a catalog of isolated API calls.
- Include imports, setup, and expected behavior where they are necessary for the example to work.
- Organize additional capabilities around tasks or outcomes, not merely a list of exported names.
- Keep advanced architecture, exhaustive configuration, and full API reference in linked documents when possible.
- Provide clear navigation with descriptive links. Do not create dead links to documentation that does not exist.
- Use accurate, conscious language and the project's exact identifiers; do not silently rename API symbols.

Avoid a fixed word count. A README should be as long as necessary to make the first steps successful and as short as practical for scanning.

## Verify

Use the code-examples skill to verify snippets against the repository. Report the actual level of evidence for each example: Verified, Type-checked, Inspected, Unverified, or Failed.

Check installation commands, paths, package names, version claims, and relative links against available evidence. If checks cannot be performed, state the limitation rather than implying success. Do not modify production code to accommodate documentation.

Use the documentation-review skill for a final pass on accuracy, audience fit, clarity, and navigability.

## Deliverables

Provide:

- The updated README.
- A retained outline or concise record of the intended reader journey.
- A verification summary identifying what was checked and what remains uncertain.

When asked only to review or propose an outline, do not rewrite the README without authorization.

