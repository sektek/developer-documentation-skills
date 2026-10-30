---
name: jsdoc
description: Write, complete, or review JSDoc and TSDoc-style comments on JavaScript and TypeScript declarations, especially public library APIs.
---

# JSDoc authoring

Document the contract a caller needs to use an API correctly. Comments should add information that the declaration and types do not already communicate. Apply [technical-writing](../technical-writing/SKILL.md); use [api-research](../api-research/SKILL.md) when behavior, intended usage, or ownership is uncertain.

## Select the scope

1. Follow the requested files, declarations, or exported surface. For a documentation coverage pass, prioritize exported classes, interfaces, types, functions, methods, properties, and options that consumers encounter.
2. Inspect existing comments, declarations, implementations, tests, and nearby conventions. Follow the project's chosen JSDoc/TSDoc tags and documentation generator, if any.
3. Preserve accurate comments and avoid reformatting unrelated code. Do not modify implementation, exported types, signatures, or runtime behavior merely to satisfy documentation.

## Describe the contract

- Start with a concise summary of what the declaration does or represents, written for its caller. Explain why or when to use it only where that is not apparent.
- Document important semantics not visible in types: defaults, units, valid ranges, ordering, side effects, resource ownership, disposal, errors, retries, and guarantees. Include only what is relevant and supported by evidence.
- For functions, document parameters and return values when they need explanation beyond names and TypeScript types. Use `@param`, `@returns`, and `@throws` according to repository conventions. Do not generate boilerplate tags that merely restate the signature.
- For generic types, explain type parameters only when their meaning or constraints are not obvious. Avoid duplicating TypeScript type annotations in prose.
- Document optional options at the declaration where their behavior is defined; avoid repeating the same details in every consuming method.
- For overloads, explain behavior that differs between call forms. For inherited or implemented members, avoid redundant comments unless the implementation changes meaningful behavior.
- Use `@example`, `@see`, `@deprecated`, and other supported tags only when they provide real value. Deprecation guidance must name a verified replacement or explain that none is known.
- Use valid JSDoc syntax and precise identifiers. Keep examples small, copyable, and aligned with public APIs; apply [code-examples](../code-examples/SKILL.md) when adding executable examples.

## Avoid misleading comments

- Do not infer runtime validation, immutability, delivery guarantees, exception types, or cleanup behavior from static types alone.
- Do not promise that a promise resolves at a stronger milestone than implementation establishes.
- Distinguish an API's own responsibilities from those of injected dependencies.
- Do not invent intent or behavior to fill gaps. Flag unresolved questions rather than asserting guesses.
- Avoid filler such as "Gets the value" for `getValue()`, and avoid comments on self-evident private implementation details unless specifically requested.

## Verify and deliver

Review comment placement, syntax, tag names, referenced symbols, and links. Run the repository's configured ESLint checks for affected files, including any JSDoc-related rules. Use the project's existing ESLint command and configuration rather than assuming a particular plugin or rule set. Fix documentation-related lint findings without disabling rules or making unrelated implementation changes. Where available, also run the documentation generator or type-checker when relevant. If ESLint is unavailable or no JSDoc rules are configured, state that limitation; a passing ESLint run alone does not prove the comments are accurate. Report the commands run and results; do not claim validation without evidence.

Report which declarations were documented, any unresolved contract questions, and verification limitations. A coverage pass should identify intentionally undocumented declarations rather than manufacturing low-value comments to reach a percentage.
