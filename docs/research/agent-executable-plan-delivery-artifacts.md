# Artifacts for Delivering Agent-Executable Plans from Research

> Research date: 2026-08-05

## Question and Decision

- **Research question:** Given the existing research, custom agents, subagents, skills, and prompts, which repository artifacts are required to reliably turn one or more research documents into an agent-executable plan for one work item?
- **Audience:** The repository maintainers and GitHub Copilot agents that research, plan, review, or implement work.
- **Decision this supports:** Whether to add a small, explicit research-to-plan delivery capability now, and which artifacts to defer until the landing-zone implementation, validation, and operational processes are known.
- **Scope:** The conversion of one or more research or other source documents into a physical work-item plan under `docs/plans/`. This covers work-item planning and review, not project planning, infrastructure implementation, deployment, issue-tracker configuration, or organisation-wide governance.
- **Time boundary:** Repository context and public VS Code documentation were reviewed on 2026-08-05. Product capabilities and preview features can change.

## Executive Summary

The repository needs an explicit **work-item plan-authoring capability**, not another general research workflow. Existing artifacts can create evidence-backed research, establish SOR authority, and run controlled requirement review, but none owns the conversion from one or more source documents to atomic tasks, target maps, checks, and stop conditions. A work-item plan is distinct from a project plan: it does not carry project-governance or authorization requirements and may be used outside a project governed by an SOR.

Adopt six artifacts as one small delivery package:

1. A versioned plan instance for each bounded work item at `docs/plans/<work-item>.md`, produced directly from one or more supplied source documents.
2. A `work-item-plan-authoring` skill containing the source-extraction workflow, plan template, and plan quality gate.
3. A `work-item-plan-orchestrator` custom agent that coordinates planning and review but does not edit plans or approve them.
4. A `work-item-planner` subagent that may inspect repository context and write only the requested plan.
5. A `work-item-plan-reviewer` subagent with read and search tools only, returning independent findings against the plan quality gate.
6. A path-specific instruction for `docs/plans/**/*.md` that preserves stable plan conventions without adding planning procedure to every Copilot interaction.

This package is sufficient to produce reviewable, agent-executable work-item plans from one or more research or other source documents. The planning request is sufficient to create the physical plan; a work-item plan is not a project plan and does not require governance, authorization, or a SOR. Do not add a plan-creation prompt, implementation agent, hooks, MCP server, or repository-wide instructions yet. The repository has no implementation code, authoritative validation commands, CI workflow, deployment procedure, or chosen first work item; those facts are necessary to safely configure execution authority and deterministic checks.

## Findings

### Observed Facts

- The existing `research-authoring` skill and `Researcher` agent author bounded evidence-based documents directly under `docs/research/`. They require source links, research dates, separation of evidence from inference, and documented uncertainty. [Research authoring skill](../../.github/skills/research-authoring/SKILL.md) and [Researcher agent](../../.github/agents/researcher.agent.md), reviewed 2026-08-05.
- The repository has requirement authoring, orchestration, and review agents. The `Requirements-orchestrator` delegates only to named author and reviewer workers and does not edit documents itself. Its reviewer is independent and read-only. [Requirements orchestrator](../../.github/agents/requirements-orchestrator.agent.md) and [requirements reviewer](../../.github/agents/requirements-reviewer.agent.md), reviewed 2026-08-05.
- The approved landing-zone SOR is an authority for outcomes, pass criteria, evidence, and named-human acceptance, but explicitly excludes technical design, delivery, verification evidence, individual acceptance, and technical-design approval from its completed baseline. [Statement of Requirements: Landing Zone](../requirements/azure-landing-zone.md), version 1.0 dated 2026-08-04.
- The existing plan research recommends a plan per independently reviewable work item, stored under `docs/plans/`, with source extraction, scope boundaries, target map, atomic ordered tasks, per-task validation, final acceptance, and escalation conditions. It explicitly says that research alone is not an execution recipe. [Agent-Executable Plans for Individual Work Items](./lightweight-copilot-delivery-plan-best-practices.md), dated 2026-08-05.
- The repository has agents, prompts, and skills for research and requirements, but has no `docs/plans/` files, plan-orchestrator, planner or delivery-plan-reviewer agent, plan-authoring skill, or `.github/instructions/` directory. Repository inventory reviewed 2026-08-05.
- VS Code documents Agent Skills as task-specific workflows that can include templates and other linked resources, while instructions are durable rules automatically applied by scope. It requires a skill's name to match its directory and says the description must explain both capability and when to use it. [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-skills), updated 2026-07-29.
- VS Code custom agents can define distinct instructions and tool lists. The documentation presents a planning agent with read-only tools and an implementation agent with editing capability as an appropriate separation. [Custom agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents), updated 2026-07-29.
- VS Code subagents perform a focused subtask and return a summary to a parent. A coordinator can restrict subagent selection with an explicit `agents` list, and custom subagent settings override inherited tools and instructions. [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents), updated 2026-07-29.
- VS Code prompt files package an explicitly invoked, focused request. A prompt may select a custom agent, accept input variables, and specify tools; prompt tool lists override a referenced agent's tool list. [Use prompt files in VS Code](https://code.visualstudio.com/docs/agent-customization/prompt-files), updated 2026-08-05.

