---
name: agent-authoring
description: "Design and create one repository-scoped VS Code custom agent or subagent-ready agent profile with a bounded role, least-privilege tools, explicit delegation, and validation. Use when a user wants to make, add, scaffold, or improve an agent or subagent."
argument-hint: "[role, task, users, tools, permissions, and delegation needs]"
user-invocable: true
disable-model-invocation: true
---

# Agent Authoring

Use this workflow to design and create or revise exactly one custom agent profile for this repository. The output is normally `.github/agents/<name>.agent.md`. A subagent is represented by an agent profile whose invocation and delegation settings restrict it to focused work delegated by a parent.

## Artifact Selection

Create an agent only when the request needs a distinct role, context boundary, tool restriction, model choice, or permission boundary. Redirect the request when another primitive owns the behavior:

- Use an instruction for a durable rule that applies broadly or to matching files.
- Use a prompt for one focused, user-invoked request with parameterized input.
- Use a skill for a multi-step capability with bundled resources.
- Use a hook for deterministic enforcement at an agent lifecycle event.

Before proceeding, state why a prompt, deterministic workflow, or existing automation is insufficient. Do not create an agent merely to reuse a short prompt.

## Inputs and Boundaries

Before writing, establish the intended users, one owned decision or action, inputs, outputs, non-goals, trigger phrases, destination, required tools, permission level, validation, owner, review trigger, and invocation mode:

- **Direct agent:** available for deliberate user selection.
- **Delegation-only worker:** callable by a parent for one bounded task; normally not user-invocable.
- **Coordinator:** may delegate only to a named `agents` allowlist and remains responsible for synthesis, final communication, and final validation.

Ask only for essential missing information. Create or revise one agent profile per invocation. Preserve unrelated user changes and stop before writing if the destination conflicts with an unrelated agent.

## Procedure

1. Confirm the artifact-selection decision, role owner, destination, and whether the profile is direct, delegation-only, or a coordinator.
2. Choose a stable lowercase hyphenated filename and `name` that match. Reject names that begin or end with a hyphen, contain consecutive hyphens, or use other characters.
3. Write valid frontmatter with a precise description that states the capability, use conditions, and relevant trigger terms. Set `user-invocable` and `disable-model-invocation` deliberately. Add `agents` only when a coordinator needs delegation, and prefer a named allowlist over unrestricted selection.
4. Write the role contract: purpose, owned scope, bounded context, inputs, non-goals, deliverables, acceptance criteria, stop conditions, escalation triggers, and final report format.
5. Grant the minimum tools required. Planners, researchers, and reviewers should normally use read and search only. Add edit, terminal, web, MCP, or other execution tools only when the owned action requires them. Require reporting of destructive actions, skipped validation, and unavailable environments.
6. For a delegation-only worker, define one bounded task, allowed scope and tools, expected decision-ready summary, success criteria, stop condition, and instructions to report uncertainty rather than fabricate an answer. Keep nested delegation disabled unless a measured need justifies it.
7. Add handoffs or supporting links only when they materially improve the role. Prefer existing repository instructions and skills over duplicated guidance. Do not add credentials, broad permissions, scripts, hooks, or MCP configuration unless explicitly required and separately reviewed.
8. Validate the profile before reporting completion. Check frontmatter, name and filename consistency, description discoverability, tool allow-list, delegation settings, relative links, Markdown size, and destination. Use repository customization diagnostics or Agent Debug Logs when available.
9. Exercise representative scenarios: a request that should select the profile, a neighboring request that should not, and an insufficient-permission or invalid-destination case that should stop. For coordinators, verify that worker selection is restricted and that final validation remains with the coordinator.
10. Report the created or changed path, role and invocation mode, tools, delegation allowlist, validation commands and outcomes, scenarios exercised, skipped checks, unresolved assumptions, owner, and review trigger.

## Stop Conditions

Stop without writing when the request is better served by another primitive, the role or destination is materially unclear, the name is invalid, the destination conflicts with an unrelated profile, the required permission boundary cannot be expressed, or validation evidence is unavailable for a consequential change. Record the unresolved decision and the smallest next input needed.

## Validation and Report

A completed authoring task must leave one valid `.agent.md` profile in the intended location. Its role must be narrow and observable, its tools must follow least privilege, its completion result must be independently checkable, and any subagent result must be a concise decision-ready summary rather than a transcript. Report limitations and preview-feature assumptions instead of treating them as validated behavior.