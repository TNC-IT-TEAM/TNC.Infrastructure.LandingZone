# Effective Agents and Subagents: Design and Authoring Practices

> Research date: 2026-08-04. This document covers AI coding agents and subagents, with implementation guidance focused on GitHub Copilot in Visual Studio Code. General agent-design evidence is included where it is applicable across platforms.

## Question and Decision

- **Research question:** What makes an AI agent effective, what practices should govern agent authoring, and what additional practices apply to subagents?
- **Audience:** Repository maintainers and engineers who create or configure AI agents for software delivery.
- **Decision this supports:** Whether and how to define repository-scoped custom agents and delegate work to subagents.
- **Scope:** Agent purpose, instructions, context, tools, permissions, validation, observability, orchestration, and subagent delegation. This does not select a model provider, approve a particular agent file, or define organization-wide security policy.
- **Time boundary:** Product documentation and engineering guidance available on 2026-08-04.

## Executive Summary

A good agent has a narrow, observable job; the minimum tools and authority needed to do it; enough relevant context to make sound decisions; explicit completion and escalation conditions; and an independently checkable result. It should be introduced only where a simple prompt, deterministic workflow, or existing automation cannot achieve the required result. Agent quality depends substantially on the quality and usability of its tools, the feedback it obtains from the environment, and its evaluation process.

Subagents are useful when a focused task benefits from isolated context, a specialist role, or independent parallel analysis. They are not a default substitute for a well-scoped main-agent task. In VS Code, a subagent receives the relevant subtask, works independently, and returns a summary; the parent remains accountable for synthesis and final validation. The recommended starting point is a small coordinator plus read-only planning, research, or review workers, granting edit or execution permissions only to the worker that must perform the action.

The main limitation is that vendor documentation describes product capabilities and recommended patterns, not measured results for this repository. Validate any proposed agent with representative tasks, acceptance criteria, review, and the repository's applicable checks before treating it as reliable.

## Findings

### Observed Facts

#### What an effective agent needs

