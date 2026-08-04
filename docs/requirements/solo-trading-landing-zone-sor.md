# Statement of Requirements: Solo Trading Landing Zone

> Status: Draft
> Version: 0.6
> Date: 2026-08-04
> Project owner: Individual developer
> Baseline authority: Individual developer
> Acceptance authority: Individual developer
> Approval status: **Not approved**

## Purpose and Decision

This Draft SOR defines the user outcomes needed to assess a landing zone and a non-trading proof. It supports a future decision by the project owner on whether the proof has met its stated acceptance conditions.

The proof must allow a test-only workload to be administered non-publicly by the project owner from the home office through a status view. The workload may only display status and record a status view. The proof must show that the same status-view action by the project owner on the same workload succeeds from the home office and is refused from an independent outside connection. This bounded paired result establishes non-public administration for this proof. It must also show that Test and Production proof workloads remain distinct within the defined proof.

This document does not select or approve a solution, delivery approach, or live-trading service.

## Scope and Boundaries

**In scope**

- A landing zone and a non-trading proof only.
- Test and Production environments.
- Non-public administration by the project owner from the home office.
- Private validation by the project owner.
- A verification procedure, defined before proof execution, for recording proof observations.

**Out of scope**

- Live trading.
- Public user access.
- Trading functions beyond the test-only workload.
- Any claim of resilience or recovery capability.
- Solution, delivery, and operational-design details.
- The method for identifying home-office and outside access contexts, including any connection or location identifiers.

## Evidence Inventory

| ID | Source | Date | Claim supported | Evidence classification |
| --- | --- | --- | --- | --- |
| EVD-001 | Supplied research document | 2026-08-04 | Background context only. It contains observed facts, assumptions, inferences, and recommendations. It does not establish a project decision or a requirement in this SOR. | Supplied research context; not a decision |
| UIP-001 | User-provided input | 2026-08-04 | The individual developer is project owner, baseline authority, and acceptance authority. | User-provided input |
| UIP-002 | User-provided input | 2026-08-04 | Scope is a landing zone and a non-trading proof only. Live trading is out of scope. | User-provided input |
| UIP-003 | User-provided input | 2026-08-04 | Test and Production environments are mandatory. | User-provided input |
| UIP-004 | User-provided input | 2026-08-04 | The project owner must perform the same status-view action on the same proof workload for both access attempts. The home-office attempt must succeed. The outside-home-office attempt must be refused. | User-provided input |
| UIP-005 | User-provided input | 2026-08-04 | The proof workload may only display status and record that its status was viewed. It must not trade, connect to a broker, perform a financial transaction, or perform another function without controlled change. | User-provided input |
| UIP-007 | User-provided input | 2026-08-04 | The separation proof must identify the Test workload and controlled Test update action before verification. The update must not add a workload function beyond status display and status-view recording. It must identify the Production workload's status and owner access before the Test update. After the update, the owner must view Production status and record whether both identified outcomes match their before-update observations. | User-provided input |
| UIP-008 | User-provided input | 2026-08-04 | Non-public administration by the named owner from the home office is mandatory. Public user access remains a scope boundary only, with no control requirement or acceptance test. | User-provided input |
| UIP-006 | User-provided input | 2026-08-04 | Public user access is excluded as a scope boundary only. No acceptance test or control requirement is required for it. | User-provided input |
| UIP-009 | User-provided input | 2026-08-04 | The method for identifying home-office and outside access contexts is outside this SOR. It is a verification-procedure detail to define before proof execution. No evidence in this Draft establishes that method. | User-provided input |

No regional location, access-context identification method, public exposure, monitoring approach, security approach, or UK West option is a confirmed decision in this Draft.

## Stakeholders and Governance

