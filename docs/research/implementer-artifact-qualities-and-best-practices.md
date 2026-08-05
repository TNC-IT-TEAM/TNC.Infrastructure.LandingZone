# Qualities and Best Practices for Work-Item Plan Implementer Artifacts

> Research date: 2026-08-05

## Question and Decision

- **Research question:** What qualities should implementer artifacts have when they are used to execute an approved work-item plan, and which practices make those artifacts reliable, safe, and reviewable?
- **Audience:** Repository maintainers, work-item planners, human reviewers, and GitHub Copilot agents that execute approved plans.
- **Decision this supports:** Whether, and to what standard, to introduce reusable implementation-facing artifacts before executing work-item plans.
- **Scope:** Artifacts that guide or constrain execution of a bounded work-item plan: implementation-agent definitions, path-specific instructions, skills, task templates, validation checklists, evidence/report formats, and narrowly scoped automation. This research does not authorize infrastructure changes, deployments, external-system mutations, credentials, or a particular implementation-agent tool configuration.
- **Time boundary:** Repository context and public documentation were reviewed on 2026-08-05. VS Code and GitHub Copilot product behavior may change.

## Executive Summary

An implementer artifact should execute an approved work-item plan **from entry gate to final product and evidence handoff**, without becoming a second, competing plan. It is an orchestrating delivery capability: it selects and coordinates only the specialist subagents required by the plan, such as document writers, coding agents, configuration agents, test agents, security reviewers, or release-evidence agents. Its central qualities are: a clear role and entry gate; direct traceability to the plan and authority source; complete task coverage; concrete, local context; least-privilege authority; small, ordered, falsifiable work units; validation and durable evidence; explicit stop and human-handoff behavior; and a narrow, maintainable scope.

The recommended package for a mature implementation surface is a plan-bound implementor orchestrator with only required coordination tools; a plan-specific allowlist of specialist subagents; scoped path instructions containing verified repository conventions; reusable skills for repeatable methods; a validation-and-evidence checklist; and a read-only independent review artifact. The orchestrator must account for every plan step, sequence dependencies, integrate specialist outputs into one final product, run or delegate the plan's final validation, and return a complete handoff. Each artifact must refer to the work-item plan as the authority for objective, scope, ordered tasks, and acceptance; none should invent a missing architecture, value, approval, or production action.

The most important limitation is local: this repository has planning artifacts but no implementation tree, authoritative build/test commands, CI workflow, deployment procedure, or approved technical baseline. Therefore it is not yet possible to safely define a concrete executor tool allowlist, command catalog, or implementation-specific instruction file. Add those only after a real low-risk work item establishes them through evidence.

## Findings

### Observed Facts

- VS Code recommends that AI work requests state specific inputs, outputs, constraints, expected behavior, and verification results. It recommends decomposing complex tasks into smaller, well-scoped steps and using expected outputs, tests, or acceptance criteria so the AI can verify work. [Best practices for using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices), page reviewed 2026-08-05.
- VS Code recommends an explore, plan, implement, and review sequence for complex changes. It says to review the plan before implementation, include tests or expected outputs during implementation, and review and test generated changes before integration. [Best practices for using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices), page reviewed 2026-08-05.
- VS Code recommends providing relevant context by naming files, folders, symbols, current terminal output, and test failures. It also recommends using separate sessions or subagents for focused investigation so irrelevant context does not degrade response quality. [Best practices for using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices), page reviewed 2026-08-05.
- VS Code advises keeping instructions concise, scoping them with `applyTo` patterns, and limiting enabled tools to those required for the task. [Best practices for using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices), page reviewed 2026-08-05.
- GitHub documents repository-wide, path-specific, and agent instructions as distinct mechanisms. Path-specific instructions use an `applyTo` glob, and multiple relevant instruction sets can be supplied together; GitHub advises avoiding conflicting instruction sets. [Adding repository custom instructions for GitHub Copilot](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot), page reviewed 2026-08-05.
- GitHub's repository-instruction guidance calls for documented build, test, validation, environmental prerequisites, command ordering, known failures, and validation outcomes that have been checked in the repository. [Adding repository custom instructions for GitHub Copilot](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot), page reviewed 2026-08-05.
- The repository's existing plan research defines a work-item plan as an implementation recipe with evidence. It requires named sources and targets, atomic ordered tasks, expected outputs, per-task verification, explicit non-goals, final evidence, and stop conditions. [Agent-Executable Plans for Individual Work Items](./lightweight-copilot-delivery-plan-best-practices.md), dated 2026-08-05.
- Existing repository research concludes that an implementation agent cannot yet be standardized because the repository lacks an implementation tree, actual validation commands, CI workflow, deployment procedure, and approved technical design. [Artifacts for Delivering Agent-Executable Plans from Research](./agent-executable-plan-delivery-artifacts.md), dated 2026-08-05.

