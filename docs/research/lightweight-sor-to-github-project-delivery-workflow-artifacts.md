# Lightweight Copilot Artifacts for SOR-to-GitHub-Project Delivery Planning

> Research date: 2026-08-05

## Question and Decision

- **Research question:** Given that the repository already has the recommended SOR-authoring artifacts, which additional GitHub Copilot customization artifacts are required to create and sign off lightweight technical documents before separately creating a GitHub Project implementation plan for a two-person team?
- **Audience:** The two delivery-team members who own requirements, technical definition, implementation planning, delivery, and GitHub Project administration.
- **Decision this supports:** Select the smallest maintainable artifact set that preserves requirement-to-delivery traceability without introducing enterprise-scale governance.
- **Scope:** Repository-scoped Copilot skills, agents, prompts, instructions, templates, MCP-server access, and GitHub Project conventions for three distinct stages: approved SOR to signed-off technical baseline; signed-off technical baseline to ready delivery Issues; and approved planning records to verified GitHub Project updates. This does not replace the existing SOR workflow, configure a GitHub organisation, or govern delivery execution.
- **Time boundary:** Repository context and public documentation were reviewed on 2026-08-05. Product capabilities and team needs can change.

## Executive Summary

Add **thirteen repository artifacts, an approved GitHub MCP server configuration, and one GitHub Project template/configuration**:

1. A user-invocable `technical-definition` skill that creates lightweight technical requirements, solution design, ADRs, verification strategy, and a signed-off technical baseline from an approved SOR.
2. A user-facing `technical-orchestrator` custom agent that delegates technical authoring and review to named workers.
3. An editable `technical-author` worker and read-only `technical-reviewer` worker.
4. A user-invocable `delivery-planning` skill that turns only a signed-off technical baseline into a traceability register and issue-ready backlog.
5. A user-facing `delivery-planning-orchestrator` custom agent that delegates planning authoring and review to named workers.
6. An editable `delivery-planning-author` worker and read-only `delivery-planning-reviewer` worker.
7. A targeted `technical-and-planning-documents.instructions.md` file with distinct path rules for technical and planning documents.
8. A user-invocable `github-project-management` skill that applies only reviewed, approved planning changes to GitHub through the approved MCP server and verifies the resulting Project state.
9. A user-facing `github-project-orchestrator` custom agent that delegates GitHub Project changes and read-only verification to named workers.
10. An MCP-enabled `github-project-manager` worker and read-only `github-project-reviewer` worker.
11. A manually configured GitHub Project template with a small field set, three saved views, and issue forms or templates.

Use the approved GitHub MCP server only for the GitHub Project management stage. Do **not** add hooks, GitHub Actions automation, separate prompt files, or plugins at this stage. The new artifacts should mirror the existing `requirements-orchestrator` -> `requirements-author` -> `requirements-reviewer` pattern: an orchestrator coordinates work, independent read-only validation, user decisions through `prompt-me`, and human approval. Reusing the approved SOR and its traceability baseline avoids duplicate governance. AI review improves completeness and consistency, but a named team member remains the technical sign-off and GitHub-change approval authority and cannot delegate that accountability to an agent.

## Findings

### Observed Facts