| Role | Person or team | Accountability | Authority |
| --- | --- | --- | --- |
| Project owner | Individual developer | Owns scope, requirements, and unresolved matters. | Requests changes and resolves open questions. |
| Baseline authority | Individual developer | Approves or rejects a future baseline. | Sole baseline authority. |
| Acceptance authority | Individual developer | Accepts or rejects proof evidence. | Sole acceptance authority. |

## Requirement Baseline

All requirements below are mandatory, Draft, and not approved.

### SOR-FR-001: Bound Proof Workload Behaviour

| Field | Value |
| --- | --- |
| Normative statement | The proof workload shall only display status and record that its status was viewed. It shall not trade, connect to a broker, perform a financial transaction, or perform another function without controlled change. |
| Type | Functional |
| Source / rationale | User-provided input: UIP-005. The proof workload has a stated, limited behaviour boundary. |
| Priority | Must have |
| Owner | Individual developer |
| Status | Draft |
| Dependency | A verification procedure must define the bounded demonstration and review before proof execution. |
| Verification method | Demonstration and review |
| Verification responsibility | Individual developer |
| Objective pass criterion | A bounded demonstration and review of the identified Test proof workload shows status display and status-view recording as its stated allowed behaviour. The review records that no additional function is included in the demonstrated workload behaviour without controlled change. |
| Required evidence | Dated proof record identifying the Test proof workload, the bounded demonstration and review, its stated allowed behaviour, and the review result. |
| Evidence location / data constraints | Evidence location: To be recorded. Data constraints: Not applicable; none are confirmed. |
| Acceptance authority | Individual developer |

### SOR-FR-002: Non-Public Home-Office Owner Administration

| Field | Value |
| --- | --- |
| Normative statement | The service shall demonstrate non-public administration for this proof: the same identified project-owner status-view action on the same identified proof workload shall succeed from the home office and shall be refused from an independent outside connection. |
| Type | Functional |
| Source / rationale | User-provided input: UIP-004; UIP-008; UIP-009. The paired owner outcome is the bounded proof of non-public administration. Public user access remains a scope boundary only. |
| Priority | Must have |
| Owner | Individual developer |
| Status | Draft |
| Dependency | A verification procedure must define, before proof execution, the observation boundary and the format used to identify the project-owner role, proof workload, status-view action, and paired outcomes. The method for identifying the home-office and independent outside connection contexts is outside this SOR. |
| Verification method | Demonstration |
| Verification responsibility | Individual developer |
| Objective pass criterion | All of the following outcomes are required: the identified project owner successfully performs the identified status-view action on the identified proof workload from the home office; the same identified owner, workload, and action are used from an independent outside connection; and that outside attempt is refused. This bounded paired result establishes non-public administration for this proof. |
| Required evidence | One dated paired proof record that identifies the project owner, proof workload, and status-view action consistently; records the successful home-office outcome and refused independent-outside-connection outcome; and records the comparison against the required paired outcomes in the format defined before proof execution. |
| Evidence location / data constraints | Evidence location: To be recorded. Data constraints: Not applicable; none are confirmed. |
| Acceptance authority | Individual developer |

### SOR-FR-003: View Operational Activity

| Field | Value |
| --- | --- |
| Normative statement | The service shall allow the project owner to view the status of the named proof workload and record that the status was viewed. |
| Type | Functional |
| Source / rationale | User-provided input: UIP-005. The proof workload may show its status and record that the status was viewed. |
| Priority | Must have |
| Owner | Individual developer |
| Status | Draft |
| Dependency | The proof record must identify the proof workload and the status-view action in the format defined by the verification procedure. |
| Verification method | Demonstration |
| Verification responsibility | Individual developer |
| Objective pass criterion | The project-owner role views the status of the identified proof workload. A dated status-view record identifies that workload and records that its status was viewed. |
| Required evidence | Dated proof record identifying the proof workload and a dated status-view record for that same workload. |
| Evidence location / data constraints | Evidence location: To be recorded. Data constraints: Not applicable; none are confirmed. |
| Acceptance authority | Individual developer |

