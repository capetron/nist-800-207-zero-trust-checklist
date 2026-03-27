# NIST SP 800-207: Zero Trust Architecture Compliance Checklist

A comprehensive, actionable checklist and implementation guide for NIST Special Publication 800-207, "Zero Trust Architecture." This resource is designed for organizations implementing Zero Trust principles, including federal agencies responding to Executive Order 14028, defense contractors, and enterprises modernizing their security architectures. It covers the seven tenets of Zero Trust, the Policy Engine/Policy Administrator/Policy Enforcement Point (PE/PA/PEP) architecture, deployment models, and alignment with the CISA Zero Trust Maturity Model.

**Full compliance guide:** [https://petronellatech.com/compliance/nist-800-207-zero-trust/](https://petronellatech.com/compliance/nist-800-207-zero-trust/)

**Last Reviewed: March 2026**

---

## What Is NIST SP 800-207?

NIST SP 800-207, published in August 2020 by the National Institute of Standards and Technology, defines Zero Trust Architecture (ZTA) as a cybersecurity paradigm that shifts defenses from static, network-based perimeters to a model focused on users, assets, and resources. Under Zero Trust, no implicit trust is granted to any user, device, or network segment based solely on their physical or logical location. Every access request is authenticated, authorized, and continuously validated before granting access to applications and data.

The traditional perimeter-based security model, often described as "castle and moat," assumes that everything inside the corporate network is trusted and everything outside is not. This assumption has been increasingly dangerous as organizations adopt cloud services, support remote workforces, manage bring-your-own-device (BYOD) programs, and face sophisticated attackers who routinely breach perimeter defenses and move laterally through networks.

Zero Trust addresses these challenges by establishing the principle of "never trust, always verify." Every access decision is made dynamically, based on real-time assessment of the requester's identity, device health, network context, requested resource sensitivity, and current threat intelligence. Access is granted with the minimum privilege necessary and is continuously re-evaluated throughout the session.

Executive Order 14028, "Improving the Nation's Cybersecurity," signed in May 2021, mandated that federal agencies develop plans to implement Zero Trust Architecture. The Office of Management and Budget (OMB) Memorandum M-22-09, issued in January 2022, established a Federal Zero Trust Architecture Strategy requiring agencies to meet specific Zero Trust goals by the end of fiscal year 2024. These mandates have accelerated ZTA adoption across the federal government and the defense industrial base.

The CISA Zero Trust Maturity Model (ZTMM), updated to Version 2.0 in April 2023, provides a roadmap for agencies to assess their current ZTA maturity across five pillars (Identity, Devices, Networks, Applications and Workloads, Data) and three cross-cutting capabilities (Visibility and Analytics, Automation and Orchestration, Governance). The ZTMM complements SP 800-207 by providing measurable maturity levels (Traditional, Initial, Advanced, Optimal) for each pillar.

The source document is available at [https://csrc.nist.gov/publications/detail/sp/800-207/final](https://csrc.nist.gov/publications/detail/sp/800-207/final).

## Relationship to NIST SP 800-53

NIST SP 800-207 describes an architectural approach rather than prescribing specific controls. However, implementing a Zero Trust Architecture requires a broad set of security controls from NIST SP 800-53 Rev. 5. The following control families are most directly relevant:

- **AC (Access Control):** AC-2 Account Management, AC-3 Access Enforcement, AC-4 Information Flow Enforcement, AC-6 Least Privilege, AC-17 Remote Access, AC-20 Use of External Systems
- **IA (Identification and Authentication):** IA-2 Identification and Authentication (Organizational Users), IA-3 Device Identification and Authentication, IA-5 Authenticator Management, IA-8 Identification and Authentication (Non-Organizational Users), IA-12 Identity Proofing
- **SC (System and Communications Protection):** SC-7 Boundary Protection, SC-8 Transmission Confidentiality and Integrity, SC-12 Cryptographic Key Establishment and Management
- **CA (Assessment, Authorization, and Monitoring):** CA-7 Continuous Monitoring, CA-9 Internal System Connections
- **SI (System and Information Integrity):** SI-4 System Monitoring, SI-7 Software, Firmware, and Information Integrity
- **RA (Risk Assessment):** RA-3 Risk Assessment, RA-5 Vulnerability Monitoring and Scanning

Zero Trust does not replace SP 800-53 controls; it provides an architectural philosophy that guides how those controls are implemented. For example, AC-3 (Access Enforcement) in a traditional environment might rely on network-layer firewalls. In a Zero Trust Architecture, AC-3 is implemented through Policy Enforcement Points that make per-request access decisions based on multiple dynamic attributes.

## The Seven Tenets of Zero Trust

NIST SP 800-207 defines seven foundational tenets that underpin every Zero Trust Architecture:

### Tenet 1: All Data Sources and Computing Services Are Considered Resources
Every device, server, SaaS application, API endpoint, and data store is treated as a resource that requires protection. The network itself is not a security boundary. This includes BYOD devices, IoT sensors, cloud services, and internal applications.

### Tenet 2: All Communication Is Secured Regardless of Network Location
Communication must be encrypted and authenticated whether it traverses the public internet, an internal corporate network, or a private data center. Network location alone (being "inside the firewall") does not confer trust. All traffic is treated as potentially hostile.

### Tenet 3: Access to Individual Enterprise Resources Is Granted on a Per-Session Basis
Trust is not blanket or persistent. Each access request is evaluated independently. Authentication and authorization are performed before access is granted, and the minimum necessary access is provided for the minimum necessary duration. Session tokens are not reused across different resource accesses without re-evaluation.

### Tenet 4: Access to Resources Is Determined by Dynamic Policy
Access decisions are based on a combination of the requester's identity, device health, behavioral attributes, environmental conditions, and the sensitivity of the requested resource. Policies can consider time of day, geographic location, device compliance status, user role, and current threat intelligence. Access policies are centrally managed and consistently enforced.

### Tenet 5: The Enterprise Monitors and Measures the Integrity and Security Posture of All Owned and Associated Assets
No device is inherently trusted. The enterprise continuously assesses the security posture of every device, including patch level, configuration compliance, installed software, and presence of security agents. Devices that fail to meet minimum security requirements may be denied access or granted limited access.

### Tenet 6: All Resource Authentication and Authorization Are Dynamic and Strictly Enforced Before Access Is Allowed
Authentication and authorization are not one-time events at the beginning of a session. The system continuously monitors the session and may re-authenticate or re-authorize based on changes in context, such as the user attempting to access a more sensitive resource, the device's security posture changing, or anomalous behavior being detected.

### Tenet 7: The Enterprise Collects as Much Information as Possible About the Current State of Assets, Network Infrastructure, and Communications, and Uses It to Improve Its Security Posture
Comprehensive logging, telemetry, and analytics feed into the Zero Trust decision engine. This data is used not only for access decisions but also for threat detection, forensic investigation, and continuous improvement of security policies. Machine learning and behavioral analytics enhance the enterprise's ability to detect and respond to threats.

## Zero Trust Architecture Components

### Core Components: PE/PA/PEP

The logical architecture of a Zero Trust environment centers on three core components:

**Policy Engine (PE):** The brain of the ZTA. The Policy Engine evaluates access requests against defined policies, considering the requester's identity, device posture, resource sensitivity, environmental context, and threat intelligence. It makes the ultimate allow/deny decision.

**Policy Administrator (PA):** The Policy Administrator acts on the Policy Engine's decisions. When the PE grants access, the PA establishes the session by issuing authentication tokens, configuring session parameters, and instructing the PEP to allow the specific communication. When access is denied, the PA ensures the PEP blocks the request.

**Policy Enforcement Point (PEP):** The PEP is the gateway through which all access requests must pass. It intercepts every request, sends it to the PE/PA for evaluation, and enforces the resulting decision. The PEP exists as close to the resource as possible and ensures that no access occurs without explicit authorization.

### Supporting Components

| Component | Function |
|---|---|
| Continuous Diagnostics and Mitigation (CDM) | Monitors device and endpoint health, reports posture to PE |
| Industry Compliance System | Ensures access policies align with regulatory requirements |
| Threat Intelligence Feed | Provides real-time threat data to inform access decisions |
| Activity Logs | Captures all access requests, decisions, and sessions for audit |
| Data Access Policy | Defines rules for accessing data based on classification and attributes |
| Enterprise PKI | Manages certificates for device and service authentication |
| Identity Management System | Manages user identities, roles, and authentication mechanisms |
| SIEM/Security Analytics | Aggregates and analyzes security events from ZTA components |

## Zero Trust Deployment Models

NIST SP 800-207 describes three primary deployment models:

### Model 1: Device Agent/Gateway-Based
An agent installed on each device communicates with a gateway that acts as the PEP. The agent provides device posture information and routes access requests through the gateway. This model is well-suited for managed device environments.

### Model 2: Enclave-Based
The PEP protects a set of resources (an enclave) rather than individual resources. This model is appropriate for legacy systems that cannot be individually protected and for environments where resources are naturally grouped.

### Model 3: Resource Portal-Based
A centralized portal (often a reverse proxy or application gateway) acts as the PEP for all access requests. Users connect to the portal, which authenticates them and proxies their requests to backend resources. This model is common in cloud-first environments and does not require agents on endpoints.

## CISA Zero Trust Maturity Model Alignment

The CISA Zero Trust Maturity Model Version 2.0 defines four maturity levels across five pillars:

| Pillar | Traditional | Initial | Advanced | Optimal |
|---|---|---|---|---|
| Identity | Passwords, limited MFA | MFA for some apps, basic SSO | Phishing-resistant MFA, adaptive auth | Continuous identity validation, real-time risk scoring |
| Devices | Basic inventory, inconsistent patching | Agent-based inventory, EDR deployed | Real-time compliance checks, automated remediation | Continuous attestation, hardware root of trust |
| Networks | Perimeter firewalls, flat internal | Basic segmentation, VPN for remote | Micro-segmentation, encrypted east-west | Software-defined perimeter, per-session encryption |
| Applications | On-prem apps, basic access controls | SSO integration, some cloud apps | API-level security, runtime protection | Continuous authorization, immutable workloads |
| Data | Basic classification, perimeter DLP | Data inventory, classification policy | Automated classification, DLP at rest/transit | Real-time data tagging, granular access per object |

## Executive Order 14028 Requirements

Executive Order 14028, "Improving the Nation's Cybersecurity" (May 2021), and the subsequent OMB M-22-09 strategy require federal agencies to achieve the following Zero Trust objectives:

1. **Identity:** Agencies must use enterprise-managed identity systems and phishing-resistant multi-factor authentication for all staff accessing agency systems
2. **Devices:** Agencies must maintain a complete inventory of every device operated and authorized for government use, and the ability to detect and respond to incidents on those devices
3. **Networks:** Agencies must encrypt all DNS requests and HTTP traffic, and begin segmenting networks around specific applications
4. **Applications:** Agencies must treat all applications as internet-connected, routinely subject them to rigorous testing, and welcome external vulnerability reports
5. **Data:** Agencies must have a clear, shared path to deploying protections around sensitive data, including thorough data categorization and enterprise-wide logging and information sharing

## Common Zero Trust Implementation Challenges

**Challenge: Legacy system integration.** Many organizations operate legacy systems that do not support modern authentication protocols, encryption standards, or API-based access control. Address this by using the enclave-based deployment model with gateway PEPs that provide Zero Trust controls around legacy systems without modifying them.

**Challenge: Network visibility.** Zero Trust requires comprehensive visibility into all network traffic, users, and devices. Many organizations lack this visibility, particularly for east-west (internal) traffic. Deploy network monitoring and analytics tools that provide full traffic visibility, including encrypted traffic inspection where legally and technically appropriate.

**Challenge: Identity sprawl.** Users often have multiple identities across cloud services, on-premise systems, and partner organizations. Implement a unified identity provider with single sign-on and federated identity management. Consolidate directories and eliminate orphaned accounts.

**Challenge: Cultural resistance.** Zero Trust fundamentally changes how users access resources. Increased authentication prompts and access restrictions can frustrate users. Invest in user experience design for authentication flows, implement adaptive authentication that reduces friction for low-risk access, and communicate the "why" behind Zero Trust to the organization.

**Challenge: Incremental adoption.** Zero Trust is not a single product or a weekend project. It is a multi-year journey. Prioritize high-value resources and high-risk access patterns first. Use the CISA ZTMM to assess current maturity and define a phased roadmap with measurable milestones.

## How AI Accelerates Zero Trust Implementation

Zero Trust Architecture generates enormous volumes of telemetry data: identity signals, device posture assessments, network flow logs, application access patterns, and data classification metadata. Making real-time access decisions based on this data at scale is beyond the capacity of static rules and human analysts.

Petronella Technology Group uses its private AI fleet, including on-premise large language models and custom GPU infrastructure, to power the analytics engine at the heart of Zero Trust. PTG's AI models perform real-time behavioral analysis, detecting anomalous access patterns that indicate compromised credentials or insider threats. The AI continuously tunes access policies based on observed behavior, reducing false positives while maintaining security.

PTG's patented technology stack integrates AI-powered user and entity behavior analytics (UEBA) with automated policy enforcement, creating a self-adapting Zero Trust environment. When the AI detects a high-risk access attempt, it can dynamically require step-up authentication, limit session scope, or trigger an automated investigation, all without human intervention.

PTG's unique combination of AI development expertise and cybersecurity depth, including licensed digital forensic capabilities (Licensed Digital Forensic Examiner #604180), means that when the Zero Trust architecture detects a potential breach, the same team can investigate, preserve evidence, and respond. This end-to-end capability is rare in the industry.

## Frequently Asked Questions

**Q: Is Zero Trust a product or a strategy?**
A: Zero Trust is an architectural strategy and a set of principles, not a single product. No vendor sells a "Zero Trust box" that can be deployed to achieve Zero Trust. Implementing ZTA requires integrating multiple technologies (identity providers, endpoint security, network segmentation, encryption, analytics) under a unified policy framework. Be wary of vendors who claim their product alone delivers Zero Trust.

**Q: Does Zero Trust mean we no longer need firewalls?**
A: No. Firewalls remain important components of a defense-in-depth strategy. In a Zero Trust Architecture, network firewalls complement the PEP by providing additional enforcement layers, particularly for legacy systems and network segments that cannot yet participate in per-request access decisions. The key change is that firewalls are no longer the primary trust boundary.

**Q: How does Zero Trust apply to cloud environments?**
A: Cloud environments are naturally aligned with Zero Trust principles because there is no physical perimeter to defend. Cloud-native ZTA implementations use identity-based access controls, API gateways as PEPs, cloud workload protection platforms for device/workload posture, and cloud access security brokers (CASBs) for SaaS applications. Cloud environments often provide richer telemetry for Zero Trust decision-making than on-premise environments.

**Q: What is the relationship between Zero Trust and SASE?**
A: Secure Access Service Edge (SASE) is a network architecture that converges SD-WAN and network security services (SWG, CASB, FWaaS, ZTNA) into a cloud-delivered service. SASE is one implementation approach for delivering Zero Trust Network Access (ZTNA), which is a subset of the broader Zero Trust Architecture described in SP 800-207. SASE addresses the network and application pillars of Zero Trust but must be combined with identity, device, and data controls for a complete ZTA.

**Q: Is Zero Trust required for CMMC compliance?**
A: CMMC Level 2 does not explicitly require Zero Trust Architecture. However, many CMMC practices align with Zero Trust principles, including AC.L2-3.1.1 (Limit System Access), AC.L2-3.1.2 (Transaction and Function Control), AC.L2-3.1.5 (Least Privilege), and SC.L2-3.13.1 (Boundary Protection). Implementing Zero Trust significantly strengthens an organization's posture for CMMC compliance and positions it well for future requirements.

**Q: How long does a Zero Trust implementation take?**
A: A comprehensive Zero Trust implementation is a multi-year initiative for most organizations. The first 6 to 12 months typically focus on identity modernization (MFA, SSO, conditional access), device inventory and compliance monitoring, and micro-segmentation of the most critical assets. Years two and three address broader network segmentation, application-level controls, and data-centric protections. With AI-powered tools like those from PTG, key milestones can be accelerated significantly.

**Q: What is micro-segmentation and how does it relate to Zero Trust?**
A: Micro-segmentation divides the network into small, isolated segments, often down to individual workloads or applications. Access between segments requires explicit authorization, eliminating the ability of an attacker to move laterally after breaching the perimeter. Micro-segmentation implements Tenet 2 (all communication is secured regardless of location) and is a key enabler of the "assume breach" mindset central to Zero Trust.

**Q: Does Zero Trust work for operational technology (OT) and IoT environments?**
A: Yes, but with additional considerations. OT and IoT devices often lack the ability to run endpoint agents or participate in modern authentication protocols. For these environments, the enclave-based deployment model (Model 2) is typically most appropriate, with gateway PEPs providing Zero Trust controls at the network boundary around OT/IoT segments. Network monitoring and behavioral analytics are especially important for detecting anomalous OT/IoT traffic.

**Q: How do I measure Zero Trust progress?**
A: Use the CISA Zero Trust Maturity Model to assess your current maturity level across all five pillars (Identity, Devices, Networks, Applications, Data). Set measurable goals for advancing each pillar from its current maturity level (Traditional, Initial, Advanced, Optimal) within defined timeframes. Key metrics include percentage of access requests evaluated by PEPs, percentage of endpoints with real-time compliance monitoring, MFA adoption rate, and network segments with east-west traffic encryption.

## About the Author

This checklist was developed by **Craig Petronella**, founder and CEO of Petronella Technology Group, Inc. Craig brings over 23 years of cybersecurity experience and holds the following credentials:

- CMMC Registered Practitioner (RP)
- Licensed Digital Forensic Examiner #604180
- Cisco CCNA and CWNE certifications
- MIT Artificial Intelligence Certificate
- Amazon #1 Best-Selling Author of 14+ cybersecurity books

Craig has guided organizations across federal, defense, healthcare, and financial services sectors through Zero Trust Architecture implementations, from strategy development through technology deployment and continuous optimization.

## About Petronella Technology Group (PTG)

Petronella Technology Group, Inc. is a Raleigh, NC-based cybersecurity, compliance, and AI services firm that specializes in making enterprise-grade compliance accessible to small and mid-size businesses. PTG combines AI development (custom AI agents, private LLMs, GPU hosting) with deep cybersecurity and compliance expertise, a combination that no other firm in the Research Triangle offers.

**What sets PTG apart:**

- **AI-Powered Compliance:** PTG operates its own private AI fleet with on-premise large language models and custom GPU infrastructure to accelerate compliance assessments, automate control mapping, and continuously monitor security posture.
- **Patented Technology Stack:** PTG's proprietary, patented security and compliance tools automate what competitors do manually.
- **Licensed Digital Forensic Examiner:** When compliance fails and a breach occurs, PTG has the forensic expertise to investigate, preserve evidence, and support legal proceedings. Most compliance firms cannot do this.
- **Fleet Infrastructure:** PTG's on-premise AI infrastructure (GPU clusters, private cloud) proves PTG practices what it preaches about data sovereignty and private AI.

**Contact PTG:**

- **Phone:** 919-348-4912
- **Address:** 5540 Centerview Dr. Suite 200, Raleigh, NC 27606
- **Website:** [https://petronellatech.com](https://petronellatech.com)
- **Compliance Services:** [https://petronellatech.com/compliance/packages/](https://petronellatech.com/compliance/packages/)
- **Zero Trust Guide:** [https://petronellatech.com/compliance/nist-800-207-zero-trust/](https://petronellatech.com/compliance/nist-800-207-zero-trust/)

**Ready to start your Zero Trust journey?** Call 919-348-4912 or [schedule a free compliance assessment](https://petronellatech.com/compliance/packages/) to evaluate your current security architecture and build a Zero Trust roadmap.

## Related Resources

- [NIST SP 800-53 Compliance Guide](https://petronellatech.com/compliance/nist-800-53-compliance/)
- [NIST SP 800-171 Compliance Guide](https://petronellatech.com/compliance/nist-800-171-compliance/)
- [CMMC Compliance Guide](https://petronellatech.com/compliance/cmmc/)
- [NIST CSF 2.0 Implementation Guide](https://petronellatech.com/compliance/nist-csf-2-0-implementation/)
- [PTG Cybersecurity Services](https://petronellatech.com/cybersecurity/)
- [PTG AI Services](https://petronellatech.com/ai/)
- [PTG Managed IT Services](https://petronellatech.com/managed-it/)

## License

This checklist is released under the MIT License. See [LICENSE](LICENSE) for details.
