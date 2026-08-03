# Azure Landing Zone Platform for One Initial Application - Statement of Requirements

> Status: Draft
> Version: 0.6
> Date: 2026-08-03
> Baseline, evidence, exception, and production-entry authority: Executive sponsor (identity not supplied)
> Approval status: Not approved

## Purpose and Decision

- **Problem or opportunity:** The business needs a production-capable Azure landing-zone platform for one initial application without enterprise-scale structure or unconfirmed corporate controls.
- **Intended outcome:** A small, operable Azure platform that provides environment isolation, controlled access and deployment, observability, recovery-enabling services, cost guardrails, and an evidence-based path to grow.
- **Decision supported:** Whether this Draft describes the platform capabilities required to design and deliver the initial application foundation.
- **Success measures:** The initial application can use every applicable platform capability with the stated verification evidence; unknown design inputs remain visible; this Draft implies no baseline or production-entry decision.
- **Audience:** Executive sponsor; prospective platform and application owners; delivery team or service provider.
- **Scope and time boundary:** This Draft covers an Azure landing-zone platform for one initial application. It reflects evidence available on 2026-08-03 and does not select a region, architecture, licence, budget, provider, topology, recovery objective, or implementation.

## Scope and Boundaries

**In scope**

- Minimal Azure resource and governance structure for one application.
- Production and nonproduction isolation where both environments are required.
- Identity and privileged access, safe configuration and deployment, policy/control capability, observability, alerting, recovery-enabling services, cost visibility and guardrails, network/connectivity patterns, and growth triggers.

**Out of scope**

- Corporate governance bodies, finance processes, periodic access reviews, organization-wide operating cadence, risk appetite, broad compliance procedures, and corporate approval workflows.
- Application architecture, data classification, regulatory interpretation, region, RTO/RPO, budget, licensing, support agreement, service provider, network topology, and implementation selection.
- Approval of a requirement baseline, production deployment, exception, or implementation design.

**Boundary:** Application and platform design inputs determine configuration for the initial application. This Draft does not turn unknown inputs into requirements.

## Stakeholders and Governance

| Role | Named person or team | Accountability | Approval or escalation authority |
| --- | --- | --- | --- |
| Executive sponsor | Identity not supplied | May approve the SOR baseline, accept requirement evidence, approve exceptions, and authorize production entry only after the individual is named. | Only the named individual may perform those actions. |
| Platform owner | To be named | Delivers and operates the platform capabilities. | Escalates platform capability gaps to the executive sponsor. |
| Initial application owner | To be named | Supplies application design inputs and validates application use of the platform. | Escalates unresolved application inputs to the executive sponsor. |

Roles are needed accountabilities, not assigned people, corporate functions, or approval workflows.

## Evidence Inventory

| ID | Source | Date/version | Claim supported | Evidence status |
| --- | --- | --- | --- | --- |
| EVD-001 | User-provided input | 2026-08-03 | Production-capable Azure foundation for material workloads; executive sponsor is approval, evidence, and production-entry authority but unnamed. | User-provided |
| EVD-002 | [Azure Landing Zone Guidance for a Small Business](../research/azure-landing-zone-small-business-guidance.md) | Research date 2026-08-03 | Small landing-zone platform capabilities, design dependencies, and growth triggers. | Research evidence; observations and recommendations are distinct |
| EVD-003 | User-provided scope refinement | 2026-08-03 | Focus on platform capabilities for one initial application; exclude corporate compliance and management processes unless needed to define or validate a capability. | User-provided |

Research observations support requirement rationale. Recommendations and target-state examples are not approved requirements or implementation decisions.

## Requirement Baseline

All entries are mandatory Draft requirements. `Must` identifies a capability required for the initial application where applicable. Dependencies are design inputs or linked capabilities, not approvals. The executive sponsor is the acceptance authority by role only; the named individual remains unresolved in QST-001.

### ALZ-PLT-101

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide a documented Azure governance and resource structure that identifies the management scope and resource scope used by the initial application. |
| Type | Platform structure |
| Source or rationale | EVD-002; management groups and subscriptions provide governance scopes, and a shallow structure is recommended for a small estate. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-002, QST-003 |
| Verification method | Inspection |
| Objective pass criterion | The structure record identifies each management scope and application resource scope, its purpose, and the initial application's placement. |
| Required evidence | Platform structure record and deployed-scope inventory |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-102

