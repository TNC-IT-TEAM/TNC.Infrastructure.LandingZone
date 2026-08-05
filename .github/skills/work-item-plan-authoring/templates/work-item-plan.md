# Plan: <short work-item name>

<!-- File: docs/plans/<lowercase-hyphenated-work-item-name>.md -->

> Status: Draft | Approved for implementation | Blocked | Ready for review | Accepted
> Work item: <GitHub issue URL or identifier>
> Source of authority: <path or URL and exact heading, requirement ID, decision ID, or issue anchor>
> Prepared: <YYYY-MM-DD>
> Human approver: <named person or role>

## 1. Objective

Deliver <one observable result> for <user, operator, or system>.

## 2. Source Extraction

### Approved to implement

- <source anchor>: <faithful implementation-relevant statement>

### Constraints

- <source anchor>: <constraint to preserve>

### Unresolved or excluded source material

- <item>: <why it is excluded or which human decision is needed>

## 3. Scope Boundary

**Change in this work item**

- <specific component, behavior, configuration, or document change>

**Do not change**

- <explicit non-goal or protected neighboring surface>

## 4. Preconditions

- [ ] Repository is at <branch, commit, or stated baseline>.
- [ ] <required access, tool, environment, fixture, or decision> is available.
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
| 3 | Run `<exact command>` from `<working directory>`. | Exit code `0` and <expected output>. | <command and expected result> | Mark Blocked; do not claim completion. |
| 4 | Record `<evidence>` linked to `<source anchor>` and this work item. | <reviewable evidence> | Confirm the evidence location. | Request human review. |

Task state: Verified | Ready for review | Blocked. Do not use Complete without one of these states and its evidence.

## 7. Final Acceptance Check

- [ ] <observable criterion linked to the source>.
- [ ] `<exact validation command>` passes with <expected result>.
- [ ] <manual inspection, demonstration, or security check> is recorded at <location>.
- [ ] The review record links this work item, source authority, changed files, commands, results, and limitations.
- [ ] <named human> reviews and records acceptance. The agent must not self-accept.

## 8. Stop Conditions and Escalation

Stop and use the blocker report when:

- A source, target, or current implementation conflicts with this plan.
- Completing a task requires an unapproved dependency, credential, endpoint, permission, provider, migration, or design choice.
- A required validation command is unavailable, fails, or produces an unexpected result.
- The change would alter scope, cost, security posture, production access, an acceptance criterion, or an approved decision.
- A secret, personal data, or production action is required without an explicit authorized procedure.

Blocker report: `step`, `observed fact`, `command/output or path`, `impact`, `decision or input needed`, and `safe next action`.
