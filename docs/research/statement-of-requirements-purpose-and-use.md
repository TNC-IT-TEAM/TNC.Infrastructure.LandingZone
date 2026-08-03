# Statement of Requirements: Purpose, Content, and Use

> Research date: 2026-08-03

## Question and Decision

- **Research question:** What is a Statement of Requirements (SOR), what should it contain, and how should it be used on a project?
- **Audience:** Business sponsors, product, service, or project owners, delivery teams, architects or designers, procurement staff, and acceptance or assurance stakeholders.
- **Decision this supports:** Whether to establish an SOR before defining, sourcing, or implementing a project, and what governance and content it needs to be useful.
- **Scope:** Projects that create, change, buy, or operate a product, service, system, process, facility, or capability, including internal delivery, iterative delivery, and supplier procurement. It distinguishes related artefacts but does not provide legal, contractual, regulatory, or procurement advice for a particular jurisdiction.
- **Time boundary:** Sources were reviewed on 2026-08-03. Standards, regulations, and organisational processes can change after that date.

## Executive Summary

There is no single universal standard definition or mandatory format for a document named a **Statement of Requirements**. ISO/IEC/IEEE 29148:2018 instead defines requirements-engineering processes and required information items, including their content and format guidance; it applies across systems, software, products, and services. [ISO/IEC/IEEE 29148:2018, published 2018-11; confirmed 2024](https://www.iso.org/standard/72089.html) Therefore, this brief uses **SOR** as a practical umbrella term: an approved, versioned statement of the outcomes, constraints, and verifiable conditions that a solution or supplier must satisfy.

An effective SOR is used as the shared basis for scope decisions, architecture, estimates, procurement, delivery planning, acceptance, change control, and operational handover. It should specify **what outcome and performance are required**, the relevant constraints, and how success will be evidenced. It should avoid prematurely prescribing implementation details unless the detail is an actual constraint. This aligns with U.S. federal acquisition policy, which directs agencies to state requirements in terms of functions, performance, or essential physical characteristics, and to avoid prematurely dictating detailed design solutions. [FAR 11.002, current page effective 2026-03-13](https://www.acquisition.gov/far/11.002)

**Recommendation:** Create a concise, controlled SOR before a project is sourced or materially implemented. Baseline stable business, risk, operational, cost, integration, and acceptance requirements; retain discovery items and detailed implementation choices as explicitly managed assumptions, decisions, or backlog items. Maintain traceability from each SOR requirement to design, implementation evidence, and acceptance evidence. Do not treat the SOR as either a detailed design or a static substitute for iterative learning.

The principal limitation is that no specific project context was supplied. A useful project SOR cannot be completed until the relevant problem, stakeholders, constraints, obligations, funding, operating model, success measures, and supplier strategy are elicited and owned.

## Findings

### Observed Facts

#### The term and its role

- ISO/IEC/IEEE 29148:2018 specifies requirements-engineering processes, the information items those processes produce, their required content, and format guidance. It applies regardless of project scope, size, or complexity to systems, software-intensive systems, products, and related services. The standard does not establish a universal required document title of "Statement of Requirements." [ISO/IEC/IEEE 29148:2018, published 2018-11; confirmed 2024](https://www.iso.org/standard/72089.html)
- NASA's Systems Engineering Handbook describes systems engineering as an approach intended to produce quality products and mission success, and includes system-design-process guidance. It is a credible systems-engineering reference, but it is NASA guidance rather than a universal contractual rule. [NASA Systems Engineering Handbook, page updated 2024-03-27](https://www.nasa.gov/reference/systems-engineering-handbook/)
- NIST SP 800-160 Volume 1 Revision 1 describes principles, concepts, activities, and tasks for engineering trustworthy secure systems. Its stated scope includes requirements analysis, security requirements, specifications, stakeholders, verification, and validation. [NIST SP 800-160 Vol. 1 Rev. 1, published 2022-11](https://csrc.nist.gov/pubs/sp/800/160/v1/r1/final)

#### What a requirement statement should express

- In U.S. federal acquisition, agencies must use market research to state needs in a way designed to promote competition and include restrictive conditions only when necessary. To the maximum extent practicable, requirements are stated as functions to perform, required performance, or essential physical characteristics. [FAR 11.002, current page effective 2026-03-13](https://www.acquisition.gov/far/11.002)
- The same policy says agencies should not dictate detailed design solutions prematurely; standards and related documents should initially guide tailoring decisions made through design and development. [FAR 11.002, current page effective 2026-03-13](https://www.acquisition.gov/far/11.002)
- For performance-based service acquisition, a Performance Work Statement (PWS) describes required results rather than how work is performed or hours provided, permits assessment against measurable standards, and seeks innovation and cost effectiveness through measurable standards. [FAR 37.602, current page effective 2026-03-13](https://www.acquisition.gov/far/37.602)
- A U.S. federal Statement of Objectives (SOO) is distinct from a PWS: a supplier may use a SOO to develop a PWS, and the SOO itself does not become part of the contract. FAR specifies minimum SOO content: purpose, scope or mission, period and place of performance, background, required results, and operating constraints. [FAR 37.602, current page effective 2026-03-13](https://www.acquisition.gov/far/37.602)
- Scrum is an adaptive framework. Its Product Backlog is an emergent, ordered list of work needed to improve the product, and refinement continuously adds detail. The Product Goal is the future product state that guides planning. [The 2020 Scrum Guide, published 2020-11](https://scrumguides.org/scrum-guide.html)

#### Verification, acceptance, and quality

- The Scrum Guide defines a Definition of Done as a formal description of the state of an Increment when it meets the product's required quality measures. Work that does not meet it is not part of an Increment. [The 2020 Scrum Guide, published 2020-11](https://scrumguides.org/scrum-guide.html)
- NIST includes requirements analysis, specifications, validation, and verification among the concepts addressed by SP 800-160, supporting the need to address security requirements as part of engineering rather than only after implementation. [NIST SP 800-160 Vol. 1 Rev. 1, published 2022-11](https://csrc.nist.gov/pubs/sp/800/160/v1/r1/final)
- For complex or critical U.S. federal acquisitions, FAR requires agencies to determine whether higher-level contract quality requirements are necessary based on the risk of nonconformance and technical needs, including design, operations, testing, inspection, planning, and documentation control. [FAR 46.202-4, current page effective 2026-03-13](https://www.acquisition.gov/far/46.202-4)

### Inferences

The conclusions below are practical recommendations derived from the observed facts. They assume a cloud-infrastructure project which may be delivered internally or procured from a supplier.

1. **An SOR should be the governing statement of need, not a detailed design.** An SOR earns its place by making the desired result, scope boundary, constraints, and evidence of success explicit. Architecture, implementation components, product selection, delivery methods, and operating procedures normally explain *how* to meet it. A technical choice belongs in the SOR only when law, interoperability, an existing platform decision, security, operations, or another genuine constraint makes it mandatory.
2. **The SOR should be testable at the requirement level.** Every mandatory statement should have an identifier, owner, source or rationale, priority, verification method, and acceptance evidence. This enables a defensible answer to: "Which requirement does this control, design decision, deployment, or test satisfy?"
3. **An SOR should distinguish requirements from unresolved work.** Assumptions, risks, questions, options, and implementation decisions are valuable, but treating them as approved requirements conceals uncertainty. Record them separately with an owner, due date or review trigger, and impact on scope.
4. **The SOR is compatible with iterative delivery.** A stable baseline of outcomes, guardrails, and quality thresholds can coexist with an evolving backlog. Product Backlog items elaborate and sequence work; they should not silently change a contractual, regulatory, security, or business-critical SOR requirement. Such changes need explicit change control.
5. **Procurement needs an outcome-oriented companion, not merely a technical shopping list.** Where a supplier is involved, use the SOR to develop the solicitation's appropriate contractual artefacts with procurement and legal review. The required legal form varies by jurisdiction and contract model: an SOR may become or inform a PWS, SOO, SOW, specification, evaluation criteria, acceptance plan, or all of these. Do not label an internal SOR a contract without that review.

## What an SOR Is and Is Not

| Artefact | Primary purpose | Relationship to the SOR | Important distinction |
| --- | --- | --- | --- |
| Statement of Requirements (working definition) | Baselines required outcomes, constraints, and verifiable success conditions. | The project-level statement of need and acceptance intent. | Not a universally standardised title or contractual form. |
| Business requirements document | Explains the business problem, benefits, stakeholders, and capabilities needed. | A source for SOR business and outcome requirements. | May not contain technical, operational, or acceptance detail. |
| Software or system requirements specification | Specifies system behaviour, qualities, interfaces, and constraints. | May be the SOR itself or a detailed child specification. | Usually more technical and decomposed. |
| Architecture or high-level design | Chooses structure and technical approach. | Responds to requirements and records design decisions. | It explains how, except where the SOR has a legitimate technical constraint. |
| Statement of Work (SOW) | Defines work, deliverables, roles, and commercial obligations. | Can incorporate or reference the SOR when work is procured. | A work and contract document, not necessarily an outcome specification. |
| Statement of Objectives (SOO) | States purpose, results, and constraints for supplier solution development. | A possible procurement-facing expression of high-level SOR outcomes. | Under FAR, it does not become part of the contract. |
| Performance Work Statement (PWS) | States contracted service results and measurable performance standards. | Can be derived from the SOR/SOO. | Under FAR, it is performance-based and more directly linked to contract administration. |
| Product Backlog | Orders and refines work needed to improve a product. | Elaborates and sequences SOR scope for iterative delivery. | It is emergent, so it cannot alone preserve an approved scope or compliance baseline. |
| Test, verification, or acceptance plan | Defines evidence and evaluation methods. | Proves that SOR requirements have been met. | It should be planned alongside requirements, not invented only at handover. |

## Recommended Minimum Content

The following is a recommended content model, not a claim that every project requires every section. Scale it to the decision and risk. For a small, bounded project, a short document with a controlled requirement register is preferable to a large narrative with ambiguous commitments.

| Section | Minimum content | Why it is used |
| --- | --- | --- |
| Purpose and decision | Business problem, intended outcome, decision authority, success measures. | Aligns the work to a result rather than a preferred technology. |
| Scope and boundaries | In-scope capabilities, out-of-scope items, affected environments, users, integrations, and lifecycle stage. | Prevents inferred or unbounded scope. |
| Stakeholders and ownership | Sponsor, product or service owner, technical owner, security/privacy owner, operations owner, finance/procurement owner, and approval authority. | Makes decisions, acceptance, and escalation accountable. |
| Requirement register | Unique ID, normative statement, type, rationale/source, priority, owner, status, and dependency. | Provides a stable, reviewable baseline. |
| Functional and outcome requirements | Capabilities or services the platform must provide. | Drives solution scope and supplier evaluation. |
| Non-functional requirements | Availability, recoverability, performance, capacity, scalability, usability, supportability, observability, maintainability, and cost constraints. | Makes qualities that are often assumed explicit. |
| Security, privacy, and compliance | Data classification, identity/access, audit, encryption, logging, residency, retention, regulatory/control obligations, and evidence requirements. | Ensures controls are designed and assessed rather than retrofitted. |
| Interfaces and dependencies | Existing systems, processes, facilities, data sources, access arrangements, delivery pipelines, service desks, suppliers, APIs, and handoffs. | Reveals constraints, responsibilities, and integration risk. |
| Operating model | Support hours, incident ownership, change control, runbooks, access reviews, patching, backups, cost ownership, and service lifecycle. | Makes the delivered capability operable after deployment. |
| Acceptance and verification | Objective evidence, method, environment, responsible party, pass/fail threshold, and acceptance authority for each requirement. | Allows delivery and payment or go-live decisions to be made on evidence. |
| Assumptions, risks, issues, and decisions | Separate registers with ownership and review triggers. | Preserves uncertainty without turning it into hidden scope. |
| Traceability and change control | Links to design, backlog, implementation, tests, evidence, approvals, version history, and change impact assessment. | Controls evolution and supports auditability. |

### Requirement-writing rules

Use a consistent normative form and make each statement atomic enough to verify. The following rules are recommendations:

- Use **shall** for mandatory requirements; define the document's interpretation of **should** and **may**, or avoid them.
- Name the actor or system, required behaviour or quality, condition, threshold, and measurable unit where appropriate.
- State the desired outcome before a named technology. Example: "The platform shall retain administrative activity records for 180 days in a queryable, access-controlled store" is outcome-oriented; "The platform shall use Product X" is justified only when Product X is an approved constraint.
- Avoid ambiguous qualifiers such as "easy," "fast," "robust," "as appropriate," or "industry standard" unless the SOR defines objective criteria.
- Give every requirement a stable ID, such as `SEC-LOG-001`, and never silently reuse it for a different intent.
- Link each requirement to a verification method: inspection, analysis, demonstration, test, or operational evidence. The method and pass criterion must be feasible before approval.

## How It Is Used Through the Lifecycle

| Lifecycle point | Use of the SOR | Outputs or controls |
| --- | --- | --- |
| Discovery and investment | Establish the problem, outcomes, constraints, alternatives, risks, and minimum evidence for approval. | Approved scope, named owners, assumptions, initial success measures. |
| Architecture and planning | Derive technical requirements, evaluate solution options, estimate cost and effort, and identify dependencies. | Architecture decisions, risk treatment, delivery plan, budget assumptions. |
| Procurement | Describe needed results, constraints, evaluation criteria, acceptance evidence, and supplier responsibilities. | Appropriate solicitation and contract artefacts reviewed by procurement/legal. |
| Backlog and delivery | Decompose approved requirements into stories, tasks, tests, and operational activities; refine lower-level detail. | Traceable backlog, Definition of Done, implementation, code or configuration, and documentation. |
| Assurance and acceptance | Demonstrate conformance requirement by requirement and record exceptions. | Test results, review records, evidence pack, acceptance decision. |
| Operations and change | Maintain the baseline as services, threats, costs, regulations, and dependencies change. | Change requests, updated evidence, periodic reviews, retirement criteria. |

## Decision Matrix: Level of SOR Needed

| Context | Appropriate SOR form | Rationale and safeguards |
| --- | --- | --- |
| Small internal proof of concept with no production data | One-page outcome, scope, constraints, risks, and exit criteria; lightweight requirement list. | Limits documentation overhead while making the experiment bounded and reversible. |
| Internal production system, service, or process | Controlled SOR plus requirement register, design decisions, acceptance plan, and operating-model definition. | The delivered capability has security, cost, availability, quality, or operational consequences. |
| Supplier-delivered platform or managed service | Controlled SOR plus procurement-approved contractual artefacts, measurable service/acceptance criteria, transition and exit requirements. | Shared interpretation, evaluation, and enforceable acceptance matter more when accountability crosses organisations. |
| Regulated, safety-critical, or high-impact system | SOR with formal traceability, independent review, configuration control, rigorous verification/validation, and specialist compliance input. | The potential impact of unverified or changed requirements is materially higher. |

## Generic Application Model

### Suggested SOR requirement groups

For any project, the SOR should establish the business and operating requirements that the solution must satisfy. Tailor these prompts to the project's domain:

1. **Purpose and scope:** What problem, opportunity, users, outcomes, and boundaries define the project? What is expressly out of scope?
2. **Stakeholders and governance:** Who sponsors, funds, owns, delivers, operates, assures, and accepts the result? What decisions, approvals, exceptions, and escalation paths are required?
3. **Capabilities and user needs:** What must the product, service, process, or system enable users or operators to do? Which user journeys, service outcomes, or business rules are mandatory?
4. **Constraints and dependencies:** Which legal, regulatory, technical, physical, commercial, schedule, location, interoperability, or legacy constraints apply? What upstream and downstream dependencies exist?
5. **Security, safety, privacy, and quality:** Which hazards, data, access, confidentiality, integrity, accessibility, quality, environmental, or assurance requirements apply?
6. **Performance and resilience:** What capacity, timeliness, availability, durability, recovery, continuity, support, maintainability, or service-level outcomes are required?
7. **Operations and lifecycle:** Who will operate, support, maintain, measure, improve, transfer, and retire the delivered capability? What training, documentation, incident, change, and asset-management needs exist?
8. **Cost and commercial control:** What budget, whole-life cost, pricing, licensing, procurement, supplier, transition, warranty, and exit requirements apply?
9. **Delivery and acceptance:** What delivery approach, evidence, test environments, documentation, training, acceptance sign-offs, and transition criteria are required? Select methods and tools only after recording the genuine constraints.

### Example requirement register entries

These examples illustrate form only. They are not approved requirements for any project; accountable owners must set the values and verification approach.

| ID | Example requirement | Verification and evidence | Owner |
| --- | --- | --- | --- |
| `CAP-ACCESS-001` | Authorised users shall be able to complete the approved service request using the supported access method within the agreed service window. | Demonstrate the user journey with representative authorised and unauthorised users. | Service owner |
| `SEC-AUDIT-001` | The solution shall retain security-relevant activity records for the approved retention period and make them available to authorised responders within the agreed support window. | Inspect retention and access configuration; demonstrate a representative query or retrieval. | Security owner |
| `FIN-COST-001` | Each delivered unit of service shall be attributable to the approved budget owner or cost-allocation category before operational use. | Inspect the allocation record for representative delivered units. | Finance owner |
| `REL-RECOVERY-001` | Each critical service shall have an approved recovery objective and evidence of a successful recovery exercise at the defined frequency. | Review approved target and recovery-exercise record. | Service owner |

### Traceability model

Maintain a small register or repository-based table mapping each approved requirement through the lifecycle:

```text
SOR requirement ID
  -> design decision or rationale
  -> specification, work item, configuration, or implementation item
  -> change, build, delivery, or deployment record
  -> test, inspection, or operational evidence
  -> acceptance status / approved exception
```

This is a recommendation, not a prescribed tool choice. The register may live in a work-management system, a versioned Markdown/CSV file, or a requirements-management tool. The essential property is that it is current, reviewable, and controlled with the same care as the capability it governs.

## Recommendation

Adopt a **proportionate, versioned SOR** as the entry criterion for a project that creates, changes, buys, or transitions a consequential capability. Use it to agree outcomes and guardrails that are difficult or unsafe to infer: business scope, stakeholder ownership, relevant obligations, operational responsibilities, recovery or continuity targets, costs, dependencies, and acceptance evidence. Translate approved items into design decisions, delivery work, implementation, and tests; keep bidirectional traceability where a requirement is important to safety, security, compliance, acceptance, or recovery.

For a limited internal proof of concept, begin with a lightweight SOR and explicit exit criteria. For a production platform, supplier engagement, sensitive data, or regulatory obligation, expand it into a controlled baseline with formal acceptance and change governance. In either case, retain outcome focus: a requirement should constrain the solution only to the degree necessary to protect the business outcome, interoperability, security, cost, or operability.

This recommendation would change if the work is solely an exploratory, disposable experiment with no production data or consequential dependencies. It must also be adapted by qualified procurement and legal professionals when the SOR will contribute to a contract.

## Open Questions and Limitations

- **Open questions:** What problem and outcomes define the project? Which stakeholders, users, regulations, risks, quality levels, service targets, budgets, constraints, commercial model, and supplier responsibilities apply? Who can approve scope, risk acceptance, and final acceptance?
- **Unavailable evidence:** No project-specific architecture, requirement baseline, compliance register, business case, contract, budget, operating procedures, or test evidence was supplied for this generic research.
- **Conflicting sources:** No material conflict was found. The sources use different artefact names and contexts: ISO/IEC/IEEE 29148 addresses requirements-engineering information items, FAR distinguishes SOO and PWS for U.S. federal acquisition, and Scrum defines an evolving backlog. This brief resolves the terminology difference by using SOR as a local working definition, not as a universal standard term.
- **Validation limitations:** This research reviewed public source pages and did not obtain the full paid ISO standard, inspect any contract, perform market research, interview stakeholders, analyse a specific regulation, or validate a requirement through implementation. ISO states that ISO/IEC/IEEE 29148:2018 is published and confirmed in 2024 but is also marked to be revised; verify the edition required by any applicable contract or policy.

## Sources

- International Organization for Standardization, [ISO/IEC/IEEE 29148:2018 - Systems and software engineering: Requirements engineering](https://www.iso.org/standard/72089.html), published 2018-11, confirmed 2024.
- U.S. General Services Administration, [Federal Acquisition Regulation 11.002 - Policy](https://www.acquisition.gov/far/11.002), page effective 2026-03-13.
- U.S. General Services Administration, [Federal Acquisition Regulation 37.602 - Performance work statement](https://www.acquisition.gov/far/37.602), page effective 2026-03-13.
- U.S. General Services Administration, [Federal Acquisition Regulation 46.202-4 - Higher-level contract quality requirements](https://www.acquisition.gov/far/46.202-4), page effective 2026-03-13.
- National Institute of Standards and Technology, [SP 800-160 Volume 1 Revision 1 - Engineering Trustworthy Secure Systems](https://csrc.nist.gov/pubs/sp/800/160/v1/r1/final), published 2022-11.
- National Aeronautics and Space Administration, [Systems Engineering Handbook](https://www.nasa.gov/reference/systems-engineering-handbook/), page updated 2024-03-27.
- Ken Schwaber and Jeff Sutherland, [The 2020 Scrum Guide](https://scrumguides.org/scrum-guide.html), published 2020-11.