| Field | Value |
| --- | --- |
| Normative requirement | Where the initial application requires both production and nonproduction environments, the platform shall provide distinct deployment scopes that prevent a deployment identity assigned to one environment from modifying the other without an explicitly assigned role in that other environment. |
| Type | Isolation |
| Source or rationale | EVD-002; separate production and nonproduction subscriptions are the recommended first isolation split for production workloads. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-101, QST-002 |
| Verification method | Inspection and test |
| Objective pass criterion | Distinct scopes are inventoried, and a test deployment identity assigned only to one environment cannot modify resources in the other. |
| Required evidence | Environment-scope inventory, role-assignment inventory, and isolation test record |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-103

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall use group-based Azure access assignments for human platform administration, except for direct emergency-recovery access recorded with its recovery purpose, and shall provide an independently usable recovery path for loss of normal privileged access. |
| Type | Identity and access |
| Source or rationale | EVD-002; Azure RBAC guidance recommends group assignments, narrower scopes, and emergency access. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-004 |
| Verification method | Inspection and test |
| Objective pass criterion | Every human administrative assignment is group-based or references a direct emergency-recovery record, and a controlled test restores authorized administrative access without normal privileged access. |
| Required evidence | Privileged-access inventory, emergency-recovery record and procedure, and recovery test record |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-112

| Field | Value |
| --- | --- |
| Normative requirement | Before human privileged access is used in production, the platform shall require multi-factor authentication such that compromise of one authentication factor alone cannot authorize that access. |
| Type | Identity security |
| Source or rationale | EVD-002; research requires MFA before production and states that exact Entra configuration and licensing require validation. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-004 |
| Verification method | Inspection and test |
| Objective pass criterion | The privileged-access configuration identifies each human privileged access population and test evidence demonstrates that possession or compromise of one authentication factor alone does not authorize privileged access. |
| Required evidence | Privileged-access configuration, authentication-control evidence, and authentication-factor test record |
| Acceptance authority | Named executive sponsor (QST-001) |

### ALZ-PLT-104

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall maintain a complete inventory of applicable deployable platform configurations and reconcile each inventory item to its version-controlled source and deployed state before production operation depends on that item. |
| Type | Configuration management |
| Source or rationale | EVD-002; research recommends infrastructure as code and source control to limit drift and support change recovery. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-005 |
| Verification method | Inspection and demonstration |
| Objective pass criterion | The inventory identifies every applicable deployable platform configuration; every inventory item links to its version-controlled source and deployed state; and reconciliation records identify any mismatch and disposition. Representative deployments may supplement but cannot replace item-level reconciliation. |
| Required evidence | Complete configuration inventory, source revisions, deployed-state records, item-level reconciliation records, and representative deployment demonstration record where used |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-105

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide a policy or control capability that evaluates the initial application's applicable resource configuration at documented scopes and records the result. |
| Type | Control capability |
| Source or rationale | EVD-002; Azure Policy supports evaluation at management-group, subscription, resource-group, and resource scopes. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-101, QST-002 |
| Verification method | Demonstration |
| Objective pass criterion | A test resource configuration at each applicable scope produces a recorded compliant or noncompliant result retrievable by an authorized platform operator. |
| Required evidence | Control configuration, scope record, and evaluation demonstration record |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-106

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall collect and make retrievable Azure control-plane activity logging and application diagnostic information selected from the initial application's documented observability inputs. |
| Type | Observability |
| Source or rationale | EVD-002; research identifies activity and diagnostic logging as required to investigate platform changes, security events, and production failures. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-006 |
| Verification method | Demonstration |
| Objective pass criterion | A test control-plane activity is retrievable by an authorized operator, and for each selected application diagnostic category a test event is retrievable from the recorded destination. |
| Required evidence | Observability input record, activity-log configuration, diagnostic configuration, and retrieval test records |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-107

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide actionable alerts for privileged-access and platform-configuration changes, each with a configured response destination. |
| Type | Alerting |
| Source or rationale | EVD-002; research recommends a small actionable alert set with an owner and response path. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-106, QST-006 |
| Verification method | Test |
| Objective pass criterion | A representative privileged-access change and a representative platform-configuration change each produce an alert at their configured response destination. |
| Required evidence | Alert configuration, response-destination record, and alert test records |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-108

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide recovery-enabling services for each stateful component of the initial application according to its documented recovery inputs, including a method to create recoverable data and a method to test restoration. |
| Type | Reliability |
| Source or rationale | EVD-002; recovery goals derive from business requirements and require documented, tested recovery plans. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-007 |
| Verification method | Inspection and test |
| Objective pass criterion | Each documented stateful component has a configured recovery method, and a restoration test demonstrates recovery using that method. |
| Required evidence | Recovery-input record, recovery configuration, and restoration test record |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-109

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide cost visibility for the initial application through an attributable cost scope and shall provide a configurable spend-alert guardrail for that scope. |
| Type | Cost management |
| Source or rationale | EVD-002; Cost Management guidance recommends accountability, budgets, alerts, and investigation of anomalies. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-101, QST-008 |
| Verification method | Demonstration |
| Objective pass criterion | Cost data for the initial application's attributable scope is retrievable, and a representative actual or forecast threshold produces an alert at the configured destination. |
| Required evidence | Cost-scope record, cost-view retrieval record, budget or alert configuration, and alert test record |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-110

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall provide a documented network and connectivity pattern for the initial application that identifies its required flows, public or internal exposure, and the platform controls used to permit or restrict those flows. |
| Type | Connectivity |
| Source or rationale | EVD-002; network topology and placement depend on exposure, dependencies, and connectivity requirements. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | QST-009 |
| Verification method | Inspection and test |
| Objective pass criterion | The network pattern identifies every required flow and exposure classification, and tests demonstrate that one permitted flow succeeds while one restricted flow is denied. |
| Required evidence | Network-pattern record, network configuration, and connectivity test record |
| Acceptance authority | Executive sponsor |

