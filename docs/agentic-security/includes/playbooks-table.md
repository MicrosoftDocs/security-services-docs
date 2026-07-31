| Playbook | Description | Participating agents |
|----------|-------------|----------------------|
| Extract threat intelligence | Analyzes a threat intelligence article and produces structured intelligence objects, including TTPs, IOCs, CVEs, and KQL hunting queries. | Threat Intelligence Agent |
| Protect against a threat | Multi-agent workflow that takes a threat intelligence source and produces attack path analysis, posture findings, prioritized remediation, and new detection rules. | Threat Intelligence Agent, Recon Agent, Posture Prioritization Agent, Detection Authoring Agent |
| Investigate incident | Performs an autonomous tier-2 investigation of a Defender incident and produces a complete attack story with verdict, timeline, and remediation actions. | Attack Investigation Agent |
| Identify attack paths | Maps how an attacker could move through your Azure environment and reach valuable assets, with choke-point analysis and remediation recommendations. | Recon Agent |
| Assess identity risks | Evaluates identity exposure and lateral movement risks in your Azure environment, with identity-focused attack path analysis and remediation guidance. | Recon Agent |
| Plan for posture remediation | Build a prioritized remediation plan across clouds, devices, and AI. This playbook weighs exposure, exploitability, and asset context to target the highest-risk posture gaps. | Posture Prioritization Agent |
