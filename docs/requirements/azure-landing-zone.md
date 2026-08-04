# Statement of Requirements: Landing Zone

> Status: Draft
> Version: 0.1
> Date: 2026-08-04
> Baseline authority: Martyn Fewtrell
> Approval status: Not approved

## Purpose and Decision

This Draft defines the user requirements for a landing zone that can host workloads in separate environments and support their safe operation. It supports a decision by a named human authority on whether the requirements are ready to be baselined.

The intended audience is the future service owner, technical owner, operations owner, and acceptance authority. No people or teams have been identified in the supplied evidence.

This Draft is current only to the supplied research evidence dated 2026-08-04 and the user request dated 2026-08-04.

## Scope and Boundaries

### In Scope

- A landing zone for hosted workloads.
- Separate workload environments.
- Controlled public access and separate administrative access.
- Access control, handling of sensitive access information, activity records, monitoring, operational readiness, and recovery readiness.
- Requirements evidence and human acceptance.

### Out of Scope

- Hosted workload features and business processes.
- Selection or design of products, platforms, locations, networks, deployment methods, or other technical solutions.
- Service targets, data retention periods, data classifications, legal obligations, budgets, and recovery targets. These facts are not supplied.
- Approval of this Draft or any technical design.

## Stakeholders and Governance

| Role | Named person or team | Accountability | Approval or escalation authority |
| --- | --- | --- | --- |
| Sponsor | Unknown | Set the intended business outcome. | Unknown |
| Service owner | Unknown | Own the landing zone outcome and priorities. | Unknown |
| Technical owner | Unknown | Own technical-design decisions outside this SOR. | Unknown |
| Security, privacy, or compliance owner | Unknown | Decide applicable obligations and controls. | Unknown |
| Operations owner | Unknown | Own operational readiness and evidence. | Unknown |
| Acceptance authority | Martyn Fewtrell | Accept or reject requirement evidence. | Martyn Fewtrell |

### Named Human Approval Actions

| Action | Named human required | Status |
| --- | --- | --- |
| Assign a service owner. | TBD | Open |
| Assign the unassigned role owners. | TBD | Open |
| Review this Draft for baseline approval. | Martyn Fewtrell | Not approved |
| Record acceptance or rejection of each requirement. | Martyn Fewtrell | Open |

## Evidence Inventory

| ID | Source | Date | Claim supported | Evidence status |
| --- | --- | --- | --- | --- |
| EVD-001 | Supplied research evidence | 2026-08-04 | The landing zone needs environment separation, controlled access, public and administrative access boundaries, monitoring, governance, and staged recovery planning. | Research recommendation; not a requirement or approval |
| EVD-002 | User request | 2026-08-04 | Create a Draft SOR for the landing zone using functional and non-functional user requirements only. | User-provided input |

## Requirement Baseline

All requirements below have Draft status and Must priority. `TBD` values identify a required named human decision; they do not represent an assigned role or approval.

### FR1: Separate Workload Environments

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall provide separately identified environments for hosted workloads. |
| Type | Functional |
| Source or rationale | EVD-001; supports separation between workload environments. |
| Priority | Must |
| Owner | Service owner: TBD |
| Status | Draft |
| Dependency | QST-001: environment purpose and lifecycle need confirmation. |
| Verification method | Demonstration and inspection |
| Objective pass criterion | Evidence identifies each environment and shows that an authorized user can select the intended environment for a hosted workload. |
| Required evidence | Environment inventory and recorded demonstration result. |
| Acceptance authority | Martyn Fewtrell |

### FR2: Controlled Environment Administration

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall allow authorized administrators to manage each hosted-workload environment. |
| Type | Functional |
| Source or rationale | EVD-001; supports operation of separate environments. |
| Priority | Must |
| Owner | Operations owner: TBD |
| Status | Draft |
| Dependency | QST-002: authorized administrator population needs definition. |
| Verification method | Demonstration and inspection |
| Objective pass criterion | Evidence shows an authorized administrator completing an agreed management action in each environment. |
| Required evidence | Access record, agreed management-action record, and demonstration result. |
| Acceptance authority | Martyn Fewtrell |

