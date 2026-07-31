---
title: Run playbooks from incidents and threat intelligence
description: Learn how to start agentic sessions from incident detail pages and threat intelligence articles without navigating to Project Perception first.
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
#customer intent: As a security professional, I want to run playbooks from incidents and threat intelligence articles so that I can automate investigations without leaving my current context.
---

# Run playbooks from incidents and threat intelligence



[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

Integration scenarios allow you to start agentic sessions from other areas of the Microsoft Defender portal without navigating to Project Perception first. You can run playbooks directly from incident detail pages and threat intelligence articles, streamlining your workflow and reducing context switching.

## What are integration scenarios?

Integration scenarios are in-context session initiation points that connect specific Microsoft Defender surfaces to Project Perception. When you're investigating an incident or reviewing a threat intelligence article, you can immediately start an agentic session on that item without leaving the page.

Integration scenarios are available in:

- **Incident detail pages**: Run a playbook on a specific incident to automate triage, investigation, or response tasks.
- **Threat intelligence article pages**: Run a playbook on a threat intelligence article to automate threat research, indicator analysis, or proactive hunting.

## Run a playbook from an incident

To start an agentic session from an incident:

1. In the Microsoft Defender portal, go to **Incidents & alerts** > **Incidents**.
1. Select an incident to open its detail page.
1. On the incident detail page, locate the **Run playbook** button. The button appears near the top of the page, typically alongside other incident actions such as **Assign** or **Resolve**.
1. Select **Run playbook**. A menu appears showing available playbooks.
1. The menu displays only playbooks that:
   - Accept an incident as input
   - Have all required agents set up and enabled
   - Are accessible to users with the **Security Reader** or **Security Admin** role
1. Select a playbook from the menu. If only one applicable playbook exists, the button text might show the playbook name instead of "Run playbook."
1. (Optional) Add a session name or description to help you identify the session later.
1. Select **Start session**.

Project Perception creates a new shared session. The session appears in the **Sessions** list in Project Perception with an "In progress" status.

### View sessions related to an incident

To see all agentic sessions linked to a specific incident:

1. Open the incident detail page.
1. Scroll to the **Agentic Sessions** section (the location varies by incident detail page layout).
1. The section lists all sessions related to the incident, including:
   - Session name
   - Start time
   - Status
   - Agents involved

Select a session name to open its detail page in Project Perception.

> [!NOTE]
> The Agentic Sessions section only appears if at least one session is linked to the incident.

## Run a playbook from a threat 

To start an agentic session from a threat:

1. In the Microsoft Defender portal, go to **Threat intelligence** > **Threat analytics**.
1. Select a threat to open its detail page.
1. On the article detail page, locate the **Run agentic playbook** button. The button appears near the top of the page.
1. Select **Run agentic playbook**. A menu appears showing available playbooks.
1. The menu displays only playbooks that:
   - Accept a threat intelligence article as input
1. Select a playbook from the menu. If only one applicable playbook exists, the button text might show the playbook name instead of "Run playbook."
1. (Optional) Add a session name or description.
1. Select **Start session**.

Project Perception creates a new shared session. The session appears in the **Sessions** list in Project Perception with an "In progress" status.

### View sessions related to a threat intelligence article

To see all agentic sessions linked to a specific threat intelligence article:

1. Open the threat intelligence article detail page.
1. Scroll to the **Agentic Sessions** section (the location varies by article detail page layout).
1. The section lists all sessions related to the article, including:
   - Session name
   - Start time
   - Status
   - Agents involved

Select a session name to open its detail page in Project Perception.

> [!NOTE]
> The Agentic Sessions section only appears if at least one session is linked to the article.

## Understand playbook scoping

When you use integration scenarios, the playbook menu shows only playbooks compatible with the current input type. This scoping ensures you don't see irrelevant playbooks.

| Input type | Playbooks shown |
|------------|-----------------|
| Incident | Only playbooks that accept incidents as required input. |
| Threat intelligence article | Only playbooks that accept threat intelligence articles as required input. |

If no playbooks are available for the input type, the **Run playbook** button is disabled or does not appear.

### Multiple playbooks vs. single playbook

- **Multiple playbooks available**: The button text shows "Run playbook," and a menu appears when you select it.
- **Single playbook available**: The button text shows the playbook name (for example, "Incident Triage Automation"). Selecting the button starts the session immediately without showing a menu.

## Benefits of integration scenarios

Integration scenarios provide several advantages:

- **Reduced context switching**: Start agentic sessions without leaving your current investigation.
- **Faster response**: Automate tasks immediately when you identify a relevant incident or threat.
- **Contextual recommendations**: See only playbooks relevant to the item you're investigating.
- **Integrated workflow**: Sessions appear in both Project Perception and the related incident or article detail page, creating a unified view.

## Limitations

Integration scenarios have some limitations:

- **Input type restrictions**: Playbooks must be designed to accept the specific input type (incident or threat intelligence article). Playbooks that require other inputs (such as IP addresses or file hashes) are not available through integration scenarios.
- **Agent access requirements**: You must have the **Security Reader** or **Security Admin** role to use agents in a playbook. If you don't have the required role, the playbook does not appear in the menu.
- **Manual triggers only**: Integration scenarios support only playbooks with manual triggers. Automatic triggers (event-based or time-based) are not available through integration scenarios.

## Next steps

- [View and manage sessions](agentic-security-sessions.md)
- [Work with playbooks](agentic-security-playbooks.md)
