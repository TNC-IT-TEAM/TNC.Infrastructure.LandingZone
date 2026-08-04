# Statement of Requirements: Landing Zone

> Status: Draft
> Version: 0.1
> Date: 2026-08-04
> Baseline authority: Martyn Fewtrell
> Approval status: Not approved

## Purpose and Decision

This Draft defines the user requirements for a landing zone that can host workloads in separate environments and support their safe operation. It supports a decision by a named human authority on whether the requirements are ready to be baselined.

The intended audience is the service owner, technical owner, operations owner, and acceptance authority. Martyn Fewtrell is the named person for each of these roles in the user-provided decisions.

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
- Service lifecycle management is out of scope. This does not change QST-001's decision that test and production environments are required.
- Selection or design of products, platforms, locations, networks, deployment methods, or other technical solutions.
- Service targets, legal obligations, budgets, and workload-specific recovery targets. These remain subject to named owner decisions.
- Approval of this Draft or any technical design.

## Stakeholders and Governance

| Role | Named person or team | Accountability | Approval or escalation authority |
| --- | --- | --- | --- |
| Sponsor | Martyn Fewtrell | Set the intended business outcome. | Martyn Fewtrell |
| Service owner | Martyn Fewtrell | Own the landing zone outcome and priorities. | Martyn Fewtrell |
| Technical owner | Martyn Fewtrell | Own technical-design decisions outside this SOR. | Martyn Fewtrell |
| Security, privacy, or compliance owner | Martyn Fewtrell | Decide applicable obligations and controls. | Martyn Fewtrell |
| Operations owner | Martyn Fewtrell | Own operational readiness and evidence. | Martyn Fewtrell |
| Acceptance authority | Martyn Fewtrell | Accept or reject requirement evidence. | Martyn Fewtrell |

### Named Human Approval Actions

| Action | Named human required | Status |
| --- | --- | --- |
| Assign a service owner. | Martyn Fewtrell | Complete for Draft; baseline review remains open |
| Assign the unassigned role owners. | Martyn Fewtrell | Complete for Draft; baseline review remains open |
| Review this Draft for baseline approval. | Martyn Fewtrell | Not approved |
| Record acceptance or rejection of each requirement. | Martyn Fewtrell | Open |

## Evidence Inventory

| ID | Source | Date | Claim supported | Evidence status |
| --- | --- | --- | --- | --- |
| EVD-001 | Supplied research evidence | 2026-08-04 | The landing zone needs environment separation, controlled access, public and administrative access boundaries, monitoring, governance, and staged recovery planning. | Research recommendation; not a requirement or approval |
| EVD-002 | User request | 2026-08-04 | Create a Draft SOR for the landing zone using functional and non-functional user requirements only. | User-provided input |
| EVD-003 | User-provided elicitation decisions | 2026-08-04 | Resolve environment, administration, data, access, recovery, evidence, and ownership questions without approving the Draft. | User-provided input |
| EVD-004 | Latest user decisions | 2026-08-04 | No legal, regulatory, or other obligations are currently known; an owner review remains open before security and data acceptance. The project will use agile build demonstrations and recorded sign-off for acceptance. Service lifecycle management is explicitly out of scope. | User-provided input; not evidence that no obligations apply |

## Requirement Baseline

All requirements below have Draft status and Must priority. Open questions and pending decisions remain subject to named human review; none represents baseline approval.

### FR1: Separate Workload Environments

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall provide separately identified environments for hosted workloads. |
| Type | Functional |
| Source or rationale | EVD-001; supports separation between workload environments. |
| Priority | Must |
| Owner | Service owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | DEC-004: test and production are required environments. |
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
| Owner | Operations owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | DEC-005: application developers may administer both environments. |
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
| Owner | Service owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | DEC-004: test and production are required environments. |
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
| Owner | Service owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | QST-005: each workload's recovery objectives and outage impact remain to be defined separately. |
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
| Owner | Security, privacy, or compliance owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | DEC-005: application developers may administer both environments. |
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
| Owner | Security, privacy, or compliance owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | DEC-006: data is Internal with normal retention of 30 days, subject to applicable holds and obligations. |
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
| Owner | Operations owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | DEC-006: records have normal retention of 30 days, except legal, regulatory, or investigation holds; applicable obligations remain subject to the security, privacy, or compliance owner. |
| Verification method | Inspection |
| Objective pass criterion | A selected privileged change and access decision each have a record that identifies the action, actor, and time, and the record remains available for the normal 30-day retention period unless a hold applies. |
| Required evidence | Sample activity records and inspection result. |
| Acceptance authority | Martyn Fewtrell |

