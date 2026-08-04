---
name: skill-authoring
description: "Create or revise one repository-scoped Agent Skill with compliant metadata, bounded instructions, linked resources, and validation. Use when a user wants to make, add, scaffold, or improve a reusable multi-step skill."
argument-hint: "[capability, users, trigger phrases, and constraints]"
user-invocable: true
disable-model-invocation: true
---

# Skill Authoring

Use this workflow to create or revise exactly one Agent Skill for this repository. Prefer a portable skill format and preserve the repository convention `.github/skills/<skill-name>/SKILL.md`.

## Artifact Selection

Create a skill only when the requested capability is repeatable, multi-step, or benefits from bundled resources. Redirect the request when another customization is a better fit:

- Use an instruction for a durable rule that should apply broadly or to matching files.
- Use a prompt for a single focused task with parameterized input.
- Use a custom agent for a distinct role, context boundary, tool restriction, or permission boundary.
- Use a hook for deterministic enforcement at an agent lifecycle event.

## Inputs and Boundaries

Before creating files, establish the capability, intended users, trigger phrases, inputs, outputs, required tools, resource needs, boundaries, success criteria, invocation behavior, owner, and review trigger. Ask only for missing information needed to proceed.

- Create or revise one skill directory per invocation.
- Use `.github/skills/<skill-name>/` unless the user explicitly provides another compatible repository location.
- Do not create files until the name is valid and the destination is confirmed to be new or intentionally being revised.
- Preserve existing files and unrelated user changes.
- Do not add scripts, references, examples, or assets unless they materially improve repeated execution and are explicitly justified.
- Do not invent tools, permissions, prerequisites, policies, owners, approval, or validation results.

## Procedure

1. Decide whether the request needs a skill using the artifact-selection gate. Stop and recommend the better customization type when it does not.
2. Select a lowercase hyphenated name from 1 to 64 characters. Reject names that begin or end with a hyphen, contain consecutive hyphens, use other characters, or do not match the parent directory.
3. Confirm the target directory and whether this is a new skill or an intentional revision. Stop before writing if the destination conflicts with an unrelated existing skill.
4. Define the skill's discovery description. It must state what the skill does, when it applies, and include relevant trigger terms. Keep it non-empty and no longer than 1,024 characters.
5. Create or revise the smallest valid `SKILL.md`. Use portable `name` and `description` metadata by default. Add `argument-hint`, `user-invocable`, or `disable-model-invocation` only when their intended behavior is understood; default this authoring skill to explicit user invocation.
6. Write a concise body covering purpose, use conditions, required inputs, ordered actions, boundaries, failure or stop conditions, validation, and the expected final report. Keep the body under 500 lines and approximately 5,000 tokens.
7. Add supporting resources only when needed. Link every resource directly from `SKILL.md` with a relative path. For scripts, document prerequisites, inputs, outputs, failure behavior, and least-privilege assumptions.
8. Validate the generated skill with `skills-ref validate <skill-directory>` when available. Inspect VS Code customization diagnostics, frontmatter, name-directory matching, relative links, Markdown rendering, and body size.
9. Exercise at least two representative scenarios: a request that should activate the skill and a neighboring request that should be redirected to another customization type. Also check that invalid names and conflicting destinations stop before file creation.
10. Report the created or changed paths, selected invocation behavior, commands and diagnostics run, validation outcomes, skipped checks, unresolved assumptions, owner, and review trigger.

## Stop Conditions

Stop without creating files when the request lacks an essential capability or destination decision, the name is invalid, the destination conflicts with an unrelated skill, a required tool or prerequisite is unavailable, or the request requires a different customization primitive. Record the unresolved decision and the smallest next input needed.

## Validation and Report

A completed authoring task must leave a directory containing at least `SKILL.md`, valid required frontmatter, a name matching its directory, a discovery description that states capability and use conditions, and no unlinked supporting files. Report unavailable validation tooling or untested invocation behavior as limitations rather than assuming success.
