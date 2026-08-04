<!-- Historical Draft version 2.1 retained for traceability; superseded by active Draft version 3.0 below.
# Azure Landing Zone Platform for One Initial Application - Statement of Requirements

> Status: Draft
> Version: 2.1
> Date: 2026-08-03
> Baseline, evidence, exception, and production-entry authority: Martyn Fewtrell (executive sponsor); no approval or authorization has been recorded
> Approval status: Not approved

## Purpose and Decision

- **Problem or opportunity:** The business needs a production-capable Azure landing-zone platform for one initial application without enterprise-scale structure or unconfirmed corporate controls.
- **Intended outcome:** A small, operable Azure platform that provides environment isolation, controlled access and deployment, observability, recovery-enabling services, cost guardrails, support for the one initial application, which is containerized, through applicable platform capabilities, and an evidence-based path to grow.
- **Decision supported:** Whether this Draft describes the platform capabilities required to design and deliver the initial application foundation.
- **Success measures:** The initial application can use every applicable platform capability with the stated verification evidence; unknown design inputs remain visible; this Draft implies no baseline or production-entry decision.
- **Audience:** Executive sponsor; prospective platform and application owners; delivery team or service provider.
- **Scope and time boundary:** This Draft covers an Azure landing-zone platform for one initial application, including dedicated test and production environments for that one application, which is containerized. It reflects evidence available on 2026-08-03 and does not select a region, architecture, licence, budget, provider, topology, recovery-objective classification, container hosting solution, Azure service, resource set, or implementation.

## Scope and Boundaries

**In scope**

- Minimal Azure resource and governance structure for one application, including support for required site-to-site and point-to-site VPN connectivity.
- Dedicated test and production environments with effective isolation between them.
- Identity and privileged access, safe configuration and deployment, policy/control capability, observability, alerting, recovery-enabling services, cost visibility and guardrails, network/connectivity patterns, support for the one initial containerized application's applicable platform capabilities, and growth triggers.

**Out of scope**

- Corporate governance bodies, finance processes, periodic access reviews, organization-wide operating cadence, risk appetite, broad compliance procedures, and corporate approval workflows.
- Application architecture, container hosting solution, container runtime, registry, Kubernetes, Azure Container Apps, AKS, container registry, networking pattern, identities, secrets approach, Azure resource selection, data classification, regulatory interpretation, region, RTO/RPO classification, budget, licensing, support agreement, service provider, network topology, and implementation selection.
- Approval of a requirement baseline, production deployment, exception, or implementation design.

**Boundary:** Application and platform design inputs determine configuration and the applicability of platform capabilities for the one initial application, which is containerized. User-provided input indicates application resource boundaries will be managed by the application, but the Azure platform governance boundaries and the impact of that statement on platform design remain unresolved. This Draft does not turn unknown inputs into requirements or select a container hosting solution, Azure service, or resource set.

## Stakeholders and Governance

| Role | Named person or team | Accountability | Approval or escalation authority |
| --- | --- | --- | --- |
| Executive sponsor | Martyn Fewtrell | May approve the SOR baseline, accept requirement evidence, approve exceptions, and authorize production entry only through the required records and conditions. | Only Martyn Fewtrell may perform those actions. |
| Platform owner | To be named | Delivers and operates the platform capabilities and supplies home-office network and VPN technical inputs. | Escalates platform capability gaps or unresolved home-office network and VPN technical inputs to the executive sponsor. |
| Initial application owner | To be named | Supplies application design inputs, authorizes remote users, devices, and required application flows, and validates application use of the platform. | Escalates unresolved application inputs or authorization needs to the executive sponsor. |

Roles are needed accountabilities, not assigned people, corporate functions, or approval workflows.

## Evidence Inventory

| ID | Source | Date/version | Claim supported | Evidence status |
| --- | --- | --- | --- | --- |
| EVD-001 | User-provided input | 2026-08-03 | Production-capable Azure foundation for material workloads; Martyn Fewtrell is the named executive sponsor and is the approval, evidence, exception, and production-entry authority by role. | User-provided |
| EVD-002 | [Azure Landing Zone Guidance for a Small Business](../research/azure-landing-zone-small-business-guidance.md) | Research date 2026-08-03 | Nonbinding research guidance on small landing-zone capabilities, design dependencies, and growth triggers. | Research evidence; observations and recommendations are distinct |
| EVD-003 | User-provided scope refinement | 2026-08-03 | Focus on platform capabilities for one initial application; exclude corporate compliance and management processes unless needed to define or validate a capability. | User-provided |
| EVD-004 | User-provided connectivity and ownership input | 2026-08-03 | The Azure landing zone must support a site-to-site VPN between the home-office network and Azure and point-to-site VPN access for individual home-office users and devices; the platform owner supplies home-office network and VPN technical inputs, and the initial application owner authorizes remote users, devices, and required application flows. | User-provided; primary direct source for VPN requirements |
| EVD-005 | User-provided containerized application and boundary clarification | 2026-08-03 | The one initial application in scope is the containerized application; no second application is in scope. The Azure landing zone must support that containerized application without selecting a container hosting solution, Azure service, or resource set. User input also states application resource boundaries will be managed by the application, but does not resolve Azure platform governance boundaries. | User-provided; primary direct source for containerized-application scope clarification |
| EVD-006 | User-provided drafting decision | 2026-08-03 | Apply solution-neutral drafting across the entire SOR. Requirements must state outcomes and capabilities rather than implementation patterns unless directly user-provided. | User-provided; governs this material Draft revision |
| EVD-007 | User-provided growth reassessment decision | 2026-08-03 | Growth reassessment requires a documented trigger-selection basis and reassessment action; no fixed trigger catalogue is required. | User-provided; primary direct source for ALZ-PLT-111 revision |
| EVD-008 | User-provided alert-verification decision | 2026-08-03 | ALZ-PLT-107 verification tests representative privileged-access and platform-configuration change conditions only, rather than every configured or documented alert condition. | User-provided; primary direct source for ALZ-PLT-107 verification scope |
| EVD-009 | User-provided scope decision | 2026-08-03 | Both a dedicated test environment and a dedicated production environment are mandatory for the one initial containerized application in scope. | User-provided; primary direct source for environment scope |
| EVD-010 | User-provided evidence-retention decision | 2026-08-03 | Controlled platform evidence and acceptance records must be retained, but this Draft must not prescribe how or where retention is implemented. | User-provided; primary direct source for evidence-retention wording |

Research observations support requirement rationale. Recommendations and target-state examples are not approved requirements or implementation decisions.

## Requirement Baseline

All entries are mandatory Draft requirements. `Must` identifies a capability required for the initial application where applicable. Dependencies are design inputs or linked capabilities, not approvals. Martyn Fewtrell is the named executive sponsor and acceptance authority by role; this Draft records no approval or authorization.

### ALZ-PLT-117

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide documented Azure platform governance boundaries and application resource boundaries that identify each boundary's purpose and the initial application's placement. |
| Type | Platform boundaries |
| Source or rationale | EVD-002, EVD-006; documented boundaries support governable placement without selecting a governance structure or resource arrangement. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-002, QST-003 |
| Verification method | Inspection |
| Objective pass criterion | The boundary record identifies every applicable platform governance boundary and application resource boundary, its purpose, and the initial application's placement. |
| Required evidence | Platform-boundary record and deployed-boundary inventory |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-118

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide dedicated test and production environments for the initial application and effective environment isolation such that authorized deployment activity for one environment cannot modify the other without separate authorization for that other environment. |
| Type | Isolation |
| Source or rationale | EVD-002, EVD-006, EVD-009; dedicated test and production environments and their isolation are required without selecting an isolation arrangement or authorization mechanism. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-117, QST-002 |
| Verification method | Inspection and test |
| Objective pass criterion | Dedicated test and production environment boundaries are inventoried, and separate tests show that deployment activity authorized only for test cannot modify production and deployment activity authorized only for production cannot modify test. |
| Required evidence | Dedicated test and production environment-boundary inventory, separate authorization records, and separate test-to-production and production-to-test isolation test records |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-119

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide controlled human privileged access and an independently usable recovery access path that can restore authorized platform administration when normal privileged access is unavailable. |
| Type | Identity and access |
| Source or rationale | EVD-002, EVD-006; controlled privileged access and recovery are required without selecting an access-assignment or recovery mechanism. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-004 |
| Verification method | Inspection and test |
| Objective pass criterion | The privileged-access inventory identifies each human administrator, its authorization basis, and its purpose; a controlled test restores authorized administrative access without normal privileged access. |
| Required evidence | Privileged-access inventory, recovery-access record and procedure, and recovery test record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-120

| Field | Value |
| --- | --- |
| Normative requirement | Before human privileged access is used in production, the platform shall protect that access such that compromise of one authentication factor alone cannot authorize it. |
| Type | Identity security |
| Source or rationale | EVD-002, EVD-006; authentication resilience is required without selecting an identity service or authentication mechanism. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-004 |
| Verification method | Inspection and test |
| Objective pass criterion | The privileged-access record identifies each human privileged access population and test evidence demonstrates that possession or compromise of one authentication factor alone does not authorize privileged access. |
| Required evidence | Privileged-access record, authentication-protection evidence, and authentication-factor test record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-121

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall maintain a complete inventory of applicable deployable platform configurations and reconcile each inventory item to its identified controlled configuration definition and deployed state before production operation depends on that item. |
| Type | Configuration management |
| Source or rationale | EVD-002, EVD-006; configuration reconciliation is required without selecting a configuration-management or deployment mechanism. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-005 |
| Verification method | Inspection and demonstration |
| Objective pass criterion | The inventory identifies every applicable deployable platform configuration; every inventory item links to its identified controlled configuration definition and deployed state; and reconciliation records identify any mismatch and disposition. Representative deployments may supplement but cannot replace item-level reconciliation. |
| Required evidence | Complete configuration inventory, controlled configuration definitions, deployed-state records, item-level reconciliation records, and representative deployment demonstration record where used |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-105

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall evaluate the initial application's applicable resource configuration at documented boundaries and record each result. |
| Type | Configuration evaluation |
| Source or rationale | EVD-002, EVD-006; configuration evaluation and recorded results are required without selecting a control service or mechanism. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-117, QST-002 |
| Verification method | Demonstration |
| Objective pass criterion | A test resource configuration at each applicable boundary produces a recorded evaluation result retrievable by an authorized platform operator. |
| Required evidence | Evaluation-method record, boundary record, and evaluation demonstration record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-106

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall collect and make retrievable Azure control-plane activity information and application diagnostic information selected from the initial application's documented observability inputs. |
| Type | Observability |
| Source or rationale | EVD-002; research identifies activity and diagnostic logging as required to investigate platform changes, security events, and production failures. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-006 |
| Verification method | Demonstration |
| Objective pass criterion | A test control-plane activity is retrievable by an authorized operator, and for each selected application diagnostic category a test event is retrievable from the recorded destination. |
| Required evidence | Observability input record, control-plane activity collection record, diagnostic collection record, and retrieval test records |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-107

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide alerts for privileged-access and platform-configuration changes, and each configured alert shall identify a response destination, responder, and documented response action. |
| Type | Alerting |
| Source or rationale | EVD-002, EVD-008; research supports alerts with an owner and response path, and the user-provided decision defines representative verification scope. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-106, QST-006 |
| Verification method | Test and inspection |
| Objective pass criterion | The configured-alert record identifies the response destination, responder, and documented response action for every configured alert. Separate test records show that one representative privileged-access change and one representative platform-configuration change each produce an alert at its identified response destination. The two representative test records do not test every configured alert condition. |
| Required evidence | Configured-alert record identifying the response destination, responder, and documented response action for every configured alert; one representative privileged-access change alert test record; and one representative platform-configuration change alert test record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-108

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide recovery capability for each stateful component of the initial application according to its documented recovery inputs, including a method to create recoverable data and a method to test restoration. |
| Type | Reliability |
| Source or rationale | EVD-002; recovery goals derive from business requirements and require documented, tested recovery plans. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-007 |
| Verification method | Inspection and test |
| Objective pass criterion | Each documented stateful component has a documented recovery method, and a restoration test demonstrates recovery using that method. |
| Required evidence | Recovery-input record, recovery-capability record, and restoration test record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-109

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide cost visibility attributable to the initial application and a spend-alert guardrail for that attributable cost. |
| Type | Cost management |
| Source or rationale | EVD-002; research supports accountable cost visibility, spend alerts, and investigation of anomalies. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-117, QST-008 |
| Verification method | Demonstration |
| Objective pass criterion | Cost data attributable to the initial application is retrievable, and a representative actual or forecast threshold produces an alert at the identified destination. |
| Required evidence | Cost-attribution record, cost-view retrieval record, spend-alert record, and alert test record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-122

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide connectivity for the initial application's documented authorized flows and exposure needs, and shall restrict a documented verification-only flow not authorized for that connectivity. |
| Type | Connectivity |
| Source or rationale | EVD-002, EVD-006; required connectivity outcomes are retained without selecting a network pattern or control mechanism. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-009 |
| Verification method | Inspection and test |
| Objective pass criterion | The connectivity record identifies every documented authorized flow and exposure need, and tests demonstrate that one authorized flow succeeds while one verification-only unauthorized flow is denied. |
| Required evidence | Connectivity record, authorization record, and connectivity test record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-114

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide site-to-site VPN connectivity between the home-office network and Azure for each documented and authorized applicable route and application flow. |
| Type | Site-to-site VPN connectivity |
| Source or rationale | EVD-004; primary direct user-provided connectivity input. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-122, QST-009, QST-011, QST-013 |
| Verification method | Inspection and test |
| Objective pass criterion | Capability evidence identifies the documented applicable site-to-site routes and application flows authorized by the initial application owner; an authorized-path test succeeds for each applicable documented route and flow; and either a denied-path test demonstrates denial for a documented verification-only denied test candidate or a documented non-applicability rationale records why no denied-path candidate applies to verification. |
| Required evidence | Home-office network and site-to-site VPN technical-input record, initial-application-owner flow-authorization record, site-to-site VPN capability record, applicable route-and-flow record, authorized-path test record, and either an initial-application-owner verification-only denied test-candidate record with denied-path test record or a documented non-applicability rationale |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-115

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide point-to-site VPN access for each remote home-office user and device authorized for its documented applicable route and application flow. |
| Type | Point-to-site VPN connectivity |
| Source or rationale | EVD-004; primary direct user-provided connectivity input. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-122, QST-009, QST-012, QST-014 |
| Verification method | Inspection and test |
| Objective pass criterion | Capability evidence identifies each remote user and device and its documented applicable routes and application flows authorized by the initial application owner; an authorized-path test succeeds for each applicable authorized user or device route and flow; and either a denied-path test demonstrates denial for a documented verification-only denied test candidate or a documented non-applicability rationale records why no denied-path candidate applies to verification. |
| Required evidence | Point-to-site VPN technical-input record, initial-application-owner authorization record for remote users, devices, routes, and flows, point-to-site VPN capability record, applicable access record, authorized-path test record, and either an initial-application-owner verification-only denied test-candidate record with denied-path test record or a documented non-applicability rationale |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-116

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall maintain a documented, evidence-based applicability assessment for the one initial application, which is containerized, covering access, deployment and configuration management, observability, recovery, cost, and connectivity; record an applicable or not-applicable disposition for each area; and demonstrate the application's consumption of every applicable capability. |
| Type | Containerized application platform capability |
| Source or rationale | EVD-005; user-provided outcome requires support for the one initial containerized application without selecting a container hosting solution, Azure service, or resource set. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-105 through ALZ-PLT-109, ALZ-PLT-117 through ALZ-PLT-122, QST-015; ALZ-PLT-114 where site-to-site VPN connectivity is applicable; ALZ-PLT-115 where point-to-site VPN connectivity is applicable |
| Verification method | Inspection and demonstration |
| Objective pass criterion | The applicability assessment records an evidence-based applicable or not-applicable disposition for each named area, and successful consumption evidence exists for every applicable capability. |
| Required evidence | Container-specific technical-documentation input record; documented applicability assessment; evidence supporting each disposition; applicable platform-capability records; and consumption evidence for every applicable capability, including ALZ-PLT-114 or ALZ-PLT-115 evidence where the corresponding VPN connectivity is applicable |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-111

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall maintain a documented growth reassessment record that states the trigger-selection basis and reassessment action for expanding the initial platform capabilities. |
| Type | Evolution |
| Source or rationale | EVD-002, EVD-007; growth reassessment is required without prescribing a fixed trigger catalogue or future implementation. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-105 through ALZ-PLT-109, ALZ-PLT-117 through ALZ-PLT-122 |
| Verification method | Inspection |
| Objective pass criterion | The growth reassessment record states the basis used to select its trigger or triggers and the reassessment action for each selected trigger without selecting a future implementation. |
| Required evidence | Growth reassessment record containing the documented trigger-selection basis and reassessment action |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

