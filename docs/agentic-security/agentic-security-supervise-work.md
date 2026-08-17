---
title: Approve, reject, or stop agentic work
description: Learn how to supervise agentic work by responding to approval requests, providing alternative guidance, and stopping sessions in Microsoft Defender.
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
#customer intent: As a security professional, I want to supervise agentic work so that I can ensure agents take appropriate actions and stay on track.
---

# Approve, reject, or stop agentic work



[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

Supervising agentic work ensures agents operate within appropriate boundaries and take actions aligned with your security objectives. This article explains how to respond to agent requests, provide alternative guidance, and stop sessions when necessary.

## Understand waiting for input status

When an agent needs your input or approval before proceeding, the session status changes to **Waiting for input**. This status indicates that one or more agents have paused their work and are requesting:

- **Approval**: Permission to take a significant action, such as disabling a user account or isolating a device.
- **Additional information**: Clarification or additional context to continue the investigation.
- **Guidance**: Direction on which approach to take when multiple options are available.

Agents request input to ensure high-impact actions are reviewed by humans before execution and to stay aligned with your intent when uncertainty arises.

## Find sessions waiting for input

You can identify sessions waiting for input in two places:

### From the Sessions list

1. Go to **Perception** > **Sessions**.
1. Apply the **Status** filter and select **Waiting for input**.
1. The list displays all sessions in this state.

> [!TIP]
> Check for sessions waiting for input regularly to avoid delays. Agents remain paused until you respond to their requests.

## Respond to an approval request

When an agent requests approval:

1. Go to the session detail page by selecting the session name from the Sessions list.
1. Select the **Progress** tab to view conversations.
1. Find the conversation where the agent requested approval. Conversations with pending requests show a "Waiting for input" status.
1. Review the agent's request message. The request includes:
   - **Action description**: What the agent wants to do.
   - **Impact assessment**: Potential consequences of the action, including risks and benefits.
   - **Context**: Why the agent is recommending this action.

### Approve the action

If you agree with the agent's recommendation:

1. Select **Approve** in the conversation.
1. The agent proceeds with the action.
1. The session status returns to **In progress**.

### Reject the action

If you disagree with the agent's recommendation:

1. Select **Reject** in the conversation.
1. (Optional) Provide a reason for the rejection. This feedback helps the agent understand your decision.
1. The agent skips the proposed action and continues with other tasks.
1. The session status returns to **In progress**.

### Suggest an alternative

If you want the agent to take a different approach:

1. Select **Suggest an alternative** in the conversation.
1. Enter your alternative guidance. Be specific about what you want the agent to do instead. For example:
   - "Isolate the device instead of disabling the user account."
   - "Focus on investigating lateral movement before taking containment actions."
   - "Query logs from the past 14 days instead of the past 7 days."
1. Select **Submit**.
1. The agent evaluates your suggestion and determines how to proceed.

## How agents handle alternative suggestions

When you suggest an alternative:

1. The agent evaluates whether your suggestion is feasible given its capabilities and available data.
1. If the agent can implement your suggestion, it creates an updated plan and requests approval again. The new approval request includes:
   - The updated action based on your guidance
   - A new impact assessment
1. If the agent cannot implement your suggestion (for example, it lacks the necessary tools or data), it explains why and may propose a different approach or request additional clarification.

You can continue providing guidance until the agent's plan aligns with your intent.

> [!TIP]
> Be specific in your alternative suggestions. Vague guidance such as "try something else" makes it difficult for agents to understand your intent.

## Stop a session

If you determine a session is not progressing appropriately or is no longer needed, you can stop it.

[!INCLUDE [stop-session-steps](includes/stop-session-steps.md)]

### When to stop a session

Consider stopping a session when:

- **The agent is pursuing the wrong objective**: The agent misunderstood the initial instructions and is investigating an unrelated issue.
- **The session is redundant**: You discover another session or manual investigation already addressed the same issue.
- **The agent is stuck**: The agent repeatedly requests the same information or fails to make progress.
- **Priorities changed**: The incident or threat is no longer relevant due to new information or resolution through other means.

> [!WARNING]
> Stopping a session cannot be undone. Agents cannot resume their work after you stop a session. If you want the agent to try a different approach, suggest an alternative instead of stopping the session.

## Best practices for supervising agentic work

Follow these practices to supervise agents effectively:

### Respond promptly to approval requests

Agents remain paused until you respond. Delays in approval can slow down incident response and investigation timelines. Set up notifications or check the **Sessions Waiting on Input** widget regularly.

### Provide specific feedback

When you reject an action or suggest an alternative, include clear reasoning. Specific feedback helps agents learn and adjust their behavior.

### Use rejection sparingly

Frequent rejections may indicate the agent needs configuration changes or additional training. If you find yourself rejecting most requests from an agent, review the agent's settings or consult the agent's documentation.

### Trust high-performing agents

Agents with high approval rates and low error rates can be trusted with more autonomy. Consider reducing approval gates for these agents by working with your administrator to adjust agent settings.

### Review completed sessions

After a session completes, review the summary and artifacts to ensure the agent's work meets your standards. Use this review to identify patterns and improvement opportunities.

## Next steps

- [View and manage sessions](agentic-security-sessions.md)
