---
title: Posture Prioritization Agent 
description: Learn how the Posture Prioritization Agent analyzes posture findings and produces an explainable, prioritized action plan based on risk, exploitability, exposure, asset criticality, and available signals.
ms.service: defender-xdr
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.collection:
  - m365-security
  - tier1
  - security-copilot
ms.topic: how-to
ms.date: 08/03/2026
appliesto:
- Project Perception
ms.custom: Project Perception
ai-usage: ai-assisted
---

# Posture Prioritization Agent

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

The Posture Prioritization Agent helps security teams and stakeholders across the organization understand what to fix first and why. The agent supports two scenarios: **broad posture prioritization** for routine remediation planning, and **threat-driven posture response** for understanding exposure to a specific threat. In both cases, the agent analyzes posture findings and produces an explainable, prioritized action plan based on risk, exploitability, exposure, asset criticality, and available Defender signals. In preview, the agent is read-only and focuses on cloud and device posture scenarios.

The agent's core value is in cutting through large volumes of posture findings to surface what actually matters:

- **Reduces manual triage** - ingests posture findings at scale so security admins and vulnerability management teams don't have to sort through them manually.
- **Produces a ranked action plan** - delivers an ordered list of remediation actions, not a raw dump of findings.
- **Explains the reasoning** - for every prioritized action, the agent provides the rationale, the supporting evidence, and the impact of not acting, so teams can justify decisions to stakeholders.
- **Uses real-world risk signals** - rankings reflect real-world risk signals, not just severity scores.


## Why use the Posture Prioritization Agent?

The Posture Prioritization Agent addresses the pre-breach side of security - the work that happens before an attack occurs. Security admins and vulnerability management teams maintain a continuous queue of posture recommendations: patch this software, fix this network configuration, close this exposure. The challenge is not a shortage of recommendations - it's knowing which ones to act on first to maximally reduce risk.

The Posture Prioritization Agent reduces that manual triage burden. It ingests posture findings across your cloud assets and devices and produces a ranked action plan with explainable, risk-based prioritization. The agent does not only rank findings; it explains why each action is prioritized, what signals influenced the decision, and what evidence supports the recommendation. It also communicates the impact of not addressing each item, so teams can justify prioritization decisions to stakeholders. This reasoning is central to how security teams can trust and communicate the output.


## Scenarios

The Posture Prioritization Agent supports the following scenarios:

| | Broad posture prioritization | Threat-driven posture response |
|---|---|---|
| **Question it answers** | *"What should I fix first in my environment?"* | *"Am I exposed to this threat, and what should I do?"* |
| **When to use** | Routine posture management - no specific threat in mind | A specific threat has surfaced and you need to understand your exposure |
| **Input required** | None | Threat intelligence article URL, threat actor name, CVE, or TTPs |
| **Playbook** | Plan for posture remediation | Protect against a threat |
| **How it works** | Evaluates posture signals across your environment and produces a prioritized action plan | Maps threat techniques to your posture findings first, then ranks remediation in the context of that specific threat |

### Broad posture prioritization