## Verification and Acceptance

- **Verification environments and data constraints:** Verification shall use the dedicated test environment. Representative non-sensitive test data shall be used where available. Any verification performed in the dedicated production environment is supplementary and cannot replace verification in the mandatory dedicated test environment; it must remain limited to the evidence needed for the requirement and compatible with the named sponsor's production-entry boundary.
- **Evidence retention:** Controlled platform evidence and acceptance records shall be retained. This Draft does not select the repository, record system, location, or implementation approach for that retention, and those details remain open in QST-010.
- **Acceptance approach:** The platform owner assembles requirement evidence; the initial application owner validates application-specific inputs and tests. Only Martyn Fewtrell, as the named executive sponsor, may approve the SOR baseline, accept evidence, approve an exception, or authorize production entry, and each action still requires its respective records and conditions. This Draft records none of those actions.
- **Exceptions:** This Draft grants no exception. An unmet requirement remains visible in traceability and only Martyn Fewtrell, as the named executive sponsor, may approve a recorded exception before production entry.

## Assumptions

| ID | Statement | Owner | Impact if false | Review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| ASM-001 | Azure is the selected cloud platform for the stated scope. | Executive sponsor | The SOR requires material revision. | Cloud-platform decision changes | Open |
| ASM-002 | The one initial application in scope is the containerized application; no second application is in scope. | Executive sponsor | Platform scope, scale, isolation, and growth requirements may change. | A second application or a separate non-containerized application is proposed | Open |
| ASM-003 | The initial application's test and production resource needs are not yet known, and its data characteristics and applicable obligations remain unresolved and deferred to the technical requirements. These application inputs may affect sizing, data, verification, and boundary details, but cannot remove the mandatory dedicated test environment or dedicated production environment requirement. | Initial application owner | ALZ-PLT-118, ALZ-PLT-117, and related verification may require revision. | Record the inputs in the technical requirements and progress QST-002 before platform design | Open |

## Risks

| ID | Risk | Owner | Impact | Treatment or review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| RSK-001 | Unknown home-office network, site-to-site VPN, or point-to-site VPN technical inputs and constraints could make the affected platform connectivity capability unsuitable. | Platform owner | Rework or unsuitable connectivity capability. | Resolve QST-011 and QST-012 before providing ALZ-PLT-114 or ALZ-PLT-115, as applicable. | Open |
| RSK-004 | Unknown authorized application flows, remote users or devices, or undocumented justification for N/A verification-only denied test candidates could prevent provision or objective verification of the affected VPN capability. | Initial application owner | Rework or unverified connectivity capability. | Resolve QST-009, QST-013, and QST-014 before providing or verifying ALZ-PLT-114 or ALZ-PLT-115, as applicable. | Open |
| RSK-002 | Unknown available capabilities, service constraints, or unresolved application-versus-platform boundary responsibilities could constrain access and authentication, configuration, observability, recovery, cost, or governance-boundary outcomes. | Platform owner | Rework, ambiguity, or unavailable capability. | Resolve QST-003 through QST-008 before the affected capability design. | Open |
| RSK-003 | Growth beyond one application could exceed the initial platform's isolation or operational model. | Platform owner | Cost, security, or operability degradation. | Evaluate ALZ-PLT-111 when a recorded trigger occurs. | Open |

## Issues, Questions, and Decisions

| ID | Type | Statement | Owner | Due date or trigger | Status |
| --- | --- | --- | --- | --- | --- |
| QST-001 | Question | Martyn Fewtrell is the named executive sponsor who alone may approve the SOR baseline, accept requirement evidence, approve exceptions, and authorize production entry. The answer records the authority identity, not any approval or authorization. | Executive sponsor | Resolved by user-provided input; action-specific records and conditions remain required | Resolved |
| QST-002 | Question | What are the initial application's test and production resource needs, data characteristics, and applicable obligations? User input confirms these are not yet known and remain deferred to the technical requirements, so this question is only partially answered and remains open here. These inputs must inform design and verification without removing the mandatory dedicated test environment or dedicated production environment requirement. | Initial application owner | Technical requirements dependency; before platform design | Open |
| QST-003 | Question | Which Azure platform governance boundaries and application resource boundaries are appropriate for the initial application? User input states the application resource boundaries will be managed by the application, which is treated here only as an application-boundary input. The Azure governance boundaries and the impact of that statement on platform design remain unresolved. | Platform owner | Before ALZ-PLT-117 design | Open |
| QST-004 | Question | Which available capabilities and design approach will provide controlled human privileged access, recovery access, and protection against authorization by compromise of one authentication factor? The intended design input is the technical specification, but that document is not yet written, so this question remains open. | Platform owner | Before ALZ-PLT-119 and ALZ-PLT-120 design | Open |
| QST-005 | Question | Which controlled configuration definition and deployment approach will manage platform configuration reconciliation? The intended design input is technical documentation to be written, but that documentation is not yet written, so this question remains open. | Platform owner | Before ALZ-PLT-121 design | Open |
| QST-006 | Question | Which application diagnostic categories, retention needs, configured alert conditions, alert thresholds, response destinations, responders, and documented response actions does the initial application require; and which representative privileged-access change and representative platform-configuration change conditions will be used for ALZ-PLT-107 verification? The intended design inputs are technical documentation to be written, but that documentation is not yet written, so this question remains open. The two representative test conditions do not select or test every configured alert condition. | Initial application owner | Before observability capability design and ALZ-PLT-107 verification | Open |
| QST-007 | Question | What recovery objectives, data retention needs, and stateful components apply to the initial application? User input supplies a 24-hour recovery objective, but this Draft does not yet know whether that figure is the RTO, the RPO, or another recovery objective, and data-retention needs and stateful components remain unknown. This question is therefore only partially answered and remains open. | Initial application owner | Before ALZ-PLT-108 capability design | Open |
| QST-008 | Question | What cost allocation, budget, and alert threshold inputs apply to the initial application? User input confirms these inputs are not yet documented, so this question remains open. | Executive sponsor | Before ALZ-PLT-109 capability design | Open |
| QST-009 | Question | Which connectivity dependencies, exposure needs, and application flows does the initial application owner authorize, including the flows requiring site-to-site or point-to-site VPN access? The intended design input is application documentation to be written, but that documentation is not yet written, so this question remains open. | Initial application owner | Before ALZ-PLT-122, ALZ-PLT-114, and ALZ-PLT-115 design | Open |
| QST-010 | Question | Which controlled record system, repository, or retained record set will hold the required platform evidence and acceptance records? This Draft explicitly requires those records to be retained but does not prescribe how or where that retention is implemented. | Platform owner | Before evidence acceptance | Open |
| QST-011 | Question | What home-office network and site-to-site VPN technical inputs and constraints, including applicable address spaces, overlaps, and routes, must be captured for ALZ-PLT-114? Specific inputs remain open, and this Draft does not prescribe how they are supplied or implemented. | Platform owner | Before providing site-to-site VPN capability for ALZ-PLT-114 | Open |
| QST-012 | Question | What point-to-site VPN technical inputs and constraints must be captured for ALZ-PLT-115? Specific inputs remain open, and this Draft does not prescribe how they are supplied or implemented. | Platform owner | Before providing point-to-site VPN capability for ALZ-PLT-115 | Open |
| QST-013 | Question | Which verification-only denied test candidate for site-to-site VPN, such as an unauthorized user or device or a flow not authorized for site-to-site VPN, applies to ALZ-PLT-114? User input currently records this as N/A. Before verification, either a denied test candidate and denied-path test must be documented or the reason that a denied test candidate is not applicable to verification must be documented. This input is solely for verification and does not establish a broader security policy. | Initial application owner | Before ALZ-PLT-114 denied-path verification or non-applicability determination | Open |
| QST-014 | Question | Which verification-only denied test candidate for point-to-site VPN, such as an unauthorized user or device or a flow not authorized for point-to-site VPN, applies to ALZ-PLT-115? User input currently records this as N/A. Before verification, either a denied test candidate and denied-path test must be documented or the reason that a denied test candidate is not applicable to verification must be documented. This input is solely for verification and does not establish a broader security policy. | Initial application owner | Before ALZ-PLT-115 denied-path verification or non-applicability determination | Open |
| QST-015 | Question | Which container-specific application characteristics are needed to determine the evidence-based applicable or not-applicable disposition for access, deployment and configuration management, observability, recovery, cost, and connectivity in the ALZ-PLT-116 applicability assessment for the one initial application, which is containerized? The intended design inputs are technical documentation not yet written. Environment and resource needs are deferred to the technical requirements through open QST-002; observability by QST-006; recovery by QST-007; cost by QST-008; and connectivity and VPN technical inputs by QST-009, QST-011, and QST-012. This question selects no container hosting solution, Azure service, or resource set. | Initial application owner | Before ALZ-PLT-116 capability assessment and verification | Open |
| DEC-001 | Decision | This Draft is limited to platform capabilities for one initial application and does not impose corporate compliance procedures or select application/platform design values. | Executive sponsor | Revisit on material scope change | Draft |
| DEC-002 | Decision | Growth reassessment will record its trigger-selection basis and reassessment action without using a fixed trigger catalogue. | Platform owner | When ALZ-PLT-111 is prepared or reassessed | Draft |
| DEC-003 | Decision | ALZ-PLT-107 verification will test one representative privileged-access change condition and one representative platform-configuration change condition, not every configured or documented alert condition. | User | When ALZ-PLT-107 verification is planned or reassessed | Draft |
| DEC-004 | Decision | Both a dedicated test environment and a dedicated production environment are mandatory for the one initial containerized application in scope. | User | Revisit on material scope change | Draft |

## Traceability

All lifecycle links are **Unverified for Draft**. No entry demonstrates delivery, verification, acceptance, an approved exception, baseline approval, or production-entry authorization.