### ALZ-PLT-111

| Field | Value |
| --- | --- |
| Normative requirement | The platform shall maintain a growth-trigger record that identifies the observed condition, impact, and reassessment action for expanding the initial platform structure or shared services. |
| Type | Evolution |
| Source or rationale | EVD-002; recommended triggers include another independently owned workload, sensitive or regulated data, private connectivity, shared ingress or egress, delegated teams, availability commitments, and recurring manual operations. |
| Priority | Must |
| Owner | Platform owner |
| Status | Draft |
| Dependency | ALZ-PLT-101 through ALZ-PLT-110 |
| Verification method | Inspection |
| Objective pass criterion | The record contains each trigger relevant to the initial application and its reassessment action without selecting a future implementation. |
| Required evidence | Growth-trigger record |
| Acceptance authority | Executive sponsor |

## Verification and Acceptance

- **Verification environments and data constraints:** Use nonproduction environments and representative non-sensitive test data where available. The need for production testing remains an application design input.
- **Evidence location:** The controlled evidence repository or record system is not supplied and remains open in QST-010.
- **Acceptance approach:** The platform owner assembles requirement evidence; the initial application owner validates application-specific inputs and tests. Only the named executive sponsor may approve the SOR baseline, accept evidence, approve an exception, or authorize production entry. Naming the individual is a prerequisite to each action.
- **Exceptions:** This Draft grants no exception. An unmet requirement remains visible in traceability and only the named executive sponsor may approve a recorded exception before production entry.

## Assumptions

| ID | Statement | Owner | Impact if false | Review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| ASM-001 | Azure is the selected cloud platform for the stated scope. | Executive sponsor | The SOR requires material revision. | Cloud-platform decision changes | Open |
| ASM-002 | One initial application is the current platform consumer. | Executive sponsor | Platform scale and isolation requirements may change. | A second application is proposed | Open |
| ASM-003 | The initial application may require a production environment. | Initial application owner | ALZ-PLT-102 applicability changes. | Application environment decision | Open |

## Risks

| ID | Risk | Owner | Impact | Treatment or review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| RSK-001 | Unknown application data, recovery, and exposure inputs could make an initial platform capability unsuitable. | Initial application owner | Rework or unsafe production configuration. | Resolve QST-002, QST-006, QST-007, and QST-009 before configuring affected capabilities. | Open |
| RSK-002 | Unknown licensing or service availability could constrain identity, monitoring, recovery, or cost features. | Platform owner | Rework or unavailable capability. | Resolve QST-004 and QST-005 before implementation selection. | Open |
| RSK-003 | Growth beyond one application could exceed the initial platform's isolation or operational model. | Platform owner | Cost, security, or operability degradation. | Evaluate ALZ-PLT-111 when a recorded trigger occurs. | Open |

## Issues, Questions, and Decisions

