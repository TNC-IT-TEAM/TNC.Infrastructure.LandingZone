# Instruction File Templates

Use the smallest applicable form. Replace every `<placeholder>` with verified repository-specific content. Remove optional sections that do not add decision value.

## Repository-Wide

Save exactly as `.github/copilot-instructions.md`. Do not add path-specific frontmatter.

```markdown
# Copilot Instructions

- <Durable repository fact or rule that applies across the workspace>. <Why it matters, when useful>.
- For <repository-wide change type>, run `<verified command>` and report failures, because <observable reason>.

Authoritative references:
- [<local source>](<relative path>)
```

Keep this file short. Omit rules that apply only to a directory, file type, test suite, or temporary task.

## Path-Specific

Save as `.github/instructions/<descriptive-name>.instructions.md`. The `applyTo` value must be a workspace-relative glob that matches the intended files and avoids unrelated files.

```markdown
---
name: <descriptive instruction name>
description: "Rules for <specific path or file type>."
applyTo: "<narrow workspace-relative glob>"
---

# <Scope> Instructions

- For <scoped change>, <required action>. <Why it matters, when useful>.
- Prefer <specific local pattern> because <verified reason>.
- Run `<verified validation>` for changed <scope> and report any module or file that cannot be checked.

Authoritative references:
- [<local source>](<relative path>)
```

Do not use `applyTo: "**"` unless the rule genuinely applies to every file and the broader context cost is justified. Do not include a command, policy, or convention unless repository evidence verifies it.
