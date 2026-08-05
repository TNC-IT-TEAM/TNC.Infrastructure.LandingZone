# Recommended Artifacts for Implementing Work-Item Plans

> Research date: 2026-08-05

## Question and Decision

- **Research question:** Which GitHub Copilot customization artifacts should this repository create to execute approved work-item plans reliably, safely, and consistently with its existing research, requirements, and work-item-plan authoring artifacts?
- **Audience:** Repository maintainers, human reviewers, work-item planners, and GitHub Copilot agents that will execute approved work-item plans.
- **Decision this supports:** Whether to add a reusable plan-implementation capability now, what its smallest artifact set should be, and which implementation-specific artifacts must wait for verified technical context.
- **Scope:** Repository-local artifacts that coordinate and evidence execution of one approved work-item plan. This includes agents, skills, templates, scoped instructions, review, validation, and evidence handoff. It excludes infrastructure implementation, deployment, GitHub mutation, credentials, MCP configuration, and the technical-definition, delivery-planning, and GitHub Project artifacts already specified by `WIP-DELIVERY-ARTIFACTS`.
- **Time boundary:** Repository context and supplied research were reviewed on 2026-08-05. Copilot customization capabilities and repository implementation context may change.

## Executive Summary

Create a **plan-bound implementation package** only when a first low-risk work item supplies real targets, commands, environment boundaries, and acceptance evidence. The package should use the repository's established coordinator-worker-reviewer pattern: one user-invocable `work-item-implementation-orchestrator`, one editable `work-item-implementer`, and one independent, read-only `work-item-implementation-reviewer`. A `work-item-plan-implementation` skill should own the reusable execution method and bundle an execution ledger and evidence-handoff template.

The approved work-item plan remains the authority for the work item's objective, scope, ordered tasks, validation gates, and stop conditions. The implementation artifacts coordinate its execution and preserve evidence; they must not reinterpret the research, select architecture, approve work, or grant deployment authority. This separation keeps the new capability consistent with the existing `work-item-plan-orchestrator`, `work-item-planner`, and `work-item-plan-reviewer` roles.

Do not create Terraform-specific instructions, a command catalog, hooks, MCP configuration, deployment tooling, or fixed specialist-agent teams yet. The current repository has planning artifacts but no verified infrastructure source tree, toolchain, validation commands, CI workflow, operational access model, or successful implementation run. Those absent facts are a blocker to safely standardizing concrete implementation authority.

## Findings

### Observed Facts

- The repository already uses a consistent orchestration pattern. `requirements-orchestrator` is user-invocable, has only `read`, `search`, and `agent` tools, and delegates document edits and independent review to distinct named workers. The author has `read`, `search`, and `edit`; the reviewer has `read` and `search` only. [Requirements orchestrator](../../.github/agents/requirements-orchestrator.agent.md), [requirements author](../../.github/agents/requirements-author.agent.md), and [requirements reviewer](../../.github/agents/requirements-reviewer.agent.md), reviewed 2026-08-05.
- The implemented work-item-plan capability follows the same pattern. Its user-invocable orchestrator delegates only to `work-item-planner` and `work-item-plan-reviewer`; the planner writes exactly one plan under `docs/plans/`; the reviewer is read-only and does not repair or approve the plan. [Work-item plan orchestrator](../../.github/agents/work-item-plan-orchestrator.agent.md), [work-item planner](../../.github/agents/work-item-planner.agent.md), and [work-item plan reviewer](../../.github/agents/work-item-plan-reviewer.agent.md), reviewed 2026-08-05.
- The work-item-plan skill defines a plan as a physical execution recipe. It requires a bounded objective, source extraction, target map, atomic ordered tasks, expected outputs, per-task checks, completion evidence, and stop conditions. [Work-item plan authoring skill](../../.github/skills/work-item-plan-authoring/SKILL.md), reviewed 2026-08-05.
- The existing plan instruction confines durable plan conventions to `docs/plans/**/*.md` and explicitly states that a plan does not authorize production action. [Work-item plan conventions](../../.github/instructions/work-item-plans.instructions.md), reviewed 2026-08-05.
- The implementation-artifact research states that an executor needs a clear entry gate, plan traceability, bounded authority, local context, falsifiable validation, durable evidence, safe stop conditions, and independent review proportional to risk. It defines the implementor as the end-to-end delivery orchestrator and requires plan-directed specialist workers rather than a fixed team. [Qualities and Best Practices for Work-Item Plan Implementer Artifacts](./implementer-artifact-qualities-and-best-practices.md), dated 2026-08-05.
- The same research concludes that this repository cannot yet safely define a concrete executor allowlist, command catalog, or implementation-specific instructions because it lacks an implementation tree, authoritative checks, CI workflow, deployment process, and approved technical baseline. [Qualities and Best Practices for Work-Item Plan Implementer Artifacts](./implementer-artifact-qualities-and-best-practices.md), dated 2026-08-05.
- The existing delivery-artifact plan already specifies technical-definition, delivery-planning, and GitHub Project artifacts, but makes their creation conditional on explicit baseline, readiness, MCP, and human-approval gates. It does not define a work-item execution agent set. [Plan: Deliver Technical Planning and GitHub Project Artifacts](../plans/deliver-technical-planning-github-project-artifacts.md), prepared 2026-08-05.
- The customization-artifact research assigns durable rules to instructions, repeatable multi-step methods to skills, permission-bounded roles to custom agents, and independent focused work to subagents. It recommends the smallest artifact that owns the behavior and least-privilege tool lists. [GitHub Copilot Customization Artifacts](./github-copilot-customization-artifacts.md), dated 2026-08-03.

