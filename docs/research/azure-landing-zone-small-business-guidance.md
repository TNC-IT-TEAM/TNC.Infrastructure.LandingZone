# Azure Landing Zone Guidance for a Small Business

> Research date: 2026-08-03

## Question and Decision

- **Research question:** What Azure landing-zone practices and management model should a small business adopt to create a secure, governable, cost-conscious foundation without unnecessary enterprise complexity?
- **Audience:** The business owner/executive sponsor, the person accountable for IT and security, and the engineer or managed service provider (MSP) that will implement and run Azure.
- **Decision this supports:** Select an initial Azure landing-zone scope, implementation approach, governance controls, ownership model, and growth triggers.
- **Scope:** Azure platform foundation, subscriptions, identity, policy, networking, cost management, operations, security, reliability, and change management. It does not select a specific workload architecture, region, licensing plan, MSP, or regulatory control set.
- **Time boundary:** Microsoft guidance and product documentation reviewed through 2026-08-03. Service capabilities, pricing, and built-in policy content can change.

## Executive Summary

Azure landing zones are a Microsoft-recommended architecture for governing, securing, and scaling a multi-subscription Azure environment. They separate a centrally managed **platform landing zone** from **application landing zones** where workloads run. Microsoft recommends infrastructure as code (IaC) for the platform, with its Azure Landing Zones IaC Accelerator and Azure Verified Modules as implementation options. [Microsoft, updated 2026-07-31](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/) [Microsoft, updated 2025-12-15](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/implementation-options)

**Recommendation:** Start with a deliberately small but production-capable platform: one Microsoft Entra tenant; a shallow management-group hierarchy; separate production and nonproduction subscriptions where the business has production workloads; group-based, least-privilege access with just-in-time elevation where licensing and risk justify it; a small policy baseline; central logging and alerts; budgets; and IaC in source control. Add dedicated connectivity, security, management, sandbox, and more granular workload subscriptions only when an identified requirement or growth trigger makes their extra cost and operational burden worthwhile.

The important limitation is that "small business" does not establish the business's regulatory obligations, workloads, data sensitivity, uptime targets, network dependencies, team size, Azure agreement type, or available Entra licensing. Those facts can change the required controls materially. A landing zone should be a product that is operated and improved, not a one-time deployment.

## Findings

### Observed Facts

#### Architecture and implementation