| SOR ID | Source | Design/delivery link | Verification evidence | Acceptance status |
| --- | --- | --- | --- | --- |
| ALZ-PLT-117 | EVD-002, EVD-003, EVD-005, EVD-006 | Unverified; Azure governance-boundary design remains pending QST-003, and the application-managed resource-boundary input does not resolve platform governance boundaries | Unverified; boundary inspection required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-118 | EVD-002, EVD-003, EVD-006, EVD-009 | Unverified; dedicated test and production environment design depends on the still-open technical requirements input deferred in QST-002 | Unverified; separate test-to-production and production-to-test isolation tests required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-119 | EVD-002, EVD-003, EVD-006 | Unverified; privileged-access and recovery design pending QST-004 | Unverified; access and recovery test required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-120 | EVD-002, EVD-003, EVD-006 | Unverified; authentication-protection design pending QST-004 | Unverified; one-factor test required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-121 | EVD-002, EVD-003, EVD-006 | Unverified; configuration-reconciliation approach pending QST-005 | Unverified; reconciliation demonstration required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-105 | EVD-002, EVD-003, EVD-006 | Unverified; applicable evaluation boundaries depend on the technical requirements input deferred in QST-002 | Unverified; evaluation demonstration required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-106 | EVD-002, EVD-003 | Unverified; observability inputs pending QST-006 | Unverified; retrieval test required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-107 | EVD-002, EVD-003, EVD-008 | Unverified; alert inputs and representative test conditions pending QST-006 | Unverified; inspection of records for every configured alert and separate tests of one representative privileged-access change and one representative platform-configuration change required; the tests do not cover every configured alert condition | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-108 | EVD-002, EVD-003 | Unverified; recovery inputs remain partially open in QST-007 because the 24-hour recovery objective is not yet classified and data-retention needs and stateful components remain unknown | Unverified; restoration test required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-109 | EVD-002, EVD-003 | Unverified; cost inputs pending QST-008 | Unverified; cost and alert demonstration required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-122 | EVD-002, EVD-003, EVD-006 | Unverified; connectivity inputs pending QST-009 | Unverified; connectivity test required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-114 | EVD-004 | Unverified; application-flow authorization pending QST-009, site-to-site technical inputs pending QST-011, and denied-path verification remains conditional on the QST-013 outcome | Unverified; authorized-path site-to-site tests are required, and denied-path testing is required only where a documented verification-only denied test candidate applies; otherwise a documented non-applicability rationale is required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-115 | EVD-004 | Unverified; application authorization pending QST-009, point-to-site technical inputs pending QST-012, and denied-path verification remains conditional on the QST-014 outcome | Unverified; authorized-path point-to-site tests are required, and denied-path testing is required only where a documented verification-only denied test candidate applies; otherwise a documented non-applicability rationale is required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-116 | EVD-005 | Unverified; the one initial application is containerized, but container-specific technical inputs remain pending QST-015; site-to-site VPN dependency applies only where site-to-site VPN connectivity is applicable and point-to-site VPN dependency applies only where point-to-site VPN connectivity is applicable | Unverified; documented applicability assessment with an evidence-based disposition for each named area and consumption evidence for every applicable capability required; applicable VPN evidence required only where the corresponding VPN connectivity is applicable | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-111 | EVD-002, EVD-007 | Unverified; growth reassessment record required | Unverified; inspection of documented trigger-selection basis and reassessment action required | Unverified; Martyn Fewtrell evidence acceptance required |

### Active Lifecycle Detail

All lifecycle links below are **Unverified for Draft**. QST-001 is resolved as an identity question, but no acceptance or exception status can change without the required action-specific records and conditions. QST-002 remains partially answered and open through the technical-requirements dependency. QST-003 has application-boundary input but does not resolve Azure governance boundaries. QST-010 requires retention of controlled evidence and acceptance records without selecting a repository or implementation. QST-013 and QST-014 currently record N/A user input, but each still requires either a denied-path verification case or a documented non-applicability rationale before verification. Each entry uses an associated compact field/value record so lifecycle fields remain readable in Markdown renderers.

#### ALZ-PLT-117
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003, EVD-005, EVD-006 |
| Design or work item | Azure governance-boundary design pending QST-003; the application-managed resource-boundary input does not resolve platform governance boundaries |
| Implementation configuration | Boundary implementation record required |
| Deployment | Unverified |
| Verification | Boundary inspection required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-118
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003, EVD-006, EVD-009 |
| Design or work item | Dedicated test and production environment design depends on the still-open technical requirements input deferred in QST-002 |
| Implementation configuration | Dedicated environment and isolation implementation record required |
| Deployment | Unverified |
| Verification | Separate test-to-production and production-to-test isolation tests required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-119
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003, EVD-006 |
| Design or work item | Privileged-access and recovery design pending QST-004 and the technical specification intended to answer it is not yet written |
| Implementation configuration | Privileged-access and recovery implementation record required |
| Deployment | Unverified |
| Verification | Access/recovery test required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-120
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003, EVD-006 |
| Design or work item | Authentication-protection design pending QST-004 and the technical specification intended to answer it is not yet written |
| Implementation configuration | Authentication-protection implementation record required |
| Deployment | Unverified |
| Verification | One-factor test required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-121
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003, EVD-006 |
| Design or work item | Configuration-reconciliation approach pending QST-005 and the intended technical documentation is not yet written |
| Implementation configuration | Controlled configuration-definition and reconciliation record required |
| Deployment | Unverified |
| Verification | Item-level reconciliation required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-105
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003, EVD-006 |
| Design or work item | Applicable evaluation boundaries depend on the technical requirements input deferred in QST-002 |
| Implementation configuration | Evaluation-method record required |
| Deployment | Unverified |
| Verification | Evaluation demonstration required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-106
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003 |
| Design or work item | Observability inputs pending QST-006 and the intended technical documentation is not yet written |
| Implementation configuration | Control-plane activity and diagnostic collection record required |
| Deployment | Unverified |
| Verification | Retrieval test required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-107
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003, EVD-008 |
| Design or work item | Response destination, responder, documented response action, and representative test conditions pending QST-006 and the intended technical documentation is not yet written |
| Implementation configuration | Configured-alert record identifying the response destination, responder, and documented response action for every configured alert required |
| Deployment | Unverified |
| Verification | Inspect the configured-alert record for every configured alert; separately test one representative privileged-access change and one representative platform-configuration change. The two test records do not cover every configured alert condition. |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-108
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003 |
| Design or work item | Recovery inputs remain partially open in QST-007 because the 24-hour recovery objective is not yet classified and data-retention needs and stateful components remain unknown |
| Implementation configuration | Recovery-capability record required |
| Deployment | Unverified |
| Verification | Restoration test required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-109
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003 |
| Design or work item | Cost inputs pending QST-008 because they are not yet documented |
| Implementation configuration | Cost-attribution and spend-alert record required |
| Deployment | Unverified |
| Verification | Cost/alert demonstration required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-122
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-003, EVD-006 |
| Design or work item | Connectivity inputs pending QST-009 and the intended application documentation is not yet written |
| Implementation configuration | Connectivity implementation record required |
| Deployment | Unverified |
| Verification | Connectivity test required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-114
| Field | Value |
| --- | --- |
| Source/rationale | EVD-004 |
| Design or work item | Application-flow authorization pending QST-009, site-to-site technical inputs pending QST-011, and denied-path verification remains conditional on the QST-013 outcome |
| Implementation configuration | Site-to-site VPN capability record required |
| Deployment | Unverified |
| Verification | Authorized-path site-to-site tests are required. Denied-path testing is required only where a documented verification-only denied test candidate applies; otherwise a documented non-applicability rationale is required. |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-115
| Field | Value |
| --- | --- |
| Source/rationale | EVD-004 |
| Design or work item | Application authorization pending QST-009, point-to-site technical inputs pending QST-012, and denied-path verification remains conditional on the QST-014 outcome |
| Implementation configuration | Point-to-site VPN capability record required |
| Deployment | Unverified |
| Verification | Authorized-path point-to-site tests are required. Denied-path testing is required only where a documented verification-only denied test candidate applies; otherwise a documented non-applicability rationale is required. |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-116
| Field | Value |
| --- | --- |
| Source/rationale | EVD-005 |
| Design or work item | The one initial application is containerized, but container-specific technical inputs remain pending QST-015; site-to-site VPN dependency applies only where site-to-site VPN connectivity is applicable and point-to-site VPN dependency applies only where point-to-site VPN connectivity is applicable |
| Implementation configuration | Applicable platform-capability record required |
| Deployment | Unverified |
| Verification | Documented applicability assessment with an evidence-based disposition for each named area and consumption evidence for every applicable capability required; applicable VPN evidence required only where the corresponding VPN connectivity is applicable |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

#### ALZ-PLT-111
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-007 |
| Design or work item | Growth reassessment record required under DEC-002 |
| Implementation configuration | Growth reassessment record required |
| Deployment | Unverified |
| Verification | Inspection of documented trigger-selection basis and reassessment action required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-03 |

## Legacy Requirement Retirement Register

| Retired ID | Status | Rationale | Replacement ALZ-PLT ID(s) |
| --- | --- | --- | --- |
| ALZ-SOR-001 | Retired | Discovery profile replaced by application inputs and questions. | No replacement |
| ALZ-SOR-002 | Retired | Corporate production gate is outside scope. | No replacement |
| ALZ-SOR-003 | Retired | Governance-boundary outcome retained. | ALZ-PLT-117 |
| ALZ-SOR-004 | Retired | Configuration-reconciliation outcome retained. | ALZ-PLT-121 |
| ALZ-SOR-005 | Retired | Controlled privileged-access outcome retained. | ALZ-PLT-119 |
| ALZ-SOR-006 | Retired | Recovery-access outcome retained. | ALZ-PLT-119 |
| ALZ-SOR-007 | Retired | Control evaluation retained. | ALZ-PLT-105 |
| ALZ-SOR-008 | Retired | Corporate exception process is outside scope. | No replacement |
| ALZ-SOR-009 | Retired | Observability retained. | ALZ-PLT-106 |
| ALZ-SOR-010 | Retired | Alerting retained. | ALZ-PLT-107 |
| ALZ-SOR-011 | Retired | Recovery retained. | ALZ-PLT-108 |
| ALZ-SOR-012 | Retired | Restoration retained. | ALZ-PLT-108 |
| ALZ-SOR-013 | Retired | Cost visibility retained. | ALZ-PLT-109 |
| ALZ-SOR-014 | Retired | Cost-estimate review is outside scope. | No replacement |
| ALZ-SOR-015 | Retired | Change integrity represented by configuration reconciliation. | ALZ-PLT-121 |
| ALZ-SOR-016 | Retired | Connectivity outcome retained. | ALZ-PLT-122 |
| ALZ-SOR-017 | Retired | Exposure input retained in connectivity outcome. | ALZ-PLT-122 |
| ALZ-SOR-018 | Retired | Corporate runbook management is outside scope. | No replacement |
| ALZ-SOR-019 | Retired | Corporate review cadence is outside scope. | No replacement |
| ALZ-SOR-020 | Retired | Production authorization remains an acceptance boundary. | No replacement |
| ALZ-SOR-021 | Retired | Access/recovery retained without periodic review management. | ALZ-PLT-119 |
| ALZ-SOR-022 | Retired | Authentication-resilience outcome retained as a distinct security requirement. | ALZ-PLT-120 |
| ALZ-SOR-023 | Retired | Activity logging and diagnostics retained. | ALZ-PLT-106 |
| ALZ-SOR-024 | Retired | Sponsor naming remains a QST-001 prerequisite. | No replacement |
| ALZ-PLT-113 | Retired | The combined VPN requirement was non-atomic and had ambiguous shared verification. Its changed intent is not reused. | ALZ-PLT-114; ALZ-PLT-115 |
| ALZ-PLT-101 | Retired | Its mandate for a particular governance and resource structure materially changed to solution-neutral boundary outcomes. | ALZ-PLT-117 |
| ALZ-PLT-102 | Retired | Its scope and role-based isolation mechanism materially changed to a solution-neutral isolation outcome. | ALZ-PLT-118 |
| ALZ-PLT-103 | Retired | Its group-assignment mandate materially changed to controlled privileged access and recovery outcomes. | ALZ-PLT-119 |
| ALZ-PLT-104 | Retired | Its version-controlled-source mandate materially changed to configuration reconciliation against a controlled definition. | ALZ-PLT-121 |
| ALZ-PLT-110 | Retired | Its network-pattern and control mandate materially changed to connectivity outcomes. | ALZ-PLT-122 |
| ALZ-PLT-112 | Retired | Its named authentication-pattern mandate materially changed to authentication-resilience outcome. | ALZ-PLT-120 |

## Quality Review

Stakeholder review is permitted for this Draft and is intended to resolve QST-002 through QST-015 and progress the deferred technical-requirements input. QST-001 records Martyn Fewtrell as the named executive sponsor, but this does not approve the baseline, accept evidence, approve an exception, or authorize production entry; those actions remain gated by Martyn Fewtrell and their respective required records and conditions.

| Check | Result | Finding |
| --- | --- | --- |
| Draft status and approval authority are recorded | Pass with limitation | Stakeholder review is permitted to resolve QST-002 through QST-015. Martyn Fewtrell is recorded as the named executive sponsor, but no baseline, evidence acceptance, exception approval, or production-entry authorization has occurred; each action still requires its respective records and conditions. |
| Decision, audience, scope, time boundary, and evidence are recorded | Pass | EVD-001 through EVD-010 distinguish user input, research evidence, the material scope refinement, VPN and containerized-application requirements, solution-neutral drafting, the growth reassessment decision, the representative-alert-verification decision, the mandatory test-and-production environment decision, and the solution-neutral evidence-retention decision. |
| Facts, recommendations, and unknowns are distinct | Pass | Research recommendations are not adopted as requirements; unknown inputs remain in questions and assumptions. |
| Assumptions, risks, issues, questions, and decisions are separate and owned | Pass with limitation | Independent-review ownership defect corrected across v0.9, v1.7, and v1.9: RSK-001 is limited to platform-owner technical-input gaps, RSK-004 is limited to initial-application-owner authorization and verification-input gaps, QST-011 through QST-015 have one accountable owner each, DEC-004 ownership was corrected in v1.7, and DEC-003 ownership was corrected in v1.9. QST-002 remains a partially answered technical-requirements dependency, QST-003 remains ambiguous at the Azure-governance-boundary level, QST-013 and QST-014 require documented non-applicability rationale if they remain N/A, and platform and application owners are not yet named. |
| Mandatory requirements have complete metadata | Pass | Active ALZ-PLT-105 through ALZ-PLT-109 and ALZ-PLT-114 through ALZ-PLT-122 have unique IDs, owner, priority, status, source/rationale, dependency, verification, pass criterion, evidence, and acceptance authority; retired IDs remain in the retirement register. |
| Requirements are atomic, outcome-oriented, and verifiable | Corrected; unverified | v1.2 retires and replaces the materially changed prescriptive intents for governance boundaries, environment isolation, privileged access, configuration reconciliation, connectivity, and authentication protection. ALZ-PLT-105 now states configuration-evaluation outcomes. v1.3 makes ALZ-PLT-116 a documented, evidence-based applicability assessment with applicable or not-applicable dispositions and consumption evidence for each applicable capability, without prescribing an evidence format. ALZ-PLT-111 objectively requires a documented trigger-selection basis and reassessment action without a fixed trigger catalogue. v1.5 requires each configured ALZ-PLT-107 alert to identify its response destination, responder, and documented response action; inspection covers every configured alert record, while separate test records cover only one representative privileged-access change and one representative platform-configuration change. v1.6 makes dedicated test and production environments mandatory and requires separate isolation tests in both directions. v1.7 clarifies that verification uses the dedicated test environment and that unresolved application inputs cannot remove the mandatory environment requirement. v2.1 makes ALZ-PLT-114 and ALZ-PLT-115 denied-path verification conditional on applicability or documented non-applicability rather than unconditionally mandatory. All inputs and verification evidence remain open and unverified for Draft. |
| Prescription is evidence-backed or avoided | Pass | EVD-006 governs solution-neutral drafting. Azure, the one initial containerized application, and both VPN types are direct user-provided scope; specific governance arrangements, access-assignment models, Azure services, control mechanisms, configuration-management methods, network patterns, authentication mechanisms, architectures, products, container hosting solutions, runtimes, and resource sets remain design inputs. |
| Scope coverage is addressed or explicitly not applicable | Pass | Structure, dedicated test and production environment isolation, access, configuration, controls, observability, alerting, recovery, cost, general connectivity, site-to-site and point-to-site VPN support, containerized-application capability consumption, evolution, and acceptance are covered; corporate processes are expressly out of scope. |
| Material traceability is complete | Pass with limitation | Summary and active lifecycle detail separate source, design/work, implementation configuration, deployment, verification, acceptance/exception status, and active-lifecycle review date; QST-002's technical-requirements deferral, QST-003's Azure-governance-boundary ambiguity, QST-010's solution-neutral retention requirement, and the conditional denied-path verification state for QST-013 and QST-014 are visible in affected links; every legacy ALZ-SOR ID, ALZ-PLT-113, and the six v1.2 replacement IDs is visibly retired. Delivery, verification, and acceptance evidence remain unverified for Draft. |
| Markdown rendering and field association | Pass | Requirement metadata and active lifecycle detail use individual two-column field/value tables. Other active tables have matched delimiter columns and no fenced code blocks; historical commented content was not modified. |

