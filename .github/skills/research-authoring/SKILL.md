---
name: research-authoring
description: "Research, compare, and write evidence-based research documents. Use when investigating a technology, evaluating options, preparing a recommendation, or creating or revising a research document."
argument-hint: "[topic, audience, decision, and time boundary]"
user-invocable: true
---

# Research Authoring

Use this workflow for substantial research that must support a decision and remain useful after the chat ends.

All research documents created by this workflow must be Markdown files saved directly under `docs/research/`. Use a descriptive `.md` filename and do not create research documents in another folder or format.

## Procedure

1. Clarify the research question, intended audience, decision to support, scope, and time boundary. Ask only for information that is necessary to proceed.
2. Inspect relevant repository files and existing research before looking outward. Record how the repository context affects the question.
3. Gather primary and authoritative sources first. Record source titles, links, publication or update dates, and the specific claims each source supports.
4. Compare sources and identify contradictions, assumptions, unavailable evidence, and confidence limitations. Keep direct evidence, inference, and recommendation distinct.
5. Create or update a Markdown document at `docs/research/<descriptive-name>.md` from the [research document template](./templates/research-document.md). Adapt sections only when the research question requires it.
6. Use the [source evaluation guidance](./references/source-evaluation.md) when ranking sources or resolving conflicting claims.
7. Review every material claim and link before finishing. Mark claims that could not be verified and report unresolved questions and validation limitations.
8. Report the document path, sources consulted, decisions supported, limitations, and any follow-up research needed.

## Output Requirements

- Include a research date for time-sensitive work.
- Save every authored research document under `docs/research/` with a `.md` extension.
- Cite sources as Markdown links close to the claims they support and in a consolidated Sources section.
- Separate observed facts, assumptions, inferences, trade-offs, and recommendations.
- State the confidence or evidence limitation when a conclusion depends on incomplete or conflicting information.
- Do not present an unverified claim as settled fact.