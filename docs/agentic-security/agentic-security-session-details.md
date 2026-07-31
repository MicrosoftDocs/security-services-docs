---
title: Work with a session in Project Perception
description: Learn how to review session activity and agent outputs, interact with agents, stop work, and respond to agent requests in Microsoft Defender.
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
#customer intent: As a security professional, I want to work with a session so that I can guide agent work and review what agents accomplish.
---

# Work with a session in Project Perception



[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

The session detail page shows a full record of agent work, including the conversation history, a generated summary, inputs provided, and any output files produced. Use this page to follow session progress, review results, and continue interacting with agents. For information about browsing and filtering sessions, see [View and manage sessions](agentic-security-sessions.md).

## Open a session

To open a session detail page:

1. Go to **Perception** > **Sessions**.
1. Select a session card.

## Session detail page layout

The session detail page has the following areas:

- **Conversation metadata** (left): The main activity feed showing agent progress, status updates, and messages.
- **Summary panel** (center): Opens when you select **Session summary** in the right sidebar. Displays a generated summary of the session outcome. Available in multi-agent sessions only.
- **Overview sidebar** (right): Shows session metadata, including agent activity, inputs provided, and output files. Available in multi-agent sessions only.

At the top of the page, the session name and current status badge are displayed. Additional controls in the upper right let you access **Session details** and **Shared session** information, and see the timestamp of the most recent activity.

## Conversation metadata

The conversation metadata shows the full activity history for the session. The content and structure vary depending on the type of session.

**Multi-agent sessions** open with an **Overview** section that shows coordinated progress messages describing which agents are running, when they finish, and whether they succeed or encounter issues.

**Single-agent sessions** show the agent's name as the panel header and display that agent's activity directly.

Regardless of session type, the conversation includes:

- **User messages**: The input or instructions that started the session, shown as highlighted chat bubbles.
- **Progress updates**: Messages announcing which agents are running and what they have produced.
- **Completion markers**: **Done in X sec** or **Done in X min** entries that mark when an agent finished. Select the chevron (∨) to expand and see additional detail.
- **Recap**: When all agents have finished, a final message summarizes what each agent produced and the overall outcome.

> [!NOTE]
> The exact content and length of the conversation varies by session. Multi-agent sessions show coordinated progress across several agents, while single-agent sessions show a simpler, more direct activity feed. Sessions where some agents fail may still show partial results from agents that completed successfully.

### Ask about this session / Ask the agent a question

At the bottom of the conversation panel, there is an input field for interacting with the session. The label varies by session type:

- **Multi-agent sessions**: The field is labeled **Ask about this session**. Use it to ask questions about what the agents did, request clarification on findings, or explore results across the full session.
- **Single-agent sessions**: The field is labeled **Ask the agent a question**. Use it to ask the agent directly about its work or current activity.

The **Ask about this session** field is available while a multi-agent session is running and after it completes. The **Ask the agent a question** field is unavailable while the agent is actively running and becomes available when the agent pauses for input or completes its current step.

> [!NOTE]
> AI-generated content may be incorrect. Check for accuracy. This chat is not private and may be viewed by others.

## Overview sidebar

> [!NOTE]
> The Overview sidebar is available in multi-agent sessions only. Single-agent sessions show agent activity, inputs, and outputs inline without a dedicated sidebar.

The right sidebar organizes the session's key elements into collapsible sections.

### Session summary

Select **Session summary** to open the **Perception Run Summary** in the center panel. The summary includes:

- **Headline**: A one-sentence description of the overall outcome.
- **What happened**: A narrative of what each agent did, what it found, and how agents responded to each other's outputs.
- **What to do next**: A prioritized list of recommended actions based on the session findings.

The summary is AI-generated and may update as agents complete their work. Select **Download** to save the summary.

### Agent activity

Shows all agents that participated in the session. The count shows how many agents completed out of the total (for example, **4/4** or **1/1**). Expand the section to see each agent listed individually with its completion status.

Agent activity reflects what actually ran. If an agent encountered an error or was skipped, that is reflected here.

### Inputs

Shows the inputs provided when the session was started, such as a link to a threat intelligence article. Select an input to open it.

### Outputs

Lists the output files produced during the session, typically Markdown reports generated by individual agents. Select a file name to view its contents, or select **Download** to save it locally.

> [!NOTE]
> The number and type of outputs vary by session and depend on which agents completed successfully. A session where some agents fail may still produce outputs from agents that completed. If no agents produced output, this section shows **0**.

## Stop a session

If you have the **Security Reader** or **Security Admin** role, you can stop a session at any time.

[!INCLUDE [stop-session-steps](includes/stop-session-steps.md)]

## Respond to agent requests

When an agent pauses and requires your input or approval, the session status changes to **Waiting for input**. The agent's request appears in the conversation panel. Respond directly in the conversation to allow the agent to continue.

For more information, see [Approve, reject, or stop agentic work](agentic-security-supervise-work.md).

## Understand task statuses

For a description of all task status values, see [Key concepts in Project Perception](agentic-security-concepts.md).

The session's overall status reflects the combined state of all conversations:

- If any conversation is **In progress**, the session status is **In progress**.
- If all conversations are **Completed**, the session status is **Completed**.
- If all conversations ended but at least one is **Failed**, the session status is **Failed**.

## Next steps

- [Approve, reject, or stop agentic work](agentic-security-supervise-work.md)
- [View and manage sessions](agentic-security-sessions.md)