**Unverified at stakeholder review:** QST-002 through QST-015; named platform and initial application owners; all platform-capability evidence, verification evidence, acceptance records, and lifecycle delivery links. QST-001 is resolved as the identity question only. QST-002 and QST-007 are only partially answered, QST-003 remains ambiguous at the Azure-governance-boundary level, QST-010 leaves the retention implementation open, and QST-013 and QST-014 require documented non-applicability rationale if they remain N/A. Stakeholder review is permitted and is intended to resolve the remaining questions, including the QST-002 technical-requirements dependency. These remain open Draft items, not approvals or accepted risks; Martyn Fewtrell and the respective evidence, exception, baseline, and production-entry conditions remain required for those actions.

## Approval and Change History

| Version | Date | Change summary | Drafted by | Approved by | Approval status |
| --- | --- | --- | --- | --- | --- |
| 0.1 | 2026-08-03 | Initial controlled Draft based on the initial evidence set. | GitHub Copilot | Not approved | Draft |
| 0.2 | 2026-08-03 | Draft correction recording executive-sponsor evidence and production-entry authority and strengthening testability. | GitHub Copilot | Not approved | Draft |
| 0.3 | 2026-08-03 | Draft correction strengthening configuration reconciliation and authentication-assurance testability. | GitHub Copilot | Not approved | Draft |
| 0.4 | 2026-08-03 | Material scope refinement: replaced corporate compliance and management-process requirements with eleven new `ALZ-PLT` platform capability requirements for one initial application; retired prior `ALZ-SOR` IDs rather than reusing changed intent; moved corporate processes to boundaries and design inputs. | GitHub Copilot | Not approved | Draft |
| 0.5 | 2026-08-03 | Independent-review corrections: named-sponsor approval boundary; MFA; activity logging and privileged/platform-change alerts; item-level IaC reconciliation; verifiable group-based access; visible retirement and lifecycle traceability registers. | GitHub Copilot | Not approved | Draft |
| 0.6 | 2026-08-03 | Draft correction: clarified that stakeholder review is permitted to resolve QST-001 through QST-010 while preserving named-sponsor and action-specific gates; added ALZ-PLT-112 to summary traceability. | GitHub Copilot | Not approved | Draft |
| 0.7 | 2026-08-03 | Material Draft update: recorded the user-provided requirement for site-to-site and point-to-site VPN support; added ALZ-PLT-113 with verification evidence; added focused VPN input questions and updated risk, traceability, and quality review. | GitHub Copilot | Not approved | Draft |
| 0.8 | 2026-08-03 | Independent-review corrections and user ownership decision: retired non-atomic ALZ-PLT-113; added separately verifiable ALZ-PLT-114 site-to-site VPN connectivity and ALZ-PLT-115 point-to-site VPN access; made EVD-004 the primary direct VPN source; recorded platform-owner technical-input and initial-application-owner authorization accountabilities; updated questions, risk, traceability, lifecycle review dates, and quality review. | GitHub Copilot | Not approved | Draft |
| 0.9 | 2026-08-03 | Independent-review corrections: separated platform-owner VPN technical inputs from initial-application-owner authorization inputs; split technical and authorization/flow risks; added verification-only denied test-candidate questions for each VPN type without establishing security policy; updated VPN requirement dependencies, evidence, traceability, and quality-review limitations. | GitHub Copilot | Not approved | Draft |
| 1.0 | 2026-08-03 | Material Draft update: recorded user-provided containerized-application support input; added solution-neutral ALZ-PLT-116 and the focused QST-015 input question; updated scope, boundaries, both traceability tables, and quality review without selecting a container hosting solution, Azure service, or resource set. | GitHub Copilot | Not approved | Draft |
| 1.1 | 2026-08-03 | Independent-review corrections: made ALZ-PLT-116 verification a complete, evidence-based capability applicability matrix with consumption demonstration for every applicable entry; made ALZ-PLT-114 and ALZ-PLT-115 conditional dependencies only where their respective VPN connectivity is applicable; narrowed QST-015 to container-specific inputs and updated required evidence, traceability, and quality review without selecting a container hosting solution, Azure service, or resource set. | GitHub Copilot | Not approved | Draft |
| 1.2 | 2026-08-03 | Material Draft revision applying the user-provided solution-neutral drafting decision across the active SOR. Retired and replaced ALZ-PLT-101 through ALZ-PLT-104, ALZ-PLT-110, and ALZ-PLT-112 with ALZ-PLT-117 through ALZ-PLT-122; revised ALZ-PLT-105 without changing its normative intent; updated evidence, dependencies, uncertainty registers, traceability, lifecycle detail, retirement links, and quality review. No alternative implementation was selected. | GitHub Copilot | Not approved | Draft |
| 1.3 | 2026-08-03 | Independent-review corrections and user-provided growth reassessment decision: revised ALZ-PLT-116 to a solution-neutral documented applicability assessment and evidence record; revised ALZ-PLT-111 to require a documented trigger-selection basis and reassessment action without a fixed trigger catalogue; added EVD-007 and DEC-002; aligned RSK-002 with QST-004 through QST-008; and reformatted active lifecycle detail as compact field/value blocks. No baseline, evidence, exception, or production-entry approval was made. | GitHub Copilot | Not approved | Draft |
| 1.4 | 2026-08-03 | Independent-review correction: made ALZ-PLT-107's actionable-alert outcome measurable by requiring each alert to identify a response destination, responder, and documented response action; aligned QST-006, required evidence, traceability, active lifecycle detail, and quality review. No alerting service, management process, or response mechanism was selected; all lifecycle links remain unverified and no approval was made. | GitHub Copilot | Not approved | Draft |
| 1.5 | 2026-08-03 | User-provided decision and independent-review corrections: removed the undefined actionable qualifier from ALZ-PLT-107; retained complete configured-alert records for response destination, responder, and documented response action; and set verification to inspection of every configured-alert record plus separate tests of one representative privileged-access change and one representative platform-configuration change, not every configured or documented alert condition. Added EVD-008 and DEC-003 and aligned QST-006, traceability, active lifecycle detail, and quality review. No alerting service, process, or mechanism was selected; all lifecycle links remain unverified and no approval was made. | GitHub Copilot | Not approved | Draft |
| 1.6 | 2026-08-03 | User-provided scope decision: made a dedicated test environment and a dedicated production environment mandatory for the one initial application; aligned scope, ALZ-PLT-118, verification evidence, questions, assumptions, traceability, lifecycle detail, and quality review. No Azure service, topology, isolation mechanism, implementation, baseline approval, or production-entry decision was selected or made. | GitHub Copilot | Not approved | Draft |
| 1.7 | 2026-08-03 | Accepted independent-review corrections: clarified mandatory use of the dedicated test environment, preserved the conditional use of representative non-sensitive test data, clarified ASM-003's impact boundary, and recorded User ownership for the user-provided DEC-004 decision. No baseline or production-entry approval was made. | GitHub Copilot | Not approved | Draft |
| 1.8 | 2026-08-03 | Independent-review wording correction: clarified that any production verification is supplementary and cannot replace verification in the mandatory dedicated test environment. | GitHub Copilot | Not approved | Draft |
| 1.9 | 2026-08-03 | User-provided clarification: recorded User ownership for DEC-003. | GitHub Copilot | Not approved | Draft |
| 2.0 | 2026-08-03 | Independent-review correction: corrected the Quality Review wording to identify DEC-004 ownership correction in v1.7 and DEC-003 ownership correction in v1.9. | GitHub Copilot | Not approved | Draft |
| 2.1 | 2026-08-03 | User-provided updates: confirmed Martyn Fewtrell as the named executive sponsor while preserving the role boundary and no-approval status; clarified that the one initial application in scope is the containerized application and no second application is in scope; recorded partial or still-open answers for QST-002 through QST-009 and QST-015; made evidence retention explicit but solution-neutral through QST-010 and verification/acceptance wording; made QST-011 and QST-012 capture-focused and solution-neutral; and made ALZ-PLT-114 and ALZ-PLT-115 denied-path verification conditional on applicability or documented non-applicability for QST-013 and QST-014. | GitHub Copilot | Not approved | Draft |

Retired 0.3 content retained only to preserve file-provider history; it is not part of the 0.4 Draft.
# Azure Landing Zone for Material Workloads - Statement of Requirements

> Status: Draft
> Version: 0.3
> Date: 2026-08-03
> Baseline and production-entry acceptance authority: Executive sponsor (named human authority; identity not supplied)
> Approval status: Not approved

## Purpose and Decision

- **Problem or opportunity:** The business needs a production-capable Azure foundation for material workloads without assuming an enterprise-scale design or unconfirmed business constraints.
- **Intended outcome:** A governed Azure foundation that can host approved production workloads with defined ownership, security, operational, change, and cost controls.
- **Decision supported:** Whether the Draft requirements and associated discovery outputs are sufficient to authorize a baseline and delivery of the foundation.
- **Success measures:** Required discovery decisions are recorded and approved; all Must requirements have objective evidence; no production workload is accepted until applicable gates are passed.
- **Audience:** Business owner/executive sponsor; future platform, workload, security, operations, and finance owners; any delivery supplier.
- **Scope and time boundary:** This Draft covers an Azure platform foundation for material production workloads. It is based on evidence current to 2026-08-03 and does not approve a design, supplier, budget, region, recovery target, or implementation.

## Scope and Boundaries

**In scope**

- Azure governance boundaries, identity and privileged access, policy, logging and alerting, cost accountability, operational readiness, change governance, and production-entry acceptance.
- Discovery and approval gates for workload, data, recovery, network, region, licensing, support, and cost decisions.
- Platform capabilities needed to support production workloads once their workload-specific requirements are approved.

**Out of scope**

- A workload architecture, Azure region selection, network topology, Azure or Microsoft Entra licence selection, support agreement, supplier selection, budget, regulatory interpretation, and legal or procurement advice.
- Approval of a production deployment, a requirement baseline, a policy definition set, or an implementation design.

**Lifecycle context:** Discovery, controlled design, delivery, verification, acceptance, and operation. Material changes require impact assessment against this Draft's requirements, evidence, and acceptance records.

## Stakeholders and Governance

| Role | Named person or team | Accountability | Approval or escalation authority |
| --- | --- | --- | --- |
| Executive sponsor | Executive sponsor; identity not supplied | Business outcomes, risk appetite, SOR baseline approval, acceptance of requirement evidence, and authorization of production entry | Sole authority to approve the SOR baseline, accept requirement evidence, and authorize production entry after the individual is named and the decision is recorded |
| Platform owner | To be named | Platform configuration and operating model | Escalates unresolved platform risks to sponsor |
| Workload owner | To be named per workload | Workload requirements, data classification, recovery needs | Approves workload evidence for sponsor acceptance |
| Security/privacy/compliance owner | To be named | Applicable control and obligation discovery | Escalates unknown obligations to qualified authority |
| Operations owner | To be named | Runbooks, monitoring, support and recovery operation | Escalates failed operational controls |
| Finance owner | To be named | Cost accountability and budget decisions | Escalates unapproved cost exposure |
| Acceptance authority | Executive sponsor; identity not supplied | Human acceptance of requirement evidence and production-entry evidence | Sole stated authority; no acceptance or production-entry authorization exists until the individual is named and records the decision |

No role above is deemed assigned merely by appearing in this Draft. A supplier or managed service provider, if used, must have responsibilities and access separately recorded; it does not replace business risk ownership.

## Evidence Inventory

| ID | Source | Date/version | Claim supported | Evidence status |
| --- | --- | --- | --- | --- |
| EVD-001 | User-provided input | 2026-08-03 | Target document path and scope: production-capable Azure foundation for material workloads | User-provided |
| EVD-002 | User-provided input | 2026-08-03 | Business owner/executive sponsor is the human authority permitted to approve the SOR baseline | User-provided; identity unresolved |
| EVD-003 | [Azure Landing Zone Guidance for a Small Business](../research/azure-landing-zone-small-business-guidance.md) | Research date 2026-08-03 | Azure landing-zone governance, security, cost, operations, reliability, and change-management practices | Research evidence, not an approved requirement set |
| EVD-004 | User-provided decision | 2026-08-03 | The executive sponsor will accept requirement evidence and authorize production entry, in addition to approving the SOR baseline; the individual remains to be named | User-provided; identity unresolved |