### IR1: Access Path Separation

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall provide public access to hosted workloads through a path distinct from the administrative path used by application developers. |
| Type | Interface |
| Source or rationale | EVD-001; supports controlled public access and private administration. |
| Priority | Must |
| Owner | Technical owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | DEC-007: hosted workloads require public access and application developers use a separate administrative path. |
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
| Owner | Operations owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | DEC-008: the project acceptance process uses agile demonstrations and recorded sign-off. |
| Verification method | Inspection |
| Objective pass criterion | Each Must requirement has current, repeatable evidence that supports a pass or fail decision against its pass criterion. |
| Required evidence | Requirement evidence and the recorded pass/fail decision. |
| Acceptance authority | Martyn Fewtrell |

### OR1: Operational Visibility

| Field | Value |
| --- | --- |
| Requirement | The landing zone shall enable operators to identify changes, access failures, and loss of hosted-workload health. |
| Type | Operational |
| Source or rationale | EVD-001; supports central diagnostics and actionable alerts. |
| Priority | Must |
| Owner | Operations owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | DEC-009 and QST-008: operational information is received by the operations owner; response targets and escalation rules remain open. |
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
| Owner | Operations owner: Martyn Fewtrell |
| Status | Draft |
| Dependency | QST-005 and QST-008 |
| Verification method | Inspection and demonstration |
| Objective pass criterion | Guidance exists for each stated event, identifies an owner and escalation route, and is used successfully in an agreed exercise. |
| Required evidence | Current guidance, exercise record, and review record. |
| Acceptance authority | Martyn Fewtrell |

## Acceptance Approach

The project will use an agile build with show-and-tell demonstrations to Martyn Fewtrell. The demonstrations and requirement sign-off will be recorded as project acceptance evidence. The assigned acceptance authority shall review each requirement's repeatable evidence, record pass or fail against its pass criterion, and record a decision. This activity is required before any baseline approval. This Draft does not authorize delivery or record acceptance.

An unmet requirement remains Draft until a named human authority records either acceptance after corrective evidence or an approved exception. No approved exception exists in this Draft.

## External Technical-Design Dependencies

These matters are not requirements. They must be resolved by the assigned technical owner outside this SOR and linked to the relevant requirement evidence.

| ID | External technical-design dependency | Related requirements | Owner | Status |
| --- | --- | --- | --- | --- |
| TDD-001 | Select the technical approach for environment separation, controlled access, public access, administrative access, monitoring, and activity records. | FR1, FR2, NF1, SR1, DR1, IR1, OR1 | Technical owner: Martyn Fewtrell | Open |
| TDD-002 | Select the technical approach for handling sensitive access information. | SR2 | Technical owner: Martyn Fewtrell | Open |
| TDD-003 | Select the technical approach for recovery readiness and response guidance. | NF2, OR2 | Technical owner: Martyn Fewtrell | Open |

## Assumptions

| ID | Statement | Owner | Impact if false | Review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| ASM-001 | The landing zone will host workloads that need separate test and production environments. | Service owner: Martyn Fewtrell | FR1 and NF1 may need revision. | Scope confirmation | Open |
| ASM-002 | Hosted workloads require public access and application developers require a separate administrative path. | Service owner: Martyn Fewtrell | IR1 may not apply or may need revision. | Access-use-case confirmation | Open |
| ASM-003 | Data in scope is classified as Internal and normally retained for 30 days, except where a legal, regulatory, or investigation hold applies. | Security, privacy, or compliance owner: Martyn Fewtrell | SR2 and DR1 may need revision if applicable obligations differ. | Owner review of applicable obligations | Open |

## Risks

