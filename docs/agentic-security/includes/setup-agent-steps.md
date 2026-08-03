To set up and enable an agent, you need the **Security Admin** role. For more information, see [Required permissions](../agentic-security-get-started.md#required-permissions).

> [!NOTE]
> The Recon Agent requires additional setup steps. Before you set it up, review [Set up the Recon Agent](../recon-agent.md#set-up-the-recon-agent) to make sure you complete all required permissions and configuration steps.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
1. Select **Perception** in the navigation pane.
1. Select **Agents**.
1. In the **Ready for setup** section, find the agent you want to enable and select **Set up**.

   > [!NOTE]
   > The **Set up** button is unavailable if you don't have the Security Admin role. Contact your administrator to enable agents.

1. Create a new agent identity. The wizard automatically creates a Microsoft Entra Agent ID. Agent IDs keep access scoped, secure, and easier to manage. For more information, see [What are agent identities?](/entra/agent-id/identity-platform/what-is-agent-id).

1. Assign the agent the required permissions. The agent detail page shows the minimum required permissions.
1. Select **Finish setup**.

After setup completes, the agent moves from **Ready for setup** to the main agents list with a status of **Enabled**.
