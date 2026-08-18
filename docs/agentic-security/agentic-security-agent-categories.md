---
title: Agent categories in Project Perception
description: Learn how red team, blue team, and green team agents work together in Project Perception to expose gaps, detect threats, and harden your security posture.
ms.service: project-perception
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
ai-usage: ai-assisted
appliesto:
- Project Perception
ms.custom: Project Perception
#customer intent: As a security professional, I want to understand how red team, blue team, and green team agents are categorized in Project Perception so that I can use the right agents for the right security objectives.
---

# Agent categories in Project Perception


[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

Each agent in Project Perception belongs to one of the following categories, identified by color: red team, blue team, or green team. The category reflects the agent's role in a coordinated defense system. Red team agents find and expose gaps. Blue team agents detect, triage, and investigate. Green team agents remediate and harden your posture. Together, they form a multi-agent defense that responds continuously to threats.

:::image type="content" source="media/red-blue-green-agents.png" alt-text="Illustration of the categories of agents":::


## Red team agents

Red team agents simulate attacker behavior to expose vulnerabilities before adversaries can exploit them. They map your environment, identify attack paths, and surface gaps in your defenses so you can act before a real attack occurs.

| Agent | What it does |
|---|---|
| [**Recon Agent**](recon-agent.md) | Performs attacker scouting activities to map your environment, surface attack paths, choke points, valuable assets, configuration issues, and excess permissions. |

## Blue team agents

Blue team agents detect, triage, and investigate threats. They operationalize threat intelligence, close coverage gaps, triage alerts, reconstruct attack stories, and author new detections to keep your defenses current.

| Agent | What it does |
|---|---|
| [**Triage Agent**](triage-agent.md) | Classifies and resolves alerts as true or false positives, with detailed explanations behind its conclusions. It learns from context and feedback to improve accuracy over time. |
| [**Threat Intelligence Agent**](threat-intelligence-agent.md) | Extracts attack patterns, indicators, and key threat intelligence objects, then analyzes them to identify how to defend against or respond to a threat. |
| [**Attack Investigation Agent**](attack-investigation-agent.md) | Reconstructs the full attack story by correlating alerts, incidents, and security signals. It provides analyst-ready insights, including verdicts, timelines, techniques, indicators of compromise, and affected entities. |
| [**Detection Authoring Agent**](detection-authoring-agent.md) | Identifies gaps in threat coverage and creates detection rules to improve defenses as threats evolve. |

## Green team agents

Green team agents remediate and harden your security posture. They evaluate exposure, prioritize fixes by real-world risk, and surface the actions that reduce risk most effectively.

| Agent | What it does |
|---|---|
| [**Posture Prioritization Agent**](posture-prioritization-agent.md) | Ranks posture issues by real-world risk, exposure, exploitability, and asset criticality. It provides focused guidance on what to fix first and why. |

## How agent categories work together

These categories are designed to work as a coordinated system, not as independent tools. A typical workflow moves through all of them:

1. **Blue team agents gather intelligence.** The Threat Intelligence Agent analyzes campaigns and threat actors relevant to your environment.
1. **Red team agents map the exposure.** The Recon Agent simulates attacker movement, mapping attack paths against what blue team intelligence surfaced.
1. **Green team agents prioritize remediation.** The Posture Prioritization Agent evaluates exploitability and surfaces the highest-value fixes.
1. **Blue team agents close coverage gaps.** The Detection Authoring Agent creates detections for newly discovered techniques, and the Attack Investigation Agent investigates any incidents that surfaced during the workflow.

Throughout this process, agents pause and request your approval before taking high-impact actions. You review, approve, or reject each proposed action before the agent proceeds.

## Related content

- [What is Project Perception?](agentic-security-overview.md)
- [Key concepts in Project Perception](agentic-security-concepts.md)
- [Work with agents](agentic-security-agents.md)
