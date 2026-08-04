---
name: review-research-document
description: "Review a research document for unsupported claims, source quality, stale information, omitted alternatives, and editorial clarity."
argument-hint: "[document path or selected research document]"
agent: ask
tools: [read, search, web]
---

Review this research document: ${selection}

If no document is selected, review: ${input:documentPath:path to a document under docs/research/}

Only review Markdown research documents stored under `docs/research/`. If the supplied path is outside that folder or does not end in `.md`, report the invalid location and stop without editing or reviewing it.

Assess the document against the [research-authoring skill](../skills/research-authoring/SKILL.md), its [template](../skills/research-authoring/templates/research-document.md), and the [source evaluation guidance](../skills/research-authoring/references/source-evaluation.md). Check repository context, source authority and dates, traceability of material claims, separation of facts and inferences, alternatives and trade-offs, uncertainty, stale claims, link validity, and editorial clarity.

Return findings first, ordered by impact:

1. Unsupported or misleading claims
2. Source-quality or traceability problems
3. Stale or time-sensitive information
4. Omitted alternatives, trade-offs, or limitations
5. Editorial clarity issues

For each finding, include the affected section, evidence, impact, and precise remediation. Then provide a short summary of strengths, open questions, and remaining validation gaps. Do not edit the document.