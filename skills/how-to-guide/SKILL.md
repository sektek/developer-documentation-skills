---
name: how-to-guide
description: Write, revise, or review task-oriented developer how-to guides that lead readers from prerequisites to a verifiable outcome.
---

# How-to guide authoring

Write instructions for a developer who knows what they want to accomplish and needs a reliable path to doing it. A how-to guide is **task-oriented**: it is not a tutorial teaching fundamentals, an explanation of architecture, or an exhaustive API reference.

Apply [technical-writing](../technical-writing/SKILL.md), [markdown-authoring](../markdown-authoring/SKILL.md), and [code-examples](../code-examples/SKILL.md). Use [documentation-workflow](../documentation-workflow/SKILL.md) for discovery, drafting, verification, and review.

## Discover the task

1. Define a concrete outcome and a reader with the minimum necessary prior knowledge.
2. Inspect implementation, public exports, package metadata, tests, and existing examples for each API the guide will use.
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

- Keep one coherent scenario throughout; use the same identifiers, queue names, and event types across steps.
- Prefer the shortest path to a useful result. Include alternative approaches only if a choice is necessary to complete the task.
- Explain *why* only when it affects a choice, a safety condition, or successful execution.
- Use public APIs rather than internal helpers; show lifecycle management for services, connections, and consumers.
- Make asynchronous ordering explicit: start listeners before publishing when delivery depends on them.
- Do not silently imply exactly-once delivery, persistence, retries, or successful delivery merely because a send method resolved.
- Avoid mixing a tutorial's conceptual progression, an explanation's architectural argument, or a reference's exhaustive option tables into the procedure.
- Prefer a link to a detailed explanation over an extended detour.

## Verify and deliver

Use the code-examples skill to check every code block. Run type-checking and an end-to-end exercise when the environment permits; verify commands, links, and expected output. Record the actual evidence level for each example: **Verified**, **Type-checked**, **Inspected**, **Unverified**, or **Failed**.

Review with the documentation-review skill. Deliver the guide, a brief record of the reader's path, and a verification summary with any untested external-service assumptions. Never call an example "working" solely because it resembles an existing README snippet.

## Evaluation prompts (not instructions for the guide)

Use the following to evaluate the skill itself, not as content to insert into a user's document:

- Given a library with an AMQP publisher and listener, write a guide that connects both and demonstrates a received event.
- Given an incomplete guide with a missing broker prerequisite, repair the prerequisite and verification steps.
- Given an API reference listing publisher options, rewrite it as a task-specific guide without copying the option catalog.
- Given an example that calls an internal handler adapter directly, replace it with the intended public entry point.
