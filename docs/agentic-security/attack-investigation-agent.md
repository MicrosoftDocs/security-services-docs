---
title: Attack Investigation Agent
description: Learn how to set up and use the Attack Investigation Agent to reconstruct attacks from alerts, incidents, and related security signals.
ms.service: project-perception
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: how-to
ms.date: 08/05/2026
ms.custom: Project Perception, msecd-doc-authoring-1015
ms.update-cycle: 180-days
ai-usage: ai-assisted
appliesto:
- Project Perception
#customer intent: As a security analyst, I want to use the Attack Investigation Agent in Microsoft Defender so that I can reconstruct the full attack story and produce analyst-ready insights without manual correlation work.
---

# Attack Investigation Agent

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

The Attack Investigation Agent is an autonomous tier 2 investigator for security operations teams. Starting from a single alert or incident, the agent correlates signals in Microsoft Defender to reconstruct the attack story, scope, and impact.

You can start an investigation with or without prior triage by an analyst or the Triage Agent. This article describes the agent's capabilities and prerequisites. It also explains how to set up the agent, run and monitor a session, and review the results.

## Key capabilities

The Attack Investigation Agent runs a multi-step, AI-orchestrated investigation that:

- **Reconstructs the full attack story**: Explains who attacked, how they gained access, which resources they affected, and the scope and impact of the attack. The agent goes beyond individual alerts.
- **Provides clear, actionable answers**: Explains the attack scope, initial access, progression, technical impact, investigation status, and classification.
- **Investigates a broad range of attacks**: Investigates attacks involving users, devices, cloud apps, containers, and other entities without relying on a predefined scenario.
- **Supports interactive investigation**: Lets analysts chat with the agent throughout the investigation to ask questions or request deeper analysis.
- **Adapts to your environment**: Uses multiple data sources and follows your organization's policies and practices.

## Prerequisites

### Required licenses

To use the Attack Investigation Agent, your organization needs:

- Microsoft 365 E5
- Microsoft Defender XDR

For broader investigation coverage, the recommended products depend on the attack type:

- **Cloud and container attacks**:
  - Microsoft Defender for Cloud
  - Microsoft Defender for Containers
- **Identity attacks**:
  - Microsoft Entra ID P2
  - Microsoft Defender for Identity
  - Microsoft Defender for Cloud Apps

### Recommended role-based access control

Use [Microsoft Defender unified role-based access control (RBAC)](/defender-xdr/manage-rbac). This configuration is recommended for investigation quality and coverage.

### Recommended configuration for phishing investigations

For the best coverage and investigation quality in user-reported phishing investigations, configure the following settings:

- **Microsoft Defender for Office 365**: Configure the following [user reported settings](/defender-office-365/submissions-user-reported-messages-custom-mailbox):
  - Select **Monitor reported messages in Outlook**.
  - Configure user reported messages to go to the reporting mailbox, to Microsoft, or both. If you use a [non-Microsoft reporting tool](/defender-office-365/submissions-user-reported-messages-custom-mailbox#options-for-non-microsoft-reporting-tools), configure the tool so reported messages go to Microsoft and the reporting mailbox or to the reporting mailbox only.
- **Microsoft Defender**:
  - Enable the **Email reported by user as malware or phish** alert policy. For more information, see [Alert policies in Microsoft Defender](/defender-xdr/alert-policies).
  - Disable the built-in **Auto-Resolve - Email reported by user as malware or phish** alert tuning rule and any custom tuning rules that resolve this alert. For more information, see [Tune an alert](/defender-xdr/investigate-alerts#tune-an-alert).

## Set up the agent

To set up this agent, follow the steps in [Set up an agent](agentic-security-get-started.md#path-2-set-up-and-run-an-agent).

## Start a session

For ways to start a session, see [Start a new session](agentic-security-sessions.md#start-a-new-session).

The Attack Investigation Agent uses the following playbook:

|Playbook|Required input|
|---|---|
| **Investigate attack** | The ID of a single alert or incident from the Microsoft Defender portal. |

> [!NOTE]
> You can also start this agent directly from an alert or incident detail page in the Defender portal. For more information, see [Run playbooks from incidents and threat intelligence](agentic-security-integration-scenarios.md).

## Monitor session progress

While the session runs, the session detail panel shows:

- **Summary**: Current session status and completed work.
- **Progress**: Completed investigation steps.
- **Agents**: The agent assigned to the session.
- **Inputs**: The alert or incident ID you provided.
- **Artifacts**: Output files generated during the investigation.

### Session status values

|Status|Description|
|---|---|
|**In progress**|The agent is actively working.|
|**Completed**|The session finished successfully, and all output is available.|
|**Completed with failures**|The session finished with one or more problems. Review the session details for more information.|

## Review the output

The Attack Investigation Agent produces an investigation report with the following sections:

- **Executive summary**: An overview of the attack for stakeholders and escalation.
- **Incident verdict**: Classification as true positive, false positive, or benign with transparent reasoning.
- **Attack timeline**: A chronological sequence of key events showing the progression of the attack from initial access through post-compromise activity.
- **Affected entities**: Identified users, devices, and applications affected by the attack.
- **MITRE ATT&CK techniques observed**: Mapping of observed attacker behavior to MITRE ATT&CK techniques with evidence for each technique.
- **Indicators of compromise**: Extracted and enriched indicators of compromise (IOCs), including IP addresses, domains, file hashes, URLs, and email addresses with threat intelligence context.
- **Recommended next steps**: Prioritized actions for containment, remediation, and prevention.

The report appears as a Markdown file in the **Artifacts** section of the session details. You can download the report to add to incident documentation or compliance records.

> [!IMPORTANT]
> Attack Investigation Agent output is AI-generated and grounded in data available through Defender APIs. Always review the findings for accuracy before you make remediation decisions or communicate the findings to stakeholders.

## Related content

- [What is Project Perception?](agentic-security-overview.md)
- [Understand key concepts in Project Perception](agentic-security-concepts.md)
- [Work with agents](agentic-security-agents.md)
- [View and manage sessions](agentic-security-sessions.md)
- [Recon Agent](recon-agent.md)
- [Triage Agent](triage-agent.md)