The research's observed facts inform rationale. Its inferences, recommendations, target state, and options are not automatically approved requirements; this Draft selectively translates them into outcome-based requirements.

## Requirement Baseline

All entries are mandatory Draft requirements. `Must` is the priority taxonomy for a condition required before baseline acceptance or production entry. Dependencies identify prerequisite decisions, records, or requirements and do not constitute approval. “Approval record” means a controlled record that identifies the subject, decision, decision-maker name and role, date, and any conditions or expiry. In every requirement metadata entry, the acceptance authority is the executive sponsor; legacy values labelled “Business owner/executive sponsor” mean the executive sponsor and do not identify a named individual.

### ALZ-SOR-001

| Field | Value |
| --- | --- |
| Normative requirement | The business shall complete and record a discovery profile for each material workload before that workload enters production, covering workload owner, data classification, applicable obligations, critical user flows, RTO, RPO, primary and recovery region constraints, connectivity dependencies, licensing, support arrangement, and cost assumptions. |
| Type | Operational |
| Source or rationale | EVD-001, EVD-003; research identifies these as unresolved inputs required for reliable design |
| Priority | Must |
| Owner | Business owner/executive sponsor |
| Status | Draft |
| Dependency | Named platform and workload owners |
| Verification method | Inspection |
| Objective pass criterion | A profile contains all listed fields, an owner for each field, and an unresolved status where a value is not yet known. |
| Required evidence | Workload discovery profile |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-002

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall prevent a material workload from entering production until each discovery-profile field is marked applicable or not applicable and every applicable field has a disposition in an approval record. |
| Type | Delivery |
| Source or rationale | EVD-001, EVD-003 |
| Priority | Must |
| Owner | Executive sponsor |
| Status | Draft |
| Dependency | ALZ-SOR-001, ALZ-SOR-024 |
| Verification method | Inspection |
| Objective pass criterion | The production-entry record links the profile; every field is marked applicable or not applicable; and every applicable field references an approval record. |
| Required evidence | Workload discovery profile, production-entry checklist, and linked approval records |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-003

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall document a governance-boundary record for every production workload that identifies its Azure governance scope, accountable owner, production or nonproduction classification, inherited controls, and the recorded isolation decision. |
| Type | Constraint |
| Source or rationale | EVD-001, EVD-003; Azure management groups and subscriptions provide governance scopes |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-SOR-001, ALZ-SOR-024 |
| Verification method | Inspection |
| Objective pass criterion | Each production workload has one governance-boundary record containing every listed field and an approval record for its isolation decision. |
| Required evidence | Governance-boundary records and approval records |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-004

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall maintain a complete inventory of deployable governance controls, access assignments, monitoring configuration, and cost controls, and shall manage every applicable inventory item through version-controlled infrastructure-as-code before production operation depends on that item. |
| Type | Delivery |
| Source or rationale | EVD-003; research recommends IaC as the platform management system of record |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-SOR-024; source-control service |
| Verification method | Inspection and demonstration |
| Objective pass criterion | The inventory contains every applicable item in each listed configuration category; every applicable inventory item reconciles to its version-controlled source and deployed state; and every reconciliation records peer review and deployment from that source. Sampling may supplement this evidence but cannot be the sole proof. |
| Required evidence | Complete configuration inventory, source revisions, review records, deployment outputs, and item-level source-to-deployed-state reconciliation records |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-005

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall use group-based Azure access assignments for human privileged platform administration, except where an emergency-access record identifies a direct assignment and its recovery purpose. |
| Type | Security |
| Source or rationale | EVD-003; Microsoft RBAC guidance summarized in research |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-SOR-006, ALZ-SOR-024 |
| Verification method | Inspection |
| Objective pass criterion | The privileged-access inventory shows each human privileged assignment is group-based or references an emergency-access record. |
| Required evidence | Privileged-access inventory and emergency-access records |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-006

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall provide an emergency-access recovery procedure for loss of normal administrative access and shall test that procedure before production entry. |
| Type | Security |
| Source or rationale | EVD-003; research identifies emergency access and testing as foundational |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-SOR-005 |
| Verification method | Test |
| Objective pass criterion | A controlled test restores authorized administrative access using the documented procedure without relying on ordinary privileged access. |
| Required evidence | Emergency-access procedure and test record |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-007

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall apply version-controlled governance controls at documented scopes and shall assess their effect before enforcement can block production deployments. |
| Type | Security |
| Source or rationale | EVD-003; policy supports audit and deny effects and research recommends monitored rollout |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-SOR-003, ALZ-SOR-004 |
| Verification method | Demonstration |
| Objective pass criterion | For every blocking control, a nonproduction assessment record identifies scope, tested workload effect, remediation path, and approval to enforce. |
| Required evidence | Policy/control configuration, nonproduction assessment, and enforcement approval record |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-008

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall maintain a time-bounded exception process for governance controls that records owner, business justification, compensating control, expiry date, and review date. |
| Type | Governance |
| Source or rationale | EVD-003; research recommendation |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-SOR-007 |
| Verification method | Inspection |
| Objective pass criterion | Each active exception record contains every required field and no expired exception is treated as active without a renewed approval record. |
| Required evidence | Exception register |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-009

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall collect the control-plane, security, and workload diagnostic information marked applicable in the approved logging disposition for each production workload and make it retrievable by an authorized operator. |
| Type | Operational |
| Source or rationale | EVD-003; research identifies logging, retention, access, and recurring cost validation |
| Priority | Must |
| Owner | Operations owner |
| Status | Draft |
| Dependency | ALZ-SOR-023, ALZ-SOR-024 |
| Verification method | Demonstration |
| Objective pass criterion | For every applicable diagnostic category, a test event is retrievable by an authorized operator from the recorded destination. |
| Required evidence | Logging configuration and retrieval-test records |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-010

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall maintain an alert inventory in which every configured production alert identifies a named response owner, runbook reference, delivery destination, and test result. |
| Type | Operational |
| Source or rationale | EVD-003; research recommends owner and response path for actionable alerts |
| Priority | Must |
| Owner | Operations owner |
| Status | Draft |
| Dependency | ALZ-SOR-018, ALZ-SOR-024 |
| Verification method | Test |
| Objective pass criterion | Each alert inventory entry contains every listed field, and a representative test for each alert type records delivery to its configured destination. |
| Required evidence | Alert inventory, runbooks, and alert-test records |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-011

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall prevent a stateful production workload from entering production until its approved recovery objective, backup method, retention, restore-test frequency, and accountable owner are recorded. |
| Type | Reliability |
| Source or rationale | EVD-003; reliability targets must derive from business requirements |
| Priority | Must |
| Owner | Workload owner |
| Status | Draft |
| Dependency | ALZ-SOR-001 |
| Verification method | Inspection |
| Objective pass criterion | The workload recovery record contains each required field and is approved by the workload owner. |
| Required evidence | Workload recovery record |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-012

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall demonstrate restoration of data for each stateful production workload using its approved backup and recovery method before acceptance of that workload for production operation. |
| Type | Reliability |
| Source or rationale | EVD-003; research requires documented and tested recovery plans |
| Priority | Must |
| Owner | Operations owner |
| Status | Draft |
| Dependency | ALZ-SOR-011 |
| Verification method | Test |
| Objective pass criterion | The restore test record identifies the workload, backup source, test date, restored outcome, observed recovery result, and any approved variance from the recovery objective. |
| Required evidence | Restore-test record and variance approval where applicable |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-013

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall provide cost accountability for each production workload through a recorded owner, cost allocation approach, budget, and alert recipients before production entry. |
| Type | Cost |
| Source or rationale | EVD-003; research recommends accountability, tagging, budgets, and alerts |
| Priority | Must |
| Owner | Finance owner |
| Status | Draft |
| Dependency | ALZ-SOR-001; named finance owner |
| Verification method | Inspection and demonstration |
| Objective pass criterion | The workload cost record identifies all required fields, and a representative actual or forecast budget alert is delivered to the recorded recipients. |
| Required evidence | Cost allocation record, budget configuration, and alert-test record |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-014

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall record and review each production workload's cost assumptions before production entry, including the assumptions needed to estimate its Azure consumption and operational monitoring cost. |
| Type | Cost |
| Source or rationale | EVD-003; research recommends estimates and explicit assumption sets |
| Priority | Must |
| Owner | Finance owner |
| Status | Draft |
| Dependency | ALZ-SOR-001 |
| Verification method | Analysis |
| Objective pass criterion | A dated estimate identifies its workload, assumptions, currency, owner, and review outcome; any unknown assumption is recorded as an open question or approved contingency. |
| Required evidence | Cost estimate and review record |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-015

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall use a documented, peer-reviewed change process for production changes to privileged access, governance controls, network controls, backup/recovery configuration, and production data access. |
| Type | Change |
| Source or rationale | EVD-003; research identifies these as high-risk changes |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-SOR-004; named operations owner |
| Verification method | Inspection |
| Objective pass criterion | A sampled change record for each applicable change category includes peer review, impact assessment, implementation result, and rollback or recovery disposition. |
| Required evidence | Change records and linked configuration revisions |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-016

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall record the approved connectivity and exposure requirements for each production workload before selecting or deploying its network topology. |
| Type | Interface |
| Source or rationale | EVD-003; topology depends on internal/public classification and connectivity requirements |
| Priority | Must |
| Owner | Workload owner |
| Status | Draft |
| Dependency | ALZ-SOR-001 |
| Verification method | Inspection |
| Objective pass criterion | The workload network record identifies internal/public exposure classification, required data flows, external dependencies, address-space considerations where applicable, and approving owner. |
| Required evidence | Workload network record |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-017

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall require explicit recorded approval for every production workload resource with public network exposure. |
| Type | Security |
| Source or rationale | EVD-003; research recommends explicit approval for internet-facing resources |
| Priority | Must |
| Owner | Security/privacy/compliance owner |
| Status | Draft |
| Dependency | ALZ-SOR-016; named security/privacy/compliance owner |
| Verification method | Inspection |
| Objective pass criterion | The public-exposure inventory has an approval record for every listed resource, or the inventory records no publicly exposed resources. |
| Required evidence | Public-exposure inventory and approvals |
| Acceptance authority | Business owner/executive sponsor |

### ALZ-SOR-018

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall maintain one current controlled runbook for each of the following scenarios before supporting production workloads: privileged-access emergency, credential compromise, service outage, backup restore, failed deployment recovery, and cost anomaly response. |
| Type | Operational |
| Source or rationale | EVD-003; research identifies these runbook scenarios |
| Priority | Must |
| Owner | Operations owner |
| Status | Draft |
| Dependency | ALZ-SOR-006, ALZ-SOR-010, ALZ-SOR-012, ALZ-SOR-024 |
| Verification method | Inspection |
| Objective pass criterion | The runbook register contains one runbook for every listed scenario; each identifies an owner, controlled location, review date, escalation path, and current status. |
| Required evidence | Runbook register and runbook set |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-019

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall maintain an approved operational-review schedule that assigns an owner, recurrence, and next review date to access, security posture, backup/recovery evidence, cost, control exceptions, and unresolved operational risks. |
| Type | Operational |
| Source or rationale | EVD-003; research recommends periodic operational reviews |
| Priority | Must |
| Owner | Operations owner |
| Status | Draft |
| Dependency | ALZ-SOR-008, ALZ-SOR-012, ALZ-SOR-013, ALZ-SOR-021, ALZ-SOR-024 |
| Verification method | Inspection and operational evidence |
| Objective pass criterion | The schedule contains every listed review area and its required fields; for every due review period after production entry, a retained review record identifies the date, reviewer, findings, and disposition. |
| Required evidence | Approved operational-review schedule and review records |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-020

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall retain a production-entry acceptance record for each material workload before it enters production. |
| Type | Delivery |
| Source or rationale | EVD-001, EVD-003, EVD-004 |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-SOR-001 through ALZ-SOR-019 and ALZ-SOR-021 through ALZ-SOR-024, as applicable |
| Verification method | Inspection |
| Objective pass criterion | The record identifies the workload; applicability decisions; evidence references for every applicable requirement; open risks and their disposition; approved exceptions; the named executive sponsor; decision date; and the sponsor's recorded authorization to enter production. |
| Required evidence | Production-entry acceptance record |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-021

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall retain an approval record and a completed review record for each human privileged access assignment before production entry and at each recurrence defined in the approved operational-review schedule. |
| Type | Security |
| Source or rationale | EVD-003; Microsoft RBAC guidance summarized in research |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-SOR-005, ALZ-SOR-019, ALZ-SOR-024 |
| Verification method | Inspection |
| Objective pass criterion | The privileged-access inventory links every assignment to an approval record and the latest required review record; each review records reviewer, date, findings, and removal or approved exception disposition. |
| Required evidence | Privileged-access inventory, approval records, and access-review records |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-022

| Field | Value |
| --- | --- |
| Normative requirement | Before human privileged access is used in production, the foundation shall require authentication assurance such that compromise of one authentication factor alone cannot authorize that access, and shall retain an approved authentication-assurance decision that identifies the human privileged access population, accountable decision-maker, authentication assurance controls, evidence that the controls are enabled or otherwise operating, residual risks, and review trigger. |
| Type | Security |
| Source or rationale | EVD-003; research recommends MFA but states that exact Entra configuration and licensing require validation |
| Priority | Must |
| Owner | Security/privacy/compliance owner |
| Status | Draft |
| Dependency | ALZ-SOR-001, ALZ-SOR-024; licensing and configuration decision in QST-007 |
| Verification method | Inspection and test |
| Objective pass criterion | The decision record contains every listed field, identifies the exact selected configuration as a decision, and links evidence for every identified control; test evidence demonstrates that possession or compromise of any one authentication factor alone does not authorize human privileged access to the production-capable foundation; it does not rely on an unrecorded licensing or configuration assumption. |
| Required evidence | Authentication-assurance decision, approval record, control-operation evidence, and authentication-factor compromise test record |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-023

