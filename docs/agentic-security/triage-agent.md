---
title: Triage Agent
description: Learn how the Triage Agent uses AI-driven reasoning to triage and classify alerts at scale, helping analysts focus on real threats.
ms.service: project-perception
f1.keywords:
- NOCSH
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: how-to
search.appverid:
- MOE150
- MET150
ms.date: 08/10/2026
appliesto:
- Project Perception
ai-usage: ai-assisted
ms.custom:
- msecd-doc-authoring-1023
- Project Perception
#customer intent: As a security analyst, I want to learn about the Triage Agent so that I can triage and classify security incidents efficiently at scale.
---

# Triage Agent

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

Security Operations Centers (SOCs) process large volumes of alerts in multiple workloads, and each workload requires different context, signals, and investigative depth. Differences in how analysts evaluate these alerts can lead to inconsistent triage decisions and slow the ability to distinguish real threats from false alarms. As a result, high-risk activity can be missed or delayed, while analysts spend disproportionate time filtering noise instead of acting on what matters most.

The Triage Agent is an autonomous agent embedded in Microsoft Defender that helps security teams triage alerts at scale. It applies AI-driven, dynamic reasoning over evidence to deliver clear verdicts for supported security workloads. By identifying which alerts represent real attacks and which are false positives, the agent enables analysts to focus on investigating real threats, with transparent, step-by-step reasoning to support every decision.

## Key capabilities

The Triage Agent classifies and triages alerts in Microsoft Defender for supported workloads and alert types. The agent's key capabilities include:

- **Autonomous triage**: Uses advanced AI tools to evaluate alerts and determine whether they represent malicious activity or false alarms without requiring step-by-step human input.
- **Transparent rationale**: Records classification verdicts and provides supporting reasoning in natural language and visual graphs, including the evidence used to reach each conclusion.
- **Learning based on feedback**: For supported alert types, the agent can incorporate analyst feedback when explicitly provided and approved to tune its verdict analysis. This capability is currently available for email and collaboration alerts only.

## Supported alerts

The Triage Agent currently supports the following subset of alert types in Microsoft Defender. The set of supported alerts is expected to grow over time.

|Alert type|Alert name|
|---|---|
|**Email and collaboration alerts, including phishing**|Email reported by user as malware or phish|
|**Cloud alerts, including containers**|<details><summary>View all cloud alerts</summary><ul><li>Potential Backdoor Utilities or Proxy Binaries Detected (preview)</li><li>Potential backdoor installations from running processes (preview)</li><li>Possible executable detected in a command line, encoded in Base64 (preview)</li><li>Potential base64 encoded shell script execution (preview)</li><li>Unusual access to Bash profile file</li><li>SSH server is running inside a container (preview)</li><li>Suspicious Cron operations in command line detected</li><li>Process associated with digital currency mining detected</li><li>Possible Cryptocoinminer download detected</li><li>Kubernetes crypto-miner process kills detected (preview)</li><li>Possible access to a cryptocurrency mining pool detected (preview)</li><li>Digital currency mining related behavior detected</li><li>Possible web service exploitation by using path traversal (preview)</li><li>Detected possible disabling of security tools (preview)</li><li>Blocked binary drift executing in the container (preview)</li><li>A drift binary detected executing in the container</li><li>Suspicious file attribute changes using chattr detected (preview)</li><li>Docker build operation detected on a Kubernetes node (preview)</li><li>Access to cloud metadata service detected</li><li>Possible Impairing of Command History Logging (preview)</li><li>Possible attack tool detected</li><li>Possible credential access tool detected</li><li>Access to kubelet kubeconfig file detected</li><li>Attempt to create a new Linux namespace from a container detected</li><li>Network Scanning Tool Detected (preview)</li><li>Account added to sudo group</li><li>Usage of OAST domain detected (preview)</li><li>Kubernetes penetration testing tool detected (preview)</li><li>Possible exploitation of java based program has been detected (preview)</li><li>Command within a container running with high privileges</li><li>Suspicious Proxyware or Traffic monetizers detected in command line</li><li>Potential React2Shell command injection detected</li><li>Unusual access to bash history file</li><li>Potential reverse shell detected</li><li>Possible Secret Reconnaissance Detected</li><li>Detected possible tampering of security configurations (preview)</li><li>Detected suspicious termination of security process (preview)</li><li>Sensitive Files Access Detected</li><li>Sha1-Hulud Campaign Detected: Possible command injection to exfiltrate credentials (preview)</li><li>Process seen accessing the SSH authorized keys file in an unusual way</li><li>An uncommon connection attempt detected</li><li>Detected file download from a known malicious source</li><li>Suspicious PHP execution detected</li><li>Potential port forwarding to external IP address</li><li>Process Invocation By a DB Process Detected</li><li>Suspicious Netcat activity detected on a Kubernetes node (preview)</li><li>Possible Log Tampering Activity Detected</li><li>Suspicious file timestamp modification</li><li>Possible malicious web shell detected</li><li>Suspicious request to Kubernetes API</li><li>Possible Web Shell Activity Detected</li><li>Suspicious access to workload identity token or service account token detected</li><li>Permissions to run a binary from a suspicious folder has been granted after download (preview)</li><li>A command line executed within a container contains a suspicious DNS</li><li>A command line executed within a container contains a suspicious IP address</li><li>Microsoft Defender for Cloud Kubernetes Malware execution detected (preview)</li><li>Microsoft Defender for Cloud Kubernetes Malware execution blocked (preview)</li></ul></details>|
|**Identity alerts**|<details><summary>View all identity alerts</summary><ul><li>Password spray</li><li>Possible BEC-related inbox rule</li><li>Account compromised following a password-spray attack</li></ul></details>|
|**Microsoft Defender for Endpoint**|Suspicious PowerShell command line|
|**Microsoft Defender for Cloud Apps**|<details><summary>View all Microsoft Defender for Cloud Apps alerts</summary><ul><li>Suspicious OAuth app registration</li><li>Suspicious OAuth app registered through Azure CLI or PowerShell</li><li>Malicious OAuth application added by a compromised user</li><li>Suspicious OAuth app-related activity by a compromised user</li></ul></details>|

