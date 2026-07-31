---
title: Detection Authoring Agent in Microsoft Defender
description: Learn how the Detection Authoring Agent helps security operations teams create, refine, and validate detection rules to improve threat coverage.
ms.service: defender-xdr
ms.localizationpriority: medium
ms.author: macapara
author: mjcaparas
ms.collection: 
- m365-security
- tier1
- security-copilot
- magic-ai-copilot 
ms.topic: how-to
ms.date: 07/31/2026
ms.update-cycle: 180-days
ai-usage: ai-assisted
appliesto:
- Project Perception
#customer intent: As a security analyst, I want to learn about the Detection Authoring Agent in Microsoft Defender so that I can create and improve detection rules efficiently and expand my organization's threat coverage.
---

# Detection Authoring Agent in Microsoft Defender


[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

Detection gaps are a persistent challenge for security operations teams. Building effective custom detections requires analysts to understand attacker behaviors, available data schemas, and query logic before they can create rules that are useful in their environment.

The Detection Authoring Agent helps analysts generate custom detection recommendations from threat intelligence and accelerate the creation of custom detection rules. The Detection Authoring Agent operates as part of the proactive protection workflow. The proactive protection workflow is the end-to-end process that starts with a Threat Intelligence (TI) article and uses multiple agents to turn threat intelligence into actionable detections. The Threat Intelligence Agent analyzes the TI article and extracts information about attacker behaviors and techniques. The Detection Authoring Agent uses that analysis to generate custom detection recommendations that help security teams identify similar activity in their environment.

The agent provides a Detection Coverage Report that includes:

- **Proposed detections** with KQL query logic and explanations of the query approach, selected tables, and schemas, along with frequency and lookback configurations, and full detection and alert enrichment including title, description, severity, MITRE tactics and techniques, entity mapping configuration, and recommended actions to help analysts act on the alert if it triggers.
- **Additional information in each proposed detection**, including the strategy used to generate it, alert volume estimation, known benign sources, parameter tuning recommendations, and potential limitations to consider before deploying the detection.
- **Existing custom detections and analytics rules** that already cover similar behaviors, so detection engineers can review them and avoid creating duplicates.

Analysts can review the recommendations, ask follow-up questions about the report, and open a suggested detection in the custom detection wizard to review, adjust, and save it. Saving the detection is what activates it in the tenant.

> [!IMPORTANT]
> The Detection Authoring Agent is available in preview. Features and behavior may change before general availability.

## Why use the Detection Authoring Agent?

Building high-fidelity detections requires detection engineers to understand attacker tradecraft, map behaviors to detection logic, and validate rules against real data without generating excessive noise. The Detection Authoring Agent acts as an autonomous detection engineer in Microsoft Defender, helping detection engineers expand threat coverage faster by generating detection recommendations based on threat intelligence and observed attack patterns.

In the proactive protection workflow, the detection engineer starts from a threat intelligence article. The Threat Intelligence Agent analyzes the article and produces Tactics, Techniques, and Procedures (TTPs), and the Detection Authoring Agent uses those TTPs to recommend detections. Detection engineers can continue refining detection rules, adjusting thresholds, and exploring coverage gaps through an interactive chat experience.

### Use cases

| Use case | Detection Authoring Agent |
| --------------- | ----------- |
| **Generate detection recommendations from threat intelligence** | Creates proposed KQL-based detections that help cover attacker behaviors identified in a threat intelligence article. |
| **Map detection coverage to MITRE ATT&CK** | Identify which techniques are covered by existing rules and surface gaps in detection coverage. |
| **Review detection tuning recommendations** | Provides recommendations to help detection engineers tune proposed detections for their environment. |
| **Explain detection rationale** | Provide plain-language explanations of what each rule detects and why the logic is structured that way. |
| **Create a custom detection from a recommendation** | Opens the suggested detection in the custom detection wizard with fields such as frequency, severity, MITRE techniques, alert details, and entity mapping prefilled. |
| **Ask follow-up questions about the report** | Lets detection engineers use the agent chat to ask questions about the detection report and its output. |

## Before you begin

Confirm the required product availability, licensing, permissions, and configuration before you use the Detection Authoring Agent.

### Prerequisites

To run the Detection Authoring Agent in your environment, you need:

- **Security Copilot**: Provisioned capacity in Security Compute Units (SCU). See [Get started with Security Copilot](/copilot/security/get-started-security-copilot).
- **Plugins**: The Detection Authoring Agent automatically activates these Security Copilot plugins: Microsoft Defender XDR, Microsoft Threat Intelligence, and Microsoft Sentinel (if applicable).
- **Unified RBAC**: Enable unified role-based access control and activate the relevant workloads for the data sources you want to query. For more information, see [Workload-specific prerequisites](/defender-xdr/triage-agent#workload-specific-prerequisites).

### Additional permissions required

To use the Detection Authoring Agent, you also need the following permissions in Microsoft Defender XDR:

- **Security data basics for all workloads**: Read
- **Custom detection rules**: Read and Write
- **Advanced hunting**: Read

For more information about unified RBAC in the Defender portal, see [Microsoft Defender XDR Unified role-based access control (RBAC)](/defender-xdr/manage-rbac).

## Set up the Detection Authoring Agent

To set up this agent, follow the steps in [Set up an agent](agentic-security-get-started.md#path-2-set-up-and-run-an-agent).

## Start a new Detection Authoring Agent session

For ways to start a session, see [Start a new session](agentic-security-sessions.md#start-a-new-session).

This agent runs through the following playbook:

| Playbook | Required input |
|---|---|
| **Protect against a threat** | A threat intelligence article. |

[!INCLUDE [manage-agent-ellipsis](includes/manage-agent-ellipsis.md)]

After the session starts, the proactive protection workflow analyzes the selected threat intelligence article and generates a **Detection Report**. The report includes recommended detections, detection logic, and supporting information that help analysts understand how the recommendations address threats identified in the article.

## Review the Detection coverage report

When a session completes, the agent generates output that appears in the Summary view.

You can ask follow-up questions on the report in the chat interface.

The agent essentially provides a proposal for detections that will cover the threats that appear in the TI article. Multiple detections are usually proposed per TI article. Each detection has a **Threat summary**, the **Methodology and strategy**.

Within the report in the Detections section, select **Open in wizard** to open the proposed detection in the Microsoft Defender **Custom detection** wizard. Review and modify the detection settings as needed, and then save the detection rule.

### Tenant-aware detection analysis and tuning

Unlike generic detection recommendations, the agent tailors every proposal to your specific environment. It does this through three core capabilities:

**Tenant-aware detection creation**

The agent identifies which tables and data sources are available in the tenant and bases its recommendations on that data. This means every proposed detection is grounded in what your environment actually collects, rather than assuming data availability that may not exist.

**Detection simulation and noise estimation**

For each proposed detection, the agent runs a simulation against historical tenant data and reports the projected alert volume. This gives you an early indication of the detection's expected coverage, potential noise level, and overall quality before you deploy it.

**Automated tenant-specific tuning**

Based on simulation results, the agent identifies detections likely to be noisy and automatically suggests optimizations. By analyzing the generated alerts, it can detect recurring benign patterns and refine the rule accordingly. For example, if a specific user, device, or application appears frequently in simulated alerts and is assessed as benign, the agent may recommend excluding it from the detection logic.

#### Detection categories

Based on the results and tenant-specific baselines, proposed detections are automatically categorized into two groups:

- **Ready to deploy**: Detections expected to be high quality and relatively low noise compared to other custom detections in the environment. These can typically be enabled with minimal additional review.
- **Requires tuning**: Detections expected to generate a relatively high level of noise based on simulation results and tenant-specific characteristics. The agent provides concrete recommendations to improve their quality before deployment.

#### Detection provider

Detections proposed by the agent are tagged with a **Provider** value of **Copilot**. You can use this property to filter and identify agent-generated detections in your custom detections list.


## Related content

- [What is Project Perception?](agentic-security-overview.md)
- [Understand key concepts in Project Perception](agentic-security-concepts.md)
- [Work with agents](agentic-security-agents.md)
- [Monitor and manage agent sessions](agentic-security-sessions.md)
- [Threat Intelligence Agent](threat-intelligence-agent.md)
- [Attack Investigation Agent](attack-investigation-agent.md)
- [Triage Agent](triage-agent.md)
