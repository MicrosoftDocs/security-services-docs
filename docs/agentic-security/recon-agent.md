---
title: Use the Recon Agent in Project Perception
description: Learn how to set up and use the Recon Agent in Project Perception to map your Azure environment, find attack paths, and identify security gaps.
ms.service: project-perception
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: how-to
ms.date: 08/20/2026
ms.update-cycle: 180-days
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
ContentLastModified: 06/03/2026
LastPublished: 06/03/2026
FirstPublishDateTime: 05/27/2026
appliesto:
- Project Perception
#customer intent: As a security analyst or red team operator, I want to use the Recon Agent in Project Perception so that I can map my Azure environment, discover attack paths, and identify security gaps without executing attacks.
---

# Use the Recon Agent in Project Perception

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

The Recon Agent in Project Perception gives security teams and red team operators an attacker-perspective view of an Azure environment. It correlates assets, identities, permissions, and network exposure to identify realistic attack paths, configuration issues, and exposure risks without changing resources.

Use this article to understand the Recon Agent's capabilities, review its prerequisites and permissions, set it up, start a session, and interpret its report.

## Key capabilities

The Recon Agent runs multi-step, AI-orchestrated reconnaissance in your Azure environment.

- **Read-only assessment**: Provides an evidence-backed risk assessment without changing resources.
- **Input for other agents**: Provides findings to other agents, including investigation agents.
- **Environment-grounded analysis**: Analyzes only data from your Azure environment.

> [!NOTE]
> The Recon Agent creates a **read-only** assessment. It doesn't exploit vulnerabilities, execute payloads, modify resources, deploy detections, persist attack graphs, or operate outside your organization. The agent analyzes your environment through read-only API calls. Results are a point-in-time snapshot and don't replace continuous monitoring systems.

## Why use the Recon Agent?

Microsoft Security Exposure Management continuously identifies attack paths that originate from internet-exposed assets, critical resources, and sensitive identities. It monitors these marked assets and identities, but doesn't generate attack paths from arbitrary starting points that don't meet these criteria.

The Recon Agent complements Exposure Management with assumed-breach analysis. Analysts can start with any asset or identity in an Azure subscription. Assets don't need to be designated as critical or internet exposed, and identities don't need to be marked as sensitive. The analysis answers the question, "If an attacker already controlled this asset or identity, where could they go next?"

For example, a phishing attack might compromise a user who isn't marked as a sensitive identity in Defender. Exposure Management typically doesn't generate an attack path from that user unless the path includes another marked asset. The Recon Agent can use the user as the starting point to reveal potential attacker pivots. Teams can then identify effective choke points before those paths lead to incidents involving critical resources or sensitive identities.

This broader starting-point coverage helps teams identify attack paths across their Azure environment and prioritize critical paths in time to reduce security operations center (SOC) incident volume.

| Use case | Recon Agent |
| --- | --- |
| **Attack paths from unmarked assets and identities** | Generates assumed-breach attack paths from any asset or identity in an Azure subscription, including assets that aren't designated as critical or internet exposed and identities that aren't marked as sensitive. |
| **Posture and exposure visibility** | Interprets those signals in context and explains which combinations of identity, permission, asset, and network exposure create realistic attack paths. |
| **Alert investigation** | Explains whether an alert or finding is part of a broader attacker route and what downstream assets could be reached. |
| **Attack path analysis** | Runs targeted, session-based reconnaissance scoped to a subscription, resource group, or critical asset and can reason over missing data, failed steps, and inferred paths. |
| **Detection coverage** | Maps attack-path steps to existing Defender alerts and hunting coverage, then highlights where the SOC may lack visibility. |
| **Prioritization** | Prioritizes the paths and fixes most likely to reduce exploitability, blast radius, and business impact for the selected environment. |
| **Remediation planning** | Identifies the smallest set of high-impact changes that would break the largest number of attack paths and shows which paths each fix eliminates. |
| **Analyst usability** | Produces plain-language explanations, evidence-backed reasoning, and attack-path diagrams that are easier for analysts, red teams, and stakeholders to review. |

**In short**: Microsoft Defender products help detect, protect, and manage exposure. The Recon Agent explains how an attacker could use that exposure in a specific Azure environment and which actions would most effectively reduce risk.

## Before you begin

Review the following product and permission requirements before you set up the Recon Agent.

### Prerequisites

To use the Recon Agent, you need:

- Microsoft Entra ID P2
- Microsoft Defender XDR
- Microsoft Defender for Cloud with the Defender CSPM plan
- An Azure subscription

### Required permissions

[!INCLUDE [permissions-table](includes/permissions-table.md)]

### Additional permissions required

The Recon Agent requires two more permission sets to perform reconnaissance. The user who grants each permission set needs the corresponding role in the following table.

| Role required to grant permissions | Permissions to grant to the Recon Agent |
| --- | --- |
| Privileged Role Administrator (Microsoft Entra role) | **Microsoft Graph API permissions**:<br><br>- `User.Read.All`<br>- `Organization.Read.All`<br>- `Group.Read.All`<br>- `GroupMember.Read.All`<br>- `Application.Read.All`<br>- `DelegatedPermissionGrant.Read.All`<br>- `Policy.Read.All`<br>- `RoleManagement.Read.Directory`<br>- `AuditLog.Read.All` |
| Role Based Access Control Administrator on the subscription that is the target environment for the Recon Agent | **Azure role-based access control (RBAC) roles (assign at subscription scope)**:<br><br>- Reader<br>- Key Vault Reader<br>- Log Analytics Reader<br>- Security Reader |

## Set up the Recon Agent

To set up this agent, follow the steps in [Set up an agent](agentic-security-get-started.md#path-2-set-up-and-run-an-agent).

> [!NOTE]
> The Recon Agent uses an agent identity rather than an agent user identity. Because of current technical limitations, agent user identities don't support the Recon Agent's read-only operations.

After you create the Recon Agent's Agent ID, use the following scripts to assign the permissions listed in [Additional permissions required](#additional-permissions-required). Both scripts require the Agent ID as input.

**Grant Microsoft Graph API permissions**:

Run this script to grant the Microsoft Graph application permissions that the Recon Agent needs:

```powershell
<
.SYNOPSIS
    Assigns the set of Graph API roles required for the Recon Agent Blueprint.

.DESCRIPTION
    Assigns the following Graph API Roles:
      - User.Read.All
      - Organization.Read.All
      - Group.Read.All
      - GroupMember.Read.All
      - Application.Read.All
      - DelegatedPermissionGrant.Read.All
      - Policy.Read.All
      - RoleManagement.Read.Directory
      - AuditLog.Read.All

.PARAMETER TenantId
    The Tenant Id.

.PARAMETER AgentObjectId
    The Entra ID Object ID (principal ID) of the Agent Identity to assign roles to. To get this value,
    1. Go to the Microsoft Defender portal at https://security.microsoft.com/ -> Perception -> Agents
    2. Search for the Recon Agent and click on it to open the agent details page
    3. Copy the value under the "Identity" section
>

[CmdletBinding()]
param(
    [Parameter(Mandatory = $true)]
    [ValidatePattern('^[0-9a-fA-F]{8}-([0-9a-fA-F]{4}-){3}[0-9a-fA-F]{12}$')]
    [string]$TenantId,

    [Parameter(Mandatory = $true)]
    [ValidatePattern('^[0-9a-fA-F]{8}-([0-9a-fA-F]{4}-){3}[0-9a-fA-F]{12}$')]
    [string]$AgentObjectId
)

# Ensure signed in
az login --tenant $TenantId | Out-Null

# Graph API roles (AppRoleId -> Role Name)
$roleIds = @{
    "df021288-bdef-4463-88db-98f22de89214" = "User.Read.All"
    "498476ce-e0fe-48b0-b801-37ba7e2685c6" = "Organization.Read.All"
    "5b567255-7703-4780-807c-7be8301ae99b" = "Group.Read.All"
    "98830695-27a2-44f7-8c18-0c3ebc9698f6" = "GroupMember.Read.All"
    "9a5d68dd-52b0-4cc2-bd40-abcf44ac3a30" = "Application.Read.All"
    "81b4724a-58aa-41c1-8a55-84ef97466587" = "DelegatedPermissionGrant.Read.All"
    "246dd0d5-5bd0-4def-940b-0421030a5b68" = "Policy.Read.All"
    "483bed4a-2ad3-4361-a73b-c83ccdbdc53c" = "RoleManagement.Read.Directory"
    "b0afded3-3588-46d8-8b3d-9842eff778da" = "AuditLog.Read.All"
}

# Get the Entra Object ID of the Microsoft Graph Service Principal in the specified tenant
$GraphObjectId = Get-AzADServicePrincipal -DisplayName "Microsoft Graph" | Select-Object -ExpandProperty Id

# Assign Graph API roles to the agent identity
$results = @()
foreach ($rid in $roleIds.Keys) {
    $roleName = $roleIds[$rid]
    $body = "{\`"principalId\`":\`"$AgentObjectId\`",\`"resourceId\`":\`"$GraphObjectId\`",\`"appRoleId\`":\`"$rid\`"}"

    # az is an external process; capture output and evaluate success explicitly.
    az rest --method POST `
        --uri "https://graph.microsoft.com/v1.0/servicePrincipals/$AgentObjectId/appRoleAssignments" `
        --headers "Content-Type=application/json" `
        --body $body 2>&1

    if ($LASTEXITCODE -ne 0) {
        $results += [pscustomobject]@{ Role = $roleName; Status = "Failed" }
        continue
    }

    $results += [pscustomobject]@{ Role = $roleName; Status = 'Assigned' }
}