### Inferences

1. An implementer artifact should be a **controlled execution aid**, not a new source of product or technical authority. The approved work-item plan remains authoritative for the work item's objective, constraints, task sequence, expected results, and escalation conditions.
2. The most useful implementation artifacts remove avoidable choices at execution time. They must say where to work, what conventions to preserve, which check to run, what result to expect, and where to record evidence. A generic instruction such as "implement safely" does not meet this standard.
3. Least privilege applies to both tools and edit scope. An artifact should grant only the repository, paths, operations, and external capabilities required by the current task; it should not imply permission for deployment, credential access, destructive changes, or external writes merely because an implementation may eventually need them.
4. Validation must be near the relevant change and produce reviewable evidence. A final broad test alone cannot reliably isolate which implementation step caused a failure.
5. An implementer artifact must fail safely. When a source conflicts, a required value is unknown, an unplanned design decision appears, a check fails, or an approval-sensitive action is needed, the artifact should require a blocker report and human decision rather than a plausible guess.
6. Artifacts should be specialized by stable responsibility: instructions for durable local conventions, skills for repeatable multi-step methods, plan instances for work-item-specific direction, and agent definitions for permission-constrained roles. Combining all of these into a large always-on instruction increases conflict and staleness risk.
7. End-to-end execution needs an orchestrator distinct from its workers. The orchestrator owns plan-step coverage, sequencing, handoffs, integration, final-product assembly, final validation, and the final report; a specialist worker owns only its delegated output. This permits a plan to use a document writer, coding agent, tester, or other worker without granting each agent authority over the whole work item.

## Quality Model