Use this scenario for ongoing posture management. No threat input is required. The agent evaluates posture signals across your cloud assets and devices and produces a prioritized action plan. For details on how findings are ranked, see [Report contents](#report-contents).

**Playbook:** Plan for posture remediation

### Threat-driven posture response

Use this scenario when a specific threat has surfaced and you need to understand your exposure. The agent maps threat techniques to your posture findings before prioritizing, so the output is scoped to what matters for that specific threat rather than your full posture queue.

**Playbook:** Protect against a threat  
**Required input:** A threat intelligence article URL, threat actor name, CVE, or set of TTPs

> [!NOTE]
> These are distinct flows with different outputs. The **Protect against a threat** playbook applies a threat-scoped lens to posture analysis before prioritization. The **Plan for posture remediation** playbook prioritizes directly against your current posture findings without a threat filter.

## Before you begin

Confirm the required product availability, licensing, permissions, and configuration before you use the Posture Prioritization Agent.

### Prerequisites

To run the Posture Prioritization Agent in your environment, you need:

- Microsoft 365 E5


Microsoft Defender for Cloud with Defender Cloud Security Posture Management (CSPM) enabled is required on the subscription level for Cloud signals. Enabling additional plans surfaces more posture signals for the agent to work with. For more information, see [What is Cloud Security Posture Management (CSPM)](/azure/defender-for-cloud/concept-cloud-security-posture-management).

For more information about unified RBAC in the Defender portal, see [Microsoft Defender XDR Unified role-based access control (RBAC)](/defender-xdr/manage-rbac).

## Set up the Posture Prioritization Agent

To set up this agent, follow the steps in [Set up an agent](agentic-security-get-started.md#path-2-set-up-and-run-an-agent).

## Start a Posture Prioritization Agent session

For ways to start a session, see [Start a new session](agentic-security-sessions.md#start-a-new-session). This agent supports two playbooks with different scenarios. Select the one that matches your current need.

> [!NOTE]
> These are distinct flows. The **Protect against a threat** playbook applies a threat-scoped lens to posture analysis before prioritization. The **Plan for posture remediation** playbook applies prioritization directly to your current posture findings without a threat filter.

### Plan for posture remediation

**Scenario (Broad posture prioritization):** *"What should I fix first in my environment?"*

Use this playbook when you want a ranked remediation plan based on your current cloud and device posture findings. No threat input is required. The agent evaluates posture signals across your environment and produces a prioritized action plan.

1. Go to **Playbooks**.
2. Select the **Plan for posture remediation** playbook.
3. Select **New session**.
4. Select **Start session**.

### Protect against a threat

**Scenario (Threat-driven posture response):** *"A new threat dropped. Am I exposed, and what should I do?"*

Use this playbook when a specific threat has surfaced and you want to understand your exposure and prioritize remediation accordingly. The agent maps the threat to your posture findings before prioritizing.

1. Go to **Playbooks**.
2. Select the **Protect against a threat** playbook.
3. Select **New session**.
4. Provide the required threat input: a threat intelligence article.
5. Select **Start session**.



## Monitor session progress

When a session starts, the agent creates a session in Project Perception. To view and manage sessions, go to **Agents**, locate the Posture Prioritization Agent under **Agents in use**, and select **Go to agent**.

The Posture Prioritization Agent page includes the following tabs:

[!INCLUDE [agent-page-tabs](includes/agent-page-tabs.md)]

[!INCLUDE [manage-agent-ellipsis](includes/manage-agent-ellipsis.md)]

## Understand the report

>[!NOTE]
> Results may vary between runs. This does not mean the recommendations are incorrect. Each recommended action is evaluated against the available risk signals and evidence at the time of analysis.

When a session completes, select **Summary** in the session interface to view the session summary. Full output files are also available as downloadable Markdown files in the **Outputs** section of the session details panel. The output is the primary result of a run. It contains the top exposures to prioritize to reduce risk in your environment.

You can follow up on the report in the session chat interface. Ask the agent to explain a specific action, focus on a particular workload, or provide more detail on the reasoning behind a recommendation.

### Report contents

The session summary includes:

- **Headline** - A concise overview of the session findings and key outcomes.
- **What happened** - A narrative describing what the agent analyzed and what it found.
- **What to do next** - A prioritized list of recommended remediation actions.

Full output is also available as downloadable Markdown files in the **Outputs** section of the session details panel.


## Preview scope and limitations

The following scope and limitations apply during preview:

| Scope | Details |
|---|---|
| **Read-only** | The agent analyzes and recommends; it does not make changes to your environment or enforce remediation actions |
| **Cloud and device posture** | In preview, the agent focuses on cloud assets and devices.|
| **Defender signals only** | The agent works with posture signals available in your Defender environment. Third-party CSPM data and signals from external sources are not supported in preview.|



## Related content

- [What is Project Perception?](agentic-security-overview.md)
- [Understand key concepts in Project Perception](agentic-security-concepts.md)
- [Work with agents](agentic-security-agents.md)
- [Monitor and manage agent sessions](agentic-security-sessions.md)
- [Recon Agent](recon-agent.md)
