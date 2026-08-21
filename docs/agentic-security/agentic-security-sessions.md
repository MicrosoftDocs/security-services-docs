---
title: View and manage sessions in Project Perception
description: Learn how to view, filter, and manage agentic sessions using the Sessions list and Kanban board in Microsoft Defender.
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
#customer intent: As a security professional, I want to view and manage sessions so that I can track agent work and ensure sessions are progressing appropriately.
---

# View and manage sessions in Project Perception

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

The **Sessions** page displays all sessions visible to you based on your access permissions. Use this page to monitor active sessions, review completed work, and start new sessions.

## Access the Sessions page

To view the Sessions list:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
1. Select **Perception** in the navigation pane.
1. Select **Sessions**.

## Understand session visibility

The Sessions page shows only shared sessions. Private sessions are not displayed.

[!INCLUDE [session-visibility-note](includes/session-visibility-note.md)]

## Switch between list view and Kanban board view

The Sessions page supports the following viewing modes:

- **List view**: Displays sessions in a table with detailed columns. Use list view when you need to see comprehensive information or sort by specific fields.
- **Kanban board view**: Displays sessions as cards organized by status. Use Kanban board view when you want a visual overview of session states.

To toggle between views:

1. Select **List view** or **Board view** at the top of the Sessions page.

## Start a new session

You can start a session from multiple entry points in Project Perception. Choose the approach that best fits your current workflow:

- [Start a session using the New session button](#start-a-session-using-the-new-session-button)
- [Start from a specific playbook](#start-from-a-specific-playbook)
- [Start from an incident or threat intelligence article](#start-from-an-incident-or-threat-intelligence-article)
- [Start from chat](#start-from-chat)

### Start a session using the New session button

The **New session** button is available from the Sessions list and other locations in Project Perception.

1. Select **New session**.
1. Choose a playbook from the list.
1. Provide the required inputs.
1. Select **Start session**.

### Start from a specific playbook

Open the playbook details by using one of the following paths:

- Go to **Perception** > **Playbooks**, and then select a playbook and run it.
- Go to **Perception** > **Agents**, open an agent, and then select one of its playbooks.

From the playbook details, select **New session**, provide the required inputs, and select **Start session**. For the complete procedure, see [Start a session from a playbook](agentic-security-playbooks.md#start-a-session-from-a-playbook).

### Start from an incident or threat intelligence article

If you're already viewing an incident or a threat intelligence article, you can start a session directly from that page without navigating to Project Perception first. For more information, see [Run playbooks from incidents and threat intelligence](agentic-security-integration-scenarios.md).

### Start from chat

Use chat to describe your task in natural language. Project Perception identifies the most appropriate playbook, pre-populates the inputs it can infer, and runs the session for you. For more information, see [Interact with Project Perception using chat](agentic-security-chat.md).

The new session appears in the Sessions list with an **In progress** status.

## View session details from the sessions list

Select a session to open its detail page. For a detailed walkthrough of the session detail page, including the conversation panel, overview sidebar, and how to respond to agent requests, see [Work with a session](agentic-security-session-details.md).

## Understand session statuses

Sessions progress through the following statuses:

[!INCLUDE [session-status-table](includes/session-status-table.md)]

Sessions do not automatically restart. To investigate a similar scenario, start a new session.

> [!NOTE]
> Session status also controls the availability of agent chat. The dedicated chat for each agent is disabled while the agent is actively running and becomes available when the agent is waiting for input or has completed its current step. For more information, see [Work with a session](agentic-security-session-details.md).

## Next steps

- [Approve, reject, or stop agentic work](agentic-security-supervise-work.md)
- [Work with playbooks](agentic-security-playbooks.md)
