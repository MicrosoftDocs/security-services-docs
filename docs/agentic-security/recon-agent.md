---
title: Recon Agent
description: Learn how the Recon Agent maps your Azure environment, builds attack paths, and identifies security gaps without executing any attacks.
ms.service: defender-xdr
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: how-to
ms.date: 07/31/2026
ms.update-cycle: 180-days
ai-usage: ai-assisted
ContentLastModified: 06/03/2026
LastPublished: 06/03/2026
FirstPublishDateTime: 05/27/2026
appliesto:
- Project Perception
#customer intent: As a security analyst or red team operator, I want to use the Recon Agent in Microsoft Defender so that I can map my Azure environment, discover attack paths, and identify security gaps without executing any attacks.
---

# Recon Agent

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]


Security teams often discover exposure gaps only after an incident. By then, response options are limited. To view your environment from an attacker perspective, you need to correlate assets, identities, permissions, and network exposure in a tenant. Correlating these signals often requires significant manual effort and specialized red team expertise.

This read-only threat analysis agent provides a comprehensive overview of your tenant. It presents realistic attack paths, misconfigurations, and exposure risks in a single pane of glass, enabling security teams and red team operators to address these issues promptly or forward them to downstream agents for further validation.

Use this article to review capabilities, prerequisites, and run steps.

## Key capabilities

The Recon Agent runs multi-step, AI-orchestrated reconnaissance in your Azure environment. 

- **Read-only assessment** - Delivers an evidence-backed risk assessment with zero customer impact.
- **Recon Agent output is key input** to all the other agents in the loop including other agents such as investigation agents
- **Tenant-grounded analysis** - Analyzes your Azure cloud environment using only customer tenant data.

> [!NOTE]
> The Recon Agent creates a **read-only** assessment. The agent doesn't exploit vulnerabilities, execute payloads, modify any resources, deploy detections, persist attack graphs, or operate outside your tenant boundary. All analysis is performed through read-only API calls to your environment. Results represent a point-in-time snapshot and don't replace continuous monitoring systems.

## Why use the Recon Agent?
Recon Agent does not replace Microsoft Defender products. Defender products provide core protection, posture management, exposure visibility, alerting, and detection coverage across the environment.

**The Recon Agent is a single pane of glass** that adds an AI-orchestrated, attacker-perspective analysis layer that helps security teams understand how identities, permissions, assets, trust relationships, and network exposure combine into realistic attack paths within a specific Azure subscription.

The agent helps answer practical questions such as how an attacker could move through this environment, which paths create the highest blast radius, which detection gaps matter most, and what small set of fixes would reduce the most risk.

| Use case | Recon Agent |
|---|---|
| **Posture and exposure visibility** | Interprets those signals in context and explains which combinations of identity, permission, asset, and network exposure create realistic attack paths. |
| **Alert investigation** | Explains whether an alert or finding is part of a broader attacker route and what downstream assets could be reached. |
| **Attack path analysis** | Runs targeted, session-based reconnaissance scoped to a subscription, resource group, or critical asset and can reason over missing data, failed steps, and inferred paths. |
| **Detection coverage** | Maps attack-path steps to existing Defender alerts and hunting coverage, then highlights where the SOC may lack visibility. |
| **Prioritization** | Prioritizes the paths and fixes most likely to reduce exploitability, blast radius, and business impact for the selected environment. |
| **Remediation planning** | Identifies the smallest set of high-impact changes that would break the largest number of attack paths and shows which paths each fix eliminates. |
| **Analyst usability** | Produces plain-language explanations, evidence-backed reasoning, and attack-path diagrams that are easier for analysts, red teams, and stakeholders to review. |

**In short:** Microsoft Defender products help detect, protect, and manage exposure. Recon Agent helps explain how an attacker could use that exposure in this specific tenant and what actions would most effectively reduce risk.




## Before you begin
This section provides information on the preparatory steps required prior to configuring and using the Recon Agent.


### Prerequisites
The following products are essential for the optimal functioning of the Recon Agent within the environment.

- Microsoft Entra ID P2 
- Microsoft 365 Defender XDR  
- Defender for Cloud with Defender CSPM Plan 
- An Azure subscription 
- Microsoft Copilot SCU either via Microsoft 365 E5 or Security Copilot standalone access  

### Required permissions
[!INCLUDE [permissions-table](includes/permissions-table.md)]



### Additional permissions required

Setting up the Recon Agent requires the **Azure User Access Administrator** role on the target subscription. This role is needed to grant permissions to the agent identity. We recommend using [Delegate Azure role assignment management to others with conditions](/azure/role-based-access-control/delegate-role-assignments-portal) when delegating this permission to Security Admins.


### Permissions granted to the agent

During the agent configuration process, the user must grant the agent specific permissions to ensure optimal functionality. Limiting the permissions granted to the agent can restrict its capabilities. Please ensure that your security team has approved these permission grants for the Recon Agent.

