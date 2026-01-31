# Enterprise Architecture Principles — UK Smart Meter Data Consumer Mobile App

> **Template Status**: Live | **Version**: 1.0.3 | **Command**: `/arckit.principles`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-000-PRIN-v1.0 |
| **Document Type** | Enterprise Architecture Principles |
| **Project** | UK Smart Meter Data Consumer Mobile App (Project 000 — Global) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-01-31 |
| **Last Modified** | 2026-01-31 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-04-30 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Architecture Review Board, Delivery Teams, DESNZ, DCC Integration Partners |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-31 | ArcKit AI | Initial creation from `/arckit.principles` command | PENDING | PENDING |

---

## Executive Summary

This document establishes the architecture principles governing all technology decisions for the UK Smart Meter Data Consumer Mobile App programme and related initiatives. These principles ensure consistency, security, scalability, and alignment with UK Government standards across all projects and system components.

**Scope**: All technology projects, systems, and initiatives within the smart meter consumer data programme
**Authority**: Enterprise Architecture Review Board
**Compliance**: Mandatory unless exception approved through the process defined in Section VII

**Philosophy**: These principles are **technology-agnostic** — they describe WHAT qualities the architecture must have, not HOW to implement them with specific products. Technology selection happens during the `/arckit.research` phase guided by these principles.

**UK Government Alignment**: These principles are designed to support compliance with the GDS Service Standard (14 points), Technology Code of Practice (13 points), NCSC Secure by Design, and the Smart Energy Code (SEC).

---

## I. Strategic Principles

### 1. User-Centred Design

**Principle Statement**:
All systems MUST be designed around the needs of end users — energy consumers — validated through user research, usability testing, and iterative delivery.

**Rationale**:
The GDS Service Standard mandates understanding user needs (Point 1) and solving a whole problem for users (Point 2). Energy consumers have diverse digital literacy levels, accessibility needs, and motivations for engaging with their smart meter data. Design decisions must be grounded in evidence from real users.

**Implications**:
- Conduct user research with energy consumers across demographics before and during design
- Design mobile interfaces for simplicity — energy data must be comprehensible without domain expertise
- Support progressive disclosure: summary views by default, detailed data on demand
- Iterate based on analytics and user feedback, not assumptions
- Design for the least digitally confident users first

**Validation Gates**:
- [ ] User research conducted with representative energy consumers
- [ ] Usability testing performed on key user journeys
- [ ] Accessibility testing with assistive technology on mobile platforms
- [ ] Analytics instrumented to measure task completion and user satisfaction
- [ ] Iterative design process documented with evidence of changes based on user feedback

---

### 2. Scalability and Elasticity

**Principle Statement**:
All systems MUST be designed to scale horizontally to meet demand, with the ability to dynamically adjust capacity based on load patterns including seasonal energy usage peaks.

**Rationale**:
The smart meter estate covers approximately 34 million households. Usage patterns will be highly variable — morning and evening peaks, seasonal heating demand, energy price cap announcements driving tariff comparison traffic, and viral adoption curves. Systems must handle both steady growth and sudden traffic spikes without degradation.

**Implications**:
- Design for stateless components that can be replicated independently
- Avoid hard-coded limits or fixed capacity assumptions
- Plan for distributed deployment across multiple availability zones
- Use load balancing to distribute traffic across instances
- Implement auto-scaling based on demand metrics and predictive patterns
- Design data pipelines to handle burst ingestion of half-hourly readings from millions of meters

**Validation Gates**:
- [ ] System can scale horizontally (add more instances) without architectural changes
- [ ] No single points of failure that limit scaling
- [ ] Load testing demonstrates linear capacity growth with added resources
- [ ] Scaling metrics and triggers defined for each component
- [ ] Cost model accounts for variable capacity and seasonal patterns

---

### 3. Resilience and Fault Tolerance

**Principle Statement**:
All systems MUST gracefully degrade when dependencies fail and recover automatically without data loss or manual intervention. Smart meter data retrieval failures MUST NOT prevent consumers from accessing previously retrieved data.

**Rationale**:
The system depends on external parties — DCC infrastructure, energy supplier APIs, and third-party services — each with their own availability characteristics. Failures in upstream systems are inevitable. The architecture must assume failures will occur and prioritise consumer access to their data above all else.