| ID | Type | Statement | Owner | Due date or trigger | Status |
| --- | --- | --- | --- | --- | --- |
| QST-001 | Question | What is the name of the executive sponsor who alone may approve the SOR baseline, accept requirement evidence, approve exceptions, and authorize production entry? | Executive sponsor | Before baseline approval, evidence acceptance, exception approval, or production entry | Open |
| QST-002 | Question | What are the initial application's environments, resource needs, data characteristics, and applicable obligations? | Initial application owner | Before platform configuration | Open |
| QST-003 | Question | Which management and resource scopes are appropriate for the initial application? | Platform owner | Before ALZ-PLT-101 configuration | Open |
| QST-004 | Question | Which Entra capabilities, licensing, and configuration will provide multi-factor authentication for human privileged access and support the selected privileged-access model? | Platform owner | Before ALZ-PLT-103 and ALZ-PLT-112 configuration | Open |
| QST-005 | Question | Which source-control and repeatable deployment mechanism will manage platform configuration? | Platform owner | Before ALZ-PLT-104 configuration | Open |
| QST-006 | Question | Which application diagnostic categories, retention needs, alert thresholds, and response destinations does the initial application require? | Initial application owner | Before application observability configuration | Open |
| QST-007 | Question | What recovery objectives, data retention needs, and stateful components apply to the initial application? | Initial application owner | Before ALZ-PLT-108 configuration | Open |
| QST-008 | Question | What cost allocation, budget, and alert threshold inputs apply to the initial application? | Executive sponsor | Before ALZ-PLT-109 configuration | Open |
| QST-009 | Question | What connectivity dependencies, data flows, address-space constraints, and public exposure needs apply to the initial application? | Initial application owner | Before ALZ-PLT-110 configuration | Open |
| QST-010 | Question | Where will controlled platform evidence and acceptance records be retained? | Platform owner | Before evidence acceptance | Open |
| DEC-001 | Decision | This Draft is limited to platform capabilities for one initial application and does not impose corporate compliance procedures or select application/platform design values. | Executive sponsor | Revisit on material scope change | Draft |

## Traceability

All lifecycle links are **Unverified for Draft**. No entry demonstrates delivery, verification, acceptance, an approved exception, baseline approval, or production-entry authorization.

| SOR ID | Source | Design/delivery link | Verification evidence | Acceptance status |
| --- | --- | --- | --- | --- |
| ALZ-PLT-101 | EVD-002, EVD-003 | Unverified; structure decision pending QST-003 | Unverified; structure inspection required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-102 | EVD-002, EVD-003 | Unverified; environment design pending QST-002 | Unverified; isolation test required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-103 | EVD-002, EVD-003 | Unverified; identity design pending QST-004 | Unverified; access and recovery test required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-112 | EVD-002, EVD-003 | Unverified; MFA approach pending QST-004 | Unverified; one-factor test required | Unverified; named executive sponsor required |
| ALZ-PLT-104 | EVD-002, EVD-003 | Unverified; deployment mechanism pending QST-005 | Unverified; deployment demonstration required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-105 | EVD-002, EVD-003 | Unverified; applicable controls pending QST-002 | Unverified; evaluation demonstration required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-106 | EVD-002, EVD-003 | Unverified; observability inputs pending QST-006 | Unverified; retrieval test required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-107 | EVD-002, EVD-003 | Unverified; alert inputs pending QST-006 | Unverified; alert test required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-108 | EVD-002, EVD-003 | Unverified; recovery inputs pending QST-007 | Unverified; restoration test required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-109 | EVD-002, EVD-003 | Unverified; cost inputs pending QST-008 | Unverified; cost and alert demonstration required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-110 | EVD-002, EVD-003 | Unverified; network inputs pending QST-009 | Unverified; connectivity test required | Unverified; executive-sponsor evidence acceptance required |
| ALZ-PLT-111 | EVD-002, EVD-003 | Unverified; trigger record required | Unverified; record inspection required | Unverified; executive-sponsor evidence acceptance required |

### Active Lifecycle Detail

All lifecycle links below are **Unverified for Draft**. QST-001 must be resolved before an acceptance or exception status can change.

