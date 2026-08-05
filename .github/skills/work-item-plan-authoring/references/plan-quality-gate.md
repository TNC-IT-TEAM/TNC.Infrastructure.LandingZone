# Work-Item Plan Quality Gate

The planner produces the physical plan when requested. Use this gate to assess whether it is executable and well bounded. A material `No` requires a bounded discovery action or a blocker; the author must not invent missing facts.

| Criterion | Pass condition |
| --- | --- |
| Source traceability | Every material plan claim links to one or more supplied research headings, requirements, decisions, issues, or other source anchors. No particular source type is required. |
| Objective | The plan has one singular, observable outcome. |
| Scope | The change boundary and explicit non-goals are stated. |
| Targets | Every target has a path plus a symbol, resource, heading, or bounded discovery action. |
| Atomicity | Each task has one concrete action and does not require an unstated architecture, policy, or product choice. |
| Order | Dependencies are expressed as ordered steps or blockers. |
| Falsifiability | Each task has an expected output and a command, inspection, demonstration, or other observable check. |
| Commands | Each command has a working directory, prerequisites, and an expected result. |
| Unknowns | Material unknowns have a bounded discovery action or a stop condition; they do not require project governance or authorization to plan the work item. |
| Evidence | Completion evidence links source documents, changed files, validation results, and limitations. |
| Destination | The plan is a physical Markdown file directly under `docs/plans/` and uses a lowercase, hyphenated filename. |
| File handoff | The exact file exists, is readable, contains the required sections, and its path is reported; chat output alone does not satisfy delivery. |
| Source conflict | Conflicting source material is named with its impact and a bounded discovery action or stop condition rather than silently reconciled. |
| Placeholders | An executable plan contains no unresolved material placeholders for targets, values, commands, expected results, or evidence. |

## Review Output

Return findings first, ordered by impact:

1. Missing source traceability or scope boundary.
2. Unsafe scope expansion.
3. Non-executable target or task.
4. Missing validation or evidence.
5. Editorial clarity or structure.

For each finding state the affected section, evidence, impact, and precise remediation. Then report passed criteria, open questions, discovery actions, and unverified checks. Do not edit the plan.
