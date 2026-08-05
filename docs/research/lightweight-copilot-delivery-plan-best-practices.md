# Agent-Executable Plans for Individual Work Items

> Research date: 2026-08-05

## Question and Decision

- **Research question:** What should a lightweight but detailed plan for one piece of work contain, how should it be derived from research or a similar source, and how should it be written so that a small GitHub Copilot agent can carry it out with very little additional reasoning?
- **Audience:** The two human project members who approve scope and review changes, plus GitHub Copilot acting as the implementation agent.
- **Decision this supports:** Whether to adopt a standard, repository-resident implementation-plan format for individual work items rather than use a project plan or a high-level backlog item as the agent's instructions.
- **Scope:** A plan for one bounded change, investigation, configuration change, documentation change, defect repair, or small feature. It begins from an approved research document, requirement, issue, decision record, or equivalent source and ends when the specific work item is implemented, verified, and handed back for human review. It does not prescribe project roadmaps, team ceremonies, portfolio reporting, or organisation-mandated controls.
- **Time boundary:** Public sources and repository context were reviewed on 2026-08-05. GitHub, VS Code, and Copilot capabilities can change.

## Executive Summary

A work-item plan is an **implementation recipe with evidence**, not a project plan. It converts an approved source into a bounded sequence of concrete operations: inspect named inputs, make specific edits in named locations, run specified checks, record outputs, and stop for a human decision when a stated condition occurs.

For a small agent, the plan must remove avoidable choices. It should state the source claims to implement, target repository paths or discovery commands, exact intended changes, ordered atomic tasks, expected outputs, validation commands and expected results, prohibited changes, and escalation conditions. A capable agent may still need to inspect code, but it should not need to infer the work item's purpose, scope, success criteria, sequencing, or approval boundary.

The recommended model is:

```text
Research / requirement / decision
  -> Extraction of implementable claims
  -> One work-item plan
  -> Ordered atomic tasks with checks
  -> Code or configuration change and evidence
  -> Human review and acceptance
```

This is proportionate for two people because GitHub Issues and pull requests can hold the work record and implementation evidence, while the plan keeps the source-to-change reasoning durable. GitHub Issues support dependencies, sub-issues, and links to pull requests. [GitHub Docs, About issues, current page reviewed 2026-08-05](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues)

## Findings

### Observed Facts

