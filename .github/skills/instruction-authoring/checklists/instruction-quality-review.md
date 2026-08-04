# Instruction Quality Review

Review every proposed or changed rule. Mark each check `Pass`, `Fail`, or `Unverified`, and record evidence for failures and unverified checks.

## Placement And Discovery

- [ ] The file is exactly `.github/copilot-instructions.md` or is under `.github/instructions/` with a `.instructions.md` extension.
- [ ] The selected artifact is the smallest one that owns the behavior; a prompt, skill, agent, or automation is not more appropriate.
- [ ] A path-specific file has valid YAML frontmatter and an explicit workspace-relative `applyTo` glob.
- [ ] The `applyTo` glob matches intended representative files and does not match unrelated files.
- [ ] The file can be discovered in the target Copilot client; unavailable diagnostics are reported.

## Rule Quality

- [ ] Each rule is durable and applies to the stated scope.
- [ ] Each rule is specific, self-contained, and actionable rather than vague advice.
- [ ] The rationale or example is included only where it resolves a real ambiguity.
- [ ] Claims, commands, paths, versions, and local references are supported by repository evidence.
- [ ] Rules do not duplicate or contradict applicable instruction files.
- [ ] Content is concise enough for its loading scope, especially the always-on root file.

## Enforcement And Maintenance

- [ ] Mandatory behavior is enforced by an appropriate formatter, linter, test, CI check, hook, or access control when available.
- [ ] Instructions do not claim deterministic compliance or replace human approval and repository enforcement.
- [ ] The rule is not already fully enforced elsewhere without adding useful context or reporting guidance.
- [ ] Relative links resolve, and referenced commands or checks are available or explicitly reported as unavailable.
- [ ] Stale, product-version-specific, or unsupported assumptions are marked for confirmation rather than presented as fact.

## Review Result

- Changed paths: `<paths>`
- Scope decision: `<root or path-specific, with rationale>`
- Failed checks: `<none or list>`
- Unverified checks: `<none or list>`
- Required remediation: `<none or precise next action>`
