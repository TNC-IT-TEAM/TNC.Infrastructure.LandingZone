# GitHub Copilot Customization Artifacts

> Research date: 2026-08-03. This guide covers the current GitHub Copilot and Visual Studio Code customization model. Some capabilities noted as preview or experimental can change.

## Purpose

GitHub Copilot customizations supply the repository context, repeatable workflows, roles, external tools, and deterministic safeguards that a general-purpose model does not know by default. They are most effective when each artifact has one purpose:

- **Instructions** define durable rules for how work should be done.
- **Prompt files** package a user-invoked, repeatable request.
- **Skills** package a task-specific capability, including its scripts and reference material.
- **Custom agents** define a role, its tool permissions, and its operating procedure.
- **Subagents** isolate focused work delegated by a parent agent.
- **MCP servers** provide controlled access to external tools and data.
- **Hooks** run deterministic commands at defined points in the agent lifecycle.
- **Plugins** distribute a bundle of the artifacts above.

The key design rule is to use the smallest artifact that owns the behaviour. Do not turn a global instruction file into a catalogue of procedures, and do not create an agent merely to reuse a short prompt.

## Selection Matrix

| Need | Use | Invocation | Appropriate content |
| --- | --- | --- | --- |
| Repository-wide conventions and verified build commands | `.github/copilot-instructions.md` | Automatic | Architecture, commands, non-obvious standards, constraints |
| Rules for a language, module, or file type | `*.instructions.md` | Automatic when `applyTo` matches, or manually referenced | Terraform rules, Markdown conventions, test-only rules |
| One repeatable command a developer chooses to run | `*.prompt.md` | `/name` slash command | Generate an ADR, prepare a PR, explain a module |
| A reusable workflow with scripts, templates, or examples | `SKILL.md` directory | Auto-loaded when relevant or `/name` | Validate a landing zone, diagnose a pipeline, generate a module |
| A specialised role with a constrained tool set or model | `*.agent.md` | Selected by user or delegated | Read-only planner, security reviewer, implementation coordinator |
| A bounded, independent investigation or review perspective | Subagent | Parent agent calls `agent/runSubagent` | Research, parallel analysis, focused review |
| Access to an external system | MCP server | Agent calls an exposed tool | Azure inventory, ticket tracker, database, internal service |
| An action that must happen consistently | Hook | Matching lifecycle event | Format after edit, deny unsafe command, emit audit record |
| A shareable, installable workflow suite | Agent plugin | Installed from a source or marketplace | Team/domain bundle of agents, skills, MCP, and prompts |

## Artifact Catalogue

### Instructions

Instructions are Markdown rules supplied as context to Copilot. They should state stable facts and standards rather than temporary task directions.

| Form | Default repository location | Scope and use |
| --- | --- | --- |
| Repository-wide instructions | `.github/copilot-instructions.md` | Always-on rules for the whole workspace |
| Path-specific instructions | `.github/instructions/*.instructions.md` | Rules selected with YAML `applyTo` glob patterns |
| Multi-agent instructions | `AGENTS.md` | Always-on shared guidance; nested files are experimental in VS Code |
| Cross-tool compatibility | `CLAUDE.md`, `.claude/rules/` | Optional compatibility with Claude-oriented tooling |

An `.instructions.md` file can include `name`, `description`, and `applyTo` frontmatter. `applyTo` is relative to the workspace root; without it, the file is not applied automatically in VS Code.

```markdown
---
name: Terraform standards
description: Rules for Azure Terraform modules and environments.
applyTo: "**/*.tf,**/*.tfvars"
---

- Use the repository's approved Azure provider version because environments must remain reproducible.
- Keep environment-specific values in the existing variable pattern; do not hard-code subscription IDs.
- Run the documented validation command before proposing a change.
```

On GitHub.com, a repository-wide file and a matching path-specific file can both apply. `AGENTS.md` is also supported as agent guidance; GitHub documents nearest-file precedence for `AGENTS.md` files in the directory tree. Avoid assuming that separate instruction files have a stable merge order in VS Code: make them non-conflicting.

Instruction sources commonly have this conflict priority: personal instructions, repository instructions, then organization instructions. All applicable instructions are still provided to the model, so priority is not a substitute for avoiding contradictory policies.

### Prompt Files