### SOR-NFR-002: Identify Test and Production

| Field | Value |
| --- | --- |
| Normative statement | Test and Production proof workloads shall be separately identifiable and separately administered for this proof. |
| Type | Non-functional: environment separation |
| Source / rationale | User-provided input: UIP-003; UIP-007. Test and Production must remain distinct within the stated proof boundary. |
| Priority | Must have |
| Owner | Individual developer |
| Status | Draft |
| Dependency | A verification procedure must define, before proof execution, the format used to identify each proof workload, its named environment, and the proof observations. |
| Verification method | Review and demonstration |
| Verification responsibility | Individual developer |
| Objective pass criterion | Before the controlled Test update, the proof record identifies the Test and Production proof workloads under their named environments and records a status view for each. The project-owner role administers each identified workload separately for the stated proof actions. |
| Required evidence | Dated proof record identifying each proof workload and its named environment, with a recorded status view for each before the controlled Test update. |
| Evidence location / data constraints | Evidence location: To be recorded. Data constraints: Not applicable; none are confirmed. |
| Acceptance authority | Individual developer |

### SOR-NFR-003: Protect Production from a Test Action

| Field | Value |
| --- | --- |
| Normative statement | The service shall preserve the observed status and project-owner access outcomes for the identified Production proof workload after the identified, controlled Test update. The Test update shall not add a workload function beyond status display and status-view recording. |
| Type | Non-functional: environment separation |
| Source / rationale | User-provided input: UIP-003; UIP-007. The proof must demonstrate bounded Test and Production separation. |
| Priority | Must have |
| Owner | Individual developer |
| Status | Draft |
| Dependency | A verification procedure must define, before proof execution, the observation boundary and format used to identify the workloads, the controlled Test update action, its bounded workload behaviour, and the observed Production outcomes. |
| Verification method | Demonstration and review |
| Verification responsibility | Individual developer |
| Objective pass criterion | All of the following outcomes are required: before the controlled Test update, the proof record identifies the Test workload and update action and records the identified Production status and project-owner access outcomes; the Test update does not add a workload function beyond status display and status-view recording; and after the update, the identified Production status and project-owner access outcomes match their recorded before-update outcomes. The comparison is required evidence of the matching outcomes. |
| Required evidence | Dated proof record identifying the Test proof workload and controlled update action; the stated bounded workload behaviour of that update; the Production proof workload and its identified status and project-owner access outcomes before the update; the completed Test update; the subsequent Production status and project-owner access outcomes; and the recorded before-and-after comparison. |
| Evidence location / data constraints | Evidence location: To be recorded. Data constraints: Not applicable; none are confirmed. |
| Acceptance authority | Individual developer |

## Verification and Acceptance

The acceptance authority will assess each requirement separately against its stated evidence and pass criterion. The proof is ready for acceptance assessment only when all of the following are demonstrated:

- A bounded demonstration and review shows status display and status-view recording as the stated allowed behaviour of the Test proof workload.
- The same identified project owner, proof workload, and status-view action succeed from the home office and are refused from an independent outside connection. This bounded paired result establishes non-public administration for this proof.
- A status-view record for the identified proof workload records that its status was viewed.
- Before the controlled Test update, the Test and Production proof workloads are identified under their named environments and each has a recorded status view.
- The controlled Test update does not add a workload function beyond status display and status-view recording. After the update, the identified Production status and project-owner access outcomes match their recorded before-update outcomes, with the comparison recorded as evidence.

The verification procedure must define the observation boundary and proof-record format before proof execution. It must not prescribe or claim that this Draft establishes the method used to identify home-office and outside access contexts. Acceptance is not recorded until the acceptance authority records a decision. This Draft does not establish approval, live-trading readiness, or any recovery capability.

## Assumption Register

