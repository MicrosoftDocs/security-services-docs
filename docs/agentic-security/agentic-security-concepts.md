---
title: Key concepts in Project Perception
description: Understand sessions, agents, and playbooks in Project Perception.
ms.service: project-perception
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: concept-article
ms.date: 07/31/2026
ai-usage: ai-assisted
appliesto:
- Project Perception
ms.custom: Project Perception
#customer intent: As a security professional, I want to understand the core concepts in Project Perception so that I can effectively use agents and playbooks.
---

# Key concepts in Project Perception


[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

Project Perception uses the following concepts to organize agentic work: sessions, agents, and playbooks. Understanding these concepts helps you configure, delegate, and supervise agentic operations effectively.

## Sessions

A session is the record of an agent interaction. Sessions capture agent activity, decisions, inputs, outputs, and any approvals or human interventions. Sessions can involve a single agent or multiple agents working in coordination. Each session has a status that reflects the aggregate state of all tasks within it.

For more information about sessions, see [View and manage sessions](agentic-security-sessions.md).


## Agents

An agent is an autonomous or semi-autonomous software entity that can reason, use tools, and perform tasks. Project Perception agents are Microsoft-published agents designed for deep, autonomous security operations work. They form the core of Microsoft's multi-agent SOC system, covering the full security operations lifecycle from threat intelligence through detection authoring, exposure analysis, posture prioritization, alert triage, and incident investigation.

Perception agents are designed to collaborate. The output from one agent becomes input for another, enabling end-to-end workflows. For example, threat intelligence extracted by the Threat Intelligence Agent feeds directly into detections created by the Detection Authoring Agent.

Perception agents require an agent identity and role assignment before they can be used. For setup instructions, see [Work with agents](agentic-security-agents.md).

Perception agents include:

[!INCLUDE [agents-table](includes/agents-table.md)]

## Playbook

A playbook is a reusable, agent-driven set of actions for a specific security objective. When run, agents execute the playbook's steps on behalf of the user, investigating signals, correlating data, and producing output without requiring manual intervention at each step.

Key characteristics of playbooks:

- **Preset by Microsoft.** The playbook list is read-only. You can't create custom playbooks in this release.
- **Can use multiple agents.** A single playbook can involve multiple agents, and a single agent can be used by multiple playbooks.
- **Might require an input to run.** Depending on the playbook, a session might not start until you provide the specific input it needs. For example, the *Investigate attack* playbook requires an incident ID before it can run.
- **Require all agents to be enabled.** A playbook is only active when all of its required agents are set up and enabled.

Perception includes the following playbooks. Some playbooks run a single agent for a focused task. Others coordinate multiple agents in sequence, where each agent's output feeds the next.

[!INCLUDE [playbooks-table](includes/playbooks-table.md)]



## How the concepts relate

The following table shows how the concepts work together:

| Concept | Creates or uses | Example |
|---------|-----------------|---------|
| Sessions | Contains agent work; can be created by playbooks | A session investigating a phishing incident involves three agents working in sequence. |
| Agents | Participates in sessions | A threat intelligence agent joins a session to research indicators of compromise. |
| Playbooks | Creates sessions; assigns agents | A playbook for high-severity incidents creates a session with triage, investigation, and response agents. |

## Next steps

- [Get started with Project Perception](agentic-security-get-started.md)
- [Work with agents](agentic-security-agents.md)
