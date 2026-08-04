# GitHub Copilot Instruction Authoring Best Practices

> Research date: 2026-08-04. This document reflects GitHub Copilot and Visual Studio Code documentation available on that date. Product support and settings can change.

## Question and Decision

- **Research question:** How should a team author GitHub Copilot instructions that reliably improve response quality without creating conflicting or excessive context?
- **Audience:** Maintainers and contributors of this repository who configure GitHub Copilot in Visual Studio Code and GitHub.
- **Decision this supports:** Whether, where, and how to add or revise repository Copilot instruction files.
- **Scope:** Repository-wide and path-specific instruction files, `AGENTS.md`, instruction precedence, authoring quality, and validation. Prompts, skills, agents, hooks, and MCP servers are considered only to establish boundaries.
- **Time boundary:** Product documentation available through 2026-08-04.

## Executive Summary

Use a small repository-wide `.github/copilot-instructions.md` file for enduring, broadly applicable project facts and rules. Put conventions that apply only to a language, framework, directory, test suite, or documentation area in narrowly matched `.github/instructions/*.instructions.md` files. Each rule should be short, self-contained, concrete, and non-obvious; explain its rationale and include a preferred or avoided example only where ambiguity remains.

Instructions are context, not enforcement: Copilot is non-deterministic and may not follow them consistently. Use formatters, linters, tests, CI, and hooks for mandatory outcomes. Validate an instruction both mechanically (discovery, frontmatter, and glob matching) and behaviorally with representative tasks. The most important limitation is feature variance: GitHub and VS Code document overlapping but not identical precedence and support details, so the team should test the target client and workflow.

## Findings

### Observed Facts

