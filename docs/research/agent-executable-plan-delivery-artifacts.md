# Artifacts for Delivering Agent-Executable Plans from Research

> Research date: 2026-08-05

## Question and Decision

- **Research question:** Given the existing research, custom agents, subagents, skills, and prompts, which repository artifacts are required to reliably turn an approved research document into an agent-executable plan for one work item?
- **Audience:** The repository maintainers, the named human approval authority, and GitHub Copilot agents that research, plan, review, or implement work.
- **Decision this supports:** Whether to add a small, explicit research-to-plan delivery capability now, and which artifacts to defer until the landing-zone implementation, validation, and operational processes are known.
- **Scope:** The conversion of an approved research recommendation, SOR requirement, decision, or issue into a reviewable plan under `docs/plans/`. This covers the planning and plan-review boundary, not infrastructure implementation, deployment, issue-tracker configuration, or organisation-wide governance.
- **Time boundary:** Repository context and public VS Code documentation were reviewed on 2026-08-05. Product capabilities and preview features can change.

## Executive Summary

The repository needs an explicit **plan-authoring capability**, not another general research workflow. Existing artifacts can create evidence-backed research, establish SOR authority, and run controlled requirement review, but none owns the conversion from an approved source to atomic tasks, target maps, checks, and stop conditions. No `docs/plans/` directory or plan-specific customization currently exists.

Adopt six artifacts as one small delivery package:

1. A versioned plan instance for each approved work item at `docs/plans/<work-item>.md`.
2. A `work-item-plan-authoring` skill containing the source-extraction workflow, plan template, and plan quality gate.
3. A `work-item-planner` custom agent that may inspect repository context and write only the requested plan.
4. A `work-item-plan-reviewer` custom agent with read and search tools only, returning independent findings against the plan quality gate.
5. A `create-work-item-plan` prompt that explicitly starts the planner with source, work-item identifier, and target plan path.
6. A path-specific instruction for `docs/plans/**/*.md` that preserves stable plan conventions without adding planning procedure to every Copilot interaction.

This package is sufficient to produce reviewable, agent-executable plans from research documents. Do not add a delivery coordinator, implementation agent, hooks, MCP server, or repository-wide instructions yet. The repository has no implementation code, authoritative validation commands, CI workflow, deployment procedure, or chosen first work item; those facts are necessary to safely configure execution authority and deterministic checks.

## Findings

### Observed Facts

- The existing `research-authoring` skill and `Researcher` agent author bounded evidence-based documents directly under `docs/research/`. They require source links, research dates, separation of evidence from inference, and documented uncertainty. [Research authoring skill](../../.github/skills/research-authoring/SKILL.md) and [Researcher agent](../../.github/agents/researcher.agent.md), reviewed 2026-08-05.
- The repository has requirement authoring, orchestration, and review agents. The `Requirements-orchestrator` delegates only to named author and reviewer workers and does not edit documents itself. Its reviewer is independent and read-only. [Requirements orchestrator](../../.github/agents/requirements-orchestrator.agent.md) and [requirements reviewer](../../.github/agents/requirements-reviewer.agent.md), reviewed 2026-08-05.
- The approved landing-zone SOR is an authority for outcomes, pass criteria, evidence, and named-human acceptance, but explicitly excludes technical design, delivery, verification evidence, individual acceptance, and technical-design approval from its completed baseline. [Statement of Requirements: Landing Zone](../requirements/azure-landing-zone.md), version 1.0 dated 2026-08-04.
- The existing plan research recommends a plan per independently reviewable work item, stored under `docs/plans/`, with source extraction, scope boundaries, target map, atomic ordered tasks, per-task validation, final acceptance, and escalation conditions. It explicitly says that research alone is not an execution recipe. [Agent-Executable Plans for Individual Work Items](./lightweight-copilot-delivery-plan-best-practices.md), dated 2026-08-05.
- The repository has agents, prompts, and skills for research and requirements, but has no `docs/plans/` files, planner or delivery-plan-reviewer agent, plan-authoring skill, plan-specific prompt, or `.github/instructions/` directory. Repository inventory reviewed 2026-08-05.
- VS Code documents Agent Skills as task-specific workflows that can include templates and other linked resources, while instructions are durable rules automatically applied by scope. It requires a skill's name to match its directory and says the description must explain both capability and when to use it. [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-skills), updated 2026-07-29.
- VS Code custom agents can define distinct instructions and tool lists. The documentation presents a planning agent with read-only tools and an implementation agent with editing capability as an appropriate separation. [Custom agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents), updated 2026-07-29.
- VS Code subagents perform a focused subtask and return a summary to a parent. A coordinator can restrict subagent selection with an explicit `agents` list, and custom subagent settings override inherited tools and instructions. [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents), updated 2026-07-29.
- VS Code prompt files package an explicitly invoked, focused request. A prompt may select a custom agent, accept input variables, and specify tools; prompt tool lists override a referenced agent's tool list. [Use prompt files in VS Code](https://code.visualstudio.com/docs/agent-customization/prompt-files), updated 2026-08-05.