**Implications**:
- Implement circuit breakers for DCC and energy supplier API integrations
- Use timeouts on all network calls with sensible defaults
- Retry with exponential backoff for transient failures
- Cache retrieved consumption data locally so consumers can always view historical usage
- Graceful degradation when non-critical services (recommendations, tariff comparison) fail
- Automated health checks and recovery mechanisms
- Avoid cascading failures through bulkhead isolation of integration points

**Validation Gates**:
- [ ] Failure modes identified for all external dependencies (DCC, suppliers, payment systems)
- [ ] Fault injection testing performed for each integration point
- [ ] Recovery Time Objective (RTO) and Recovery Point Objective (RPO) defined per component
- [ ] Automated failover tested and documented
- [ ] Degraded mode behaviour documented — consumers can always view cached data

---

### 4. Interoperability and Open Standards

**Principle Statement**:
All systems MUST expose functionality through well-defined, versioned interfaces using industry-standard protocols. Direct database access across system boundaries is prohibited. Integration with the DCC and energy suppliers MUST use published standards and open interfaces.

**Rationale**:
The smart meter ecosystem involves multiple parties — DCC, energy suppliers, In-Home Displays, third-party service providers. The Technology Code of Practice (Point 4: Make use of open standards) and GDS Service Standard require use of open standards. Loose coupling through standard interfaces enables independent evolution and multi-supplier delivery.

**Implications**:
- Use standardised protocols for all external and internal interfaces
- Version all interfaces with backward compatibility strategy
- Publish interface specifications using open formats (OpenAPI, AsyncAPI, or equivalent)
- No direct database access across system boundaries
- Asynchronous communication for non-real-time interactions (e.g., batch meter reading ingestion)
- Conform to Smart Energy Code (SEC) technical specifications for DCC integration
- Support multiple energy supplier API formats through abstraction layers

**Validation Gates**:
- [ ] Interface specifications published in open, machine-readable formats
- [ ] Versioning strategy defined with deprecation policy
- [ ] Authentication and authorisation model documented for each interface
- [ ] Error handling and retry behaviour specified per integration
- [ ] No direct database coupling across system boundaries
- [ ] SEC compliance validated for DCC-facing interfaces

---

### 5. Security by Design (NON-NEGOTIABLE)

**Principle Statement**:
All architectures MUST implement defence-in-depth security with zero-trust principles. Security is NOT a feature to be added later — it is a foundational requirement. Energy consumption data is personal data under UK GDPR and MUST be protected accordingly.

**Rationale**:
Smart meter consumption data reveals intimate details about household behaviour — occupancy patterns, daily routines, appliance usage. This is classified as personal data under UK GDPR. The NCSC Cyber Assessment Framework and Secure by Design principles mandate that security is embedded from the outset. The Smart Energy Code (SEC) imposes specific security requirements for handling meter data.

**Zero Trust Pillars**:
1. **Identity-Based Access**: No network-based trust; every request authenticated and authorised
2. **Least Privilege**: Grant minimum necessary permissions, time-boxed where possible
3. **Encryption Everywhere**: Data encrypted in transit and at rest — no exceptions for energy consumption data
4. **Continuous Verification**: Monitor, log, and analyse all access patterns for anomalies

**Mandatory Controls**:
- [ ] Multi-factor authentication for all consumer accounts
- [ ] Service-to-service authentication (mutual authentication or equivalent)
- [ ] Secrets management via secure vault (never in code, configuration files, or mobile app bundles)
- [ ] Network segmentation with minimal trust zones
- [ ] Encryption at rest for all data stores containing personal or consumption data
- [ ] Encrypted transport for all network communication without exception
- [ ] Structured logging of all authentication/authorisation events
- [ ] Regular security testing (penetration testing, vulnerability scanning, mobile app security review)
- [ ] Consumer consent recorded and auditable before any data sharing

**Compliance Frameworks**:
- NCSC Cyber Assessment Framework / Secure by Design
- UK GDPR / Data Protection Act 2018
- Smart Energy Code (SEC) security requirements
- OWASP Mobile Application Security Verification Standard (MASVS)
- Privacy and Electronic Communications Regulations (PECR)

**Exceptions**:
- NONE. Security principles are non-negotiable.
- Specific control implementations may vary with documented compensating controls.