| Quality | Required characteristic | Observable review question | Common failure mode |
| --- | --- | --- | --- |
| Plan fidelity | Names the plan path and applies only its approved objective, scope, tasks, and acceptance conditions. | Can a reviewer trace every required action to a plan step or a repository convention explicitly referenced by the plan? | Reinterpreting research or silently expanding scope. |
| Clear entry and exit | States prerequisites, permitted start state, expected completion evidence, and which actor accepts the result. | Does it say when execution may begin and what it must return without self-accepting? | Running against an unsigned, stale, or incomplete plan. |
| End-to-end delivery ownership | Owns completion of every executable plan step, final-product assembly, final validation, and the handoff report. | Does a plan-step ledger show each step as completed and verified, ready for required human review, or blocked? | Individual workers report their work, but no role delivers the integrated final product. |
| Plan-directed specialization | Selects specialist workers only when their capability is required by a named plan step and gives each a bounded delegation. | Does each subagent have a named step range, input, output, permitted paths/tools, and return condition? | A fixed collection of agents runs regardless of plan needs, or workers receive the entire work item's authority. |
| Concrete context | Identifies relevant paths, symbols, commands, working directories, dependencies, conventions, and protected surfaces. | Can the executor locate each target and run each check without choosing a material value or architecture? | Broad search followed by guessed conventions. |
| Bounded authority | Limits tools, editable paths, environments, external systems, and mutation types to what the task requires. | Does it prohibit unneeded deployment, access, secret, destructive, or external mutation capability? | A general-purpose agent has authority beyond the work item. |
| Atomic execution | Uses a small ordered unit of work with a specified action, target, expected output, and next gate. | Can a step be completed without choosing among materially different approaches? | "Improve", "handle", or "implement" tasks with no observable end state. |
| Falsifiable validation | Pairs each material change with an executable or inspectable check and an expected result. | Does every task have a command, test, inspection, or human-review gate with a stated result? | Deferring all validation to "run tests" at the end. |
| Evidence and traceability | Records changed paths, commands, exit status or observed result, source/plan references, and residual limitations in a durable location. | Can an independent reviewer reconstruct why the change was made and how it was checked? | A chat-only claim that work is complete. |
| Safe uncertainty handling | Defines stop conditions and a concise blocker-report format. | Does it stop for missing authority, conflicts, failed checks, secrets, production actions, or unapproved choices? | Guessing a value, bypassing a failing check, or treating ambiguity as permission. |
| Independent reviewability | Separates implementation from review where risk or scope warrants it and makes artifacts readable without hidden session context. | Can a read-only reviewer assess plan conformance, diff, evidence, and unresolved risks? | The executor validates and accepts its own assumptions. |
| Scoped maintainability | Is concise, path- or task-scoped, versioned with the repository, and updated only from observed conventions. | Does it avoid duplicating the plan or applying rules to unrelated work? | A large, stale instruction file with conflicting rules. |

## Recommended Artifact Set and Contracts

| Artifact | Use it for | Minimum contract | Do not use it for |
| --- | --- | --- | --- |
| Plan-bound implementor orchestrator | Delivering one reviewed, bounded plan from its entry gate through its final product and evidence handoff. | Read the plan and applicable instructions; build a plan-step ledger; delegate only required specialist workers in dependency order; integrate outputs; run or delegate final validation; return the final product, completed-step evidence, required human actions, or one blocker report. | Selecting product scope, architecture, acceptance, or deployment authority. |
| Plan-specific specialist subagent | Producing one bounded output required by a named plan step, such as a document, code change, configuration update, test result, security assessment, or release evidence. | Receive the named step(s), inputs, output location, allowed paths/tools, validation, and return format; perform only that delegation; report evidence and blockers to the orchestrator. | Owning the whole plan, changing another worker's area, accepting the final product, or choosing an unapproved approach. |
| Path-specific instruction | Stable, verified conventions for a language, module, or infrastructure directory. | Explain layout, command sequence, required checks, protected files, and local evidence rules; apply only to matching paths. | Work-item-specific steps or transient rationale already contained in a plan. |
| Implementation skill | A repeatable method that requires several ordered actions, such as a controlled migration or test-evidence workflow. | State entry criteria, procedure, resources, outputs, validation, and stop conditions; link templates or checklists. | A container for credentials, external connection configuration, or general repository policy. |
| Task template or execution checklist | Consistent task handoff within a plan. | Capture action, target, expected output, validation, evidence location, and failure behavior. | Replacing target-specific detail with placeholders at execution time. |
| Validation and evidence format | Reporting an executed plan step or work item. | Record plan step, changed paths, command and working directory, exit code or observation, evidence location, and remaining limitations. | Declaring acceptance or concealing failed/unavailable checks. |
| Read-only implementation reviewer | Checking plan conformance, regression risk, missing validation, and evidence sufficiency. | Review the plan, diff, command results, and evidence; report findings in severity order; do not edit or accept. | Repairing the change, making risk decisions, or substituting for human acceptance. |
| Narrow automation | Deterministic formatting, validation, or evidence collection already proven locally. | Have a named owner, documented inputs/outputs, non-secret configuration, a failure mode, and an exact command or trigger. | Encoding uncertain policy, privileged deployment, or irreversible mutation. |