### Inferences

1. The gap is not research quality or requirement control; it is an owned conversion step between an approved source and an implementation-ready plan. Reusing the research agent would blur its `docs/research/` output boundary, while extending the requirements orchestrator would mix requirement-baseline governance with delivery planning.
2. A skill should own the plan-authoring method because it is a repeatable multi-step procedure with reusable resources: source extraction, plan template, quality gate, and blocker-report format. A plan instance should remain outside the skill because it is work-item evidence, not a reusable resource.
3. A planner and reviewer should be separate custom agents. The planner needs repository read/search access and a constrained document-editing responsibility; the reviewer needs only read/search access and must not approve a plan. This follows the repository's requirements-agent pattern and the documented least-privilege separation between planning and implementation roles.
4. A custom coordinator is not required in the first version. A human can invoke the plan prompt, review the plan, request reviewer findings, and approve the result. Adding a coordinator before the first trial would add another permission, handoff, and maintenance boundary without addressing an observed need.
5. An implementation agent cannot be safely standardized yet. Agent-executable plans require actual targets, commands, expected results, and escalation conditions, but the repository has not yet established the Terraform layout, build or validation commands, CI workflow, deployment procedure, or approved technical design.

## Required Artifact Set

| Artifact | Required location | Owner and purpose | Minimum content or control | Completion evidence |
| --- | --- | --- | --- | --- |
| Work-item plan | `docs/plans/<lowercase-hyphenated-work-item>.md` | Human approver owns authorization; planner drafts the execution record for one work item. | Approved source extraction; objective; scope and non-goals; prerequisites; target map; atomic ordered tasks; expected output; validation gates; final acceptance; stop conditions. | Reviewer can trace every task and check to source authority or repository evidence. |
| Plan-authoring skill | `.github/skills/work-item-plan-authoring/SKILL.md` | Owns the reusable research-to-plan method. | Valid skill metadata, source-authority gate, discovery-or-escalation rule, plan quality gate, report format, and direct links to all bundled resources. | Skill name matches directory; referenced resources resolve; skill passes its authoring checks. |
| Plan template | `.github/skills/work-item-plan-authoring/templates/work-item-plan.md` | Reusable resource owned by the skill. | The plan format recommended in the existing plan research, with no unresolved placeholders permitted in an implementation-ready plan. | A sample plan can be created without changing template structure. |
| Plan quality checklist | `.github/skills/work-item-plan-authoring/references/plan-quality-gate.md` | Reusable reviewer and author checklist. | The ten quality questions from the existing plan research, plus checks for approved authority, valid destination, source conflict, and named human acceptance. | Reviewer output identifies a pass, finding, or blocker for every criterion. |
| Planner custom agent | `.github/agents/work-item-planner.agent.md` | Creates or revises exactly one plan after inspection. | Read, search, and edit access; edits only the requested `docs/plans/` file; no source approval, requirement acceptance, implementation, deployment, or broad refactoring; reports source use, unknowns, and plan validation. | A representative plan includes every required section and stops on a material unknown. |
| Plan reviewer custom agent | `.github/agents/work-item-plan-reviewer.agent.md` | Independently tests whether a draft plan is executable and appropriately bounded. | Read/search tools only; findings-first output; no edits, approval, or inferred technical decision; validates sources, atomicity, target discovery, commands, expected results, scope, and escalation. | Independent review covers the quality checklist and identifies remaining human decisions. |
| Plan-creation prompt | `.github/prompts/create-work-item-plan.prompt.md` | Human-invoked entry point that reliably supplies the planner's inputs. | Selects `work-item-planner`; asks for source path and exact heading/ID, work-item identifier, requested plan path, approval status, and approver; rejects invalid destinations. | Invocation produces either one plan draft or the specified blocker report. |
| Plan path instruction | `.github/instructions/work-item-plans.instructions.md` | Applies stable document conventions only when plan files are in scope. | `applyTo: "docs/plans/**/*.md"`; one plan per file; lowercase-hyphenated filename; required status and source metadata; never self-accept; link source anchors; do not use a plan to amend a requirement or decision. | VS Code customization diagnostics discovers it and it does not conflict with the skill or agents. |

