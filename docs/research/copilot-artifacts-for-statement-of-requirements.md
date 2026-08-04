# GitHub Copilot Artifacts for High-Quality Statements of Requirements

> Research date: 2026-08-03

## Question and Decision

- **Research question:** Which GitHub Copilot and VS Code customization artifacts should be used to reliably produce high-quality Statements of Requirements (SORs) for this repository and future projects?
- **Audience:** The user who owns the reusable SOR practice; project sponsors and requirement owners; delivery, architecture, security, operations, procurement, and assurance stakeholders who review SORs.
- **Decision this supports:** Select a small, portable, governed set of Copilot artifacts that improve the repeatability, completeness, reviewability, and project fit of SOR authoring without misrepresenting AI output as approved requirements.
- **Scope:** Copilot customization artifacts and an SOR authoring workflow for software, infrastructure, service, process, procurement, and other project types. This assesses the artifact design, not a specific project's substantive requirements, contractual terms, legal obligations, or regulatory controls.
- **Time boundary:** Sources and repository context were reviewed on 2026-08-03. VS Code customization features, especially preview and experimental capabilities, can change.

## Executive Summary

**Recommendation:** Establish two portable, user-level Agent Skills: `statement-of-requirements` for the reusable SOR method and `prompt-me` for resolving essential unknowns with the user. The SOR skill should bundle an SOR template, a requirement-register schema, elicitation question sets, a quality-review checklist, and a short workflow that separates evidence, assumptions, decisions, and approved requirements. The `prompt-me` skill must ask exactly one question per message, offer numbered responses, and always include a final free-text `Other` option. Make a user-facing `requirements-orchestrator` custom agent the primary entry point. It should use `prompt-me` for essential unknowns and delegate only to an editable `requirements-author` subagent that creates and revises the SOR and to a read-only `requirements-reviewer` subagent that performs an independent quality pass. For each project repository, add only a narrowly scoped requirements-document instruction file that supplies its local terminology, policies, owners, source locations, and validation expectations.

This bundle fits the available evidence. VS Code identifies skills as reusable, portable, task-specific workflows that can include resources and load progressively; prompt files are user-invoked reusable tasks; custom agents can restrict tools and give a reviewer a focused role; and instructions are for concise workspace conventions. [VS Code, *Use Agent Skills*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/agent-skills) [VS Code, *Use prompt files*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/prompt-files) [VS Code, *Custom agents*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/custom-agents) [VS Code, *Use custom instructions*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/custom-instructions)

Do **not** begin with a universal always-on SOR instruction, an MCP server, hooks, or plugins. They either create unnecessary context and conflicting rules, expand the security/governance surface, or do not solve the central quality problem: correctly eliciting, attributing, verifying, and approving requirements. The authoring agent should create drafts only and must not claim approval. Add a deterministic linter or a read-only project-data connector only after a stable requirement schema and a genuine recurring validation or data-access need exist.

The material limitation is that an SOR is a controlled stakeholder baseline, not an AI-generated deliverable. ISO/IEC/IEEE 29148 defines requirements-engineering processes and information items across project types, while the repository's prior SOR research recommends a versioned, outcome-oriented, testable baseline with named owners and traceability. AI can structure, challenge, and review this work, but it cannot establish project facts, accept risk, approve scope, or provide legal/procurement authority. [ISO/IEC/IEEE 29148:2018, published 2018-11; confirmed 2024](https://www.iso.org/standard/72089.html) [Statement of Requirements: Purpose, Content, and Use](statement-of-requirements-purpose-and-use.md)

## Findings

### Observed Facts