| Field | Value |
| --- | --- |
| Normative requirement | The foundation shall retain an approved logging disposition for each production workload that states, for each control-plane, security, and workload diagnostic category, whether it is applicable and, when applicable, its destination, retention, authorized access, and cost disposition. |
| Type | Operational |
| Source or rationale | EVD-003; research identifies logging, retention, access, and recurring cost validation |
| Priority | Must |
| Owner | Operations owner |
| Status | Draft |
| Dependency | ALZ-SOR-001, ALZ-SOR-024 |
| Verification method | Inspection |
| Objective pass criterion | The logging disposition lists all three diagnostic categories and contains every listed field for each applicable category. |
| Required evidence | Approved logging disposition |
| Acceptance authority | Executive sponsor |

### ALZ-SOR-024

| Field | Value |
| --- | --- |
| Normative requirement | Before SOR baseline acceptance or production-entry acceptance, the business shall record the named individual assigned to the executive sponsor, platform owner, workload owner, security/privacy/compliance owner, operations owner, and finance owner roles, including each individual's acceptance of the assigned accountability. |
| Type | Governance |
| Source or rationale | EVD-003, EVD-004 |
| Priority | Must |
| Owner | Executive sponsor |
| Status | Draft |
| Dependency | QST-001; owner appointments |
| Verification method | Inspection |
| Objective pass criterion | The accountability register identifies a named individual for every listed role and includes a dated acceptance record for each assignment. |
| Required evidence | Accountability register and role-acceptance records |
| Acceptance authority | Executive sponsor |

## Verification and Acceptance

- **Verification environments and data constraints:** Nonproduction environments and representative non-sensitive test data must be used where practical. Any exception must be recorded in the applicable verification evidence.
- **Evidence location:** The platform owner must identify the controlled repository or record system before baseline acceptance; this Draft does not designate one.
- **Acceptance process:** The responsible owner supplies required evidence. The platform owner assembles the traceability and production-entry record. Only the named executive sponsor may approve the SOR baseline, accept requirement evidence, or authorize production entry. Recording the role without naming the individual is not an acceptance decision.
- **Exceptions:** An unmet requirement remains Draft and visible. Only a recorded, time-bounded exception with compensating control may be considered for acceptance; this Draft does not grant any exception.

## Assumptions

| ID | Statement | Owner | Impact if false | Review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| ASM-001 | Azure is the selected cloud platform for the scope stated by the user. | Business owner/executive sponsor | SOR scope and requirements require revision. | Change of cloud-platform decision | Open |
| ASM-002 | Material workloads will require a production-capable foundation, but their inventory and criticality are not yet supplied. | Business owner/executive sponsor | Scope, control depth, and acceptance gates may change. | Completion of ALZ-SOR-001 | Open |
| ASM-003 | The executive sponsor will name the required accountable owners before SOR baseline acceptance and production entry. | Executive sponsor | Requirements cannot be accepted or operated. | Before SOR baseline acceptance | Open |

## Risks

| ID | Risk | Owner | Impact | Treatment or review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| RSK-001 | Unknown regulatory, privacy, or data-residency obligations could require controls outside this Draft. | Security/privacy/compliance owner | Inadequate controls or delayed delivery | Complete obligation discovery under ALZ-SOR-001; escalate interpretation to qualified authority. | Open |
| RSK-002 | Unapproved recovery objectives could create a foundation unable to meet business needs. | Workload owner | Service or data loss beyond business tolerance | Set and approve recovery objectives before production entry under ALZ-SOR-011. | Open |
| RSK-003 | Unknown licensing, support, or cost arrangements could make proposed controls unavailable or unaffordable. | Finance owner | Rework, unplanned spend, or unsupported operation | Complete discovery profile and cost review before production entry. | Open |
| RSK-004 | Undocumented connectivity requirements could lead to unsuitable network controls or exposure. | Workload owner | Security, availability, or integration failure | Complete and approve ALZ-SOR-016 before topology selection. | Open |

## Issues, Questions, and Decisions

| ID | Type | Statement | Owner | Due date or trigger | Status |
| --- | --- | --- | --- | --- | --- |
| QST-001 | Question | What is the name of the executive sponsor who may approve the SOR baseline, accept requirement evidence, and authorize production entry? | Executive sponsor | Before SOR baseline acceptance | Open |
| QST-002 | Question | Which material workloads, data classifications, and applicable obligations are in scope? | Workload owner | Before workload design | Open |
| QST-003 | Question | What RTO, RPO, availability expectations, and support hours apply to each workload? | Workload owner | Before production entry | Open |
| QST-004 | Question | Which primary/recovery regions, data-residency constraints, connectivity dependencies, and public exposure needs apply? | Workload owner | Before topology or region selection | Open |
| QST-005 | Question | Which Azure agreement, Microsoft Entra licensing, support arrangement, and cost constraints are available? | Finance owner | Before control and service selection | Open |
| QST-006 | Question | Will a managed service provider be used, and what responsibilities and access will be assigned? | Business owner/executive sponsor | Before supplier access or operational handover | Open |
| QST-007 | Question | Which authentication-assurance controls, Microsoft Entra licensing, and exact configuration will be approved for human privileged access? | Security/privacy/compliance owner | Before use of human privileged access in production | Open |
| DEC-001 | Decision | No implementation design, region, topology, licensing, support plan, supplier, cost limit, or recovery target is selected by this Draft. | Business owner/executive sponsor | Revisit following discovery | Draft |

## Traceability

All lifecycle links below are **Unverified for Draft**. They are required before SOR baseline acceptance where stated, and before production-entry acceptance for any applicable workload. No row is evidence of completed delivery, verification, acceptance, or an approved exception.

| SOR ID | Source or rationale | Design decision or rationale | Specification, work item, or configuration | Build, change, or deployment record | Verification evidence | Acceptance status or approved exception | Last reviewed |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ALZ-SOR-001 | EVD-001, EVD-003 | Unverified for Draft; discovery profile required before design | Unverified for Draft; required before production entry | Unverified for Draft | Unverified for Draft; profile required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-002 | EVD-001, EVD-003 | Unverified for Draft; production-entry gate | Unverified for Draft; required before production entry | Unverified for Draft | Unverified for Draft; checklist and approvals required before production entry | Unverified for Draft; executive-sponsor authorization required before production entry | 2026-08-03 |
| ALZ-SOR-003 | EVD-001, EVD-003 | Unverified for Draft; governance-boundary decision pending | Unverified for Draft; required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-004 | EVD-003 | Unverified for Draft; IaC approach pending | Unverified for Draft; required before production entry | Unverified for Draft | Unverified for Draft; demonstration required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-005 | EVD-003 | Unverified for Draft; access model pending | Unverified for Draft; required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-006 | EVD-003 | Unverified for Draft; emergency-access recovery pending | Unverified for Draft; procedure required before production entry | Unverified for Draft | Unverified for Draft; controlled test required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-007 | EVD-003 | Unverified for Draft; control rollout pending | Unverified for Draft; configuration required before production entry | Unverified for Draft | Unverified for Draft; nonproduction assessment required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-008 | EVD-003 | Unverified for Draft; exception process pending | Unverified for Draft; register required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-009 | EVD-003 | Unverified for Draft; observability decision pending | Unverified for Draft; configuration required before production entry | Unverified for Draft | Unverified for Draft; retrieval demonstration required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-010 | EVD-003 | Unverified for Draft; alerting decision pending | Unverified for Draft; configuration required before production entry | Unverified for Draft | Unverified for Draft; alert test required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-011 | EVD-003 | Unverified for Draft; recovery decision pending | Unverified for Draft; record required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-012 | EVD-003 | Unverified for Draft; recoverability evidence pending | Unverified for Draft; implementation required before production entry | Unverified for Draft | Unverified for Draft; restore test required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-013 | EVD-003 | Unverified for Draft; cost-control decision pending | Unverified for Draft; configuration required before production entry | Unverified for Draft | Unverified for Draft; budget-alert test required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-014 | EVD-003 | Unverified for Draft; cost estimate pending | Unverified for Draft; estimate required before production entry | Unverified for Draft | Unverified for Draft; analysis required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-015 | EVD-003 | Unverified for Draft; change process pending | Unverified for Draft; process required before production entry | Unverified for Draft | Unverified for Draft; sampled records required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-016 | EVD-003 | Unverified for Draft; connectivity decision pending | Unverified for Draft; network record required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-017 | EVD-003 | Unverified for Draft; public-exposure decision pending | Unverified for Draft; inventory required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-018 | EVD-003 | Unverified for Draft; runbook set pending | Unverified for Draft; runbooks required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-019 | EVD-003 | Unverified for Draft; operational-review schedule pending | Unverified for Draft; schedule required before production entry | Unverified for Draft | Unverified for Draft; review records required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-020 | EVD-001, EVD-003, EVD-004 | Unverified for Draft; human production-entry acceptance | Unverified for Draft; acceptance record required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; named executive-sponsor authorization required before production entry | 2026-08-03 |
| ALZ-SOR-021 | EVD-003 | Unverified for Draft; privileged-access review decision pending | Unverified for Draft; required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-022 | EVD-003 | Unverified for Draft; authentication configuration decision pending | Unverified for Draft; required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-023 | EVD-003 | Unverified for Draft; logging disposition pending | Unverified for Draft; required before production entry | Unverified for Draft | Unverified for Draft; inspection required before production entry | Unverified for Draft; executive-sponsor acceptance required before production entry | 2026-08-03 |
| ALZ-SOR-024 | EVD-003, EVD-004 | Unverified for Draft; accountable roles pending | Unverified for Draft; accountability register required before baseline acceptance | Unverified for Draft | Unverified for Draft; role-acceptance records required before baseline acceptance | Unverified for Draft; named executive-sponsor acceptance required before baseline acceptance and production entry | 2026-08-03 |

## Quality Review

| Check | Result | Finding |
| --- | --- | --- |
| Draft status and approval authority are recorded | Pass with limitation | The authority role is recorded; the human's identity is unresolved in QST-001. |
| Decision, audience, scope, time boundary, and evidence are recorded | Pass | Evidence status distinguishes user input from research evidence. |
| Facts, recommendations, and unknowns are distinct | Pass | Research is explicitly non-approving evidence; unknowns are in separate registers and gates. |
| Assumptions, risks, issues, questions, and decisions are separate and owned | Pass with limitation | Several accountable role identities remain unassigned. |
| Mandatory requirements have complete metadata | Pass | ALZ-SOR-001 through ALZ-SOR-024 include all required fields and identify the executive sponsor as acceptance authority. |
| Requirements are atomic, outcome-oriented, and verifiable | Pass with limitation | The second independent review findings for ALZ-SOR-004 and ALZ-SOR-022 are resolved: ALZ-SOR-004 requires complete item-level inventory reconciliation, and ALZ-SOR-022 has an outcome and test that prevent authorization from compromise of one factor alone. Exact authentication configuration and Entra licensing remain open in QST-007. |
| Prescription is evidence-backed or avoided | Pass | Azure is within user-supplied scope; implementation choices are not selected. |
| Scope, security, interfaces, operations, lifecycle, cost, and acceptance coverage | Pass with limitation | Actual regulatory, privacy, and compliance controls cannot be determined until discovery. |
| Material traceability is complete | Unverified for Draft | Lifecycle links remain planned or blank. Requirement-specific delivery, verification, and executive-sponsor acceptance links are required before baseline acceptance and/or production entry. |

**Unverified before stakeholder review:** QST-001 through QST-007; assignment and recorded acceptance of the executive sponsor, platform, workload, security/privacy/compliance, operations, and finance owners; all lifecycle, delivery, verification, and executive-sponsor acceptance evidence. ALZ-SOR-024 is a mandatory gate before baseline acceptance and production-entry acceptance. These are open Draft items, not approvals or accepted risks.

## Approval and Change History

| Version | Date | Change summary | Drafted by | Approved by | Approval status |
| --- | --- | --- | --- | --- | --- |
| 0.1 | 2026-08-03 | Initial controlled Draft based on EVD-001 through EVD-003 | GitHub Copilot | Not approved | Draft |
| 0.2 | 2026-08-03 | Draft correction: executive-sponsor acceptance and production-entry authority recorded; access/logging obligations split; authentication assurance and named-role gates added; testability and traceability corrected using EVD-004 | GitHub Copilot | Not approved | Draft |
| 0.3 | 2026-08-03 | Draft correction resolving the second independent review: ALZ-SOR-004 now requires complete inventory and item-level reconciliation to source and deployed state; ALZ-SOR-022 now prevents authorization from compromise of one authentication factor alone and correctly retains QST-007 for Entra licensing and configuration. | GitHub Copilot | Not approved | Draft |
-->

# Shared Foundation and Shared Resources - Statement of Requirements

> Status: Draft
> Version: 3.3
> Date: 2026-08-04
> Baseline, evidence, exception, and production-entry authority: Martyn Fewtrell (executive sponsor); no approval or authorization has been recorded
> Approval status: Not approved

## Purpose and Decision

- **Problem or opportunity:** The business requires a controlled shared foundation and shared resources for future use without establishing a Platform Engineering function or assuming application responsibilities.
- **Intended outcome:** A controlled, operable shared foundation that supports future shared use, maintains clear responsibility boundaries, and has controlled definition and management.
- **Decision supported:** Whether this Draft accurately defines the required shared-foundation outcomes and boundaries for stakeholder review.
- **Success measures:** Shared-foundation requirements have objective evidence; application onboarding, deployment, and cost management remain application responsibilities; shared-resource scope remains unresolved rather than assumed.
- **Audience:** Executive sponsor; prospective shared-foundation owner; current and future application owners; delivery team or service provider.
- **Scope and time boundary:** This Draft covers a shared foundation and shared resources intended for future shared use. It reflects evidence available on 2026-08-04 and does not approve a technical design, implementation, baseline, exception, or production entry.

## Scope and Boundaries

**In scope:** Shared-foundation responsibility boundaries; controlled human privileged access and authentication resilience; controlled definition and management; activity visibility and alerting; reassessment for future shared use; and shared resources for authorized shared use once their scope and responsibilities are documented.

**Out of scope:** Platform Engineering; application onboarding, deployment, cost management, architecture, operation, recovery, and application-specific connectivity; and selection of shared-resource types, users, identities, catalogue, architecture, configurations, delivery methods, management mechanisms, delivery plans, regions, budgets, licences, providers, topology, or implementation.