| ID | Assumption | Owner | Impact if false | Review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| ASM-001 | A verification procedure can define a repeatable observation boundary and proof-record format for the paired status-view demonstration without adding an access-context identification requirement to this SOR. | Individual developer | SOR-FR-002 may not be verifiable as drafted or may need revision. | Before proof execution. | Open |
| ASM-002 | A test-only workload can be defined without live trading or public user access. | Individual developer | SOR-FR-001 and its acceptance evidence may need revision. | Before verification planning. | Open |

## Risk Register

| ID | Risk | Owner | Impact | Review trigger | Status |
| --- | --- | --- | --- | --- |
| RSK-001 | The verification procedure may not define a repeatable way to observe the required paired status-view outcomes. | Individual developer | SOR-FR-002 may be delayed, infeasible, or require a scope decision. | Before proof execution. | Open |
| RSK-002 | Unresolved privacy, legal, or data-handling needs may change later operating requirements. | Individual developer | Later scope, evidence, or acceptance conditions may need change. | Before handling personal, trading, or regulated data. | Open |
| RSK-003 | An unmade UK West decision may create an unsupported recovery expectation. | Individual developer | No recovery claim can be made until a decision and supporting requirements exist. | Any request for a UK West or recovery outcome. | Open |

## Issue Register

| ID | Issue | Owner | Impact | Review trigger | Status |
| --- | --- | --- | --- | --- |
| ISS-001 | No evidenced issue is recorded in this Draft. | Individual developer | None known. | Update when an evidenced problem is identified. | Open |

## Open Question Register

| ID | Question | Owner | Impact | Review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| QST-001 | Is a regional location required for this work? | Individual developer | No location requirement can be added until decided. | Before any location-dependent commitment. | Open |
| QST-002 | What retention period is required for proof records? | Individual developer | No retention requirement can be set. | Before setting record-retention expectations. | Open |
| QST-003 | What data classification applies to the proof and its records? | Individual developer | Data-handling requirements cannot be set. | Before creating, collecting, or retaining data. | Open |
| QST-004 | Which privacy or legal obligations apply? | Individual developer | Scope, evidence, and acceptance conditions may need change. | Before handling personal, trading, or regulated data. | Open |
| QST-005 | What recovery time objective is required? | Individual developer | No recovery-time requirement can be set. | Before requesting a recovery outcome. | Open |
| QST-006 | What recovery point objective is required? | Individual developer | No recovery-point requirement can be set. | Before requesting a recovery outcome. | Open |
| QST-007 | Which data stores or external integrations are needed? | Individual developer | Later scope, dependencies, and acceptance evidence may need change. | Before expanding beyond the proof. | Open |
| QST-008 | What capacity or service targets are required? | Individual developer | No capacity or service requirement can be set. | Before setting service expectations. | Open |
| QST-009 | What budget is available? | Individual developer | Feasibility and future scope decisions may be affected. | Before approving a later scope or commitment. | Open |
| QST-010 | What observation boundary and proof-record format will the verification procedure use for the paired status-view demonstration? | Individual developer | Direct dependency for SOR-FR-002. The method for identifying access contexts remains outside this SOR. | Before proof execution. | Open |
| QST-011 | Should UK West support a future outcome? | Individual developer | No UK West scope or recovery claim can be made. | Before any UK West work or recovery claim. | Open |
| QST-012 | What operating responsibilities, review frequency, and record ownership are needed after the proof? | Individual developer | Later-operation requirements cannot be set. | Before moving beyond the proof. | Open |

## Decision Register

