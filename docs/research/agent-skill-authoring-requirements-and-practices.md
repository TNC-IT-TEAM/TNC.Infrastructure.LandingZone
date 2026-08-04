# Agent Skill Authoring Requirements and Best Practices

> Research date: 2026-08-04. This document covers repository-scoped Agent Skills authored for GitHub Copilot in Visual Studio Code and the portable Agent Skills specification as available on this date.

## Question and Decision

- **Research question:** What requirements and best practices should govern a skill that creates other Agent Skills?
- **Audience:** Repository maintainers and GitHub Copilot users who will author and review shared skills.
- **Decision this supports:** Whether and how to add a repository-scoped `skill-authoring` skill under `.github/skills/`.
- **Scope:** Agent Skill directory structure, required metadata, workflow design, resource layout, validation, discovery, and governance. It does not design a particular generated skill or configure custom agents, MCP servers, hooks, or extensions.
- **Time boundary:** Product documentation and the Agent Skills specification available on 2026-08-04.

## Executive Summary

A skill that creates other skills should be a narrow, user-invocable authoring workflow rather than a generic instruction file. The generated output must be a directory containing `SKILL.md`; its `name` and `description` YAML frontmatter are required and are the primary discovery contract. The name must match the directory and comply with the Agent Skills naming rules. The description must say both what the created skill does and when it applies.

The recommended workflow is to first decide whether the request actually needs a skill, collect the capability and execution constraints, create the smallest valid directory, author a concise `SKILL.md`, add only explicitly referenced resources, and validate both structure and representative invocation scenarios. This repository already follows the expected `.github/skills/<skill-name>/SKILL.md` layout, so a future authoring skill should preserve that convention.

The main limitation is that portability is not identical to feature parity. The Agent Skills specification defines portable fields and layout, while VS Code adds its own discovery locations and controls such as `user-invocable`, `disable-model-invocation`, and experimental forked context. Generated skills should use the portable core by default and add VS Code-specific controls only when their behavior is required.

## Findings

### Observed Facts

#### Required skill shape

