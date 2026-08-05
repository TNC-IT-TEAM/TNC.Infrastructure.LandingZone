# Lightweight Delivery Plans for a Two-Person Project Using GitHub Copilot

> Research date: 2026-08-05

## Question and Decision

- **Research question:** What should a good lightweight implementation plan contain, how should it be written, and how should a two-person project operate it when GitHub Copilot will use the plan to deliver work?
- **Audience:** The two human project members who set priorities, review work, and accept outcomes; GitHub Copilot acting as an implementation assistant.
- **Decision this supports:** Whether to adopt a small repository-resident plan and a minimal GitHub Issues/Project workflow instead of a heavier project-governance model.
- **Scope:** Planning and execution of a small software, infrastructure, or documentation change delivered from one repository. It covers plan content, writing rules, Copilot context, work-item decomposition, review, and change control. It does not prescribe an organisation's mandatory security, procurement, legal, regulatory, or release controls.
- **Time boundary:** Public sources and repository context were reviewed on 2026-08-05. Product capabilities and Copilot behaviour can change.

## Executive Summary

A good lightweight plan is an **executable agreement**, not a miniature project-management system. It gives the two humans and Copilot the minimum durable context needed to make correct local decisions: the desired outcome, the scope boundary, measurable success and acceptance evidence, constraints, the intended technical direction, the ordered work, dependencies and risks, and the validation and review path.

For this project size, maintain one short Markdown plan in the repository for the current outcome, use GitHub Issues as the living record of committed work, and use a minimal Project board only if it genuinely improves visibility. A plan should normally be one to three pages before appendices; it should link to source material and repository locations rather than duplicate them. Copilot should receive the plan and the relevant source files as explicit context for each delivery request. Repository instructions should contain only durable rules that apply across work, not the temporary plan.

The recommended lightweight governance model is:

```text
Approved outcome and scope boundary
  -> One current delivery plan in the repository
  -> Small, ordered GitHub Issues (the delivery record)
  -> Pull requests, checks, and demonstrable evidence
  -> Human review and recorded acceptance
```

This is proportionate because GitHub Issues already support hierarchy, dependencies, and pull-request links, while GitHub Projects can show the same work as a table or board. [GitHub Docs, About issues, current page reviewed 2026-08-05](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues) [GitHub Docs, About Projects, current page reviewed 2026-08-05](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)

## Findings

### Observed Facts

