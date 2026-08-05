---
name: work-item-plan-authoring
description: "Create or revise one agent-executable work-item plan from one or more research documents, requirements, decisions, or issues. Use when a bounded change needs named targets, atomic tasks, validation evidence, and a physical Markdown plan for human review before implementation."
argument-hint: "[one or more source documents, work-item identifier, destination, scope, and approver]"
user-invocable: true
disable-model-invocation: false
---

# Work-Item Plan Authoring

Use this workflow to convert one or more supplied source documents into one physical, reviewable Markdown implementation plan. Research documents are valid inputs for drafting a plan even when their recommendations have not been approved for implementation. The plan file is the execution recipe with evidence; chat output is only a report about that file. It is not a project roadmap, technical-design approval, implementation, or requirement acceptance record.

## Authority Gate

Before drafting, confirm all of the following:

- At least one source path and a precise heading, requirement ID, decision ID, or issue anchor are supplied. Multiple source documents may be supplied.
- The source material is sufficient to draft a bounded plan. A research recommendation is valid planning input, but it is not implementation authorization.
- The objective is one bounded, independently reviewable outcome.
- The destination is a Markdown file directly under `docs/plans/` with a lowercase, hyphenated filename.
- The destination path is writable, and the planner is authorized to create or revise that one file.
- The work-item identifier and named human approver are supplied for the plan's review and acceptance gate. The repository's current named approver is Martyn Fewtrell unless the work item records an approved change.
- Conflicting source material is identified in the plan and left for human resolution; it does not prevent drafting unless the conflict makes the objective or scope impossible to state.

Stop and report a blocker when the material sources cannot support a bounded objective, or when a target, command, expected result, approval boundary, credential, technical decision, or acceptance condition is required for an implementation-ready task but is unknown. Do not block plan drafting merely because implementation or technical-design approval is still outstanding; record that gate in the plan. Create a discovery work item only when the request explicitly authorizes discovery; do not fill a gap with an assumption.

## Procedure

1. Read all supplied source documents at their named anchors and the closest repository context.
2. Extract claims, recommendations, constraints, evidence requirements, unresolved decisions, and exclusions relevant to this work item. Label research recommendations as proposed inputs where implementation approval is absent.
3. Inspect the immediate repository surface needed to replace placeholders with real paths, symbols, resources, commands, working directories, and expected results.
4. Draft exactly one plan using the [work-item plan template](./templates/work-item-plan.md), and write it to the requested physical path under `docs/plans/`.
5. Confirm the file exists at that exact path, is readable as Markdown, and contains the required sections before continuing.
6. Check the physical file against the [plan quality gate](./references/plan-quality-gate.md). Every task must end as Verified, Ready for review, or Blocked.
7. Report the created or revised path, all source anchors, file check, validation performed, unresolved assumptions, human decisions, and any blocker. Never treat chat output as the plan, or mark the plan Approved, Accepted, or a requirement accepted.

## Required Plan Boundary

Plans must state the objective, source extraction, implementation-approval status, constraints, scope and non-goals, preconditions, target map, ordered atomic tasks, expected outputs, per-task checks, final acceptance evidence, and stop conditions. Preserve the distinction between research input, SOR baseline approval, technical-design approval, delivery evidence, and individual requirement acceptance.

## Blocker Report

Use this format when work cannot proceed:

`step`, `observed fact`, `command/output or path`, `impact`, `decision or input needed`, and `safe next action`.