### Inferences

1. A new implementation coordinator should be a sibling of the existing work-item-plan coordinator, not an extension of it. Planning creates and reviews the execution recipe; implementation executes that recipe and returns change and validation evidence. Combining them would blur the plan's physical-file handoff and independent-review boundary.
2. The implementation package should use the same role shape and front-matter conventions already proven in this repository: a user-invocable coordinator with a named delegate allowlist, a non-user-invocable editable worker, and a non-user-invocable read-only reviewer. This is a local convention supported by the existing requirements and planning workflows.
3. The implementation skill should contain the reusable execution procedure, plan-step ledger, blocker-report format, and evidence-handoff template. Those are repeatable methods and resources, while the work-item plan remains the work-item-specific authority and the implementation report remains the work-item's evidence.
4. A general `work-item-implementer` may execute a plan only when the plan names its allowed paths, commands, expected results, and external boundaries. It must return a blocker rather than infer a missing material fact. A generic agent definition cannot safely fill gaps in the plan.
5. Specialist workers should be added only as a named plan step establishes a stable, repeatable need. For example, a future Terraform validation worker or security reviewer requires observed toolchain commands, paths, and review criteria. A fixed roster of specialists now would imply knowledge and authority the repository does not have.
6. The technical-definition, delivery-planning, and GitHub Project package in `WIP-DELIVERY-ARTIFACTS` is complementary but not a substitute for execution artifacts. It governs upstream baseline and delivery-record workflows; the proposed package governs one plan's controlled implementation and evidence handoff.

## Recommended Artifact Set