- Anthropic distinguishes a workflow, where code prescribes the path through LLM and tool calls, from an agent, where the LLM dynamically directs its process and tool use. It advises using the simplest solution first because agentic systems trade cost and latency for task performance. [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) (published 2024-12-19).
- The same guidance identifies open-ended problems with unpredictable step counts and a trusted execution environment as appropriate for agents. It says agents should obtain ground truth from tool results or code execution during work, can pause at human checkpoints or blockers, and should have stopping conditions such as a maximum iteration count. [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) (published 2024-12-19).
- VS Code documents agents as appropriate for multi-file changes requiring autonomous planning and tool use, while its Plan mode is for structured planning and its Ask mode is for questions and exploration. [Best Practices for Using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices) (updated 2026-07-29).
- A VS Code custom agent is a Markdown-defined combination of instructions and available tools. The tool list can be tailored by role; the documentation gives a planning agent with read-only tools and an implementation agent with editing capability as examples. [Custom Agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents) (updated 2026-07-29).
- VS Code advises concise project instructions, scoping instructions by path where appropriate, and limiting enabled tools because fewer active tools produce faster, more relevant responses. [Best Practices for Using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices) (updated 2026-07-29).
- VS Code advises prompt authors to state inputs, outputs, constraints, and expected verification; to split complex work into well-scoped steps; and to ask clarifying questions rather than guess when a task is ambiguous. [Best Practices for Using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices) (updated 2026-07-29).
- VS Code recommends review and tests after AI changes, warning that generated code can contain bugs, security issues, and subtle logic errors. It also provides tool-call approvals, permission levels, and sandboxing to control agents that can edit files, execute commands, or call external services. [Best Practices for Using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices) and [Build with Agents in VS Code](https://code.visualstudio.com/docs/agents/overview) (updated 2026-07-29).
- Anthropic recommends transparent planning steps and careful agent-computer interface design. Its tool guidance recommends unambiguous descriptions, examples, edge cases, input formats, clear boundaries between similar tools, and testing actual model use of tools. [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) (published 2024-12-19).
- OpenAI's Agents SDK documentation separates specialist definitions, orchestration and handoffs, guardrails and human review, integrations and observability, and evaluation. It supports different specialists with distinct instructions, tools, or policies, as well as traces across model calls, tools, agents, guardrails, and handoffs. [OpenAI Agents SDK](https://developers.openai.com/api/docs/guides/agents) (accessed 2026-08-04; no publication or update date displayed).

#### What subagents add and require

- VS Code defines a subagent as an independent AI agent that completes focused work, such as research, analysis, or review, and reports results to the main agent. It lists research before implementation, parallel code analysis, exploring alternatives, specialist review, and multi-model consensus as suitable scenarios. [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents) (updated 2026-07-29).
- In the documented VS Code flow, the main agent passes only a relevant subtask; the subagent works autonomously and returns a summary that the main agent incorporates. The documentation recommends clearly defining both the task and expected output to avoid passing unnecessary context back to the parent. [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents) (updated 2026-07-29).
- A VS Code subagent inherits the parent's agent, model, and tools unless a custom agent provides its own values. A custom subagent's settings override those defaults. The `user-invocable` and `disable-model-invocation` properties separately govern direct user selection and model-initiated subagent use. [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents) and [Custom Agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents) (updated 2026-07-29).
- VS Code supports an `agents` allowlist on a coordinator. An explicit list restricts its eligible subagents, `[]` prevents subagent use, and `*` allows all eligible agents. The documentation warns that otherwise similarly named or described agents can be selected unintentionally. [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents) (updated 2026-07-29).
- Nested subagents are disabled by default in VS Code to avoid accidental infinite recursion. When explicitly enabled, their maximum nesting depth is five. [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents) (updated 2026-07-29).
- VS Code's documented coordinator-worker pattern assigns narrowly scoped tools to workers: planning and review agents use read-only access, while an implementer has edit capability. Its multi-perspective review pattern runs independent review lenses in parallel and then synthesizes prioritized findings. [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents) (updated 2026-07-29).

### Inferences

- **Inference:** Agent quality is a system property, not merely a property of its instruction text. A concise role contract, usable tools, appropriate permissions, relevant context, environmental feedback, and verification jointly reduce unbounded behavior and unsupported conclusions. This follows the cited requirements for clear prompts, tool design, ground truth, guardrails, and review.
- **Inference:** A custom agent should own one repeatable decision or execution boundary, such as planning, implementation, security review, or documentation review. Mixing incompatible goals and permission levels in one persona makes its behavior harder to reason about and test.
- **Inference:** A useful completion contract should name deliverables, success criteria, validation commands or evidence, report format, and stop/escalation conditions. This turns a general-purpose response into an auditable work result and gives the parent or reviewer a concrete acceptance boundary.
- **Inference:** A subagent is justified when isolation or specialization improves the result enough to offset extra latency, cost, coordination, and synthesis risk. If a task is short, sequential, shares all required context, or has one clear execution owner, it should normally stay with the main agent.
- **Inference:** Subagents should return decision-ready summaries, not raw transcripts: scope examined, evidence or files consulted, findings, uncertainty, recommended next action, and any validation performed. This preserves the benefit of context isolation while allowing the parent to validate and synthesize.
- **Inference:** The coordinator should be the sole owner of final user communication, cross-task consistency, and acceptance. A delegated result is input to the final decision, not final proof.

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| Single agent with explicit plan, tools, and validation | Lowest coordination overhead; shared context; simplest to observe. | Context can become noisy; one generalist may miss specialist perspectives. | Fits well-scoped work. VS Code recommends planning then implementation and lean context. |
| Coordinator with fixed specialist subagents | Isolated context, least-privilege tools, repeatable delegation, and independent review. | Added model cost, latency, prompt handoff loss, and synthesis responsibility. | VS Code documents coordinator-worker and multi-perspective-review patterns. |
| Nested or recursively delegated subagents | Can decompose unusually large, irregular work. | Compounds cost, weakens observability, and risks recursive delegation. | VS Code disables nesting by default and caps explicitly enabled nesting at five levels. |
| Deterministic workflow or existing automation instead of an agent | Predictable, testable execution for stable tasks. | Less adaptable to unanticipated paths. | Anthropic distinguishes fixed workflows from model-directed agents and recommends starting with the simplest solution. |

## Recommendation

Use this authoring checklist for each proposed repository agent:

1. **Prove agent fit.** State why a prompt, script, CI workflow, or fixed workflow is insufficient. Prefer those alternatives for predictable paths.
2. **Define one role contract.** Name the target users, input, owned decision or action, non-goals, deliverables, acceptance criteria, escalation triggers, and termination conditions.
3. **Provide bounded context.** Reference only the project rules, source locations, examples, and current evidence that the role needs. Keep durable repository conventions in instructions rather than repeatedly embedding them in prompts.
4. **Grant least privilege.** Give planning, research, and review roles read-only tools; grant editing, terminal, network, or write access only where an explicit task needs it. Require approval or human review for consequential actions.
5. **Design tools as interfaces.** Use unambiguous names and parameters, examples where non-obvious, explicit input/output expectations, and error behavior. Remove overlapping or unnecessary tools.
6. **Require environmental feedback.** For code work, require focused tests, type checks, linting, builds, or reproducible inspections appropriate to the change. Distinguish a passing command from validation of the requested behavior.
7. **Make results reviewable.** Require a concise report of changed artifacts or findings, validation run, unresolved assumptions, and any proposed follow-up. Review generated changes before acceptance.
8. **Evaluate before standardizing.** Run representative successful, ambiguous, and failure cases; inspect tool calls and outcomes; then refine the role, context, tools, and checks. Preserve a small evaluation set to detect regressions.

For subagents, start with a coordinator and at most three clear worker types: a read-only explorer or planner, an implementer only when edits are required, and a read-only reviewer. Use a named `agents` allowlist rather than the unrestricted default when predictable delegation matters. Set workers intended only for delegation to `user-invocable: false`; use `disable-model-invocation: true` for agents that must remain directly user-controlled. Keep nested delegation disabled unless a measured divide-and-conquer need requires it.

Each delegation prompt should include: a single bounded question or task, allowed scope and tools, expected output structure, success criteria, deadline or stop condition, and instructions to report uncertainty rather than fabricate an answer. Run independent reviews in parallel only when their scopes do not overlap or when deliberate independent perspectives reduce anchoring. The coordinator must reconcile conflicts, make or seek the final decision, and run final validation.

Reassess this recommendation if agents will access production systems, secrets, regulated data, or irreversible actions. Those cases need an explicit threat model, organizational policy, approval controls, audit requirements, and tested rollback procedures beyond this document's scope.

## Open Questions and Limitations

- **Open questions:** Which repository tasks are sufficiently frequent and error-prone to justify custom agents? Which validation commands, CI workflows, or approval gates should each role run or report? What data classifications and external services may an agent access?
- **Unavailable evidence:** This repository currently contains requirements and research documentation but no custom-agent definitions, test suite, CI workflow, or agent evaluation data. The research cannot establish a role-specific baseline, cost target, or success rate.
- **Conflicting sources:** No material conflict was found. Anthropic's general guidance emphasizes choosing fixed workflows for predictable tasks, while VS Code provides agent and subagent features for complex development work; these are compatible because tool availability does not imply that delegation is the best design for every task.
- **Validation limitations:** Product documentation can establish intended behavior and configuration semantics but not actual model quality, selection reliability, security, or costs in this repository. VS Code subagent features and some agent customization capabilities are documented as experimental or preview, so revalidate metadata behavior against the installed VS Code version.

## Sources

- [Best Practices for Using AI in VS Code](https://code.visualstudio.com/docs/agents/best-practices), updated 2026-07-29.
- [Build with Agents in VS Code](https://code.visualstudio.com/docs/agents/overview), updated 2026-07-29.
- [Custom Agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents), updated 2026-07-29.
- [Subagents in Visual Studio Code](https://code.visualstudio.com/docs/agents/subagents), updated 2026-07-29.
- [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents), published 2024-12-19.
- [OpenAI Agents SDK](https://developers.openai.com/api/docs/guides/agents), accessed 2026-08-04; no publication or update date displayed.