- GitHub Copilot custom instructions provide reusable context automatically instead of requiring it in every prompt, but GitHub states that Copilot may not follow them the same way every time because AI is non-deterministic. [GitHub: About customizing GitHub Copilot responses](https://docs.github.com/en/copilot/concepts/prompting/response-customization) (accessed 2026-08-04).
- A repository-wide instruction file is `.github/copilot-instructions.md`; in VS Code it is automatically applied to all chat requests in that workspace. It is intended for project-wide standards, technology choices, architectural patterns, security/error-handling approaches, and documentation standards. [VS Code: Use custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) (updated 2026-07-29).
- Path-specific instructions reside under `.github/instructions/` and use the `.instructions.md` extension. In VS Code, `applyTo` is optional frontmatter containing a workspace-relative glob; without it, the file is not automatically applied, though it can be attached manually. [VS Code: Use custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) (updated 2026-07-29).
- GitHub documents that applicable path-specific and repository-wide instructions are both used. Its stated precedence is personal instructions, then applicable path-specific repository instructions, repository-wide instructions, agent instructions, and organization instructions. It also warns to avoid conflicting sets because all relevant instructions are provided to the model. [GitHub: About customizing GitHub Copilot responses](https://docs.github.com/en/copilot/concepts/prompting/response-customization) (accessed 2026-08-04).
- VS Code documents that it combines multiple instruction files and does not guarantee a specific order. This makes non-conflicting, independently understandable rules necessary even when GitHub's precedence model exists. [VS Code: Use custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) (updated 2026-07-29).
- GitHub recommends short, self-contained, broadly applicable statements because repository instructions are sent with every chat message. It recommends project purpose, relevant structure, conventions, and relevant tools or versions as useful content. [GitHub: About customizing GitHub Copilot responses](https://docs.github.com/en/copilot/concepts/prompting/response-customization) (accessed 2026-08-04).
- VS Code recommends explaining why a rule exists, using concrete preferred and avoided examples, omitting conventions already enforced by linters or formatters, selectively applying topic-specific files, and avoiding duplicated content by referencing instruction files from prompts and custom agents. [VS Code: Use custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) (updated 2026-07-29).
- VS Code supports `AGENTS.md` as always-on guidance and identifies it as useful for teams using multiple AI agents or experimental subfolder-level guidance. GitHub documents agent instructions as a separate repository instruction type and says the nearest `AGENTS.md` in the directory tree takes precedence. [VS Code: Use custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) (updated 2026-07-29); [GitHub: Adding repository custom instructions](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions-in-your-ide/add-repository-instructions-in-your-ide) (accessed 2026-08-04).
- VS Code provides Chat Customization Diagnostics and response References to confirm loaded instruction files. Its troubleshooting guidance specifically calls out incorrect locations, unmatched `applyTo` patterns, and disabled instruction settings. [VS Code: Use custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) (updated 2026-07-29).

### Inferences

- **Inference:** An instruction should be written as an operational contract: scope, action or fact, reason, and observable validation where relevant. This combines GitHub's requirements for concise self-contained context with VS Code's rationale and concrete-example guidance. It is an authoring pattern, not a product guarantee.
- **Inference:** Context budget is a quality concern. A rule that only affects Terraform, research Markdown, or a test directory should not be placed in an always-on repository file because it is irrelevant to many requests and increases the chance of conflict.
- **Inference:** A rule already guaranteed by a formatter, linter, test, CI policy, or access control should be enforced there. Copilot instructions should explain the project context and ask for reporting or validation, rather than being the sole control.

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| One large repository-wide instruction file | Easy to discover and applies uniformly. | Sends irrelevant context to every request; conflicts and stale procedural detail become likely. | GitHub and VS Code describe repository-wide instructions as always-on/broadly applicable context. |
| Small repository-wide file plus path-specific files | Keeps global context focused while applying domain rules where needed. | Requires accurate `applyTo` globs and validation of discovery. | Both products support the locations; VS Code explicitly recommends selective topic files. |
| `AGENTS.md` as the only shared guidance | Can be portable across multiple AI agents. | Support differs by feature and nested behavior is experimental in VS Code; it does not replace path matching where that is needed. | VS Code and GitHub document `AGENTS.md` support with differing operational details. |
| Rely on instructions for compliance | Low initial implementation cost. | Non-deterministic behavior leaves mandatory controls unenforced. | GitHub explicitly warns that instructions are not followed consistently; enforcement recommendation is an inference. |

## Recommendation

Adopt the second option: a concise `.github/copilot-instructions.md` plus path-specific `.instructions.md` files only for demonstrated scope differences. Use root instructions for repository purpose, verified build and validation entry points, material architecture boundaries, and non-obvious team conventions. Use path-specific files for documentation, infrastructure, tests, and languages once each has rules that do not apply globally.

Apply this quality checklist to every candidate rule:

1. **Durable and scoped:** Does it apply to most requests in its intended scope, rather than a temporary task or one contributor's preference?
2. **Specific:** Does it name the required or avoided behavior and the affected files or component?
3. **Self-contained:** Can Copilot act correctly without a vague external reference? Link the authoritative local source when detail is too large to repeat.
4. **Reasoned:** Does it state why the rule exists when that helps resolve an edge case?
5. **Concrete:** Does it include a short preferred/avoided example when prose alone leaves multiple plausible implementations?
6. **Non-duplicative:** Is it absent from another instruction file and not already fully enforced by automation?
7. **Verifiable:** Is there a named check, expected artifact, or explicit report of validation that cannot run?

Preferred rule:

```markdown
- For changed Terraform modules, run `terraform validate` in the module directory and report any module that cannot be validated, because provider and variable errors should be detected before review.
```

Avoided rule:

```markdown
- Be careful with Terraform and follow our standards.
```

The recommendation would change if contributors primarily use a Copilot client that supports only the repository-wide file, or if experimentation shows that a proposed path rule is not consistently loaded in the team's target workflow. In that case, retain a concise shared root file and enforce the affected behavior through repository automation.

## Open Questions and Limitations

- **Open questions:** Which infrastructure, documentation, and validation conventions in this repository have already been verified and are stable enough to encode? Which Copilot clients and GitHub features must the team support?
- **Unavailable evidence:** No controlled evaluation of instruction quality in this repository was available. The product documentation gives authoring guidance, not measured compliance or quality improvements for a particular rule set.
- **Conflicting sources:** GitHub presents a detailed precedence order, while VS Code states that multiple instruction files are combined with no specific order guaranteed. Treat both as true in their documented contexts; avoid relying on ordering between overlapping files.
- **Validation limitations:** This research validates documentation availability and repository context, not the behavior of a future instruction file. Validate any implementation through VS Code diagnostics, response references, representative tasks, and repository automation.

## Sources

- [VS Code: Use custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions), updated 2026-07-29, accessed 2026-08-04.
- [GitHub Docs: About customizing GitHub Copilot responses](https://docs.github.com/en/copilot/concepts/prompting/response-customization), publication or update date not displayed, accessed 2026-08-04.
- [GitHub Docs: Adding repository custom instructions for GitHub Copilot in your IDE](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions-in-your-ide/add-repository-instructions-in-your-ide), publication or update date not displayed, accessed 2026-08-04.
- [GitHub Copilot Customization Artifacts](./github-copilot-customization-artifacts.md), repository research, 2026-08-03. Used as repository context, not as a primary source.