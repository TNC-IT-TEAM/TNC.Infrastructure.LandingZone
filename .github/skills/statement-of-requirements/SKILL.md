---
name: statement-of-requirements
description: "Create or revise a Statement of Requirements (SOR), requirement register, or traceability register. Use when eliciting, drafting, reviewing, or governing outcome-oriented, testable project requirements."
argument-hint: "[project evidence, decision, and requested document location]"
user-invocable: true
disable-model-invocation: false
---

# Statement of Requirements

Use this workflow to prepare a proportionate, controlled SOR. An SOR is a versioned statement of user requirements: the functional and non-functional outcomes, constraints, and verifiable conditions a solution or supplier must satisfy. It contains no technical solution information. It is not a technical specification, detailed design, contract, legal advice, procurement advice, or an approval record.

## Required Boundaries

- Treat all produced material as `Draft` until a named human authority records baseline approval.
- Establish project facts from supplied evidence. Label direct evidence, user-provided input, inference, recommendation, and unresolved information distinctly.
- Do not invent laws, policies, controls, stakeholder approvals, budget limits, timelines, performance thresholds, technology mandates, or contractual commitments.
- Keep requirements separate from assumptions, risks, issues, questions, options, implementation decisions, and technical solution information.
- Include functional and non-functional user requirements only. Do not include or prescribe technologies, products, platforms, architectures, designs, configurations, technical mechanisms, or delivery methods, even when supplied as an input or constraint. Record such material outside the SOR as an external technical-design dependency or an owned question.
- Write the SOR in clear, plain English. Use short sentences, active voice, and common words. Avoid jargon, buzzwords, corporate or legal language, and unnecessary technical terms. State what is required and why when that helps understanding. Focus on the outcome unless implementation is itself a requirement.
- Escalate project-specific legal, procurement, privacy, safety, security, accessibility, or regulatory interpretation to the responsible qualified authority.
- Create SOR documents and accompanying requirement or traceability registers only as Markdown files directly under `docs/requirements/`. Stop and report an invalid destination rather than writing outside that directory or in another format.

## Procedure

1. Establish or record the decision to support, audience, scope, time boundary, document authority, and available evidence. Use `docs/requirements/<descriptive-name>.md` for every generated SOR artifact.
2. Inspect supplied project evidence before drafting. Build an evidence inventory and identify essential unknowns.
3. Resolve essential unknowns one at a time using the `prompt-me` skill. If an answer is unavailable, record an owned open question or assumption with impact; do not infer an answer.
4. Select a proportionate form using the [SOR template](./templates/sor.md). Use a lightweight form only for a bounded, reversible proof of concept with no consequential data or dependencies.
5. Draft functional and non-functional user requirements with the [requirement register](./templates/requirement-register.md) and [requirement-writing rules](./references/requirement-writing-rules.md). Each mandatory requirement must be atomic, outcome-oriented, solution-free, feasible to verify, and clear on the first reading to business stakeholders, technical teams, and suppliers.
6. Plan verification and acceptance alongside the requirement using [verification methods](./references/verification-methods.md). Record the evidence, pass criterion where applicable, responsible party, and acceptance authority.
7. Capture lifecycle links in the [traceability register](./templates/traceability-register.md), from source through design, delivery, implementation, evidence, and acceptance or approved exception.
8. Use renderer-safe Markdown for requirement metadata. Do not use a wide requirements table when its columns are likely to wrap, truncate, or misalign; instead, use a heading for each requirement with a compact two-column `Field | Value` table or field list.
9. Use the [elicitation checklist](./checklists/elicitation.md) to expose missing scope, governance, operational, security, dependency, cost, and acceptance information.
10. Run the [quality review checklist](./checklists/quality-review.md) before presenting a draft for stakeholder review. Report every failed or unverified check.
11. Present the Draft status, change summary, evidence inventory, review findings, open questions, assumptions, risks, and approval actions. A named human must approve the baseline and material changes.

## Mandatory Requirement Metadata

Every mandatory requirement must include:

- Stable ID and normative statement
- Type, source or rationale, priority, owner, status, and dependency
- Verification method and objective pass criterion where applicable
- Required evidence and acceptance authority

Use `shall` only for mandatory requirements. Do not silently reuse an ID after its intent changes.

## Draft Output

A usable Draft SOR contains a purpose and decision, scope and boundaries, stakeholders and governance, requirement baseline, acceptance approach, uncertainty registers, and traceability. It supports architecture, procurement, delivery, assurance, operations, change control, and human acceptance without representing itself as approval.
