---
name: instruction-authoring
description: "Create, revise, or review GitHub Copilot repository-wide and path-specific instruction files. Use when deciding instruction scope, writing `.github/copilot-instructions.md`, configuring `.github/instructions/*.instructions.md`, or checking instruction quality and loading."
argument-hint: "[requested behavior, target scope, evidence, and validation constraints]"
user-invocable: true
---

# Instruction Authoring

Use this workflow to create or revise concise, evidence-based GitHub Copilot instructions for this repository. Instructions guide Copilot but do not enforce behavior; use automation for mandatory outcomes.

## Artifact Boundary

Choose the smallest artifact that owns the behavior:

- Use `.github/copilot-instructions.md` for a small set of durable rules and facts that apply across the workspace.
- Use `.github/instructions/<name>.instructions.md` for a genuine language, framework, directory, test, or documentation scope difference. Give it a narrow workspace-relative `applyTo` glob.
- Use a prompt for one focused, deliberately invoked task; a skill for a resource-backed multi-step workflow; a custom agent for a role or tool boundary; and a hook, CI check, formatter, or linter for deterministic enforcement.
- This workflow does not create or revise `AGENTS.md`, personal instruction files, prompts, agents, hooks, or MCP configuration.

## Boundaries

- Do not invent repository conventions, commands, owners, policies, approvals, tool support, or validation results.
- Preserve unrelated instructions and user changes. Do not broaden scope merely to simplify placement.
- Keep instructions non-conflicting and non-duplicative. A more specific file is not permission to contradict a broadly applicable file.
- Do not encode a rule as an instruction when it is already reliably enforced by automation; reference the check and report its result instead.
- Treat unsupported product behavior and feature variance as uncertainty. Report checks that could not be performed.

## Procedure

1. Establish the requested behavior, intended users, target files, client(s), evidence, and success check. Ask only essential missing questions.
2. Inspect existing `.github/copilot-instructions.md`, `.github/instructions/`, `AGENTS.md` (for conflict awareness only), relevant repository files, and configured formatters, linters, tests, CI, and hooks.
3. Decide the artifact and scope. Reject a root instruction when the rule is not broadly applicable; reject a path instruction when no real scope difference exists.
4. Draft each candidate rule as an operational contract: affected scope, action or fact, rationale when useful, and observable validation where relevant. Prefer concise, self-contained wording. Add an example only when prose leaves multiple plausible interpretations.
5. Check each rule for durability, evidence, duplication, conflict, context cost, and automation ownership using the [quality checklist](./checklists/instruction-quality-review.md).
6. Create or revise the file using the [instruction templates](./templates/instruction-file.md). Root instructions must remain concise and must be saved exactly at `.github/copilot-instructions.md`. Path-specific instructions must use `.github/instructions/`, end in `.instructions.md`, and include valid frontmatter with an `applyTo` glob.
7. Mechanically validate paths, filename extensions, frontmatter, relative links, and representative files matched by every `applyTo` glob. Confirm that a path glob does not unintentionally load unrelated files.
8. Where available, use VS Code Chat Customization Diagnostics, response References, or Agent Debug Logs to confirm discovery and loading. Exercise a representative task that should use each changed instruction and a nearby task or file that should not use a path-specific instruction.
9. Report changed paths, scope rationale, rules added or rejected, validation performed and results, unavailable checks, and residual uncertainty.

## Stop Conditions

Stop before editing when the requested scope is essential but unknown, the destination is invalid, the proposed rule conflicts with an existing instruction, the rule is temporary or already enforced elsewhere, or required evidence and validation are unavailable. State the smallest missing decision or check.

## Expected Output

A completed task leaves only the necessary instruction file changes, with concise rules supported by repository evidence. The final report must distinguish facts from recommendations and must never claim that Copilot will follow an instruction consistently or that an instruction provides deterministic enforcement.