| ID | Decision | Owner | Source | Status |
| --- | --- | --- | --- | --- |
| DEC-001 | The individual developer is the project owner, baseline authority, and acceptance authority. | Individual developer | UIP-001 | Recorded |
| DEC-002 | The scope is a landing zone and a non-trading proof only. Live trading is out of scope. | Individual developer | UIP-002 | Recorded |
| DEC-003 | Test and Production environments are mandatory. | Individual developer | UIP-003 | Recorded |
| DEC-004 | The project owner must use the same proof workload and status-view action for both administration attempts. The home-office attempt must succeed. The outside-home-office attempt must be refused. | Individual developer | UIP-004 | Recorded |
| DEC-005 | The proof workload may only display status and record that its status was viewed. Any additional function requires controlled change. | Individual developer | UIP-005 | Recorded |
| DEC-006 | Public user access is excluded as a scope boundary only. It has no acceptance test or control requirement. | Individual developer | UIP-006 | Recorded |
| DEC-007 | The separation proof identifies the Test workload and controlled Test update action before verification. The update does not add a workload function beyond status display and status-view recording. It observes the Production workload's status and project-owner access before the Test update. After the update, the project owner views Production status and records whether both outcomes match their before-update observations. | Individual developer | UIP-007 | Recorded |
| DEC-008 | Non-public administration by the named owner from the home office is mandatory. Public user access remains a scope boundary only, with no control requirement or acceptance test. | Individual developer | UIP-008 | Recorded |
| DEC-009 | The method for identifying home-office and independent outside connection contexts is a verification-procedure detail outside SOR scope. | Individual developer | UIP-009 | Recorded |

## Traceability Register

The requirement-to-source links below are stable Draft links. Design, work item or implementation, delivery, evidence, and acceptance records do not yet exist. Lifecycle traceability remains unverified until those records are created.

### SOR-FR-001

| Field | Value |
| --- | --- |
| Source | UIP-005 |
| Design | Not yet created - Draft |
| Work item / implementation | Not yet created - Draft |
| Delivery | Not yet created - Draft |
| Evidence | Not yet created - Draft |
| Acceptance status | Not yet created - Draft |
| Last reviewed | 2026-08-04 (Draft review) |
| Lifecycle traceability | Unverified |

### SOR-FR-002

| Field | Value |
| --- | --- |
| Source | UIP-004; UIP-008; UIP-009 |
| Design | Not yet created - Draft |
| Work item / implementation | Not yet created - Draft |
| Delivery | Not yet created - Draft |
| Evidence | Not yet created - Draft |
| Acceptance status | Not yet created - Draft |
| Last reviewed | 2026-08-04 (Draft review) |
| Lifecycle traceability | Unverified |

### SOR-FR-003

| Field | Value |
| --- | --- |
| Source | UIP-005 |
| Design | Not yet created - Draft |
| Work item / implementation | Not yet created - Draft |
| Delivery | Not yet created - Draft |
| Evidence | Not yet created - Draft |
| Acceptance status | Not yet created - Draft |
| Last reviewed | 2026-08-04 (Draft review) |
| Lifecycle traceability | Unverified |

### SOR-NFR-002

| Field | Value |
| --- | --- |
| Source | UIP-003; UIP-007 |
| Design | Not yet created - Draft |
| Work item / implementation | Not yet created - Draft |
| Delivery | Not yet created - Draft |
| Evidence | Not yet created - Draft |
| Acceptance status | Not yet created - Draft |
| Last reviewed | 2026-08-04 (Draft review) |
| Lifecycle traceability | Unverified |

### SOR-NFR-003

| Field | Value |
| --- | --- |
| Source | UIP-003; UIP-007 |
| Design | Not yet created - Draft |
| Work item / implementation | Not yet created - Draft |
| Delivery | Not yet created - Draft |
| Evidence | Not yet created - Draft |
| Acceptance status | Not yet created - Draft |
| Last reviewed | 2026-08-04 (Draft review) |
| Lifecycle traceability | Unverified |

## Change and Approval Controls

This document is a Draft and is not approved. Only the baseline authority may approve a future baseline or a change to a baseline.

A proposed change must record its reason, affected requirements, effects on open questions, verification evidence, and acceptance. It remains Draft until the baseline authority records approval.