## Best Practices

1. **Bind every execution artifact to one plan.** Include the plan path, work-item identifier, source references, and only the relevant plan steps. Refuse to execute when the plan is missing, unapproved where approval is required, or materially inconsistent with the repository state.
2. **Make one orchestrator accountable for end-to-end delivery.** It must create a plan-step ledger before work starts; assign every executable step to itself or a specialist worker; wait for dependency gates; integrate all outputs; and finish only when the final product and final validation evidence required by the plan exist. A required human review or acceptance gate may remain `Ready for review`; it must not be represented as complete or self-approved.
3. **Choose specialist subagents from the plan, not from a fixed team shape.** A documentation-only plan may need a document writer and reviewer; a code change may need a coding agent and tester; an infrastructure change may also need configuration, security, and evidence workers. Do not invoke a specialist whose capability is not required by a named plan task.
4. **Make authority explicit.** Preserve the separation among source authority, planning authority, implementation evidence, and human acceptance. An executor may implement and report; it must not approve requirements, accept risk, or self-accept completion.
5. **Use verified facts, not anticipated conventions.** Add commands, working directories, tool versions, environment prerequisites, expected output, and workarounds only after they have been observed and checked. Mark unverified facts as discovery work or a blocker.
6. **Keep instructions narrow and non-conflicting.** Put durable path-level rules in scoped instructions, repeatable process in skills, and temporary work-item direction in the plan. Do not duplicate the same rule across all three unless one is a short reference to the other.
7. **Grant the minimum useful capability.** Prefer read/search for review, add edit only for an implementation role, and add terminal or external tools only when a named validation or approved operation requires them. Separate read-only inspection from approved mutation when an external system is involved.
8. **Put a check after each material change.** State its command or inspection method, working directory, prerequisites, expected result, and what to record. Run the narrowest relevant check first, then the required broader check.
9. **Make evidence a required output.** Require a compact implementation report: plan steps completed; files changed; commands, working directories, and exit status; observed key output; evidence links; and remaining human actions. Preserve failed or unavailable validation as evidence, not as an omission.
10. **Define stop conditions before execution.** Stop for source conflict, unknown material value, new dependency, credential or personal-data need, privileged or production action, scope change, unavailable validation, or unexpected result. Use the plan's blocker format: `step`, `observed fact`, `command/output or path`, `impact`, `decision or input needed`, and `safe next action`.
11. **Review independently in proportion to risk.** At minimum, a human reviews generated changes and validation. Use a separate read-only reviewer artifact for multi-file, security-sensitive, externally mutating, or infrastructure work; it should assess both the diff and plan/evidence conformance.
12. **Pilot and measure before standardizing.** Trial the artifacts on a low-risk work item. Record unplanned decisions, incorrect targets, unavailable commands, review findings, and staleness. Promote only facts that repeatedly reduce implementation ambiguity.

## Implementation-Readiness Gate

Do not create or invoke a plan-bound implementation agent unless every applicable statement is true:

- [ ] The physical work-item plan has a singular observable objective, named authority, scope boundary, target map, ordered atomic tasks, and final evidence requirements.
- [ ] The plan identifies actual repository paths or a bounded discovery step and does not leave a material architecture, policy, value, or approval to the executor.
- [ ] Applicable instruction files and skill resources are identified and non-conflicting.
- [ ] One implementor orchestrator is responsible for the whole plan, and a plan-step ledger maps every executable step to that orchestrator or a named specialist worker.
- [ ] Each proposed specialist worker has a plan-required capability, a bounded delegation, minimal tools and paths, a defined output location, and a return condition.
- [ ] Required tools, editable paths, environments, and external boundaries are known and can be limited to each delegated task.
- [ ] Validation commands or inspections, their working directories, prerequisites, expected results, and evidence location are known or the task is explicitly a bounded discovery item.
- [ ] Stop conditions protect failed validation, secrets, production or external mutation, scope change, and human approval boundaries.
- [ ] A reviewer and acceptance authority are named for work that needs them.