| ID | Risk | Owner | Impact | Treatment or review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| RSK-001 | Unassigned owners may delay decisions, evidence review, and acceptance. | Sponsor: Martyn Fewtrell | Requirements cannot be baselined or accepted. | Review named ownership before baseline review. | Open |
| RSK-002 | Unknown recovery objectives may lead to a recovery approach that does not meet stakeholder needs. | Service owner: Martyn Fewtrell | NF2 and OR2 cannot be fully assessed. | Define recovery objectives and outage impact separately for each workload. | Open |
| RSK-003 | Unknown applicable obligations may make activity records or sensitive-information handling incomplete. | Security, privacy, or compliance owner: Martyn Fewtrell | SR2 and DR1 may need revision. | Owner identifies applicable obligations; data classification and normal retention are recorded. | Open |

## Issues

| ID | Statement | Owner | Review trigger | Status |
| --- | --- | --- | --- | --- |
| ISS-001 | No named people or teams were supplied for sponsor, service, technical, security, privacy, compliance, or operations roles. | Sponsor: Martyn Fewtrell | Before baseline review | Resolved by EVD-003; retain as historical issue |

## Open Questions

| ID | Question | Owner | Review trigger | Status |
| --- | --- | --- | --- | --- |
| QST-001 | Resolved: test and production environments are required. | Service owner: Martyn Fewtrell | Before baseline review | Resolved by EVD-003 |
| QST-002 | Resolved: application developers may perform privileged administration in both environments. | Service owner: Martyn Fewtrell | Before access acceptance | Resolved by EVD-003 |
| QST-003 | What legal, regulatory, or other obligations apply to the landing zone and its data and activity records? No obligations are currently known from EVD-004; this is not evidence that none apply. | Security, privacy, or compliance owner: Martyn Fewtrell | Before security and data acceptance, and when the scope or data changes | Open; owner review required |
| QST-004 | Resolved: hosted workloads require public access and application developers use a separate administrative path. | Service owner: Martyn Fewtrell | Before interface acceptance | Resolved by EVD-003 |
| QST-005 | Resolved: recovery objectives and acceptable outage impact will be defined separately for each workload. | Service owner: Martyn Fewtrell | Before resilience acceptance | Resolved by EVD-003 |
| QST-006 | Resolved: the project will use agile show-and-tell demonstrations and recorded requirement sign-off as its acceptance process. | Acceptance authority: Martyn Fewtrell | Before acceptance activity | Resolved by EVD-004 |
| QST-007 | Resolved: the operations owner receives operational information. Response targets and escalation rules remain open. | Operations owner: Martyn Fewtrell | Before operational acceptance | Resolved in part by EVD-003 |
| QST-008 | What response times and escalation rules shall the service owner define for operational information? | Service owner: Martyn Fewtrell | Before operational acceptance | Open |

## Decisions

| ID | Decision | Owner | Status |
| --- | --- | --- | --- |
| DEC-001 | Keep technical-solution choices outside the requirement baseline. | User request | Draft working decision |
| DEC-002 | Do not claim regional resilience until recovery objectives and evidence are agreed. | Service owner: Martyn Fewtrell | Pending |
| DEC-003 | Keep this SOR as Draft pending resolution of the listed open questions and objective verification criteria. No baseline approval is granted. | Martyn Fewtrell | Draft; not approved |
| DEC-004 | The required environments are test and production. | Martyn Fewtrell | Draft working decision |
| DEC-005 | Application developers may administer both test and production. | Martyn Fewtrell | Draft working decision |
| DEC-006 | Data is classified as Internal and has normal retention of 30 days, subject to the outcome of the open obligations review in QST-003. | Martyn Fewtrell | Draft working decision; QST-003 open |
| DEC-007 | Hosted workloads require public access, and application developers use a separate administrative path. | Martyn Fewtrell | Draft working decision |
| DEC-008 | The project will use an agile build with show-and-tell demonstrations to the project owner, and requirement sign-off will occur through that process. | Martyn Fewtrell | EVD-004; user-provided project process; Draft working decision |
| DEC-009 | The operations owner receives operational information. The service owner defines response times and escalation rules; the targets and rules remain an open decision under QST-008. | Martyn Fewtrell | Partially resolved; QST-008 open |
| DEC-010 | Recovery objectives and acceptable outage impact will be defined separately for each hosted workload. | Martyn Fewtrell | Draft working decision |

## Traceability Register

> Status: Draft. Design, delivery, and acceptance records are not yet available.