- The Agent Skills specification defines a skill as a directory that contains, at minimum, a `SKILL.md` file. Optional directories include `scripts/`, `references/`, and `assets/`. [Agent Skills Specification](https://agentskills.io/specification) (accessed 2026-08-04; no publication or update date displayed).
- `SKILL.md` must contain YAML frontmatter followed by Markdown instructions. The required frontmatter fields are `name` and `description`. [Agent Skills Specification](https://agentskills.io/specification) (accessed 2026-08-04; no publication or update date displayed).
- The `name` must be 1 to 64 characters, use lowercase letters, numbers, and hyphens, not begin or end with a hyphen, not contain consecutive hyphens, and match the parent directory name. VS Code warns that an invalid name can cause a skill to fail to load without a visible error. [Agent Skills Specification](https://agentskills.io/specification) (accessed 2026-08-04; no publication or update date displayed); [VS Code: Use Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills) (updated 2026-07-29).
- The `description` must be non-empty and no more than 1,024 characters. The specification and VS Code both say it should describe both the capability and when to use it; the specification also recommends relevant keywords for task matching. [Agent Skills Specification](https://agentskills.io/specification) (accessed 2026-08-04; no publication or update date displayed); [VS Code: Use Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills) (updated 2026-07-29).

#### Discovery and progressive loading

- VS Code discovers project skills from `.github/skills/`, `.claude/skills/`, and `.agents/skills/`, and personal skills from corresponding user-profile locations. It supports additional configured project locations through `chat.agentSkillsLocations`. [VS Code: Use Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills) (updated 2026-07-29).
- Skills load progressively: an agent first uses the `name` and `description` for discovery, then loads the `SKILL.md` body after activation, and only accesses additional files when the instructions reference them. [VS Code: Use Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills) (updated 2026-07-29).
- The specification recommends keeping the `SKILL.md` body under 5,000 tokens and under 500 lines, moving detailed content to separately referenced resources. It advises keeping resource references one level deep from `SKILL.md`. [Agent Skills Specification](https://agentskills.io/specification) (accessed 2026-08-04; no publication or update date displayed).

#### VS Code controls and validation

- In VS Code, `argument-hint`, `user-invocable`, `disable-model-invocation`, and experimental `context: fork` are optional frontmatter controls. By default, skills can be invoked as slash commands and automatically selected when relevant. [VS Code: Use Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills) (updated 2026-07-29).
- VS Code documents `/create-skill` as an AI-assisted way to create a skill and `/skills` as a shortcut to configure skills. The Agent Customizations editor can also create and manage skills, but it is marked preview. [VS Code: Use Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills) (updated 2026-07-29).
- The Agent Skills specification recommends validating a skill with the `skills-ref` reference library command `skills-ref validate ./my-skill`. [Agent Skills Specification](https://agentskills.io/specification) (accessed 2026-08-04; no publication or update date displayed).
- VS Code documents a preview Chat Customizations Evaluations extension that analyzes skill files for ambiguity, contradictions, cognitive load, missing error paths, and linked-customization conflicts. It can also scaffold and run Waza evaluations for skills. [VS Code: Customize Agent Behavior](https://code.visualstudio.com/docs/agent-customization/overview) (updated 2026-07-29).

#### Repository context

- This repository already stores skills at `.github/skills/<name>/SKILL.md`. The existing `research-authoring` and `statement-of-requirements` skills use lowercase hyphenated names, required metadata, a clear boundary section, a numbered procedure, and linked templates or references where needed.
- The repository's existing research guidance distinguishes skills from prompts, agents, and instructions. It recommends skills for task-specific, multi-step capabilities with bundled resources, rather than using them for durable rules or short manually invoked requests. [GitHub Copilot Customization Artifacts](./github-copilot-customization-artifacts.md) (research date 2026-08-03).

### Inferences

- **Inference:** A skill authoring workflow should begin with an artifact-selection gate. A request should become a skill only when it is a repeatable capability with a multi-step procedure, reusable resources, or both. A short one-off command is usually a prompt file; a stable rule is usually an instruction; a role or permission boundary is usually a custom agent. This follows the documented distinction between skills, prompts, instructions, and agents.
- **Inference:** The generated skill's description deserves explicit review because it is both user-facing command metadata and the automatic relevance signal. A technically correct skill with a vague description is likely to be undiscoverable or selected at the wrong time.
- **Inference:** Defaulting a meta-skill to `user-invocable: true` and `disable-model-invocation: true` is appropriate. Skill creation changes repository behavior and creates files, so explicit user intent is safer than opportunistic automatic invocation. This recommendation is based on the documented invocation controls, not a product requirement.
- **Inference:** The authoring skill should keep a portable baseline: `name`, `description`, a concise Markdown procedure, and standard relative resource links. It should add VS Code-specific metadata only for an explicit need, improving the chance that the resulting skill works in another skills-compatible agent.

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| Rely on VS Code `/create-skill` only | No repository maintenance; uses the supported interactive generator. | Generated output may not encode this repository's local review, layout, or validation conventions. | VS Code documents `/create-skill`; assumes ad hoc generation is sufficient for the team. |
| Add a repository `skill-authoring` skill | Encodes a repeatable quality gate, local destination, lightweight template, and validation/reporting contract. | Requires maintenance and can become redundant with product tooling if it merely repeats generic instructions. | Fits the documented purpose of a task-specific reusable workflow with resources. |
| Add a custom agent for skill authoring | Could isolate a specialist role and tool set. | Additional surface area and no inherent need for a distinct role or permission boundary. | Custom agents are intended for role and tool specialization; no such requirement is established here. |

## Recommendation

Create a single repository-scoped skill at `.github/skills/skill-authoring/SKILL.md` after agreeing its desired output contract. Make it manually invoked and use it to create or revise exactly one skill directory per invocation.

The authoring skill should require the following sequence:

1. Confirm the requested capability, intended users, trigger phrases, destination, required tools, resource needs, success criteria, and whether the artifact should instead be an instruction, prompt, or custom agent.
2. Select a compliant lowercase hyphenated name and confirm the directory is `.github/skills/<name>/`. Reject invalid names before creating files.
3. Create the minimal `SKILL.md` with `name` and a precise `description`. Include `argument-hint` only when meaningful. Set `user-invocable` and `disable-model-invocation` deliberately, rather than copying defaults blindly.
4. Write a bounded Markdown body: purpose, use conditions, required inputs, ordered procedure, failure or stop conditions, expected final report, and references to supporting files.
5. Add scripts only when deterministic execution improves reliability. Document their prerequisites, inputs, outputs, failure behavior, and least-privilege assumptions. Add templates, examples, and references only when they materially improve repeated execution.
6. Link every resource from `SKILL.md` using a relative path. Do not leave unlinked files as assumed context, because VS Code loads resources on demand only when the instructions reference them.
7. Run structural validation with `skills-ref validate` when available, inspect any VS Code diagnostics, and execute at least two representative scenarios: a normal request that should activate the skill and a neighboring request that should not.
8. Report the created paths, selected invocation behavior, commands run, validation outcomes, and any unverified environment or tool assumptions.

A future `skill-authoring` skill should use a small template such as:

```markdown
---
name: skill-name
description: Performs a specific capability. Use when a user needs that capability in these stated conditions.
argument-hint: "[required input]"
user-invocable: true
disable-model-invocation: true
---

# Skill Title

Use this skill when ...

## Inputs and Boundaries

- Require ...
- Do not ...

## Procedure

1. ...
2. ...

## Validation and Report

- Validate ...
- Report ...
```

This is a template, not a mandatory fixed section order. The generated body should be as short as possible while retaining the decisions, procedure, boundaries, and validation that the target capability needs. Reassess the recommendation if skill authoring becomes a distinct governed role with separate approval or tool restrictions; that would justify a custom agent as well.

## Open Questions and Limitations

- **Open questions:** Should generated skills be permitted to add executable scripts, and if so, what code review or approval requirement applies? Who owns ongoing review of generated skills and removal of stale ones?
- **Unavailable evidence:** The repository has no current automation, CI rule, or documented policy that validates `.github/skills/` contents. This document cannot establish whether `skills-ref` is installed or permitted in the target environment.
- **Conflicting sources:** No material conflict was found. The portable specification defines optional fields such as `license`, `compatibility`, `metadata`, and experimental `allowed-tools`; VS Code documents different optional invocation and context fields. This is a scope difference, so the recommendation uses only the portable required core by default.
- **Validation limitations:** Documentation confirms the intended format and VS Code behavior but does not prove that a generated skill will be selected correctly in every model, workspace configuration, or future product release. Test selection with representative prompts and review Agent Debug Logs or customization diagnostics when available.

## Sources

- [VS Code: Use Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills), updated 2026-07-29.
- [VS Code: Customize Agent Behavior](https://code.visualstudio.com/docs/agent-customization/overview), updated 2026-07-29.
- [Agent Skills Specification](https://agentskills.io/specification), accessed 2026-08-04; no publication or update date displayed.
- [GitHub Copilot Customization Artifacts](./github-copilot-customization-artifacts.md), research date 2026-08-03.
- [Copilot Research Workflow Recommendations](./copilot-research-workflow-recommendations.md), research date 2026-08-03.