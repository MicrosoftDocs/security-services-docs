---
title: Use the Project Perception overview and navigation
description: Learn how to use the Project Perception overview and navigate to chat, sessions, agents, and playbooks in Microsoft Defender.
ms.service: project-perception
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
#customer intent: As a security professional, I want to use the Project Perception overview and navigation so that I can monitor activity and access agentic workflows.
---

# Use the Project Perception overview and navigation



[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

Project Perception provides a central view of agent activity and access to chats, sessions, agents, and playbooks. This article describes how to use the overview and navigate the main sections.

## Access the dashboard

To access Project Perception:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
1. Select **Perception** in the navigation pane.
1. The Overview dashboard appears by default.

## Use the Overview dashboard

The **Overview** dashboard summarizes Project Perception activity for the selected time range. Use the date range selector to adjust the reporting period, or select **New session** to start agentic work.

The dashboard includes the following sections:

| Section | Description |
|---|---|
| **Waiting for input** | Shows sessions that need your attention. Select **View sessions** to review and respond to pending requests. If no sessions need input, the section displays an empty state. |
| **Agent activity** | Shows totals for sessions, inputs, agents used, and playbooks used. The flow diagram connects inputs to the playbooks and agents used to process them. |
| **Recommended playbooks** | Provides playbooks that can help you coordinate agents and automate security work. Use the search box to find a playbook by name. |
| **Session status** | Shows the progress of sessions across playbooks, grouped by statuses such as **Waiting for input**, **In progress**, **Completed**, and **Stopped**. Select **View all** to review the sessions. |
| **Performance** | Shows per-agent usage and efficiency information, including activity and **Approvals granted**. |

## Navigate Project Perception

Project Perception contains the following sections:

| Section | Description |
|---|---|
| **Overview** | Dashboard for monitoring agent activity, sessions that need attention, recommended playbooks, session status, and agent performance. |
| **New Chat** | Conversational interface for starting playbooks and interacting with agents using natural language. |
| **Sessions** | List of all sessions across all agents, organized by status. |
| **Agents** | List of all agents available in your environment. |
| **Playbooks** | List of all playbooks available in your organization, with their descriptions, agent counts, required inputs, and trigger type. |

## Chat

Select **New Chat** to describe a task in natural language. Project Perception identifies the right playbook, pre-populates inputs, and runs the session inline.

For more information, see [Interact with Project Perception using chat](agentic-security-chat.md).

## Sessions

The **Sessions** page lists all sessions across all agents. You can toggle between a Kanban board view (organized by status) and a list view.

Select any session to open the session detail view, which shows agent activity, pending approval requests, and output files produced during the session.

Users with **Run** access can select **Stop** to force a session to end. Stopping a session terminates all ongoing agent work and changes the session status to **Stopped**.

For more information, see [View and manage sessions](agentic-security-sessions.md).

## Agents

The **Agents** page lists all agents available in your environment. Agents are grouped into **Ready for setup** and **Agents in use**.

Select an agent to open its detail view, which shows the agent's description, identity, permissions, associated playbooks, and recent activity.

For more information, see [Work with agents](agentic-security-agents.md).

## Playbooks

The **Playbooks** page lists all playbooks available in your organization. Use it to find playbooks, review their required inputs and agents, and start sessions.

For more information, see [Work with playbooks](agentic-security-playbooks.md).

## Ways to start a session

For a full overview of the ways to start a session, see [Start a new session](agentic-security-sessions.md#start-a-new-session).

## Next steps

- [Interact with Project Perception using chat](agentic-security-chat.md)
- [View and manage sessions](agentic-security-sessions.md)
- [Work with agents](agentic-security-agents.md)