**Validation Gates**:
- [ ] Threat model completed and reviewed (including mobile-specific threats)
- [ ] Security controls mapped to SEC and UK GDPR requirements
- [ ] Security testing plan defined including mobile penetration testing
- [ ] Incident response runbook created with ICO notification procedures
- [ ] Data Protection Impact Assessment (DPIA) completed

---

### 6. Observability and Operational Excellence

**Principle Statement**:
All systems MUST emit structured telemetry (logs, metrics, traces) enabling real-time monitoring, troubleshooting, and capacity planning. Telemetry MUST NOT contain personal energy consumption data.

**Rationale**:
We cannot operate what we cannot observe. The GDS Service Standard (Point 14: Operate a reliable service) requires demonstrable operational capability. Instrumentation is a first-class architectural requirement, not an afterthought. However, observability data must not inadvertently expose consumer personal data.

**Telemetry Requirements**:
- **Logging**: Structured logs with correlation IDs; PII redacted or excluded
- **Metrics**: Request volume, latency percentiles (p50, p95, p99), error rates, meter data retrieval success rates
- **Tracing**: Distributed trace context for request flows across DCC and supplier integrations
- **Alerting**: Service Level Objective (SLO)-based alerting with actionable runbooks

**Required Instrumentation**:
- Request volume, latency distribution, error rate per endpoint and integration
- Resource utilisation (CPU, memory, I/O, network)
- Business metrics (meter linkage success rate, data retrieval freshness, recommendation engagement)
- Security events (authentication failures, policy violations, suspicious access patterns)
- DCC and supplier API availability and response times

**Log Retention**:
- **Security/audit logs**: 7 years (ICO and SEC requirements)
- **Application logs**: 90 days for troubleshooting
- **Metrics**: 2 years with aggregation for trend analysis

**Validation Gates**:
- [ ] Logging, metrics, tracing instrumented across all components
- [ ] Dashboards and alerts configured for each service
- [ ] SLOs and SLIs defined and monitored
- [ ] Runbooks created for common failure scenarios
- [ ] Telemetry verified to contain no PII or consumption data
- [ ] Capacity planning metrics tracked and reviewed monthly

---

## II. Data Principles

### 7. Privacy by Design and Data Minimisation

**Principle Statement**:
All systems MUST implement privacy by design, collecting and processing only the minimum personal data necessary for the stated purpose. Consumer consent MUST be explicit, granular, and revocable.

**Rationale**:
Energy consumption data is personal data under UK GDPR. Half-hourly readings can reveal occupancy patterns, daily routines, and lifestyle information. The Data Protection Act 2018, PECR, and Ofgem's data access framework require explicit consumer control over their data. Privacy must be the default, not an opt-in.

**Data Minimisation Rules**:
- Collect only the data granularity required for the specific feature
- Do not retain raw half-hourly data beyond the period required for the stated purpose
- Aggregate data as early as possible when individual readings are not needed
- Anonymise or pseudonymise data for analytics and research purposes
- Purpose limitation: data collected for one purpose MUST NOT be repurposed without fresh consent

**Consent Framework**:
- Consumers MUST explicitly consent to each data use (viewing, recommendations, tariff comparison, research sharing)
- Consent MUST be granular — consumers can allow some uses and deny others
- Consent MUST be revocable at any time with immediate effect
- Consent records MUST be auditable and time-stamped
- Withdrawal of consent MUST trigger data deletion within the defined retention period

**Validation Gates**:
- [ ] Data Protection Impact Assessment (DPIA) completed
- [ ] Lawful basis identified for each data processing activity
- [ ] Consent mechanisms implemented with granular controls
- [ ] Data retention periods defined and automated deletion configured
- [ ] Right to erasure (Article 17) process implemented and tested
- [ ] Subject Access Request (SAR) process operational within 30-day response window
- [ ] Data sharing with third parties governed by data processing agreements

---

### 8. Data Sovereignty and Residency

**Principle Statement**:
All personal data and energy consumption data MUST reside within UK data centres. Cross-border transfers MUST comply with UK GDPR adequacy requirements.

**Rationale**:
Energy consumption data for UK citizens must be processed within jurisdictions that meet UK data protection standards. The Smart Energy Code and Ofgem requirements mandate appropriate handling of consumer energy data. Hosting within UK regions ensures compliance and reduces latency for UK consumers.

