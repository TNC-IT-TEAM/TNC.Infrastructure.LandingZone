---
name: prompt-me
description: "Elicit an essential user decision one question at a time using numbered, evidence-grounded options. Use when an unanswered project fact blocks an SOR or other controlled workflow."
user-invocable: false
disable-model-invocation: false
---

# Prompt Me

Use this protocol only when an essential unknown blocks a controlled workflow. It gathers user input; it does not decide facts, draft requirements, or convert uncertainty into approval.

## Required Interaction

1. Ask exactly one substantive question in each message.
2. State in one short sentence which decision or document field the answer affects.
3. Offer a short numbered list of plausible options grounded in supplied evidence.
4. Always make the final option exactly: `N. Other: enter your answer in free text.`
5. Wait for the user's response before asking another question or continuing the workflow.
6. Accept a numeric response only against the immediately preceding option list. Accept free text as user-provided input.
7. Record the response, its source as `User-provided input`, and the affected decision or field.

## Constraints

- Do not bundle questions or use unnumbered choices.
- Do not present an invented obligation, threshold, stakeholder preference, approval, or constraint as an established option.
- Do not infer an answer from silence or ambiguity.
- If the user cannot answer, record an owned open question or assumption, its impact, and a review trigger. Do not continue when the missing answer remains essential.

## Format

```text
[Question]? This determines [decision or SOR field].

1. [Evidence-grounded option]
2. [Evidence-grounded option]
3. Other: enter your answer in free text.
```