### Inferences

1. The gap is not research quality or requirement control; it is an owned conversion step between source documents and a work-item plan. Reusing the research agent would blur its `docs/research/` output boundary, while extending the requirements orchestrator would mix requirement-baseline governance with work-item planning.
2. A skill should own the plan-authoring method because it is a repeatable multi-step procedure with reusable resources: source extraction, plan template, quality gate, and blocker-report format. A plan instance should remain outside the skill because it is work-item evidence, not a reusable resource.
3. A planner and reviewer should be separate custom agents. The planner needs repository read/search access and a constrained document-editing responsibility; the reviewer needs only read/search access and must not approve a plan. This follows the repository's requirements-agent pattern and the documented least-privilege separation between planning and implementation roles.
4. The user has selected an agent-orchestrated workflow rather than a prompt-based workflow. The orchestrator should own sequencing, delegation, and synthesis while the planner and reviewer own their separate specialist responsibilities. It should have no edit authority and use an explicit two-agent allowlist.
5. An implementation agent cannot be safely standardized yet. Agent-executable plans require actual targets, commands, expected results, and escalation conditions, but the repository has not yet established the Terraform layout, build or validation commands, CI workflow, deployment procedure, or approved technical design.

## Required Artifact Set

| Artifact | Required location | Owner and purpose | Minimum content or control | Completion evidence |
| --- | --- | --- | --- | --- |
| Work-item plan | `docs/plans/<lowercase-hyphenated-work-item>.md` | Planner writes a physical execution record from one or more source documents. | Source extraction; objective; scope and non-goals; prerequisites; target map; atomic ordered tasks; expected output; validation gates; completion check; stop conditions. | The exact file exists, is readable, is handed to the reviewer by path, and the reviewer can trace every task and check to source material or repository evidence. |
| Plan-authoring skill | `.github/skills/work-item-plan-authoring/SKILL.md` | Owns the reusable research-to-plan method. | Valid skill metadata, source-authority gate, discovery-or-escalation rule, plan quality gate, report format, and direct links to all bundled resources. | Skill name matches directory; referenced resources resolve; skill passes its authoring checks. |
| Plan template | `.github/skills/work-item-plan-authoring/templates/work-item-plan.md` | Reusable resource owned by the skill. | The plan format recommended in the existing plan research, with no unresolved placeholders permitted in an implementation-ready plan. | A sample plan can be created without changing template structure. |
| Plan quality checklist | `.github/skills/work-item-plan-authoring/references/plan-quality-gate.md` | Reusable reviewer and author checklist. | The ten quality questions from the existing plan research, adapted for source traceability, valid destination, source conflict, physical-file handoff, and bounded discovery. | Reviewer output identifies a pass, finding, or blocker for every criterion. |
| Plan orchestrator custom agent | `.github/agents/work-item-plan-orchestrator.agent.md` | Human-invoked coordinator for one planning workflow. | Read, search, and `agent/runSubagent` access; `agents: [work-item-planner, work-item-plan-reviewer]`; no edit access; validates inputs, delegates drafting then independent review, routes accepted findings to the planner, and reports unresolved decisions. | The workflow returns a reviewed plan or one blocker report, with each delegation and review disposition recorded. |
| Planner subagent | `.github/agents/work-item-planner.agent.md` | Creates or revises exactly one plan when delegated by the orchestrator. | `user-invocable: false`; read, search, and edit access; edits only the requested `docs/plans/` file; no implementation, deployment, or broad refactoring; reports source use, unknowns, and plan validation. | A representative plan includes every required section and records a bounded discovery action or stop condition for a material unknown. |
| Plan reviewer subagent | `.github/agents/work-item-plan-reviewer.agent.md` | Independently tests whether a plan is executable and appropriately bounded when delegated by the orchestrator. | `user-invocable: false`; read/search tools only; findings-first output; no edits or inferred technical decision; validates sources, atomicity, target discovery, commands, expected results, scope, and escalation. | Independent review covers the quality checklist and identifies remaining discovery actions or blockers. |
| Plan path instruction | `.github/instructions/work-item-plans.instructions.md` | Applies stable document conventions only when plan files are in scope. | `applyTo: "docs/plans/**/*.md"`; one plan per file; lowercase-hyphenated filename; required work-item and source metadata; link source anchors; do not use a plan to amend a source document. | VS Code customization diagnostics discovers it and it does not conflict with the skill or agents. |