**Data Classification Tiers**:
1. **Public**: App store listings, public documentation, anonymised aggregate statistics
2. **Internal**: Operational metrics, system configuration, non-personal analytics
3. **Confidential**: Consumer personal data, energy consumption data, account information
4. **Restricted**: Authentication credentials, encryption keys, DCC security certificates

**Data Residency Requirements**:
- All consumer personal data and consumption data MUST be stored in UK data centres
- Backups and disaster recovery replicas MUST remain within UK jurisdiction
- Third-party processors MUST demonstrate UK data residency compliance
- Cross-border transfers (if any) require UK GDPR-compliant safeguards

**Validation Gates**:
- [ ] All data stores mapped to UK data centre locations
- [ ] Backup and DR replicas confirmed within UK jurisdiction
- [ ] Third-party data processing agreements include residency clauses
- [ ] No inadvertent cross-border data flows (including CDN caching, logging services)

---

### 9. Data Quality and Lineage

**Principle Statement**:
Data pipelines MUST maintain data quality standards and provide end-to-end lineage from smart meter reading through to consumer-facing visualisation.

**Rationale**:
Consumers rely on the accuracy of their energy data for financial decisions — tariff switching, budget management, and identifying wasteful consumption. Inaccurate data erodes trust and could lead to incorrect financial decisions. End-to-end lineage is required for auditability and dispute resolution.

**Quality Standards**:
- **Completeness**: Missing half-hourly readings detected and flagged to consumers
- **Consistency**: Gas (kWh converted from m³) and electricity readings reconciled against supplier data
- **Accuracy**: Validation rules applied at ingestion (range checks, unit validation, meter serial number matching)
- **Timeliness**: Freshness SLAs defined — consumers should see yesterday's data by a defined time each day

**Lineage Requirements**:
- Source-to-visualisation mapping documented for all data flows
- Transformation logic (unit conversions, cost calculations, carbon estimates) version-controlled
- Data quality metrics tracked per pipeline and per energy supplier
- Impact analysis capability for schema changes in DCC or supplier data formats

**Validation Gates**:
- [ ] Data quality rules defined and automated at ingestion
- [ ] Lineage metadata captured from meter reading to consumer display
- [ ] Data quality metrics published and monitored per supplier
- [ ] Schema evolution strategy documented for DCC and supplier API changes

---

### 10. Single Source of Truth

**Principle Statement**:
Every data domain MUST have a single authoritative source. Derived copies — including on-device cached data — MUST be clearly labelled with their freshness and synchronisation status.

**Rationale**:
Multiple authoritative sources create inconsistency and erode consumer trust. Energy consumption data has a clear lineage: meter → DCC/supplier → platform → mobile device. Each stage must be unambiguous about its role.

**Implications**:
- The platform's ingestion store is the system of record for retrieved consumption data
- On-device cached data is explicitly a derived copy with visible freshness indicators
- Supplier-provided data is the upstream authority — platform data is a consumer-accessible mirror
- Avoid bidirectional synchronisation between device and platform (device is read-only for consumption data)
- Reference data (tariff rates, carbon factors) sourced from authoritative bodies

**Validation Gates**:
- [ ] System of record identified for each data entity (consumption, tariff, consumer profile, consent)
- [ ] Derived copies documented with synchronisation frequency and staleness indicators
- [ ] No bidirectional sync for consumption data
- [ ] Reference data sourced from authoritative external providers

---

## III. Integration Principles

### 11. Loose Coupling

**Principle Statement**:
Systems MUST be loosely coupled through published interfaces, avoiding shared databases, file systems, or tight runtime dependencies. The mobile app, backend platform, and external integrations (DCC, suppliers) MUST be independently deployable.

**Rationale**:
The smart meter ecosystem involves multiple independent parties with different release cycles, availability characteristics, and contractual relationships. Loose coupling enables independent evolution, multi-supplier delivery, and resilience to partner system outages.

**Implications**:
- Communicate through published APIs or asynchronous events
- No direct database access across system boundaries
- Each bounded context manages its own data lifecycle
- The mobile app MUST function offline with cached data when the backend is unavailable
- Integration adapters isolate DCC and supplier-specific protocols from core business logic
- Avoid distributed transactions across system boundaries