- **Graph API Permissions:**
    - User.Read.All
    - Organization.Read.All
    - Group.Read.All
    - GroupMember.Read.All
    - Application.Read.All
    - DelegatedPermissionGrant.Read.All
    - Policy.Read.All
    - RoleManagement.Read.Directory
    - AuditLog.Read.All

- **Azure RBAC (assign at subscription scope):**
    - Reader
    - Key Vault Reader
    - Log Analytics Reader
    - Security Reader


#### Grant required permissions using PowerShell

After the Recon Agent's Agent ID has been created, use the scripts below to assign the permissions outlined in the prior section. The scripts require the Agent ID as an input.

**Grant Graph API permissions**

```<#
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
#>

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

**Grant Azure RBAC permissions**

```
<#
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
#>

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



In alignment with the principle of least privilege, assign the agent identity only the read-only permissions it needs.

## Set up the Recon Agent

To set up this agent, follow the steps in [Set up an agent](agentic-security-get-started.md#path-2-set-up-and-run-an-agent).

> [!NOTE]
> During setup, select the Azure subscriptions this agent should operate on. This restricts all users of this agent to only the preconfigured subscriptions. You also need to grant the agent the [permissions listed above](#permissions-granted-to-the-agent) in the Azure portal.

### Allow other users access

[!INCLUDE [setup-assign-permissions](includes/setup-assign-permissions.md)]

## Start a Recon Agent session

For ways to start a session, see [Start a new session](agentic-security-sessions.md#start-a-new-session).

Use these steps to start a session:

1. In the navigation pane, select **Perception** > **Sessions**.
1. Select **New session**.

1. Choose one of the Recon Agent playbooks from the playbook list: **Assess identity risks**.

     :::image type="content" source="media/agentic-security-job.png" alt-text="Screenshot of options of jobs to complete.":::


    The **Additional inputs needed** panel opens. Two inputs are required:

    | Field | Description |
    |-------|-------------|
    | **Azure subscription** | The Azure subscription ID or name to scope the session to. Each session is limited to one subscription. The administrator preconfigures this list during Recon Agent setup and you can only use preconfigured subscriptions. |
    | **Managed identity** |Select the managed identity. |

     :::image type="content" source="media/assess-identity-risks.png" alt-text="Screenshot of assess identity risks.":::

    >[!NOTE]
    >When you set up the Identify attack paths playbook, a subscription picker appears in the UI to define the session scope as shown below. This picker shows the subscriptions available to the signed-in playbook initiator, not the Recon Agent application. As a workaround, the user starting the playbook must have read access to the full subscription. This limitation applies only when the session starts. After the session begins, the Recon Agent uses its own identity to perform the reconnaissance work.
   

1. Fill in both fields and select **Start session**.

The session opens in **Running** status. The agent displays its thought process while it drafts a task list and starts its work. 


## Monitor session progress

While the session is running, the right-side panel shows:

- **Overview** - Session summary and current status.
- **Progress** - Tracks completed steps (for example, **0/1** → **1/1** when complete).
- **Recon Agent** - The active agent for this session.
- **Inputs** - The target environment and use case you provided.
- **Outputs** - Files generated so far (updated as the session progresses).



## Understand the report

The report contains the following sections:

- **Key findings** - A narrative summary of the most significant risks and indicators discovered, with evidence (for example, IP addresses observed hosting malicious content, DNS resolution history). Each finding is labeled **confirmed**, **likely**, or **inferred** to communicate the strength of evidence behind it.
- **Asset inventory table** - A structured table of discovered assets with columns for Indicator, Type, Threat Verdict, Confidence, and First Seen.
- **Attack-path graph** - A visual representation of realistic attacker-viable paths through your environment, showing relationships between assets, identities, and access paths (for example: Corp tenant → Privileged user OBO token → Production). Paths show the fastest, stealthiest, and widest routes where applicable.
- **MITRE ATT&CK mapping** - Each relevant finding is mapped to MITRE ATT&CK techniques. Techniques are classified as *applicable*, *not applicable*, or *insufficient data*, so you can assess how much of the attack surface your current detections cover.
- **Detection coverage gaps** - Surfaces attack paths that aren't covered by existing Defender detections, along with relevant Defender alerts and KQL hunting queries where coverage does exist.

> [!IMPORTANT]
> Recon Agent outputs are AI-generated and grounded in the data available through read-only API access. Always review findings for accuracy before using them to drive remediation or communicate risk to stakeholders. The banner **"AI-generated content may be incorrect. Check it for accuracy."** appears in the report view as a reminder.

## Agent Output
The output is shown as markdown files alongside the agent session.

:::image type="content" source="media/agentic-security-reconnaissance-output.png" alt-text="Screenshot of agent output.":::

## Related content

- [What is Project Perception?](agentic-security-overview.md)
- [Understand key concepts in Project Perception](agentic-security-concepts.md)
- [Work with agents](agentic-security-agents.md)
- [Monitor and manage agent sessions](agentic-security-sessions.md)
- [Attack Investigation Agent](attack-investigation-agent.md)
- [Triage Agent](triage-agent.md)


