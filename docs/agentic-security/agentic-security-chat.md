---
title: Interact with Project Perception using chat
description: Learn how to use chat in Project Perception to start playbooks using natural language, confirm inputs, and track agent activity inline.
ms.service: defender-xdr
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.collection:
  - m365-security
  - tier1
  - security-copilot
ms.topic: how-to
ms.date: 07/31/2026
appliesto:
- Project Perception
ms.custom: Project Perception
ai-usage: ai-assisted
---

# Interact with Project Perception using chat

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

Chat is a conversational entry point in Project Perception. Instead of navigating to playbooks, selecting a playbook, and manually entering inputs, you describe the task you want to perform and Perception identifies the right playbook, pre-populates the inputs it can infer, and runs the session inline in the chat interface.

Project Perception has two types of chat:

- **Main chat**: the conversational interface described in this article. Use it to start new sessions, trigger playbooks, and track session progress from a central place.
- **Agent chat**: a dedicated chat scoped to each individual agent within a running session. Agent chat lets you ask questions, provide input, or steer a specific agent's work. It's available from the session detail view and is disabled while the agent is actively running. For more information, see [Work with a session](agentic-security-session-details.md).

## Access chat

You can access Perception chat in the following ways:

- In the navigation pane, select **Perception** > **Chat**.
- Select **Copilot** from any portal page and use the toggle to switch to Perception chat.

## The welcome screen

When you open chat, a welcome screen appears with:

- **A free-text input field** - describe the task you want to perform in plain language. For example: *"Gather threat intelligence and map possible attack paths from this threat article."*
- **Suggestion cards** - a set of cards representing available playbooks, each with a short description of what it does. Select a card to use that playbook directly without typing.
- **Show more** - expands the full list of suggestion cards.

> [!NOTE]
> AI-generated content may be incorrect. Check for accuracy.

## How Perception identifies a playbook

After you submit your input, Perception reasons over your request and identifies the most appropriate playbook. It presents a **playbook card** in the chat that includes:

- The matched playbook name and the number of agents involved
- A description of what the playbook does
- An **Input selected** section showing any inputs Perception identified or inferred from your message - for example, a related threat intelligence article or outbreak


## Run the playbook

After you select **Run playbook**, the session starts and Perception displays live progress inline in Chat:

- The playbook name and elapsed time
- The current step (for example, *Step 1/5: Threat Intelligence*)
- Agent activity showing which agents are queued or running

When the session is underway, Perception provides a confirmation message that includes the **Session ID** and a link to the session.

## Follow up with Ask anything

While the session is running or after it completes, use the **Ask anything** field at the bottom of Chat to continue the conversation. 
You'll need to open the specific session to continue the conversation about a session. You can ask follow-up questions about a specific finding or get more details on agent activity or outputs.



## Related content

- [Work with playbooks](agentic-security-playbooks.md)
- [View and manage sessions](agentic-security-sessions.md)
- [What is Project Perception?](agentic-security-overview.md)