**Validation Gates**:
- [ ] Systems communicate via APIs or events, not shared databases
- [ ] No shared mutable state across service boundaries
- [ ] Each service has an independent data store
- [ ] Deployment of one service does not require deployment of another
- [ ] Interface changes versioned with backward compatibility guarantees
- [ ] Mobile app functions offline with graceful degradation

---

### 12. Asynchronous Communication for Data Ingestion

**Principle Statement**:
Systems SHOULD use asynchronous communication for non-real-time interactions, particularly smart meter data ingestion, batch processing, and notification delivery.

**Rationale**:
Half-hourly meter readings are inherently asynchronous — they represent historical data, not real-time streams. Asynchronous patterns reduce temporal coupling with DCC and supplier systems, improve fault tolerance, and enable better scalability for batch data processing.

**When to Use Async**:
- Smart meter reading ingestion (half-hourly data batch processing)
- Energy-saving recommendation generation
- Tariff comparison calculations
- Push notification delivery
- Anonymised data publishing for research (with consent)

**When Synchronous is Acceptable**:
- Consumer authentication and account operations
- Real-time meter data requests (if supported by supplier/DCC)
- Query operations for cached/stored data
- Consent management operations requiring immediate confirmation

**Validation Gates**:
- [ ] Async patterns used for meter data ingestion and batch processing
- [ ] Message durability and delivery guarantees defined (at-least-once for consumption data)
- [ ] Event schemas versioned and published
- [ ] Dead letter queues and error handling configured for failed ingestion
- [ ] Retry strategies defined for DCC and supplier API failures

---

## IV. Quality Attributes

### 13. Performance and Efficiency

**Principle Statement**:
All systems MUST meet defined performance targets under expected load. The mobile app MUST be responsive on mid-range devices and mobile networks typical across the UK.

**Rationale**:
Energy consumers will disengage with a slow or unresponsive app. The diverse UK device landscape (including older smartphones) and network conditions (including rural areas with limited connectivity) require performance optimisation as a core design consideration.

**Performance Targets** (indicative — refine during requirements):
- **App launch to usable**: Under 3 seconds on mid-range device over 4G
- **Dashboard load**: Under 2 seconds for cached data, under 5 seconds for fresh data retrieval
- **API response time**: p95 under 500ms for platform APIs
- **Data ingestion**: Half-hourly batch processing completed within defined SLA window
- **Offline capability**: Previously viewed data available immediately without network

**Implications**:
- Performance requirements defined before implementation
- Load testing performed at scale (millions of concurrent users modelled)
- Performance monitoring continuous in production
- Mobile app optimised for battery life, data usage, and storage footprint
- Caching strategies for expensive operations (tariff calculations, recommendation generation)

**Validation Gates**:
- [ ] Performance requirements defined with measurable targets per component
- [ ] Load testing performed at expected peak capacity
- [ ] Mobile performance tested on representative mid-range devices
- [ ] Performance metrics monitored in production with alerting
- [ ] Battery and data usage impact assessed for mobile app

---

### 14. Availability and Reliability

**Principle Statement**:
All systems MUST meet defined availability targets with automated recovery and minimal data loss. Consumers MUST be able to view their cached energy data even when backend systems are unavailable.

**Availability Targets** (indicative — refine during requirements):
- **Platform services**: 99.9% uptime (43.8 minutes downtime per month)
- **Mobile app**: Available offline for cached data viewing
- **Data ingestion**: 99.95% for scheduled batch processing windows
- **RTO**: 1 hour for platform services
- **RPO**: Zero data loss for confirmed consumption readings

**High Availability Patterns**:
- Redundancy across multiple availability zones within UK regions
- Automated health checks and failover for all stateful components
- Active-passive or active-active configurations based on criticality
- Regular disaster recovery testing (at least quarterly)
- Mobile app offline-first architecture for consumer data access

**Validation Gates**:
- [ ] Availability SLA defined per component
- [ ] RTO and RPO requirements documented and tested
- [ ] Redundancy strategy implemented across availability zones
- [ ] Failover tested regularly (quarterly minimum)
- [ ] Backup and restore procedures validated
- [ ] Offline capability tested for mobile app

---

### 15. Accessibility

