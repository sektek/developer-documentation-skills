---
name: jsdoc
description: Write, complete, or review JSDoc and TSDoc-style comments on JavaScript and TypeScript declarations, especially public library APIs.
---

# JSDoc authoring

Document the contract a caller needs to use an API correctly. Favor thorough, useful documentation of the public contract, including generic type parameters and options. TypeScript declarations express structure but do not replace explanations of roles, relationships, defaults, or intended usage. Apply [technical-writing](../technical-writing/SKILL.md) and use [api-research](../api-research/SKILL.md) to establish relevant purpose, terminology, behavior, and relationships when writing technical claims.

## Select the scope

1. Follow the requested files, declarations, or exported surface. For a documentation coverage pass, prioritize exported classes, interfaces, types, functions, methods, properties, and options that consumers encounter.
2. Inspect existing comments, declarations, implementations, tests, and nearby conventions. Check the project's JSDoc/TSDoc tag syntax and configured lint rules before drafting, especially requirements for `@throws`, `@template`, `@param`, and `@returns`. Do not infer a project's rules solely from examples or assume that another project's conventions apply.
3. Preserve accurate comments and avoid reformatting unrelated code. Do not modify implementation, exported types, signatures, or runtime behavior merely to satisfy documentation.

## Establish intent and documentation ownership

- Use api-research findings to identify a declaration's primary public purpose and established terminology. Keep the summary focused on that purpose rather than secondary behavior or implementation mechanics. Flag unresolved intent rather than guessing.
- Give each fact one natural documentation home. Class documentation explains the component's purpose and essential usage; related types describe their own contracts; options and properties describe configuration; methods describe invocation-specific behavior. **Connect readers to useful related declarations** with supported documentation links rather than repeating their details. Prioritize links that help consumers discover capabilities, configuration, results, or constraints; avoid links that merely restate inheritance or implementation details.
- Do not narrate a class's implementation or enumerate details already documented by dedicated public declarations. When those details are important to consumers, provide a concise contextual pointer to their documentation. Repeat a detail only when it is essential to understand the higher-level contract without navigating elsewhere.
- Before drafting, inspect the related public types and existing JSDoc to identify what is already documented. After drafting, check for duplicated information and for descriptions that overemphasize incidental behavior.

## Describe the contract

- Start with a clear summary of what the declaration does or represents, written for its caller. Expand with paragraphs or short lists when they explain responsibilities, intended use, interactions with other components, or important behavior. Do not impose an artificial brevity limit.
- Document important semantics not visible in types: defaults, units, valid ranges, ordering, side effects, resource ownership, disposal, errors, retries, and guarantees. Include only what is relevant and supported by evidence. Frame these as **positive, consumer-relevant guarantees and behavior**, not inventories of capabilities the API lacks. Describe an absence or limitation only when it is a surprising, material part of the contract that callers must account for.
- For public functions and methods, ordinarily document each parameter with `@param` and the result with `@returns` where applicable, including what values mean or how they are used. Use `@throws` for meaningful, verified failure contracts, following the project's required exception-type and description syntax. Do not invent a specific exception type merely to satisfy a rule; flag unknown types when the tooling requires one. Avoid tautologies, but do not omit a useful tag solely because TypeScript declares the type.
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
- Do not invent intent or behavior to fill gaps. Flag unresolved questions rather than asserting guesses. Avoid phrases such as "the current implementation" that make documentation sound like a snapshot of internals instead of a stable API contract; if a behavior appears to be a bug or conflicts with intended semantics, flag it for review rather than normalizing it in JSDoc.
- Avoid filler such as "Gets the value" for `getValue()`, but prefer a concrete description of the value's role over omitting documentation for a public member. Do not spend coverage effort on self-evident private implementation details unless specifically requested.

## Verify and deliver

Review comment placement, syntax, tag names, referenced symbols, and links. Run the repository's configured ESLint checks for affected files, including any JSDoc-related rules. Pay particular attention to newly introduced tags and their required types, descriptions, and formatting; correct violations before delivery. Use the project's existing ESLint command and configuration rather than assuming a particular plugin or rule set. Fix documentation-related lint findings without disabling rules or making unrelated implementation changes. Where available, also run the documentation generator or type-checker when relevant. If ESLint is unavailable or no JSDoc rules are configured, state that limitation; a passing ESLint run alone does not prove the comments are accurate. Report the commands run and results; do not claim validation without evidence.

Report which declarations were documented, any unresolved contract questions, and verification limitations. A coverage pass should identify intentionally undocumented declarations rather than manufacturing low-value comments to reach a percentage.
