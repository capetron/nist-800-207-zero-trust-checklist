# NIST SP 800-207: Zero Trust Architecture Compliance Checklist

Use this checklist to plan, implement, and validate your Zero Trust Architecture. Items are organized by the five pillars of the CISA Zero Trust Maturity Model and aligned with NIST SP 800-207 principles. Mark items as complete when documented, implemented, and validated.

**Sources:**
- [NIST SP 800-207](https://csrc.nist.gov/publications/detail/sp/800-207/final)
- [CISA Zero Trust Maturity Model v2.0](https://www.cisa.gov/zero-trust-maturity-model)
- [OMB M-22-09 Federal Zero Trust Strategy](https://www.whitehouse.gov/wp-content/uploads/2022/01/M-22-09.pdf)

---

## Foundation: Strategy and Governance

- [ ] Obtain executive sponsorship for Zero Trust initiative
- [ ] Assign a Zero Trust program lead/architect
- [ ] Conduct a current-state assessment using the CISA ZTMM
- [ ] Define target maturity levels for each of the five pillars
- [ ] Develop a phased Zero Trust implementation roadmap (12-36 months)
- [ ] Establish a Zero Trust governance board with representatives from security, IT, networking, and business units
- [ ] Define and document Zero Trust access policies aligned with the seven tenets of SP 800-207
- [ ] Inventory all data flows, applications, and access patterns
- [ ] Identify high-value assets (HVAs) for prioritized Zero Trust implementation
- [ ] Establish success metrics and key performance indicators (KPIs)
- [ ] Allocate budget and resources for the implementation roadmap

## Pillar 1: Identity

### Traditional to Initial
- [ ] Implement a centralized identity provider (IdP) for all users
- [ ] Deploy multi-factor authentication (MFA) for all externally accessible applications
- [ ] Implement single sign-on (SSO) across enterprise applications
- [ ] Establish automated account provisioning and deprovisioning
- [ ] Conduct access reviews at least quarterly for privileged accounts
- [ ] Implement password policies aligned with NIST SP 800-63B (no forced rotation, minimum 8 characters, check against breached password lists)

### Initial to Advanced
- [ ] Deploy phishing-resistant MFA (FIDO2/WebAuthn) for all users
- [ ] Implement adaptive/risk-based authentication that adjusts requirements based on context
- [ ] Integrate identity signals into the Policy Engine (PE) for access decisions
- [ ] Implement just-in-time (JIT) and just-enough-access (JEA) for privileged access
- [ ] Deploy privileged access management (PAM) with session recording
- [ ] Federate identity across organizational boundaries (partners, contractors)
- [ ] Implement service account governance with automated credential rotation

### Advanced to Optimal
- [ ] Implement continuous identity validation throughout sessions
- [ ] Deploy real-time identity risk scoring using behavioral analytics
- [ ] Implement identity threat detection and response (ITDR)
- [ ] Achieve passwordless authentication for the majority of access scenarios
- [ ] Integrate identity analytics with UEBA for anomaly detection

## Pillar 2: Devices

### Traditional to Initial
- [ ] Maintain a complete inventory of all enterprise-owned devices
- [ ] Deploy endpoint detection and response (EDR) on all managed endpoints
- [ ] Implement automated patch management for operating systems and applications
- [ ] Establish minimum security configuration baselines for all device types
- [ ] Implement mobile device management (MDM) for corporate and BYOD devices

### Initial to Advanced
- [ ] Deploy device compliance checking before granting resource access
- [ ] Integrate device posture signals into the Policy Engine for access decisions
- [ ] Implement real-time device health attestation
- [ ] Deploy automated remediation for non-compliant devices (quarantine, forced update)
- [ ] Implement certificate-based device authentication
- [ ] Monitor and enforce application allowlisting on critical endpoints

### Advanced to Optimal
- [ ] Implement hardware root of trust (TPM-based attestation)
- [ ] Deploy continuous device integrity monitoring
- [ ] Achieve real-time risk scoring for all devices with dynamic access adjustment
- [ ] Integrate IoT and OT device monitoring into the ZTA decision framework
- [ ] Implement automated threat response at the device level

## Pillar 3: Networks

### Traditional to Initial
- [ ] Implement network segmentation between major zones (production, development, DMZ, user)
- [ ] Encrypt all external network traffic (TLS 1.2+ minimum, TLS 1.3 preferred)
- [ ] Encrypt DNS traffic (DoH or DoT)
- [ ] Deploy VPN or ZTNA for remote access (transitioning from VPN to ZTNA)
- [ ] Implement network access control (NAC) for wired and wireless networks

### Initial to Advanced
- [ ] Implement micro-segmentation around critical applications and workloads
- [ ] Encrypt all east-west (internal) traffic between segments
- [ ] Deploy software-defined networking (SDN) for dynamic network policy enforcement
- [ ] Implement network traffic analysis and anomaly detection
- [ ] Deploy distributed firewalls or host-based firewalls on all servers
- [ ] Migrate from traditional VPN to ZTNA for all remote access
- [ ] Implement DNS filtering and monitoring for threat detection

### Advanced to Optimal
- [ ] Achieve per-session network encryption for all resource access
- [ ] Deploy a software-defined perimeter (SDP) for all application access
- [ ] Implement real-time network traffic analysis with AI-powered threat detection
- [ ] Achieve full east-west traffic visibility and encryption
- [ ] Eliminate implicit trust zones entirely (no "trusted" network segments)

## Pillar 4: Applications and Workloads

### Traditional to Initial
- [ ] Inventory all applications (on-premise, cloud, SaaS) with ownership and classification
- [ ] Integrate all applications with the centralized identity provider (SSO/SAML/OIDC)
- [ ] Implement web application firewalls (WAF) for externally facing applications
- [ ] Conduct regular vulnerability scanning of all applications
- [ ] Implement a secure software development lifecycle (SSDLC)

### Initial to Advanced
- [ ] Deploy application-level access controls (API gateways as PEPs)
- [ ] Implement runtime application self-protection (RASP)
- [ ] Conduct regular penetration testing and bug bounty programs
- [ ] Deploy container security and workload protection platforms
- [ ] Implement CI/CD pipeline security (SAST, DAST, SCA, secrets scanning)
- [ ] Segment application-to-application communication with service mesh

### Advanced to Optimal
- [ ] Implement continuous authorization for application access (re-evaluate on each request)
- [ ] Deploy immutable workloads (containers, serverless) where possible
- [ ] Achieve application-level micro-segmentation with per-service access policies
- [ ] Implement zero-standing-privilege for application administration
- [ ] Integrate application telemetry into the PE for contextual access decisions

## Pillar 5: Data

### Traditional to Initial
- [ ] Conduct a data inventory and classification exercise
- [ ] Define data classification levels (Public, Internal, Confidential, Restricted)
- [ ] Implement data loss prevention (DLP) for email and web traffic
- [ ] Encrypt data at rest for all sensitive data stores
- [ ] Encrypt data in transit (TLS for all internal and external communications)
- [ ] Implement access controls on data stores based on identity and role

### Initial to Advanced
- [ ] Deploy automated data classification using content inspection
- [ ] Implement DLP at rest, in transit, and in use
- [ ] Deploy data access governance with activity monitoring
- [ ] Implement database activity monitoring for sensitive data stores
- [ ] Enforce data-centric access policies in the PE (attribute-based access control)
- [ ] Implement data masking and tokenization for sensitive data in non-production environments

### Advanced to Optimal
- [ ] Achieve real-time data tagging and classification with AI
- [ ] Implement granular, per-object access decisions based on data sensitivity and user context
- [ ] Deploy rights management/information protection for sensitive documents
- [ ] Achieve continuous data monitoring with automated policy enforcement
- [ ] Integrate data lineage tracking into the ZTA decision framework

## Cross-Cutting: Visibility and Analytics

- [ ] Deploy a SIEM with centralized log aggregation from all ZTA components
- [ ] Implement user and entity behavior analytics (UEBA)
- [ ] Configure dashboards for Zero Trust metrics (access requests, denials, anomalies)
- [ ] Establish alert thresholds and automated response playbooks
- [ ] Conduct regular analysis of access patterns to refine policies
- [ ] Implement threat intelligence integration with the PE
- [ ] Achieve full audit trail for all access decisions (who, what, when, where, why, outcome)

## Cross-Cutting: Automation and Orchestration

- [ ] Automate device compliance remediation (quarantine, patching, re-enrollment)
- [ ] Automate identity lifecycle management (onboarding, role changes, offboarding)
- [ ] Implement automated incident response for common Zero Trust alerts
- [ ] Automate policy updates based on threat intelligence
- [ ] Deploy infrastructure as code (IaC) for ZTA component configuration
- [ ] Implement automated testing of Zero Trust policies and enforcement

## Cross-Cutting: Governance

- [ ] Document Zero Trust policies and standards
- [ ] Establish a regular review cycle for access policies (at least quarterly)
- [ ] Conduct annual Zero Trust maturity assessments using the CISA ZTMM
- [ ] Report Zero Trust progress to executive leadership quarterly
- [ ] Integrate Zero Trust requirements into procurement and vendor management
- [ ] Ensure compliance with regulatory requirements (EO 14028, OMB M-22-09, CMMC, HIPAA, etc.)

---

**Need help building your Zero Trust roadmap?** Contact Petronella Technology Group at 919-348-4912 or visit [https://petronellatech.com/compliance/nist-800-207-zero-trust/](https://petronellatech.com/compliance/nist-800-207-zero-trust/) for expert guidance.