**Boundary:** The shared foundation provides shared outcomes and shared resources only within their documented scope and responsibilities. Each application remains responsible for its onboarding, deployment, and cost management. The shared-resource scope must not be inferred from this Draft.

## Stakeholders and Governance

| Role | Named person or team | Accountability | Approval or escalation authority |
| --- | --- | --- | --- |
| Executive sponsor | Martyn Fewtrell | May authorize each shared resource's intended users, approve the SOR baseline, accept requirement evidence, approve exceptions, and authorize production entry only through required records and conditions. | Only Martyn Fewtrell may perform those actions. |
| Shared-foundation owner | To be named | Delivers and manages shared-foundation outcomes, maintains evidence, and escalates unresolved shared-resource scope. | Escalates scope gaps and unresolved dependencies to the executive sponsor. |
| Application owner | To be named for each application | Owns application onboarding, deployment, cost management, and application-specific requirements. | Escalates a need that may require a shared-foundation scope change. |

## Evidence Inventory

| ID | Source | Date/version | Claim supported | Evidence status |
| --- | --- | --- | --- | --- |
| EVD-001 | User-provided input | 2026-08-03 | A foundation is required and Martyn Fewtrell is the named executive sponsor and approval authority by role. | User-provided; sponsor authority remains active |
| EVD-002 | [Small Business Foundation Guidance](../research/azure-landing-zone-small-business-guidance.md) | Research date 2026-08-03 | Nonbinding research guidance on foundation capabilities, dependencies, and growth triggers. | Research evidence; observations and recommendations are distinct |
| EVD-003 | User-provided scope refinement | 2026-08-03 | Previous focus on one initial application. | User-provided; superseded for active scope by EVD-011 |
| EVD-004 | User-provided connectivity and ownership input | 2026-08-03 | Previous application-specific VPN input. | User-provided; superseded for active scope by EVD-011 |
| EVD-005 | User-provided containerized application clarification | 2026-08-03 | Previous one-initial-containerized-application scope. | User-provided; superseded for active scope by EVD-011 |
| EVD-006 | User-provided drafting decision | 2026-08-03 | Requirements must be outcome-oriented and solution-neutral. | User-provided; active |
| EVD-007 | User-provided growth reassessment decision | 2026-08-03 | Growth reassessment requires a documented trigger-selection basis and reassessment action. | User-provided; active |
| EVD-008 | User-provided alert-verification decision | 2026-08-03 | Representative privileged-access and foundation-change alert verification. | User-provided; active with scope revised by EVD-011 |
| EVD-009 | User-provided scope decision | 2026-08-03 | Previous dedicated application test and production environment scope. | User-provided; superseded for active scope by EVD-011 |
| EVD-010 | User-provided evidence-retention decision | 2026-08-03 | Controlled foundation evidence and acceptance records must be retained without prescribing retention implementation. | User-provided; active |
| EVD-011 | User-provided material scope change | 2026-08-04 | A shared foundation and shared resources are required for future shared use; this is not Platform Engineering; application onboarding, deployment, and cost management remain application responsibilities. | User-provided; primary direct source for the active scope |
| EVD-012 | User-provided decision | 2026-08-04 | Option 1 selected: shared resources are required for authorized shared use after their scope and responsibilities are documented. | User-provided; primary direct source for ALZ-PLT-126 |
| EVD-013 | User-provided final-review decision | 2026-08-04 | The executive sponsor authorizes each shared resource's intended users; the scope-and-responsibility record identifies those users, authorization basis/evidence is retained, and verification demonstrates shared use only for users so authorized. | User-provided; primary direct source for ALZ-PLT-126 authorization and verification revision |

Research recommendations and superseded historical inputs are not active requirements or approvals. The direct user-provided technical direction is retained solely as external technical-design dependency TD-001; it is not selected or prescribed by this SOR.

## External Technical-Design Dependencies

| ID | Supplied technical-design information | Owner | Required disposition | Status |
| --- | --- | --- | --- | --- |
| TD-001 | User-provided technical-design input names Azure, Landing Zone, infrastructure-as-code, and centrally hosted shared resources as the intended technical direction. | Executive sponsor | Record any technical-design decision outside this SOR and confirm it supports, rather than changes, the active outcome requirements. | Open; not an SOR requirement or approval |

## Requirement Baseline

All entries are mandatory Draft requirements. Dependencies are open questions or linked requirements, not approvals. Martyn Fewtrell is the named executive sponsor and acceptance authority by role; this Draft records no approval or authorization.

### ALZ-PLT-127
| Field | Value |
| --- | --- |
| Normative requirement | The shared foundation shall provide controlled human privileged access and an independently usable recovery access path that can restore authorized administration when normal privileged access is unavailable. |
| Type | Identity and access |
| Source or rationale | EVD-002, EVD-006, EVD-011 |
| Priority | Must |
| Owner | Shared-foundation owner |
| Status | Draft; replacement for materially changed ALZ-PLT-119 |
| Dependency | QST-004 |
| Verification method | Inspection and test |
| Objective pass criterion | The privileged-access inventory identifies each human administrator, authorization basis, and purpose; a controlled test restores authorized administration without normal privileged access. |
| Required evidence | Privileged-access inventory, recovery-access record, and recovery test record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-128
| Field | Value |
| --- | --- |
| Normative requirement | Before human privileged access is used for shared-foundation administration, the shared foundation shall protect that access such that compromise of one authentication factor alone cannot authorize it. |
| Type | Identity security |
| Source or rationale | EVD-002, EVD-006, EVD-011 |
| Priority | Must |
| Owner | Shared-foundation owner |
| Status | Draft; replacement for materially changed ALZ-PLT-120 |
| Dependency | QST-004 |
| Verification method | Inspection and test |
| Objective pass criterion | Test evidence demonstrates that compromise of one authentication factor alone does not authorize shared-foundation administration. |
| Required evidence | Privileged-access record, authentication-protection evidence, and authentication-factor test record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-125
| Field | Value |
| --- | --- |
| Normative requirement | The shared foundation shall maintain controlled records for each applicable shared-foundation responsibility that reconcile its agreed intended state and observed state before it supports production use. |
| Type | Controlled definition and management |
| Source or rationale | EVD-006, EVD-011; retains the solution-neutral outcome needed for controlled definition and management without selecting a technical delivery method. |
| Priority | Must |
| Owner | Shared-foundation owner |
| Status | Draft; new ID replacing the materially changed ALZ-PLT-121 outcome |
| Dependency | QST-005, TD-001 |
| Verification method | Inspection and demonstration |
| Objective pass criterion | The controlled record identifies every applicable shared-foundation responsibility; each record links its agreed intended state and observed state; reconciliation records identify mismatches and disposition; and a representative update demonstrates that the record can be maintained. |
| Required evidence | Controlled responsibility records, observed-state records, reconciliation records, and representative update demonstration record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-129
| Field | Value |
| --- | --- |
| Normative requirement | The shared foundation shall provide alerts for privileged-access and shared-foundation changes, and each configured alert shall identify a response destination, responder, and documented response action. |
| Type | Alerting |
| Source or rationale | EVD-002, EVD-008, EVD-011 |
| Priority | Must |
| Owner | Shared-foundation owner |
| Status | Draft; replacement for materially changed ALZ-PLT-107 |
| Dependency | ALZ-PLT-124, QST-006 |
| Verification method | Test and inspection |
| Objective pass criterion | The configured-alert record identifies the response destination, responder, and documented response action for every configured alert. Separate tests show one representative privileged-access change and one representative shared-foundation change each produce an alert at its identified destination. |
| Required evidence | Configured-alert record and two representative alert test records |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-130
| Field | Value |
| --- | --- |
| Normative requirement | The shared foundation shall maintain a documented growth reassessment record that states the trigger-selection basis and reassessment action for future shared use. |
| Type | Evolution |
| Source or rationale | EVD-002, EVD-007, EVD-011 |
| Priority | Must |
| Owner | Shared-foundation owner |
| Status | Draft; replacement for materially changed ALZ-PLT-111 |
| Dependency | QST-016 |
| Verification method | Inspection |
| Objective pass criterion | The growth reassessment record states the basis used to select its triggers and the reassessment action for each trigger, without specifying a future implementation. |
| Required evidence | Growth reassessment record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-123
| Field | Value |
| --- | --- |
| Normative requirement | The shared foundation shall maintain documented boundaries that distinguish shared-foundation responsibilities, shared-resource responsibilities, and application responsibilities. |
| Type | Responsibility boundaries |
| Source or rationale | EVD-006, EVD-011 |
| Priority | Must |
| Owner | Shared-foundation owner |
| Status | Draft; new ID because the prior initial-application placement intent materially changed |
| Dependency | QST-016 |
| Verification method | Inspection |
| Objective pass criterion | The boundary record identifies the shared-foundation responsibility, documented shared-resource responsibility for each defined shared resource, and application responsibility; it assigns application onboarding, deployment, and cost management to applications. |
| Required evidence | Responsibility-boundary record and shared-resource scope record |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-124
| Field | Value |
| --- | --- |
| Normative requirement | The shared foundation shall collect and make retrievable its activity information required to investigate shared-foundation changes and privileged-access events. |
| Type | Observability |
| Source or rationale | EVD-002, EVD-006, EVD-011 |
| Priority | Must |
| Owner | Shared-foundation owner |
| Status | Draft; new ID because the prior application-diagnostic intent materially changed |
| Dependency | QST-006 |
| Verification method | Demonstration |
| Objective pass criterion | A representative shared-foundation activity and a representative privileged-access event are retrievable by an authorized shared-foundation operator. |
| Required evidence | Shared-foundation activity-information record and retrieval test records |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

### ALZ-PLT-126
| Field | Value |
| --- | --- |
| Normative requirement | The shared foundation shall provide each defined shared resource only for use by intended users identified in that resource's documented scope-and-responsibility record and authorized by the executive sponsor. |
| Type | Shared-resource provision |
| Source or rationale | EVD-012, EVD-013; user-provided option 1 and final-review decisions. |
| Priority | Must |
| Owner | Shared-foundation owner |
| Status | Draft; new ID |
| Dependency | ALZ-PLT-123, QST-016 |
| Verification method | Inspection and demonstration |
| Objective pass criterion | For every defined shared resource, the scope-and-responsibility record exists before provision and identifies its intended users; the executive sponsor's authorization basis or evidence for those intended users is retained; and shared-use verification demonstrates use only by intended users covered by that retained authorization basis or evidence. |
| Required evidence | Defined shared-resource scope-and-responsibility record identifying intended users, retained executive-sponsor authorization basis or evidence, and shared-use verification record for each defined resource |
| Acceptance authority | Martyn Fewtrell (executive sponsor) |

## Verification and Acceptance

- **Verification conditions:** Verification shall use controlled, representative conditions appropriate to the requirement. No application onboarding, deployment, cost-management, or application-specific verification is required by this Draft.
- **Evidence retention:** Controlled shared-foundation evidence and acceptance records shall be retained. This Draft does not select the retention implementation; QST-010 remains open.
- **Acceptance approach:** The shared-foundation owner assembles requirement evidence. The executive sponsor's authorization of intended users for a shared resource is distinct from acceptance of requirement evidence. Only Martyn Fewtrell may authorize intended users, approve the SOR baseline, accept evidence, approve an exception, or authorize production entry; each action requires its respective records and conditions. This Draft records none of those actions.

## Assumptions

| ID | Statement | Owner | Impact if false | Review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| ASM-004 | Shared resources will be used across future applications, but their types, users, catalogue, identities, delivery plan, and applicable obligations are not yet defined. | Executive sponsor | Scope, responsibilities, evidence, and affected requirements may require revision; no resource type or obligation may be assumed. | A shared-resource scope, user group, catalogue, identity, delivery plan, or obligation is proposed or recorded | Open |

## Risks

| ID | Risk | Owner | Impact | Treatment or review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| RSK-002 | Unknown capabilities, constraints, or unresolved shared-foundation and shared-resource boundaries could constrain required outcomes. | Shared-foundation owner | Rework, ambiguity, or unavailable capability. | Resolve QST-004 through QST-006 and QST-016 before affected technical-design work. | Open |
| RSK-003 | Future shared use could exceed the initial shared-foundation scope or operational model. | Shared-foundation owner | Cost, security, or operability degradation. | Evaluate ALZ-PLT-130 when a documented trigger occurs. | Open |
| RSK-005 | An undefined shared-resource scope, intended-user authorization, or applicable obligation could cause application responsibilities to be incorrectly transferred to the shared foundation, use beyond authorized users, or an obligation to be left unaddressed. | Executive sponsor | Scope creep, unclear accountability, use beyond authorized users, unverified outcomes, or unmet applicable obligations. | Resolve QST-016 before providing a shared resource or accepting evidence for ALZ-PLT-123 or ALZ-PLT-126. | Open |

## Issues, Questions, and Decisions