- ISO/IEC/IEEE 29148:2018 specifies requirements-engineering processes, required information items, their required content, and format guidance. Its stated application covers systems, software-intensive systems, products, and related services regardless of scope, methodology, size, or complexity. It is published and marked "to be revised." [ISO/IEC/IEEE 29148:2018, published 2018-11; confirmed 2024](https://www.iso.org/standard/72089.html)
- The existing SOR research defines an effective SOR as a versioned statement of outcomes, constraints, and verifiable conditions. It recommends a requirement-level ID, owner, source/rationale, priority, verification method, acceptance evidence, and traceability to implementation and acceptance. It also distinguishes approved requirements from assumptions, risks, questions, options, and decisions. [Statement of Requirements: Purpose, Content, and Use](statement-of-requirements-purpose-and-use.md)
- U.S. federal acquisition policy requires agencies, to the maximum extent practicable, to state needs as functions, required performance, or essential physical characteristics. It says agencies should not prematurely dictate detailed design solutions. This is U.S. federal policy, not a universal SOR rule, but it is relevant outcome-oriented guidance. [FAR 11.002, effective 2026-03-13](https://www.acquisition.gov/far/11.002)
- VS Code describes Agent Skills as task-specific folders of instructions and optional scripts, examples, and resources. Skills work across VS Code, Copilot CLI, and Copilot cloud agent; they load progressively from frontmatter discovery, to `SKILL.md`, to explicitly referenced resources. Project skills can live in `.github/skills/`; personal skills can live in `~/.copilot/skills/`. [VS Code, *Use Agent Skills*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/agent-skills)
- A skill must have a lowercase, hyphenated `name` matching its directory and a description that says both what it does and when to use it. Its `user-invocable` and `disable-model-invocation` fields control slash-command and model-triggered access. [VS Code, *Use Agent Skills*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/agent-skills)
- Prompt files are standalone, manually invoked Markdown tasks. They can select an agent, define tools, request inputs, and reference other workspace files. Workspace prompt files live in `.github/prompts/`; VS Code also supports user-level prompt files. A prompt's explicit tool list takes precedence over its selected custom agent's tool list. [VS Code, *Use prompt files*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/prompt-files)
- A custom agent combines a role, instructions, and an allowed tool list. An agent can make named agents available as subagents when it includes the agent tool and an `agents` list. VS Code recommends read-only tools for security-sensitive review workflows. Workspace agents live in `.github/agents/`; user-level agents can be reused across workspaces. [VS Code, *Custom agents*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/custom-agents)
- Custom instructions are automatically included either always-on or conditionally by path/task. VS Code advises starting with one concise repository instruction file, adding targeted instruction files only for distinct scopes, keeping instructions short and self-contained, and avoiding conflicting rules because applicable instruction files are combined. [VS Code, *Use custom instructions*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/custom-instructions)
- GitHub supports `.github/copilot-instructions.md` for repository-wide instructions, `.github/instructions/*.instructions.md` for path-specific instructions, and `AGENTS.md` for agent instructions. Multiple applicable instruction sources can apply, so GitHub advises avoiding conflicts. [GitHub Docs, *Adding repository custom instructions for GitHub Copilot*, accessed 2026-08-03](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)
- VS Code characterizes hooks as deterministic commands for lifecycle guardrails and MCP servers as connections to external tools, databases, and services. It recommends incremental adoption: project instructions, targeted instructions, skills, custom agents, then external tools and hooks. [VS Code, *Customize agent behavior*, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/overview)

### Inferences

The following are recommendations derived from the observed facts and the supplied SOR research.

1. **The workflow should use portable skills, not a global instruction or a prompt alone.** SOR authoring needs a multi-step procedure and reusable resources: elicitation, draft structure, requirement writing, traceability, review, and human approval. It also needs a consistent way to resolve unknowns without overwhelming the accountable user. These are task-specific workflows that match the documented purpose of Agent Skills. Keeping them user-level allows the same method to be used across present and future projects; keeping project facts outside them prevents a generic method from falsely applying local policy.
2. **A reliable SOR practice needs coordinated editable generation and adversarial review.** An authoring agent needs edit capability to create and revise an SOR and its registers, while a separate reviewer needs read-only access to preserve its independent findings. An orchestrator restricted to those two named subagents gives the user one controlled entry point, orders the workflow, and prevents unrelated worker selection.
3. **Project-specific facts belong in a small repository instruction, not the portable skill.** Compliance regimes, named approvers, approved platforms, document locations, terminology, and applicable source systems differ by project. Keeping them in a project artifact maintains portability and gives the team version-controlled local governance.
4. **Human gates are stronger than instruction-only safeguards.** The skill and reviewer should label every item by status and source, then require named human approval for the baseline and exceptions. This is needed because no Copilot customization can determine whether a claimed stakeholder statement, legal obligation, budget, or risk acceptance is true.
5. **MCP, hooks, and plugins are conditional extensions.** A read-only MCP connection may improve grounding when authoritative requirements inputs live in a controlled system; a linter or hook may improve schema conformance after the schema is stable. Neither should be the first quality mechanism, because both increase implementation and governance cost and do not replace elicitation or approval.

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| One universal SOR prompt | Fastest to create and easy to invoke. | Repeats resources and rules; weak review separation; no durable project context. | Prompt files suit reusable invoked tasks, but not a full resource-backed workflow. |
| Always-on global SOR instructions | Makes some rules automatic. | Pollutes unrelated work, can conflict with project instructions, and invites generic rather than project-grounded content. | VS Code distinguishes always-on standards from task-specific skills and warns that multiple instructions combine. |
| **Recommended layered bundle: personal SOR and prompt-me skills + orchestrator + author/reviewer subagents + project instruction** | Separates method, controlled user elicitation, controlled orchestration, editable authoring, independent review, and local facts; portable across projects; least privilege. | Requires initial curation and testing of questions, subagent delegation, and handoffs. | Custom agents can define tools and named subagents; skills hold the reusable workflow/resources. |
| Add MCP and hooks from the start | Could ground drafts in project data and enforce mechanical checks. | Requires credentials, source authority, security review, maintenance, and a stable schema; may create false confidence from stale or incomplete data. | MCP/hook capabilities are documented, but no supplied need or approved source system justifies them yet. |

## Recommended Artifact Set

### 1. Primary artifact: personal `statement-of-requirements` skill

Create this as a personal skill under `~/.copilot/skills/statement-of-requirements/` so it is available in every future workspace. Set `user-invocable: true` and leave model invocation enabled only if its description is precise enough to prevent irrelevant loading. The skill is the reusable process, not the repository's policy.

Recommended contents:

```text
statement-of-requirements/
  SKILL.md
  templates/
    sor.md
    requirement-register.md
    traceability-register.md
  checklists/
    elicitation.md
    quality-review.md
  references/
    requirement-writing-rules.md
    verification-methods.md
```

The skill procedure should require the following:

1. Restate the decision, audience, scope, time boundary, and document authority; ask only for essential missing inputs.
2. Inspect supplied project evidence before drafting. Record each claim's source and distinguish direct evidence from inference.
3. Produce an SOR that separates purpose, scope, stakeholders, requirements, acceptance, assumptions, risks, issues, decisions, dependencies, and traceability.
4. Write only atomic, outcome-oriented, testable functional and non-functional user requirements. Exclude all technical solution information, including products, platforms, architecture, designs, configurations, technical mechanisms, and delivery methods. Each mandatory requirement must have an ID, owner, source/rationale, priority, verification method, measurable pass criterion where applicable, and acceptance authority.
5. Flag missing or unverified facts as open questions. Never invent thresholds, laws, stakeholder approvals, product constraints, cost limits, or contractual commitments.
6. Run the bundled quality checklist and report failures before presenting a draft as ready for stakeholder review.
7. Require a named human baseline approval and change-control record; state that draft status is not approval.

The template should be compatible with the existing [SOR content model](statement-of-requirements-purpose-and-use.md), but should not duplicate changing project rules. Include examples as clearly fictional or parameterized examples.

### 2. Personal `prompt-me` skill

Create a second personal skill under `~/.copilot/skills/prompt-me/`. Set `user-invocable: false` and leave model invocation enabled so the orchestrator can use it automatically when an essential unknown blocks the next workflow step. This skill owns the user-question protocol; it does not create SOR content or decide the answer.

Its `SKILL.md` must enforce these rules:

1. Ask **exactly one** substantive question in each message, then wait for the user's response before asking another question.
2. Explain the decision or SOR field the answer will affect in one short sentence.
3. Offer a short numbered list of plausible answers grounded in the supplied evidence. Do not present an invented fact, obligation, threshold, approval, or stakeholder preference as an established option.
4. Always make the final option a free-text response in this form: `N. Other: enter your answer in free text.`
5. Permit the user to reply with a number or free text. Interpret a number only against the immediately preceding list; record the selected answer and its source as user-provided input.
6. Do not bundle questions, use unnumbered choices, infer an answer from silence, or continue to drafting when the unanswered item is essential. If the user cannot answer, record an open question or assumption with its impact and owner rather than inventing a value.

Example interaction format:

```text
Which approval authority will baseline this SOR? This determines the acceptance record.

1. Project sponsor
2. Product or service owner
3. Designated governance board
4. Other: enter your answer in free text.
```

### 3. Personal `requirements-orchestrator` custom agent

Create one user-level, user-invocable custom agent as the sole workflow entry point. Give it read, search, and agent-delegation capability, but no edit capability: the author subagent owns document changes. Its frontmatter must include the agent tool and restrict `agents` to `requirements-author` and `requirements-reviewer`; do not use `*`.

Its body should run this sequence:

1. Inspect supplied evidence and identify essential missing inputs.
2. Use `prompt-me` to resolve each essential unknown one at a time before delegating work. Record the response as user-provided input or, when unanswered, as an explicitly owned open question or assumption.
3. Delegate the draft or revision to `requirements-author`, passing only grounded project context and the requested destination.
4. Delegate independent assessment of the resulting draft to `requirements-reviewer`.
5. Use `prompt-me` for each essential user decision raised by review findings, then delegate accepted corrections to `requirements-author` and report the resulting draft status, changes, and outstanding items.

The orchestrator must not bypass the reviewer for a material SOR change, make edits itself, invent decisions, or present a draft as approved.

### 4. Personal editable `requirements-author` subagent

Create a user-level custom agent with the workspace read, search, and edit tools required to create and revise the SOR, requirement register, and traceability register. Set `user-invocable: false` so it is used through the orchestrator, and leave model invocation enabled so the named parent can delegate to it. It should use the `statement-of-requirements` skill and create files only in the location requested or established by the project's instruction file.

Its body should require evidence-first drafting, explicit `Draft` status, and a summary of changes and unresolved questions after each edit. It must keep the SOR to functional and non-functional user requirements and exclude all technical solution information. It must not invent project facts, silently convert assumptions into requirements, approve a baseline, accept risk, or provide legal or procurement advice. Give it no terminal, external-system, or MCP tool by default; add such a tool only when a project has an approved need and the minimum access has been reviewed.

### 5. Personal read-only `requirements-reviewer` subagent

Create a user-level custom agent with only read/search capabilities. Set `user-invocable: false` so it is used through the orchestrator, and leave model invocation enabled so the named parent can delegate to it. Its body should require a review-first output and explicitly prohibit editing, approval, legal/procurement advice, and factual invention.

The agent's review checklist should inspect:

- Requirement IDs, duplicate or conflicting requirements, and stated priority/owner.
- Atomicity, normative language, objective condition, threshold/unit, and feasible verification method.
- Functional and non-functional user requirements only, with no technical solution information.
- Scope boundaries, dependencies, interfaces, security/privacy, operations, recovery, cost, lifecycle, and acceptance coverage relevant to the project.
- Traceability to a source, design/work item, evidence, acceptance status, and approved exception where required.
- Clear separation of fact, assumption, decision, risk, issue, question, and recommendation.

Return the findings to the orchestrator, which decides whether to obtain user direction or delegate an accepted correction to `requirements-author`. The reviewer must never be the final acceptance authority.

### 6. Optional personal `/draft-sor` prompt

The three-agent workflow does not require prompt files. Optionally add one user-level `/draft-sor` prompt as a short, deliberate shortcut that selects `requirements-orchestrator` and asks for the project evidence and requested SOR location. Do not create a separate review prompt: review is an obligatory orchestrator stage.

Do not define a prompt-level `tools` list unless necessary, because it overrides the selected agent's tool list. Add a web or controlled data tool only when the user deliberately needs research or evidence retrieval.

### 7. Per-project `requirements-documents.instructions.md`

For a repository that contains SORs, add a narrowly scoped file at `.github/instructions/requirements-documents.instructions.md`, with an `applyTo` pattern matching only the repository's requirements-document location, for example `"docs/requirements/**/*.md"`. Use it for facts the portable skill must not guess:

- Local SOR term and document location.
- Official source systems and source-of-truth precedence.
- Named roles or role definitions for sponsor, owner, security, operations, procurement, assurance, and acceptance.
- Applicable standard, policy, record-retention, privacy, accessibility, security, or procurement constraints.
- Approved requirement-ID taxonomy, status values, templates, validation commands, and baseline/change-control process.
- Rules for references to sensitive material and prohibited content.

Keep it short, non-conflicting, and version-controlled. Do not use `.github/copilot-instructions.md` for the full SOR workflow: it is always-on and is more appropriate for durable repository-wide conventions. This repository can add the targeted instruction once it establishes a concrete location and governance model for project SORs.

### 8. Conditional extensions, not initial artifacts

| Artifact | Adopt only when | Minimum safeguard |
| --- | --- | --- |
| Read-only MCP server | Authoritative project facts, controls, architecture records, backlog items, or test evidence live outside the workspace and a clear owner approves agent access. | Least-privilege read scopes, no credentials in prompts/artifacts, provenance in outputs, source freshness stated. |
| Requirement-schema linter or hook | The requirement register format and validation rules have stabilized across several SORs. | Check only deterministic properties, such as required fields, unique IDs, broken links, status vocabulary, and traceability references; do not claim semantic quality. |
| Repository skill | A repository's SOR procedure has stable local resources and must be shared with its team. | Keep generic method in the personal skill and add only local supplements to `.github/skills/`. |
| Plugin | The artifact bundle has been tested and is needed across multiple teams or repositories. | Review scripts, hooks, MCP configuration, tool grants, versioning, and ownership before distribution. |

## Recommended Workflow and Quality Gates

```text
Evidence and stakeholder inputs
  -> requirements-orchestrator
  -> prompt-me resolves essential unknowns one at a time
  -> requirements-author drafts SOR + requirement / traceability registers
  -> requirements-reviewer returns independent findings
  -> prompt-me obtains required user decisions one at a time
  -> requirements-author applies accepted corrections
  -> named stakeholder baseline approval
  -> controlled change and re-verification
```

Use these gates:

| Gate | Required human decision | Copilot contribution | Record |
| --- | --- | --- | --- |
| Discovery complete | Inputs are sufficient to draft, or explicit discovery work is authorized. | Elicitation questions and evidence inventory. | Sources, gaps, assumptions, questions. |
| Draft ready for review | The document accurately represents supplied inputs. | Structure, consistency, requirement quality checks. | Draft version and review findings. |
| Baseline approval | Accountable authority accepts scope, risk, obligations, and acceptance approach. | Traceability and unresolved-item report. | Approval, exceptions, version. |
| Change approval | Change is necessary and impacts are understood. | Impact analysis against linked requirements and evidence. | Change request and revised baseline. |

The measurable definition of a high-quality draft is not merely fluent prose. At a minimum, every in-scope mandatory requirement should be uniquely identified, sourced, owned, prioritized, testable, and linked to a verification/acceptance approach; all uncertainty should be visible rather than converted into invented commitments. The project owner must tailor this definition for legal, procurement, safety, security, privacy, and operational needs.

## Adoption Plan

1. Create and test the personal `statement-of-requirements` and `prompt-me` skills with the supplied SOR research as the initial method reference. Test that `prompt-me` asks only one question per message, always supplies numbered options and a free-text `Other` option, and waits for a response.
2. Create the user-facing `requirements-orchestrator` agent plus the editable `requirements-author` and read-only `requirements-reviewer` worker subagents. Test both good and intentionally weak SOR samples, including missing owners, vague terms, design prescriptions, and absent acceptance evidence. Verify that the orchestrator delegates only to the two named workers, uses `prompt-me` for essential unknowns, and that workers do not appear as direct user choices.
3. For each new project, create its targeted requirements-document instruction file only after naming the SOR location, source systems, owner roles, and local governance. Do not copy the same project rule into the personal skill.
4. Establish a small evaluation set: a proof of concept, an internal production change, a supplier-facing requirement set, and a sensitive/regulatory scenario. Score completeness, traceability, review findings, stakeholder correction rate, and time to usable draft.
5. Introduce a linter/hook or a read-only MCP connector only when the evaluation shows a recurring, deterministic schema failure or an approved authoritative data source that cannot be adequately supplied as workspace context.

## Recommendation

Adopt the recommended layered bundle: personal **`statement-of-requirements`** and **`prompt-me`** skills, a user-facing **`requirements-orchestrator`** agent, editable **`requirements-author`** and read-only **`requirements-reviewer`** worker subagents, and a **minimal, repository-specific requirements-document instruction** for each project. The author has the edit capability necessary to create and revise the SOR; the reviewer remains read-only for independent assurance; the orchestrator restricts delegation to those two workers; and `prompt-me` resolves essential unknowns one numbered question at a time with a free-text `Other` option. The bundle makes the reusable method portable while locating project facts and approvals where they belong.

For this repository, begin with the two personal skills, orchestrator, editable author, and reviewer using [the existing SOR research](statement-of-requirements-purpose-and-use.md) as the initial method reference. Add no repository-wide Copilot instruction, MCP server, hook, or plugin solely for SOR work at this stage. The recommendation changes when a project has an approved authoritative requirements system, stable schema rules, or a team-wide SOR process that justifies the added governance and maintenance cost of a repository artifact, connector, or deterministic check.

## Open Questions and Limitations

- **Open questions:** Which tools beyond VS Code will the user employ? Where should each project's SOR and registers live? Which source systems are authoritative? Which roles may approve an SOR and changes? Which projects require procurement, legal, privacy, safety, security, accessibility, or regulatory review? Is a common requirement-register schema acceptable across the user's projects?
- **Unavailable evidence:** No project-specific SOR template, requirement-management platform, approval workflow, internal policy, regulatory profile, source-system inventory, or Copilot license/feature configuration was supplied.
- **Conflicting sources:** No material conflict was found. VS Code presents skills as task-specific and portable, while instructions are workspace-scoped guidance; GitHub documents repository instruction precedence and advises avoiding conflict. The exact user-profile storage UI and preview features can vary by VS Code version.
- **Validation limitations:** This research reviewed public documentation and the two supplied research documents. It did not create or execute the recommended artifacts, test their discovery in VS Code, evaluate model outputs against a stakeholder-approved corpus, inspect a contract, or assess an MCP server's security controls. The SOR research is a useful generic method source, but not legal, procurement, or compliance advice.

## Sources

- International Organization for Standardization, [ISO/IEC/IEEE 29148:2018 - Systems and software engineering: Requirements engineering](https://www.iso.org/standard/72089.html), published 2018-11, confirmed 2024; marked to be revised.
- U.S. General Services Administration, [Federal Acquisition Regulation 11.002 - Policy](https://www.acquisition.gov/far/11.002), effective 2026-03-13.
- Microsoft, [Customize agent behavior in Visual Studio Code](https://code.visualstudio.com/docs/agent-customization/overview), updated 2026-07-29.
- Microsoft, [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-skills), updated 2026-07-29.
- Microsoft, [Use prompt files in VS Code](https://code.visualstudio.com/docs/agent-customization/prompt-files), updated 2026-07-29.
- Microsoft, [Custom agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents), updated 2026-07-29.
- Microsoft, [Use custom instructions in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-instructions), updated 2026-07-29.
- GitHub, [Adding repository custom instructions for GitHub Copilot](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions), accessed 2026-08-03.
- Repository research, [GitHub Copilot Customization Artifacts](github-copilot-customization-artifacts.md), research date 2026-08-03.
- Repository research, [Statement of Requirements: Purpose, Content, and Use](statement-of-requirements-purpose-and-use.md), research date 2026-08-03.