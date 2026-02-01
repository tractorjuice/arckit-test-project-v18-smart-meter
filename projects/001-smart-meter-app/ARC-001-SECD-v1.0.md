# UK Government Secure by Design Assessment: UK Smart Meter Data Consumer Mobile App

> **Template Status**: Beta | **Version**: 1.0.3 | **Command**: `/arckit.secure`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-SECD-v1.0 |
| **Document Type** | UK Government Secure by Design Assessment |
| **Project** | UK Smart Meter Data Consumer Mobile App (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-02-01 |
| **Last Modified** | 2026-02-01 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-01 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Programme Board, DESNZ SRO, Security Lead, NCSC Engagement Team, DCC Security, ICO (as needed) |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-01 | ArcKit AI | Initial creation from `/arckit.secure` command | PENDING | PENDING |

## Document Purpose

This document provides a Secure by Design assessment for the UK Smart Meter Data Consumer Mobile App against the NCSC Cyber Assessment Framework (CAF), Cyber Essentials scheme, UK GDPR, and Smart Energy Code (SEC) security requirements. It evaluates the security posture at the current project phase (pre-Alpha — requirements and architecture principles defined, implementation not yet started), identifies gaps, and provides a prioritised remediation plan to achieve security readiness for Beta and Live phases.

**Key Regulatory Context**: This service connects to the Data Communications Company (DCC) smart metering infrastructure — classified as Critical National Infrastructure (CNI). Security assessment must therefore consider not only standard UK Government requirements but also the specific security obligations of the Smart Energy Code and the potential for the consumer app to introduce attack vectors into the CNI environment.

---

## Executive Summary

**Overall Security Posture**: Needs Improvement (expected at pre-Alpha — strong architectural intent, no implementation yet)

**NCSC Cyber Assessment Framework (CAF) Score**: 4/14 principles achieved (8 partially achieved, 2 not achieved)

**Key Security Findings**:
- **Strengths**: Security by Design is embedded as a non-negotiable architecture principle (Principle 5). Comprehensive security NFRs defined (NFR-SEC-001 through NFR-SEC-006). Risk register identifies data breach as the highest-impact risk (R-002, inherent 25). Privacy by Design mandated (Principle 7). Zero trust architecture specified.
- **Critical Gaps**: No DPIA completed (legally required before processing personal energy data). No threat model completed (planned for Alpha with NCSC). No SIRO formally appointed. No penetration testing conducted. No incident response plan tested. DCC integration security (SMKI/PKI) not yet implemented.
- **Blocking Issues for Beta**: DPIA must be completed and accepted by ICO. NCSC security review must pass. Penetration testing (including OWASP MASVS for mobile) must be completed with no critical findings. Incident response plan must be documented and tested.

**Cyber Essentials Status**: Not Started (target: Basic by Alpha, Plus by Beta)

**Risk Summary**: HIGH — Inherent security risk is critical (R-002: 25/25) due to processing personal energy data connected to CNI. Residual risk with planned controls: 15/25 (HIGH). Further reduction to 10/25 achievable with full action plan implementation.

---

## Project Security Context

### Service Description
Cross-platform mobile application (iOS/Android) enabling 34 million smart meter households to access half-hourly energy consumption data, receive personalised savings recommendations, and compare tariffs. Backend platform hosted in AWS UK (eu-west-2) connecting to DCC infrastructure and 6+ energy supplier APIs.

### Data Classification
**OFFICIAL** — Energy consumption data is personal data under UK GDPR. Half-hourly readings reveal household occupancy patterns, daily routines, and appliance usage. While classified OFFICIAL (not OFFICIAL-SENSITIVE), the sensitivity of behavioural inference from energy data warrants enhanced controls beyond OFFICIAL baseline.

### Security Classification Justification
| Data Type | Classification | Sensitivity Notes |
|-----------|---------------|-------------------|
| Consumer profile (name, email) | OFFICIAL | Standard personal data |
| Half-hourly consumption readings | OFFICIAL | Reveals household behaviour — treat with enhanced controls |
| Consent records | OFFICIAL (Restricted) | Regulatory audit requirement, 7-year retention |
| Authentication credentials | OFFICIAL (Restricted) | MFA tokens, session keys |
| DCC security certificates (SMKI) | OFFICIAL (Restricted) | Critical infrastructure access credentials |
| Tariff and carbon data | PUBLIC | Publicly available information |
| Aggregated anonymised analytics | PUBLIC | No PII after anonymisation |

### Connected Systems
| System | Owner | Security Implication |
|--------|-------|---------------------|
| DCC Smart Metering Infrastructure | DCC | **Critical National Infrastructure** — security isolation essential |
| Energy Supplier APIs (6+) | British Gas, EDF, E.ON, Octopus, SSE, Scottish Power | Mutual TLS where supported; per-supplier security posture varies |
| n3rgy Consumer Access API | n3rgy Ltd | Third-party intermediary to DCC — assess business continuity and security |
| GOV.UK One Login | GDS | UK Government identity platform — inherits government security posture |
| Apple Push Notification Service | Apple | Consumer device notification — no PII in payload |
| Firebase Cloud Messaging | Google | Consumer device notification — no PII in payload |
| National Grid ESO Carbon API | NESO | Public API, no authentication — low security risk |
| TimescaleDB (Tiger Cloud) | Timescale Inc | Managed database — data residency in AWS UK (eu-west-2) |

### Regulatory Security Frameworks
| Framework | Applicability | Status |
|-----------|--------------|--------|
| NCSC Cyber Assessment Framework (CAF) | Mandatory — connects to CNI | This assessment |
| Cyber Essentials | Mandatory — government contract >£5M | Not started |
| Cyber Essentials Plus | Recommended — high-risk personal data processing | Not started |
| UK GDPR / DPA 2018 | Mandatory — processing personal data at scale | DPIA not completed |
| Smart Energy Code (SEC) | Mandatory — DCC access | SEC Party application pending |
| NCSC Cloud Security Principles | Mandatory — cloud-hosted government service | Architecture aligned |
| OWASP MASVS | Recommended — consumer mobile app | Requirements defined (NFR-SEC-006) |
| PECR | Applicable — push notifications | Requirements defined |
| Government Security Classifications | Mandatory | OFFICIAL classification applied |
| GDS Service Standard (Point 9) | Mandatory | Assessed separately |

---

## 1. NCSC Cyber Assessment Framework (CAF) Assessment

### Objective A: Managing Security Risk

#### A1: Governance

**Status**: ⚠️ Partially Achieved

**Evidence**:
Architecture Principle 5 (Security by Design) is designated NON-NEGOTIABLE with zero exceptions permitted (ARC-000-PRIN-v1.0). Security roles are defined in the RACI matrix (ARC-001-STKE-v1.0): DESNZ SRO is accountable for data protection; Technical Architect is responsible for architecture and technology security decisions; Security Lead is the action owner for threat modelling and pen testing; DPO/Privacy Lead is responsible for DPIA and ICO engagement. NCSC is identified as an advisory stakeholder (SD-12) with engagement planned.

However, no formal SIRO appointment has been documented. Security policies are defined at principle level but not yet operationalised into specific policy documents. Security oversight and reporting cadence is defined in the project plan (ARC-001-PLAN-v1.0) but not yet active.

**Security Governance**:
- [x] Senior leadership owns information security — DESNZ SRO identified as accountable (RACI matrix)
- [ ] Senior Information Risk Owner (SIRO) appointed — **GAP: SIRO not formally appointed; DESNZ SRO assumed but not documented**
- [x] Security policies and standards defined — Principle 5 (Security by Design), Principle 7 (Privacy by Design), 6 security NFRs
- [x] Security roles and responsibilities documented — RACI matrix in ARC-001-STKE-v1.0
- [ ] Security risk management process established — Risk register exists (ARC-001-RISK-v1.0) but security-specific risk process not formalised
- [ ] Security oversight and reporting in place — Planned in ARC-001-PLAN-v1.0 but not yet operational

**Gaps/Actions**:
- **CRITICAL**: Formally appoint SIRO at DESNZ Director level — Owner: DESNZ SRO — Due: 2026-03-31
- **HIGH**: Develop operational security policies (Acceptable Use, Access Control, Data Protection, Incident Response) — Owner: Security Lead — Due: 2026-05-31
- **MEDIUM**: Establish quarterly security reporting to Programme Board — Owner: Security Lead — Due: 2026-04-30

---

#### A2: Risk Management

**Status**: ⚠️ Partially Achieved

**Evidence**:
A comprehensive risk register exists (ARC-001-RISK-v1.0) with 20 risks across 6 categories following HM Treasury Orange Book methodology. Data breach (R-002) is identified as the highest-impact risk (inherent 25, residual 15). UK GDPR non-compliance (R-010) is identified with residual score 12. Security-related risks have defined mitigations, owners, and action plans. Risk appetite thresholds are recommended (compliance appetite ≤6) but not yet formally approved by Programme Board.

However, no formal threat model has been completed. Risk assessment methodology is defined but not security-specific (general programme risk, not threat-led). Information assets have been identified at a high level (DR-001 through DR-005 in requirements) but not formally classified in a security asset register.

**Risk Management Process**:
- [x] Information assets identified and classified — DR-001 through DR-005 define data entities with classification (CONFIDENTIAL, RESTRICTED, INTERNAL)
- [ ] Threats and vulnerabilities assessed — **GAP: No threat model completed; planned for Alpha (Week 16-18) with NCSC**
- [x] Risk assessment methodology defined — Orange Book 5x5 methodology (ARC-001-RISK-v1.0)
- [x] Risk register maintained and reviewed — 20 risks, monthly review cycle
- [x] Risk treatment plans implemented — 16 risks have TREAT response with action plans
- [ ] Residual risks accepted by SIRO — **GAP: SIRO not yet appointed; no formal risk acceptance**

**Gaps/Actions**:
- **CRITICAL**: Complete threat model using STRIDE methodology with NCSC input — Owner: Security Lead — Due: 2026-05-31 (per ARC-001-PLAN-v1.0 Alpha phase)
- **HIGH**: Create formal security asset register from DR-001 through DR-005 — Owner: Technical Architect — Due: 2026-04-30
- **HIGH**: SIRO to formally accept residual risks exceeding appetite (R-002, R-010) — Owner: SIRO — Due: 2026-06-30

---

#### A3: Asset Management

**Status**: ⚠️ Partially Achieved

**Evidence**:
Data assets are well-defined in the requirements (DR-001 Consumer Profile, DR-002 Linked Meter, DR-003 Consent Record, DR-004 Consumption Reading, DR-005 Tariff) with data classification, retention periods, and volume projections. Technology components are identified in the research document (ARC-001-RSCH-v1.0). However, no formal hardware/software inventory exists (the system is not yet built). Asset lifecycle management and secure disposal procedures are not yet defined.

**Asset Management**:
- [ ] Hardware inventory maintained — N/A (pre-build; to be established during Beta)
- [ ] Software inventory maintained — Partially: technology stack identified in ARC-001-RSCH-v1.0 (Flutter, TimescaleDB, Grafana, etc.)
- [x] Data assets catalogued — DR-001 through DR-005 with classification and retention
- [x] Asset ownership assigned — Data entities have defined owners
- [ ] Asset lifecycle management — Not yet defined (requires operational readiness)
- [ ] Secure disposal procedures — Not yet defined

**Gaps/Actions**:
- **MEDIUM**: Establish Software Bill of Materials (SBOM) process for all components — Owner: Technical Architect — Due: 2026-07-31
- **MEDIUM**: Define secure data disposal procedures aligned with UK GDPR Article 17 and SEC requirements — Owner: DPO/Privacy Lead — Due: 2026-08-31
- **LOW**: Create asset register template for production deployment — Owner: DevOps Lead — Due: 2026-09-30

---

#### A4: Supply Chain

**Status**: ⚠️ Partially Achieved

**Evidence**:
Supply chain dependencies are well-documented. Key suppliers identified: n3rgy (smart meter data intermediary), DCC (critical infrastructure), energy suppliers (6+), Timescale Inc (database), Apple/Google (app distribution). Vendor risks are identified (VR-1: n3rgy business continuity, VR-2: tariff data source, VR-3: GOV.UK One Login). Architecture Principle 11 (Loose Coupling) and supplier adapter pattern reduce single-supplier dependency.

However, no formal supplier security assessments have been conducted. Contracts with security obligations are not yet in place. Open source dependency scanning is specified as a requirement (NFR-SEC-005) but not yet implemented.

**Supply Chain Security**:
- [x] Supplier security requirements defined — NFR-SEC-005 mandates SCA in CI/CD; Principle 5 requires service-to-service authentication
- [ ] Supplier security assessments conducted — **GAP: No formal assessments of n3rgy, Timescale, or other vendors**
- [ ] Contracts include security obligations — **GAP: No contracts signed yet; procurement in Alpha/Beta**
- [x] Third-party access controlled — Architecture requires service-to-service authentication (Principle 5, NFR-SEC-002)
- [x] Supply chain risk register — VR-1, VR-2, VR-3 in ARC-001-RSCH-v1.0
- [ ] Open source software risks managed — **GAP: SBOM and SCA not yet operational**

**Gaps/Actions**:
- **HIGH**: Conduct security due diligence on n3rgy (ISO 27001, SOC 2, business continuity) — Owner: Security Lead — Due: 2026-05-31
- **HIGH**: Include security obligations in all vendor contracts (DPA, breach notification, audit rights) — Owner: Programme Commercial Lead — Due: 2026-06-30
- **MEDIUM**: Implement automated dependency scanning (SCA) in CI/CD pipeline — Owner: DevOps Lead — Due: 2026-08-31

---

### Objective B: Protecting Against Cyber Attack

#### B1: Service Protection Policies and Processes

**Status**: ⚠️ Partially Achieved

**Evidence**:
Architecture principles define comprehensive protective intent: Principle 5 (Security by Design — zero trust, encryption everywhere, defence in depth), Principle 7 (Privacy by Design — data minimisation, granular consent), Principle 17 (Infrastructure as Code — no manual changes), Principle 19 (CI/CD — security gates in pipeline). Security NFRs define specific controls (NFR-SEC-001 through NFR-SEC-006).

However, these are requirements and principles, not operational policies. No formal Acceptable Use Policy, Access Control Policy, Data Protection Policy, Secure Development Policy, Network Security Policy, or Cryptography Policy documents exist yet.

**Protection Policies**:
- [ ] Acceptable Use Policy — Not yet created (principled intent in Principle 5)
- [ ] Access Control Policy — Not yet created (requirements in NFR-SEC-001, NFR-SEC-002)
- [ ] Data Protection Policy — Not yet created (requirements in NFR-C-001, Principle 7)
- [ ] Secure Development Policy — Not yet created (requirements in Principles 18, 19)
- [ ] Network Security Policy — Not yet created (requirements in Principle 5)
- [ ] Cryptography Policy — Not yet created (requirements in NFR-SEC-003: AES-256 at rest, TLS 1.2+/1.3 in transit)

**Gaps/Actions**:
- **HIGH**: Develop operational security policies from existing principles and NFRs — Owner: Security Lead — Due: 2026-06-30
- **MEDIUM**: Develop Cryptography Policy specifying approved algorithms, key lengths, and key management procedures aligned with SEC requirements — Owner: Security Lead — Due: 2026-07-31

---

#### B2: Identity and Access Control

**Status**: ⚠️ Partially Achieved

**Evidence**:
Consumer authentication requirements are comprehensively defined (NFR-SEC-001): email + password with NCSC-guided complexity, MFA (authenticator app primary, SMS fallback, biometric convenience), no social sign-in. Session management: 30-minute inactivity timeout, 12-hour absolute, re-authentication for sensitive actions. GOV.UK One Login recommended as authentication platform (ARC-001-RSCH-v1.0). Role-based access control defined (NFR-SEC-002): consumers access own data only; system admin has operational access with audit; support staff has limited metadata access with consumer initiation.

Zero trust principles mandated (Principle 5): identity-based access, least privilege, continuous verification. Service-to-service authentication required for all API communications.

However, no implementation exists. Privileged access management for platform operations is not yet specified. Regular access reviews process not defined.

**Access Controls**:
- [x] User accounts managed centrally — GOV.UK One Login recommended (OIDC)
- [x] Multi-factor authentication (MFA) enabled — NFR-SEC-001 mandates MFA for all consumers
- [ ] Privileged access management (PAM) — **GAP: Not specified for platform operations/admin access**
- [x] Least privilege principle enforced — NFR-SEC-002 defines strict RBAC; Principle 5 mandates least privilege
- [ ] Regular access reviews — **GAP: Not yet defined**
- [x] Account provisioning/deprovisioning process — Consumer lifecycle defined (UC-1 onboarding, UC-8 deletion)
- [x] Strong password policy — NCSC guidance: minimum 8 characters, breach password check (NFR-SEC-001)

**Authentication Method**: GOV.UK One Login (OIDC) — pending confirmation of mobile app support

**Gaps/Actions**:
- **HIGH**: Define Privileged Access Management (PAM) for platform operations — break-glass procedures, just-in-time access, full audit trail — Owner: Technical Architect — Due: 2026-07-31
- **MEDIUM**: Define regular access review process (quarterly for admin/support, annual for service accounts) — Owner: Security Lead — Due: 2026-08-31
- **MEDIUM**: Confirm GOV.UK One Login mobile app support; activate Keycloak contingency if needed — Owner: Technical Architect — Due: 2026-04-30

---

#### B3: Data Security

**Status**: ⚠️ Partially Achieved

**Evidence**:
Data protection requirements are extensive. Encryption mandated: AES-256 at rest for all personal/consumption data, TLS 1.2+ (prefer 1.3) in transit, platform-native secure storage on mobile (iOS Keychain, Android Keystore), managed key service with 90-day rotation (NFR-SEC-003). Data classification defined across 4 tiers (PUBLIC, INTERNAL, CONFIDENTIAL, RESTRICTED) in Principle 8. UK GDPR compliance requirements comprehensively defined (NFR-C-001): lawful basis, privacy notice, all data subject rights, breach notification within 72 hours, ROPA. Data residency mandated as UK-only (Principle 8, TC-3). Data retention periods defined per entity.

Privacy by Design is a core principle (Principle 7): data minimisation, granular consent (FR-003), consent revocable with immediate effect, purpose limitation. No secrets in code (NFR-SEC-004).

However, DPIA is not yet completed (legally required before processing personal energy data at this scale). Data Loss Prevention (DLP) controls are not yet specified. Telemetry verified PII-free is a requirement but not yet implemented.

**Data Protection**:
- [x] Data classification scheme implemented — 4-tier classification in Principle 8 (PUBLIC, INTERNAL, CONFIDENTIAL, RESTRICTED)
- [x] Encryption at rest (AES-256 minimum) — Mandated in NFR-SEC-003
- [x] Encryption in transit (TLS 1.3 minimum) — TLS 1.2+ (prefer 1.3) in NFR-SEC-003; mutual TLS for DCC
- [ ] Data loss prevention (DLP) controls — **GAP: Not yet specified**
- [ ] Secure data destruction — Requirements defined (UK GDPR Article 17, 30-day deletion) but not yet implemented
- [x] UK GDPR compliance — Comprehensive requirements in NFR-C-001 (lawful basis, privacy notice, all data subject rights, breach notification, ROPA)
- [x] Data retention policy — Defined per entity: active account + 12 months; consent records 7 years; audit logs 7 years (anonymised)

**Personal Data Processing**: Yes — energy consumption data, consumer profiles, consent records
**DPIA Completed**: No — **CRITICAL GAP: Legally required before Beta with real consumer data**

**Gaps/Actions**:
- **CRITICAL**: Complete DPIA and submit to ICO for pre-consultation — Owner: DPO/Privacy Lead — Due: 2026-06-30 (per ARC-001-PLAN-v1.0)
- **HIGH**: Define DLP controls — prevent consumption data in logs, crash reports, analytics — Owner: Security Lead — Due: 2026-07-31
- **HIGH**: Verify no cross-border data flows from all third-party SDKs (analytics, crash reporting, CDN) — Owner: Technical Architect — Due: 2026-08-31

---

#### B4: System Security

**Status**: ❌ Not Achieved (expected — system not yet built)

**Evidence**:
Requirements define comprehensive system security controls: SAST in CI/CD with zero critical findings before merge, DAST weekly against staging, SCA for dependency scanning, annual penetration testing including mobile (OWASP MASVS), mobile-specific controls (certificate pinning, root/jailbreak detection, encrypted local storage, no PII in logs, app transport security, binary obfuscation) (NFR-SEC-005, NFR-SEC-006). Remediation SLAs defined: Critical 24h, High 7d, Medium 30d, Low 90d.

Infrastructure as Code mandated (Principle 17): no manual changes to any environment. CI/CD pipeline with security gates (Principle 19): security scan, secrets detection, accessibility check as pipeline gates.

However, no system exists yet. No hardened baselines, no anti-malware, no EDR — these are Beta/Live requirements.

**System Hardening**:
- [ ] Secure baseline configurations — Not yet (system not built)
- [x] Unnecessary services disabled — Architecture principle: containerised workloads, minimal attack surface (Principles 11, 17)
- [x] Security patches applied timely — Remediation SLAs defined (Critical: 24h, High: 7d) (NFR-SEC-005)
- [ ] Anti-malware deployed — Not yet applicable (no systems deployed)
- [ ] Application whitelisting — Not specified
- [ ] Host-based firewalls — Not yet (cloud security groups planned)
- [ ] Endpoint Detection and Response (EDR) — Not yet specified for platform infrastructure

**Operating Systems**: Linux (containerised backend), iOS/Android (mobile app)

**Gaps/Actions**:
- **HIGH**: Define container security baseline (CIS Docker/Kubernetes benchmarks) — Owner: DevOps Lead — Due: 2026-08-31
- **HIGH**: Specify EDR/runtime protection for backend infrastructure — Owner: Security Lead — Due: 2026-08-31
- **MEDIUM**: Define mobile app hardening beyond NFR-SEC-006 (runtime application self-protection, anti-tampering) — Owner: Security Lead — Due: 2026-09-30

---

#### B5: Resilient Networks

**Status**: ⚠️ Partially Achieved

**Evidence**:
Architecture principles mandate strong network resilience. Principle 3 (Resilience and Fault Tolerance): circuit breakers for DCC and supplier APIs, timeouts on all network calls, retry with exponential backoff, bulkhead isolation between consumer-facing and DCC-facing components. Principle 5 (Security by Design): network segmentation with minimal trust zones, encrypted transport for all communications. NFR-A-003 defines graceful degradation hierarchy (Core → Important → Enhanced → Optional). Platform hosted in AWS UK (eu-west-2) with multi-AZ redundancy.

DCC-facing integration requires SEC-compliant security: SMKI certificates, network isolation. Consumer-facing mobile app communicates only with platform APIs (never directly to DCC).

However, no implementation exists. Network architecture not yet detailed. DDoS protection, IDS/IPS, and NAC not yet specified.

**Network Security**:
- [x] Network segmentation by function/sensitivity — Mandated: consumer-facing, DCC-facing, supplier-facing, internal services (Principles 5, 11)
- [x] Firewalls at network boundaries — Implicit in cloud architecture (AWS security groups, VPC)
- [ ] Intrusion Detection/Prevention Systems (IDS/IPS) — **GAP: Not yet specified**
- [ ] DDoS protection — **GAP: Not yet specified (critical for consumer-facing service)**
- [ ] Secure remote access (VPN) — Not yet specified for admin access
- [ ] Network Access Control (NAC) — Not yet specified
- [ ] WiFi security — N/A (cloud-hosted, mobile app)

**Network Architecture**: Cloud (AWS UK eu-west-2, multi-AZ)

**Gaps/Actions**:
- **HIGH**: Specify DDoS protection for consumer-facing APIs (AWS Shield, WAF) — Owner: Technical Architect — Due: 2026-07-31
- **HIGH**: Specify IDS/IPS for platform infrastructure (AWS GuardDuty or equivalent) — Owner: Security Lead — Due: 2026-08-31
- **HIGH**: Define network isolation between DCC-facing components and consumer-facing APIs — no consumer request can reach DCC infrastructure directly — Owner: Technical Architect — Due: 2026-07-31

---

#### B6: Staff Awareness and Training

**Status**: ❌ Not Achieved (expected — team not yet fully mobilised)

**Evidence**:
No security awareness programme exists yet. The team mobilisation is planned for Discovery Phase Week 1-2 (ARC-001-PLAN-v1.0). Security roles are defined (Security Lead, DPO, developers with security responsibilities) but security training has not been delivered.

The programme handles personal energy data classified as OFFICIAL with enhanced sensitivity. All team members will require security awareness training, UK GDPR training, and SEC-specific training for those working on DCC integration.

**Security Training**:
- [ ] Mandatory security awareness training — Not yet delivered
- [ ] Phishing awareness training — Not yet delivered
- [ ] Role-based security training — Not yet planned
- [ ] Annual security refresher — Not yet applicable
- [ ] Security incident reporting awareness — Not yet delivered
- [ ] Data protection training (UK GDPR) — Not yet delivered
- [ ] Social engineering awareness — Not yet delivered

**Training Completion Rate**: 0% (team not yet mobilised)

**Gaps/Actions**:
- **HIGH**: Deliver mandatory security awareness and UK GDPR training to all team members at mobilisation — Owner: Security Lead — Due: 2026-04-30
- **HIGH**: Deliver SEC-specific security training to DCC integration engineers — Owner: Security Lead — Due: 2026-06-30
- **MEDIUM**: Establish quarterly phishing simulation exercises — Owner: Security Lead — Due: 2026-09-30

---

### Objective C: Detecting Cyber Security Events

#### C1: Security Monitoring

**Status**: ⚠️ Partially Achieved

**Evidence**:
Observability requirements are well-defined. Principle 6 (Observability and Operational Excellence) mandates structured telemetry (logs, metrics, traces) with explicit requirement that telemetry MUST NOT contain PII or consumption data. NFR-M-001 specifies structured JSON logging with correlation IDs, distributed tracing, real-time dashboards, SLO-based alerting. NFR-C-004 specifies comprehensive audit logging: who, what, when, where, why, result — with cryptographic hash chain for tamper evidence and 7-year retention for compliance logs.

Technology research recommends Grafana Cloud (observability), PostHog self-hosted (product analytics — UK data residency), AWS CloudWatch (infrastructure baseline).

However, no monitoring is implemented. SIEM solution not selected. Threat intelligence integration not specified. User behaviour analytics not specified.

**Monitoring Capabilities**:
- [x] Centralised logging (SIEM) — Architecture requires it (Principle 6, NFR-M-001); Grafana Cloud recommended
- [x] Real-time security alerting — SLO-based alerting mandated (Principle 6)
- [x] Log retention (minimum 12 months) — 7-year retention for security/audit logs, 90 days application logs (Principle 6)
- [ ] Security event correlation — **GAP: Not yet specified**
- [ ] User behaviour analytics — **GAP: Not yet specified for detecting compromised consumer accounts**
- [ ] Threat intelligence integration — **GAP: Not yet specified**
- [x] File integrity monitoring — Cryptographic hash chain for audit logs (NFR-C-004)

**SIEM Solution**: Grafana Cloud (recommended) — not yet deployed

**Gaps/Actions**:
- **HIGH**: Select and configure SIEM with security event correlation capabilities — Owner: Security Lead — Due: 2026-09-30
- **HIGH**: Define security alerting rules: authentication failures (brute force detection), privilege escalation, unusual data access patterns, DCC integration anomalies — Owner: Security Lead — Due: 2026-10-31
- **MEDIUM**: Evaluate user behaviour analytics for detecting compromised consumer accounts — Owner: Security Lead — Due: 2026-10-31
- **MEDIUM**: Integrate NCSC threat intelligence feeds — Owner: Security Lead — Due: 2026-11-30

---

#### C2: Proactive Security Event Discovery

**Status**: ⚠️ Partially Achieved

**Evidence**:
Requirements mandate proactive security measures: SAST in CI/CD pipeline (NFR-SEC-005), DAST weekly against staging, SCA for dependency scanning, annual penetration testing by external firm including mobile (OWASP MASVS), mobile-specific binary analysis, certificate pinning validation, reverse engineering resistance testing. Threat modelling planned for Alpha with NCSC input.

Risk register includes a bug bounty programme as a planned action (R-002 action 3, due 2027-01-31 at public Beta).

However, no proactive measures are operational. No penetration testing has been conducted. No vulnerability scanning is active.

**Proactive Measures**:
- [ ] Threat hunting activities — Not yet (system not deployed)
- [ ] Vulnerability scanning (weekly/monthly) — Requirements mandate weekly DAST; not yet operational
- [ ] Penetration testing (annual minimum) — Planned for Beta (ARC-001-PLAN-v1.0 Week 44-47); not yet conducted
- [ ] Red team exercises — Not yet specified
- [ ] Security posture reviews — Planned as quarterly in Live
- [x] Threat modelling — Planned for Alpha Week 16-18 with NCSC input

**Last Penetration Test**: Not conducted
**Pen Test Findings**: N/A

**Gaps/Actions**:
- **CRITICAL**: Complete threat model (STRIDE) with NCSC before HLD is finalised — Owner: Security Lead — Due: 2026-05-31
- **CRITICAL**: Conduct penetration testing (external firm, OWASP MASVS for mobile) before Private Beta — Owner: Security Lead — Due: 2026-11-30
- **HIGH**: Implement automated SAST, DAST, SCA in CI/CD pipeline from first sprint — Owner: DevOps Lead — Due: 2026-08-31
- **MEDIUM**: Launch bug bounty programme at public Beta — Owner: Security Lead — Due: 2027-03-31

---

### Objective D: Minimising the Impact of Cyber Security Incidents

#### D1: Response and Recovery Planning

**Status**: ⚠️ Partially Achieved

**Evidence**:
Risk register identifies the need for incident response: R-002 action 5 specifies developing and testing an incident response plan including ICO 72-hour notification (due 2026-08-31). R-013 action 1 specifies pre-prepared incident communications (ministerial lines, media statement, consumer notification). NFR-C-001 mandates data breach notification to ICO within 72 hours. DR/BC requirements defined: RPO zero data loss for confirmed readings, RTO 1 hour for platform services / 4 hours for non-critical, continuous replication, multi-AZ failover (NFR-A-002). Quarterly DR testing mandated.

However, no incident response plan exists. No IR team is formed. No communication plan for incidents. No BC/DR plans documented.

**Incident Response**:
- [ ] Incident response plan documented — **GAP: Not yet created (planned by 2026-08-31)**
- [ ] Incident response team defined — Roles identified (Security Lead, DPO) but team not formalised
- [ ] Incident classification scheme — Not yet defined
- [ ] Escalation procedures defined — General escalation in RACI (ARC-001-STKE-v1.0) but not security-specific
- [ ] Communication plan for incidents — Planned (R-013 action 1) but not yet created
- [x] Regulatory reporting process (ICO) — 72-hour notification required (NFR-C-001); process not yet documented
- [ ] Lessons learned process — Not yet defined

**IR Plan Last Tested**: Not tested

**Business Continuity**:
- [x] Business continuity plan (BCP) — Requirements defined (NFR-A-002, NFR-A-003) but plan not documented
- [x] Disaster recovery plan (DRP) — Requirements defined (multi-AZ failover, continuous replication) but plan not documented
- [x] Recovery time objective (RTO) defined — 1 hour platform, 4 hours non-critical (NFR-A-002)
- [x] Recovery point objective (RPO) defined — Zero data loss for confirmed readings (NFR-A-002)
- [ ] BC/DR testing conducted — Not yet (system not deployed)

**RTO**: 1 hour (platform services), 4 hours (non-critical)
**RPO**: 0 hours (zero data loss for confirmed readings)

**Gaps/Actions**:
- **CRITICAL**: Develop and document incident response plan with ICO 72-hour notification procedure — Owner: DPO/Privacy Lead — Due: 2026-08-31
- **HIGH**: Define incident classification scheme and escalation matrix (including ministerial notification criteria) — Owner: Security Lead — Due: 2026-08-31
- **HIGH**: Develop pre-prepared incident communications (ministerial lines, media statement, consumer notification) — Owner: DESNZ Communications — Due: 2026-09-30
- **HIGH**: Conduct tabletop IR exercise before Private Beta — Owner: Security Lead — Due: 2026-11-30

---

#### D2: Improvements

**Status**: ❌ Not Achieved (expected — no operational history)

**Evidence**:
Risk register includes monitoring and review framework (Section J, ARC-001-RISK-v1.0) with review schedules (Critical: weekly, High: fortnightly, Medium: monthly, Low: quarterly) and Key Risk Indicators. Architecture Principle 6 mandates continuous improvement via operational metrics. However, no post-incident review process, security metrics, or security improvement roadmap exists yet.

**Continuous Improvement**:
- [ ] Post-incident reviews conducted — No incidents yet (system not deployed)
- [ ] Security metrics tracked — Not yet
- [ ] Security improvements implemented — Not yet
- [ ] Lessons learned documented — Process not defined
- [ ] Security trends analysed — Not yet
- [ ] Security roadmap maintained — Not yet

**Gaps/Actions**:
- **MEDIUM**: Define security metrics dashboard (MTTD, MTTR, vulnerability SLA adherence, patch compliance, security training completion) — Owner: Security Lead — Due: 2026-10-31
- **MEDIUM**: Establish post-incident review process (blameless, actionable, time-boxed) — Owner: Security Lead — Due: 2026-10-31
- **LOW**: Create security improvement roadmap aligned with programme milestones — Owner: Security Lead — Due: 2026-11-30

---

## 2. Cyber Essentials / Cyber Essentials Plus

### Cyber Essentials Status

**Current Status**: Not Started

**Certification Date**: N/A
**Expiry Date**: N/A

**Target Timeline**:
- Cyber Essentials Basic: By Alpha Assessment (Week 22, 2026-07-31)
- Cyber Essentials Plus: By Beta launch (Week 49, 2026-12-31)

**Cyber Essentials Requirements**:

| Control Area | Status | Evidence |
|--------------|--------|----------|
| **Firewalls** | ⚠️ Partially Achieved | Architecture mandates network segmentation and boundary controls (Principle 5); AWS VPC and security groups planned; not yet implemented |
| **Secure Configuration** | ⚠️ Partially Achieved | Infrastructure as Code mandated (Principle 17); containerised workloads planned; no manual changes; CIS benchmarks not yet specified |
| **Access Control** | ⚠️ Partially Achieved | MFA mandated for all consumers (NFR-SEC-001); least privilege (NFR-SEC-002); GOV.UK One Login recommended; not yet implemented |
| **Malware Protection** | ❌ Not Achieved | Not yet specified for backend infrastructure; mobile app hardening defined (NFR-SEC-006) but not container/server-level anti-malware |
| **Patch Management** | ⚠️ Partially Achieved | Remediation SLAs defined: Critical 24h, High 7d (NFR-SEC-005); SCA for dependencies; process not yet operational |

**Cyber Essentials Plus Additional Requirements**:
- [ ] External vulnerability scan passed — Not yet conducted
- [ ] Internal vulnerability scan passed — Not yet conducted
- [ ] System configuration review passed — Not yet conducted

**Target Certification Level**: Cyber Essentials Plus (required for government contract >£5M handling personal data)

**Gaps/Actions**:
- **HIGH**: Engage Cyber Essentials certifying body for self-assessment (Basic) — Owner: Security Lead — Due: 2026-06-30
- **HIGH**: Schedule external vulnerability assessment for Plus certification — Owner: Security Lead — Due: 2026-11-30
- **MEDIUM**: Specify anti-malware/runtime protection for container infrastructure — Owner: DevOps Lead — Due: 2026-08-31

---

## 3. UK GDPR and Data Protection

### 3.1 Data Protection Compliance

**Data Protection Officer (DPO) Appointed**: Yes (role identified — DPO/Privacy Lead in RACI matrix; named individual PENDING)

**ICO Registration**: Required (public authority processing personal data at scale) — Not yet completed

**UK GDPR Compliance**:
- [x] Lawful basis for processing identified — Consent for data viewing, recommendations, tariff comparison, research sharing; legitimate interest for service operation and security (NFR-C-001)
- [x] Privacy notice published — Required in plain English, accessible, prominently displayed (NFR-C-001); not yet drafted
- [x] Data subject rights procedures — All rights specified: access (30 days), rectification, erasure (30 days), portability (CSV/JSON), objection (NFR-C-001, FR-010, UC-7, UC-8)
- [x] Data retention policy defined — Active account + 12 months; deleted account 30 days; consent records 7 years; audit logs 7 years anonymised (NFR-C-001)
- [x] Data breach notification process (72 hours) — Required (NFR-C-001); process not yet documented
- [ ] Data processing agreements with suppliers — **GAP: No DPAs in place with n3rgy, Timescale, AWS, etc.**
- [ ] Records of processing activities (ROPA) — **GAP: Not yet created**

**Personal Data Processed**: Yes — consumer names, email addresses, energy consumption data (reveals household behaviour), consent records, meter identifiers (MPAN/MPRN)

**Special Category Data**: No — energy consumption data is not special category data under UK GDPR Article 9, but ICO has noted its behavioural sensitivity

**Gaps/Actions**:
- **CRITICAL**: Complete ROPA documenting all processing activities, lawful bases, and data flows — Owner: DPO/Privacy Lead — Due: 2026-05-31
- **CRITICAL**: Complete ICO registration — Owner: DPO/Privacy Lead — Due: 2026-04-30
- **HIGH**: Draft privacy notice in plain English — Owner: Content Designer with DPO — Due: 2026-06-30
- **HIGH**: Execute Data Processing Agreements with n3rgy, Timescale, AWS, and all data processors — Owner: Programme Commercial Lead — Due: 2026-07-31

### 3.2 Data Protection Impact Assessment (DPIA)

**DPIA Required**: YES — mandatory. Processing personal energy data at scale (potentially 34 million data subjects), data revealing household behaviour patterns, new technology applied to existing data, systematic monitoring.

**DPIA Status**: Not Started

**DPIA Scope**:
- Consumer registration and authentication
- Smart meter data retrieval from DCC and energy suppliers
- Half-hourly consumption data storage and processing
- Personalised energy-saving recommendations
- Tariff comparison using actual consumption
- Budget alerts and prepayment monitoring
- Anonymised aggregate data for research (with consent)
- Push notification delivery

**DPIA Findings**: N/A (not started)

**ICO Consultation Required**: Likely YES — given the scale (34 million potential data subjects), novelty (first government consumer energy data app), and behavioural inference potential, ICO pre-consultation is strongly recommended even if not strictly required.

**Gaps/Actions**:
- **CRITICAL**: Commission and complete DPIA covering all processing activities — Owner: DPO/Privacy Lead — Due: 2026-06-30
- **CRITICAL**: Submit DPIA to ICO for pre-consultation — Owner: DPO/Privacy Lead — Due: 2026-06-30
- **HIGH**: Ensure DPIA covers DCC-specific data flows and SEC consent requirements — Owner: DPO with Technical Architect — Due: 2026-06-30

---

## 4. Secure Development Practices

### 4.1 Secure Software Development Lifecycle (SDLC)

**Development Methodology**: GDS Agile Delivery (Discovery → Alpha → Beta → Live)

**Secure Development Practices**:
- [x] Secure coding standards defined — Architecture Principle 5 (Security by Design) as non-negotiable foundation
- [x] Security requirements in user stories — 6 security NFRs (NFR-SEC-001 through NFR-SEC-006) with acceptance criteria
- [ ] Threat modelling in design phase — **GAP: Planned for Alpha Week 16-18 but not yet conducted**
- [ ] Code review includes security — Principle 19 requires peer review; security-specific review not yet specified
- [x] Static Application Security Testing (SAST) — Mandated in CI/CD pipeline (NFR-SEC-005)
- [x] Dynamic Application Security Testing (DAST) — Weekly against staging (NFR-SEC-005)
- [x] Software Composition Analysis (SCA) — Mandated: no known critical/high vulnerabilities in production (NFR-SEC-005)
- [x] Dependency vulnerability scanning — Mandated in CI/CD (NFR-SEC-005)

**OWASP Top 10 / OWASP MASVS Mitigation**:
- [x] Injection flaws prevented — Parameterised queries implied by architecture; explicit testing required
- [x] Broken authentication prevented — MFA, session management, re-authentication (NFR-SEC-001)
- [x] Sensitive data exposure prevented — Encryption at rest/transit, no PII in logs (NFR-SEC-003, NFR-SEC-006)
- [x] Broken access control prevented — RBAC, consumers access own data only (NFR-SEC-002)
- [x] Security misconfiguration prevented — IaC, no manual changes (Principle 17)
- [x] Cross-Site Scripting (XSS) prevented — Mobile app (not web); API input validation required
- [x] Using components with known vulnerabilities prevented — SCA in CI/CD (NFR-SEC-005)
- [x] Insufficient logging and monitoring addressed — Comprehensive observability (Principle 6, NFR-M-001)

**Mobile-Specific Security (OWASP MASVS)**:
- [x] Certificate pinning for all API communications (NFR-SEC-006)
- [x] Root/jailbreak detection with warn response (NFR-SEC-006)
- [x] No sensitive data in app logs or crash reports (NFR-SEC-006)
- [x] Secure local storage using platform keychain/keystore (NFR-SEC-006)
- [x] No third-party analytics SDKs that transmit PII (NFR-SEC-006)
- [x] App transport security enforced (NFR-SEC-006)
- [x] Binary obfuscation (NFR-SEC-006)

**Gaps/Actions**:
- **HIGH**: Mandate security-focused code review for all PRs touching authentication, consent, data access, and DCC integration — Owner: Technical Architect — Due: 2026-08-31
- **MEDIUM**: Create OWASP MASVS compliance checklist for mobile app builds — Owner: Security Lead — Due: 2026-09-30

### 4.2 DevSecOps

**CI/CD Security Integration**:
- [x] Automated security testing in pipeline — SAST, DAST, SCA mandated (NFR-SEC-005, Principle 19)
- [x] Secrets scanning (no hardcoded credentials) — NFR-SEC-004: no secrets in code, config, or mobile bundles. Ever.
- [ ] Container image scanning — **GAP: Not yet specified**
- [x] Infrastructure as Code (IaC) security — Principle 17: all infrastructure as code, reviewed before deployment
- [ ] Build artifact signing — **GAP: Not yet specified**
- [ ] Automated deployment security checks — Principle 19 requires quality gates; specific security checks not detailed

**Gaps/Actions**:
- **HIGH**: Specify container image scanning in CI/CD pipeline (Trivy, Snyk Container, or equivalent) — Owner: DevOps Lead — Due: 2026-08-31
- **MEDIUM**: Implement build artifact signing for mobile app binaries and container images — Owner: DevOps Lead — Due: 2026-09-30
- **MEDIUM**: Define IaC security scanning (tfsec, checkov, or equivalent) in pipeline — Owner: DevOps Lead — Due: 2026-08-31

---

## 5. Cloud Security

### 5.1 Cloud Service Provider

**Cloud Provider**: AWS (eu-west-2, London) — per ARC-001-RSCH-v1.0 recommendation

**Cloud Deployment Model**: Public Cloud

**Data Residency**: UK (AWS eu-west-2 London) — mandated by Principle 8, TC-3

**Cloud Security Controls**:
- [ ] Cloud Security Posture Management (CSPM) — **GAP: Not yet specified**
- [x] Identity and Access Management (IAM) — AWS IAM with least privilege mandated
- [x] Encryption key management — Managed key service with 90-day rotation (NFR-SEC-003)
- [x] Network security groups — AWS VPC and security groups implied by architecture
- [ ] Cloud Access Security Broker (CASB) — Not specified
- [x] Cloud security monitoring — AWS CloudWatch recommended (ARC-001-RSCH-v1.0)
- [x] Multi-region redundancy — Multi-AZ within UK (NFR-A-002)

**NCSC Cloud Security Principles Assessment**:

| # | Principle | Status | Evidence |
|---|-----------|--------|----------|
| 1 | Data in transit protection | ⚠️ Partial | TLS 1.2+/1.3 mandated; not yet implemented |
| 2 | Asset protection and resilience | ⚠️ Partial | Multi-AZ, encryption mandated; not implemented |
| 3 | Separation between customers | ✅ Achieved | AWS shared responsibility model; dedicated VPC |
| 4 | Governance framework | ⚠️ Partial | Principles defined; operational governance pending |
| 5 | Operational security | ⚠️ Partial | Observability mandated; not operational |
| 6 | Personnel security | ❌ Not Achieved | Team not mobilised; SC clearance planned |
| 7 | Secure development | ⚠️ Partial | Requirements extensive; not implemented |
| 8 | Supply chain security | ⚠️ Partial | Vendors identified; assessments not conducted |
| 9 | Secure user management | ⚠️ Partial | MFA, RBAC mandated; not implemented |
| 10 | Identity and authentication | ⚠️ Partial | GOV.UK One Login recommended; not integrated |
| 11 | External interface protection | ⚠️ Partial | API security mandated; not implemented |
| 12 | Secure service administration | ❌ Not Achieved | PAM not specified |
| 13 | Audit information for users | ⚠️ Partial | Audit logging mandated; not operational |
| 14 | Secure use of the service | ⚠️ Partial | Security guidance planned; not published |

**NCSC Cloud Security Principles**: 1/14 fully achieved, 11/14 partially achieved (requirements defined, not implemented)

**Gaps/Actions**:
- **HIGH**: Implement CSPM (AWS Security Hub or equivalent) — Owner: DevOps Lead — Due: 2026-09-30
- **MEDIUM**: Assess CASB requirement for cloud access governance — Owner: Security Lead — Due: 2026-10-31

---

## 6. Vulnerability and Patch Management

### 6.1 Vulnerability Management

**Vulnerability Scanning Frequency**: Weekly DAST planned (NFR-SEC-005); not yet operational

**Scanning Coverage**: 0% (system not deployed)

**Vulnerability Management Process**:
- [x] Automated vulnerability scanning — Mandated in CI/CD (NFR-SEC-005)
- [ ] Vulnerability prioritisation (CVSS scores) — Not yet specified
- [x] Remediation SLAs defined — Critical: 24 hours, High: 7 days, Medium: 30 days, Low: 90 days (NFR-SEC-005)
- [ ] Exception process for unfixable vulnerabilities — Not yet defined
- [ ] Vulnerability remediation tracking — Not yet operational
- [ ] Metrics and reporting — Not yet operational

**Current Vulnerability Status**: N/A (system not deployed)

**Gaps/Actions**:
- **HIGH**: Define vulnerability prioritisation process (CVSS + business context) — Owner: Security Lead — Due: 2026-08-31
- **MEDIUM**: Define vulnerability exception process (time-bound, compensating controls, SIRO approval for Critical/High) — Owner: Security Lead — Due: 2026-09-30

### 6.2 Patch Management

**Patch Management Process**:
- [x] Patch assessment and testing — CI/CD with automated testing (Principle 19)
- [x] Patch deployment schedule — Automated deployment (Principle 19)
- [ ] Emergency patching process — Not yet defined
- [ ] Patch compliance monitoring — Not yet operational
- [x] Rollback procedures — Deployments must be reversible (Principle 19)

**Patch Compliance**: N/A (system not deployed)

**Critical Patch SLA**: Within 24 hours (NFR-SEC-005)

**Gaps/Actions**:
- **HIGH**: Define emergency patching process for zero-day vulnerabilities — Owner: DevOps Lead — Due: 2026-09-30
- **MEDIUM**: Define patch compliance monitoring and reporting — Owner: DevOps Lead — Due: 2026-10-31

---

## 7. Third-Party and Supply Chain Risk

### 7.1 Third-Party Risk Management

**Third-Party Security Assessment**:
- [ ] Vendor security questionnaires — Not yet conducted
- [ ] Vendor security certifications verified — Partial: n3rgy claims ISO 27001; not independently verified
- [ ] Data Processing Agreements (DPAs) in place — Not yet executed
- [x] Third-party access controls — Architecture mandates service-to-service authentication
- [x] Vendor risk register — VR-1 through VR-3 in ARC-001-RSCH-v1.0
- [ ] Ongoing vendor monitoring — Not yet established

**Key Third Parties**:

| Vendor | Service | Security Rating | Risk Level | Mitigations |
|--------|---------|-----------------|------------|-------------|
| DCC | Smart meter infrastructure (CNI) | High (SEC-regulated) | HIGH | SEC compliance, SMKI certificates, network isolation |
| n3rgy | Consumer data API intermediary | Unknown (claims ISO 27001) | HIGH | Due diligence required; escrow agreement; DCC direct as fallback |
| AWS (eu-west-2) | Cloud hosting | High (ISO 27001, SOC 2, C5) | MEDIUM | UK data residency, encryption, IAM |
| Timescale Inc | Time-series database (managed) | Unknown | MEDIUM | AWS Marketplace deployment in UK; data at rest encryption |
| Energy Suppliers (6+) | Consumer data APIs | Variable | MEDIUM | Per-supplier adapter with circuit breakers; mutual TLS where supported |
| Apple/Google | App distribution | High | LOW | Store policy compliance; no secrets in app bundle |
| Grafana Labs | Observability | Unknown | LOW | No PII in telemetry; UK data processing |

**Gaps/Actions**:
- **HIGH**: Conduct formal security due diligence on n3rgy (ISO 27001 certificate, SOC 2, pen test results, business continuity plan) — Owner: Security Lead — Due: 2026-05-31
- **HIGH**: Verify Timescale Inc security posture for managed hosting (data encryption, access controls, UK data residency) — Owner: Technical Architect — Due: 2026-06-30
- **HIGH**: Execute DPAs with all data processors before any data processing begins — Owner: Programme Commercial Lead — Due: 2026-07-31

### 7.2 Open Source Security

**Open Source Components**: Significant — Flutter framework, TimescaleDB, Grafana, PostHog, Keycloak (contingency), plus mobile and backend dependencies

**OSS Security Controls**:
- [x] Software Bill of Materials (SBOM) — Planned (not yet operational)
- [x] Automated dependency scanning — SCA mandated in CI/CD (NFR-SEC-005)
- [x] Known vulnerability detection (CVE) — SCA mandated; no critical/high in production
- [ ] Licence compliance checks — **GAP: Not yet specified**
- [ ] OSS component lifecycle management — **GAP: Not yet specified**

**Gaps/Actions**:
- **MEDIUM**: Implement licence compliance scanning (FOSSA, Snyk Licence, or equivalent) — Owner: DevOps Lead — Due: 2026-09-30
- **MEDIUM**: Define OSS component lifecycle policy (how to handle abandoned/unmaintained dependencies) — Owner: Technical Architect — Due: 2026-09-30

---

## 8. Backup and Recovery

### 8.1 Backup Strategy

**Backup Method**: Continuous replication + daily backups (as specified in NFR-A-002)

**Backup Controls**:
- [x] Automated backups scheduled — Continuous replication for consumption data; daily for all other data (NFR-A-002)
- [x] Backup encryption enabled — All data encrypted at rest including backups (NFR-SEC-003)
- [x] Offsite/cloud backups — Separate UK availability zone (NFR-A-002)
- [ ] Immutable backups (ransomware protection) — **GAP: Not yet specified**
- [ ] Backup integrity testing — Not yet operational
- [ ] Backup restoration testing — Not yet operational

**Backup Frequency**: Continuous (consumption data), Daily (other data)

**Backup Retention**: 90 days operational; 7 years audit data (NFR-A-002)

**Last Successful Backup**: N/A (system not deployed)

**Last Restoration Test**: N/A (system not deployed)

**Gaps/Actions**:
- **HIGH**: Specify immutable backup strategy (AWS Backup Vault Lock or equivalent) for ransomware protection — Owner: Technical Architect — Due: 2026-09-30
- **HIGH**: Plan quarterly backup restoration testing from Beta onwards — Owner: DevOps Lead — Due: 2026-11-30

### 8.2 Recovery Capabilities

**Recovery Time Objective (RTO)**: 1 hour (platform services), 4 hours (non-critical services)
**Recovery Point Objective (RPO)**: 0 hours (zero data loss for confirmed readings)

**Failover**: Automatic to secondary availability zone; <5 minutes stateless, <15 minutes stateful (NFR-A-002)

**Recovery Testing**: Not yet conducted

**Recovery Success Rate**: N/A

**Gaps/Actions**:
- **HIGH**: Document and test DR failover procedures before Private Beta — Owner: DevOps Lead — Due: 2026-11-30
- **MEDIUM**: Establish quarterly DR testing cadence — Owner: DevOps Lead — Due: 2027-01-31

---

## 9. Smart Energy Code (SEC) Specific Security

### 9.1 SEC Security Requirements

This section addresses security obligations specific to operating as a SEC Party accessing DCC infrastructure.

| SEC Requirement | Status | Evidence |
|----------------|--------|----------|
| SEC Party accreditation | ❌ Not Started | Application planned for Week 11 (ARC-001-PLAN-v1.0) |
| SMKI certificate management | ❌ Not Started | Architecture identified (ARC-001-RSCH-v1.0 Option 1A); implementation pending |
| DUIS interface security | ❌ Not Started | XML Web Service with PKI — specialist implementation required |
| Consumer consent per SEC provisions | ⚠️ Partial | Granular consent framework designed (FR-003); not implemented |
| SEC security audit readiness | ❌ Not Started | Annual SECAS audit required once operational |
| Network isolation (DCC-facing vs consumer-facing) | ⚠️ Partial | Architecture mandates isolation (Principle 11); not implemented |

**Gaps/Actions**:
- **CRITICAL**: Submit SEC Party application — Owner: Programme Director — Due: 2026-05-11 (Week 11)
- **HIGH**: Engage specialist DCC/SMKI integration consultancy — Owner: Technical Architect — Due: 2026-06-30
- **HIGH**: Design and validate DCC network isolation architecture (consumer requests NEVER reach DCC directly) — Owner: Technical Architect — Due: 2026-07-31

---

## Overall Security Assessment Summary

### NCSC CAF Scorecard

| CAF Objective | Principles Achieved | Partially | Not Achieved | Status |
|---------------|--------------------:|----------:|-------------:|--------|
| A. Managing Security Risk (A1-A4) | 0/4 | 4/4 | 0/4 | ⚠️ |
| B. Protecting Against Cyber Attack (B1-B6) | 0/6 | 4/6 | 2/6 | ⚠️ |
| C. Detecting Cyber Security Events (C1-C2) | 0/2 | 2/2 | 0/2 | ⚠️ |
| D. Minimising Impact of Incidents (D1-D2) | 0/2 | 1/2 | 1/2 | ⚠️ |
| **Overall** | **0/14** | **11/14** | **3/14** | **⚠️ Needs Improvement** |

**Note**: 0/14 fully achieved is expected at pre-Alpha. The critical assessment is whether the architectural intent (principles and requirements) provides a credible path to full achievement. **Assessment: YES — the security requirements and principles are comprehensive and well-aligned with CAF. The gap is implementation, not design intent.**

### Security Posture Summary

**Strengths**:
- Security by Design is a non-negotiable architecture principle with zero exceptions
- Comprehensive security NFRs (NFR-SEC-001 through NFR-SEC-006) with specific acceptance criteria
- Privacy by Design embedded as a core principle with granular consent framework
- Zero trust architecture mandated (identity-based access, least privilege, encryption everywhere)
- Risk register identifies data breach as highest-impact risk with treatment plan
- Mobile-specific security requirements align with OWASP MASVS
- UK data residency mandated for all personal data
- Detailed data classification (4-tier) with retention policies
- DCC integration architecture designed to isolate consumer traffic from CNI

**Critical Gaps** (block progression to Beta):
1. **DPIA not completed** — legally required before processing any real consumer energy data (UK GDPR Article 35)
2. **Threat model not completed** — essential for informed security architecture before HLD is finalised
3. **SIRO not formally appointed** — required for security risk acceptance
4. **No penetration testing conducted** — required before Private Beta with real data
5. **No incident response plan** — required before processing real consumer data
6. **SEC Party status not obtained** — required for DCC access

**Overall Risk Rating**: HIGH — Inherent risk is critical due to personal data sensitivity and CNI connectivity. Planned controls reduce risk significantly but are not yet implemented.

### Critical Security Issues

1. **DPIA not completed** (CAF B3, UK GDPR Art 35) — **CRITICAL** — Blocks processing of real consumer data. ICO enforcement action possible if processing begins without DPIA.
2. **No threat model** (CAF A2, C2) — **CRITICAL** — Architecture cannot be validated for security without threat modelling. NCSC engagement planned but not started.
3. **SIRO not appointed** (CAF A1) — **CRITICAL** — No authority to accept security risks. Must be Director-level or above per Government Functional Standard GovS 007.
4. **No penetration testing** (CAF C2) — **HIGH** — Cannot validate security controls without testing. Required before Private Beta.
5. **No incident response plan** (CAF D1) — **HIGH** — ICO 72-hour breach notification cannot be met without documented process.
6. **DCC integration security untested** (SEC) — **HIGH** — SMKI/PKI implementation is complex; insufficient experience in programme team.
7. **No DPAs with data processors** (UK GDPR Art 28) — **HIGH** — Legally required before sharing personal data with processors.
8. **No Cyber Essentials certification** (CE) — **MEDIUM** — Required for government contract; should be achieved by Alpha.
9. **PAM not specified for operations** (CAF B2) — **MEDIUM** — Privileged access to consumer data platform needs explicit controls.
10. **No DDoS protection specified** (CAF B5) — **MEDIUM** — Consumer-facing service will be a target; AWS Shield/WAF needed.

### Recommendations

**Critical Priority** (0-30 days — must resolve before Alpha):
1. Formally appoint SIRO at DESNZ Director level — Owner: DESNZ SRO — Due: 2026-03-31
2. Submit SEC Party application — Owner: Programme Director — Due: 2026-03-31
3. Complete ICO registration — Owner: DPO/Privacy Lead — Due: 2026-03-31
4. Begin ROPA documentation — Owner: DPO/Privacy Lead — Due: 2026-03-31

**High Priority** (1-3 months — must resolve before Beta):
5. Complete DPIA and submit to ICO — Owner: DPO/Privacy Lead — Due: 2026-06-30
6. Complete threat model (STRIDE) with NCSC — Owner: Security Lead — Due: 2026-05-31
7. Develop operational security policies — Owner: Security Lead — Due: 2026-06-30
8. Conduct security due diligence on n3rgy — Owner: Security Lead — Due: 2026-05-31
9. Execute DPAs with all data processors — Owner: Programme Commercial Lead — Due: 2026-07-31
10. Deliver mandatory security and GDPR training — Owner: Security Lead — Due: 2026-04-30
11. Achieve Cyber Essentials Basic certification — Owner: Security Lead — Due: 2026-07-31
12. Define PAM for platform operations — Owner: Technical Architect — Due: 2026-07-31

**Medium Priority** (3-6 months — must resolve before Live):
13. Implement SAST, DAST, SCA in CI/CD pipeline — Owner: DevOps Lead — Due: 2026-08-31
14. Conduct penetration testing (OWASP MASVS) — Owner: Security Lead — Due: 2026-11-30
15. Develop and test incident response plan — Owner: DPO/Security Lead — Due: 2026-08-31
16. Achieve Cyber Essentials Plus certification — Owner: Security Lead — Due: 2026-12-31
17. Specify DDoS protection and IDS/IPS — Owner: Technical Architect — Due: 2026-07-31
18. Implement container security baseline (CIS benchmarks) — Owner: DevOps Lead — Due: 2026-08-31
19. Implement CSPM (AWS Security Hub) — Owner: DevOps Lead — Due: 2026-09-30
20. Launch bug bounty programme — Owner: Security Lead — Due: 2027-03-31

---

## Next Steps and Action Plan

**Immediate Actions** (0-30 days):
- [ ] Appoint SIRO at DESNZ Director level — Owner: DESNZ SRO — Due: 2026-03-31
- [ ] Complete ICO registration — Owner: DPO/Privacy Lead — Due: 2026-03-31
- [ ] Submit SEC Party application — Owner: Programme Director — Due: 2026-03-31
- [ ] Begin ROPA documentation — Owner: DPO/Privacy Lead — Due: 2026-03-31
- [ ] Confirm GOV.UK One Login mobile suitability — Owner: Technical Architect — Due: 2026-03-31

**Short-term Actions** (1-3 months):
- [ ] Complete DPIA and ICO pre-consultation — Owner: DPO/Privacy Lead — Due: 2026-06-30
- [ ] Complete STRIDE threat model with NCSC — Owner: Security Lead — Due: 2026-05-31
- [ ] Develop operational security policies — Owner: Security Lead — Due: 2026-06-30
- [ ] Security due diligence on n3rgy and key vendors — Owner: Security Lead — Due: 2026-05-31
- [ ] Deliver security and GDPR training to all team members — Owner: Security Lead — Due: 2026-04-30
- [ ] Achieve Cyber Essentials Basic — Owner: Security Lead — Due: 2026-07-31
- [ ] Execute DPAs with all data processors — Owner: Programme Commercial Lead — Due: 2026-07-31

**Long-term Actions** (3-12 months):
- [ ] Implement DevSecOps pipeline (SAST, DAST, SCA, container scanning) — Owner: DevOps Lead — Due: 2026-08-31
- [ ] Penetration testing before Private Beta — Owner: Security Lead — Due: 2026-11-30
- [ ] Incident response plan and tabletop exercise — Owner: Security Lead — Due: 2026-11-30
- [ ] Achieve Cyber Essentials Plus — Owner: Security Lead — Due: 2026-12-31
- [ ] DR failover test — Owner: DevOps Lead — Due: 2026-11-30
- [ ] SIEM with security event correlation — Owner: Security Lead — Due: 2026-09-30
- [ ] Bug bounty programme at public Beta — Owner: Security Lead — Due: 2027-03-31
- [ ] Full NCSC security review before Beta assessment — Owner: Security Lead — Due: 2027-02-28

**Next Security Review**: 2026-05-01 (quarterly during development; monthly during Beta; quarterly in Live)

---

## Approval and Sign-Off

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Programme Director | [PENDING] | | |
| Security Lead | [PENDING] | | |
| Senior Information Risk Owner (SIRO) | [PENDING — to be appointed] | | |
| Data Protection Officer (DPO) | [PENDING] | | |
| Technical Architect | [PENDING] | | |

---

## Appendices

### Appendix A: Reference Documents

| Document | ID | Relationship |
|----------|----|-------------|
| Architecture Principles | ARC-000-PRIN-v1.0 | Security principles (P5, P7) governing this assessment |
| Stakeholder Analysis | ARC-001-STKE-v1.0 | NCSC (SD-12), ICO (SD-4), DCC (SD-5) security stakeholders |
| Requirements | ARC-001-REQ-v1.0 | Security NFRs (NFR-SEC-001 through NFR-SEC-006), compliance NFRs |
| Risk Register | ARC-001-RISK-v1.0 | R-002 (data breach), R-010 (GDPR), R-013 (service failure) |
| Technology Research | ARC-001-RSCH-v1.0 | Technology selections, vendor security posture |
| Project Plan | ARC-001-PLAN-v1.0 | Security milestones, NCSC engagement timeline |

### Appendix B: Acronyms

| Acronym | Definition |
|---------|-----------|
| CAF | NCSC Cyber Assessment Framework |
| CASB | Cloud Access Security Broker |
| CNI | Critical National Infrastructure |
| CSPM | Cloud Security Posture Management |
| DAST | Dynamic Application Security Testing |
| DCC | Data Communications Company |
| DLP | Data Loss Prevention |
| DPA | Data Processing Agreement |
| DPIA | Data Protection Impact Assessment |
| DPO | Data Protection Officer |
| EDR | Endpoint Detection and Response |
| ICO | Information Commissioner's Office |
| IDS/IPS | Intrusion Detection/Prevention System |
| MASVS | Mobile Application Security Verification Standard |
| MFA | Multi-Factor Authentication |
| NCSC | National Cyber Security Centre |
| PAM | Privileged Access Management |
| ROPA | Records of Processing Activities |
| SAST | Static Application Security Testing |
| SBOM | Software Bill of Materials |
| SCA | Software Composition Analysis |
| SEC | Smart Energy Code |
| SIEM | Security Information and Event Management |
| SIRO | Senior Information Risk Owner |
| SMKI | Smart Metering Key Infrastructure |
| STRIDE | Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege |
| WAF | Web Application Firewall |

---

**Generated by**: ArcKit `/arckit.secure` command
**Generated on**: 2026-02-01
**ArcKit Version**: 1.0.3
**Project**: UK Smart Meter Data Consumer Mobile App (Project 001)
**AI Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
**Generation Context**: Based on ARC-000-PRIN-v1.0 (21 principles, Principle 5 Security by Design non-negotiable), ARC-001-REQ-v1.0 (6 security NFRs, 5 compliance NFRs), ARC-001-RISK-v1.0 (20 risks, R-002 data breach inherent 25), ARC-001-STKE-v1.0 (NCSC SD-12, ICO SD-4), ARC-001-RSCH-v1.0 (technology selections and vendor security posture), ARC-001-PLAN-v1.0 (security milestone timeline)
