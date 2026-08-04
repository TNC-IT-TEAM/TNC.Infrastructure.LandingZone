---
name: research-topic
description: "Start an evidence-based research document for a technology, investigation, option comparison, or recommendation."
argument-hint: "[topic, audience, decision, time boundary, and optional source constraints]"
agent: agent
tools: [read, search, web, edit]
---

Use the [research-authoring skill](../skills/research-authoring/SKILL.md) to investigate and write a research document.

Research topic: ${input:topic:the topic or question to investigate}
Intended audience: ${input:audience:the intended audience}
Decision to support: ${input:decision:the decision this research should inform}
Time boundary: ${input:timeBoundary:the date range or currency requirement}
Optional source constraints: ${input:sourceConstraints:none}
Document filename: ${input:documentFilename:descriptive lowercase filename without the .md extension}

Ask only essential clarification questions before starting. Inspect relevant repository context, gather and compare primary sources, and create exactly one Markdown document at `docs/research/<documentFilename>.md` using the skill's template and evidence requirements. The output path must remain under `docs/research/` and the filename must end in `.md`; do not create another format or save the research document elsewhere. Report the document path, sources consulted, recommendation, uncertainty, and validation performed.