Prompt files are reusable slash commands. They capture a focused outcome and are intentionally invoked by a developer rather than applied to every request.

- Repository location: `.github/prompts/*.prompt.md`.
- Typical frontmatter: `name`, `description`, `argument-hint`, `agent`, `model`, and `tools`.
- A prompt can reference repository files with Markdown links, use `${selection}` and input variables, and choose a custom agent.
- When both a prompt and agent specify `tools`, the prompt's tool list has priority.

```markdown
---
name: review-infrastructure-change
description: Review an infrastructure change for correctness, safety, and validation gaps.
agent: infrastructure-reviewer
tools: [read, search]
argument-hint: "[pull request, branch, or file set]"
---

Review ${input:target:the change to review}. Return findings ordered by severity,
with evidence, an impact statement, and a precise remediation. Do not edit files.
```

Use a prompt file for a concise task recipe. Promote it to a skill only when it requires a larger procedure, bundled resources, or automatic relevance-based discovery.

### Agent Skills

An Agent Skill is a directory that contains a required `SKILL.md` and optionally scripts, templates, examples, and reference documentation. Skills follow the open Agent Skills standard and are portable across Copilot in VS Code, Copilot CLI, and Copilot cloud agent.

- Repository locations: `.github/skills/`, `.claude/skills/`, or `.agents/skills/`.
- Each skill uses its own directory, for example `.github/skills/terraform-validate/SKILL.md`.
- `name` and `description` frontmatter are required. The lowercase, hyphenated `name` must match the parent directory name and is limited to 64 characters.
- `description` must state both what the skill does and when to use it. It drives relevance matching.
- Optional controls include `argument-hint`, `user-invocable`, `disable-model-invocation`, and experimental `context: fork`.

Copilot loads skills progressively: it first considers the name and description, then loads the `SKILL.md` instructions when relevant, and only then reads resources explicitly linked by the skill. This makes a skill the right home for a large operational procedure without placing every detail in every chat context.

```text
.github/skills/terraform-validate/
  SKILL.md
  scripts/validate.ps1
  examples/valid-module.md
```

```markdown
---
name: terraform-validate
description: Validate Terraform changes in this repository. Use after changes to Terraform modules, variables, providers, or environment definitions.
user-invocable: true
---

# Terraform validation

1. Read the affected module and its closest documentation.
2. Run [the validation script](./scripts/validate.ps1) from the repository root.
3. Report commands run, results, and any checks that could not run.
4. Use [the module example](./examples/valid-module.md) only when evaluating module structure.
```

Use `context: fork` only for a self-contained, potentially large investigation whose intermediate details should not occupy the parent conversation. It runs in a dedicated subagent context and returns its final result to the caller; this is experimental and requires the relevant VS Code setting.

### Custom Agents

A custom agent is a named role with instructions, a tool allow-list, an optional model preference, and optional handoffs to other agents. In VS Code, custom agents are defined in `.agent.md` files. GitHub Copilot cloud agent also consumes repository custom-agent profiles.

- Repository location: `.github/agents/*.agent.md` (VS Code detects Markdown files in this folder).
- User-level location: `~/.copilot/agents/` or the VS Code profile location.
- Common frontmatter: `name`, `description`, `argument-hint`, `tools`, `agents`, `model`, `user-invocable`, `disable-model-invocation`, `handoffs`, `target`, and `mcp-servers`.
- The Markdown body is the role's operating procedure. It can link to instruction files instead of duplicating their content.

```markdown
---
name: infrastructure-reviewer
description: Read-only reviewer for Terraform and Azure landing-zone changes.
tools: [read, search]
user-invocable: true
disable-model-invocation: false
---

Review only. Check changes against nearby patterns, provider constraints,
least-privilege design, destructive-change risks, and documented validation.
Return findings first, ordered by severity. Do not modify files.
```

Use tool allow-lists as a security boundary. A planner or reviewer usually needs `read` and `search`, not terminal or edit access. Keep the agent prompt specific about outputs and stopping conditions; an evocative persona alone does not create dependable behaviour.

### Subagents

Subagents are independent instances that perform a bounded subtask and return a summary to the parent agent. They provide context isolation, allowing the parent conversation to retain only the conclusion rather than every explored file and failed hypothesis.

