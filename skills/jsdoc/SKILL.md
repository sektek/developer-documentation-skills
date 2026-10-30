---
name: jsdoc
description: Write, complete, or review JSDoc and TSDoc-style comments on JavaScript and TypeScript declarations, especially public library APIs.
---

# JSDoc authoring

Document the contract a caller needs to use an API correctly. Favor thorough, useful documentation of the public contract, including generic type parameters and options. TypeScript declarations express structure but do not replace explanations of roles, relationships, defaults, or intended usage. Apply [technical-writing](../technical-writing/SKILL.md); use [api-research](../api-research/SKILL.md) when behavior, intended usage, or ownership is uncertain.

## Select the scope

1. Follow the requested files, declarations, or exported surface. For a documentation coverage pass, prioritize exported classes, interfaces, types, functions, methods, properties, and options that consumers encounter.
2. Inspect existing comments, declarations, implementations, tests, and nearby conventions. Follow the project's chosen JSDoc/TSDoc tags and documentation generator, if any.
3. Preserve accurate comments and avoid reformatting unrelated code. Do not modify implementation, exported types, signatures, or runtime behavior merely to satisfy documentation.

## Establish intent and documentation ownership

- Determine a declaration's **primary purpose** from its public role, naming, usage, and surrounding architecture before writing its summary. Implementation mechanics and optional secondary behavior must not displace that purpose. For example, a filter with an optional rejection handler remains a filter, not a router.
- Give each fact one natural documentation home. Class documentation explains the component's purpose and essential usage; event types describe emitted events; options and properties describe configuration; methods describe invocation-specific contracts. Link related declarations rather than restating their details.
- Do not narrate a class's implementation, list all of its events, or enumerate its options when dedicated public declarations already document them. Repeat a detail only when it is essential to understand the higher-level contract without navigating elsewhere.
- Before drafting, inspect the related public types and existing JSDoc to identify what is already documented. After drafting, check for duplicated information and for descriptions that overemphasize incidental behavior.

## Describe the contract

- Start with a clear summary of what the declaration does or represents, written for its caller. Expand with paragraphs or short lists when they explain responsibilities, intended use, interactions with other components, or important behavior. Do not impose an artificial brevity limit.
- Document important semantics not visible in types: defaults, units, valid ranges, ordering, side effects, resource ownership, disposal, errors, retries, and guarantees. Include only what is relevant and supported by evidence.
- For public functions and methods, ordinarily document each parameter with `@param` and the result with `@returns` where applicable, including what values mean or how they are used. Use `@throws` for meaningful, verified failure contracts. Avoid tautologies, but do not omit a useful tag solely because TypeScript declares the type.
- Document **every generic type parameter** on public generic declarations with `@template`, including what it represents, how it flows through the API, and the meaning of defaults or constraints where applicable. Describe the role of each parameter, not merely its type or letter. Match existing repository conventions for `@template` formatting.
- Document public options types and their properties, including required inputs, optional defaults, and behavioral consequences. Use `{@link ...}` to connect related declarations when supported by repository conventions. Avoid copying the same detailed explanation into every consuming method.
- For overloads, explain behavior that differs between call forms. For inherited or implemented members, avoid redundant comments unless the implementation changes meaningful behavior.
- Use `@example`, `@see`, `@deprecated`, and other supported tags only when they provide real value. Deprecation guidance must name a verified replacement or explain that none is known.
- Use valid JSDoc syntax and precise identifiers. Keep examples small, copyable, and aligned with public APIs; apply [code-examples](../code-examples/SKILL.md) when adding executable examples.

## Keep development history out of JSDoc

JSDoc describes the **current public contract**, not the history of how the implementation arrived there. Do not include ticket or issue IDs, PR references, review discussions, incident narratives, implementation chronology, or explanations such as "changed to this approach because of issue X." Do not use JSDoc to bypass a repository's restrictions on implementation comments.

Document the observable behavior, constraints, or caveats that callers need to know, without the development backstory. If the rationale itself must be preserved, use an appropriate design document, ADR, issue, or PR discussion rather than attaching it to an API declaration. A reference to an external issue is appropriate only when it is itself part of an explicitly requested, consumer-relevant public contract and repository conventions permit it.

## Avoid misleading comments

- Do not infer runtime validation, immutability, delivery guarantees, exception types, or cleanup behavior from static types alone.
- Do not promise that a promise resolves at a stronger milestone than implementation establishes.
- Distinguish an API's own responsibilities from those of injected dependencies.
- Do not invent intent or behavior to fill gaps. Flag unresolved questions rather than asserting guesses.
- Avoid filler such as "Gets the value" for `getValue()`, but prefer a concrete description of the value's role over omitting documentation for a public member. Do not spend coverage effort on self-evident private implementation details unless specifically requested.

## Verify and deliver

Review comment placement, syntax, tag names, referenced symbols, and links. Run the repository's configured ESLint checks for affected files, including any JSDoc-related rules. Use the project's existing ESLint command and configuration rather than assuming a particular plugin or rule set. Fix documentation-related lint findings without disabling rules or making unrelated implementation changes. Where available, also run the documentation generator or type-checker when relevant. If ESLint is unavailable or no JSDoc rules are configured, state that limitation; a passing ESLint run alone does not prove the comments are accurate. Report the commands run and results; do not claim validation without evidence.

Report which declarations were documented, any unresolved contract questions, and verification limitations. A coverage pass should identify intentionally undocumented declarations rather than manufacturing low-value comments to reach a percentage.