The first and final rows are needed for every work item and repository-wide plan consistency respectively. The middle rows form the reusable planning capability. The template and quality checklist should be bundled under the skill rather than created as freestanding policy documents because they are procedural resources loaded only for relevant planning work.

## Proposed Workflow

```text
Approved research / SOR / decision / issue
  -> Human selects one bounded outcome and approval authority
  -> /create-work-item-plan invokes work-item-planner
  -> Planner writes docs/plans/<work-item>.md or returns a blocker
  -> work-item-plan-reviewer provides independent findings
  -> Human resolves findings and approves plan for implementation
  -> Implementation agent executes only the approved plan
  -> Human reviews evidence and records acceptance
```

The plan itself, not the planner's chat transcript, is the handoff artifact to the implementation agent. The planner must link the precise research heading, SOR requirement, decision, or issue that authorizes each material task. A research recommendation is not authorization until the named human marks it approved for that work item.

### Planner Contract

The planner agent should use the existing `Researcher` and requirements artifacts as inputs, not as workers it can freely delegate to. Its contract should require it to:

1. Confirm that the destination is Markdown directly under `docs/plans/`.
2. Extract only approved claims, constraints, uncertainties, and evidence requirements from named source anchors.
3. Inspect the immediate repository surface needed to replace plan placeholders with real targets, commands, and expected results.
4. Create a discovery work item or return a blocker if a material target, command, design decision, credential, approval, or acceptance condition is unavailable.
5. Write one plan only, then check it against the bundled quality gate.
6. Return changed path, source anchors, validation performed, unresolved assumptions, and human decisions needed. It must not mark the plan approved or accepted.

### Reviewer Contract

The reviewer must treat a plan as insufficient when it requires the future execution agent to choose an architecture, policy, source value, target location, validation command, expected result, or approval boundary. It should return findings in this order: missing authority or approval, unsafe scope or authority expansion, non-executable target or task, missing validation or evidence, then editorial clarity. It must not repair the plan itself or convert an unapproved research recommendation into a decision.

## Deferred Artifacts

| Artifact | Decision | Rationale and activation condition |
| --- | --- | --- |
| Delivery-plan coordinator agent | Defer. | A planner prompt plus independent reviewer is adequate for the first trial. Add a coordinator only after repeated manual handoff errors or a demonstrated need to coordinate planner, implementer, and reviewer workers. |
| Implementation agent | Defer. | No actual implementation tree, validation commands, CI, deployment process, or approved technical design exists. Add only after one low-risk plan names real checks and its implementation boundaries are understood. |
| Implementation-review agent | Defer. | Plan review is required now; code or infrastructure review should be designed after the toolchain and risk controls are known. |
| Repository-wide `.github/copilot-instructions.md` | Defer. | The current durable rules are confined to planning documents. Do not use always-on instructions for a procedure that only applies to work-item plans. |
| Terraform or infrastructure path instruction | Defer. | It would require verified language, provider, directory, security, and validation conventions that do not yet exist. |
| Hooks | Defer. | Hooks enforce deterministic behavior. No authoritative formatter, test, or policy command has been identified to enforce. |
| MCP server | Defer. | Repository sources and normal GitHub/VS Code context are sufficient for plan creation. Add an MCP server only for a recurring approved external evidence or ticketing dependency with scoped credentials and an owner. |
| Plugin | Defer. | Distribution across repositories is not an immediate need; first validate the workflow locally. |

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| Pass research documents directly to the implementation agent | No new artifacts. | Forces the implementation agent to interpret recommendation status, scope, technical targets, task order, and validation; research is not a work-item execution record. | Contradicts the existing work-item-plan recommendation. |
| Add only a plan template under `docs/plans/` | Fast to begin and low maintenance. | Consistency, source extraction, quality review, and stop behavior depend on each author remembering the process. | Suitable only for a one-off, human-authored plan. |
| Recommended: skill, template, planner, reviewer, prompt, scoped instruction, and plan instances | Separates durable rules, repeatable procedure, role permissions, independent review, explicit invocation, and work-item evidence. | Seven repository artifacts plus one plan per work item require ownership and realistic testing. | Fits VS Code customization boundaries and existing research/requirements patterns. |
| Add a full coordinator, implementation, review, hooks, and MCP suite now | Strong automation potential. | Would encode unknown commands, permissions, designs, and rollout controls; high maintenance and unsafe implied authority. | Current repository evidence does not justify these controls. |

