---
name: how-to-guide
description: Write, revise, or review task-oriented developer how-to guides that lead readers from prerequisites to a verifiable outcome.
---

# How-to guide authoring

Write instructions for a developer who knows what they want to accomplish and needs a reliable path to doing it. A how-to guide is **task-oriented**: it is not a tutorial teaching fundamentals, an explanation of architecture, or an exhaustive API reference.

Apply [api-research](../api-research/SKILL.md) when choosing or explaining public API usage. Apply [technical-writing](../technical-writing/SKILL.md), [markdown-authoring](../markdown-authoring/SKILL.md), and [code-examples](../code-examples/SKILL.md). Use [documentation-workflow](../documentation-workflow/SKILL.md) for discovery, drafting, verification, and review.

## Discover the task

1. Define a concrete outcome and a reader with the minimum necessary prior knowledge.
2. Research relevant public APIs and intended usage with api-research; retain only findings that affect this task.
3. Identify prerequisites: tools, runtime, external services, credentials, permissions, and expected starting state.
4. Identify operational hazards: destructive actions, duplicate processing, resource cleanup, retries, credentials, and environment-specific behavior.
5. Record unknowns; never manufacture commands, flags, API signatures, guarantees, or expected output.

## Structure the guide

Adapt the following path rather than treating it as a mandatory template:

1. **Title:** Start with a task verb and name the result, such as "Publish and consume events with RabbitMQ."
2. **Outcome:** State what the reader will have working, in one or two sentences.
3. **Prerequisites:** List only the setup the reader actually needs. Give version constraints only when verified.
4. **Steps:** Number the actions in execution order. Provide complete, copyable commands and code; show where files belong and when to run them.
5. **Verify:** Give an observable success condition, including expected output or behavior that is supported by evidence.
6. **Clean up / troubleshoot:** Explain how to stop resources and diagnose likely failures relevant to this task.
7. **Next steps:** Link to API reference, conceptual explanations, and related guides instead of expanding the guide into a catalog.

## Writing rules

- Keep one coherent scenario throughout; use consistent names, identifiers, configuration values, and example data across steps.
- Prefer the shortest path to a useful result. Include alternative approaches only if a choice is necessary to complete the task.
- Explain *why* only when it affects a choice, a safety condition, or successful execution.
- Use public APIs rather than internal helpers; show lifecycle management for services, connections, and consumers.
- Make asynchronous ordering explicit: start listeners before publishing when delivery depends on them.
- Do not silently imply exactly-once delivery, persistence, retries, or successful delivery merely because a send method resolved.
- Avoid mixing a tutorial's conceptual progression, an explanation's architectural argument, or a reference's exhaustive option tables into the procedure.
- Prefer a link to a detailed explanation over an extended detour.

## Verify and deliver

Review the chosen API path against the api-research findings separately from code correctness; compiling and running do not establish idiomatic usage.

Use the code-examples skill to check every code block. Run type-checking and an end-to-end exercise when the environment permits; verify commands, links, and expected output. Record the actual evidence level for each example: **Verified**, **Type-checked**, **Inspected**, **Unverified**, or **Failed**.

Review with the documentation-review skill. Deliver the guide, a brief record of the reader's path, and a verification summary with any untested external-service assumptions. Never call an example "working" solely because it resembles an existing README snippet.
