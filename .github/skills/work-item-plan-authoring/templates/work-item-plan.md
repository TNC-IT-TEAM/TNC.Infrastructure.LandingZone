# Plan: <short work-item name>

<!-- This template must be written as a physical file at docs/plans/<lowercase-hyphenated-work-item-name>.md. -->

> Work item: <GitHub issue URL or identifier>
> Source documents: <one or more paths or URLs and exact headings, requirement IDs, decision IDs, or issue anchors>
> Prepared: <YYYY-MM-DD>

## 1. Objective

Deliver <one observable result> for <user, operator, or system>.

## 2. Source Extraction

### Source material

- <source anchor>: <faithful statement, labelled as fact, recommendation, constraint, or unresolved question>

### Constraints

- <source anchor>: <constraint to preserve>

### Unresolved or excluded source material

- <item>: <why it is excluded, a bounded discovery action, or a stop condition>

## 3. Scope Boundary

**Change in this work item**

- <specific component, behavior, configuration, or document change>

**Do not change**

- <explicit non-goal or protected neighboring surface>

## 4. Preconditions

- [ ] Repository is at <branch, commit, or stated baseline>.
- [ ] <required access, tool, environment, or fixture> is available.
- [ ] Read <repository instructions> and <source paths>.
- [ ] Stop and report if <precondition cannot be confirmed>.

## 5. Target Map

| Target | Locate / current state | Required change | Preserve |
| --- | --- | --- | --- |
| `<path>` | `<symbol, heading, resource, or bounded discovery command>` | `<precise change>` | `<behavior, interface, convention, or no-go area>` |

## 6. Ordered Tasks

| Step | Action | Expected output | Verify before continuing | On failure or ambiguity |
| --- | --- | --- | --- | --- |
| 1 | Read `<source>` and inspect `<target>`. Confirm the target map. | <confirmation or mismatch> | <exact observation or command> | Stop; report the path and excerpt. |
| 2 | Edit `<path>`: <precise intended change>. Do not modify `<protected surface>`. | <file or resource state> | <format, lint, or targeted check> | Stop; report the check output. |
| 3 | Run `<exact command>` from `<working directory>`. | Exit code `0` and <expected output>. | <command and expected result> | Stop and return the blocker report. |
| 4 | Record `<evidence>` linked to `<source anchor>` and this work item. | <reviewable evidence> | Confirm the evidence location. | Stop and return the blocker report if evidence cannot be recorded. |

## 7. Completion Check

- [ ] <observable plan criterion linked to the source>.
- [ ] `<exact validation command>` passes with <expected result>.
- [ ] <manual inspection, demonstration, or security check> is recorded at <location>.
- [ ] The review record links this work item, source documents, changed files, commands, results, and limitations.

## 8. Stop Conditions and Escalation

Stop and use the blocker report when:

- A source, target, or current implementation conflicts with this plan.
- Completing a task requires a dependency, credential, endpoint, permission, provider, migration, or design choice that cannot be represented as a bounded discovery action.
- A required validation command is unavailable, fails, or produces an unexpected result.
- The change would alter the stated objective or scope boundary without an updated work-item request.
- A secret, personal data, or production action is required without an explicit authorized procedure.

Blocker report: `step`, `observed fact`, `command/output or path`, `impact`, `decision or input needed`, and `safe next action`.

## 9. File Handoff

- [ ] This plan is saved as a physical Markdown file at `docs/plans/<lowercase-hyphenated-work-item-name>.md`.
- [ ] The exact file path is reported to the orchestrator and reviewer.
- [ ] The saved file was reopened or otherwise inspected after writing, and the required sections are present.
