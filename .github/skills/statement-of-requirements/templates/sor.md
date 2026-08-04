# Statement of Requirements

> Status: Draft
> Version: [version]
> Date: [YYYY-MM-DD]
> Baseline authority: [name or role]
> Approval status: Not approved

> Content boundary: Record functional and non-functional user requirements only. Do not include technical solution information, such as products, platforms, architecture, design, configuration, mechanisms, or delivery methods.

## 1. Summary

- Business requirements: [path or reference]
- Owner: [name or team]
- Intended outputs: [technical specification, delivery plan, or other downstream artifacts]

### 1.1 Document Links

| Document | Path or reference |
| --- | --- |
| Business requirements | [reference] |
| Requirements | [this document] |
| Technical specification | [reference or Not applicable] |
| Initial delivery plan | [reference or Not applicable] |

## 2. Purpose and Decision

- Problem or opportunity: [evidence-backed statement]
- Intended outcome: [outcome]
- Decision supported: [decision]
- Success measures: [measures]
- Audience: [roles]
- Scope and time boundary: [scope and currency]

## 3. Scope and Boundaries

### 3.1 In Scope

- [capability, user outcome, environment, integration, or lifecycle context]

### 3.2 Out of Scope

- [explicit exclusion, including technical solution information]

### 3.3 Target Implementation Surfaces

- [target boundary, component, service, route, page, or test surface; use only as an external technical-design dependency]

### 3.4 Behavior-Preservation Boundary

- [observable behavior that must remain unchanged]

### 3.5 Refactoring Cleanup Boundaries

- [area intentionally excluded to prevent cleanup sprawl]

## 4. Stakeholders and Governance

| Role | Named person or team | Accountability | Approval or escalation authority |
| --- | --- | --- | --- |
| Sponsor | [value] | [value] | [value] |
| Product or service owner | [value] | [value] | [value] |
| Technical owner | [value] | [value] | [value] |
| Security, privacy, or compliance owner | [value] | [value] | [value] |
| Operations owner | [value] | [value] | [value] |
| Finance or procurement owner | [value] | [value] | [value] |
| Acceptance authority | [value] | [value] | [value] |

## 5. Evidence Inventory

| ID | Source | Date or version | Claim supported | Evidence status |
| --- | --- | --- | --- | --- |
| EVD-001 | [source] | [value] | [claim] | Direct evidence / User-provided |

## 6. Functional Requirements

Use IDs `FR1`, `FR2`, and so on. Use the [requirement register](./requirement-register.md) for complete metadata and traceability.

> Writing standard: Use clear, plain English. Use short sentences, active voice, and common words. Avoid jargon, buzzwords, corporate or legal language, and unnecessary technical terms. State the required outcome and explain why only when it helps understanding.

### FR1: [short name]

| Field | Value |
| --- | --- |
| Requirement | [actor or system] shall [required outcome or behavior]. |
| Rationale | [why this outcome is needed] |
| Acceptance criteria | [testable statement] |
| Notes or constraints | [optional, outcome-only constraint] |

## 7. Non-Functional Requirements

Use IDs `NF1`, `NF2`, and so on. Include only applicable categories, such as performance, reliability and availability, maintainability and supportability, observability, and usability or accessibility.

### NF1: [short name]

| Field | Value |
| --- | --- |
| Category | [category] |
| Requirement | [actor or system] shall [required quality outcome]. |
| Measure or target | [measurable target, if evidenced] |
| Acceptance criteria | [testable statement] |

## 8. Security Requirements

Use IDs `SR1`, `SR2`, and so on. Include only evidenced security requirements, such as authentication and authorization, data protection, secrets and key management, or threats and abuse cases.

### SR1: [short name]

| Field | Value |
| --- | --- |
| Category | [category] |
| Requirement | [actor or system] shall [required security outcome]. |
| Acceptance criteria | [testable statement] |

## 9. Data Requirements (Optional)

Use IDs `DR1`, `DR2`, and so on when data requirements apply.

## 10. Interfaces and Integration Requirements (Optional)

Use IDs `IR1`, `IR2`, and so on when interface or integration requirements apply.

## 11. Testing Requirements

Use IDs `TR1`, `TR2`, and so on. For refactoring-focused packages, define regression-safety, behavior-preservation checks, and the narrowest executable validation expected for each implementation slice.

## 12. Operational Requirements (Optional)

Use IDs `OR1`, `OR2`, and so on when operational requirements apply.

## 13. Verification and Acceptance

- Verification environments and data constraints: [value]
- Evidence repository or locations: [value]
- Acceptance process and authority: [value]
- Approved exceptions process: [value]

## 14. Assumptions

| ID | Statement | Owner | Impact if false | Review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| ASM-001 | [value] | [value] | [value] | [value] | Open |

## 15. Risks

| ID | Risk | Owner | Impact | Treatment or review trigger | Status |
| --- | --- | --- | --- | --- | --- |
| RSK-001 | [value] | [value] | [value] | [value] | Open |

## 16. Issues, Questions, and Decisions

| ID | Type | Statement | Owner | Due date or trigger | Status |
| --- | --- | --- | --- | --- | --- |
| QST-001 | Question | [value] | [value] | [value] | Open |

## 17. Traceability

Use the [traceability register](./traceability-register.md) to link material requirements through design, delivery, evidence, and acceptance.

## 18. Approval and Change History

| Version | Date | Change summary | Drafted by | Approved by | Approval status |
| --- | --- | --- | --- | --- | --- |
| [version] | [YYYY-MM-DD] | Initial Draft | [value] | [value] | Not approved |
