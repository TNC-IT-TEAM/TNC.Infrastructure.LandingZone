# Work-Item Plan Quality Gate

Approve a draft for human review only when every criterion passes. A material `No` requires clarification, a discovery work item, or a blocker; the author must not invent the missing decision.

| Criterion | Pass condition |
| --- | --- |
| Source traceability | Every material plan claim links to one or more supplied research headings, requirement IDs, decision IDs, or issue anchors, and the plan distinguishes proposed research recommendations from approved implementation decisions. |
| Objective | The plan has one singular, observable outcome. |
| Scope | The change boundary and explicit non-goals are stated. |
| Targets | Every target has a path plus a symbol, resource, heading, or bounded discovery action. |
| Atomicity | Each task has one concrete action and does not require an unstated architecture, policy, or product choice. |
| Order | Dependencies are expressed as ordered steps or blockers. |
| Falsifiability | Each task has an expected output and a command, inspection, demonstration, or human review gate. |
| Commands | Each command has a working directory, prerequisites, and an expected result. |
| Decisions | Stop conditions protect approvals, secrets, production actions, technical design, and failed validation; pending implementation approval is recorded as a human gate rather than treated as a reason to refuse Draft plan creation. |
| Evidence | Final evidence links source authority, changed files, validation results, limitations, and named-human acceptance. |
| Destination | The plan is a physical Markdown file directly under `docs/plans/` and uses a lowercase, hyphenated filename. |
| File handoff | The exact file exists, is readable, contains the required sections, and its path is reported for review; chat output alone does not satisfy delivery. |
| Source conflict | Conflicting or lower-authority source material is named and escalated rather than silently reconciled. |
| Human acceptance | A named human owns plan approval and final requirement or work-item acceptance; the agent does not self-accept. |
| Placeholders | An implementation-ready plan contains no unresolved material placeholders for targets, values, commands, expected results, evidence, or approval. |

## Review Output

Return findings first, ordered by impact:

1. Missing authority or approval.
2. Unsafe scope or authority expansion.
3. Non-executable target or task.
4. Missing validation or evidence.
5. Editorial clarity or structure.

For each finding state the affected section, evidence, impact, and precise remediation. Then report passed criteria, open questions, unverified checks, and human decisions needed. Do not edit or approve the plan.