- Microsoft defines an Azure landing zone as a flexible architecture for governing, securing, and scaling a multi-subscription Azure environment. Its platform component establishes centralized governance, security, and shared resources; application landing zones host workloads under the platform's standards. [Microsoft, updated 2026-07-31](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/)
- Microsoft states that most organizations should have one platform landing zone per Microsoft Entra tenant, and recommends centralizing a capability only when it delivers a clear governance, operational, or economic benefit across multiple workloads. [Microsoft, updated 2026-07-31](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/)
- Microsoft recommends its IaC accelerator using Bicep or Terraform and Azure Verified Modules. The portal accelerator is intended for organizations without IaC expertise but is less flexible and harder to update and version-control; Microsoft recommends transitioning it to IaC when possible. [Microsoft, updated 2025-12-15](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/implementation-options)
- Management groups provide a governance scope above subscriptions: policies and role assignments inherit through descendants. Azure supports up to six management-group levels below the root, but root-level assignments affect all resources and should be limited to "must have" controls. [Microsoft, updated 2025-07-21](https://learn.microsoft.com/en-us/azure/governance/management-groups/overview)
- The landing-zone reference model distinguishes internal/hybrid-facing workloads (Corp) from public-facing workloads (Online). A dedicated connectivity subscription commonly hosts shared network services, but which services to centralize depends on requirements. [Microsoft, updated 2026-01-09](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/network-topology-and-connectivity)
- Microsoft positions Virtual WAN for large-scale connectivity, including several regions, more than 30 branch sites, or certain VPN/ExpressRoute routing requirements. Traditional hub-and-spoke is presented for organizations that need controlled routing and have fewer than 30 IPsec tunnels per region. [Microsoft, updated 2025-10-29](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/define-an-azure-network-topology)

#### Identity, security, and governance

- Identity is a core platform responsibility in Azure Landing Zones; RBAC and least privilege are fundamental concepts for both platform and application landing zones. [Microsoft, updated 2026-01-09](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/identity-access)
- Azure RBAC guidance recommends least privilege, limiting a subscription to at most three Owners, assigning roles to groups rather than individual users, using narrower scopes for privileged roles, and using Privileged Identity Management (PIM) to time-bound privileged access. [Microsoft, updated 2026-03-25](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices)
- Azure Policy evaluates resource state against rules at management-group, subscription, resource-group, or resource scopes. It supports effects including audit, deny, modify, and deployment of related resources. Microsoft recommends starting with audit effects before enforcement, using initiatives to group policies, and managing policy resources as code with reviews. [Microsoft, updated 2026-07-08](https://learn.microsoft.com/en-us/azure/governance/policy/overview)
- Cloud Adoption Framework governance guidance says governance is continuous, calls for a small cross-functional team with executive sponsorship, and recommends a RACI to clarify responsibility. [Microsoft, updated 2026-03-09](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/govern/build-cloud-governance-team)
- Microsoft recommends an inheritance model for governance, a monitor-first approach for lower-priority risk, a small initial control set, and automated enforcement where feasible. Its guidance also identifies MFA, RBAC, Entra governance, Defender for Cloud, Azure Monitor, management groups, and IaC as relevant governance tools. [Microsoft, updated 2026-07-29](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/govern/enforce-cloud-governance-policies)

#### Cost, reliability, and operations

- Cost Management guidance calls for planning, visibility, accountability, optimization, and iteration. It recommends organizing subscriptions and resource groups for accountability, using tags for shared or cross-scope costs, budgets and alerts, and regularly investigating anomalies and idle resources. [Microsoft, updated 2026-05-21](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/cost-mgt-best-practices)
- Budgets can notify stakeholders based on actual or forecasted cost, but they do not stop resources or consumption. Budget and cost data are delayed; Cost Management data is typically available within 8-24 hours and budget evaluation occurs every 24 hours. [Microsoft, updated 2025-09-26](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/tutorial-acm-create-budgets)
- Azure operations guidance separates central platform responsibilities from workload responsibilities for compliance, security, deployment, monitoring, cost, reliability, and performance. It calls for named owners, operational procedures, centrally accessible runbooks, automated repetitive work, and periodic operational reviews. [Microsoft, updated 2026-04-07](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/manage/ready-cloud-operations)
- Well-Architected reliability guidance says recovery goals and architecture must derive from explicit business requirements, including critical user flows, cost, RTO, RPO, geography, and dependencies. It recommends documented and tested recovery plans, backups appropriate to targets, observable systems, actionable alerts, and avoiding overengineering. [Microsoft, updated 2026-03-17](https://learn.microsoft.com/en-us/azure/well-architected/reliability/principles)

### Inferences

The following conclusions are recommendations derived from the observed facts. They assume a small business with a limited cloud team, initially few workloads, and a need to run at least one production workload. They must be adjusted after discovery.

1. **Use a thin platform, not the complete enterprise reference architecture.** Microsoft describes the reference architecture as a starting point to adapt and directs organizations to centralize only capabilities with clear benefit. For a small estate, separate subscriptions for connectivity, identity, management, and security can become empty administrative containers and add cost. Start with only the subscriptions needed to establish isolation and accountability; evolve when workload count, compliance, hybrid connectivity, or delegated teams demand it.
2. **Make subscriptions the primary isolation and accountability boundary.** A separate production subscription and nonproduction subscription are generally the first useful split because they separate billing, RBAC, policy, quotas, and blast radius. Add a dedicated shared-services or connectivity subscription only when shared network services, central monitoring, or multiple workloads make it operationally beneficial. Create per-workload subscriptions when ownership, data sensitivity, lifecycle, compliance, quota, or risk materially differ.
3. **Prefer managed PaaS and serverless services where they meet requirements.** This is an operational recommendation, not a Microsoft landing-zone requirement. A small team should avoid self-managed virtual machines, domain controllers, network virtual appliances, and complex transit routing unless a workload requires them, because they add patching, backup, monitoring, incident, and skills obligations.
4. **Build enforcement gradually, but do not defer foundational security.** Require MFA and emergency-access planning, use group-based RBAC, restrict privileged owners, enable logging/alerts, set budgets, and protect backups before production launch. For policies that could interrupt delivery, observe first, fix existing noncompliance, then enforce. High-confidence controls such as approved regions, mandatory ownership/environment tags, and diagnostic settings may move to enforcement sooner after testing.
5. **IaC is the management system of record.** A portal-created proof of concept can accelerate learning, but the platform, policy assignments, budgets, alerts, and role assignments should be represented in reviewed source-controlled IaC before production operations depend on them. This limits configuration drift and makes recovery and change review practical for a small team.

## Recommended Initial Target State

### 1. Resource hierarchy

Use stable, descriptive IDs and keep the hierarchy shallow:

```text
Tenant root group
  business-root
    platform
    landing-zones
      production
      nonproduction
    sandbox (optional)
```

- Apply only tenant-wide, non-negotiable controls at `business-root`; do not use the tenant root group for ordinary administration.
- Put initial workload subscriptions under `production` and `nonproduction`.
- A single subscription may be acceptable for a short proof of concept with no sensitive production data, but it is not the recommended steady state once production is in use.
- Add `connectivity`, `management`, or `security` child groups and subscriptions only when dedicated shared services actually exist. A first shared-services subscription can host common logging/action-group resources when more than one subscription needs them.
- Do not create a hierarchy merely to match Microsoft diagrams. The hierarchy must represent a governance boundary that needs different inherited access or policy.

### 2. Identity and access baseline

- Use Microsoft Entra groups for all Azure RBAC assignments. Avoid direct user assignments except documented emergency access.
- Enable MFA for all human identities. Establish two cloud-only emergency-access accounts, tightly protect them, test them, and exclude them only from controls necessary to preserve recovery access. This is a widely used operational pattern; the exact Entra configuration and licensing need validation.
- Keep subscription Owner assignments to the minimum and at most three, following Microsoft RBAC guidance. Use Contributor or service-specific roles at resource-group scope for ordinary operators and developers.
- Use managed identities for Azure workloads and deployment automation where supported. Avoid long-lived client secrets; store unavoidable secrets in Key Vault with owners, expiry, rotation, and access logging.
- Use PIM or an approved equivalent just-in-time procedure for high-privilege roles if available under the business's licensing. Perform a quarterly access review at minimum, and promptly remove access when staff or supplier roles change.

### 3. Policy baseline and exceptions

Start with a versioned, policy-as-code initiative set. Assign policy at the narrowest management-group scope that meets the need.

| Control area | Initial action | Enforcement path |
| --- | --- | --- |
| Allowed regions | Restrict to one primary region and a documented recovery region after dependency and data-residency review. | Test in nonproduction, then deny. |
| Required metadata | Require/inherit `environment`, `workload`, `owner`, `costCenter` or equivalent, and `dataClassification` where applicable. | Modify/inherit where feasible; audit missing tags before deny. |
| Diagnostics | Audit that supported resources send required activity, security, and workload logs to the approved destination. | Deploy or modify only after access, retention, and cost are confirmed. |
| Security posture | Enable the applicable Microsoft cloud security baseline/Defender recommendations in audit mode. | Triage recommendations; enforce only controls justified by risk and tested impact. |
| Public exposure | Audit public network access and require explicit approval for internet-facing resources. | Deny public exposure where a private alternative is required and proven. |
| Data protection | Audit encryption, backup, soft delete, and recovery configuration for stateful services. | Enforce according to each workload's approved RTO/RPO and service support. |
| Expensive or prohibited services | Maintain a short list of services/SKUs that are expressly prohibited by cost, support, or risk. | Deny after a documented exception route exists. |

Every policy exception should identify the owner, business justification, compensating control, expiry date, and review date. Do not rely on a permanent exception simply to overcome an inconvenient baseline.

### 4. Network and workload placement

- Begin with direct PaaS access or a simple virtual network per workload when it meets the security and connectivity needs.
- Use hub-and-spoke only when private connectivity, central inspection, shared DNS, on-premises connectivity, or multiple virtual networks require common transit. Document address space before creating any virtual network, especially if on-premises integration is possible.
- Reserve Virtual WAN for requirements that meet its scale or connectivity rationale, not because it appears in a reference architecture.
- Classify every workload as internal, public-facing, or both. Place public endpoints behind the appropriate application-layer protection and isolate them from internal systems according to their data flows.
- Treat network security rules, DNS, private endpoints, and routing as IaC with peer review. Network changes can have broad blast radius.

### 5. Logging, monitoring, incident response, and backup

- Enable and retain Azure Activity Logs and diagnostic logs required to investigate control-plane changes, security events, and production failures. Validate log destinations, retention, access, and recurring costs before enforcing diagnostic settings broadly.
- Define a small actionable alert set: service health, subscription owner/RBAC or policy changes, backup failures, critical resource availability, capacity/quota risk, and budget threshold breaches. Every alert needs an owner and a response path.
- Write and test runbooks for: privileged access emergency, account/subscription recovery, suspected credential compromise, service outage, backup restore, failed deployment rollback, and cost anomaly.
- Assign a business owner, technical owner, RTO, RPO, backup method, retention period, and restore-test frequency to each stateful production workload. Do not claim a recovery target until a restore or failover test has demonstrated it.

### 6. Cost controls

- Estimate every production workload before approval using current pricing and document the assumption set (region, SKU, runtime hours, storage, egress, support, and observability).
- Set subscription and workload/resource-group budgets with a named business recipient and technical recipient. Configure actual and forecast alerts at conservative early thresholds, such as 50%, 80%, and 100%, then tune based on observed spend.
- Budgets notify but do not stop spend. Use policy, deployment approvals, scheduled shutdown where appropriate, quota controls, and documented response playbooks for stronger prevention.
- Review cost at least weekly during the first three months, then monthly if spending and workload change are stable. Review Azure Advisor and remove or resize idle resources before buying reservations or savings plans.
- Do not make long-term commitments until usage is stable and the business accepts the commitment risk.

### 7. IaC and change management

- Choose **one** primary IaC tool for the platform: Bicep if Azure-native tooling and Microsoft-first modules suit the team; Terraform if the team has established Terraform skills or a genuine multi-cloud need. Avoid two tools managing the same Azure control-plane resources.
- Store platform IaC, policy, role assignments, monitoring, budgets, and documentation in version control. Use separate environment parameters and prohibit subscription IDs, secrets, and credentials in source.
- Require pull-request review and a nonproduction plan/what-if before production changes. Require explicit approval for changes to management groups, policy effects, RBAC, networking, backups, and production data access.
- Use workload-specific IaC repositories or clearly separated directories. Record ownership and the exact deployment identity for each.
- Treat portal changes as exceptions: record the reason, add an IaC equivalent promptly, and reconcile drift.

## Management Model

For a small business, one person can fill more than one role, but each accountability must have a named primary and a named backup. A managed service provider can be Responsible for agreed technical operations; it should not silently become the unreviewed owner of business risk decisions.

| Activity | Executive sponsor | Cloud/platform owner | Workload owner | Security/privacy adviser | Finance owner / MSP |
| --- | --- | --- | --- | --- | --- |
| Risk appetite, budget, and recovery priorities | A | R | C | C | C |
| Landing-zone IaC, hierarchy, policies, and shared services | I | A/R | C | C | R where contracted |
| Workload architecture, data classification, and backup requirements | I | C | A/R | C | C |
| Access approvals and quarterly reviews | A | R | C | C | R where contracted |
| Security incident response | I | R | R | A/C | R where contracted |
| Cost review and optimization | A | R | R | I | R |
| Production change approval | A for high-risk changes | R | R | C | R where contracted |

`A` means accountable, `R` responsible, `C` consulted, and `I` informed. This is a proposed model, not a Microsoft-prescribed assignment.

### Operating cadence

| Cadence | Minimum activities |
| --- | --- |
| Daily / on alert | Triage actionable security, availability, backup, and budget alerts; record response and escalation. |
| Weekly | Review new policy noncompliance, failures, cost anomalies, unresolved alerts, changes, and upcoming high-risk work. |
| Monthly | Review spend against budget and forecast; Azure Advisor recommendations; security posture; backup success; open exceptions; resource ownership/tags. |
| Quarterly | Review RBAC and supplier access; test a representative restore; review policies, IaC dependencies, recovery targets, incident runbooks, and business owners. |
| Annually / after a major incident | Reconfirm risk appetite, regulatory needs, RTO/RPO, architecture fit, emergency access, and MSP contract/SLA. Conduct a lessons-learned review after material incidents. |

## Options and Trade-offs

| Option | Benefits | Costs or risks | Evidence and assumptions |
| --- | --- | --- | --- |
| Single subscription, portal-first | Lowest initial setup effort. Suitable for short-lived experimentation. | Weak production/nonproduction isolation, high configuration-drift risk, difficult delegated ownership and cost attribution. | Microsoft identifies subscriptions and management groups as governance scopes and recommends IaC; this option is an inference for limited proofs of concept. |
| Minimal governed landing zone: production + nonproduction subscriptions, shallow hierarchy, IaC, core policies | Strong early isolation and a practical operating baseline without dedicated empty platform subscriptions. | Requires initial design, source control, alerting, and named owners. | Recommended for the stated small-business assumption; supported by Microsoft's platform/workload separation, centralize-only-when-beneficial, IaC, policy, and operations guidance. |
| Full reference-aligned platform from day one: dedicated identity, connectivity, management, security, sandbox, multiple workload subscriptions | Supports complex hybrid networks, multiple teams, regulatory separation, and many workloads. | Higher recurring service cost, more deployment dependencies, more specialist skills, and more operational burden. | Appropriate only when actual requirements justify it; Microsoft presents the reference architecture as adaptable, not mandatory. |
| MSP-operated landing zone | Can supply monitoring, incident coverage, specialist skills, and operational discipline. | Shared-responsibility gaps, privileged access risk, unclear ownership, lock-in, and cost opacity if contracts and access controls are weak. | Requires a clear RACI, group-based access, auditability, service levels, exit process, and customer-controlled break-glass access. This is an operational inference. |

## Phased Implementation Plan

1. **Discover and decide (before deployment):** Inventory workloads and data; identify legal/regulatory obligations; name owners; define critical user flows, RTO/RPO, expected scale, budget, primary/recovery regions, internet exposure, on-premises/SaaS dependencies, and Azure/Entra licensing. Produce a one-page risk register and initial RACI.
2. **Establish the tenant and billing foundation:** Verify Microsoft Entra administration, emergency access, MFA/Conditional Access, billing ownership, support plan, cost recipients, and subscription naming. Do not begin production deployment until recovery access and billing responsibility are clear.
3. **Deploy the minimal platform with IaC:** Create management groups, production/nonproduction subscriptions, groups and RBAC, baseline tags, budgets, activity-log collection, initial alerts, and audit-mode policy. Store configuration, deployment instructions, and architecture decisions in source control.
4. **Pilot one nonproduction workload:** Deploy through the intended pipeline. Test access, policy behavior, tag/cost attribution, diagnostic data, alert routing, backup/restore, and deprovisioning. Fix friction and policy false positives before widening enforcement.
5. **Harden for production:** Approve workload-specific architecture; configure data protection, monitoring, recovery, incident runbooks, and production policy effects; complete a restore test; and secure formal sign-off on cost and RTO/RPO.
6. **Operate and evolve:** Hold the stated reviews, track exceptions, remediate drift, and add platform subscriptions or topology complexity only when a documented trigger occurs.

### Growth triggers

Reassess the target state when any of these occur: a second independently owned production workload; regulated or highly sensitive data; a need for private/on-premises connectivity; public workloads with shared ingress/egress controls; more than a small number of administrators; 24/7 availability commitments; material or unpredictable spend; mergers/multiple Entra tenants; a need to delegate workload teams; or evidence that manual operations and policy exceptions are recurring.

## Recommendation

Adopt the **minimal governed landing zone** option. Build production and nonproduction subscriptions under a shallow hierarchy, operate the foundation through a single IaC approach, and establish the identity, policy, logging, backup, budget, and ownership controls described above before hosting material production data or customer-facing services.

This recommendation fits a small business because it preserves the landing zone's meaningful control boundaries while limiting central components to ones that solve an actual problem. It also creates a path to the fuller Azure landing-zone reference architecture without forcing the business to operate enterprise networking and dedicated platform subscriptions before it has the workloads, staff, or risk profile to justify them.

Change this recommendation toward a more complete dedicated platform early when discovery shows hybrid connectivity, regulated data, multiple autonomous teams, high availability commitments, or a managed-services model requiring robust separation and auditing. Change it toward an even smaller proof-of-concept only when there is no production workload or sensitive data, the environment has a fixed end date, and the business explicitly accepts that it is not a production foundation.

## Open Questions and Limitations

- **Open questions:** What business processes will run in Azure? Which data classifications and regulations apply? What availability, recovery, and support hours are promised? Is on-premises, branch, partner, or SaaS private connectivity needed? Which Azure agreement, Microsoft Entra edition, and support plan are available? Will an MSP administer the platform? What are the target regions and data-residency constraints?
- **Unavailable evidence:** The repository contains no workload inventory, architecture, identity/licensing, financial, contractual, regulatory, or existing Azure configuration information. This brief therefore cannot validate a specific subscription count, network design, product SKU, policy definition set, RTO/RPO, or monthly cost.
- **Conflicting sources:** No material conflict was found among the reviewed Microsoft sources. The primary tension is intentional: enterprise reference diagrams show dedicated platform subscriptions and sophisticated network patterns, while the landing-zone guidance also says to centralize only capabilities with clear governance, operational, or economic benefit. This document resolves that tension as a small-business recommendation, not a direct Microsoft mandate.
- **Validation limitations:** Links and publication/update dates were reviewed from Microsoft Learn on the research date. The research did not deploy an Azure environment, price a workload, inspect applicable policy definitions, validate licensing, assess a specific regulatory regime, or test recovery. Verify current product availability, pricing, policy versions, and agreement-specific Cost Management behavior before implementation.

## Sources

- Microsoft Learn, [What is an Azure landing zone?](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/), updated 2026-07-31.
- Microsoft Learn, [Platform landing zone implementation options](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/implementation-options), updated 2025-12-15.
- Microsoft Learn, [Organize your resources with management groups](https://learn.microsoft.com/en-us/azure/governance/management-groups/overview), updated 2025-07-21.
- Microsoft Learn, [Azure identity and access management design area](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/identity-access), updated 2026-01-09.
- Microsoft Learn, [Best practices for Azure RBAC](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices), updated 2026-03-25.
- Microsoft Learn, [Overview of Azure Policy](https://learn.microsoft.com/en-us/azure/governance/policy/overview), updated 2026-07-08.
- Microsoft Learn, [Build a cloud governance team](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/govern/build-cloud-governance-team), updated 2026-03-09.
- Microsoft Learn, [Enforce cloud governance policies](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/govern/enforce-cloud-governance-policies), updated 2026-07-29.
- Microsoft Learn, [Ready your Azure cloud operations](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/manage/ready-cloud-operations), updated 2026-04-07.
- Microsoft Learn, [Optimize your cloud investment with Cost Management](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/cost-mgt-best-practices), updated 2026-05-21.
- Microsoft Learn, [Create and manage budgets](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/tutorial-acm-create-budgets), updated 2025-09-26.
- Microsoft Learn, [Overview of network topology and connectivity for Azure](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/network-topology-and-connectivity), updated 2026-01-09.
- Microsoft Learn, [Define an Azure network topology](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/define-an-azure-network-topology), updated 2025-10-29.
- Microsoft Learn, [Reliability design principles](https://learn.microsoft.com/en-us/azure/well-architected/reliability/principles), updated 2026-03-17.