The default subagent inherits its parent agent's model and tools. A custom agent used as a subagent overrides those settings. The parent must have the `agent` or `agent/runSubagent` tool available. Subagents do not recursively invoke more subagents by default; nested delegation requires an experimental setting and is capped at a depth of five.

Good uses:

- Research a narrowly framed question before implementation.
- Inspect separate modules or competing approaches in parallel.
- Run independent correctness, security, and architecture review passes.
- Delegate a large, self-contained report while the main agent coordinates edits.

Poor uses:

- Tiny tasks that cost more to delegate than to perform.
- Work requiring immediate shared state between agent and parent.
- Unbounded exploration without an expected report format.

Use `user-invocable: false` on a worker agent that should be callable only as a subagent. Use `disable-model-invocation: true` to prevent general delegation. A coordinator can restrict delegation with its `agents` list, which prevents accidental selection of a similarly named agent.

### MCP Servers, Hooks, and Plugins

These are supporting artifacts rather than replacements for instructions, skills, or agents.

- **MCP servers** expose tools that connect Copilot to external services and data. Add only the minimum tools required, use scoped credentials, and treat each server configuration as code requiring review. A custom agent can be configured with agent-specific MCP servers.
- **Hooks** run commands at matching lifecycle events. Use them for deterministic guardrails such as formatting, policy checks, or blocking unsafe commands. Prefer a hook when an action must happen, rather than relying on an instruction that asks the model to remember it.
- **Agent plugins** are distributable bundles of customizations such as skills, agents, prompts, MCP configuration, and hooks. They are useful when a workflow is shared across repositories. Review plugin contents and command execution behaviour before installation.

## Recommended Repository Layout

Start small, then add artifacts only after a concrete recurring need appears.

```text
.github/
  copilot-instructions.md
  instructions/
    terraform.instructions.md
    documentation.instructions.md
  prompts/
    review-infrastructure-change.prompt.md
  agents/
    infrastructure-reviewer.agent.md
    planner.agent.md
  skills/
    terraform-validate/
      SKILL.md
      scripts/
      examples/
docs/
  research/
```

For a monorepo opened below its root, VS Code can discover customizations in parent repositories only when `chat.useCustomizationsInParentRepositories` is enabled and the parent repository is trusted. By default, it is disabled. Keep shared repository artifacts near the repository root; use narrowly targeted instructions for package-specific rules.

## Authoring Practices

### Write Testable, Local Rules

State an action, scope, reason, and verification where possible:

- Prefer: "Run `terraform validate` for every changed Terraform module because provider and variable errors are caught before plan. Report any module that cannot be validated."
- Avoid: "Be careful with Terraform."

Keep instructions concise and self-contained. Include only non-obvious conventions that are not reliably enforced by formatters, linters, type checks, or CI. For each rule, explain *why* it exists; that helps the agent choose correctly at the boundary cases.

Reference the authoritative file rather than duplicating it. An agent, prompt, or skill can link to a shared instruction file, which avoids drift. Make link paths relative and verify them after moves.

### Keep Roles and Workflows Separate

- An **agent** answers "who is working and what may it do?"
- A **skill** answers "how is this capability performed, including resources?"
- A **prompt** answers "what repeatable request does a user want now?"
- An **instruction** answers "what enduring constraints apply?"

For example, a read-only `infrastructure-reviewer` agent can run a `review-infrastructure-change` prompt and load a `terraform-validate` skill when validation evidence is needed. Each artifact remains small and independently maintainable.

### Practice Least Privilege

1. Give read-only analysis agents read and search tools only.
2. Give editing agents only the edit and execution tools their workflow requires.
3. Permit a coordinator to delegate only to named, appropriate worker agents.
4. Never put credentials, access tokens, subscription secrets, or production connection strings in instructions, prompts, skills, or agent files.
5. Review bundled scripts, MCP server configurations, and hooks as executable supply-chain dependencies.
6. Require explicit reporting of destructive operations, skipped validation, and unavailable environments.

Tool lists are especially important for repository-shared agents because they communicate and enforce the intended capability boundary. For sensitive workflows, configure agent-specific MCP tools instead of granting broad tools to every agent.

## Lifecycle and Governance

Treat customization artifacts as production developer tooling.