### NF1: Environment Isolation

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall keep hosted-workload environments separate so that a change in one environment cannot change another environment without an authorized decision. |
| Type | Non-functional - reliability and maintainability |
| Source or rationale | EVD-001; supports a meaningful production boundary. |
| Priority | Must |
| Owner | Service owner: TBD |
| Status | Draft |
| Dependency | QST-001: environment purpose and lifecycle need confirmation. |
| Verification method | Inspection and test |
| Objective pass criterion | A change made in one environment does not alter the agreed observable state of another environment, unless the evidence includes an authorized decision for that alteration. |
| Required evidence | Change record, test result, and authorization record where applicable. |
| Acceptance authority | Martyn Fewtrell |

### NF2: Recovery Readiness

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall support a documented recovery decision for each hosted workload. |
| Type | Non-functional - resilience |
| Source or rationale | EVD-001; recovery approach depends on unresolved recovery objectives. |
| Priority | Must |
| Owner | Service owner: TBD |
| Status | Draft |
| Dependency | QST-005: recovery objectives and outage impact need agreement. |
| Verification method | Inspection |
| Objective pass criterion | Each hosted workload has a recovery decision record that names the decision owner, the recovery objective status, and the next review trigger. |
| Required evidence | Recovery decision records. |
| Acceptance authority | Martyn Fewtrell |

### SR1: Controlled Privileged Access

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall restrict privileged actions to authorized people. |
| Type | Security |
| Source or rationale | EVD-001; supports least-privilege and auditable changes. |
| Priority | Must |
| Owner | Security owner: TBD |
| Status | Draft |
| Dependency | QST-002: authorized administrator population needs definition. |
| Verification method | Inspection and test |
| Objective pass criterion | Evidence shows that a person not recorded as authorized cannot complete an agreed privileged action, and an authorized person can complete it. |
| Required evidence | Access record, authorization record, and test result. |
| Acceptance authority | Martyn Fewtrell |

### SR2: Sensitive Access Information Protection

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall protect sensitive access information from unauthorized disclosure and use. |
| Type | Security |
| Source or rationale | EVD-001; supports protection of secrets and least privilege. |
| Priority | Must |
| Owner | Security owner: TBD |
| Status | Draft |
| Dependency | QST-003: data classification and applicable obligations need definition. |
| Verification method | Inspection and test |
| Objective pass criterion | Evidence identifies sensitive access information in scope and shows that an unauthorized person cannot view or use a selected sample. |
| Required evidence | Information inventory, authorization record, and test result. |
| Acceptance authority | Martyn Fewtrell |

### DR1: Change Activity Records

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall produce records of privileged changes and access decisions. |
| Type | Data |
| Source or rationale | EVD-001; supports auditable changes. |
| Priority | Must |
| Owner | Operations owner: TBD |
| Status | Draft |
| Dependency | QST-003: record retention and data obligations need definition. |
| Verification method | Inspection |
| Objective pass criterion | A selected privileged change and access decision each have a record that identifies the action, actor, and time. |
| Required evidence | Sample activity records and inspection result. |
| Acceptance authority | Martyn Fewtrell |

### IR1: Access Path Separation

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall distinguish public access to hosted workloads from administrative access. |
| Type | Interface |
| Source or rationale | EVD-001; supports controlled public access and private administration. |
| Priority | Must |
| Owner | Technical owner: TBD |
| Status | Draft |
| Dependency | QST-004: public access and administration use cases need agreement. |
| Verification method | Demonstration and inspection |
| Objective pass criterion | Evidence identifies the public and administrative access paths and shows that each agreed access path has the intended access outcome. |
| Required evidence | Access-path inventory and demonstration result. |
| Acceptance authority | Martyn Fewtrell |

### TR1: Requirement Evidence

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall provide repeatable evidence for every Must requirement before it is presented for acceptance. |
| Type | Testing |
| Source or rationale | EVD-002; every mandatory requirement needs verifiable evidence and human acceptance. |
| Priority | Must |
| Owner | Operations owner: TBD |
| Status | Draft |
| Dependency | QST-006: evidence location and acceptance process need definition. |
| Verification method | Inspection |
| Objective pass criterion | The acceptance pack contains one current evidence item for every Must requirement and identifies its result. |
| Required evidence | Requirement-to-evidence index and acceptance pack. |
| Acceptance authority | Martyn Fewtrell |