**Principle Statement**:
All consumer-facing systems MUST meet WCAG 2.2 Level AA accessibility standards. The mobile app MUST be fully usable with screen readers, voice control, and other assistive technologies on both mobile platforms.

**Rationale**:
The Public Sector Bodies (Websites and Mobile Applications) Accessibility Regulations 2018 require WCAG 2.2 AA compliance. The GDS Service Standard (Point 5: Make sure everyone can use the service) mandates inclusive design. Energy data access is a utility service that must be available to all consumers regardless of ability.

**Accessibility Requirements**:
- All content perceivable by screen readers (VoiceOver, TalkBack)
- Charts and visualisations MUST have text alternatives and accessible data tables
- Colour is never the sole means of conveying information (energy usage RAG status must include labels/icons)
- Touch targets meet minimum size requirements (44x44 CSS pixels)
- Support for dynamic text sizing and high contrast modes
- Keyboard/switch navigation support on mobile platforms
- Plain English for all consumer-facing content (energy jargon avoided or explained)

**Validation Gates**:
- [ ] WCAG 2.2 AA automated audit passed
- [ ] Manual accessibility testing with assistive technology (screen reader, voice control)
- [ ] Accessibility tested with users who have access needs
- [ ] Accessibility statement published and maintained
- [ ] Energy data visualisations have accessible alternatives

---

### 16. Maintainability and Evolvability

**Principle Statement**:
All systems MUST be designed for change, with clear separation of concerns, modular architecture, and the ability to adapt as the smart meter ecosystem evolves.

**Rationale**:
The smart meter landscape is evolving — new meter types, changing regulatory requirements, new supplier APIs, evolving DCC services. The architecture must accommodate change without wholesale replacement. The Technology Code of Practice (Point 6: Make things accessible and open) supports this through modular, well-documented systems.

**Implications**:
- Modular architecture with clear bounded contexts
- Separation of concerns (mobile UI, business logic, data access, integration adapters)
- DCC and supplier integrations abstracted behind adapter interfaces (new suppliers added without core changes)
- Architecture Decision Records (ADRs) for significant choices
- Automated testing to enable confident refactoring
- Configuration-driven behaviour where requirements vary by supplier or meter type

**Validation Gates**:
- [ ] Architecture documentation exists and is current
- [ ] Module boundaries clear with defined responsibilities
- [ ] Automated test coverage enables safe refactoring
- [ ] ADRs document key architectural choices
- [ ] New energy supplier integration achievable without core platform changes

---

## V. Development Practices

### 17. Infrastructure as Code

**Principle Statement**:
All infrastructure MUST be defined as code, version-controlled, and deployed through automated pipelines. No manual changes to any environment.

**Rationale**:
Manual infrastructure changes create drift, inconsistency, and undocumented state. Infrastructure as Code enables repeatability, auditability, and disaster recovery — critical for a service handling personal data of millions of consumers.

**Implications**:
- All infrastructure defined in declarative code
- Infrastructure changes go through code review and approval
- Environments are reproducible from code (dev, staging, production identical in structure)
- No manual changes to production infrastructure — all changes via pipeline
- Infrastructure versioned alongside application code
- Secrets and configuration separated from infrastructure definitions

**Validation Gates**:
- [ ] Infrastructure defined as code in version control
- [ ] Infrastructure code reviewed before deployment
- [ ] Automated deployment pipeline for infrastructure changes
- [ ] No manual infrastructure changes in any environment
- [ ] Environment parity verified between staging and production

---

### 18. Automated Testing

**Principle Statement**:
All code changes MUST be validated through automated testing before deployment. Mobile app testing MUST include device-specific and accessibility testing.

**Test Pyramid**:
- **Unit Tests**: Fast, isolated, high coverage (70-80% of tests)
- **Integration Tests**: Test component interactions and API contracts (15-20% of tests)
- **End-to-End Tests**: Critical consumer journeys — meter linking, data viewing, tariff comparison (5-10% of tests)

**Required Test Types**:
- Functional tests (does it work?)
- Performance tests (is it fast enough on target devices?)
- Security tests (is it secure? OWASP MASVS for mobile)
- Accessibility tests (is it usable by all consumers?)
- Resilience tests (does it handle DCC/supplier failures gracefully?)