| Version | Date | Change summary | Drafted by | Approval status |
| --- | --- | --- | --- | --- |
| 0.1 | 2026-08-04 | Superseded Draft. Its requirements are not retained in this SOR. | GitHub Copilot on behalf of the individual developer | Not approved |
| 0.2 | 2026-08-04 | Superseded Draft. It records public user access as a scope boundary only and strengthens the bounded home-office and Test/Production proof criteria. | GitHub Copilot on behalf of the individual developer | Not approved |
| 0.3 | 2026-08-04 | Makes the paired home-office and independent-connection proof explicit. Requires the proof record to identify the workload as test-only and non-trading, and binds the viewed activity record to that workload. | GitHub Copilot on behalf of the individual developer | Not approved |
| 0.4 | 2026-08-04 | Defines non-public owner administration as the home-office current-status view. Binds harmlessness and status-view records to the named workload, bounds the Test/Production proof, adds verification-planning fields, and expands Draft traceability fields. | GitHub Copilot on behalf of the individual developer | Not approved |
| 0.5 | 2026-08-04 | States the proof workload's allowed behaviour boundary and controlled-change condition. Makes non-public home-office administration explicit, strengthens the bounded Test/Production comparison, and defers access-context identification and proof-record format to a pre-execution verification procedure. | GitHub Copilot on behalf of the individual developer | Not approved |
| 0.6 | 2026-08-04 | Consolidates the logically inseparable paired owner proof in SOR-FR-002 and requires both outcomes. Requires Production status and owner-access outcomes after the controlled Test update to match their recorded before-update outcomes, records the comparison as evidence, bounds the Test update to existing workload behaviour, and records UIP-009 as a Draft decision. | GitHub Copilot on behalf of the individual developer | Not approved |

## Draft Quality Review

| Check | Result | Notes |
| --- | --- | --- |
| Draft status, authority, decision, scope, date, and evidence are recorded. | Pass | Status is Draft and approval status is explicitly Not approved. |
| Facts, user decisions, research context, and unresolved information are distinguished. | Pass | EVD-001 is research context only. UIP and DEC records identify confirmed user decisions. |
| Registers are separate and owned. | Pass | Assumptions, risks, issues, questions, and decisions are separate and owned by the individual developer. |
| Mandatory requirements have required metadata. | Pass | Each requirement has an ID, statement, type, source, priority, owner, status, dependency, verification method, verification responsibility, pass criterion, evidence, evidence location or data constraints, and acceptance authority. |
| Requirements are atomic, outcome-oriented, and free of vague qualifiers. | Unverified | SOR-FR-002 combines the home-office success and independent-outside-connection refusal because both are required outcomes of one bounded proof of non-public administration. SOR-NFR-003 combines the before-and-after Production outcomes and Test-update behaviour boundary because all are required for one bounded separation proof. The terms status, test-only workload, controlled Test update, and independent outside connection are used only with their stated proof contexts; the verification procedure still needs to define its observation boundary and proof-record format. |
| Requirements and supporting content are solution-free. | Pass | No product, protocol, architecture, configuration, regional location, delivery mechanism, or unconfirmed research recommendation is required. |
| Acceptance conditions are explicit and repeatable at outcome level. | Unverified | SOR-FR-002 requires both paired owner outcomes. SOR-NFR-003 requires the identified Production status and project-owner access outcomes after the controlled Test update to match their recorded before-update outcomes, with comparison as evidence. The observation boundary and proof-record format must still be defined in a verification procedure before proof execution; access-context identification remains outside SOR scope. |
| Lifecycle traceability is complete. | Unverified | Requirement-to-source links are recorded. Design, work item or implementation, delivery, evidence, and acceptance records are not yet created. |
| Operational and verification-procedure uncertainties are visible. | Unverified | Region, retention, classification, privacy/legal applicability, recovery objectives, data stores or integrations, capacity or service targets, budget, verification procedure, UK West, and later-operation decisions remain open. |
| Markdown structure | Pass | Manual structural review confirms a hierarchical heading sequence and matching delimiter columns in each table. |