### OR1: Operational Visibility

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall enable operators to identify changes, access failures, and loss of hosted-workload health. |
| Type | Operational |
| Source or rationale | EVD-001; supports central diagnostics and actionable alerts. |
| Priority | Must |
| Owner | Operations owner: TBD |
| Status | Draft |
| Dependency | QST-007: operator, notification recipient, and response expectations need definition. |
| Verification method | Demonstration and inspection |
| Objective pass criterion | Evidence shows that agreed simulated examples of a change, an access failure, and loss of health are visible to the designated operator. |
| Required evidence | Demonstration results and operator-view records. |
| Acceptance authority | Martyn Fewtrell |

### OR2: Operational Response Guidance

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall provide operators with current response guidance for access compromise, service loss, and recovery decisions. |
| Type | Operational |
| Source or rationale | EVD-001; supports operational readiness and recovery planning. |
| Priority | Must |
| Owner | Operations owner: TBD |
| Status | Draft |
| Dependency | QST-005 and QST-007 |
| Verification method | Inspection and demonstration |
| Objective pass criterion | Guidance exists for each stated event, identifies an owner and escalation route, and is used successfully in an agreed exercise. |
| Required evidence | Current guidance, exercise record, and review record. |
| Acceptance authority | Martyn Fewtrell |

## Acceptance Approach

The assigned acceptance authority shall review each requirement's required evidence, record pass or fail against its pass criterion, and record a decision. This activity is required before any baseline approval. This Draft does not authorize delivery or record acceptance.

An unmet requirement remains Draft until a named human authority records either acceptance after corrective evidence or an approved exception. No approved exception exists in this Draft.

## External Technical-Design Dependencies

These matters are not requirements. They must be resolved by the assigned technical owner outside this SOR and linked to the relevant requirement evidence.

| ID | External technical-design dependency | Related requirements | Owner | Status |
| --- | --- | --- | --- |
| TDD-001 | Select the technical approach for environment separation, controlled access, public access, administrative access, monitoring, and activity records. | FR1, FR2, NF1, SR1, DR1, IR1, OR1 | Technical owner: TBD | Open |
| TDD-002 | Select the technical approach for handling sensitive access information. | SR2 | Technical owner: TBD | Open |
| TDD-003 | Select the technical approach for recovery readiness and response guidance. | NF2, OR2 | Technical owner: TBD | Open |
| TDD-004 | Define the method for gathering and retaining requirement evidence. | TR1 | Technical owner: TBD | Open |

## Assumptions

| ID | Statement | Owner | Impact if false | Review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| ASM-001 | The landing zone will host workloads that need separate environments. | Service owner: TBD | FR1 and NF1 may need revision. | Scope confirmation | Open |
| ASM-002 | The landing zone will have both public and administrative access needs. | Service owner: TBD | IR1 may not apply or may need revision. | Access-use-case confirmation | Open |

## Risks

| ID | Risk | Owner | Impact | Treatment or review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| RSK-001 | Unassigned owners may delay decisions, evidence review, and acceptance. | Sponsor: TBD | Requirements cannot be baselined or accepted. | Assign named owners before baseline review. | Open |
| RSK-002 | Unknown recovery objectives may lead to a recovery approach that does not meet stakeholder needs. | Service owner: TBD | NF2 and OR2 cannot be fully assessed. | Agree recovery objectives and outage impact. | Open |
| RSK-003 | Unknown data obligations may make activity records or sensitive-information handling incomplete. | Security, privacy, or compliance owner: TBD | SR2 and DR1 may need revision. | Identify applicable obligations and data classification. | Open |

## Issues

| ID | Statement | Owner | Review trigger | Status |
| --- | --- | --- | --- | --- |
| ISS-001 | No named people or teams were supplied for sponsor, service, technical, security, privacy, compliance, or operations roles. | Sponsor: TBD | Before baseline review | Open |

## Open Questions

| ID | Question | Owner | Review trigger | Status |
| --- | --- | --- | --- | --- |
| QST-001 | What environments are required, and what are their purposes and lifecycles? | Service owner: TBD | Before baseline review | Open |
| QST-002 | Who may perform privileged administration in each environment? | Service owner: TBD | Before access acceptance | Open |
| QST-003 | What data classifications, retention needs, and obligations apply? | Security, privacy, or compliance owner: TBD | Before security and data acceptance | Open |
| QST-004 | Which public and administrative access use cases are required? | Service owner: TBD | Before interface acceptance | Open |
| QST-005 | What recovery objectives and outage impact are acceptable for each hosted workload? | Service owner: TBD | Before resilience acceptance | Open |
| QST-006 | Where will evidence be stored, and what is the acceptance process? | Acceptance authority: Martyn Fewtrell | Before acceptance activity | Open |
| QST-007 | Who receives operational information, and what response expectations apply? | Operations owner: TBD | Before operational acceptance | Open |