## Recommendation

Create the recommended package in one controlled follow-up work item, beginning with the `work-item-plan-authoring` skill and its template and quality-gate resources. Then add the planner and independent reviewer agents, the explicit prompt, and the `docs/plans` path instruction. Create the directory through the first real plan rather than adding an empty placeholder document.

Use the existing [research authoring skill](../../.github/skills/research-authoring/SKILL.md), [Researcher agent](../../.github/agents/researcher.agent.md), and [requirements orchestrator](../../.github/agents/requirements-orchestrator.agent.md) unchanged as upstream evidence and governance inputs. Do not make them create delivery plans: their current output boundaries are appropriately narrower.

Pilot the package on one low-risk documentation or configuration work item whose source is already approved. A plan passes the pilot only if the planner can name each source anchor, target, preservation boundary, command, expected result, evidence location, and human acceptance action without an unplanned design decision. Record whether the planner needed to invent a value, the reviewer found a material omission, the executing agent left scope, or a named check could not run. Those outcomes determine whether a coordinator or implementation-specific artifacts are warranted.

## Open Questions and Limitations

- **Open questions:** Which source recommendations are approved for the first work item; who will approve plans for implementation; whether GitHub Issues or pull requests will be the evidence record; and which build, Terraform, security, and deployment checks become authoritative once implementation begins.
- **Assumptions:** The `docs/plans/` location, plan template, and quality gate recommended by the existing plan research are accepted as the provisional planning standard. The named SOR acceptance authority remains the named human, not an agent.
- **Unavailable evidence:** The repository contains no infrastructure source tree, CI workflow, deployment process, branch policy, issue template, credentials model, or plan implementation history. This research cannot specify an execution agent's tool allow-list, an implementation-review checklist, or deterministic hook commands.
- **Conflicting sources:** No material conflict was found. The current plan research recommends a work-item plan; existing customization research assigns workflows, roles, prompts, and instructions to distinct artifact types. The proposed artifact package combines these complementary recommendations rather than treating any product feature as mandatory.
- **Validation limitations:** The proposed artifact names, frontmatter, and tool lists have not been trialled in this repository. Custom-agent and subagent selection behavior can vary by installed VS Code version and enabled preview settings. Validate artifact discovery in VS Code diagnostics and run a successful, ambiguous, and blocked planning scenario before relying on the workflow for infrastructure changes.

## Sources

- Repository context: [Agent-Executable Plans for Individual Work Items](./lightweight-copilot-delivery-plan-best-practices.md), dated 2026-08-05.
- Repository context: [GitHub Copilot Customization Artifacts](./github-copilot-customization-artifacts.md), dated 2026-08-03.
- Repository context: [Effective Agents and Subagents: Design and Authoring Practices](./effective-agents-and-subagents-best-practices.md), dated 2026-08-04.
- Repository context: [Copilot Research Workflow Recommendations](./copilot-research-workflow-recommendations.md), dated 2026-08-03.
- Repository context: [Statement of Requirements: Landing Zone](../requirements/azure-landing-zone.md), version 1.0 dated 2026-08-04.
- Visual Studio Code, [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-skills), updated 2026-07-29.
- Visual Studio Code, [Custom agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents), updated 2026-07-29.
- Visual Studio Code, [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents), updated 2026-07-29.
- Visual Studio Code, [Use prompt files in VS Code](https://code.visualstudio.com/docs/agent-customization/prompt-files), updated 2026-08-05.