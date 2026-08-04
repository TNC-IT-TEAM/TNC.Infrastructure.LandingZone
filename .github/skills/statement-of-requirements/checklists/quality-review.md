# SOR Draft Quality Review

Mark each failed or unverified check as a finding. Passing this checklist means ready for stakeholder review, not approved.

## Governance and Evidence

- [ ] The document is explicitly marked Draft and names an approval authority.
- [ ] Decision, audience, scope, time boundary, evidence sources, and source status are recorded.
- [ ] Facts, user-provided inputs, inferences, recommendations, and unknowns are visibly distinct.
- [ ] Assumptions, risks, issues, questions, and decisions are separate from requirements and have owners and review triggers.

## Requirement Quality

- [ ] Every mandatory requirement has a unique stable ID, owner, priority, status, source or rationale, and dependency.
- [ ] Each requirement is atomic, normative, outcome-oriented, and free of vague qualifiers.
- [ ] The SOR contains functional and non-functional user requirements only; no products, platforms, architectures, designs, configurations, technical mechanisms, or delivery methods appear in its requirements, scope, evidence, or supporting registers.
- [ ] Each requirement has a feasible verification method, objective pass criterion where relevant, required evidence, and acceptance authority.
- [ ] The entire document renders as valid, readable Markdown. Check heading hierarchy, lists, tables and their delimiter columns, fenced code blocks, links, and field associations. Do not use a wide requirement table where metadata columns wrap, truncate, or misalign; use per-requirement headings with compact field/value metadata where needed.

## Coverage and Traceability

- [ ] Scope boundaries, stakeholders, capabilities, qualities, security/privacy/compliance, interfaces, dependencies, operations, lifecycle, cost, and acceptance are covered or explicitly not applicable.
- [ ] Each material requirement traces to source, design or rationale, delivery or implementation item, verification evidence, and acceptance status or approved exception.
- [ ] Material changes preserve history and assess impacts on linked requirements, evidence, and approvals.
