---
title: What is Project Perception?
description: Learn how Project Perception helps you govern, monitor, and operate AI agents at scale.
ms.service: project-perception
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: overview
ms.date: 07/31/2026
ai-usage: ai-assisted
appliesto:
- Project Perception
ms.custom: Project Perception
#customer intent: As a security professional, I want to understand what Project Perception is so that I can determine how it fits into my security operations.
---

# What is Project Perception?

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]


:::image type="content" source="media/project-perception.png" alt-text="Illustration of the Project Perception":::

Project Perception is a new multi-agent security system designed for the realities of AI. Perception brings together signals, context, models, and specialized agents into a continuously learning system of defense. It can reason, prioritize, and act at machine speed while keeping humans firmly in control and empowering them with powerful new workflows.

Perception is based on a simple idea: effective defense requires continuously understanding how an attacker sees the world, how a defender evaluates risk, and how protections are improved over time. 

Perception brings together three categories of specialized security agents: **red team agents** that expose vulnerabilities before attackers can exploit them, **blue team agents** that detect, triage, and investigate threats, and **green team agents** that remediate and harden your posture. Working together, they form a closed-loop system that continuously discovers, evaluates, and improves an organization's security posture.

For a full breakdown of each category and the agents within it, see [Agent categories in Project Perception](agentic-security-agent-categories.md).



## How does Project Perception work?
Perception uses coordinated agent playbooks to achieve specific security outcomes. A playbook assigns a team of specialized agents a set of objectives and orchestrates their actions throughout the workflow. Each agent has a distinct role, but they work together by sharing intelligence, findings, and security context to drive coordinated defense. Throughout the workflow, agents surface recommendations and request approvals when needed, keeping security teams in control of critical decisions.

To see how the agents work together in a complete workflow, see [Agent categories in Project Perception](agentic-security-agent-categories.md).


## Working with Project Perception agents

With Project Perception, you can:

### Configure agents

View all agents enabled for your organization, enable or disable specific agents, and configure agent identity, roles, and custom settings. You control which users can execute or view agent sessions, ensuring that access aligns with your organization's security policies.

For more information, see [Work with agents](agentic-security-agents.md).

### Delegate work to agents

Initiate autonomous execution using playbooks. Playbooks are reusable templates that define how agents should respond to specific scenarios. 

You can also use **Chat** to start a session using natural language. Describe the task and Perception identifies the right playbook, pre-populates inputs, and runs inline. For more information, see [Interact with Project Perception using chat](agentic-security-chat.md).

For more information on playbooks, see [Work with playbooks](agentic-security-playbooks.md).

### Supervise agentic work

Monitor work happening now or recently completed. Understand what initiated each session, approve or reject agent actions when they request input, stop sessions that are headed in the wrong direction, and provide alternative guidance when agents need redirection.

For more information, see [Approve, reject, or stop agentic work](agentic-security-supervise-work.md).


## Navigate Project Perception

Project Perception is organized into the following primary sections in the Microsoft Defender portal: **Overview**, **New Chat**, **Sessions**, **Agents**, and **Playbooks**. For details on what each section contains and how to navigate between them, see [Use the Project Perception overview and navigation](agentic-security-dashboard.md).


## Next steps

- [Understand key concepts in Project Perception](agentic-security-concepts.md)
- [Get started with Project Perception](agentic-security-get-started.md)
