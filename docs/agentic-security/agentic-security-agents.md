---
title: Work with agents in Project Perception
description: Learn how to view, enable, configure, and manage agents in Project Perception for Microsoft Defender.
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
#customer intent: As a security administrator, I want to manage agents in Project Perception so that I can control which agents are available and how they're configured.
---

# Work with agents in Project Perception

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

The **Agents** page displays all agents available to your organization, grouped into **Agents ready for setup** and **Agents in use**. Use this page to set up new agents, view agent details, and manage agent settings.

## Access the Agents page

To view the Agents list:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
1. Select **Perception** in the navigation pane.
1. Select **Agents**.

## View agents ready for setup

The **Ready for setup** section appears at the top of the Agents page when agents need configuration. This section displays detail cards for agents that are available but not yet enabled.

> [!NOTE]
> If you're not an administrator, the **Set up** button is unavailable. Contact your administrator to enable agents.

## Set up an agent

For the complete setup procedure, including identity and permission configuration, see [Set up an agent](agentic-security-get-started.md#path-2-set-up-and-run-an-agent).

Some agents have additional configuration requirements. Review the documentation for the agent you want to set up before starting the setup wizard.

## Filter and sort the agents list

Use filters and sorting to find specific agents:

- **Keyword search**: Enter text in the search box to filter by agent name or description.
- **Publisher filter**: Select a publisher from the dropdown to view only agents from that publisher (Microsoft, partner names, or third parties).
- **Status filter**: Select a status from the dropdown to view agents by their current state (Enabled, Setup required, or Disabled).

Select column headers to sort the list by Name, Publisher, Status, or Playbooks.

## Permissions

Permissions in Project Perception work at the agent level, not the playbook level.

[!INCLUDE [permissions-table](includes/permissions-table.md)]

[!INCLUDE [session-visibility-note](includes/session-visibility-note.md)]

## View agent details

Select an agent name from the agents list to open its detail page. The page header shows the agent name, its status (**Active** or inactive), the publisher, and an **Edit agent** button. The page has the following tabs:

- **Overview**: agent configuration and recent sessions
- **Sessions**: full session history for this agent

### Overview tab

The **Overview** tab has a left panel and a right panel.

**Left panel:**

| Section | Description |
| --- | --- |
| **About this agent** | A description of what the agent does and the tasks it performs. |
| **Playbooks** | Playbooks that use this agent, with agent count. Select the link icon to open a playbook's detail page. |
| **Permissions** | Permissions the agent needs to access data and take actions. Select **Permission details** for the full reference. |
| **Identity** | The Microsoft Entra agent ID the agent runs under. Select it to view. |
| **Plugins** | Plugins enabled for this agent. Shows **None** if none are configured. |
| **Role-based access** | Describes who can view and manage this agent's output. |

**Right panel - Recent Sessions:**

Shows the most recent sessions involving this agent. Columns: **Session name**, **Session status**, **Activity status**, **Last activity**. Select **View all** to open the full session history.

### Sessions tab

The **Sessions** tab shows all sessions in which this agent has participated. Each row shows the **Session name**, **Session status**, **Activity status**, and **Last activity** timestamp. Use this tab to review historical activity and find specific sessions by status or time.

Select a session name to open its detail page. For information about the page layout, agent chat, inputs, outputs, and approval requests, see [Work with a session](agentic-security-session-details.md).

## Administrative actions for agents

If you're an administrator you can perform additional actions on enabled agents.

### Edit agent configuration

To modify an agent's settings:

1. Go to **Perception** > **Agents**.
1. Select the agent name to open the agent detail page.
1. Select **Edit** (available only to administrators).
1. Modify any of the following:
   - Agent identity
   - Agent role
   - User roles that can execute or steer sessions
   - User roles that can view sessions
   - Custom agent settings (if applicable)
1. Select **Save changes**.

### Remove an agent

To disable an agent:

1. Go to **Perception** > **Agents**.
1. Select the agent name to open the agent detail page.
1. Select **Remove Agent** (available only to administrators).
1. Review the warning message. Removing an agent:
   - Disables the agent immediately
   - Stops any in-progress sessions using the agent
   - Prevents the agent from being used in new sessions
   - Marks playbooks that require the agent as needing setup
1. Select **Remove** to confirm.

> [!WARNING]
> Removing an agent stops all active sessions that include the agent. Ensure no critical sessions are running before you remove an agent.

## Next steps

- [Work with playbooks](agentic-security-playbooks.md)
- [Get started with Project Perception](agentic-security-get-started.md)
