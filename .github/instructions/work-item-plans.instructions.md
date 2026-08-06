---
name: Work-Item Plan Conventions
description: Stable conventions for reviewable work-item plans under docs/plans.
applyTo: "docs/plans/**/*.md"
---

- Keep one independently reviewable work item per Markdown file directly under `docs/plans/`.
- The plan deliverable is the physical Markdown file at the requested path; chat output is only a report and does not replace the file.
- Use a lowercase, hyphenated filename and retain the required work-item, source-documents, and prepared-date metadata.
- Link every material plan claim to one or more supplied source anchors. Research, project-plan, requirement, decision, issue, and other documents are optional source types; no governance document is required.
- State both the change boundary and explicit non-goals. Keep targets, commands, expected results, evidence locations, and stop conditions concrete.
- A completed plan authorizes its stated repository-local tasks. Human authorization, low-risk-pilot selection, designation, and a durable-record gate are not prerequisites before execution.
- Do not use a plan to amend a source document or authorize production action.
- Do not add project-governance, authorization, approver, SOR, technical-design, or requirement-acceptance requirements unless they are directly relevant to the supplied work-item sources.
- After creating or revising a plan, reopen or inspect the exact file path and report its existence, readability, and required-section check.
- The plan is finished once its physical Markdown file has been created, reopened, and checked. Do not add a status or lifecycle field.
