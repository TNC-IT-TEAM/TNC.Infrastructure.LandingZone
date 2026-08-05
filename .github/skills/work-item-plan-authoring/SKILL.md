---
name: work-item-plan-authoring
description: "Create or revise one agent-executable work-item plan from an approved research document, requirement, decision, or issue. Use when a bounded change needs named targets, atomic tasks, validation evidence, and human approval before implementation."
argument-hint: "[approved source, work-item identifier, destination, scope, and approver]"
user-invocable: true
disable-model-invocation: false
---

# Work-Item Plan Authoring

Use this workflow to convert one approved source into one reviewable implementation plan. The plan is an execution recipe with evidence; it is not a project roadmap, technical-design approval, implementation, or requirement acceptance record.

## Authority Gate

Before drafting, confirm all of the following:

- The source path and precise heading, requirement ID, decision ID, or issue anchor are supplied.
- The source claim is approved for this work item. A research recommendation alone is not implementation authorization.
- The objective is one bounded, independently reviewable outcome.
- The destination is a Markdown file directly under `docs/plans/` with a lowercase, hyphenated filename.
- The work-item identifier and named human approver are supplied. The repository's current named approver is Martyn Fewtrell unless the work item records an approved change.
- The source does not conflict with a higher-authority requirement or decision.

Stop and report a blocker when a material authority, scope, target, command, expected result, approval, credential, technical decision, or acceptance condition is unknown. Create a discovery work item only when the request explicitly authorizes discovery; do not fill the gap with an assumption.

## Procedure

1. Read the supplied source anchors and the closest repository context.
2. Extract only approved claims, constraints, evidence requirements, unresolved decisions, and exclusions relevant to this work item.
3. Inspect the immediate repository surface needed to replace placeholders with real paths, symbols, resources, commands, working directories, and expected results.
4. Draft exactly one plan using the [work-item plan template](./templates/work-item-plan.md).
5. Check the draft against the [plan quality gate](./references/plan-quality-gate.md). Every task must end as Verified, Ready for review, or Blocked.
6. Report the changed path, source anchors, validation performed, unresolved assumptions, human decisions, and any blocker. Never mark the plan Approved, Accepted, or a requirement accepted.

## Required Plan Boundary

Plans must state the objective, approved source extraction, constraints, scope and non-goals, preconditions, target map, ordered atomic tasks, expected outputs, per-task checks, final acceptance evidence, and stop conditions. Preserve the distinction between SOR baseline approval, technical-design approval, delivery evidence, and individual requirement acceptance.

## Blocker Report

Use this format when work cannot proceed:

`step`, `observed fact`, `command/output or path`, `impact`, `decision or input needed`, and `safe next action`.