**Validation Gates**:
- [ ] Automated tests exist and pass before merge
- [ ] Test coverage meets defined thresholds per component
- [ ] Critical consumer journeys have end-to-end tests
- [ ] Mobile tests run on representative device matrix
- [ ] Security and accessibility tests included in pipeline

---

### 19. Continuous Integration and Deployment

**Principle Statement**:
All code changes MUST go through automated build, test, and deployment pipelines with quality gates at each stage. Deployments MUST be repeatable and reversible.

**Pipeline Stages**:
1. **Source Control**: All changes committed to version control with peer review
2. **Build**: Automated compilation and packaging (including mobile app builds)
3. **Test**: Automated test execution across the test pyramid
4. **Security Scan**: Dependency vulnerability scanning, static analysis, secrets detection
5. **Accessibility Check**: Automated WCAG audit as pipeline gate
6. **Deployment**: Automated deployment to environments with approval gates for production

**Quality Gates**:
- All tests must pass
- No critical or high security vulnerabilities
- Code review approval required
- Accessibility checks pass
- Deployment requires production readiness checklist sign-off

**Validation Gates**:
- [ ] Automated CI/CD pipeline exists for all components
- [ ] Pipeline includes security scanning and accessibility checks
- [ ] Deployment is automated and repeatable
- [ ] Rollback capability tested and documented
- [ ] Mobile app release pipeline includes store submission automation

---

## VI. UK Government Principles

### 20. GDS Service Standard Alignment

**Principle Statement**:
The service MUST be designed and operated in accordance with the GDS Service Standard (14 points) and pass service assessment at each phase (Discovery, Alpha, Beta, Live).

**Rationale**:
If delivered as a government service or on behalf of government, compliance with the Service Standard is mandatory. Even if delivered by the private sector, the Standard provides a proven framework for building user-centred, accessible, reliable digital services.

**Key Alignment Areas**:
- Points 1-3: User needs, whole problem, joined-up experience
- Point 5: Accessibility and inclusion
- Point 6: Multidisciplinary team
- Point 8: Iterate and improve frequently
- Point 9: Create a secure service
- Point 11: Choose the right tools and technology
- Point 12: Make new source code open
- Point 13: Use and contribute to open standards
- Point 14: Operate a reliable service

**Validation Gates**:
- [ ] Service assessment preparation documented per phase
- [ ] Evidence collected against all 14 points
- [ ] Assessor feedback addressed from previous phases
- [ ] Public-facing service meets government branding and content standards (if applicable)

---

### 21. Open Source and Reuse

**Principle Statement**:
Source code SHOULD be made open unless there are clear security reasons not to. The service MUST reuse existing government components, patterns, and platforms where appropriate.

**Rationale**:
The Technology Code of Practice (Point 3: Be open and use open source, Point 12: Make new source code open) and GDS Service Standard (Point 12) require openness by default. Reusing government platforms (GOV.UK Notify, GOV.UK Pay, if applicable) reduces cost and improves consistency.

**Implications**:
- Default to open source for application code
- Security-sensitive components (authentication, encryption key management) may be exceptions
- Evaluate government shared platforms before building bespoke
- Contribute improvements back to shared components
- Document reuse decisions in Architecture Decision Records

**Validation Gates**:
- [ ] Source code published in the open (or exception documented)
- [ ] Government shared platforms evaluated and used where appropriate
- [ ] Open source dependencies assessed for security and maintenance health
- [ ] Licensing compliance verified for all dependencies

---

## VII. Exception Process

### Requesting Architecture Exceptions

Principles are mandatory unless a documented exception is approved by the Architecture Review Board.

**Valid Exception Reasons**:
- Technical constraints that prevent compliance (e.g., DCC protocol limitations)
- Regulatory or legal requirements that conflict with a principle
- Transitional state during migration with a defined remediation timeline
- Pilot or proof-of-concept with a defined end date and evaluation criteria

**Exception Request Requirements**:
- [ ] Justification with business and technical rationale
- [ ] Alternative approach and compensating controls documented
- [ ] Risk assessment and mitigation plan (cross-reference ARC-001-RISK)
- [ ] Expiration date — all exceptions are time-bound
- [ ] Remediation plan to achieve full compliance

**Approval Process**:
1. Submit exception request to the Architecture Review Board
2. Review by architecture team with security and data protection input
3. Senior Responsible Owner (SRO) approval for exceptions to critical principles
4. Document exception in project architecture documentation
5. Regular review of exceptions (quarterly, aligned with principle review cycle)

