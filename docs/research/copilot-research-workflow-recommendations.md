# Copilot Research Workflow Recommendations

> Research date: 2026-08-03. This recommendation applies to creating repeatable research documents in this repository, including topics beyond the landing-zone implementation.

## Recommendation

Adopt a small, layered set of repository-scoped Copilot artifacts:

1. A `research-authoring` skill as the primary workflow.
2. A read-only `researcher` custom agent for bounded investigations.
3. Two prompt files for the most common research entry points.
4. A narrowly scoped Markdown instruction file only after the team has established durable research-document conventions.

This combination keeps procedural detail out of always-on context, gives large investigations an isolated workspace, and makes common tasks quick to invoke. Do not add MCP servers, hooks, or a repository-wide instruction file for research until a concrete need proves they are necessary.

## Recommended Artifact Set

| Artifact | Location | Purpose | Why it fits research work |
| --- | --- | --- | --- |
| Agent skill | `.github/skills/research-authoring/SKILL.md` | Defines the end-to-end process for researching, writing, validating, and reporting a document. | Research has multiple repeatable stages and benefits from linked templates, source-evaluation guidance, and examples. Skills load progressively, avoiding permanent context cost. |
| Custom agent | `.github/agents/researcher.agent.md` | Performs a bounded, read-only research investigation and returns evidence, uncertainties, and source links. | Context isolation prevents source gathering and intermediate analysis from overwhelming the parent conversation. A read-only tool allow-list keeps the role focused. |
| Prompt file | `.github/prompts/research-topic.prompt.md` | Starts a new investigation from a topic and intended audience. | This is a concise, parameterized request a developer can deliberately invoke. |
| Prompt file | `.github/prompts/review-research-document.prompt.md` | Reviews an existing research document for evidence quality, structure, gaps, and stale claims. | Review is a distinct recurring outcome and should not be buried in a general authoring workflow. |
| Path-specific instruction | `.github/instructions/research-documents.instructions.md` | Applies confirmed conventions to `docs/research/**/*.md`. | Keeps stable document rules close to the files they govern without affecting infrastructure or unrelated documentation work. |

## Primary Workflow: `research-authoring` Skill

Make the skill the centre of the system. It should define a practical workflow rather than impose a generic writing style:

1. Clarify the question, audience, decision the document should support, and time boundary.
2. Inspect relevant repository context before looking outward, so the research addresses the actual project.
3. Gather and compare primary sources first; record publication dates and distinguish facts from recommendations.
4. Identify contradictions, assumptions, unavailable evidence, and areas needing explicit user confirmation.
5. Create the document from a shared template, including scope, findings, recommendations, trade-offs, and sources.
6. Perform a final evidence and link review; report unverified claims rather than presenting them as settled facts.

Place any reusable assets under the skill directory. Useful candidates are a research-document template, a source-quality checklist, and examples of well-structured repository research. The skill description should include trigger terms such as "research document", "technology research", "investigate", "compare options", and "recommendation" so Copilot can select it reliably.

Suggested shape:

```text
.github/
  skills/
    research-authoring/
      SKILL.md
      templates/
        research-document.md
      references/
        source-evaluation.md
```

## Read-Only `researcher` Agent

Use the custom agent when an investigation is substantial enough that source discovery, competing interpretations, and working notes would distract from the parent task. It should return a compact research brief, not edit files.

Give it only the read, search, and web-fetch capabilities available in the team's environment. Its operating procedure should require:

- A restatement of the question and scope.
- Findings tied to authoritative sources, with links and publication dates.
- Separation of direct evidence, inference, and recommendation.
- Conflicts between sources and confidence limitations.
- A proposed document outline or decision matrix when appropriate.

The authoring skill or a coordinator can use this agent as a subagent. Avoid giving the researcher terminal or edit tools: those permissions do not improve research quality and blur the responsibility boundary.

## Prompt Files

Use prompts as lightweight, explicit shortcuts around the skill and agent.

`research-topic.prompt.md` should accept inputs for topic, audience, decision, and optional source constraints. It should instruct Copilot to invoke the research workflow, ask only essential clarification questions, and create a document at the agreed location.

`review-research-document.prompt.md` should accept a document path or selection. It should be read-only and return findings first, ordered by impact: unsupported claims, source-quality problems, stale information, omitted alternatives, then editorial clarity.

Prompts are intentionally narrow. Do not put the full source-evaluation process in them; link to or invoke the skill instead so the process has one owner.

## Add Instructions Only After Conventions Stabilize

Create `research-documents.instructions.md` after at least a few research documents establish rules the team wants to preserve. Set `applyTo: "docs/research/**/*.md"` and include only durable, testable conventions, for example:

- Use the repository's research template and required section order.
- Cite sources as Markdown links and record a research date for time-sensitive claims.
- Separate observed facts, assumptions, and recommendations.
- State validation limitations and unresolved questions.

Do not use `applyTo: "**"`; research-document rules should not consume context during Terraform, code, or operational tasks. Keep source-evaluation procedure in the skill, where it is loaded only when relevant.

## Deliberately Defer These Artifacts

| Artifact | Recommendation | Reason |
| --- | --- | --- |
| Repository-wide `copilot-instructions.md` | Defer. | There are no verified repository-wide research rules yet, and always-on instructions should be minimal. |
| MCP server | Defer unless research depends repeatedly on an approved external system. | Public web and repository sources cover general research. Add an MCP server only for a specific source such as a controlled knowledge base, with scoped credentials and an owner. |
| Hooks | Do not use for research authoring initially. | Hooks are appropriate for deterministic enforcement, not judgment-heavy source assessment or writing quality. |
| Additional specialised agents | Defer. | Separate security, architecture, or editorial agents are useful only once those review modes recur and have different tools or output contracts. |
| Plugin | Defer. | A plugin adds distribution and maintenance overhead before this workflow has proved reusable across repositories. |

## Phased Adoption

1. Create the `research-authoring` skill with a template and source-evaluation reference.
2. Create the read-only `researcher` agent and test it on one substantial topic.
3. Add the two prompts once their invocation wording and output shape are known.
4. After three to five documents, extract stable conventions into the Markdown path instruction.
5. Review usage quarterly: remove unused prompts, update source guidance, and consider an MCP server only where a repeatable external-data need remains unmet.

## Success Criteria

The workflow is successful when a typical research request produces a document with clear scope, traceable evidence, explicit uncertainty, and actionable recommendations without requiring the user to restate the process. It should be possible to inspect a document later and tell which claims are sourced, which are inferences, and what decision the research was intended to inform.

## Sources

- [GitHub Copilot Customization Artifacts](./github-copilot-customization-artifacts.md)
- [VS Code: Customize agent behavior](https://code.visualstudio.com/docs/agent-customization/overview)
- [VS Code: Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills)
- [VS Code: Custom agents](https://code.visualstudio.com/docs/agent-customization/custom-agents)