| SOR ID | Source or rationale | External technical-design dependency or rationale | Specification or work-item record | Implementation or delivery record | Verification evidence | Acceptance status | Last reviewed |
| --- | --- | --- | --- | --- | --- | --- | --- |
| FR1 | EVD-001; EVD-003 | TDD-001 | Not available | Not available | Environment inventory and demonstration result | Draft; not accepted | 2026-08-04 |
| FR2 | EVD-001; EVD-003 | TDD-001 | Not available | Not available | Access record and demonstration result | Draft; not accepted | 2026-08-04 |
| NF1 | EVD-001; EVD-003 | TDD-001 | Not available | Not available | Change record and test result | Draft; not accepted | 2026-08-04 |
| NF2 | EVD-001; EVD-003 | TDD-003 | Not available | Not available | Recovery decision records | Draft; not accepted | 2026-08-04 |
| SR1 | EVD-001; EVD-003 | TDD-001 | Not available | Not available | Access record and test result | Draft; not accepted | 2026-08-04 |
| SR2 | EVD-001; EVD-003 | TDD-002 | Not available | Not available | Information inventory and test result | Draft; not accepted | 2026-08-04 |
| DR1 | EVD-001; EVD-003 | TDD-001 | Not available | Not available | Sample activity records | Draft; not accepted | 2026-08-04 |
| IR1 | EVD-001; EVD-003 | TDD-001 | Not available | Not available | Access-path inventory and demonstration result | Draft; not accepted | 2026-08-04 |
| TR1 | EVD-002; EVD-003; EVD-004 | Not applicable; evidence location and acceptance process are recorded in DEC-008 | Not available | Not available | Requirement evidence and recorded pass/fail decision | Draft; not accepted | 2026-08-04 |
| OR1 | EVD-001; EVD-003 | TDD-001 | Not available | Not available | Demonstration results and operator-view records | Draft; not accepted | 2026-08-04 |
| OR2 | EVD-001; EVD-003 | TDD-003 | Not available | Not available | Guidance and exercise record | Draft; not accepted | 2026-08-04 |

## Quality Review

| Check | Result | Finding |
| --- | --- | --- |
| Draft status and approval authority are explicit. | Pass | Martyn Fewtrell is the named baseline and acceptance authority. |
| Decision, audience, scope, time boundary, evidence sources, and evidence status are recorded. | Pass | Named stakeholder roles and the acceptance authority are recorded. |
| Facts, recommendations, and unknowns are distinct. | Pass | Research recommendations are held as external technical-design dependencies. |
| Uncertainty registers are separate and owned. | Pass | Open recovery, obligations, and operational-response questions have named owners and review triggers. |
| Every requirement has complete metadata and a matching category ID. | Pass | Named owners are recorded; Martyn Fewtrell remains the acceptance authority. |
| Requirements are atomic, outcome-focused, and solution-free. | Pass | The requirement wording is solution-free; the agile demonstrations and sign-off process are recorded only in acceptance governance. |
| Each requirement has verification, pass criteria, evidence, and acceptance authority. | Pass | Martyn Fewtrell is the acceptance authority. |
| Scope, capabilities, qualities, security, data, interfaces, operations, lifecycle, dependencies, and acceptance are covered or explicitly excluded. | Pass | Service lifecycle management is explicitly out of scope; this does not change QST-001's decision that test and production environments are required. Cost, applicable obligations, service targets, and workload-specific recovery targets remain open or excluded pending owner decisions. |
| Each requirement traces through rationale, design dependency, specification/work-item record, implementation/delivery record, evidence, and acceptance. | Unverified | The separate specification/work-item and implementation/delivery fields are present, but no records are currently available. |
| Markdown structure is readable. | Pass | Per-requirement two-column tables avoid a wide baseline table. |

## Change History

| Version | Date | Change summary | Drafted by | Approved by | Approval status |
| --- | --- | --- | --- | --- | --- |
| 0.3 | 2026-08-04 | Recorded the user-provided obligations input and open owner review, moved agile demonstrations and sign-off into acceptance governance, removed the Kanban prescription from TR1, and separated traceability record fields. | GitHub Copilot | None | Not approved |
| 0.4 | 2026-08-04 | Recorded the user decision that service lifecycle management is out of scope, while preserving QST-001's decision that test and production environments are required, and corrected QST-006 traceability to EVD-004. | GitHub Copilot | None | Not approved |