1. **Discover the repeat.** Capture a customization only after a convention or workflow has recurred and has a stable owner.
2. **Choose the narrowest artifact.** Start with repository instructions. Add path rules for a genuine scope difference; add a prompt for a manually repeated request; add a skill when resources or multiple steps are necessary; add an agent when permissions or role separation matter.
3. **Version with code.** Commit repository-specific artifacts. Put personal preferences in user-level files and do not impose them on a team repository.
4. **Assign an owner.** Every shared artifact should have a responsible team or area and should name its purpose in its filename and description.
5. **Test realistic tasks.** Use representative prompts and inspect whether the intended files are loaded, tools are available, commands work, and the result is useful. Test denial paths for read-only and sensitive agents.
6. **Use diagnostics.** In VS Code, use Chat customizations diagnostics or the Agent Debug Logs to see discovered artifacts and load errors. Inspect response references to confirm instruction use.
7. **Review changes.** Require review for changes that broaden tools, add hooks or MCP servers, change validation commands, or alter organization-wide policy.
8. **Measure and prune.** Periodically remove unused prompts, merge duplicate rules, correct stale command paths, and replace verbose boilerplate with links to authoritative documentation.

VS Code's preview Agent Customizations editor centralizes discovery and editing. The separately published preview Chat Customizations Evaluations extension can identify ambiguous or conflicting `SKILL.md`, `.agent.md`, `.instructions.md`, and `.prompt.md` files. Use it as a quality signal, then confirm outcomes with representative tasks.

## Common Failure Modes

| Symptom | Likely cause | Corrective action |
| --- | --- | --- |
| Copilot ignores a rule | Wrong directory, missing `applyTo`, disabled relevant setting, or a conflicting instruction | Verify discovery with diagnostics and response references; make scopes non-conflicting |
| A skill is never selected | Generic or inaccurate description, invalid name, or unlinked resource | State capability and trigger conditions; ensure directory name equals lowercase hyphenated `name`; link resources from `SKILL.md` |
| A reviewer edits files | Agent has edit tools or an ambiguous role prompt | Remove edit/terminal tools and state read-only output requirements |
| A command is skipped despite an instruction | The behaviour is mandatory but modeled as a suggestion | Enforce it with CI or a hook; retain an instruction only for context and reporting |
| Agent context becomes noisy | Large procedures live in always-on instructions | Move procedural detail and resources to a skill; consider experimental forked context for isolated work |
| A subagent chooses an inappropriate worker | Agent names/descriptions overlap or delegation is unrestricted | Give worker agents distinct responsibilities and constrain the coordinator's `agents` list |
| Cross-repository behaviour differs | Personal, repository, and organization rules conflict | Document intended ownership and resolve conflicts rather than relying on priority |

## Adoption Path for This Repository

For an Azure landing-zone infrastructure repository, an incremental rollout is preferable:

1. Add `.github/copilot-instructions.md` only after verifying the actual IaC toolchain, validation commands, naming rules, environment boundaries, and security constraints.
2. Add `.github/instructions/terraform.instructions.md` when Terraform files exist and their rules should not apply to documentation or auxiliary scripts.
3. Add a `terraform-validate` skill when validation has repeatable multi-step setup, scripts, known failure handling, or module-specific examples.
4. Add a read-only infrastructure-reviewer agent before creating broad autonomous implementation agents; it offers an immediate quality and least-privilege benefit.
5. Add MCP access only when repository content is insufficient and the external system has a clear approval, credential, and audit model.

This order keeps global context small, makes the repository useful to both local and cloud Copilot workflows, and avoids committing speculative artifacts before the infrastructure conventions exist.

## Primary Sources

- [VS Code: Customize agent behavior](https://code.visualstudio.com/docs/agent-customization/overview)
- [VS Code: Agent customization decision matrix](https://code.visualstudio.com/docs/agents/concepts/customization)
- [VS Code: Custom instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions)
- [VS Code: Prompt files](https://code.visualstudio.com/docs/agent-customization/prompt-files)
- [VS Code: Custom agents](https://code.visualstudio.com/docs/agent-customization/custom-agents)
- [VS Code: Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills)
- [VS Code: Subagents](https://code.visualstudio.com/docs/agents/subagents)
- [GitHub Docs: Repository custom instructions](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)
- [GitHub Docs: Custom agents for Copilot cloud agent](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-custom-agents)
- [Agent Skills specification](https://agentskills.io/specification)