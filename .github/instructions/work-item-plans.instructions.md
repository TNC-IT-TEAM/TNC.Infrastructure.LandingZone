---
name: Work-Item Plan Conventions
description: Stable conventions for reviewable work-item plans under docs/plans.
applyTo: "docs/plans/**/*.md"
---

- Keep one independently reviewable work item per Markdown file directly under `docs/plans/`.
- The plan deliverable is the physical Markdown file at the requested path; chat output is only a report and does not replace the file.
- Use a lowercase, hyphenated filename and retain the required status, work-item, source-documents, prepared-date, and human-approver metadata.
- Link every material plan claim to one or more precise research headings, requirement IDs, decision IDs, or issue anchors. Research recommendations are valid inputs for a Draft plan; they do not authorize implementation.
- State both the change boundary and explicit non-goals. Keep targets, commands, expected results, evidence locations, and stop conditions concrete.
- Do not use a plan to amend a requirement or decision, approve technical design, authorize production action, or record requirement acceptance.
- The agent must not mark a plan Approved or Accepted. A named human records plan approval and final acceptance evidence.
- After creating or revising a plan, reopen or inspect the exact file path and report its existence, readability, and required-section check.