| SOR ID | Source/rationale | Design or work item | Implementation configuration | Deployment record | Verification evidence | Acceptance/exception status |
| --- | --- | --- | --- | --- | --- | --- |
| ALZ-PLT-101 | EVD-002, EVD-003 | Structure decision pending QST-003 | Scope configuration required | Unverified | Structure inspection required | Unverified; named sponsor required |
| ALZ-PLT-102 | EVD-002, EVD-003 | Environment design pending QST-002 | Scope/role configuration required | Unverified | Isolation test required | Unverified; named sponsor required |
| ALZ-PLT-103 | EVD-002, EVD-003 | Access/recovery design pending QST-004 | Access configuration required | Unverified | Access/recovery test required | Unverified; named sponsor required |
| ALZ-PLT-104 | EVD-002, EVD-003 | Deployment mechanism pending QST-005 | Inventory and source required | Unverified | Item-level reconciliation required | Unverified; named sponsor required |
| ALZ-PLT-105 | EVD-002, EVD-003 | Applicable controls pending QST-002 | Control configuration required | Unverified | Evaluation demonstration required | Unverified; named sponsor required |
| ALZ-PLT-106 | EVD-002, EVD-003 | Observability inputs pending QST-006 | Activity-log and diagnostic configuration required | Unverified | Retrieval test required | Unverified; named sponsor required |
| ALZ-PLT-107 | EVD-002, EVD-003 | Response destination pending QST-006 | Alert configuration required | Unverified | Alert test required | Unverified; named sponsor required |
| ALZ-PLT-108 | EVD-002, EVD-003 | Recovery inputs pending QST-007 | Recovery configuration required | Unverified | Restoration test required | Unverified; named sponsor required |
| ALZ-PLT-109 | EVD-002, EVD-003 | Cost inputs pending QST-008 | Cost/alert configuration required | Unverified | Cost/alert demonstration required | Unverified; named sponsor required |
| ALZ-PLT-110 | EVD-002, EVD-003 | Network inputs pending QST-009 | Network configuration required | Unverified | Connectivity test required | Unverified; named sponsor required |
| ALZ-PLT-111 | EVD-002, EVD-003 | Growth triggers required | Growth-trigger record required | Unverified | Record inspection required | Unverified; named sponsor required |
| ALZ-PLT-112 | EVD-002, EVD-003 | MFA approach pending QST-004 | MFA configuration required | Unverified | One-factor test required | Unverified; named sponsor required |

## Legacy Requirement Retirement Register

| Retired ID | Status | Rationale | Replacement ALZ-PLT ID |
| --- | --- | --- | --- |
| ALZ-SOR-001 | Retired | Discovery profile replaced by application inputs and questions. | No replacement |
| ALZ-SOR-002 | Retired | Corporate production gate is outside scope. | No replacement |
| ALZ-SOR-003 | Retired | Governance structure retained. | ALZ-PLT-101 |
| ALZ-SOR-004 | Retired | IaC reconciliation retained and strengthened. | ALZ-PLT-104 |
| ALZ-SOR-005 | Retired | Group access retained. | ALZ-PLT-103 |
| ALZ-SOR-006 | Retired | Emergency recovery retained. | ALZ-PLT-103 |
| ALZ-SOR-007 | Retired | Control evaluation retained. | ALZ-PLT-105 |
| ALZ-SOR-008 | Retired | Corporate exception process is outside scope. | No replacement |
| ALZ-SOR-009 | Retired | Observability retained. | ALZ-PLT-106 |
| ALZ-SOR-010 | Retired | Alerting retained. | ALZ-PLT-107 |
| ALZ-SOR-011 | Retired | Recovery retained. | ALZ-PLT-108 |
| ALZ-SOR-012 | Retired | Restoration retained. | ALZ-PLT-108 |
| ALZ-SOR-013 | Retired | Cost visibility retained. | ALZ-PLT-109 |
| ALZ-SOR-014 | Retired | Cost-estimate review is outside scope. | No replacement |
| ALZ-SOR-015 | Retired | Change integrity represented by IaC reconciliation. | ALZ-PLT-104 |
| ALZ-SOR-016 | Retired | Network outcome retained. | ALZ-PLT-110 |
| ALZ-SOR-017 | Retired | Exposure is a network input. | ALZ-PLT-110 |
| ALZ-SOR-018 | Retired | Corporate runbook management is outside scope. | No replacement |
| ALZ-SOR-019 | Retired | Corporate review cadence is outside scope. | No replacement |
| ALZ-SOR-020 | Retired | Production authorization remains an acceptance boundary. | No replacement |
| ALZ-SOR-021 | Retired | Access/recovery retained without periodic review management. | ALZ-PLT-103 |
| ALZ-SOR-022 | Retired | MFA retained as distinct security requirement. | ALZ-PLT-112 |
| ALZ-SOR-023 | Retired | Activity logging and diagnostics retained. | ALZ-PLT-106 |
| ALZ-SOR-024 | Retired | Sponsor naming remains a QST-001 prerequisite. | No replacement |