The first and final rows are needed for every work item and repository-wide plan consistency respectively. The middle rows form the reusable planning capability. The template and quality checklist should be bundled under the skill rather than created as freestanding policy documents because they are procedural resources loaded only for relevant planning work.

## Proposed Workflow

```text
Research / project-plan / requirement / decision / issue / other documents
  -> Orchestrator selects one bounded outcome
  -> work-item-plan-orchestrator validates inputs and delegates work-item-planner
  -> Planner writes and reopens docs/plans/<work-item>.md or returns a blocker
  -> Orchestrator verifies the physical file and delegates its path to work-item-plan-reviewer
  -> Orchestrator delegates remediable findings to planner or records a discovery action or blocker
  -> Physical work-item plan is available for its requested use
```

The physical plan file itself, not the orchestrator's or subagents' chat transcripts, is the handoff artifact for the requested work item. The orchestrator must verify that the exact file exists and is readable before review. The planner must link each material task to the supplied source documents. Project plans, SORs, requirements, decisions, and issues are useful source types when available, but none is required to create a work-item plan.

### Orchestrator Contract

The orchestrator should be the only user-invocable planning role. It should have `read`, `search`, and `agent/runSubagent` access, an explicit `agents` allowlist containing only `work-item-planner` and `work-item-plan-reviewer`, and no `edit` or terminal access. Its contract should require it to:

1. Confirm one or more supplied sources, work-item identifier, requested plan destination, and bounded outcome.
2. Reject a destination that is not Markdown directly under `docs/plans/`.
3. Delegate plan drafting to the planner with only the source, scope, target destination, and relevant repository context; require the planner to write the physical file.
4. Verify that the exact plan file exists and is readable, then delegate its path to the reviewer without asking it to edit or approve.
5. Categorize review findings as planner-remediable, a bounded discovery action, or a blocker; delegate only remediable changes back to the planner.
6. Stop and return the plan's blocker-report format only when the sources cannot support a bounded plan, the physical file cannot be created, or a material unknown cannot be bounded.
7. Report the final plan path, each subagent result, reviewer-findings disposition, validation limitations, unresolved facts, and blockers. It must not implement the plan.

### Planner Contract

The planner agent should use the existing `Researcher` and requirements artifacts as inputs, not as workers it can freely delegate to. Its contract should require it to:

1. Confirm that the destination is Markdown directly under `docs/plans/` and can be written.
2. Extract claims, recommendations, constraints, uncertainties, and evidence requirements from all supplied sources.
3. Inspect the immediate repository surface needed to replace plan placeholders with real targets, commands, and expected results.
4. Record a bounded discovery action or return a blocker if the sources cannot support a bounded objective, or if a material target, command, value, credential, or expected result is unavailable.
5. Write one physical plan file only, reopen or inspect it, then check it against the bundled quality gate.
6. Return changed path, sources used, validation performed, unresolved facts, discovery actions, and blockers.

### Reviewer Contract