A failed item is a blocker or a reason to revise or split the plan; it is not a prompt for the executor to infer the missing control.

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| Give an agent only the research document or high-level issue | Minimal artifact overhead. | The executor must infer scope, targets, task order, validation, and authority boundaries. | Conflicts with local work-item-plan guidance and VS Code specificity guidance. |
| Use one general-purpose implementation agent and repository-wide instructions | Simple invocation model. | Broad tools and broad instructions increase accidental scope, conflicting rules, and stale guidance. | VS Code advises limiting tools and scoping instructions; GitHub warns that multiple instruction sets can conflict. |
| Recommended: plan-bound implementor orchestrator with plan-directed specialist workers, scoped instructions, skills, validation format, and independent review as needed | Complete plan delivery, clear handoffs, low reasoning burden per worker, least privilege, evidence, and maintainability. | Requires verified repository knowledge, clear orchestration rules, and ownership of reusable artifacts. | Aligns with VS Code planning, verification, context, focused subagent use, and tool-scoping guidance; exact workers depend on the plan and local implementation surface. |
| Fully automated implementation and deployment workflow now | Potential speed after maturity. | Unsafe without known commands, environment controls, secrets model, rollback, and approval boundaries. | Current repository evidence does not justify it. |

## Recommendation

Adopt the quality model and readiness gate in this document as the acceptance standard for future implementer artifacts. Define the implementor artifact as the plan-bound **end-to-end delivery orchestrator**, rather than a worker that merely makes changes and returns evidence. It must execute every executable plan step, coordinate only the specialist subagents that the plan needs, assemble the final product, complete the final validation, and produce the plan's required evidence handoff. Keep the work-item plan as the execution authority and add only the smallest supporting artifact that removes a repeated, verified source of ambiguity: a scoped instruction for stable local conventions, a skill for a repeatable process, a template for an evidence-bearing handoff, or a least-privilege specialist worker or reviewer for a known implementation surface.

For this repository, defer concrete implementer agents, infrastructure instructions, command catalogs, and automation until a first low-risk, technically defined work item supplies real paths, commands, environment boundaries, and review evidence. The first implementation plan should treat any missing fact as bounded discovery or a blocker, then feed validated facts back into the smallest appropriate reusable artifact.

This recommendation would change if a future approved technical baseline establishes a stable implementation layout, authoritative validation commands, deployment controls, and an operational access model. At that point, define artifacts from those observed facts and pilot them before applying them to consequential infrastructure work.

## Open Questions and Limitations

- **Open questions:** Which language, infrastructure toolchain, build/test commands, CI checks, evidence store, branch policy, deployment procedure, and review authority will govern the first implementation work item?
- **Unavailable evidence:** There is no current implementation source tree or historical implementation run from which to verify an executor's targets, tool list, command sequence, expected outputs, or operational boundaries.
- **Conflicting sources:** No material conflict was found. VS Code and GitHub documentation describe product capabilities and practices rather than prescribing this repository's exact governance. The local plan research supplies the more specific work-item boundary.
- **Validation limitations:** The quality model is a synthesis of documentation and repository research, not a controlled comparison of agent outcomes. It should be piloted on a low-risk work item and revised using observed ambiguity, validation failure, and review findings.

## Sources

- Repository context: [Agent-Executable Plans for Individual Work Items](./lightweight-copilot-delivery-plan-best-practices.md), dated 2026-08-05.
- Repository context: [Artifacts for Delivering Agent-Executable Plans from Research](./agent-executable-plan-delivery-artifacts.md), dated 2026-08-05.
- Visual Studio Code, [Best practices for using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices), page reviewed 2026-08-05.
- GitHub Docs, [Adding repository custom instructions for GitHub Copilot](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot), page reviewed 2026-08-05.