Write-Host "`n=== Summary ===" -ForegroundColor Cyan
$results | Format-Table -AutoSize
```

**Grant Azure role-based access control permissions**:

Select the Azure subscriptions that the Recon Agent can analyze. This selection limits all users of the agent to the preconfigured subscriptions. Run this script for each subscription:

```powershell
<
.SYNOPSIS
    Assigns the set of Azure RBAC roles required for the Recon Agent Identity.

.DESCRIPTION
    Assigns the following built-in roles at subscription scope to the specified Agent Identity:
      - Reader
      - Key Vault Reader
      - Log Analytics Reader
      - Security Reader

.PARAMETER TenantId
    The Tenant Id.

.PARAMETER SubscriptionId
    The Azure subscription ID to scope the role assignments to.

.PARAMETER AgentObjectId
    The Entra ID Object ID (principal ID) of the Agent Identity to assign roles to. To get this value,
    1. Go to the Microsoft Defender portal at https://security.microsoft.com/ -> Perception -> Agents
    2. Search for the Recon Agent and click on it to open the agent details page
    3. Copy the value under the "Identity" section
>

[CmdletBinding()]
param(
    [Parameter(Mandatory = $true)]
    [ValidatePattern('^[0-9a-fA-F]{8}-([0-9a-fA-F]{4}-){3}[0-9a-fA-F]{12}$')]
    [string]$TenantId,

    [Parameter(Mandatory = $true)]
    [ValidatePattern('^[0-9a-fA-F]{8}-([0-9a-fA-F]{4}-){3}[0-9a-fA-F]{12}$')]
    [string]$SubscriptionId,

    [Parameter(Mandatory = $true)]
    [ValidatePattern('^[0-9a-fA-F]{8}-([0-9a-fA-F]{4}-){3}[0-9a-fA-F]{12}$')]
    [string]$AgentObjectId

)

# Ensure Az.Resources module is available
if (-not (Get-Module -ListAvailable -Name Az.Resources)) {
    Write-Error "The Az.Resources module is required. Install with: Install-Module Az -Scope CurrentUser"
    exit 1
}
Import-Module Az.Resources -ErrorAction Stop

# Ensure signed in
Connect-AzAccount -Tenant $TenantId | Out-Null

# Set subscription context
Write-Host "Setting subscription context to $SubscriptionId." -ForegroundColor Cyan
Set-AzContext -SubscriptionId $SubscriptionId | Out-Null

$scope = "/subscriptions/$SubscriptionId"

# Azure RBAC roles
$roles = @(
    'Reader',
    'Key Vault Reader',
    'Log Analytics Reader',
    'Security Reader'
)

# Assign Azure RBAC roles to the agent identity
$results = @()
foreach ($role in $roles) {
    $existing = Get-AzRoleAssignment -ObjectId $AgentObjectId `
                                     -RoleDefinitionName $role `
                                     -Scope $scope `
                                     -ErrorAction SilentlyContinue

    if ($existing) {
        $results += [pscustomobject]@{ Role = $role; Status = 'AlreadyExists' }
        continue
    }

    New-AzRoleAssignment -ObjectId $AgentObjectId `
                         -RoleDefinitionName $role `
                         -Scope $scope `
                         -ObjectType 'ServicePrincipal' | Out-Null

    if ($LASTEXITCODE -ne 0) {
        $results += [pscustomobject]@{ Role = $roleName; Status = "Failed" }
        continue
    }

    $results += [pscustomobject]@{ Role = $roleName; Status = 'Assigned' }
}