## Before you begin

Confirm the required product availability, licensing, permissions, and configuration before you use the Triage Agent.

### Prerequisites

To run the Triage Agent in your environment, you need:

|Prerequisite|Details|
|---|---|
|**Alert-tuning rules**|Disable tuning rules that resolve the alerts you want the agent to triage. The agent doesn't triage resolved alerts. For more information, see [Tune an alert](/defender-xdr/investigate-alerts#tune-an-alert).|
|**Microsoft Unified RBAC**|Enable unified role-based access control and activate the relevant workloads for the alert types you want to triage. For more information, see [Workload-specific prerequisites](#workload-specific-prerequisites).|
|**Products and licenses**|You need specific products and licenses based on the alert types you want the agent to triage. For more information, see [Workload-specific prerequisites](#workload-specific-prerequisites).|
|**Security Copilot plugins**|The Triage Agent automatically activates these plugins: Microsoft Defender XDR, Microsoft Threat Intelligence, Triage Agent, and Phishing Triage Agent. For more information, see [Plugins overview - Microsoft Security Copilot](/copilot/security/plugin-overview).|

### Workload-specific prerequisites

The following prerequisites depend on the alert types you want the agent to triage.

#### [Email and collaboration alerts](#tab/email-alerts)

- **Product and license requirements**: The following product and license are required for email and collaboration alerts:
  - [Microsoft Defender for Office 365 Plan 2](/office365/servicedescriptions/office-365-advanced-threat-protection-service-description)

- **Unified RBAC requirements**: Activate Microsoft Defender for Office 365 in Defender XDR unified RBAC settings.

  For more information, see [Activate workloads in Microsoft Defender XDR settings](/defender-xdr/activate-defender-rbac#activate-in-microsoft-defender-xdr-settings).

  :::image type="content" source="media/triage-agent/activate-defender-for-office-365-workloads.png" alt-text="Screenshot of the Activate unified role-based access control page showing the Defender for Office 365 toggle, which needs to be enabled for the Triage Agent." lightbox="media/triage-agent/activate-defender-for-office-365-workloads.png":::

- **Configure user reported settings**: Enable **Monitor reported messages in Outlook** to define how users report potentially malicious messages in Outlook and select any of the **Reported message destinations** options:

  :::image type="content" source="media/triage-agent/configure-user-reported-settings.png" alt-text="Screenshot of the User reported settings page showing the Outlook report button and reported message destinations configurations." lightbox="media/triage-agent/configure-user-reported-settings.png":::

  For more information, see [Use the Microsoft Defender portal to configure user reported settings](/defender-office-365/submissions-user-reported-messages-custom-mailbox).

  If you're using a third-party email reporting tool, review [Options for third-party reporting tools](/defender-office-365/submissions-user-reported-messages-custom-mailbox) and view your vendor's configuration options to integrate reported messages with Defender for Office 365.

- **Add alert policy**: The Triage Agent addresses email and collaboration incidents that include alerts with the type **Email reported by user as malware or phish**.

  Ensure that you have the corresponding alert policy enabled. For more information, see [Alert policies in the Microsoft Defender portal](/defender-xdr/alert-policies).

  > [!IMPORTANT]
  > The Triage Agent doesn't triage alerts resolved by [alert tuning](/defender-xdr/investigate-alerts#tune-an-alert).
  > Make sure to disable the **Auto-Resolve - Email reported by user as malware or phish** built-in alert tuning rule and any custom tuning rules that resolve this alert.

#### [Cloud alerts](#tab/cloud-alerts)

- **Product and license requirements**: Cloud alert triage requires the following products and licenses:
  - [Microsoft Defender for Cloud](/azure/defender-for-cloud/defender-for-cloud-introduction)
  - [Microsoft Defender for Containers (part of Microsoft Defender for Cloud)](/azure/defender-for-cloud/defender-for-containers-deployment-overview)

- **Unified RBAC requirements**: Unified RBAC for cloud alerts is enabled automatically. No additional activation is required.

  No additional configuration is required beyond the general prerequisites.

#### [Identity alerts](#tab/identity-alerts)

- **Product and license requirements**: Identity alert triage requires the following products and licenses:

  - [Microsoft Entra ID P2](/entra/fundamentals/licensing)
  - [Microsoft Defender for Identity](/defender-for-identity/what-is)
  - [Microsoft Defender for Cloud Apps](/defender-cloud-apps/what-is-defender-for-cloud-apps)

- **Unified RBAC requirements**: Activate Microsoft Defender for Identity and Microsoft Defender for Cloud Apps in Defender XDR unified RBAC settings.

  For more information, see [Activate workloads in Microsoft Defender XDR settings](/defender-xdr/activate-defender-rbac#activate-in-microsoft-defender-xdr-settings).

  :::image type="content" source="media/triage-agent/rbac-settings-defender-identity.png" alt-text="Screenshot of Microsoft Defender XDR Permissions and roles page showing unified RBAC activation with Identity and Cloud Apps settings." lightbox="media/triage-agent/rbac-settings-defender-identity.png":::

---

### Permissions required

This table outlines the permissions required to perform various actions related to the Triage Agent in the Defender portal.

|User action|Required permissions|
|---|---|
|**Start sessions and view manually invoked sessions**|**Security Reader** role, as with all agents.|
|**View automatically triggered sessions**|At minimum, users need the same permissions as the agent in Defender XDR unified RBAC, as described in [Triage Agent required permissions](#triage-agent-required-permissions).|
|**Configure agent** (set up, pause, remove the agent, and manage agent identity)|**Security Administrator** in **Microsoft Entra ID**.|
|**Teach agent through feedback**|The same permissions as the agent (or higher), as described at [Triage Agent required permissions](#triage-agent-required-permissions).|
|**View feedback page**|**Security Copilot (read)**, **Security data basics (read)**, and **Email & collaboration metadata (read)** under the **Security operations** permissions group in the Defender portal.</br></br>**OR**</br></br>**Security Administrator** in **Entra ID**.|
|**Reject feedback**|**Security Administrator** in **Entra ID**.|

For more information about unified RBAC in the Defender portal, see [Microsoft Defender XDR Unified role-based access control (RBAC)](/defender-xdr/manage-rbac).

## Set up the Triage Agent

Ensure you have the [required permissions](#permissions-required) and that you meet all [prerequisites](#before-you-begin) before setting up the agent.

### Begin setup

1. In the Defender portal, select **Perception** > **Agents**.
1. Find the **Triage Agent** in the **Agents ready for setup** section.
1. Select **Set up**.
1. Follow the steps in the setup wizard and select the alert types you want the agent to triage from the list of [supported alert types](#supported-alerts). Permissions and data scopes depend on that selection.

### Assign the agent's identity and permissions

The setup wizard guides you through assigning the agent an identity and the permissions it needs to do its work.

#### Assign an identity

The agent needs a Microsoft Entra Agent ID to work. The setup wizard automatically creates a new Agent ID. Microsoft Entra creates Agent IDs specifically for AI agents. When you use an Agent ID, you keep access scoped, secure, and easier to manage. For more information, see [What are agent identities?](/entra/agent-id/identity-platform/what-is-agent-id).

> [!NOTE]
> You can change the agent identity after setup as described in [Edit agent settings](#edit-agent-settings).

#### Assign permissions

To follow the [principle of least privilege](/entra/identity-platform/secure-least-privileged-access), assign the agent identity only the [permissions the Triage Agent needs to perform its tasks](#triage-agent-required-permissions).

The setup wizard automatically creates a role based on the alert types you select and the unified RBAC permissions needed to access the associated data.

##### Triage Agent required permissions

The Triage Agent needs specific permissions to access the data it needs and to perform its triage functions. The required permissions depend on the alert types and associated products you want the agent to work with.

This table summarizes the required permissions and data scopes for each alert type:

|Alert type|Permissions|Data scopes|
|---|---|---|
|**Email and collaboration alerts, including phishing**|Security Copilot (read), Security data basics (read), Alerts (manage), Email & collaboration metadata (read), Email & collaboration content: Emails associated with alerts (read)|Defender for Office 365|
|**Cloud alerts, including containers**|Security Copilot (read), Security data basics (read), Alerts (manage)|Microsoft Defender for Cloud|
|**Identity alerts**|Security Copilot (read), Security data basics (read), Alerts (manage)|Defender for Identity and Defender for Cloud Apps|
|**Endpoint alerts**|Security Copilot (read), Security data basics (read), Alerts (manage)|Microsoft Defender for Endpoint|
|**Cloud app alerts**|Security Copilot (read), Security data basics (read), Alerts (manage)|Defender for Cloud Apps|

These permissions are in the **Security operations** permissions group in unified RBAC:

:::image type="content" source="media/triage-agent/agent-permissions.png" alt-text="Screenshot of the Security operations permissions required for the Triage Agent." lightbox="media/triage-agent/agent-permissions.png":::

> [!IMPORTANT]
> After the setup wizard assigns the agent permissions, ensure the user group monitoring the agent has equal or higher permissions to oversee its activity and output of the automatic sessions. To do this, compare the permissions of the user group to the agent in the Permissions page in the Defender portal.

## Start a session

For ways to start a session, see [Start a new session](agentic-security-sessions.md#start-a-new-session).

The Triage Agent uses the following playbook:

|Playbook|Required input|
|---|---|
|**Triage alert**|The ID of a supported alert from the Defender portal.|

## Automatic triggering of the Triage Agent

The agent helps security teams manage the large volume of alerts organizations receive daily by automatically triaging supported alerts and updating their classification and status in Defender incidents.

### Agent trigger and flow

After setup, the Triage Agent automatically runs when a relevant alert is created. The agent then autonomously analyzes the alert using sophisticated AI tools and your organization's context to determine whether the associated threat is malicious or just a false alarm.

If the alert is determined to be a false alarm, the agent classifies it as a False Positive and resolves it accordingly. If the alert is deemed malicious, it's classified as a True Positive, and the status of the associated incident remains open and in progress for an analyst to investigate and take further action.

For every alert it processes, the agent provides a detailed explanation of its verdict in the corresponding incident.

### Track the agent in the queue

To maintain transparency, the agent routinely updates incident fields during the triage process. When triaging starts, the agent assigns the alert to itself and adds an **Agent** tag to the corresponding incident. Analysts can filter the incident queue to see only incidents tagged by the agent, which simplifies oversight and prioritization.

> [!TIP]
> You can also filter the incident queue by using the name of the identity you assigned to the Triage Agent to see the incidents the agent is actively working on.

When an alert is identified as a true threat, the Triage Agent marks it as a True Positive, so analysts can filter and prioritize incidents based on confirmed classifications.

:::image type="content" source="media/triage-agent/incident-queue-agent-only.png" alt-text="Screenshot of the incident queue filtered by the Triage Agent tag" lightbox="media/triage-agent/incident-queue-agent-only.png":::

### Transparency and explainability in alert triage

For each alert it processes, the Triage Agent provides a detailed explanation of its verdict and a graphical representation of its decision-making workflow.

To review the agent's findings, follow these steps:

1. Select an incident from the incident queue.
1. On the incident page, look for the Triage Agent card in the Copilot or Tasks side panel under the Guided Response Triage section. The task is marked as completed and assigned to the agent. The card presents the agent's verdict based on its classification, highlighting key pieces of incriminating evidence that informed the decision.

   :::image type="content" source="media/triage-agent/incident-main.png" alt-text="Screenshot of the incident page with the Triage Agent card highlighted" lightbox="media/triage-agent/incident-main.png":::

1. Select the **More actions** ellipsis to view more alert details, copy the agent's classification details to the clipboard, or manage feedback.

1. To view the steps the agent took before reaching its classification, select **View agent activity** in the Triage Agent card. This shows the logic behind the agent's final classification.

## Teach the agent your organization's context through feedback

> [!IMPORTANT]
> The feedback option is currently available only for email and collaboration alerts.

For supported alert types, analysts can optionally provide feedback on agent classifications in plain, natural language, with no complex configurations required. Authorized users can review feedback, evaluate it, and explicitly apply it to influence how the agent classifies similar alerts in the future. This capability is currently available for email and collaboration alerts only.

To provide feedback and teach the agent, follow these steps:

1. In the incident page, look for the Triage Agent card in the Copilot or Tasks side panel under the Guided Response Triage section.
1. Review the agent's classification and reasoning displayed in the card's title and content. If the decision doesn't align with your organization's classification criteria, select **Change classification**. Alternatively, you can update the classification by selecting the specific alert from the **Alerts** tab, then choosing **Manage alert**.

1. In the **Manage alert** pane, select the new classification from the **Classification** dropdown menu. Then, provide your reason for the change by filling out the **Why did you change this classification** field. This step records your input on the feedback management page for auditing purposes only. The agent won't use this feedback to improve its decision-making until you explicitly select **Use this feedback to teach the agent**. If you choose not to use this feedback for teaching the agent, you can select **Save**, which will only audit the feedback without inserting it into the agent's memory.

   :::image type="content" source="media/triage-agent/manage-alert-why.png" alt-text="Screenshot highlighting the classification and feedback fields in the Manage alert pane" lightbox="media/triage-agent/manage-alert-why.png":::

1. To apply your feedback, select **Use this feedback to teach the agent**. You can use the [guide to writing feedback](#best-practices-for-writing-feedback) to help you craft effective input, and then choose **Evaluate feedback** to allow you to preview how the agent translates your feedback into a lesson and assess whether the outcome aligns with your intent. The feedback evaluation also performs basic safety checks to ensure that the applied feedback is relevant for the agent to use and doesn't conflict with previous feedback.

   > [!NOTE]
   > You can only provide feedback to the agent once per alert, and it can only be used to teach the agent how to classify email and collaboration alerts, specifically by selecting either True Positive (phishing) or False Positive (not malicious).
   > Always review your feedback and verify the AI-generated response before saving the lesson.

1. If the result meets your expectations, you can choose to insert the lesson into the agent's memory to influence its future decisions. Select **Save** to save the lesson and store it as a lesson in the agent's memory if applicable. All feedback is recorded for audit purposes, and lessons added to the agent's memory can be reviewed later in the [feedback management page](#view-and-manage-feedback-to-the-agent).

The agent uses stored feedback to triage and classify similar alerts in the future. When a relevant alert that matches the feedback characteristics is received, the agent applies this feedback to determine its classification, incorporating it as supporting evidence in its decision-making process.

### Best practices for writing feedback

Lessons provide systematic guidelines that help the agent determine whether an alert is a genuine phishing threat or a false alarm. To ensure the agent effectively incorporates your feedback, follow these best practices when providing input to the Triage Agent:

1. **Ensure feedback is relevant and contextual.** Feedback should pertain only to the email currently under review. It must also align with the updated classification you assign.
1. **Be descriptive and specific.** Clearly explain the characteristics of the email. Provide relevant details like the email subject, message body, sender, or recipients to help the agent understand the context. Specific feedback with multiple details enhances effectiveness.
1. **Ensure clarity and decisiveness.** Avoid vague or universal statements. Give feedback that's clear and actionable. Use decisive and clear identification terms.
1. **Be consistent with previous feedback.** Ensure that new feedback aligns with what you previously provided to avoid contradictions that could confuse the agent or reduce the accuracy of its decisions. You can review all previously submitted input on the [Feedback](#view-and-manage-feedback-to-the-agent) management page.
1. **Review the agent's interpretation of your feedback.** When you submit feedback, always verify that the feedback is accurately translated into a lesson. Confirm that the lesson reflects your intent and maintains consistency with your original input. Check the validity of AI-generated responses to ensure they're applicable to the scenario.

Here are examples of how you can write your feedback to the agent.

|Area|Examples of well-written feedback|Examples of feedback that can lead to failure|Comparison|
|---|---|---|---|
|Feedback about a sender|Any email claiming to be from benefits providers must originate from "@benefits.company.com".|The sender in the second alert in the incident isn't legitimate.|Feedback must relate to the email in the current alert and its context. It's tied to the chosen classification (even if you don't mention it explicitly in the feedback) and used for similar future alerts.|
|Feedback about the sender and email body|Emails offering file sharing or document access should only come from our authorized provider Contoso.com.|Emails offering file sharing or document access should only come from our authorized providers.|Well-written feedback clearly states specific requirements (for example, sender domain), while vague references (for example "authorized providers") don't contain actionable information.|
|Feedback about email subject|Any email with a subject that contains a request for a billing transaction isn't allowed in our organization and is considered phishing.|If the subject has a positive natural sentiment, it's legitimate.|Descriptive and specific feedback can be effectively validated, while subjective feedback might lead to unintended outcomes.|
|Feedback about the email body|Emails requesting credential verification should include a reference to the specific account or service. Any generic 'verify your account' request without details should be treated as phishing.|This email should be treated as phishing.|Feedback that includes detailed information is more likely to be clearly understood, while feedback lacking detail might be interpreted in various ways and could lead to unpredictable outcomes.|
|Feedback about a recipient and email body|This email was sent to multiple employees, and the body instructs recipients to download an 'important attachment' without describing its contents. Legitimate emails always specify attachment details.|Mass internal emails with attachments are phishing.|Feedback that highlights specific missing details commonly found in legitimate emails is more effective. Feedback that contains broad generalizations (mass emails) or vague terms (such as "internal") might lead to an excessive number of true positives.|
|Feedback about a recipient and a domain|New contractor onboarding emails should only be sent to email addresses starting with 'v-' to ensure they go to the correct recipients.|Contractor emails look different from usual, so they might be phishing.|Well-written feedback clearly defines the expected recipient format, while feedback that is indecisive ("might be") and lacks clear identification criteria ("looks different from usual" without specifying what is different), makes detection unreliable.|

### Resolve feedback failures

When the agent takes your feedback, it translates it into a lesson. If the agent doesn't succeed in interpreting the feedback, a relevant message shows what caused the failure. You can address these failures based on the message returned by the agent.

Here are examples of failures you might encounter when writing feedback to the agent, and how you can resolve them.

|Failure message|Recommended action|
|---|---|
|:::image type="content" source="media/triage-agent/feedback-irrelevant.png" alt-text="Screenshot of the error message about irrelevant information in the feedback provided" lightbox="media/triage-agent/feedback-irrelevant.png":::  </br> Part of the feedback provided can't be addressed as the agent currently doesn't support this type of input and therefore couldn't be translated to a lesson at all.|Rewrite your feedback and ensure that it follows the best practices. Select **Evaluate feedback** to try again.|
|:::image type="content" source="media/triage-agent/feedback-unsupported.png" alt-text="Screenshot of the error message about unsupported features in the feedback provided" lightbox="media/triage-agent/feedback-unsupported.png"::: </br> The feedback contains input that the agent can support but it's not relevant to the email at hand and therefore couldn't be translated into an actionable lesson to be saved in the memory.|Rewrite your feedback and ensure that it addresses descriptions of the email that it can support. Then select **Evaluate feedback** to try again.|
|:::image type="content" source="media/triage-agent/feedback-conflict.png" alt-text="Screenshot of the error message about conflicting data in the feedback provided" lightbox="media/triage-agent/feedback-conflict.png"::: </br> The given feedback conflicts with previous feedback given to a similar email.|In the [feedback management page](#view-and-manage-feedback-to-the-agent) search for the feedback ID to view the feedback that it conflicts with. Based on your review, you can:<ul><li>Reject the previous feedback in the feedback management page. Thereafter, select **Evaluate** to try inserting your feedback again.</li><li>Rewrite your given feedback in a way that isn't conflicting and then select **Evaluate feedback** for the agent to reevaluate your new input.</li></ul>|

> [!NOTE]
> You can choose not to resolve feedback failures. You can leave your feedback and select **Save** without checking the box for teaching the agent. The feedback won't be saved to the agent's memory and will only be documented on the feedback management page for your future tracking classification changes.

When applicable feedback is approved and stored, the agent can apply it when triaging similar alerts in the future, subject to the same permissions and controls.

## Monitor and manage the Triage Agent

To view agent metrics and manage the agent, go to the **Triage Agent** card in the incident queue or the **Agents** page. To open the **Triage Agent** page:

1. Select **Perception** > **Agents**.
1. Under **Agents in use**, look for the Triage Agent and select **Go to agent**.

The page includes the following tabs:

|Tab|Description|
|---|---|
|**Overview**|Displays the agent's status, playbooks, identity, permissions, and recent sessions.|
|**Performance**|Displays key metrics about the agent's activity over time, including daily activity and mean time to triage (MTTT).|

### Performance tab

Select the ellipsis (...) at the top right corner of the page to access management options for the agent, as described in the sections below. Select **Pause** or **Run** to temporarily stop or restart the agent's activities.

### View the Triage Agent in the incident queue

To view the Triage Agent card in the incident queue, select **Investigation & response** > **Incidents & alerts** > **Incidents**.

The Triage Agent card shows some of the agent's key metrics, including **Incidents addressed**, which are incidents containing alerts that the agent classified as true threats or false alarms. This data helps demonstrate the agent's impact and can be used to inform broader strategic conversations, highlight return on investment, or support decisions around scaling automation throughout your organization. Metrics are calculated based on the agent's activity, beginning either from its first recorded incident or from the last 30 days, whichever is more recent.

Here's how the Triage Agent card appears in the incident queue:

  :::image type="content" source="media/triage-agent/incident-queue-with-agent.png" alt-text="Screenshot of the incident queue with the Triage Agent card highlighted." lightbox="media/triage-agent/incident-queue-with-agent.png":::

Select **Manage agent** on the card to open the **Triage Agent** page, which has more performance metrics and management options.

### Edit agent settings

To edit the agent settings:

1. Select **Perception** \> **Agents**.
1. Look for the Triage Agent under **Agents in use**, and select **Go to agent**.
1. Select the **ellipsis (...)** \> **Edit agent** at the top right corner of the **Triage Agent** page.

From the **Edit agent** page, you can edit these settings:

- **Identity and role**: Change the agent's identity by selecting **Select a new identity** and follow the steps to [assign the agent's identity and permissions](#assign-the-agents-identity-and-permissions).

- **Feedback**: View and manage [user-submitted feedback to the agent](#view-and-manage-feedback-to-the-agent).

- **Supported alerts**: View which of the supported alert types the agent can triage. To activate or deactivate specific alert types for the agent:
    - On the **Edit agent** page, select **Edit supported alerts** to open the **Agent supported alerts** page.
    - On the **Agent supported alerts** page, toggle individual alert types on or off, and then select **Update**.
    - On the **Update current role** page, select **Update role permissions** to apply the updates.

### View and manage feedback to the agent

The Triage Agent learns from user-submitted feedback and improves its performance over time. It stores applicable feedback in its memory as lessons. You can view and manage feedback for the Triage Agent on the **Agent feedback** page.

This page provides a comprehensive list of all feedback submitted to the agent. You can review key details for each piece of feedback, including:

- The agent's original classification and the user-applied change
- The original feedback provided by the user, when changing the classification
- The translated lesson generated by the agent (if applicable)
- Feedback status: in use, not in use, or conflict
- The user who provided the feedback
- Feedback submission date, feedback ID, alert ID, and the incident ID

:::image type="content" source="media/triage-agent/phishing-triage-feedback-management.png" alt-text="Screenshot of the Feedback management page" lightbox="media/triage-agent/phishing-triage-feedback-management.png":::

This table explains the feedback status values:

|Status|Description|
|---|---|
|In use|The feedback was successfully converted into a lesson in the agent's memory and is actively used to triage and classify similar incidents.|
|Conflict|The feedback provided conflicted with previously provided feedback in a similar incident. Learn how you can [resolve feedback failures](#resolve-feedback-failures).|
|Not in use|The feedback was either not incorporated into the agent's memory or not marked by the user for teaching. Rejected lessons appear as "not in use" and are saved only for auditing, not for triaging and classifying incidents. For more details, select the details panel.|

> [!TIP]
> You can only manage feedback individually. Bulk management of multiple feedback entries isn't currently supported.

To view and manage user-submitted feedback:

1. Select **Perception** > **Agents**, look for the Triage Agent under **Agents in use**, and select **Go to agent**.
1. Select the **ellipsis (...)** \> **Edit agent** at the top right corner of the page. This action opens the **Edit agent** page.
1. Select **Feedback** in the left pane to open the **Agent feedback** page.
1. Select an entry from the feedback list to open the **Review feedback** pane.
1. Check the details of the feedback provided, the agent's lesson, the classification changes, and other important details.

   :::image type="content" source="media/triage-agent/review-feedback-pane.png" alt-text="Screenshot of the Review feedback pane" lightbox="media/triage-agent/review-feedback-pane.png":::
1. To reject specific feedback, select **Reject feedback**. The agent stops using the feedback in future triage decisions.

   > [!NOTE]
   > To reject feedback provided, you need the **Security Administrator** role in Entra ID.

### Remove the agent

When you remove the agent, it stops triaging and classifying new incidents, and it deletes all feedback. However, the history of previously triaged incidents is retained for your reference.

To remove the agent:

1. Select **Perception** > **Agents**, look for the Triage Agent under **Agents in use**, and select **Go to agent**.
1. Select the ellipsis (...) at the top right corner of the page, and then select **Remove**.

## Frequently asked questions

Listed below are responses to commonly asked questions about the Triage Agent. For information about the agent's capabilities and requirements, see [Key capabilities](#key-capabilities) and [Prerequisites](#before-you-begin).

### When is the agent triggered?

You can trigger this agent playbook manually. The agent runs automatically when a new alert is detected. The setup process disables built-in tuning rules that resolve supported alert types.

### Can you trust the Triage Agent?

Microsoft AI agents follow strict Responsible AI guidelines and undergo thorough reviews to ensure compliance with all AI standards and safeguards. The Triage Agent is fully incorporated into these controls. During setup, you assign the agent an identity and configure it with the minimum permissions required for its operation, ensuring that it doesn't have unnecessary permissions. The system logs all agent activities in detail, and analysts and admins can review the complete flow at any time. The system logs feedback provided to the agent to help it adapt to the organization's environment. Admins can review and modify this feedback as needed.

### How does the agent differ from a standard SOAR solution?

While both SOAR solutions and the Triage Agent automate aspects of security operations, they use different approaches.

SOAR solutions typically rely on predefined, rule-based workflows that require manual configuration and ongoing maintenance. In contrast, the Triage Agent uses reasoning-based analysis to triage alerts and record classifications within Defender, with human oversight and optional feedback where supported.

The agent operates within defined permissions and workflows in Defender and doesn't replace existing investigation or response tools.

### What level of visibility and control do I have over the agent?

Microsoft provides tools for organizations to maintain visibility into and control over the Triage Agent from deployment through ongoing operations. [The agents adhere to Microsoft's Responsible AI (RAI) standards](/copilot/security/rai-faqs-security-copilot-agents) for fairness, reliability, safety, privacy, security, inclusiveness, transparency, and accountability.

Administrators configure the agent's identity and access levels during installation, following least-privilege principles. Security and IT teams can authorize specific actions, monitor performance, and review outputs directly in Defender. Administrators can also configure capacity consumption and data access limits.

The Triage Agent operates within a zero-trust environment. The system enforces organizational policies on every agent action by evaluating the intent and scope of each operation. The agent transparently documents all decisions, reasoning, and actions as a decision tree within Defender and records them in Microsoft Purview audit logs for traceability and compliance.

### If I have Perception, what happens to my Phishing Triage Agent? How does the new Triage Agent in Perception differ?

Perception doesn't automatically change your existing Phishing Triage Agent experience. If you're participating in the Security Alert Triage Agent preview, that agent also continues to run until you set up the Perception Triage Agent.

The Perception Triage Agent expands triage capabilities with additional alert types, playbooks, manual invocation, sessions, and the ability to chat about its outputs. After you set up the Perception Triage Agent, it replaces the Phishing Triage Agent and preserves the run history, metrics, and settings.

Only one triage agent can be active at a time. If you remove the Perception Triage Agent, you can set up the Phishing Triage Agent again.

## Related content

- [What is Project Perception?](agentic-security-overview.md)
- [Understand key concepts in Project Perception](agentic-security-concepts.md)
- [Work with agents](agentic-security-agents.md)
- [Monitor and manage agent sessions](agentic-security-sessions.md)
- [Attack Investigation Agent](attack-investigation-agent.md)
- [Threat Intelligence Agent](threat-intelligence-agent.md)
