---
name: work-item-plan-authoring
description: "Create or revise one agent-executable work-item plan from one or more research or other source documents. Use when a bounded change needs named targets, atomic tasks, validation evidence, and a physical Markdown plan."
argument-hint: "[one or more source documents, work-item identifier, destination, and scope]"
user-invocable: true
disable-model-invocation: false
---

# Work-Item Plan Authoring

Use this workflow to convert one or more supplied source documents into one physical Markdown work-item plan. The plan file is the execution recipe with evidence; chat output is only a report about that file. A work-item plan is not a project plan: it does not require project governance, authorization, a Statement of Requirements, technical-design approval, or requirement acceptance. It may be derived from a project plan, or it may stand outside project governance.

A plan created through this workflow authorizes execution of its stated repository-local tasks. Do not add a human-authorization, low-risk-pilot, selection, designation, or durable-record gate before those tasks. Retain a stop condition only for an external, production, privileged, or other approval-sensitive operation when the plan itself explicitly requires an authorized procedure.

## Input and Scope Check

Before drafting, confirm all of the following:

- At least one source path or other supplied source is available. Multiple source documents may be supplied.
- The source material is sufficient to draft a bounded plan. Research recommendations and other supplied source material are valid planning inputs.
- The objective is one bounded, independently reviewable outcome.
- The destination is a Markdown file directly under `docs/plans/` with a lowercase, hyphenated filename.
- The destination path is writable, and the planner is authorized to create or revise that one file.
- The work-item identifier is supplied, or a descriptive identifier can be derived from the requested work item.
- Conflicting source material is recorded in the plan with the affected scope; it does not prevent drafting unless the conflict makes the objective or scope impossible to state.

Stop and report a blocker only when the material sources cannot support a bounded objective, the plan file cannot be written, or a task cannot name a bounded discovery action for a material unknown. Do not require governance, approval, a SOR, technical design, or acceptance conditions to create a work-item plan.

## Procedure

1. Read all supplied source documents at their named anchors and the closest repository context.
2. Extract claims, recommendations, constraints, evidence requirements, unresolved facts, and exclusions relevant to this work item.
3. Inspect the immediate repository surface needed to replace placeholders with real paths, symbols, resources, commands, working directories, and expected results.
4. Draft exactly one plan using the [work-item plan template](./templates/work-item-plan.md), and write it to the requested physical path under `docs/plans/`.
5. Confirm the file exists at that exact path, is readable as Markdown, and contains the required sections before continuing.
6. Check the physical file against the [plan quality gate](./references/plan-quality-gate.md). Confirm every task has an expected output, an observable check, and a failure action.
7. Report the created or revised path, sources used, file check, validation performed, unresolved facts, and any blocker. The work-item plan is finished when the physical file has been created, reopened, and checked. Never treat chat output as the plan.

## Required Plan Boundary

Plans must state the objective, source extraction, constraints, scope and non-goals, preconditions, target map, ordered atomic tasks, expected outputs, per-task checks, completion evidence, and stop conditions. Include SOR, project-plan, decision, or governance references only when the supplied sources make them relevant to the work item.

The completed plan is the execution authority for its stated repository-local scope. Do not introduce an approval, designation, or pilot-selection prerequisite unless the supplied source explicitly requires one for an operation outside that scope.

## Blocker Report

Use this format when work cannot proceed:

`step`, `observed fact`, `command/output or path`, `impact`, `decision or input needed`, and `safe next action`.