## Decisions

| ID | Decision | Owner | Status |
| --- | --- | --- | --- |
| DEC-001 | Keep technical-solution choices outside the requirement baseline. | User request | Draft working decision |
| DEC-002 | Do not claim regional resilience until recovery objectives and evidence are agreed. | Service owner: TBD | Pending |
| DEC-003 | Keep this SOR as Draft pending resolution of the listed open questions and objective verification criteria. No baseline approval is granted. | Martyn Fewtrell | Draft; not approved |

## Traceability Register

> Status: Draft. Design, delivery, and acceptance records are not yet available.

| SOR ID | Source or rationale | External technical-design dependency or rationale | Delivery record | Verification evidence | Acceptance status | Last reviewed |
| --- | --- | --- | --- | --- | --- | --- |
| FR1 | EVD-001 | TDD-001 | Not available | Environment inventory and demonstration result | Draft; not accepted | 2026-08-04 |
| FR2 | EVD-001 | TDD-001 | Not available | Access record and demonstration result | Draft; not accepted | 2026-08-04 |
| NF1 | EVD-001 | TDD-001 | Not available | Change record and test result | Draft; not accepted | 2026-08-04 |
| NF2 | EVD-001 | TDD-003 | Not available | Recovery decision records | Draft; not accepted | 2026-08-04 |
| SR1 | EVD-001 | TDD-001 | Not available | Access record and test result | Draft; not accepted | 2026-08-04 |
| SR2 | EVD-001 | TDD-002 | Not available | Information inventory and test result | Draft; not accepted | 2026-08-04 |
| DR1 | EVD-001 | TDD-001 | Not available | Sample activity records | Draft; not accepted | 2026-08-04 |
| IR1 | EVD-001 | TDD-001 | Not available | Access-path inventory and demonstration result | Draft; not accepted | 2026-08-04 |
| TR1 | EVD-002 | TDD-004 | Not available | Requirement-to-evidence index | Draft; not accepted | 2026-08-04 |
| OR1 | EVD-001 | TDD-001 | Not available | Demonstration results and operator-view records | Draft; not accepted | 2026-08-04 |
| OR2 | EVD-001 | TDD-003 | Not available | Guidance and exercise record | Draft; not accepted | 2026-08-04 |

## Quality Review

| Check | Result | Finding |
| --- | --- | --- |
| Draft status and approval authority are explicit. | Pass | Martyn Fewtrell is the named baseline and acceptance authority. |
| Decision, audience, scope, time boundary, evidence sources, and evidence status are recorded. | Pass | Audience members are unknown. |
| Facts, recommendations, and unknowns are distinct. | Pass | Research recommendations are held as external technical-design dependencies. |
| Uncertainty registers are separate and owned. | Unverified | All accountable people are TBD. |
| Every requirement has complete metadata and a matching category ID. | Pass | Owners are explicitly TBD; Martyn Fewtrell is the acceptance authority. |
| Requirements are atomic, outcome-focused, and solution-free. | Pass | Technical choices are excluded from the baseline. |
| Each requirement has verification, pass criteria, evidence, and acceptance authority. | Pass | Martyn Fewtrell is the acceptance authority. |
| Scope, capabilities, qualities, security, data, interfaces, operations, lifecycle, dependencies, and acceptance are covered or explicitly excluded. | Pass | Cost, legal obligations, and targets are excluded pending evidence. |
| Each requirement traces through rationale, design dependency, delivery status, evidence, and acceptance. | Pass | Delivery and evidence do not yet exist. |
| Markdown structure is readable. | Pass | Per-requirement two-column tables avoid a wide baseline table. |

## Change History

| Version | Date | Change summary | Drafted by | Approved by | Approval status |
| --- | --- | --- | --- | --- | --- |
| 0.1 | 2026-08-04 | Initial Draft created from supplied research evidence and user input. | GitHub Copilot | None | Not approved |