The reviewer must first confirm that the supplied physical plan file exists and is readable. It must treat a plan as insufficient when it requires the future execution agent to choose an architecture, policy, source value, target location, validation command, or expected result without a bounded discovery action or stop condition. It should return findings in this order: missing source traceability or scope boundary, unsafe scope expansion, non-executable target or task, missing validation or evidence, then editorial clarity. It must not repair the plan itself.

## Deferred Artifacts

| Artifact | Decision | Rationale and activation condition |
| --- | --- | --- |
| Plan-creation prompt | Do not create. | The selected orchestrator supplies the controlled entry point, sequencing, and review loop. A parallel prompt would duplicate invocation paths and potentially override the orchestrator's tool constraints. |
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
| Pass research documents directly to the implementation agent | No new artifacts. | Forces the implementation agent to interpret recommendation meaning, scope, technical targets, task order, and validation; research is not a work-item execution record. | Contradicts the existing work-item-plan recommendation. |
| Add only a plan template under `docs/plans/` | Fast to begin and low maintenance. | Consistency, source extraction, quality review, and stop behavior depend on each author remembering the process. | Suitable only for a one-off, human-authored plan. |
| Recommended: skill, template, orchestrator, planner subagent, reviewer subagent, scoped instruction, and plan instances | Separates durable rules, repeatable procedure, orchestration, specialist permissions, independent review, and work-item evidence. | Six customization artifacts plus one plan per work item require ownership and realistic testing. | Fits VS Code coordinator-worker support and the repository's existing requirements-orchestrator pattern. |
| Add implementation, implementation review, hooks, and MCP now | Strong automation potential. | Would encode unknown commands, permissions, designs, and rollout controls; high maintenance and unsafe implied authority. | Current repository evidence does not justify these controls. |

## Recommendation

Create the recommended package in one controlled follow-up work item, beginning with the `work-item-plan-authoring` skill and its template and quality-gate resources. Then add the `work-item-plan-orchestrator`, `work-item-planner`, and `work-item-plan-reviewer` agents, followed by the `docs/plans` path instruction. Configure the planner and reviewer as non-user-invocable subagents, and make the orchestrator the single user-invocable entry point with an explicit two-agent allowlist. Create the directory through the first real plan rather than adding an empty placeholder document.

Use the existing [research authoring skill](../../.github/skills/research-authoring/SKILL.md), [Researcher agent](../../.github/agents/researcher.agent.md), and [requirements orchestrator](../../.github/agents/requirements-orchestrator.agent.md) unchanged as optional upstream sources when relevant. Do not make them create delivery plans: their current output boundaries are appropriately narrower.

Pilot the package on one low-risk documentation or configuration work item with supplied source material. A plan passes the pilot if the planner can name each source, target, preservation boundary, command, expected result, and evidence location, or can express an unknown as a bounded discovery action or stop condition; the orchestrator must correctly route reviewer findings without editing the plan. Record whether the planner invented a value, the reviewer found a material omission, the orchestrator misrouted a finding, or a named check could not run. Those outcomes determine whether implementation-specific artifacts are warranted.

## Open Questions and Limitations

- **Open questions:** Which source documents will be used for the first work item; whether GitHub Issues or pull requests will be the evidence record; and which build, Terraform, security, and deployment checks become authoritative once implementation begins.
- **Assumptions:** The `docs/plans/` location, plan template, and quality gate recommended by the existing plan research are accepted as the provisional planning standard. Work-item plans may be derived from a project plan but are not themselves project-governance artifacts.
- **Unavailable evidence:** The repository contains no infrastructure source tree, CI workflow, deployment process, branch policy, issue template, credentials model, or plan implementation history. This research cannot specify an execution agent's tool allow-list, an implementation-review checklist, or deterministic hook commands.
- **Conflicting sources:** No material conflict was found. The current plan research recommends a work-item plan; existing customization research assigns workflows, roles, prompts, and instructions to distinct artifact types. The proposed artifact package combines these complementary recommendations rather than treating any product feature as mandatory.
- **Validation limitations:** The proposed artifact names, frontmatter, and tool lists have not been trialled in this repository. Custom-agent and subagent selection behavior can vary by installed VS Code version and enabled preview settings. Validate artifact discovery in VS Code diagnostics and run a successful, ambiguous, and failure-reporting planning scenario before relying on the workflow for infrastructure changes.

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