| Artifact | Proposed location | Purpose and minimum contract | Create when |
| --- | --- | --- | --- |
| Plan-bound implementation orchestrator | `.github/agents/work-item-implementation-orchestrator.agent.md` | User-invocable coordinator with `tools: [read, search, agent]` and an explicit delegate allowlist. It verifies the plan's implementation-readiness gate, creates a plan-step ledger, delegates only plan-required work, integrates results, obtains final validation evidence, and returns the final handoff or one blocker report. It does not edit, approve, deploy, or mutate external systems. | Create with the first low-risk implementation work item that has real targets and checks. |
| Plan implementation worker | `.github/agents/work-item-implementer.agent.md` | Non-user-invocable editable worker with `tools: [read, search, edit]`; add terminal capability only if an approved plan requires a verified local validation command. It executes only delegated plan steps and allowed paths, runs the named checks, records evidence, and stops for unplanned design choices or failed gates. | Create with the orchestrator, after the first plan identifies concrete path and validation boundaries. |
| Plan implementation reviewer | `.github/agents/work-item-implementation-reviewer.agent.md` | Non-user-invocable, read-only reviewer with `tools: [read, search]`. It compares the plan, changed paths, validation output, and evidence ledger; returns findings by severity; does not edit, accept, or resolve findings. | Create with the orchestrator for the first multi-file, infrastructure, externally affecting, or otherwise review-sensitive implementation. |
| Plan implementation skill | `.github/skills/work-item-plan-implementation/SKILL.md` | Reusable method for readiness checks, plan-step ledger creation, delegation boundaries, narrow-first validation, evidence preservation, and blocker reporting. It links to its templates and does not duplicate plan tasks. | Create with the first executable plan, once its entry and evidence rules can be exercised. |
| Execution ledger template | `.github/skills/work-item-plan-implementation/templates/execution-ledger.md` | A skill resource with rows for plan step, delegate, changed paths, check/working directory, result, evidence location, and state: `Verified`, `Ready for review`, or `Blocked`. The ledger is an implementation report resource, not a new plan. | Bundle with the implementation skill. |
| Evidence-handoff template | `.github/skills/work-item-plan-implementation/templates/implementation-handoff.md` | A skill resource that records plan path, completed and blocked steps, files changed, commands and working directories, results, unavailable checks, review findings, residual risks, and required human decisions. It must not self-declare human acceptance. | Bundle with the implementation skill. |
| Implementation path instructions | `.github/instructions/<technology-or-area>.instructions.md` | Scoped, verified conventions for an actual implementation path, including layout, protected surfaces, authoritative commands, and evidence rules. Use a narrow `applyTo` glob. | Defer until the repository contains a stable implementation surface and its conventions are observed. |
| Specialist worker or reviewer | `.github/agents/<capability>.agent.md` | A plan-required, bounded role such as Terraform validation or security review, with explicit paths, tools, output, and return condition. The implementation orchestrator must add it to its delegate allowlist only when needed. | Defer until a real plan repeatedly demonstrates a stable capability and least-privilege boundary. |

The proposed names deliberately follow the existing lower-case, hyphenated `.agent.md` and skill-directory conventions. The three agent bodies should link to the implementation skill and applicable path instructions rather than repeat their content. The implementation worker and reviewer should be `user-invocable: false`; the orchestrator should be the single user-invocable entry point, as in the existing requirements and plan workflows.

## Proposed Workflow

```text
Approved work-item plan
  -> work-item-implementation-orchestrator checks readiness and plan path
  -> implementation ledger maps every executable plan step to itself or one named worker
  -> work-item-implementer performs bounded changes and named checks
  -> plan-directed specialist worker runs only when a plan step requires it
  -> work-item-implementation-reviewer checks plan, diff, validation, and evidence
  -> orchestrator integrates findings and returns evidence handoff or blocker report
  -> named human reviews and accepts where the plan requires it
```

### Implementation-Readiness Gate

The orchestrator should not delegate an implementation unless the supplied plan provides all applicable controls below:

- A physical Markdown plan under `docs/plans/` with a singular objective, source traceability, scope, non-goals, target map, ordered tasks, and stop conditions.
- Actual editable targets or a bounded discovery step, plus preservation boundaries for nearby surfaces.
- A material check for each change: command or inspection method, working directory, expected result, and evidence location; unavailable checks are a discovery item or blocker.
- Known edit scope, tools, environment prerequisites, external boundaries, and named human gates.
- A plan-step ledger assignment for every executable step and a reviewer where the plan's risk or scope requires one.

When a condition is missing, return the existing blocker format: `step`, `observed fact`, `command/output or path`, `impact`, `decision or input needed`, and `safe next action`. The orchestrator must not convert an unknown into an architecture choice, command, value, credential request, external mutation, or approval claim.

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| Give a general editing agent the plan and ask it to implement | Lowest artifact count. | No durable coordinator owns step coverage, evidence, independent review, or safe delegation; broad editing authority can exceed the plan. | Conflicts with the implementation-artifact quality model and does not match local orchestrator-worker-reviewer practice. |
| Add the complete proposed package immediately with generic commands and broad capability | Establishes an implementation entry point quickly. | Encodes unverified tool, path, and validation assumptions; may falsely imply deployment or infrastructure authority. | The repository inventory and implementation-artifact research identify these facts as unavailable. |
| Recommended: create the plan-bound core package with the first low-risk executable plan, then add scoped instructions and specialist roles from observed evidence | Separates plan authority from execution, preserves least privilege, uses existing repository conventions, and creates reusable evidence practices without pretending the toolchain is known. | Requires the first plan to contain genuine targets and checks; some details remain plan-specific until conventions repeat. | Supported by existing plan artifacts, implementation-artifact research, and the customization-artifact selection model. |
| Build infrastructure-specific agents, hooks, MCP integration, and deployment automation now | Could reduce manual effort after a mature operating model exists. | High authority and maintenance risk without verified commands, credential separation, environment controls, or rollback/approval design. | No current repository evidence supports these controls. |