- The Scrum Guide defines the Product Backlog as an emergent, ordered list of what is needed to improve a product. Refinement continuously adds detail, order, and size; only items sufficiently transparent to be completed in one Sprint are ready for selection. [The 2020 Scrum Guide, published 2020-11](https://scrumguides.org/scrum-guide.html)
- The Scrum Guide defines a Sprint Backlog as the goal, selected work, and actionable delivery plan. It is a visible, real-time plan that changes as the team learns. It also defines a Definition of Done as the shared quality state required before work is complete. [The 2020 Scrum Guide, published 2020-11](https://scrumguides.org/scrum-guide.html)
- Scrum is explicitly described as a lightweight framework. Its empirical model depends on transparency, inspection, and adaptation rather than predictive detail. [The 2020 Scrum Guide, published 2020-11](https://scrumguides.org/scrum-guide.html)
- GitHub Issues support assignees, labels, milestones, issue types, sub-issues, blocking dependencies, and links to pull requests. Mentioning an issue in a pull request creates a reference, and closing keywords can close a linked issue. [GitHub Docs, About issues, current page reviewed 2026-08-05](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues)
- GitHub Projects is an adaptable table, board, and roadmap over issues and pull requests. It supports custom fields, saved views, automation, and bidirectional synchronisation with issue metadata; it does not require a specific delivery methodology. [GitHub Docs, About Projects, current page reviewed 2026-08-05](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)
- GitHub Copilot custom instructions can provide repository-specific context about how to build, test, and validate changes. Repository-wide instructions belong in `.github/copilot-instructions.md`; path-specific instructions can be placed under `.github/instructions/`; nearby `AGENTS.md` files can give agent instructions. Conflicting instruction sets should be avoided. [GitHub Docs, Adding repository custom instructions for GitHub Copilot, current page reviewed 2026-08-05](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)
- VS Code guidance says that specific requests and relevant context improve agent responses; files, folders, symbols, codebase context, and terminal output can be explicitly attached to a request. Agent-created changes should be reviewed before they are accepted. [VS Code, Use chat in VS Code, updated 2026-07-29](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode)
- User stories are short, user-focused descriptions of desired outcomes. Their useful detail is developed through conversation and confirmation through acceptance criteria; a story that exceeds the team's completion horizon should be split. This is practitioner guidance rather than a formal standard. [Atlassian, User stories with examples and a template, page reviewed 2026-08-05](https://www.atlassian.com/agile/project-management/user-stories)
- UK Government Digital Service guidance recommends testing the riskiest assumptions with the minimum work needed to test them, then iterating based on learning. [GOV.UK Service Manual, How the alpha phase works, last updated 2019-05-08](https://www.gov.uk/service-manual/agile-delivery/how-the-alpha-phase-works)
- The repository has an approved SOR baseline for the landing zone. It expressly separates that baseline from delivery, technical-design approval, verification evidence, and individual requirement acceptance. [Statement of Requirements: Landing Zone](../requirements/azure-landing-zone.md)

### Inferences

1. A two-person team does not need formal roles, estimation rituals, a long-range Gantt chart, or an elaborate issue taxonomy to gain the benefits of planning. It does need explicit decisions on priority, scope, quality, and acceptance, because those are the information gaps that otherwise cause rework or ambiguous Copilot output.
2. The plan must have two layers. A stable **outcome layer** records the goal, non-goals, constraints, and acceptance conditions. A changeable **execution layer** records the next small work items, sequence, uncertainty, and validation. Combining them without labelling makes it easy for temporary implementation detail to be mistaken for approved scope.
3. Copilot needs operational instructions, not aspirational prose. A statement such as "make it secure and production ready" cannot be independently checked. A statement such as "run `terraform validate` in `infra/`; no public management endpoint; record its output in the pull request" gives an agent a bounded action and a falsifiable check.
4. The plan should be deliberately incomplete about distant work. Detail only the next delivery horizon: work that the humans intend to start after the current work is complete. Keeping later work at outcome or workstream level preserves room to learn and reduces plan-maintenance cost.
5. A human must retain approval authority for changes that alter outcome, scope, budget, delivery date, risk acceptance, credentials, external dependencies, or production access. Copilot can identify, draft, and implement options, but it cannot supply accountable approval.
6. For the existing landing-zone work, the approved SOR is the source of outcome and verification intent. The lightweight plan should link to relevant requirement IDs and evidence rather than duplicate or silently amend them.

## What a Lightweight Plan Looks Like

### Required Content

A useful plan answers the following questions in the order Copilot and reviewers need them.

| Section | Required content | Writing standard |
| --- | --- | --- |
| Outcome | One or two sentences describing the user, operational, or business result. | State the result, not the proposed technology. |
| Scope boundary | Explicit in-scope and out-of-scope bullets. | Include likely temptations that must not be delivered. |
| Source and context | Links to the request, SOR requirements, design decision, issue, and relevant repository paths. | Link rather than copy. State which source wins if sources conflict. |
| Success and acceptance | Observable acceptance criteria and required evidence. | Each criterion must be testable by inspection, automated check, demonstration, or documented human decision. |
| Constraints and guardrails | Non-negotiable technical, security, time, cost, compatibility, or operational limits. | Use imperative, precise language; name the authority for unresolved constraints. |
| Technical approach | The intended route, affected components, interfaces, data, and important alternatives rejected or deferred. | Give enough detail to direct work, not a full design unless risk requires it. |
| Delivery slices | Ordered work items, each with a clear output and validation. | Each item should be independently reviewable and small enough to finish in a few days. |
| Dependencies, assumptions, and risks | Only items that can change sequence, scope, or outcome. | Give each an owner, trigger, and next action. Convert unknowns into time-boxed discovery work. |
| Verification and release | Commands or manual checks, environment, evidence location, review path, and release/rollback decision where applicable. | Distinguish checks Copilot can run from checks requiring a human or external system. |
| Change rules | What may be adapted by the implementer and what must be re-approved. | Make the escalation boundary explicit. |

### Minimum Plan Template

The following is a recommended template. It is intentionally compact, but every heading carries delivery information.

```markdown
# <Outcome Name> Delivery Plan

> Status: Draft | Ready | In delivery | Accepted
> Owner: <human accountable for priority and acceptance>
> Technical reviewer: <human accountable for implementation review>
> Last decision: <YYYY-MM-DD, link to issue/PR/comment>

## Outcome

<Describe the useful result and who benefits.>

## Scope

**In scope**
- <Outcome or capability>

**Out of scope**
- <Explicit boundary>

## Source and Context

- <Link to requirement, issue, ADR, or user request>
- <Link to affected repository paths and current implementation>
- **Authority order:** <e.g., approved SOR, then approved ADR, then this plan>

## Acceptance

- [ ] <Observable criterion and evidence, including any requirement ID>
- [ ] <Observable criterion and evidence>
- [ ] Required validation passes: `<exact command or manual test>`.
- [ ] <Named human> reviews and records acceptance in <issue, PR, or evidence record>.

## Constraints and Decisions

- <Non-negotiable constraint>
- <Decision already made and its link>
- <Open decision; owner; deadline or trigger>

## Intended Approach

<Concise description of the affected components, main flow, interfaces/data,
and the approach deliberately not being taken.>

## Delivery Slices

| Order | Work item and expected output | Depends on | Validation and evidence |
| --- | --- | --- | --- |
| 1 | <Discovery/spike or implementation output> | - | <check; decision/evidence location> |
| 2 | <Small independently reviewable change> | 1 | <test/inspection> |
| 3 | <Integration, documentation, or release-readiness output> | 2 | <test/demonstration> |

## Risks, Assumptions, and Change Rules

| Type | Item | Owner | Trigger / next action |
| --- | --- | --- | --- |
| Assumption | <What is believed> | <name> | <How and when it will be checked> |
| Risk | <What could prevent the outcome> | <name> | <Mitigation or decision trigger> |

The implementer may adapt task detail that preserves the outcome, scope,
constraints, and acceptance criteria. Human approval is required before changing
those items, adding a dependency, accepting a material risk, or releasing to a
production environment.
```

### Example of Good and Weak Wording

| Weak wording | Why it fails | Better wording |
| --- | --- | --- |
| "Set up secure infrastructure." | No boundary, verifier, or decision rule. | "Create separate test and production environments. Restrict administrative access to the approved private path. Evidence: `terraform validate`, a reviewed plan, and an access demonstration against NF1 and FR2." |
| "Add monitoring." | Does not identify what must be observable or who responds. | "Emit an alert when deployment fails, send it to the agreed operator channel, and document the first response step in the runbook. Demonstrate with a controlled failed deployment." |
| "Use best practices." | Delegates an undefined standard to the implementer. | "Use the repository's Terraform formatting, validation, and security checks. Do not introduce a new provider or public endpoint without an approved decision." |
| "Build the whole landing zone." | Too large to sequence, review, or prove. | "First prove the environment boundary with a minimal test environment. Then create the production equivalent. Treat remote administration as a separate, blocked slice pending the access decision." |
| "The agent should decide the details." | Loses human accountability on outcome-impacting decisions. | "Copilot may choose implementation details that meet the stated constraints. It must stop and raise a decision issue if the design changes public exposure, cost model, identity boundary, or acceptance evidence." |

## How It Should Be Written for Copilot

### Use an Agent-Executable Style

Write the plan as instructions that can be checked against the repository and validation output.

1. **Start with immutable context.** Link to the approved requirement, decision, and source files. Do not rely on a chat session remembering an earlier conversation.
2. **Use exact nouns.** Name the component, environment, API, folder, command, test suite, evidence record, and owner. Prefer `modules/networking` to "the networking code".
3. **Separate facts from choices.** Mark statements as `Decision`, `Constraint`, `Assumption`, `Open question`, or `Proposal`. Copilot should not treat a proposal as permission.
4. **State negative boundaries.** Include no-go areas, prohibited changes, unsupported environments, and non-goals. This reduces well-intended scope expansion.
5. **Attach a check to each change.** State how completion will be verified and whether the agent can perform it. A task without a completion check is only a suggestion.
6. **Specify the smallest safe change.** Identify the target file or module when known, existing patterns to follow, and whether new dependencies or abstractions are allowed.
7. **Make sequencing explicit.** Use ordered slices and native issue dependencies. A child issue shows containment; a blocking relationship shows sequence. GitHub supports both, and they answer different questions. [GitHub Docs, About issues, current page reviewed 2026-08-05](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues)
8. **Ask for evidence, not assurances.** Require test output, a screenshot, a plan, a deployment record, a review, or a decision link. Avoid claims such as "works correctly" without a stated observation.
9. **Keep durable rules separate.** Put recurring repository build, test, and coding guidance in Copilot instruction files. Keep the temporary outcome and current sequence in the plan. GitHub documents repository-wide, path-specific, and agent-specific instruction mechanisms. [GitHub Docs, Adding repository custom instructions for GitHub Copilot, current page reviewed 2026-08-05](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)
10. **Include a stop condition.** Tell Copilot to stop and request a human decision when assumptions fail, a required check cannot run, a new external dependency is needed, secrets are involved, scope changes, or a material risk appears.

### A Delivery Prompt Pattern

The plan is the durable source. Each Copilot request should be short and bind the agent to a specific slice:

```text
Implement delivery slice 2 from <link/path to plan>.
Read the linked requirements, the relevant repository instructions, and the existing implementation first.
Keep the change within the stated scope and constraints.
Run the plan's listed validation. Report changed files, validation results,
remaining risks, and decisions that require human approval. Stop rather than
inventing an answer when a listed stop condition is met.
```

This pattern follows VS Code guidance to provide specific requests and relevant context, while preserving human review of generated changes. [VS Code, Use chat in VS Code, updated 2026-07-29](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode)

## Two-Person Operating Model

### Responsibilities

Two people may carry more than one responsibility; the responsibilities should still be named for each outcome.

| Responsibility | Minimum accountability | May be the same person as |
| --- | --- | --- |
| Outcome owner | Prioritises work, confirms scope, accepts or rejects the outcome. | Technical reviewer for low-risk work, subject to a deliberate self-review rule. |
| Delivery owner | Maintains the plan and issues, coordinates execution, makes progress visible. | Outcome owner. |
| Technical implementer | Makes or directs the changes, runs validation, records evidence and uncertainties. | Either human; Copilot assists but does not own accountability. |
| Technical reviewer | Reviews design fit, change quality, security/operational implications, and validation evidence. | Outcome owner where risk is low; should be the other human for consequential changes. |

For a two-person team, do not simulate a committee. A decision is effective when the relevant owner records it in the plan, an issue, a pull-request comment, or an ADR, with date and rationale.

### Minimal Cadence

| Moment | Duration | Questions to answer | Record |
| --- | --- | --- | --- |
| Start of outcome | 30 to 60 minutes | What result matters, what is excluded, what proves success, and what is most uncertain? | First plan draft and initial ordered issues. |
| Before each slice | 10 to 15 minutes | Is the item still valuable, ready, small enough, and unblocked? What does done mean? | Issue updates and any plan revision. |
| Short daily or near-daily sync | 5 to 10 minutes | What changed, what is blocked, and is a decision needed today? | Update only blockers, decisions, and status. |
| After demonstrable increment | 15 to 30 minutes | Does evidence meet acceptance? What did we learn? What is the next highest-value slice? | PR/issue evidence, acceptance decision, reprioritised backlog. |
| End of outcome | 30 minutes | Was the outcome accepted, what remains, and what one process change is worth retaining? | Final acceptance and one improvement action if useful. |

This cadence is an adaptation of the transparency, inspection, and adaptation principles described in Scrum; it is not a claim that the team is practising Scrum unless it adopts the framework in full. [The 2020 Scrum Guide, published 2020-11](https://scrumguides.org/scrum-guide.html)

### Minimal GitHub Configuration

Use the simplest option that gives a reliable shared view.

| Need | Minimum mechanism | Do not add unless it changes a decision |
| --- | --- | --- |
| Durable plan | One versioned Markdown file close to the work or under `docs/`. | Separate planning software. |
| Committed work | GitHub Issues with owner, status, plan link, acceptance, and validation fields in the body. | A large custom issue-type hierarchy. |
| Work sequence | GitHub native blocking relationships and a short ordered table in the plan. | Labels that attempt to emulate dependencies. |
| Current view | Issue list, or one Project board with `Status` only. | Estimates, iterations, roadmaps, charts, and custom fields without an active decision use. |
| Review and evidence | Pull request linked to the issue; validation results and acceptance comment. | A parallel status report. |
| Repeatable agent behaviour | Concise repository instructions for build, test, validation, and durable conventions. | Task-specific plan content in global instructions. |

If a GitHub Project is used, begin with `Status` values `Backlog`, `Ready`, `In progress`, `In review`, `Blocked`, and `Done`. Add only `Priority` if there is a real prioritisation decision to make. Projects provide table and board views and custom fields but do not impose a methodology, so a minimal configuration is valid. [GitHub Docs, About Projects, current page reviewed 2026-08-05](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)

## Ready, Done, and Change Rules

### Definition of Ready

An item may be started when:

- its outcome and scope are clear enough to implement;
- it links to the current plan and relevant source requirement or decision;
- its acceptance and validation are known;
- its dependencies are resolved or explicitly marked as blockers;
- it is small enough to complete and review within a few days; and
- the human owner has ordered it ahead of other available work.

A discovery item is ready when its question, time box, expected output, and decision owner are stated. Discovery is not a disguised implementation commitment.

### Definition of Done

An item is done only when:

- the agreed change is present and reviewed;
- the specified automated and manual validation has passed or an approved exception is recorded;
- required documentation, configuration, or operational evidence has been updated;
- the pull request and issue link to each other and record material evidence; and
- the outcome owner accepts the item where acceptance is required.

For an increment that affects a baselined SOR requirement, evidence must map back to the relevant requirement and its stated verification method. The repository's SOR explicitly separates baseline approval from verification evidence and individual requirement acceptance. [Statement of Requirements: Landing Zone](../requirements/azure-landing-zone.md)

### Change Thresholds

| Change | Who may decide | Required record |
| --- | --- | --- |
| Task sequencing or implementation detail that preserves plan scope, constraints, and acceptance | Technical implementer | Issue or pull-request comment when material to review. |
| Split, merge, or reprioritise an unstarted delivery slice | Outcome owner | Plan and issue update. |
| Alter outcome, scope, acceptance, cost, target date, external dependency, public exposure, identity boundary, or material risk | Outcome owner and technical reviewer | Plan update plus decision record; update the source baseline where applicable. |
| Use or expose credentials, access production, accept security or recovery risk, or override a failed quality check | Named human authority under applicable policy | Explicit approval and evidence record. |

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| Chat-only plan | Fast to begin and conversational. | Context is transient; decisions, scope, and evidence are difficult to inspect later; Copilot requests may diverge. | VS Code supports contextual chat, but persistent repository instructions and files provide durable shared context. |
| Long formal project plan | Stronger baseline and reporting potential. | High maintenance cost for two people; encourages speculative detail and duplicate tracking. | Appropriate where contractual, regulatory, organisational, or risk controls require it. |
| GitHub Issues only | Low friction and direct connection to pull requests. | Goal, non-goals, design direction, and cross-item acceptance can fragment across issue threads. | GitHub Issues support work tracking and links, but a concise plan supplies outcome-level context. |
| Recommended: short versioned plan plus issues, with optional minimal Project | Makes intent, constraints, and acceptance durable while keeping execution close to code and pull requests. Supports adaptation without losing scope control. | Requires both people to update the plan when material decisions change. | Aligns repository context, GitHub tracking capabilities, iterative backlog refinement, and Copilot's need for specific context. |
| Full project board, formal ceremonies, and extensive fields | Can support multiple teams, reporting, and portfolio management. | Administrative work can exceed coordination benefit for two people. | Consider only when delivery scale, stakeholder reporting, or mandated governance increases. |

## Recommendation

Adopt the **short versioned plan plus small Issues** option.

1. Create one plan per meaningful outcome, based on the template above. Keep it current through delivery and archive it with the delivered work.
2. Detail only the next two to five delivery slices. Keep later work as outcomes or candidate work until evidence makes detail worthwhile.
3. Create an issue per slice that needs independent ownership, review, sequencing, or a pull request. Link it to the plan and use native GitHub dependencies for blockers.
4. Use a minimal Definition of Ready and Definition of Done. Do not create estimates, story points, ceremonies, fields, or reports unless the team uses them to make a recurring decision.
5. Attach the plan, relevant requirements, repository instructions, and target files when asking Copilot to deliver a slice. Require validation output and a decision/risk report in its completion response.
6. Require a human review before accepting consequential changes. For this repository, treat SOR baseline changes and individual requirement acceptance as named human decisions, consistent with the existing baseline.

The recommendation would change if the work becomes regulated, safety-critical, contractually governed, spans multiple teams or repositories, handles sensitive production data, or requires formal audit traceability. In those cases, retain the lightweight plan but add only the specific controls required by that risk or obligation.

## Open Questions and Limitations

- **Open questions:** Where should delivery plans live in this repository; which GitHub plan and Project capabilities are available; who are the two named human roles; what branch, pull-request, and deployment rules apply; and which landing-zone decisions remain unresolved before implementation begins?
- **Unavailable evidence:** No current GitHub Project, issue templates, repository-wide Copilot instructions, CI workflow, branch policy, deployment process, budget, target date, or operating-risk classification was supplied. This research therefore cannot validate a repository-specific execution plan or its commands.
- **Conflicting sources:** No direct conflict was found. The Scrum Guide describes a complete framework and should not be cited to claim that a partial cadence is Scrum. Atlassian offers practitioner guidance on user stories. GitHub and VS Code sources document capabilities, not a universal planning method. The recommendations here are explicitly an inference from these sources and the stated two-person constraint.
- **Validation limitations:** Source pages were reviewed as public web content, not validated against the target GitHub organisation or VS Code/Copilot configuration. Copilot output is probabilistic and remains subject to repository policies, tool availability, and human review. Security, legal, compliance, and production-release requirements need qualified organisational review.

## Sources

- Ken Schwaber and Jeff Sutherland, [The 2020 Scrum Guide](https://scrumguides.org/scrum-guide.html), published 2020-11.
- GitHub Docs, [About issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues), current page reviewed 2026-08-05.
- GitHub Docs, [About Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects), current page reviewed 2026-08-05.
- GitHub Docs, [Adding repository custom instructions for GitHub Copilot](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot), current page reviewed 2026-08-05.
- Visual Studio Code, [Use chat in VS Code](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode), updated 2026-07-29, reviewed 2026-08-05.
- Atlassian, [User stories with examples and a template](https://www.atlassian.com/agile/project-management/user-stories), page reviewed 2026-08-05.
- GOV.UK Service Manual, [How the alpha phase works](https://www.gov.uk/service-manual/agile-delivery/how-the-alpha-phase-works), published 2016-08-04, last updated 2019-05-08.
- Repository context: [Statement of Requirements: Landing Zone](../requirements/azure-landing-zone.md), version 1.0, dated 2026-08-04.
- Repository context: [From Statement of Requirements to a GitHub Project Implementation Plan](./sor-to-github-project-implementation-planning-workflow.md), research date 2026-08-05.