| ID | Type | Statement | Owner | Due date or trigger | Status |
| --- | --- | --- | --- | --- | --- |
| QST-001 | Question | Martyn Fewtrell is the named executive sponsor who alone may approve the SOR baseline, accept requirement evidence, approve exceptions, and authorize production entry. This records authority identity only, not an approval or authorization. | Executive sponsor | Resolved by user-provided input; action-specific records and conditions remain required | Resolved |
| QST-004 | Question | What technical-design input will establish controlled human privileged access, recovery access, and protection against authorization by compromise of one authentication factor? | Shared-foundation owner | Before ALZ-PLT-127 and ALZ-PLT-128 technical-design work | Open |
| QST-005 | Question | What external technical-design approach will support the controlled records and reconciliation required by ALZ-PLT-125? It is not selected by this Draft. | Shared-foundation owner | Before ALZ-PLT-125 technical-design work | Open |
| QST-006 | Question | Which shared-foundation activity categories, configured alert conditions, response destinations, responders, response actions, and representative verification conditions apply? This is a technical-design dependency and does not include application diagnostics. | Shared-foundation owner | Before ALZ-PLT-129 and ALZ-PLT-124 technical-design work | Open |
| QST-010 | Question | Which controlled record system, repository, or retained record set will hold required shared-foundation evidence and acceptance records? This Draft does not prescribe the retention implementation. | Shared-foundation owner | Before evidence acceptance | Open |
| QST-016 | Question | For each defined shared resource, what scope and responsibility boundaries apply; which intended users are in scope; what executive-sponsor authorization basis or evidence is retained for those users; and which applicable quality, security/privacy, operational-support, recovery/lifecycle, interface, evidence, and acceptance obligations apply? Resource types, users, identities, a catalogue, delivery plan, authorization mechanism or timing, obligation values, and policies must not be inferred before an answer is recorded. | Executive sponsor | Before providing a shared resource or accepting evidence for ALZ-PLT-123 or ALZ-PLT-126; review on any proposed shared-resource scope, user group, catalogue, identity, delivery plan, or applicable obligation | Open |
| QST-017 | Question | What decision and accountable owner will record the supplied Azure, Landing Zone, and infrastructure-as-code technical direction outside this SOR? | Executive sponsor | Before technical-design work under TD-001 | Open |
| DEC-001 | Decision | The active Draft scope is a shared foundation and shared resources for future shared use, not Platform Engineering. Application onboarding, deployment, and cost management remain application responsibilities. | Executive sponsor | Revisit on material scope change | Draft; user-provided input recorded, not approved |
| DEC-002 | Decision | Growth reassessment records its trigger-selection basis and reassessment action without a fixed trigger catalogue. | Shared-foundation owner | When ALZ-PLT-130 is prepared or reassessed | Draft |
| DEC-003 | Decision | ALZ-PLT-129 verification tests one representative privileged-access change condition and one representative shared-foundation change condition, not every configured alert condition. | User | When ALZ-PLT-129 verification is planned or reassessed | Draft |
| DEC-004 | Decision | The executive sponsor authorizes each defined shared resource's intended users. The documented scope-and-responsibility record identifies intended users, authorization basis or evidence is retained, and shared-use verification demonstrates use only for users so authorized. This does not specify an authorization mechanism, timing, identity, or policy. | Executive sponsor | Before providing each defined shared resource or accepting ALZ-PLT-126 evidence | Draft; user-provided input recorded, not approved |

## Traceability

All lifecycle links are **Unverified for Draft**. No entry demonstrates delivery, verification, acceptance, an approved exception, baseline approval, or production-entry authorization.

| SOR ID | Source | Design/delivery link | Verification evidence | Acceptance status |
| --- | --- | --- | --- | --- |
| ALZ-PLT-127 | EVD-002, EVD-006, EVD-011 | Unverified; privileged-access and recovery technical design pending QST-004 | Unverified; access and recovery test required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-128 | EVD-002, EVD-006, EVD-011 | Unverified; authentication-protection technical design pending QST-004 | Unverified; authentication-factor test required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-125 | EVD-006, EVD-011 | Unverified; controlled-record technical design pending QST-005 and TD-001 | Unverified; reconciliation inspection and representative update demonstration required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-129 | EVD-002, EVD-008, EVD-011 | Unverified; alert inputs and representative conditions pending QST-006 | Unverified; configured-alert inspection and two representative alert tests required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-130 | EVD-002, EVD-007, EVD-011 | Unverified; growth reassessment record pending QST-016 | Unverified; inspection of documented trigger-selection basis and reassessment action required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-123 | EVD-006, EVD-011 | Unverified; responsibility-boundary and shared-resource scope records pending QST-016 | Unverified; boundary-record inspection required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-124 | EVD-002, EVD-006, EVD-011 | Unverified; shared-foundation activity and alert input pending QST-006 | Unverified; retrieval demonstration required | Unverified; Martyn Fewtrell evidence acceptance required |
| ALZ-PLT-126 | EVD-012, EVD-013 | Unverified; defined shared-resource scope, responsibilities, intended users, executive-sponsor authorization basis or evidence, and applicable obligations pending QST-016 | Unverified; inspect the scope-and-responsibility record and retained authorization basis or evidence, then demonstrate shared use only by intended users covered by that evidence for every defined resource | Unverified; Martyn Fewtrell evidence acceptance required, distinct from intended-user authorization |

### Active Lifecycle Detail

All lifecycle links below are **Unverified for Draft**. No entry demonstrates delivery, verification, acceptance, an approved exception, baseline approval, or production-entry authorization.

#### ALZ-PLT-127
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-006, EVD-011 |
| Design or work item | Unverified; technical-design work pending QST-004 |
| Implementation configuration | Unverified; privileged-access and recovery record required |
| Deployment | Unverified |
| Verification | Unverified; access and recovery test required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-04 |

#### ALZ-PLT-128
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-006, EVD-011 |
| Design or work item | Unverified; technical-design work pending QST-004 |
| Implementation configuration | Unverified; authentication-protection evidence required |
| Deployment | Unverified |
| Verification | Unverified; authentication-factor test required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-04 |

#### ALZ-PLT-125
| Field | Value |
| --- | --- |
| Source/rationale | EVD-006, EVD-011 |
| Design or work item | Unverified; technical-design work pending QST-005 and TD-001 |
| Implementation configuration | Unverified; controlled responsibility, intended-state, observed-state, and reconciliation records required |
| Deployment | Unverified |
| Verification | Unverified; reconciliation inspection and representative update demonstration required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-04 |

#### ALZ-PLT-129
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-008, EVD-011 |
| Design or work item | Unverified; alert inputs and representative conditions pending QST-006 |
| Implementation configuration | Unverified; configured-alert record required |
| Deployment | Unverified |
| Verification | Unverified; configured-alert inspection and two representative alert tests required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-04 |

#### ALZ-PLT-130
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-007, EVD-011 |
| Design or work item | Unverified; growth reassessment work pending QST-016 |
| Implementation configuration | Unverified; growth reassessment record required |
| Deployment | Unverified |
| Verification | Unverified; inspection of documented trigger-selection basis and reassessment action required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-04 |

#### ALZ-PLT-123
| Field | Value |
| --- | --- |
| Source/rationale | EVD-006, EVD-011 |
| Design or work item | Unverified; responsibility-boundary work pending QST-016 |
| Implementation configuration | Unverified; responsibility-boundary and shared-resource scope records required |
| Deployment | Unverified |
| Verification | Unverified; boundary-record inspection required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-04 |

#### ALZ-PLT-124
| Field | Value |
| --- | --- |
| Source/rationale | EVD-002, EVD-006, EVD-011 |
| Design or work item | Unverified; activity and alert input pending QST-006 |
| Implementation configuration | Unverified; activity-information record required |
| Deployment | Unverified |
| Verification | Unverified; retrieval demonstration required |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required |
| Last reviewed | 2026-08-04 |

#### ALZ-PLT-126
| Field | Value |
| --- | --- |
| Source/rationale | EVD-012, EVD-013 |
| Design or work item | Unverified; scope, responsibilities, intended users, executive-sponsor authorization basis or evidence, and applicable obligations pending QST-016 |
| Implementation configuration | Unverified; defined shared-resource scope-and-responsibility record identifying intended users and retained executive-sponsor authorization basis or evidence required |
| Deployment | Unverified |
| Verification | Unverified; inspect the scope-and-responsibility record and retained authorization basis or evidence, then demonstrate shared use only by intended users covered by that evidence for every defined resource |
| Acceptance/exception | Unverified; Martyn Fewtrell evidence acceptance required, distinct from intended-user authorization |
| Last reviewed | 2026-08-04 |

## Legacy Requirement Retirement Register

| Retired ID | Status | Rationale | Replacement ALZ-PLT ID(s) |
| --- | --- | --- | --- |
| ALZ-PLT-121 | Retired | Its materially changed deployment-and-management outcome is retired; its controlled-definition and management outcome is separately restated without reusing the ID. | ALZ-PLT-125 |
| ALZ-PLT-117 | Retired | Its initial-application placement intent materially changed to shared-foundation and application responsibility boundaries. | ALZ-PLT-123 |
| ALZ-PLT-118 | Retired | Dedicated test and production environments for one initial application conflict with the revised shared-foundation scope. | No replacement |
| ALZ-PLT-105 | Retired | Application resource-configuration evaluation is an application responsibility under the revised scope. | No replacement |
| ALZ-PLT-106 | Retired | Its application-diagnostic collection intent materially changed to shared-foundation activity visibility. | ALZ-PLT-124 |
| ALZ-PLT-108 | Retired | Application stateful-component recovery is an application responsibility under the revised scope. | No replacement |
| ALZ-PLT-109 | Retired | Application cost management is explicitly outside the shared-foundation scope. | No replacement |
| ALZ-PLT-122, ALZ-PLT-114, ALZ-PLT-115 | Retired | Application-specific connectivity is outside the revised scope. | No replacement |
| ALZ-PLT-116 | Retired | Application applicability assessment and consumption evidence conflict with the boundary that applications own onboarding and deployment. | No replacement |
| ALZ-PLT-119 | Retired | Its initial-application privileged-access and recovery subject materially changed to the future shared foundation. | ALZ-PLT-127 |
| ALZ-PLT-120 | Retired | Its initial-application authentication-resilience subject materially changed to the future shared foundation. | ALZ-PLT-128 |
| ALZ-PLT-107 | Retired | Its initial-application alerting subject materially changed to the future shared foundation. | ALZ-PLT-129 |
| ALZ-PLT-111 | Retired | Its initial-application growth-reassessment subject materially changed to the future shared foundation. | ALZ-PLT-130 |

## Quality Review

| Check | Result | Finding |
| --- | --- | --- |
| Draft status and approval authority are recorded | Pass with limitation | Martyn Fewtrell is named, but no approval, acceptance, exception approval, or production-entry authorization is recorded. |
| Decision, audience, scope, time boundary, and evidence are recorded | Pass | EVD-011 records the active scope; EVD-012 records the shared-resource decision; EVD-013 records intended-user authorization and verification; EVD-003 through EVD-005 and EVD-009 are retained as superseded evidence. |
| Facts, technical-design dependencies, and unknowns are distinct | Pass with limitation | TD-001 retains the supplied technical-design direction as an external technical-design dependency; QST-017 owns its disposition. QST-004 through QST-006, QST-010, and QST-016 remain open. |
| Registers are separate and owned | Pass with limitation | QST-004 through QST-006, QST-010, QST-016, and QST-017 remain open; shared-foundation and application owners are not named. |
| Mandatory requirements have complete metadata | Pass | Active requirements have stable IDs, owner, priority, status, source/rationale, dependency, verification, pass criterion, evidence, and acceptance authority. ALZ-PLT-126 retains intended-user authorization evidence separately from evidence acceptance. |
| Requirements are outcome-oriented and solution-neutral | Pass with limitation | Active requirements do not prescribe products, platforms, architecture, configurations, hosting arrangements, authorization mechanisms, or delivery methods. An audit found the technical terms externalized to TD-001 only in TD-001 and QST-017; all active requirements remain unverified. |
| Material traceability is complete | Pass with limitation | Each active requirement has source/rationale, design or work item, implementation/configuration, deployment, verification, acceptance/exception, and last-reviewed fields. ALZ-PLT-126 identifies intended users, retained executive-sponsor authorization basis or evidence, and shared-use verification. All lifecycle fields remain Unverified for Draft. |
| Markdown rendering and field association | Pass | Requirement metadata and active lifecycle detail use individual two-column field/value tables. Active tables have matched delimiter columns. |

**Unverified at stakeholder review:** QST-004 through QST-006, QST-010, QST-016, and QST-017; named shared-foundation and application owners; all technical-design, delivery, verification, intended-user authorization, acceptance, and lifecycle evidence. QST-016 must be answered for each defined shared resource before it is provided or evidence for ALZ-PLT-123 or ALZ-PLT-126 is accepted.

## Approval and Change History

| Version | Date | Change summary | Drafted by | Approved by | Approval status |
| --- | --- | --- | --- | --- | --- |
| 2.1 | 2026-08-03 | Previous application-centric Draft; retained as hidden historical material for traceability. | GitHub Copilot | Not approved | Draft |
| 3.0 | 2026-08-04 | Material Draft scope change: revised the SOR to a shared foundation and shared resources for future shared use; excluded Platform Engineering and application onboarding, deployment, and cost management; added ALZ-PLT-123 and ALZ-PLT-124; revised ALZ-PLT-121; retired application-centric requirements; added EVD-011, ASM-004, RSK-005, and QST-016. No approval was made. | GitHub Copilot | Not approved | Draft |
| 3.1 | 2026-08-04 | Accepted independent-review corrections and user decision: removed technical solution prescriptions from active SOR content; retained supplied technical direction as external technical-design dependency TD-001 and added QST-017; retired ALZ-PLT-121 and added ALZ-PLT-125 for the materially changed controlled-definition and management outcome; added approved outcome-only shared-resource requirement ALZ-PLT-126 and EVD-012; extended QST-016, ASM-004, and RSK-005 for per-resource applicable obligations; and completed active lifecycle detail. No approval was made. | GitHub Copilot | Not approved | Draft |
| 3.2 | 2026-08-04 | Accepted independent-review corrections and user decision: retired ALZ-PLT-119, ALZ-PLT-120, ALZ-PLT-107, and ALZ-PLT-111 and replaced them with ALZ-PLT-127 through ALZ-PLT-130 for the materially changed future shared-foundation scope; made ALZ-PLT-126 and all active SOR supporting content solution-neutral for authorized shared use; moved the supplied hosting prescription to external technical-design dependency TD-001; and changed QST-016 to require its scope-and-responsibility definition artifact before shared-resource provision or evidence acceptance, not before definition. No approval was made. | GitHub Copilot | Not approved | Draft |
| 3.3 | 2026-08-04 | Final-review decision: added EVD-013 and DEC-004 to record that the executive sponsor authorizes each defined shared resource's intended users; revised ALZ-PLT-126, QST-016, RSK-005, traceability, lifecycle detail, and verification/acceptance text for retained authorization basis or evidence and authorized-users-only verification; clarified that authorization is distinct from acceptance; and replaced active governance wording with shared-foundation scope change. No approval was made. | GitHub Copilot | Not approved | Draft |