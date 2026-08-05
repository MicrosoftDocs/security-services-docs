---
title: Threat Intelligence Agent
description: Use the Threat Intelligence Agent to analyze threat intelligence articles and profiles to extract attack patterns, indicators, and key threat objects.
ms.service: defender-xdr
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: how-to
ms.date: 07/30/2026
ms.update-cycle: 180-days
ai-usage: ai-assisted
appliesto:
- Project Perception
#customer intent: As a security analyst or threat intelligence analyst, I want to use the Threat Intelligence Agent in Microsoft Defender so that I can translate generic threat intelligence into actionable, organization-specific guidance.
---

# Threat Intelligence Agent

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

Threat intelligence reports are published constantly, but translating generic TI content into actionable, organization-specific guidance requires significant analyst effort. Teams struggle to keep up with the volume of intelligence and to understand its relevance to their specific environment. Extracting indicators, mapping them to MITRE ATT&CK, and generating hunting queries manually is time-consuming work that delays defensive action.

This agent analyzes threat intelligence articles and converts them into structured intelligence that security teams and other agents can consume. Rather than summarizing an article, the agent reasons over threat intelligence and environment context to extract actionable information, enriches findings with customer-specific context, and produces insights on how a specific threat applies to your organization.

The Threat Intelligence Agent serves as the entry point for the multi-agent **Protect against a threat** playbook, where its output feeds directly into the Recon Agent, Posture Prioritization Agent, and Detection Authoring Agent.

Use this article to review capabilities, prerequisites, and run steps.

## Key capabilities

The Threat Intelligence Agent runs multi-step, AI-orchestrated analysis of threat intelligence content.

- **Extracts structured intelligence objects**: Identifies IOCs, TTPs, malware families, CVEs, and threat actor information from unstructured threat intelligence reports.
- **Maps techniques to MITRE ATT&CK**: Identifies attacker techniques and maps them to the MITRE ATT&CK framework with evidence from the source intelligence.
- **Assesses relevance to your specific environment**: Analyzes how the threat maps to your organization's industry, technology stack, and environment.
- **Generates hunting queries scoped to your telemetry**: Creates KQL hunting queries tailored to your Defender XDR data sources to search for indicators of the threat.
- **Produces prioritized defensive recommendations**: Provides actionable defensive steps ranked by impact and feasibility for your environment.
- **Integrates with Microsoft Defender Threat Intelligence**: Enriches extracted IOCs with additional context from Microsoft Defender Threat Intelligence (MDTI) when available.
- **Feeds downstream agents**: Provides structured intelligence that the Detection Authoring Agent, Recon Agent, and Posture Prioritization Agent consume in multi-agent playbooks.

## Before you begin

### Prerequisites

The following products are required for the Threat Intelligence Agent:

- Microsoft Defender XDR
- Microsoft Defender Threat Intelligence (MDTI) for full TI data access and enrichment

### Permissions granted to the agent

During agent configuration, you grant the agent the following permissions:

- **Microsoft Defender XDR API permissions**:
  - ThreatIntelligence.Read.All
  - ThreatHunting.Read.All
  - AdvancedHunting.Read.All
- **Microsoft Defender Threat Intelligence API permissions**:
  - ThreatIntelligence.Read.All
- **Microsoft Graph API permissions:**
  - SecurityEvents.Read.All

## Set up the Threat Intelligence Agent

To set up this agent, follow the steps in [Set up an agent](agentic-security-get-started.md#path-2-set-up-and-run-an-agent).

## Start a Threat Intelligence Agent session

For ways to start a session, see [Start a new session](agentic-security-sessions.md#start-a-new-session).

This agent runs through the following playbooks:

| Playbook | Required input |
|---|---|
| **Extract threat intelligence** | A threat intelligence article URL, threat actor profile, or TI report. You can provide a URL from Microsoft Defender Threat Intelligence, a third-party TI provider, or select an article from the Defender portal. |
| **Protect against a threat** | A threat intelligence article. |

> [!NOTE]
> You can also start this agent directly from a threat intelligence article in the Defender portal. For more information, see [Run playbooks from incidents and threat intelligence](agentic-security-integration-scenarios.md).

## Approve the task plan

After generating its initial task plan, the agent pauses and displays a message indicating that your input is needed. The session status changes to **Waiting for input**.

You have three options:

|Option|What it does|
|---|---|
|**Approve**|Confirms the plan. The agent proceeds with its work.|
|**Deny and redirect**|Rejects the current plan and lets you provide different instructions. The agent generates a revised plan for your review.|
|**Ask a question**|Lets you ask about the plan without committing. Use this to understand what the agent will access before approving.|

## Monitor session progress

While the session runs, the session detail panel shows:

- **Summary**: Current session status and a summary of work done.
- **Progress**: Tracks completed steps in the threat intelligence analysis.
- **Agents**: The Threat Intelligence Agent assigned to this session.
- **Inputs**: The threat intelligence source you provided.
- **Artifacts**: Output files generated so far, updated as the session progresses.

### Session status values

[!INCLUDE [session-status-table](includes/session-status-table.md)]

## Review the output

The Threat Intelligence Agent produces a comprehensive threat intelligence analysis report containing the following sections:

- **Executive summary**: A concise overview of the threat, its targeting patterns, and key risks to your organization.
- **Threat actor profile**: Summary of the threat actor's TTPs, known targeting patterns, and historical activity if analyzing an actor-focused report.
- **Extracted IOCs**: A structured list of indicators of compromise including:
  - IP addresses
  - Domain names
  - File hashes (MD5, SHA-1, SHA-256)
  - URLs
  - Email addresses
  - Each IOC includes enrichment data from Microsoft Defender Threat Intelligence where available.
- **MITRE ATT&CK mapping**: Observed threat techniques mapped to the MITRE ATT&CK framework with evidence from the source intelligence.
- **Environmental relevance assessment**: Analysis of how the threat maps to your organization's industry, technology stack, and environment. This section answers: "Should we be concerned about this threat?"
- **KQL hunting queries**: Ready-to-use KQL queries scoped to your Microsoft Defender XDR telemetry to search for indicators of the threat in your environment.
- **Defensive recommendations**: Prioritized actions for detection, prevention, and mitigation ranked by impact and feasibility. Recommendations may include:
  - Detection rule updates
  - Configuration hardening
  - IOC blocking
  - User awareness guidance
  - Hunting activities

The report output appears as a markdown file in the **Artifacts** section of the session detail view. The KQL hunting queries are also provided as separate text files for easy execution in the Microsoft Defender portal.

> [!IMPORTANT]
> Threat Intelligence Agent outputs are AI-generated and grounded in data available through threat intelligence sources and Defender XDR APIs. Always review findings for accuracy and validate hunting queries in a test environment before running them in production.

## Run hunting queries

After reviewing the output, you can execute the hunting queries:

1. Copy the KQL query from the output artifacts.
2. In the Microsoft Defender portal, go to **Hunting** > **Advanced hunting**.
3. Paste the KQL query in the query editor.
4. Review the query logic and adjust time ranges or filters as needed.
5. Select **Run query** to search for indicators in your environment.
6. Review results and escalate any confirmed matches to your incident response process.

## Related content

- [What is Project Perception?](agentic-security-overview.md)
- [Understand key concepts in Project Perception](agentic-security-concepts.md)
- [Work with agents](agentic-security-agents.md)
- [Monitor and manage agent sessions](agentic-security-sessions.md)
- [Detection Authoring Agent](detection-authoring-agent.md)
- [Attack Investigation Agent](attack-investigation-agent.md)
- [Triage Agent](triage-agent.md)
