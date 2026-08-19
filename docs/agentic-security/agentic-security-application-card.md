---
title: Application card for Project Perception
description: Learn how Perception works, including its intended uses, limitations, evaluations, and safety mitigations.
ms.service: project-perception
ms.author: macapara
author: mjcaparas
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
ms.topic: overview
ms.date: 08/09/2026
ai-usage: ai-assisted
ms.custom: Project Perception, msecd-doc-authoring-1023
appliesto:
- Project Perception
#customer intent: As a security professional, I want to understand how Perception works, including its intended uses, limitations, and safety mitigations.
---

# Application card for Project Perception

[!INCLUDE [prerelease-warning](includes/prerelease-warning.md)]

## What is an Application or Platform card?

Microsoft's Application and Platform cards are intended to help you understand how our AI technology works, the choices application owners can make that influence application performance and behavior, and the importance of considering the whole application, including the technology, the people, and the environment. Application cards are created for AI applications and platform cards are created for AI platform services. These resources can support the development or deployment of your own applications and can be shared with users or stakeholders impacted by them.

As part of its commitment to responsible AI, Microsoft adheres to [six core principles](https://www.microsoft.com/ai/principles-and-approach/): fairness, reliability and safety, privacy and security, inclusiveness, transparency, and accountability. These principles are embedded in the [Responsible AI Standard](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/Microsoft-Responsible-AI-Standard-General-Requirements.pdf), which guides teams in designing, building, and testing AI applications. Application and Platform cards play a key role in operationalizing these principles by offering transparency around capabilities, intended uses, and limitations. For further insight, readers are encouraged to explore Microsoft's [Responsible AI Transparency Report](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/msc/documents/presentations/CSR/Responsible-AI-Transparency-Report-2025.pdf) and the [Microsoft Enterprise AI Services Code of Conduct](/legal/ai-code-of-conduct), which outlines how to engage with AI responsibly.

## Overview

Project Perception is a new multi-agent security system designed for the realities of AI. Perception brings together signals, context, models, and specialized agents into a continuously learning system of defense. It can reason, prioritize, and act at machine speed while keeping humans firmly in control and empowering them with powerful new workflows.

The intended users include SOC analysts, detection engineers, security architects, IT administrators, and security leaders such as Chief Information Security Officers (CISOs). Both traditional SOC teams and frontier security engineers who operate at scale across multiple security domains can use Perception.



## Key terms

The following table provides a glossary of key terms related to Perception.

| Term | Definition |
| --- | --- |
| Agent | An autonomous or semi-autonomous software entity that can reason, use tools, and perform tasks. Agents in Perception interact with data, systems, and users to accomplish security objectives. Agents can work autonomously, pause to request human approval, and resume when you respond. |
| Agent identity | The Microsoft Entra Agent ID that an agent uses to authenticate with Microsoft services and access the data it needs to perform its tasks. During setup, Microsoft Entra creates a dedicated Agent ID for the agent. The permissions assigned to the Agent ID govern what data the agent can access. |
| Playbook | A reusable set of instructions for initiating shared sessions with autonomous agent execution. Playbooks define what work should be done, which agents should do it, what inputs are required, and when the playbook should run. |
| Perception | Microsoft's multi-agent system for the security operations center. Perception coordinates specialized security agents and provides the playbooks, sessions, orchestration controls, and human oversight experiences you use to interact with them. |
| Grounding | The process of providing contextual input sources to the large language model related to an agent's task. By enabling agents to access organizational data through Microsoft Defender integrations, agents can deliver more accurate and contextually relevant responses. |
| Large language model (LLM) | AI models trained on large amounts of text data to predict words in sequences. LLMs are capable of performing various tasks such as text generation, summarization, translation, classification, and more. |
| Plan instance | A specific execution of a playbook template for a given session. The plan instance includes the actual input values provided at runtime and is specific to that session. |
| Responsible AI | Microsoft's policy, research, and engineering practices grounded in its AI principles and operationalized through the [Responsible AI standard](https://www.microsoft.com/ai/responsible-ai). |
| Session | The container for all work performed by agents. Sessions capture the full context of agentic activity, including inputs, conversations, artifacts produced, and outcomes achieved. Sessions are immutable records that serve as an audit trail for agentic work. |



## Key features or capabilities

The following table describes the key features and capabilities of Perception and how they perform in supported tasks.

| Feature or capability | Description |
| --- | --- |
| Agentic playbooks | Perception coordinates multiple specialized agents in structured sequences. The output from one agent can become input for the next, enabling end-to-end security workflows from threat intelligence through detection authoring, exposure analysis, and incident investigation. |
| Threat intelligence extraction | The Threat Intelligence Agent analyzes threat intelligence articles and extracts structured intelligence objects including threat actor profiles, MITRE ATT&CK technique mappings, IOCs, CVEs, and KQL hunting queries. |
| Alert triage | The Triage Agent classifies and resolves supported alerts, determines whether they represent malicious activity or false alarms, records verdicts with transparent supporting reasoning, and can learn from analyst feedback. The agent triggers automatically when a new supported alert is created and can also be started manually through the Triage alert playbook. |
| Incident investigation | The Attack Investigation Agent performs tier-2 investigation of Defender incidents, correlating alerts and signals to reconstruct the full attack story with verdicts, timelines, attack graphs, affected entities, and remediation actions. |
| Attack path analysis | The Recon Agent performs read-only, attacker-style analysis of Azure environments to map how an adversary could move through the environment, identifying privilege paths, choke points, and exposure risks. |
| Identity risk assessment | The Recon Agent evaluates identity exposure by analyzing privilege relationships, sensitive identities, and lateral movement opportunities in your Azure environment. |
| Detection authoring | The Detection Authoring Agent transforms threat intelligence into implementation-ready KQL detection rules tailored to specific threat actor techniques, not generic ATT&CK coverage. |
| Posture prioritization | The Posture Prioritization Agent ranks security posture findings by real-world risk, evaluating severity, exploitability, active exploitation status, internet reachability, asset criticality, and attack-path context. |
| Agent governance and management | Administrators can view all enabled agents, configure agent identities and permissions. |
| Human oversight and supervision | Users can monitor in-progress sessions, approve or reject agent actions at approval gates, stop sessions, and redirect agents with alternative guidance. Sessions surface their reasoning transparently so analysts can review, validate, or override conclusions. |
| Performance evaluation | Administrators and security engineers can track activity, understand security outcomes, and evaluate which agents and playbooks are suitable for further automation. |
| In context playbook triggering | Playbooks can be started from other Microsoft Defender surfaces, including incident detail pages and threat intelligence article pages, without navigating to the Playbooks page directly. |

Perception operates as an agentic system. To understand agent autonomy, consider:

- **Activation triggers**: what conditions or user actions cause an agent to run
- **Access permissions**: what data, systems, or resources the agent can use
- **Action rights**: what actions the agent is authorized to take on its own

The following sections describe the core agentic capabilities that underpin how Perception agents reason, plan, adapt, and extend their reach.

### Reasoning

Perception agents use the underlying large language model to analyze available context, evaluate signals, and determine the most appropriate course of action. For example, the Attack Investigation Agent correlates alerts, incidents, entities, and signals to produce a verdict and attack classification with a natural language rationale. Agents surface their reasoning transparently so analysts can review, validate, or override conclusions before acting on them.

### Planning

Agents operate against defined playbooks that instruct the agentic system to initiate a structured sequence of actions toward a security goal. Playbooks run on demand when a user triggers them.

This design gives agents a goal-directed execution model where the system determines when and how to act to complete its task. In multi-agent playbooks, each agent's output becomes a structured input for the next agent in sequence, building progressively toward a complete result.


### Adaptability

Perception agents are designed to adapt based on operational context while continuing to operate within the scope defined by their configured identity, permissions, and triggers.

- **Contextual grounding**: During execution, agents enrich their reasoning using organizational data, enabled Microsoft Defender integrations, and threat intelligence, so that outputs reflect the current customer context.
- **Agent collaboration**: Agents adapt their analysis based on findings from other agents in the same playbook. The Posture Prioritization Agent, for example, incorporates threat context from the Threat Intelligence Agent to rank findings in the context of a specific threat rather than generically.
- **Configurable identity and permissions**: Agents can be updated after setup to modify identity, triggers, and parameters, enabling them to align with evolving workflows and requirements.

### Extensibility

- **Playbooks**: Playbooks provide reusable, parameterized workflows that coordinate one or more agents. A single agent can participate in multiple playbooks, and new playbooks can coordinate agents in novel sequences.
- **Integration in Defender experiences**: Agentic workflows can be initiated from multiple surfaces in the Microsoft Defender portal, including incident pages and threat intelligence article pages, enabling contextual entry points without navigating to Perception directly.
## Intended uses

Perception is designed for security professionals and IT administrators who need AI-assisted and autonomous support for security operations workflows. The following table describes the intended use cases, the playbooks that support them, and the agents involved.

| Use case | Playbook | Agents |
| --- | --- | --- |
| **Alert triage**: Validate an alert for false positives so real threats get further attention. | Triage alert | Triage Agent |
| **End-to-end threat defense**: Take a threat intelligence source and produce a comprehensive defensive response, including attack path mapping, prioritized posture recommendations, and detection coverage. | Protect against a threat | Threat Intelligence Agent, Recon Agent, Posture Prioritization Agent, Detection Authoring Agent |
| **Autonomous incident investigation**: Perform a tier-2 investigation of a Defender incident and produce a complete attack story with verdict, timeline, attack graph, affected entities, and remediation actions. | Investigate attack | Attack Investigation Agent |
| **Threat intelligence extraction**: Analyze a threat intelligence article to extract structured intelligence objects for use in security operations. | Extract threat intelligence | Threat Intelligence Agent |
| **Attack path discovery**: Perform read-only, attacker-style reconnaissance on an Azure environment to discover how an adversary could move through it and reach valuable assets. | Identify attack paths | Recon Agent |
| **Posture remediation prioritization**: Build a prioritized remediation plan across clouds, devices, and AI. This playbook weighs exposure, exploitability, and asset context to target the highest-risk posture gaps. | Plan for posture remediation | Posture Prioritization Agent |
| **Identity risk evaluation**: Evaluate identity exposure by analyzing privilege relationships, sensitive identities, and lateral movement opportunities in an Azure environment. | Assess identity risks | Recon Agent |

## Models and training data

Perception uses Azure OpenAI large language models (LLMs) from Foundry Models sold by Azure to power agent reasoning and natural language experiences. These models aren't trained on Customer Data from Perception sessions. Model capabilities vary in reasoning, speed, limitations, and supported scenarios.

Perception incorporates security-specific knowledge and context through grounding, which provides the LLM with relevant organizational data, threat intelligence, and Defender product data at inference time rather than through model training. The quality and relevance of agent outputs depend on the data sources available to the agent at runtime, which are governed by the agent's configured identity and the permissions the administrator grants.

## Performance

Perception is designed to operate in enterprise security environments where large volumes of real-time security signals are generated throughout Microsoft Defender and integrated data sources.

Agents receive structured inputs (such as incident IDs, threat intelligence articles, or Azure subscription contexts), execute their defined tasks, and produce structured outputs. In multi-agent playbooks, each agent's output might be passed as input to the next agent, enabling progressive refinement throughout the sequence.

Outputs include:

- Structured reports with executive summaries, findings, and ranked recommendations
- Attack graph visualizations and timelines
- KQL detection rules and hunting queries
- Evidence-backed verdicts with reasoning and confidence levels
- Lists of affected entities, IOCs, and remediation actions

Sessions display intermediate steps and agent reasoning in a process log, giving users opportunities to review the agent's progress and sources. Users can stop sessions at any time. For sessions that include approval gates, agents pause and wait for user input before proceeding with high-impact actions.

## Limitations

Understanding the limitations of Perception is important to ensure it is used effectively and responsibly. While Perception enhances security workflows, it isn't designed for every scenario. Refer to the [Microsoft Enterprise AI Services Code of Conduct](/legal/ai-code-of-conduct) as well as the following considerations when choosing a use case:

- **Accuracy and completeness**: Agents can produce responses that are inaccurate, incomplete, or outdated. Output quality depends on the data sources available at runtime, the permissions the administrator grants to the agent, and the quality of the input provided. Apply human judgment and validate critical outputs before acting on them.
- **Domain-specific scope**: Perception is optimized for security-related tasks such as threat intelligence analysis, incident investigation, attack path mapping, and detection authoring. Inputs outside this domain may result in less accurate or less relevant outputs.
- **Data source dependency**: Agent outputs are grounded in available data, including connected Microsoft Defender services and the agent's configured permissions. If relevant data sources aren't available, enabled, or current, results may lack completeness or accuracy.
- **Agent setup required**: Agents must be configured with an appropriate identity and permissions before they can be used. Playbooks that include unconfigured agents aren't available for use until all required agents are set up.
- **Azure environment scope**: The Recon Agent analyzes Azure environments. Coverage is limited to the Azure subscriptions and resources visible to the agent's configured identity. Resources outside the agent's permission scope aren't analyzed.
- **Read-only reconnaissance**: The Recon Agent operates in read-only mode. It doesn't modify, exploit, or interact with the resources it analyzes. Its outputs are assessments and recommendations, not automated remediations.
- **Approval gates and human oversight**: Some agent actions require administrator or user approval before the agent proceeds. This design is intentional. High-impact actions should be reviewed by a human before execution.
- **Task-specific agent boundaries**: Each agent is designed for a specific task. Agents aren't suitable for tasks outside their defined scope and shouldn't be repurposed beyond their intended use cases.
- **Preview status**: Some capabilities in Perception may be in preview. Preview features should be treated as prerelease functionality, and outputs should be reviewed before taking action.
- **Bias, stereotyping, and ungrounded content**: Despite the implementation of responsible AI controls, AI services are probabilistic. This makes it challenging to comprehensively block all inappropriate content, which may lead to potential biases, stereotypes, or ungrounded content in AI-generated outputs.

## Evaluations

Performance and safety evaluations assess whether AI applications are operating reliably and securely by examining factors like groundedness, relevance, and coherence while identifying risks of generating harmful content. The following evaluations were conducted with safety components already in place, which are also described in the Safety components and mitigations section.

### Evaluation data for quality and safety

Evaluation data is custom-built to assess AI application performance in key areas of safety and quality, simulating real-world scenarios and risks. Microsoft identifies relevant evaluation aspects based on multi-disciplinary research and expert input. These aspects are translated into targeted evaluation objectives and guide the formulation of evaluation metrics.

For safety, Microsoft creates adversarial prompts to elicit undesirable or edge-case responses, which are then scored using AI-assisted annotators trained to assess alignment with Microsoft's safety standards. For quality, Microsoft crafts rubric-based prompts relevant to scenarios including evaluating retrieval-augmented generation (RAG) applications and agents.

Datasets are curated from diverse sources including synthetic and public datasets to simulate real-world user scenarios. Both evaluations undergo iterative refinement and human alignment to improve metric efficacy and reliability.

### Custom evaluations

Custom evaluations validate model performance in grounding, adversarial robustness, and harmful content scenarios using regression testing, curated prompt datasets, and production-aligned examples. Evaluations assess groundedness and validate protections against jailbreak, prompt injection, and intellectual property violations.

Perception agents were evaluated by the product and research team with use cases and design inputs from customers. The security of the agent system was assessed through a dedicated red teaming exercise. .

User feedback is critical in helping Microsoft improve the system. Users can provide feedback on agent responses from within the session view. This feedback goes directly to Microsoft and is used to improve platform performance through ongoing iterative refinement.

## Safety components and mitigations

Microsoft identified potential risks and misuse scenarios through processes such as red team testing, then developed mitigations to reduce the potential for harm. Microsoft continues to evaluate Perception to improve product performance and mitigations. The following list describes some of those mitigations:

- **Harmful content filtering**: Perception integrates Microsoft-developed guardrails and abuse detection models as part of the [Azure OpenAI Service](https://azure.microsoft.com/products/ai-foundry/models/openai/) foundation. These models detect and filter harmful content in categories including hate, sexual content, violence, and self-harm at multiple severity levels.
- **Responsible AI checks**: All agent outputs pass through post-processing checks that include responsible AI filters before being returned. These checks evaluate outputs for safety, accuracy, and appropriateness.
- **Approval gates**: High-impact agent actions require explicit approval from a user or administrator before the agent proceeds. This ensures that humans remain in control of consequential decisions.
- **Least-privilege identity**: Agents operate with configured identities scoped to the minimum permissions required for their task. Administrators choose the agent identity during setup, and the identity determines what data and systems the agent can access.
- **Read-only reconnaissance**: The Recon Agent is designed to analyze without acting. It doesn't modify, exploit, or interact with the resources it examines, limiting its potential for unintended impact.
- **Session immutability**: Session records are immutable. Agent work can't be retroactively altered, providing a reliable audit trail for all agentic operations.
- **User controls**: Users can stop an in-progress session at any time. For multi-agent playbooks, users can reject an agent action at an approval gate and provide alternative guidance. These controls ensure that humans can intervene when an agent is heading in an unintended direction.

## Human oversight

Perception is designed to keep humans in control of consequential decisions while enabling agents to automate high-volume, time-intensive tasks. Human oversight is built into the system at multiple levels:

- **Approval gates**: Agents can be configured to pause and request approval before taking high-impact actions. Users or administrators review the proposed action and can approve, reject, or redirect the agent.
- **Session supervision**: Users can monitor in-progress sessions through the Perception **Sessions** view, which shows what each agent is doing, what it has produced, and whether it's waiting for input.
- **Stop controls**: Users can stop any in-progress session. Stopping a session terminates all active agent tasks within it.
- **Transparent reasoning**: Agents surface their reasoning in a process log within the session view. Users can review the steps the agent took, the data it accessed, and the conclusions it reached.
- **Role-based access controls**: Administrators configure role-based access control for each agent, controlling who can run agents, who can view session results, and who can configure agent settings. This ensures that access to agentic capabilities aligns with organizational security policies.

## Data privacy and security

Perception handles data in accordance with Microsoft's data privacy and security standards:

- **Tenant isolation**: All agent sessions operate within the organizational tenant boundary. Session data isn't shared across tenants.
- **Customer data**: Prompts, session content, and agent outputs are treated as Customer Data and aren't used to train foundation models.
- **Agent identity and permissions**: Agents access data only through the identity and permissions the administrator configures. Agents can't access resources outside their configured scope.
- **Audit trail**: Sessions are immutable records that log all agent activity, inputs, and outputs. These records support security audits and compliance reviews.

### Prompt evaluation location

Prompt evaluation location determines where prompts are processed using GPU resources. When a user submits a prompt, Perception evaluates it on GPU clusters in Azure datacenters. This setting is preselected during autoprovisioning:

- If your tenant's Customer Data storage location is in the EU, prompts are processed in the EU.
- If your tenant's Customer Data storage location isn't in the EU, prompts are processed globally in the US, UK, EU, or Australia and New Zealand, depending on locality and GPU availability.

For more information about Microsoft's data handling practices, see [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement) and [Microsoft Trust Center](https://www.microsoft.com/trustcenter).

## Best practices for deploying and adopting Project Perception

Responsible AI is a shared commitment between Microsoft and its customers. While Microsoft builds AI applications and platform services with safety, fairness, and transparency at the core, customers play a critical role in deploying and using these technologies responsibly within their own contexts. To support this partnership, we offer the following best practices for deployers and end users to help customers implement responsible AI effectively.

Deployers and end-users should:

- **Exercise caution and evaluate outcomes when using Perception for consequential decisions or in sensitive domains**: Consequential decisions are those that may have a legal or significant impact on a person's access to education, employment, financial platforms, government benefits, healthcare, housing, insurance, legal platforms, or that could result in physical, psychological, or financial harm. Sensitive domains, such as financial platforms, healthcare, and housing, require particular care due to the potential for disproportionate impact on different groups of people. When using AI for decisions in these areas, make sure that impacted stakeholders can understand how decisions are made, appeal decisions, and update any relevant input data.
- **Evaluate legal and regulatory considerations**: Customers need to evaluate potential specific legal and regulatory obligations when using any AI platforms and solutions, which may not be appropriate for use in every industry or scenario. Additionally, AI platforms or solutions are not designed for and may not be used in ways prohibited in applicable terms of service and relevant codes of conduct.
- **Use Perception only for supported security scenarios and provide clear inputs**: Perception agents are designed for the security tasks described in the intended uses section. Don't repurpose an agent for decisions or actions outside its defined scope. Provide relevant context, such as the incident, threat intelligence article, Azure subscription, or time range, and state the security goal and any limits the agent should follow.
- **Exercise human oversight when appropriate**: Human oversight is an important safeguard when interacting with AI applications. While we continuously improve our AI applications, AI might still make mistakes. The outputs generated may be inaccurate, incomplete, biased, misaligned, or irrelevant to your intended goals. This could happen due to various reasons, such as ambiguity in the inputs or limitations of the underlying models. As such, users should review the responses generated by Perception and verify that they match their expectations and requirements.
- **Be aware of the risk of overreliance**: Overreliance on AI happens when users accept incorrect or incomplete AI outputs, mainly because mistakes in AI outputs may be hard to detect. For the end-user, overreliance could result in decreased productivity, loss of trust, application abandonment, financial loss, psychological harm, physical harm, among others. (e.g. a doctor accepts an incorrect AI output). In Perception, overreliance could lead to missed threats, incorrect incident conclusions, ineffective detection rules, or remediation of the wrong resources.
- **Exercise caution when designing agentic AI in sensitive domains**: Users should exercise caution when designing and/or deploying agentic AI applications in sensitive domains where agent actions are irreversible or highly consequential. Additional precautions should also be taken when creating autonomous agentic AI as described further in either the [Microsoft Enterprise AI Services Code of Conduct](/legal/ai-code-of-conduct) (for organizations) or the Code Conduct section in the [Microsoft Services Agreement](https://www.microsoft.com/servicesagreement) (for individuals). In Perception, review proposed actions at approval gates and stop or redirect a session when the agent's reasoning or output doesn't match the intended goal.
- **Configure, test, and monitor Perception carefully**: Grant each agent access only to the data and actions required for its defined task. Before broad deployment, test playbooks with representative scenarios and confirm that approval gates and user controls work as expected. Introduce autonomy gradually, train users on agent limitations, and regularly review session records, feedback, and security outcomes for changes in quality or behavior.

- **Provide feedback when issues arise**: Microsoft continuously improves Perception based on customer feedback and operational data. To provide feedback on agent performance or report unexpected behavior, use the feedback controls available in the session view after an agent completes its work.


## Learn more about Project Perception
For additional guidance or to learn more about the responsible use of Project Perception, we recommend reviewing the following documentation:

- [What is Project Perception?](agentic-security-overview.md)
- [Key concepts in Project Perception](agentic-security-concepts.md)


## Learn more about responsible AI

- [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai)
- [Microsoft responsible AI resources](https://www.microsoft.com/ai/responsible-ai-resources)
