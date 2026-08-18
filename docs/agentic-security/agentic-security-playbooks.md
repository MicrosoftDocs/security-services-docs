---
title: Work with playbooks in Project Perception
description: Learn how to view, understand, and run playbooks to automate security operations in Microsoft Defender.
ms.service: project-perception
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.date: 07/31/2026
ai-usage: ai-assisted
appliesto:
- Project Perception
ms.custom: Project Perception
#customer intent: As a security professional, I want to use playbooks so that I can automate security responses and investigations.
---

# Work with playbooks in Project Perception

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

The **Playbooks** page lists all playbooks available to your organization. Use it to browse available playbooks, review what each one does and what agents it uses, and start new sessions.

## Access the Playbooks page

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
1. Select **Perception** in the navigation pane.
1. Select **Playbooks**.

The page displays a flat list of playbooks.

## Browse the playbooks list

Each row in the list shows:

| Column | Description |
|--------|-------------|
| **Playbook name** | The name of the playbook. Select the name to open the playbook detail pane. |
| **Description** | A brief summary of what the playbook does. |
| **Agents** | The number of agents that run as part of the playbook. |
| **Required inputs** | The input the playbook needs before it can run, such as a threat intelligence article, incident, or Azure subscription. If no input is required, this field is empty. |
| **Trigger** | How the playbook is started. All current playbooks use a **Manual** trigger. |

### Filter the list

- Use the **Search playbooks** bar to find a playbook by name.
- Use the **Agents** filter to narrow the list to playbooks that use a specific agent.

## View playbook details

Select any row in the list to open the playbook detail pane on the right side of the screen. The pane shows the playbook name and the following sections:

### Description

A full description of what the playbook does and what output it produces.

### Required inputs

The input the playbook needs to run. For example, a playbook might require a threat intelligence article or an incident. Provide this input when you start a session.

### Agents

The agents that execute this playbook, listed as cards. Each card shows:

- Agent name and publisher
- A short description of what the agent does in the context of this playbook
- A **View details** link to open the agent detail page

## Start a session from a playbook

1. Select a playbook row to open its detail pane.
1. Review the **Required inputs** and **Agents** sections to confirm the playbook meets your needs.
1. Select **New session** at the top of the detail pane.
1. Provide the required input (for example, select a threat intelligence article or enter an incident ID).
1. Select **Start session**.

The session appears in the **Sessions** list with an **In progress** status.

> [!NOTE]
> Starting a session from a playbook requires **Run** access to all agents the playbook uses. If you don't have the required access, contact your administrator.

## Related content

- [View and manage sessions](agentic-security-sessions.md)
- [Work with agents](agentic-security-agents.md)
- [Run playbooks from incidents and threat intelligence](agentic-security-integration-scenarios.md)
