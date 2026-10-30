# Editorial decisions

These are original, project-specific conventions for developer documentation. Apply them as defaults, not as rigid rules that override accuracy or readability.

## Voice and audience

| Decision | Guidance | Reason |
| --- | --- | --- |
| Address readers directly | Use "you" where it makes instructions easier to follow. | Clear ownership of actions |
| Prefer active voice | Name the actor when it matters; passive voice is acceptable when it does not. | Makes responsibility and behavior easier to understand |
| Allow contractions | Use natural contractions in prose; avoid them if ambiguity results. | Conversational without sacrificing precision |
| Prefer present tense | Describe current behavior in present tense. Use future tense for actual future events. | Avoids unnecessary temporal complexity |
| Use inclusive, neutral language | Avoid assumptions about identity, ability, or background. | Broad accessibility |

## Clarity and structure

| Decision | Guidance | Reason |
| --- | --- | --- |
| Lead with the reader's goal | Put the answer, outcome, or task near the beginning. | Faster scanning |
| Prefer concise prose | Remove redundancy, not useful context. | Improves information density |
| Keep one concept per paragraph | Split paragraphs when purpose or topic changes. | Easier navigation |
| Make headings descriptive | Prefer specific subjects or tasks over generic labels. | Helps scanning and linking |
| Use lists selectively | Use ordered lists for sequential steps and bullets for unordered collections. | Communicates relationships |
| Define uncommon terms | Define terms at first use when the audience may not know them. | Reduces ambiguity |

## Instructions and claims

| Decision | Guidance | Reason |
| --- | --- | --- |
| Use imperative instructions | Start procedural steps with the action, such as "Run" or "Create". | Makes next actions explicit |
| Separate prerequisites | State required tools, permissions, and state before the procedure. | Prevents avoidable failures |
| Distinguish obligation | Reserve "must" and "required" for actual constraints; use "should" for recommendations. | Avoids false requirements |
| State observable outcomes | Describe expected results where they help confirm success. | Supports troubleshooting |
| Avoid unsupported claims | Verify compatibility, performance, defaults, and guarantees against evidence. | Maintains trust |
| Avoid misleading anthropomorphism | Prefer descriptions of observable system behavior to implied intent. | Technical precision |

## Conscious language

Prefer inclusive, neutral, and technically specific terminology in prose. Describe what systems do rather than using inherited labels when clearer language is available.

| Context | Prefer | Caution |
| --- | --- | --- |
| Access control lists | `allowlist` / `blocklist`, or "allow" / "exclude" | Avoid renaming established configuration keys in instructions |
| Data replication | `primary` / `secondary`, `source` / `replica` | Choose based on actual topology, not a universal substitution |
| Control relationships | `controller` / `worker`, `requester` / `responder` | These describe different relationships |
| Readers | Describe relevant roles, tasks, and prerequisites | Avoid assumptions about identity, ability, or background |
| Existing identifiers | Preserve exact exported symbols and commands | Propose API renames separately, with compatibility implications |

Review terminology in context. A word appearing in a compound, proper name, quotation, or public API is not automatically an editorial defect. Do not sacrifice technical accuracy to eliminate a term mechanically.

## Code and terminology

| Decision | Guidance | Reason |
| --- | --- | --- |
| Preserve API spelling | Match source identifiers, casing, and package names exactly. | Prevents copy/paste errors |
| Use consistent terminology | One concept should have one preferred term unless the source requires otherwise. | Supports understanding and search |
| Keep code examples focused | Show the smallest useful scenario, with prerequisites and expected behavior when needed. | Reduces distraction |
| Verify examples | Report execution or inspection evidence separately from prose review. | Avoids false confidence |
| Prefer Markdown | Use portable Markdown; defer formatting details to the markdown-authoring skill. | Separates editorial and markup concerns |

## Decision boundaries

These conventions do not determine a document's information architecture. The document-type skill does that. They also do not authorize changing API names, technical behavior, or product positioning.

When conventions conflict, prioritize technical accuracy, reader success, and consistency with the project's existing public terminology, in that order.

## Open questions

- Whether to standardize US English spelling across all projects.
- Whether to enforce sentence case in headings.
- Whether to adopt a fixed line length for prose.
- How much reference material belongs in a README versus linked documentation.

Resolve these questions based on real documentation examples rather than preemptively adding rules.
