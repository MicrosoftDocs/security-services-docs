---
title: Red team agent considerations 
description: Understand intended use, limitations, warning language, risks, and operational considerations for Project Perception Red team agents.
ms.service: defender-xdr
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: concept-article
ms.date: 07/31/2026
ms.update-cycle: 180-days
ai-usage: ai-assisted
appliesto:
- Project Perception
ms.custom: Project Perception
#customer intent: As a security stakeholder, I want to understand the intended uses, limitations, warnings, and operational safeguards for Red team agents so that I can deploy them safely in approved environments.
---

# Red team agent considerations 

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

This article consolidates stakeholder guidance from the Red team agents warning document and captures the required considerations for planning and operating Red team agents.


## Capabilities

Red team agents help security teams understand and validate real-world risk across cloud environments. Together, these agents can analyze:

- Tenant topology
- Identities and permissions
- Network exposure
- Misconfigurations
- Attack paths
- MITRE ATT&CK mapping
- Detection coverage

Each agent supports a specific workflow stage, from read-only reconnaissance to controlled validation and consent-driven hardening, with prioritized, evidence-backed outputs intended to be understandable for security teams that might not have deep red team specialization.

## Intended uses

Red team agents are intended for authorized security professionals assessing real-world risk in approved, controlled environments. Supported uses include:

- Cloud assessments
- Identity and privilege escalation analysis
- Internet exposure verification
- Remediation validation
- Targeted threat investigations

Red team agents support the red team lifecycle from reconnaissance and attack path discovery to controlled validation, detection gap analysis, and posture improvement.

Red team agents are not intended for:

- Real-time or unattended operation
- General-purpose AI assistance
- Use outside authorized and scoped security assessments

Human approval is required before agent actions proceed. Customers are responsible for ensuring that all assessment targets are assets they own or are explicitly authorized to test.

## Limitations

Red team agents operate with important constraints:

- Some capabilities (such as virtual machine and server coverage) require additional onboarding.
- Each session is limited to one target environment.
- Multi-environment assessments require separate sessions and aren't aggregated.
- Results are point-in-time and can become stale after significant configuration changes.

The quality and completeness of output also depend on the permissions granted to the configured agent identity.

## Warning language

The following warning statements should be treated as required guidance:

- **The quality and completeness of output depend on the permissions granted to the agent identity, and insufficient access produces incomplete analysis and can cause missed attack paths or misconfiguration signals.**
- **Agent outputs are AI-generated and can contain errors or inaccuracies; human review is always required before acting on findings.**
- Session details and output can be visible to other authorized users depending on tenant permissions.
- Because Red team agents are in Public Preview, capabilities are subject to change and outputs should be treated as prerelease.

## Risks

- **Authorized scope is required.** Using agents on assets not owned by your organization or not explicitly authorized for testing can introduce legal and security risk.
- **Overreliance on AI-generated outputs.** Findings can be incorrect or incomplete if used without human review. Confidence labels (confirmed, likely, inferred) should be used to calibrate analyst judgment.
- **Active exploit validation can affect environments.** Run active validation only with explicit authorization, change management approval, and clearly defined scope.
- **Sensitive output disclosure risk.** Session artifacts can include sensitive environment details and should be handled with controls comparable to penetration testing reports.
- **Misconfigured identities and permissions can reduce security and result quality.** Overly broad access can violate least privilege, while insufficient access can degrade analysis.

## Operational considerations

Successful deployment requires coordinated preparation across identity, permissions, process, and operations:

- Configure each agent identity with least privilege and clear auditability. A purpose-built Microsoft Entra agent identity is recommended.
- Validate per-agent permission and SKU prerequisites during setup.
- Ensure users who start or steer sessions have required access.
- Use the mandatory human-in-the-loop (HITL) checkpoint to review and explicitly approve planned task lists before environment access.
- Define organizational usage policy for which agents can be used, by whom, in which environments, and under what approvals.
- Apply formal change management controls, especially for workflows involving active exploitation or environment changes.
- Monitor Security Compute Unit (SCU) consumption during larger sessions to avoid impacting other workloads.
- Introduce agents in nonproduction environments first to build operator readiness before broader rollout.

## Evidence of accuracy, performance, and generalizability

Source evaluation notes indicate Red team agents were assessed pre-release using a structured framework aligned to customer jobs-to-be-done and measurable thresholds in SOC scenarios.

### Quality dimensions used in evaluation

- Groundedness (whether findings are substantiated by retrieved data)
- Coherence (logical consistency)
- Fluency (clarity and readability)
- Similarity to expected benchmark results

### Safety and control dimensions used in evaluation

- Red teaming and adversarial prompt testing
- AI-assisted annotation aligned to Microsoft safety standards
- Safeguards including read-only architecture (where applicable), HITL approvals, role-based access control, and managed identity constraints

### Generalizability constraints

Generalizability is influenced by:

- Completeness of granted permissions
- Breadth of onboarded security products
- Richness of available identity and network configuration data

When environmental data is limited, findings are expected to degrade gracefully and be labeled accordingly rather than overclaim confidence.

## Next steps

- [Work with agents](agentic-security-agents.md)
- [Work with playbooks](agentic-security-playbooks.md)
- [Approve, reject, or stop agentic work](agentic-security-supervise-work.md)