- VS Code recommends breaking complex work into smaller, well-scoped steps and including expected outputs, tests, or acceptance criteria so the agent can verify its own work. It also recommends providing relevant context through named files, folders, symbols, codebase context, and terminal output. [VS Code, Best practices for using AI in VS Code, page reviewed 2026-08-05](https://code.visualstudio.com/docs/agents/best-practices)
- VS Code recommends separate exploration, planning, implementation, and review for complex multi-file changes. Plans should be reviewed before execution, and generated changes should be reviewed and tested. [VS Code, Best practices for using AI in VS Code, page reviewed 2026-08-05](https://code.visualstudio.com/docs/agents/best-practices)
- VS Code guidance says a clear prompt states inputs, outputs, constraints, and expected behaviour. It recommends decomposing complex tasks and avoiding vague requests. [VS Code, Best practices for using AI in VS Code, page reviewed 2026-08-05](https://code.visualstudio.com/docs/agents/best-practices)
- GitHub Issues can track a specific change, assign responsibility, express blocking relationships, form a hierarchy with sub-issues, and link to pull requests. [GitHub Docs, About issues, current page reviewed 2026-08-05](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues)
- GitHub Copilot supports repository-wide, path-specific, and agent-specific instructions. GitHub recommends avoiding conflicting instruction sets; durable repository knowledge such as build and validation rules belongs there rather than in each transient request. [GitHub Docs, Adding repository custom instructions for GitHub Copilot, current page reviewed 2026-08-05](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)
- The Scrum Guide describes a plan as actionable and updated as learning occurs, and a Definition of Done as a shared quality state for completed work. It also states that Product Backlog items become ready as they acquire enough transparency to be completed within one Sprint. [The 2020 Scrum Guide, published 2020-11](https://scrumguides.org/scrum-guide.html)
- The repository's landing-zone SOR separates an approved requirement baseline from delivery, verification evidence, and individual requirement acceptance. Its requirements include objective pass criteria and required evidence. [Statement of Requirements: Landing Zone](../requirements/azure-landing-zone.md)

### Inferences

1. A small agent performs most reliably when the plan converts source material into an ordered algorithm: each task has one action, a known input, an expected output, and a validation or decision point. This directly applies VS Code's advice to decompose work, provide context, and include verification.
2. Research documents are usually not executable instructions. They contain evidence, alternatives, recommendations, and uncertainty. Before an agent implements anything, a human or planning agent must identify the approved recommendation, rejected alternatives, unresolved questions, and constraints that the work item must honour.
3. The appropriate planning unit is one independently reviewable pull request or similarly bounded change. If the work needs more than one independently acceptable outcome, contains an unresolved design choice, or cannot be verified as one coherent change, it should be split into separate work items or preceded by a time-boxed discovery item.
4. File names alone are not enough. A plan should say what to find in each file, what to change, what must remain unchanged, and how to confirm the change had its intended effect.
5. Precise stop conditions are a key safety mechanism. They preserve the small agent's limited reasoning budget and prevent it from inventing policy, silently choosing an architecture, or treating a failed check as success.
6. For the existing landing-zone work, the SOR remains the authority for required outcome and verification intent. A work-item plan can derive tasks from requirement IDs, but must not amend requirements or mark them accepted without the named human authority.

## Boundary: Work Item, Not Project

A work-item plan answers: **how do we complete this one bounded change safely and prove it?** It does not answer: **how do we run the whole project?**

| Include in a work-item plan | Exclude unless this work item directly needs it |
| --- | --- |
| The approved source claims being implemented | Project roadmap, release roadmap, or delivery cadence |
| Named files, modules, commands, and interfaces | Team roles and recurring ceremonies |
| Exact task order and expected intermediate outputs | Portfolio metrics, velocity, estimates, or charts |
| Per-task checks and final acceptance evidence | A generic backlog hierarchy |
| Explicit non-goals and prohibited changes | Design alternatives already rejected for unrelated work |
| Escalation conditions and human decisions needed | Broad organisational governance rules already held elsewhere |

The plan should normally be short enough to execute in one agent session. Its detail comes from precision, not from length. A one-file documentation correction may need five tasks; a multi-file infrastructure change may need ten to twenty. If a plan grows because it contains several separately reviewable changes, split the work item.

## From Research to an Executable Work-Item Plan

### 1. Establish the Authoritative Input

Start with one primary source and identify the exact portions that authorise the work.

| Input type | Extract | Do not infer without approval |
| --- | --- | --- |
| Research document | The labelled recommendation, supporting evidence relevant to the change, limitations, and stated uncertainties | That a suggested option is approved, or that an unverified claim is fact |
| Requirement or SOR | Requirement ID, required outcome, constraint, verification method, pass criterion, required evidence, and acceptance authority | A technical solution not stated or approved elsewhere |
| Decision record / ADR | Decision, consequences, rejected alternatives, constraints, and linked components | A change that reverses or extends the decision |
| Defect or issue | Reproduction, expected and actual behaviour, affected version or path, and acceptance test | Root cause when it has not been investigated |
| Existing implementation | Current behaviour, conventions, validation commands, and local ownership boundaries | That the existing behaviour is intentional |

Record the source in the plan with a path or URL and an anchor such as a requirement ID or heading. Where source material conflicts, name the authority order and stop for a human decision rather than trying to reconcile it during implementation.

### 2. Produce an Implementation Brief Before Tasks

The planner must convert the source into the following brief. This is the discriminator: if any field is unknown and material, the result is a discovery task or an escalation, not an implementation plan.

| Brief field | Required content |
| --- | --- |
| Change objective | One observable result of this work item. |
| Approved source claims | Exact IDs, headings, or quotations paraphrased faithfully. |
| Scope | What will change in this work item. |
| Non-goals | What must not change, including nearby tempting work. |
| Target surface | Known files, modules, APIs, environments, or a bounded discovery command to locate them. |
| Constraints | Compatibility, security, operational, design, and repository rules that cannot be changed by the agent. |
| Completion evidence | Exact checks, tests, inspection, demonstration, or review record needed for completion. |
| Human decisions | Decisions that must occur before or after the implementation. |

### 3. Decompose into Atomic Tasks

A task is atomic when an agent can complete it without choosing among materially different solutions. Use a verb, a target, a specified change, an output, and a check.

| Weak task | Why it is not agent-executable | Atomic replacement |
| --- | --- | --- |
| "Implement network security." | It has many possible designs and no proof of completion. | "In `modules/network/main.tf`, add the approved private-endpoint resource using the existing module variable pattern. Do not add public ingress. Run `terraform fmt -check` and `terraform validate` from `infra/`." |
| "Update monitoring." | Does not identify signal, destination, trigger, or test. | "In `<alert file>`, add the named alert rule with the threshold from DEC-012. Route it to `<existing channel>`. Use `<test command>` and attach the observed alert ID to the issue." |
| "Fix the deployment problem." | Root cause and affected component are not stated. | "Run `<existing reproduction command>`. In `<named file>`, change `<current setting>` to `<approved setting>`. Re-run the command and confirm `<expected output>`." |
| "Research the right implementation." | The expected decision and time limit are absent. | "Within two hours, compare options A and B against criteria X, Y, and Z. Update DEC-017 with evidence links, a recommendation, and a request for the named human decision. Do not modify production code." |

### 4. Give Each Task a Verification Gate

Every task must end in exactly one of the following states:

- **Verified:** A command, test, inspection, or demonstration produced the expected result.
- **Ready for review:** The task has generated a specific artefact that needs human approval before the next task.
- **Blocked:** A stated stop condition has occurred. Record the observed fact, relevant output, and decision required.

Do not use "complete" as a task state without stating which of these conditions demonstrates it.

## Recommended Work-Item Plan Template

```markdown
# Plan: <Short work-item name>

> Status: Draft | Approved for implementation | Blocked | Ready for review | Accepted
> Work item: <GitHub issue URL or identifier>
> Source of authority: <path/URL and exact heading, requirement ID, or decision ID>
> Prepared: <YYYY-MM-DD>
> Human approver: <name or role>

## 1. Objective

Deliver <one observable result> for <user, operator, or system>.

## 2. Source Extraction

### Approved to implement

- <Source ID/heading>: <faithful, concise implementation-relevant statement>

### Constraints

- <Source ID/heading>: <constraint the agent must preserve>

### Unresolved or excluded source material

- <Item>: <why it is not part of this plan or human decision needed>

## 3. Scope Boundary

**Change in this work item**
- <Specific component, behaviour, configuration, or document change>

**Do not change**
- <Explicit non-goal or protected neighbouring surface>

## 4. Preconditions

- [ ] Repository is at <branch/commit or stated baseline>.
- [ ] <Required access, tool, environment, fixture, or existing decision> is available.
- [ ] Read <repository instruction path> and <specific source paths>.
- [ ] Stop and report if <precondition cannot be confirmed>.

## 5. Target Map

| Target | Locate / current state | Required change | Preserve |
| --- | --- | --- | --- |
| `<path>` | `<symbol, heading, resource, or discovery command>` | `<precise change>` | `<behaviour, interface, convention, or no-go area>` |

## 6. Ordered Tasks

| Step | Action | Expected output | Verify before continuing | On failure or ambiguity |
| --- | --- | --- | --- | --- |
| 1 | Read `<source path>` at `<heading/symbol>` and inspect `<target>`. Confirm it matches the target map. | A short confirmation note or discovered mismatch. | `<exact observation or command>` | Stop; report mismatch with path and excerpt. |
| 2 | Edit `<path>`: `<precise intended change>`. Do not modify `<protected path/behaviour>`. | `<file/resource/document state>` | `<format/lint/unit check>` | Revert only the attempted change if needed; report the check output. |
| 3 | Edit `<path>`: `<next precise change>`. | `<file/resource/document state>` | `<targeted check>` | Stop; report the dependency or decision needed. |
| 4 | Run `<exact command>` from `<working directory>`. | Exit code `0` and `<expected key output>`. | `<command and expected result>` | Do not claim completion; attach output and mark Blocked. |
| 5 | Update `<evidence location>` with `<test result, screenshot, plan output, or decision link>`. | Reviewable evidence. | Confirm the evidence links to `<source ID>` and this work item. | Stop; request human review if evidence cannot be produced. |

## 7. Final Acceptance Check

- [ ] <Observable acceptance criterion linked to the source>.
- [ ] `<exact validation command>` passes with `<expected result>`.
- [ ] <Required manual inspection, demonstration, or security check> is recorded at `<location>`.
- [ ] The pull request links this work item and lists changed files, commands run, results, and remaining limitations.
- [ ] <Named human> reviews and records acceptance. The agent must not self-accept.

## 8. Stop Conditions and Escalation

Stop implementation and create a concise blocker report when any condition applies:

- A source, target, or current implementation conflicts with this plan.
- Completing a task requires a new dependency, credential, public endpoint, permission, provider, data migration, or unapproved design choice.
- A required validation command is unavailable, fails, or produces a result different from the expected result.
- The change would alter the stated objective, scope boundary, acceptance criterion, cost, security posture, production access, or an approved decision.
- A secret, personal data, or production action is required and no explicit procedure authorises it.

Blocker report format: `step`, `observed fact`, `command/output or path`, `impact`, `decision or input needed`, and `safe next action`.
```

## Writing Rules for Low-Reasoning Execution

Use the following rules when authoring or reviewing the plan.

1. **One work item, one objective.** Do not combine implementation, unrelated refactoring, operational rollout, and documentation cleanup because they occur in the same area.
2. **Name every source.** Link to the research heading, requirement ID, decision, or issue that authorises the task. A generic link to a long document is insufficient.
3. **Use concrete verbs.** Prefer `read`, `locate`, `add`, `replace`, `remove`, `run`, `compare`, `record`, and `stop`. Avoid `consider`, `improve`, `ensure`, `handle`, and `make robust` unless followed by an observable action.
4. **Name the execution location.** State the path, symbol, resource name, heading, command working directory, and expected artefact location. If a target is not known, provide one bounded discovery command and a decision condition.
5. **State what must remain unchanged.** This limits collateral edits and unrequested redesign.
6. **Give values or a source for values.** State thresholds, names, formats, regions, versions, and identifiers, or identify the authoritative value to read. Do not ask an agent to choose them implicitly.
7. **Put validation next to the change.** Do not defer all testing to a final generic task. Earlier checks make failures local and diagnosable.
8. **State expected results.** Include expected exit code, test count, response, resource property, document content, or evidence location. "Run tests" is not enough.
9. **Separate implementation from approval.** A task can prepare evidence for acceptance, but a named human performs acceptance when it has authority implications.
10. **Require a stop instead of a guess.** Whenever the plan cannot constrain a meaningful choice, make that choice an explicit human decision or a time-boxed discovery work item.

## Plan Quality Gate

Approve a work-item plan for an agent only when every answer is yes.

| Question | Pass condition |
| --- | --- |
| Is the source authority explicit? | Each implementation claim links to a source heading, ID, or decision. |
| Is the objective singular and observable? | A reviewer can decide whether the result exists without interpreting intent. |
| Is the scope boundary explicit? | The plan lists both what will change and what will not. |
| Can the agent find every target? | Each target has a path and symbol/resource/heading, or one bounded discovery action. |
| Is every task atomic? | No task requires an unstated architecture, policy, or product choice. |
| Is execution order explicit? | Dependencies are expressed as ordered steps or blockers. |
| Is each task falsifiable? | It has expected output and a check or a clear human review gate. |
| Are commands executable? | The working directory, command, prerequisites, and expected result are stated. |
| Are non-agent decisions protected? | Stop conditions cover approvals, secrets, production, scope, and failed validation. |
| Is final evidence sufficient? | A reviewer can link the source, changed files, validation result, and acceptance record. |

A `no` answer means the plan needs clarification, discovery, or a human decision before implementation. It does not mean the agent should fill the gap with a plausible assumption.

## Prompt Pattern for a Small Agent

Give the agent the plan and only the contextual files it needs for the current step. Do not ask it to reinterpret the entire research document on every execution request.

```text
Execute steps <N> to <M> of <path to work-item plan>.

Read the plan's source references, preconditions, target map, and the named
repository instructions before editing. Perform only the stated steps in order.
At every verification gate, compare the observed result to the expected result.
Stop and return the plan's blocker-report format if a stop condition occurs.

When finished, report:
1. each completed step and the files changed;
2. each command run, its working directory, exit code, and relevant output;
3. evidence recorded; and
4. remaining human review or acceptance actions.
Do not mark the work item accepted.
```

This prompt applies VS Code guidance to provide specific inputs, constraints, expected outputs, and relevant file context. [VS Code, Best practices for using AI in VS Code, page reviewed 2026-08-05](https://code.visualstudio.com/docs/agents/best-practices)

## Example: Turning a Research Recommendation into a Plan

Suppose research recommends a private administrative-access route and states that no public management endpoint should be introduced. The planner should not create the task "implement secure administration." It should extract the approved conclusion and then produce steps such as:

1. Read the named recommendation and decision record; confirm the permitted access route and any unresolved network decision.
2. Locate the existing Terraform module and the resource or variable that controls administrative ingress.
3. Change only that resource to use the approved private route, preserving existing workload ingress.
4. Run formatting and Terraform validation from the stated directory; inspect the generated plan for the absence of a public management endpoint.
5. Record the plan output and the requirement/decision IDs in the pull request.
6. Stop for human approval before applying changes to a shared or production environment.

This example deliberately leaves paths and values as placeholders. An executable plan must replace every placeholder with a repository-specific value or convert it into a bounded discovery step with an explicit stop condition.

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| Research document passed directly to an agent | No additional planning artefact. | Research contains alternatives, uncertainty, and high-level recommendations; the agent must infer scope, targets, and task order. | Research is valuable source material but is not normally an execution recipe. |
| High-level issue with a short acceptance list | Low administrative overhead. | Insufficient detail for a small agent; encourages exploration and unrecorded decisions. | GitHub Issues can record work, but their content must still provide adequate context and checks. |
| Recommended: one detailed work-item plan derived from source material | Bounded execution, traceability, repeatable review, and low reasoning demand on the agent. | Planning takes time and becomes stale if not updated when a human decision changes. | Aligns VS Code guidance on specificity, decomposition, context, expected outputs, and verification. |
| Full technical design and project plan for every change | Stronger governance and audit trail. | Disproportionate overhead for small work; duplicates project-level artefacts and slows adaptation. | Appropriate only when risk, regulation, contract, or change complexity requires it. |

## Recommendation

Adopt the work-item plan template and quality gate in this document for consequential changes that will be delegated to a small agent. Treat the plan as an intermediate artefact between research or requirements and implementation.

The author of the plan should first extract approved claims, constraints, unresolved decisions, and completion evidence from the source. They should then write only atomic tasks with named targets, exact expected outputs, validation gates, and stop conditions. The executing agent should receive the plan and only the plan's relevant contextual files, work through one ordered step at a time, and return evidence or a blocker rather than making a material inference.

Use a shorter issue body only for trivial changes where the issue itself can meet every item in the quality gate. Split the work or run a time-boxed discovery item whenever a task would require the agent to choose an architecture, policy, security boundary, or product outcome.

For landing-zone delivery, link every work-item plan to the relevant SOR requirement, decision, and evidence expectation. Preserve the SOR's distinction between a requirement baseline, implementation evidence, and named-human acceptance.

## Open Questions and Limitations

- **Open questions:** Which repository path should contain work-item plans; which build, test, lint, Terraform, security, and deployment commands are authoritative; which decisions and requirements are approved for the first landing-zone work item; and what agent capabilities and permissions will be used?
- **Unavailable evidence:** The repository does not yet supply an implementation codebase, actual Terraform layout, CI workflow, issue template, branch policy, deployment process, or a chosen first work item. Therefore the template cannot name real paths, commands, expected outputs, or approvers for a concrete plan.
- **Conflicting sources:** No direct conflict was found. GitHub and VS Code documentation describe capabilities and recommended interaction patterns, not a mandatory planning format. Scrum describes a complete framework; this document uses only its general evidence on actionable plans, transparency, and completion criteria and does not claim the two-person workflow is Scrum.
- **Validation limitations:** The proposed format has been checked for internal completeness against the cited guidance but has not yet been trialled against a real work item with the target small agent. Its practical adequacy should be tested on one low-risk work item, measuring whether the agent needed an unplanned decision, touched an unplanned area, or could not run a named validation.

## Sources

- Visual Studio Code, [Best practices for using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices), current page reviewed 2026-08-05.
- Visual Studio Code, [Prompt examples](https://code.visualstudio.com/docs/agents/guides/prompt-examples), current page reviewed 2026-08-05.
- GitHub Docs, [About issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues), current page reviewed 2026-08-05.
- GitHub Docs, [Adding repository custom instructions for GitHub Copilot](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot), current page reviewed 2026-08-05.
- Ken Schwaber and Jeff Sutherland, [The 2020 Scrum Guide](https://scrumguides.org/scrum-guide.html), published 2020-11.
- Repository context: [Statement of Requirements: Landing Zone](../requirements/azure-landing-zone.md), version 1.0, dated 2026-08-04.