## Quality Review

Stakeholder review is permitted for this Draft and is intended to resolve QST-001 through QST-010. It does not approve the baseline, accept evidence, approve an exception, or authorize production entry; those actions remain gated by the named executive sponsor and their respective required records and conditions.

| Check | Result | Finding |
| --- | --- | --- |
| Draft status and approval authority are recorded | Pass with limitation | Stakeholder review is permitted to resolve QST-001 through QST-010. The executive-sponsor role is recorded, but the individual is unresolved in QST-001; no baseline, evidence acceptance, exception approval, or production-entry authorization may occur until the individual is named and the respective required records and conditions are satisfied. |
| Decision, audience, scope, time boundary, and evidence are recorded | Pass | EVD-001 through EVD-003 distinguish user input, research evidence, and the material scope refinement. |
| Facts, recommendations, and unknowns are distinct | Pass | Research recommendations are not adopted as requirements; unknown inputs remain in questions and assumptions. |
| Assumptions, risks, issues, questions, and decisions are separate and owned | Pass with limitation | Platform and application owners are not yet named. |
| Mandatory requirements have complete metadata | Pass | ALZ-PLT-101 through ALZ-PLT-112 have unique IDs, owner, priority, status, source/rationale, dependency, verification, pass criterion, evidence, and acceptance authority. |
| Requirements are atomic, outcome-oriented, and verifiable | Pass | MFA is distinct; privileged access is objectively group-based with recovery; IaC requires item-level reconciliation; observability has a minimum platform baseline. |
| Prescription is evidence-backed or avoided | Pass | Azure is user-supplied scope; specific regions, services, architectures, configurations, and products remain design inputs. |
| Scope coverage is addressed or explicitly not applicable | Pass | Structure, isolation, access, configuration, controls, observability, alerting, recovery, cost, connectivity, evolution, and acceptance are covered; corporate processes are expressly out of scope. |
| Material traceability is complete | Pass with limitation | Summary and active lifecycle detail separate source, design/work, implementation, deployment, verification, and acceptance/exception status; every legacy ALZ-SOR ID is visibly retired. Delivery, verification, and acceptance evidence remain unverified for Draft. |
| Markdown rendering and field association | Pass | Requirement metadata uses individual two-column tables; other tables have matched delimiter columns and no fenced code blocks. |

**Unverified at stakeholder review:** QST-001 through QST-010; named platform and initial application owners; all platform configuration, verification evidence, acceptance records, and lifecycle delivery links. Stakeholder review is permitted and is intended to resolve QST-001 through QST-010. These remain open Draft items, not approvals or accepted risks; the named executive sponsor and the respective evidence, exception, baseline, and production-entry conditions remain required for those actions.

## Approval and Change History

| Version | Date | Change summary | Drafted by | Approved by | Approval status |
| --- | --- | --- | --- | --- | --- |
| 0.1 | 2026-08-03 | Initial controlled Draft based on the initial evidence set. | GitHub Copilot | Not approved | Draft |
| 0.2 | 2026-08-03 | Draft correction recording executive-sponsor evidence and production-entry authority and strengthening testability. | GitHub Copilot | Not approved | Draft |
| 0.3 | 2026-08-03 | Draft correction strengthening configuration reconciliation and authentication-assurance testability. | GitHub Copilot | Not approved | Draft |
| 0.4 | 2026-08-03 | Material scope refinement: replaced corporate compliance and management-process requirements with eleven new `ALZ-PLT` platform capability requirements for one initial application; retired prior `ALZ-SOR` IDs rather than reusing changed intent; moved corporate processes to boundaries and design inputs. | GitHub Copilot | Not approved | Draft |
| 0.5 | 2026-08-03 | Independent-review corrections: named-sponsor approval boundary; MFA; activity logging and privileged/platform-change alerts; item-level IaC reconciliation; verifiable group-based access; visible retirement and lifecycle traceability registers. | GitHub Copilot | Not approved | Draft |
| 0.6 | 2026-08-03 | Draft correction: clarified that stakeholder review is permitted to resolve QST-001 through QST-010 while preserving named-sponsor and action-specific gates; added ALZ-PLT-112 to summary traceability. | GitHub Copilot | Not approved | Draft |

<!-- Retired 0.3 content retained only to preserve file-provider history; it is not part of the 0.4 Draft.
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