## Recommendation

Adopt the proposed package as the implementation-artifact target, but do not create its concrete agent definitions until a first low-risk work-item plan passes the implementation-readiness gate. That plan should be the pilot and must name actual paths, a bounded edit surface, at least one executable or inspectable validation gate, an evidence destination, and the required human review boundary.

At that point, create exactly six core artifacts: the implementation orchestrator, implementer, implementation reviewer, implementation skill, execution-ledger template, and evidence-handoff template. Configure the three agents with the same authority boundaries already used by the requirements and plan-authoring sets. Keep the orchestrator's delegation allowlist narrow: initially the implementer and reviewer only. Add a plan-specific specialist only when a named plan task has an observed capability requirement that the core worker cannot safely own.

After a successful pilot, promote only repeated, verified local facts into a narrow path-specific instruction. For example, create a Terraform instruction only after Terraform files, validated commands, directory boundaries, and protected operational conventions exist. Do not use the implementation package to bypass the separate upstream gates in `WIP-DELIVERY-ARTIFACTS`, and do not represent plan completion as human acceptance, GitHub Project readiness, or deployment authorization.

This recommendation would change when the repository has a stable implementation tree, authoritative validation and CI commands, operational access boundaries, and multiple reviewed implementation runs. Those facts could justify technology-specific skills, scoped instructions, deterministic hooks, and additional read-only specialist reviewers.

## Open Questions and Limitations

- **Open questions:** What low-risk work item will serve as the pilot; which technical baseline and implementation paths will it use; what command validates the first change; where will durable implementation evidence live; and who reviews and accepts the result?
- **Unavailable evidence:** The repository does not currently provide an implementation source tree, Terraform or other toolchain layout, authoritative build/test commands, CI workflow, deployment process, credential model, or completed implementation history.
- **Conflicting sources:** No material conflict was found. The work-item-plan artifacts define planning ownership, the implementation-artifact research defines execution quality, and `WIP-DELIVERY-ARTIFACTS` defines separate upstream technical and delivery artifacts with explicit external-operation gates.
- **Validation limitations:** This recommendation is a synthesis of repository artifacts and supplied research, not a successful execution trial. Agent front matter, skill discovery, tool availability, and delegation behavior must be verified in the installed VS Code environment during the first pilot.

## Sources

- Repository context: [Qualities and Best Practices for Work-Item Plan Implementer Artifacts](./implementer-artifact-qualities-and-best-practices.md), dated 2026-08-05.
- Repository context: [GitHub Copilot Customization Artifacts](./github-copilot-customization-artifacts.md), dated 2026-08-03.
- Repository context: [Artifacts for Delivering Agent-Executable Plans from Research](./agent-executable-plan-delivery-artifacts.md), dated 2026-08-05.
- Repository context: [Agent-Executable Plans for Individual Work Items](./lightweight-copilot-delivery-plan-best-practices.md), dated 2026-08-05.
- Repository context: [Plan: Deliver Technical Planning and GitHub Project Artifacts](../plans/deliver-technical-planning-github-project-artifacts.md), prepared 2026-08-05.
- Repository artifacts: [work-item plan authoring skill](../../.github/skills/work-item-plan-authoring/SKILL.md), [work-item plan orchestrator](../../.github/agents/work-item-plan-orchestrator.agent.md), [work-item planner](../../.github/agents/work-item-planner.agent.md), [work-item plan reviewer](../../.github/agents/work-item-plan-reviewer.agent.md), and [work-item plan conventions](../../.github/instructions/work-item-plans.instructions.md), reviewed 2026-08-05.