- The existing repository SOR workflow already provides a user-facing orchestrator, editable author, read-only reviewer, `statement-of-requirements` skill, and `prompt-me` skill. It treats SOR output as Draft until human baseline approval, separates requirements from assumptions and decisions, and requires traceability through design, delivery, evidence, and acceptance. [Existing SOR artifacts](../../.github/agents/requirements-orchestrator.agent.md) [Statement of Requirements skill](../../.github/skills/statement-of-requirements/SKILL.md)
- The existing SOR agents are deliberately constrained to user requirements and explicitly exclude technical solution content. A separate technical-definition capability is therefore needed to produce technical requirements, ADRs, architecture references, and verification strategy from an approved baseline. [Requirements author](../../.github/agents/requirements-author.agent.md)
- The existing SOR-to-project research recommends separate but linked requirement, technical-design, decision, traceability, and GitHub delivery records. It identifies GitHub Issues as the delivery record and Projects as the planning control surface. [From Statement of Requirements to a GitHub Project Implementation Plan](./sor-to-github-project-implementation-planning-workflow.md)
- VS Code positions Agent Skills as reusable, on-demand, task-specific workflows with optional supporting resources, whereas custom instructions are for project rules and custom agents provide a role and constrained tool set. [VS Code, Use Agent Skills, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/agent-skills) [VS Code, Custom agents, updated 2026-07-29](https://code.visualstudio.com/docs/agent-customization/custom-agents) [VS Code, Use custom instructions, page reviewed 2026-08-05](https://code.visualstudio.com/docs/agent-customization/custom-instructions)
- GitHub Projects integrate Issues and pull requests, provide table, board, and roadmap views, allow custom fields, and support built-in workflows and project templates. GitHub does not require a particular planning hierarchy. [GitHub Docs, About Projects, page reviewed 2026-08-05](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)
- GitHub's Projects API supports querying and mutating project settings, items, and field values. Its documentation distinguishes `read:project` access for read-only queries from `project` access for queries and mutations. [GitHub Docs, Using the API to manage Projects, page reviewed 2026-08-05](https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/using-the-api-to-manage-projects)
- The prior research recommends MCP only when a recurring, approved data-access need exists and requires least-privilege read scopes, no credentials in prompts/artifacts, provenance, and stated source freshness. The user has now established that need for GitHub Project updates. [GitHub Copilot Artifacts for High-Quality Statements of Requirements](./copilot-artifacts-for-statement-of-requirements.md)

### Inferences

1. The missing capabilities are technical definition and backlog shaping, not SOR drafting or independent SOR review. They should be distinct skills and agents because their inputs, outputs, and approval conditions differ.
2. Technical documents must become a signed-off baseline before planning begins. This makes each proposed Issue traceable to an agreed design and avoids committing a backlog while material technical choices remain unresolved.
3. The existing orchestrator-author-reviewer pattern should be reused for both stages. Each orchestrator can keep user elicitation, editable generation, read-only validation, and human approval boundaries explicit without adding heavy process.
4. The technical and planning reviewers should be read-only workers, like `requirements-reviewer`. Their independent findings improve quality but do not replace the non-author's human technical sign-off or backlog-readiness decision. The existing `requirements-reviewer` should review an SOR change, not technical documents, because its remit forbids solution information.
5. GitHub Issues should contain the current delivery intent and link back to stable requirement and technical-baseline identifiers. The controlled Markdown planning register remains the compact traceability source; duplicating every field in both places would create drift.
6. The team should start with manual Project use and only three automations: add matching repository Issues, set an initial status, and archive completed items. More automation is not justified until the team observes recurring manual error.
7. An MCP server is now justified specifically for applying and reconciling approved Project changes. The manager needs write access, but review and preflight discovery should use a separate read-only credential and tool allowlist where the server and organisation support that separation.

## Recommended Artifact Set

| Artifact | Status | Purpose and required boundaries |
| --- | --- | --- |
| Existing `statement-of-requirements` and `prompt-me` skills | Reuse unchanged | Produce and clarify the approved business baseline. Do not add technical content to the SOR. |
| Existing requirements orchestrator, author, and reviewer agents | Reuse unchanged | Keep SOR drafting and review separate from technical definition. Invoke them again only when technical discovery requires an approved SOR change. |
| `.github/skills/technical-definition/SKILL.md` | **Create** | User-invocable workflow from approved SOR to technical requirements, architecture/design, ADRs, verification strategy, and technical-baseline sign-off. It creates or updates only Markdown technical documents under `docs/technical/`. |
| `.github/agents/technical-orchestrator.agent.md` | **Create** | User-invocable coordinator with `read`, `search`, and `agent` tools only. It delegates exclusively to `technical-author` and `technical-reviewer`, uses `prompt-me` for essential user decisions, and never edits or signs off documents. |
| `.github/agents/technical-author.agent.md` | **Create** | Non-user-invocable editable worker with `read`, `search`, and `edit` tools. It uses `technical-definition`; it must not edit the SOR, approve its own output, accept risk, or create delivery Issues. |
| `.github/agents/technical-reviewer.agent.md` | **Create** | Non-user-invocable read-only worker with `read` and `search` tools. It independently checks technical-document completeness, traceability, feasibility, risks, verification, and sign-off readiness; it does not edit, approve, or accept risk. |
| `.github/skills/delivery-planning/SKILL.md` | **Create** | User-invocable workflow from a signed-off technical baseline to a traceability register and issue-ready backlog. It creates or updates only Markdown planning documents under `docs/planning/`. |
| `.github/agents/delivery-planning-orchestrator.agent.md` | **Create** | User-invocable coordinator with `read`, `search`, and `agent` tools only. It delegates exclusively to `delivery-planning-author` and `delivery-planning-reviewer`, uses `prompt-me` for essential user decisions, and never edits or creates GitHub Issues. |
| `.github/agents/delivery-planning-author.agent.md` | **Create** | Non-user-invocable editable worker with `read`, `search`, and `edit` tools. It uses `delivery-planning`; it must reject an unsigned technical baseline, must not alter technical documents, and must not claim a GitHub Project was configured without user confirmation. |
| `.github/agents/delivery-planning-reviewer.agent.md` | **Create** | Non-user-invocable read-only worker with `read` and `search` tools. It independently checks the planning baseline gate, traceability, Issue readiness, dependencies, evidence approach, and GitHub Project-field completeness; it does not edit or approve committed work. |
| `.github/instructions/technical-and-planning-documents.instructions.md` | **Create** | Concise local rule file with `applyTo: "docs/{technical,planning}/**/*.md"` or two path-specific instruction files if the glob does not work in the target environment. It defines separate document boundaries, identifiers, sign-off, traceability, and issue-readiness rules. |
| `.github/skills/github-project-management/SKILL.md` | **Create** | User-invocable workflow for inspecting a named Project, presenting a mutation plan, applying only approved changes through the approved GitHub MCP server, and reconciling the live Project with the planning register. |
| `.github/agents/github-project-orchestrator.agent.md` | **Create** | User-invocable coordinator with `read`, `search`, and `agent` tools only. It delegates exclusively to `github-project-manager` and `github-project-reviewer`, uses `prompt-me` for essential user decisions, and does not call MCP mutation tools. |
| `.github/agents/github-project-manager.agent.md` | **Create** | Non-user-invocable MCP-enabled worker. It uses only allowlisted GitHub MCP tools and the approved write credential to create or update approved Project items and fields. It must perform a preflight read, obtain explicit approval for the mutation set, and return changed IDs/URLs plus post-change evidence. |
| `.github/agents/github-project-reviewer.agent.md` | **Create** | Non-user-invocable read-only worker with `read`, `search`, and read-only GitHub MCP tools. It checks the proposed and resulting GitHub Project state against the signed technical baseline and reviewed planning register; it cannot mutate GitHub. |
| Approved GitHub MCP server configuration | **Configure and approve** | Use distinct read-only and write-capable credentials where available. Store credentials in the approved secret mechanism, never in prompts, skill files, agent files, or repository configuration. Record server ownership, allowed repositories/Projects, tool allowlists, and credential-review date. |
| GitHub Project template and Issue forms/templates | **Configure manually, then manage through MCP** | The operational delivery surface. Configure its fields and views once, then use the MCP workflow for approved item and field updates. |
| New prompt, hook, action, or plugin | **Do not create now** | The three orchestrator-author/reviewer sets and the MCP server cover the established needs; no stable deterministic automation need has been established. |

## Required Content of the New Artifacts

### `technical-definition` skill

Use only when an SOR is approved. Require the user to name the SOR path, technical-document destination, accountable technical owner, and intended technical sign-off authority. If an essential fact is missing, use the existing `prompt-me` protocol one question at a time.

The skill should create a concise technical baseline under `docs/technical/`, with:

- Technical requirements linked to SOR requirement IDs, including interfaces, data, security, operational, and quality needs where applicable.
- A proportionate solution design, including boundaries, integrations, data flows, deployment/operating model, and verification approach needed to make technical decisions reviewable.
- Short ADRs for material, hard-to-reverse, cross-cutting, or externally consequential decisions. Record routine implementation choices in the relevant technical design section.
- Technical dependencies, assumptions, risks, mitigations, and unresolved questions.
- A baseline-review record: author, peer reviewer, date, outcome, decision/ADR references, open items, and explicit sign-off. The document remains `Draft` until the named non-author sign-off is recorded.
- A change trigger: when technical definition discovers a new or altered business requirement, stop and route the change to the existing SOR workflow rather than editing the baseline.

Keep the technical baseline proportionate: one technical requirements/design document plus concise ADRs and a verification section is adequate for the stated team size. Split it only when complexity, integration, security, or regulated evidence makes a single document hard to review.

### Technical-definition agent set

`technical-orchestrator` should follow the established SOR workflow pattern:

1. Confirm the approved SOR, technical-document destination, scope, named human sign-off authority, and essential unknowns.
2. Use `prompt-me` to resolve one essential unknown at a time; record unavailable answers as owned technical questions or assumptions.
3. Delegate the Draft technical baseline to `technical-author`, passing only grounded context and the requested destination.
4. Delegate the resulting Draft to `technical-reviewer` for independent, findings-first validation.
5. Use `prompt-me` for material review decisions, then delegate accepted corrections to `technical-author` and request re-review from `technical-reviewer`.
6. Report the Draft status, author changes, reviewer findings, unresolved items, and the named human technical sign-off required. Do not sign off or begin delivery planning.

`technical-author` creates or revises technical documents only. It produces Draft material, preserves traceability to the approved SOR, and must not approve its own work or create planning items. `technical-reviewer` is read-only and returns findings to the orchestrator. Its review checks technical-requirement completeness and consistency; design and ADR rationale; interfaces, data, security, operational and quality concerns where applicable; feasible verification; risks and dependencies; traceability; and document status. Neither worker is the human approval authority.

### Delivery-planning agent set

Use only when the referenced technical baseline has an explicit, recorded human sign-off. `delivery-planning-orchestrator`, `delivery-planning-author`, and `delivery-planning-reviewer` must stop and report the missing gate when the technical document is Draft, lacks a named reviewer, records an unresolved material decision, or lacks sign-off.

The skill creates a planning register under `docs/planning/` containing:

- Technical requirement/design/ADR IDs to Epic, Feature, Story, or Task mappings, retaining the linked SOR ID.
- A capability/Feature list, delivery dependencies, risks, and verification/evidence intent.
- Issue-ready work items: objective, source IDs, parent, acceptance criteria or completion evidence, dependency, test/evidence approach, and owner.
- A change trigger: when planning identifies a technical change, return it to the technical-author workflow; when it identifies a business requirement change, return it to the existing SOR workflow.

`delivery-planning-orchestrator` should follow the same controlled pattern:

1. Confirm the signed-off technical baseline, planning destination, target repository or Project, accountable delivery owner, and essential unknowns.
2. Use `prompt-me` to resolve one essential unknown at a time. Stop when the technical-baseline gate is incomplete.
3. Delegate the Draft planning register and issue-ready backlog to `delivery-planning-author`.
4. Delegate the resulting Draft to `delivery-planning-reviewer` for independent, findings-first validation.
5. Use `prompt-me` for material review decisions, then delegate accepted corrections to the planning author and request re-review from the planning reviewer.
6. Report the proposed GitHub Issues and Project-field values, the review findings, unresolved items, and the named human readiness decision required before committed Issues are created.

`delivery-planning-author` must not edit the signed-off technical baseline. `delivery-planning-reviewer` is read-only and checks baseline sign-off, bidirectional traceability, dependency links, issue readiness, completion evidence, and Project-field completeness. Neither worker approves committed work or claims external GitHub changes were made without tool evidence.

Keep planning shallow: one Epic only when it groups several Features; otherwise use Features and Tasks/Stories directly. The technical baseline already records solution choices, so the planning register should not restate design prose.

### Targeted instruction

The instruction file should be short and contain only repository policy that must apply whenever technical or planning Markdown is edited:

- Technical documents live directly under `docs/technical/`; planning documents live directly under `docs/planning/`; both are Markdown.
- Preserve requirement IDs and use the existing SOR category IDs as source references.
- Use stable technical and planning IDs, for example `TR-###`, `ADR-###`, `FEAT-###`, and `TASK-###`; do not require all categories when they add no value.
- Keep SORs solution-free; put technical material only in technical documents and work decomposition only in planning documents.
- Require technical peer review and recorded sign-off before any planning document or committed GitHub Issue is created.
- Require links from planned work to source IDs, acceptance or completion evidence, and dependencies.
- Require one named peer review before creating committed GitHub Issues for material work; record dissent or open risks instead of manufacturing agreement.
- Escalate material scope changes to the existing SOR workflow and material technical changes to the technical orchestrator workflow.

### GitHub Project management skill and agent set

Use `github-project-management` only after `delivery-planning-orchestrator` reports that the planning register and issue-ready backlog have passed review and received a named human readiness decision. It manages Project state through the approved GitHub MCP server; it does not change SORs, technical documents, or planning documents.

The skill must require a named GitHub owner, repository, Project URL or number, approved planning-document path, and an explicit mutation boundary. Its method is:

1. Read the target Project, its fields, and affected existing Issues through the read-only MCP connection; report unavailable, redacted, or mismatched data.
2. Compare the live state to the reviewed planning register and present a mutation plan listing every new Issue, Project item, field value, dependency, and proposed update. Do not mutate during this step.
3. Ask for explicit user approval of that exact mutation set. A general request such as "update the Project" is insufficient. If the scope changes, create a new plan and request approval again.
4. Delegate the approved changes to `github-project-manager`, which applies only the approved operations using the write-capable MCP connection. It must not delete Projects, Issues, or Project items, change access/visibility, modify secrets, or update settings unless the user explicitly approves that operation in the mutation plan.
5. Delegate reconciliation to `github-project-reviewer` using read-only MCP access. It verifies created or updated Issue URLs/IDs, parent and dependency links, Project inclusion, field values, and traceability identifiers against the approved plan.
6. Report the applied changes, evidence, discrepancies, errors, and any remaining manual action. Do not claim success when the MCP response or read-back cannot confirm it.

`github-project-orchestrator` follows the same repository pattern as the other orchestrators: it has no edit or MCP mutation tools and delegates only to `github-project-manager` and `github-project-reviewer`. It uses `prompt-me` when an essential Project field, target, or approval decision is unknown. The manager's tool list must name only required MCP tools instead of granting the full server wildcard where individual tool selection is supported. The reviewer's credentials and tools must be read-only. Both workers must treat MCP data as current only at the time it is read and include that time in their report.

## GitHub Project Minimum Configuration

Use one Project per delivery initiative. Configure the template and fields with the approved MCP workflow, or manually only for its initial bootstrap if the MCP server cannot create or configure Projects. Thereafter, use the approved MCP workflow for changes:

| Element | Minimum configuration |
| --- | --- |
| Work items | Repository Issues, not draft Issues, once work is committed. Use `Feature`, `Story`, `Task`, `Bug`, and `Spike` as an Issue type, label, or Project single-select field according to the available GitHub plan. Do not require an Epic for small work. |
| Fields | `Status`, `Work type`, `Priority`, `Size`, `Target date` or `Iteration`, `Requirement IDs`, `Technical baseline IDs`, `Acceptance state`, and `Risk`. Omit `Area` and `Target release` until they answer a real planning question; detailed links can remain in the Issue body. |
| Status | `Backlog`, `Ready`, `In progress`, `In review`, `Done`, and `Blocked`. A blocked item must also have a native issue dependency or a linked blocker Issue. |
| Views | `Backlog` table, `Current work` board, and `Roadmap` table or roadmap. Avoid charts and extra views until the team uses them in a decision. |
| Issue template | Objective; SOR and signed technical-baseline IDs; scope; acceptance criteria or completion evidence; dependency; test/evidence approach; parent; estimate; owner. |
| Review cadence | A 30-minute weekly planning review: reorder ready work, inspect blockers, verify closed work has evidence, decide whether any discovery changes the SOR, and approve the next bounded MCP mutation plan. |

The planning Markdown traceability register should contain the GitHub Issue number or URL after creation. The Issue body should cite the SOR ID, signed technical-baseline ID, and relevant ADR ID. This gives both forward and backward navigation without a separate requirements-management system.

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| Use existing SOR artifacts and manually create GitHub Issues | No new customization work. | Technical decisions, technical sign-off, issue readiness, and traceability checks depend on memory; live Project updates remain manual. | Existing agent boundaries establish the technical-definition gap; the user has established an MCP need for GitHub updates. |
| **Recommended: technical-definition, delivery-planning, and GitHub Project management skills, each with an orchestrator-author/reviewer agent set, one scoped instruction, an approved MCP configuration, and a minimal Project template** | Enforces technical sign-off before planning; uses the proven SOR-style orchestration; applies approved GitHub changes repeatably with read-back verification. | Requires the team to maintain nine agents, approve MCP configuration and credentials, and review bounded mutation plans. | Skills, agents, instructions, Projects, and GitHub API permissions support these distinct responsibilities. |
| Direct MCP use by a general-purpose agent | Fastest path to live updates. | Broad permissions and weak separation of planning, approval, execution, and reconciliation; higher risk of unintended changes. | GitHub mutations require write-capable project access; no workflow boundary is inherent in that access. |
| Hooks, GitHub Actions, or broader automation in addition to MCP | Could automate recurring Project changes. | Unnecessary configuration and less visible change control for a two-person team. | No stable deterministic automation need beyond reviewed update requests was supplied. |

## Recommendation

Create the thirteen repository artifacts described above, approve the GitHub MCP server configuration, and configure one minimal GitHub Project template. Reuse the SOR artifacts exactly as they are, then run three separate orchestrated workflows:

1. `technical-orchestrator` uses `prompt-me` where necessary, delegates Draft creation to `technical-author`, delegates validation to `technical-reviewer`, and obtains the named human technical sign-off on the reviewed baseline.
2. Only after that sign-off, `delivery-planning-orchestrator` uses the same pattern with `delivery-planning-author` and `delivery-planning-reviewer` to create, validate, and obtain readiness approval for the planning register and issue-ready backlog.
3. Only after planning readiness approval, `github-project-orchestrator` uses the approved GitHub MCP server through `github-project-manager` to apply an explicitly approved mutation plan, then delegates live-state reconciliation to `github-project-reviewer`.

The delivery-planning orchestrator returns a material technical change to the technical orchestrator and a material requirement change to the requirements orchestrator. The GitHub Project orchestrator returns a required planning change to the delivery-planning orchestrator rather than silently changing planning intent in GitHub. The two team members should alternate author and human reviewer/sign-off roles where practical; for high-impact decisions, both should be named in the ADR, readiness, or mutation-approval record.

Adopt only the minimum records needed to answer: what outcome is required, why this work exists, what blocks it, what proves it is complete, and who checked it. Add an ADR for consequential decisions, a larger technical requirements specification for complex work, or automated validation only when observed complexity makes the lightweight form insufficient.

## Open Questions and Limitations

- **Open questions:** Which GitHub MCP server will be used, who owns it, which exact tools does it expose, and can its read and write tools use separate credentials? Which GitHub plan and organisation settings are available? Are organisation issue types, Project templates, and native issue dependencies enabled? Will the team manage one repository or several? What kinds of data, integrations, security controls, or external commitments would require a fuller technical specification or formal review?
- **Unavailable evidence:** No GitHub MCP server configuration, tool inventory, credential model, existing GitHub Project configuration, Issue form, repository implementation workflow, branch-protection rule, target environment, compliance regime, or access model was supplied.
- **Conflicting sources:** No direct conflict was found. GitHub intentionally does not impose one work-item hierarchy; therefore `Feature`, `Story`, and `Task` remain team conventions, not platform guarantees.
- **Validation limitations:** This research inspected existing repository artifacts and public documentation but did not create the recommended artifacts, configure an MCP server or GitHub Project, or test the workflow with a real approved SOR. Confirm agent discovery, MCP tool allowlists, read/write credential separation, mutation approval, and post-change reconciliation with one small delivery slice before applying it to consequential work.

## Sources

- Repository artifacts: [Requirements orchestrator](../../.github/agents/requirements-orchestrator.agent.md), [Requirements author](../../.github/agents/requirements-author.agent.md), [Requirements reviewer](../../.github/agents/requirements-reviewer.agent.md), [Statement of Requirements skill](../../.github/skills/statement-of-requirements/SKILL.md), and [Prompt Me skill](../../.github/skills/prompt-me/SKILL.md), reviewed 2026-08-05.
- Repository research: [GitHub Copilot Artifacts for High-Quality Statements of Requirements](./copilot-artifacts-for-statement-of-requirements.md), research date 2026-08-03.
- Repository research: [From Statement of Requirements to a GitHub Project Implementation Plan](./sor-to-github-project-implementation-planning-workflow.md), research date 2026-08-05.
- Microsoft, [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-skills), updated 2026-07-29.
- Microsoft, [Custom agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents), updated 2026-07-29.
- Microsoft, [Use custom instructions in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-instructions), page reviewed 2026-08-05.
- GitHub Docs, [About Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects), page reviewed 2026-08-05.
- GitHub Docs, [Using the API to manage Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/using-the-api-to-manage-projects), page reviewed 2026-08-05.