Write-Host "`n=== Summary ===" -ForegroundColor Cyan
$results | Format-Table -AutoSize
```

### Allow other users access

[!INCLUDE [setup-assign-permissions](includes/setup-assign-permissions.md)]

## Start a Recon Agent session

For information about the available session entry points, see [Start a new session](agentic-security-sessions.md#start-a-new-session).

The Recon Agent participates in the following playbooks:

| Playbook | Required input |
| --- | --- |
| **Assess identity risks** | An Azure subscription and managed identity. |
| **Identify attack paths** | An Azure subscription. |
| **Protect against a threat** | A threat intelligence article. |

Use these steps to start an **Assess identity risks** session:

1. In the navigation pane, select **Perception** > **Sessions**.
1. Select **New session**.
1. Select the **Assess identity risks** playbook.

   :::image type="content" source="media/agentic-security-job.png" alt-text="Screenshot of Project Perception playbook options for starting a new session.":::

   The **Additional inputs needed** panel opens. Two inputs are required:

   | Field | Description |
   | --- | --- |
   | **Azure subscription** | The Azure subscription ID or name to scope the session to. Each session is limited to one subscription. The administrator preconfigures this list during Recon Agent setup and you can only use preconfigured subscriptions. |
   | **Managed identity** | Select the managed identity. |

   :::image type="content" source="media/assess-identity-risks.png" alt-text="Screenshot of the Assess identity risks playbook with its required session inputs.":::

   > [!NOTE]
   > When you set up the **Identify attack paths** playbook, a subscription picker appears for defining the session scope. The picker lists subscriptions available to the signed-in user, not the Recon Agent application. To start the playbook, the signed-in user needs read access to the entire subscription. This limitation applies only when the session starts. After the session starts, the Recon Agent uses its own identity for reconnaissance.

1. Fill in both fields and select **Start session**.

The session opens with a **Running** status. The agent shows its progress as it drafts a task list and starts its work.

## Monitor session progress

While the session is running, the right-side panel shows:

- **Overview**: Shows the session summary and current status.
- **Progress**: Tracks completed steps. For example, the value changes from **0/1** to **1/1** when the task is complete.
- **Recon Agent**: Identifies the active agent for the session.
- **Inputs**: Shows the target environment and use case you provided.
- **Outputs**: Lists files generated so far and updates as the session progresses.

## Understand the report

The report contains the following sections:

- **Key findings**: Summarizes the most significant risks and indicators with supporting evidence, such as IP addresses that host malicious content and their DNS resolution history. Each finding is labeled **confirmed**, **likely**, or **inferred** to indicate the strength of the evidence.
- **Asset inventory table**: Lists discovered assets with the columns Indicator, Type, Threat Verdict, Confidence, and First Seen.
- **Attack-path graph**: Shows realistic paths that an attacker could use and the relationships between assets, identities, and access. For example, a path might connect an organization, a privileged user's on-behalf-of token, and a production asset. Where applicable, the graph identifies the fastest, stealthiest, and widest routes.
- **MITRE ATT&CK mapping**: Maps each relevant finding to MITRE ATT&CK techniques. The report classifies techniques as _applicable_, _not applicable_, or _insufficient data_ so you can assess how much of the attack surface your current detections cover.
- **Detection coverage gaps**: Identifies attack paths that existing Defender detections don't cover. Where coverage exists, the report includes relevant Defender alerts and Kusto Query Language (KQL) hunting queries.

> [!IMPORTANT]
> Recon Agent outputs are AI-generated and based on data available through read-only API access. Review the findings for accuracy before you use them to plan remediation or communicate risk. The report includes the banner **"AI-generated content may be incorrect. Check it for accuracy."**

<a name='agent-output'></a>

## View Recon Agent output

The session displays Recon Agent output as Markdown files.

:::image type="content" source="media/agentic-security-reconnaissance-output.png" alt-text="Screenshot of Recon Agent output displayed as Markdown files in a Project Perception session.":::

## Related content

- [What is Project Perception?](agentic-security-overview.md)
- [Understand key concepts in Project Perception](agentic-security-concepts.md)
- [Work with agents](agentic-security-agents.md)
- [Monitor and manage agent sessions](agentic-security-sessions.md)
- [Attack Investigation Agent](attack-investigation-agent.md)
- [Triage Agent](triage-agent.md)
