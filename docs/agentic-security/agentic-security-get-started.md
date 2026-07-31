---
title: Get started with Project Perception
description: Learn how to access Project Perception, set up your first agent, enable a playbook, and start your first session in Microsoft Defender.
ms.service: defender-xdr
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.date: 07/31/2026
appliesto:
- Project Perception
ms.custom: Project Perception
#customer intent: As a security professional, I want to set up Project Perception so that I can start using agents to automate security tasks.
---

# Get started with Project Perception


[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

This article helps you get started with Project Perception. Before you can run agents, you need the right access and permissions. Once you're in, you have three main paths:

- **Chat** - the lowest-friction entry point. Use natural language to describe a task and Perception figures out which agents and playbooks to run.
- **Run an agent** - set up a specific agent, assign its identity and permissions, then start a session manually or let it trigger automatically.
- **Run a playbook** - choose a predefined playbook, set up the required agents, provide an input (like an incident or threat article), and let the agents execute the workflow for you.

This article walks you through the prerequisites and a quick-start flow for getting your first agent running.

## Prerequisites

Verify you fulfill the following prerequisites:

- **Microsoft Defender portal access** - You need access to the Microsoft Defender portal at [https://security.microsoft.com](https://security.microsoft.com).
- **URBAC enabled across all Defender workloads** - For more information, see [Microsoft Defender unified role-based access control ](/defender-xdr/manage-rbac).

## Required permissions

Your permissions determine what you can do in Project Perception:

[!INCLUDE [permissions-table](includes/permissions-table.md)]

> [!NOTE]
> Access to agents is controlled by your portal role. Users with the **Security Reader** role can use all configured agents. Users with the **Security Admin** role can also set up and remove agents.

## Navigate to Project Perception

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
1. In the navigation pane, select **Perception**.


## What you see when you arrive

When you first access Project Perception, you land on a welcome page where you can access the chat experience or run a playbook. The playbooks will prompt you to set up the agents required to run them. 

The interface varies based on whether agents have been configured: 

**Empty state (no sessions have been created yet)**

If no Perception sessions have been created: 
- The **Agents** page displays Perception agents in the Ready for setup section and/or enabled agents with their status and playbook counts. 
- The **Playbooks** page shows playbooks as ready for setup and/or ready for use depending on whether any Perception agents have been set up yet. 
- The **Sessions** list is empty. 


**Active state (sessions exist)**

If agents are already set up: 
- The **Agents** page lists enabled agents with their status and playbook counts. 
- The **Playbooks** page shows playbooks ready for use. 
- The **Sessions** list displays recent and active sessions. 


## Getting started paths

There are three main ways to start using Project Perception based on your needs and experience level:

- **Chat** is the quickest option if you prefer natural language interaction. Simply describe what you want to accomplish, and Project Perception handles agent and playbook selection automatically.
- **Agents** give you direct control over configuration. Set up an agent, configure its identity and permissions, then run it manually or set up automation.
- **Playbooks** are ideal for complete workflows. They orchestrate multiple agents in sequence, with each agent's output feeding into the next stage.

Choose the path that best fits your workflow, or try multiple approaches as you become more familiar with Project Perception.

## Path 1: Use chat

Chat is the fastest way to get started. Describe what you want to investigate or accomplish in natural language, and Project Perception identifies the right agents and playbooks, pre-populates the required inputs, and runs the workflow for you. For the best experience, make sure at least one agent is configured before using chat.

For more information, see [Interact with agents using Chat](agentic-security-chat.md).

## Path 2: Set up and run an agent

Use this path when you want to configure a specific agent and run it directly.

> [!NOTE]
> The following steps provide a high-level overview of the setup process. Each agent may have additional configuration requirements beyond these general steps. For detailed setup instructions, refer to the individual agent's documentation.

### Set up an agent

[!INCLUDE [setup-agent-steps](includes/setup-agent-steps.md)]

> [!TIP]
> Start with agents that have clear, well-defined functions. The Threat Intelligence Agent and Triage Agent are good first choices because they have limited permissions and provide immediate value.

### Start a session

1. Open the agent's detail page and select **New session**.
1. Provide any required input and select **Start session**.

The session appears in the **Sessions** list with an **In progress** status.

## Path 3: Run a playbook

Playbooks coordinate multiple agents in sequence, with each agent's output feeding the next. Use this path when you want to run an end-to-end workflow.

Before you can run a playbook, all agents it requires must be set up. If any required agent shows a **Setup required** status, complete [Path 2](#path-2-set-up-and-run-an-agent) for each of those agents first.

### Start a session from a playbook

To select a playbook, review its required agents and inputs, and start a session, see [Start a session from a playbook](agentic-security-playbooks.md#start-a-session-from-a-playbook).

> [!NOTE]
> Playbooks are managed by Microsoft. You cannot create, edit, or delete them.

## Monitor and interact with a session

These steps apply whether you started a session from an agent or a playbook.

1. On the session detail page, view the agent's conversation and any artifacts it produces.
1. If the agent requests approval before taking an action, select **Approve**, **Reject**, or suggest an alternative.
1. When the session completes, review artifacts in the **Outputs** section.

For more information, see [View and manage sessions](agentic-security-sessions.md).

## Next steps

- [Key concepts in Project Perception](agentic-security-concepts.md)
- [Work with agents](agentic-security-agents.md)
- [Approve, reject, or stop agentic work](agentic-security-supervise-work.md)