---

## VIII. Governance and Compliance

### Architecture Review Gates

All projects and significant changes must pass architecture reviews at key milestones:

**Discovery/Alpha**:
- [ ] Architecture principles understood by the team
- [ ] High-level approach aligns with principles
- [ ] No obvious principle violations identified
- [ ] User research underway to validate design assumptions

**Beta/Design**:
- [ ] Detailed architecture documented (HLD/DLD)
- [ ] Compliance with each principle validated and evidenced
- [ ] Exceptions requested and approved through formal process
- [ ] Security, data protection, and accessibility principles validated
- [ ] DPIA completed and reviewed

**Pre-Production/Live**:
- [ ] Implementation matches approved architecture
- [ ] All validation gates passed across all principles
- [ ] Operational readiness verified (monitoring, alerting, runbooks)
- [ ] GDS Service Standard assessment passed for current phase
- [ ] Penetration testing completed with no critical findings

### Enforcement

- Architecture reviews are **mandatory** for all projects and significant changes
- Principle violations must be remediated before production deployment
- Approved exceptions are time-bound and reviewed quarterly
- Retrospective compliance reviews conducted on live systems annually

---

## IX. Appendix

### Principle Summary Checklist

| # | Principle | Category | Criticality | Key Validation |
|---|-----------|----------|-------------|----------------|
| 1 | User-Centred Design | Strategic | HIGH | User research, usability testing |
| 2 | Scalability and Elasticity | Strategic | HIGH | Load testing, scaling metrics |
| 3 | Resilience and Fault Tolerance | Strategic | CRITICAL | Fault injection, RTO/RPO |
| 4 | Interoperability and Open Standards | Strategic | HIGH | API specs, SEC compliance |
| 5 | Security by Design | Strategic | CRITICAL | Threat model, pen testing, DPIA |
| 6 | Observability | Strategic | HIGH | Metrics, logs, traces (no PII) |
| 7 | Privacy by Design | Data | CRITICAL | DPIA, consent, data minimisation |
| 8 | Data Sovereignty | Data | CRITICAL | UK residency, compliance audit |
| 9 | Data Quality and Lineage | Data | HIGH | Quality metrics, lineage tracking |
| 10 | Single Source of Truth | Data | HIGH | System of record mapping |
| 11 | Loose Coupling | Integration | HIGH | Deployment independence |
| 12 | Asynchronous Communication | Integration | MEDIUM | Async patterns for ingestion |
| 13 | Performance and Efficiency | Quality | HIGH | Load testing, device testing |
| 14 | Availability and Reliability | Quality | CRITICAL | SLA monitoring, offline mode |
| 15 | Accessibility | Quality | CRITICAL | WCAG 2.2 AA, assistive tech |
| 16 | Maintainability and Evolvability | Quality | MEDIUM | Documentation, ADRs, tests |
| 17 | Infrastructure as Code | DevOps | HIGH | IaC coverage, no manual changes |
| 18 | Automated Testing | DevOps | HIGH | Test coverage, device matrix |
| 19 | CI/CD | DevOps | HIGH | Pipeline with security gates |
| 20 | GDS Service Standard | UK Gov | HIGH | 14-point assessment evidence |
| 21 | Open Source and Reuse | UK Gov | MEDIUM | Code published, platforms reused |

### Linked Artifacts

| Artifact | Document ID | Relationship |
|----------|------------|--------------|
| Stakeholder Analysis | ARC-001-STKE-v1.0 | Stakeholder drivers inform principle prioritisation |
| Requirements | ARC-001-REQ-v1.0 | Requirements must trace to governing principles |
| Risk Register | ARC-001-RISK-v1.0 | Risks mitigated by principle compliance |
| DPIA | ARC-001-DPIA-v1.0 | Privacy principles validated through DPIA |
| Architecture Decisions | ARC-001-ADR-*-v1.0 | ADRs reference principles as decision criteria |

---

**Generated by**: ArcKit `/arckit.principles` command
**Generated on**: 2026-01-31
**ArcKit Version**: 1.0.3
**Project**: UK Smart Meter Data Consumer Mobile App (Project 000 — Global)
**AI Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
