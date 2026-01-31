# Stakeholder Drivers & Goals Analysis: UK Smart Meter Data Consumer Mobile App

> **Template Status**: Live | **Version**: 1.0.3 | **Command**: `/arckit.stakeholders`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-STKE-v1.0 |
| **Document Type** | Stakeholder Drivers & Goals Analysis |
| **Project** | UK Smart Meter Data Consumer Mobile App (Project 001) |
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
| **Distribution** | Programme Board, DESNZ Smart Metering Team, DCC, Ofgem, GDS Assessors |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-31 | ArcKit AI | Initial creation from `/arckit.stakeholders` command | PENDING | PENDING |

---

## Executive Summary

### Purpose
This document identifies stakeholders in the UK Smart Meter Data Consumer Mobile App programme, their underlying drivers, how these drivers manifest into goals, and the measurable outcomes that will satisfy those goals. It provides end-to-end traceability from stakeholder motivations to project success metrics.

### Key Findings
The programme sits at the intersection of energy policy, consumer empowerment, and data protection — creating a complex stakeholder landscape with strong alignment on the goal of consumer empowerment but significant tensions around pace of delivery versus regulatory rigour. DESNZ and Smart Energy GB are pushing for rapid consumer adoption to justify the £13.5 billion smart meter programme investment, while Ofgem and the ICO require robust data protection and consumer safeguards. Energy suppliers are ambivalent — supportive of consumer engagement but wary of tariff comparison features that could accelerate switching. The DCC is a critical but constrained enabler, with integration complexity and capacity limitations shaping the art of the possible.

### Critical Success Factors
- Consumer trust in the security and accuracy of their energy data
- Seamless integration with DCC infrastructure and energy supplier APIs without degrading existing smart metering services
- Demonstrable compliance with UK GDPR, SEC, and Ofgem data access framework before any consumer data is processed
- App usability that serves digitally excluded and low-confidence consumers, not just tech-savvy early adopters
- Sustainable operating model that does not depend on ongoing government subsidy

### Stakeholder Alignment Score
**Overall Alignment**: MEDIUM

Strong consensus exists around consumer empowerment and Net Zero contribution, but material conflicts remain around delivery pace (DESNZ vs regulators), data access scope (suppliers vs consumers), and commercial model sustainability (Treasury vs delivery teams). These require active management through the governance structures defined in this document.

---

## Stakeholder Identification

### Internal Stakeholders (Government / Programme)

| Stakeholder | Role/Department | Influence | Interest | Engagement Strategy |
|-------------|----------------|-----------|----------|---------------------|
| DESNZ Minister for Energy | Ministerial accountability | HIGH | HIGH | Quarterly briefings, PQ responses |
| DESNZ Smart Metering Programme Director | Senior Responsible Owner (SRO) | HIGH | HIGH | Weekly programme board |
| DESNZ Digital Team | Technical delivery oversight | MEDIUM | HIGH | Sprint reviews, architecture reviews |
| HM Treasury Spending Team | Budget and spending controls | HIGH | MEDIUM | Business case gates, spend approvals |
| CDDO (Central Digital & Data Office) | Technology standards | MEDIUM | MEDIUM | TCoP assessment, spend control |
| GDS Assessors | Service Standard assessment | MEDIUM | HIGH | Phase assessments (Alpha, Beta, Live) |
| Programme Delivery Team | Build and operate the service | LOW | HIGH | Daily standups, retrospectives |

### External Stakeholders

| Stakeholder | Organisation | Relationship | Influence | Interest |
|-------------|--------------|--------------|-----------|----------|
| Ofgem | Energy regulator | Regulatory oversight | HIGH | HIGH |
| ICO | Data protection regulator | Regulatory oversight | HIGH | MEDIUM |
| DCC | Smart meter infrastructure | Critical supplier/partner | HIGH | HIGH |
| Energy Suppliers (Big Six + challengers) | Data providers | Partners / regulated parties | HIGH | HIGH |
| Citizens / Energy Consumers | End users | Beneficiaries | LOW | HIGH |
| Smart Energy GB | Consumer engagement body | Advocacy partner | LOW | HIGH |
| Consumer organisations (Citizens Advice, Which?) | Consumer advocacy | Influencers | MEDIUM | HIGH |
| NCSC | Cyber security authority | Advisory | MEDIUM | MEDIUM |
| App store operators (Apple, Google) | Distribution platforms | Gatekeepers | MEDIUM | LOW |
| Energy research bodies (UCL, UKERC) | Academic research | Data consumers | LOW | MEDIUM |

### Stakeholder Power-Interest Grid

```
                          INTEREST
              Low                         High
        ┌─────────────────────┬─────────────────────┐
        │                     │                     │
        │   KEEP SATISFIED    │   MANAGE CLOSELY    │
   High │                     │                     │
        │  • HM Treasury      │  • DESNZ Minister   │
        │  • CDDO             │  • DESNZ SRO        │
        │  • NCSC             │  • Ofgem            │
 P      │                     │  • DCC              │
 O      │                     │  • Energy Suppliers  │
 W      ├─────────────────────┼─────────────────────┤
 E      │                     │                     │
 R      │      MONITOR        │    KEEP INFORMED    │
        │                     │                     │
   Low  │  • App Stores       │  • Citizens         │
        │  • Research Bodies  │  • Smart Energy GB  │
        │                     │  • Consumer Orgs    │
        │                     │  • GDS Assessors    │
        │                     │  • Delivery Team    │
        └─────────────────────┴─────────────────────┘
```

| Stakeholder | Power | Interest | Quadrant | Engagement Strategy |
|-------------|-------|----------|----------|---------------------|
| DESNZ Minister | HIGH | HIGH | Manage Closely | Monthly ministerial briefing, PQ-ready metrics dashboard |
| DESNZ SRO | HIGH | HIGH | Manage Closely | Weekly programme board, escalation authority |
| Ofgem | HIGH | HIGH | Manage Closely | Quarterly regulatory engagement, data access framework alignment |
| DCC | HIGH | HIGH | Manage Closely | Fortnightly technical integration sessions, capacity planning |
| Energy Suppliers | HIGH | HIGH | Manage Closely | Supplier forum (monthly), API onboarding programme |
| ICO | HIGH | MEDIUM | Keep Satisfied | DPIA review engagement, pre-consultation on data processing |
| HM Treasury | HIGH | MEDIUM | Keep Satisfied | Business case gates, spend control submissions |
| CDDO | MEDIUM | MEDIUM | Keep Satisfied | TCoP assessment, spend control alignment |
| NCSC | MEDIUM | MEDIUM | Keep Satisfied | Threat assessment input, Secure by Design review |
| Consumer Orgs | MEDIUM | HIGH | Keep Informed | User research partnership, public consultation |
| Citizens | LOW | HIGH | Keep Informed | User research panels, beta testing, feedback channels |
| Smart Energy GB | LOW | HIGH | Keep Informed | Consumer messaging alignment, promotion partnership |
| GDS Assessors | MEDIUM | HIGH | Keep Informed | Phase assessments, evidence portfolio preparation |
| Delivery Team | LOW | HIGH | Keep Informed | Sprint ceremonies, architecture decisions |
| App Stores | MEDIUM | LOW | Monitor | Store guideline compliance, review process |
| Research Bodies | LOW | MEDIUM | Monitor | Data sharing framework (with consent), publications |

---

## Stakeholder Drivers Analysis

### SD-1: DESNZ Minister — Demonstrate Return on Smart Meter Investment

**Stakeholder**: Minister for Energy, Department for Energy Security & Net Zero

**Driver Category**: STRATEGIC / POLITICAL

**Driver Statement**: Demonstrate tangible consumer benefits from the £13.5 billion Smart Metering Implementation Programme (SMIP) to justify the investment to Parliament, public, and media. The smart meter rollout has faced criticism for cost overruns and consumer scepticism — a successful consumer app would provide a visible, positive narrative.

**Context & Background**:
The SMIP has been scrutinised by the NAO and PAC. Parliamentary questions about smart meter benefits are frequent. The Minister needs concrete evidence that smart meters are delivering for consumers, not just for energy suppliers and networks. The app is a potential flagship deliverable that converts infrastructure investment into consumer-facing outcomes.

**Driver Intensity**: CRITICAL

**Enablers**:
- High consumer adoption rates creating a visible success story
- Clear metrics showing energy savings and consumer satisfaction
- Positive media coverage and consumer testimonials

**Blockers**:
- Data breach or security incident destroying public trust
- Low adoption rates or poor user reviews
- NAO criticism of the app's cost-effectiveness
- Opposition parties framing the app as a waste of public money

**Related Stakeholders**: HM Treasury (value for money), Smart Energy GB (consumer messaging), Consumer Orgs (public perception)

---

### SD-2: DESNZ SRO — Deliver Against Spending Review Commitments

**Stakeholder**: Smart Metering Programme Director (SRO), DESNZ

**Driver Category**: OPERATIONAL / RISK

**Driver Statement**: Deliver the consumer mobile app on time, within budget, and to the quality standards required by the GDS Service Standard — while managing programme risks including DCC integration complexity, supplier cooperation, and cross-government dependencies.

**Context & Background**:
The SRO is personally accountable to the Permanent Secretary and Minister for programme delivery. They face pressure to move quickly (ministerial ambition) while ensuring governance is robust (NAO/PAC scrutiny). They need to balance delivery velocity with risk management — a failed launch would be career-defining in the wrong direction.

**Driver Intensity**: CRITICAL

**Enablers**:
- Experienced multidisciplinary delivery team
- Clear requirements and stable scope
- Supportive DCC and supplier ecosystem
- Adequate budget secured through Spending Review

**Blockers**:
- Scope creep driven by ministerial enthusiasm
- DCC integration delays or capacity constraints
- Energy supplier non-cooperation or slow API development
- Cross-government spend control delays

**Related Stakeholders**: DESNZ Minister (pace pressure), HM Treasury (budget), DCC (integration), GDS (assessment gates)

---

### SD-3: Ofgem — Protect Consumer Interests and Data Rights

**Stakeholder**: Ofgem (Office of Gas and Electricity Markets)

**Driver Category**: COMPLIANCE / CUSTOMER

**Driver Statement**: Ensure the app operates within the regulatory framework for consumer energy data access, protects consumers from exploitation, and supports fair competition in the energy market. The app must not create unfair advantages for any supplier or disadvantage vulnerable consumers.

**Context & Background**:
Ofgem's mandate is consumer protection in the energy market. They have developed the data access framework for smart meter data, defining how consumers can share their data with third parties. They are concerned about: (1) consumer consent being truly informed and freely given, (2) tariff comparison features being impartial and accurate, (3) vulnerable consumers not being digitally excluded, (4) data not being used for predatory marketing or discriminatory pricing.

**Driver Intensity**: HIGH

**Enablers**:
- Clear alignment with Ofgem's data access and consent framework
- Robust consumer protection measures built into the app
- Transparent tariff comparison methodology
- Vulnerability strategy addressing digital exclusion

**Blockers**:
- App design that favours certain suppliers over others
- Consent mechanisms that are confusing or manipulative ("dark patterns")
- Tariff comparison that doesn't account for all consumer circumstances
- Insufficient accessibility for vulnerable consumers

**Related Stakeholders**: Energy Suppliers (competition concerns), Citizens (consumer protection), Consumer Orgs (advocacy), ICO (data protection)

---

### SD-4: ICO — Ensure Lawful Processing of Personal Energy Data

**Stakeholder**: Information Commissioner's Office

**Driver Category**: COMPLIANCE

**Driver Statement**: Ensure energy consumption data — which reveals intimate details of household behaviour — is processed lawfully, fairly, and transparently under UK GDPR. The ICO expects privacy by design, granular consent, and robust data subject rights.

**Context & Background**:
The ICO has published guidance on smart meter data as personal data. Half-hourly consumption data can reveal occupancy patterns, daily routines, sleep patterns, and appliance usage. The ICO expects a DPIA before processing begins, privacy by design embedded in architecture, and consumer control over their data. A failure in data protection could result in enforcement action and undermine public trust in the wider smart metering programme.

**Driver Intensity**: HIGH

**Enablers**:
- Early DPIA engagement before system design is finalised
- Privacy by design embedded in architecture (ARC-000-PRIN Principle 7)
- Granular consent mechanisms exceeding minimum requirements
- Transparent privacy notices in plain English

**Blockers**:
- "Consent fatigue" — consumers clicking through without understanding
- Scope creep adding data processing activities not covered by original consent
- Third-party data sharing without adequate processing agreements
- Cross-border data flows (even inadvertent, e.g., CDN or analytics)

**Related Stakeholders**: Ofgem (data access framework), Citizens (data subjects), NCSC (data security)

---

### SD-5: DCC — Maintain Infrastructure Stability While Enabling Innovation

**Stakeholder**: Data Communications Company

**Driver Category**: OPERATIONAL / RISK

**Driver Statement**: Support the consumer app's data access requirements without compromising the stability, security, or capacity of the smart metering communications infrastructure that serves the entire energy industry. DCC must balance innovation enablement with its core obligation to maintain critical national infrastructure.

**Context & Background**:
DCC operates the communications infrastructure connecting 34 million smart meters to energy suppliers and authorised parties. Adding a consumer-facing app introduces a new access pattern — potentially millions of individual data requests rather than bulk supplier-initiated reads. DCC is concerned about: (1) capacity impact on the existing WAN, (2) security implications of a consumer-facing interface, (3) support burden from a mass-market application, (4) commercial model for the additional data access.

**Driver Intensity**: HIGH

**Enablers**:
- Well-defined API integration layer that minimises DCC system changes
- Batch retrieval patterns that align with existing DCC data flows
- Consumer app caching that reduces real-time demands on DCC
- Clear commercial model for data access costs

**Blockers**:
- Consumer app generating excessive real-time data requests
- Security vulnerability in app creating an attack vector for DCC systems
- Unclear commercial responsibility for DCC costs
- Consumer expectations exceeding what DCC can technically deliver (e.g., sub-minute data)

**Related Stakeholders**: Energy Suppliers (shared infrastructure), DESNZ SRO (delivery dependency), NCSC (security)

---

### SD-6: Energy Suppliers — Manage Customer Relationship and Competitive Position

**Stakeholder**: Energy Suppliers (British Gas/Centrica, EDF, E.ON, SSE, Scottish Power, Octopus Energy, Bulb, OVO, and others)

**Driver Category**: STRATEGIC / RISK

**Driver Statement**: Maintain control of the customer relationship while meeting regulatory obligations to share consumer data. Suppliers are ambivalent — they support consumer engagement with energy data (aligned with their own apps) but are wary of a government-backed app that could accelerate switching, commoditise their customer relationship, and expose unfavourable tariff comparisons.

**Context & Background**:
Most large suppliers have their own consumer apps. A government-backed app with trusted branding and impartial tariff comparison could divert consumers from supplier apps, increasing switching rates and reducing supplier ability to cross-sell. Challenger suppliers (Octopus, OVO) may be more enthusiastic as the app could help them acquire customers from incumbents. Suppliers are legally required to support data access under Ofgem licence conditions but may be slow to develop high-quality APIs.

**Driver Intensity**: HIGH

**Enablers**:
- App positioned as complementary to (not replacement for) supplier apps
- Standardised API specification reducing integration burden per supplier
- Consumer data access rights clearly mandated by Ofgem
- Supplier branding preserved within the app where relevant

**Blockers**:
- App perceived as competing with supplier apps for consumer engagement
- Tariff comparison feature that disproportionately drives switching from specific suppliers
- API development burden falling on suppliers without adequate support
- Data quality issues in supplier systems exposed by the app

**Related Stakeholders**: Ofgem (regulatory mandate), Citizens (data access rights), DESNZ (stakeholder management)

---

### SD-7: Citizens / Energy Consumers — Understand and Reduce Energy Costs

**Stakeholder**: 34 million smart meter households across Great Britain

**Driver Category**: CUSTOMER / FINANCIAL

**Driver Statement**: Understand where energy is being used, identify waste, and take practical steps to reduce bills — particularly in the context of energy cost-of-living pressures. Consumers want simple, trustworthy information that helps them save money, not another app to manage.

**Context & Background**:
Energy bills have been a top consumer concern since the 2022 energy crisis. Many consumers have smart meters but don't engage with the In-Home Display (IHD). Consumers want: (1) to understand their bill in plain terms, (2) to know if they're on the best tariff, (3) actionable tips to reduce usage, (4) confidence their data is safe. The key barrier is apathy — most consumers won't download a new app unless the value proposition is immediately clear and the experience is effortless.

**Driver Intensity**: HIGH

**Enablers**:
- Simple, intuitive interface requiring no energy expertise
- Immediate value (e.g., "you could save £X by switching tariff")
- Trusted branding (government or independent, not commercially compromised)
- Minimal effort to set up (easy meter linking, few steps to value)

**Blockers**:
- Complex onboarding requiring energy account details consumers don't have to hand
- Data that's hard to interpret or doesn't lead to actionable steps
- Privacy concerns about sharing energy data
- App store ratings below 4 stars (consumer perception of quality)
- Poor performance on older devices or slow networks

**Related Stakeholders**: Smart Energy GB (awareness), Ofgem (consumer protection), Energy Suppliers (data provision)

---

### SD-8: Smart Energy GB — Increase Consumer Engagement with Smart Metering

**Stakeholder**: Smart Energy GB (industry-funded consumer engagement body)

**Driver Category**: STRATEGIC / CUSTOMER

**Driver Statement**: Drive consumer engagement with smart metering to fulfil its organisational mandate and justify continued industry funding. The app represents a significant new channel for consumer engagement beyond the IHD and smart meter awareness campaigns.

**Context & Background**:
Smart Energy GB runs national campaigns to promote smart meter adoption and usage. Despite 34 million meters installed, many consumers don't actively engage with their smart metering data. The app could be a powerful tool in Smart Energy GB's arsenal — but only if it delivers a good consumer experience. Poor execution would undermine their messaging.

**Driver Intensity**: MEDIUM

**Enablers**:
- App integrated into Smart Energy GB's marketing campaigns
- Co-branded content and energy-saving advice
- Consumer research shared between Smart Energy GB and the programme

**Blockers**:
- App quality issues that Smart Energy GB would have to defend publicly
- Misalignment between app messaging and Smart Energy GB campaigns
- Cannibalisation of Smart Energy GB's own digital channels

**Related Stakeholders**: DESNZ (policy alignment), Citizens (consumer reach), Energy Suppliers (funding Smart Energy GB)

---

### SD-9: HM Treasury — Demonstrate Value for Money

**Stakeholder**: HM Treasury Spending Team (DESNZ allocation)

**Driver Category**: FINANCIAL

**Driver Statement**: Ensure the app delivers measurable benefits proportionate to its cost, with a sustainable operating model that does not create an open-ended government subsidy. Treasury expects a clear business case with quantified benefits, cost controls, and a path to commercial sustainability or justified ongoing cost.

**Context & Background**:
Treasury applies the Green Book five-case model to assess spending proposals. They will scrutinise: (1) strategic fit — why government intervention is needed, (2) economic case — benefit-cost ratio including non-monetised benefits, (3) commercial case — procurement approach, (4) financial case — affordability within departmental budgets, (5) management case — deliverability. Treasury is sceptical of government app development given mixed track record.

**Driver Intensity**: HIGH

**Enablers**:
- Strong SOBC demonstrating market failure justifying intervention
- Quantified benefits (energy savings per consumer × adoption rate)
- Clear comparisons with commercial alternatives (why government must act)
- Agile delivery with early benefit realisation

**Blockers**:
- Inability to quantify benefits in monetary terms
- High delivery costs relative to similar apps in the market
- No credible path to sustainability (perpetual subsidy)
- Competing spending priorities within DESNZ

**Related Stakeholders**: DESNZ SRO (business case preparation), CDDO (spend control), NAO (value for money audit)

---

### SD-10: Consumer Organisations — Ensure Inclusive and Fair Service

**Stakeholder**: Citizens Advice, Which?, Age UK, disability organisations

**Driver Category**: CUSTOMER / COMPLIANCE

**Driver Statement**: Ensure the app serves all consumers — including those who are digitally excluded, have disabilities, are on prepayment meters, or are in vulnerable circumstances. Consumer organisations will publicly challenge any service that widens the digital divide or disadvantages vulnerable groups.

**Context & Background**:
Consumer organisations have been vocal about smart metering excluding digitally disengaged consumers. They will scrutinise the app's accessibility, its treatment of prepayment meter customers (often the most financially vulnerable), and whether it genuinely helps consumers in fuel poverty. They have platforms to influence public opinion and political discourse.

**Driver Intensity**: HIGH

**Enablers**:
- Co-design with consumers who have access needs
- Prepayment meter features (balance alerts, top-up reminders)
- Assisted digital support channel for consumers who can't use the app independently
- Clear vulnerability strategy aligned with Ofgem's Consumer Vulnerability Strategy

**Blockers**:
- App design that only works well for tech-savvy consumers
- Prepayment features deprioritised or descoped
- No assisted digital provision
- Accessibility failures in energy data visualisations

**Related Stakeholders**: Ofgem (vulnerable consumer obligations), Citizens (end users), GDS (inclusive design)

---

### SD-11: GDS Assessors — Ensure Compliance with the Service Standard

**Stakeholder**: Government Digital Service assessment team

**Driver Category**: COMPLIANCE

**Driver Statement**: Assess the service against the 14 points of the GDS Service Standard at each phase gate (Alpha, Beta, Live). GDS expects evidence of user research, accessible design, open source, reliable operation, and continuous improvement.

**Context & Background**:
GDS assessments are mandatory for government digital services. Assessors look for evidence, not just claims — actual user research sessions, real accessibility testing results, working prototypes tested with real users, and operational metrics from live systems. A "not met" assessment would delay the programme and create political embarrassment.

**Driver Intensity**: MEDIUM

**Enablers**:
- Multidisciplinary team with user researchers, designers, and developers
- Continuous user research throughout all phases
- Evidence portfolio maintained from day one
- Open source code and open standards

**Blockers**:
- Waterfall delivery disguised as agile
- User research conducted too late or with unrepresentative participants
- Accessibility treated as an afterthought
- No operational metrics or SLOs defined

**Related Stakeholders**: DESNZ Digital Team (evidence preparation), CDDO (standards oversight)

---

### SD-12: NCSC — Ensure Cyber Security of Consumer-Facing Infrastructure

**Stakeholder**: National Cyber Security Centre

**Driver Category**: RISK / COMPLIANCE

**Driver Statement**: Ensure the consumer app and its backend infrastructure do not introduce cyber security vulnerabilities into the smart metering ecosystem. The smart metering network is critical national infrastructure — a consumer-facing app creates a new attack surface that must be managed.

**Context & Background**:
NCSC provides cyber security guidance to government and critical infrastructure operators. They are concerned that a consumer mobile app connected (directly or indirectly) to DCC infrastructure creates an attack vector. Their involvement ensures the architecture meets Secure by Design principles and the Cyber Assessment Framework.

**Driver Intensity**: MEDIUM

**Enablers**:
- Early engagement in threat modelling
- Architecture following NCSC cloud security principles
- Regular penetration testing and vulnerability management
- Security isolation between consumer-facing and DCC-facing components

**Blockers**:
- Tight delivery timescales compressing security review time
- Mobile app security challenges (reverse engineering, device compromise)
- Third-party component vulnerabilities

**Related Stakeholders**: DCC (infrastructure security), ICO (data security), DESNZ SRO (security governance)

---

## Driver-to-Goal Mapping

### Goal G-1: Achieve 5 Million Active Users Within 18 Months of Launch

**Derived From Drivers**: SD-1 (ministerial visibility), SD-7 (consumer value), SD-8 (engagement), SD-9 (value for money)

**Goal Owner**: DESNZ SRO

**Goal Statement**: Achieve 5 million monthly active users (15% of smart meter households) within 18 months of public launch, with a 30-day retention rate above 40%.

**Why This Matters**: Adoption is the single biggest determinant of programme success. Without users, there are no benefits, no ministerial success story, no value for money, and no justification for the investment. The 5 million target represents the threshold at which the app becomes a meaningful national service rather than a niche product.

**Success Metrics**:
- **Primary Metric**: Monthly Active Users (MAU)
- **Secondary Metrics**:
  - App store downloads
  - Meter linkage completion rate (% of downloads that successfully link a meter)
  - 30-day retention rate
  - App store rating (target: 4.2+)

**Baseline**: 0 (new service)

**Target**: 5 million MAU by Month 18

**Measurement Method**: Mobile analytics platform (privacy-preserving, no PII in analytics)

**Dependencies**:
- Energy suppliers deliver functional APIs for meter data access
- DCC supports the data retrieval volume
- Smart Energy GB promotes the app through existing channels
- App store approval process completed without delays

**Risks to Achievement**:
- Low consumer awareness despite marketing investment
- Complex onboarding process causing drop-off before meter linking
- Poor app store reviews from early users deterring later adopters
- Energy supplier API quality issues causing inconsistent consumer experience

---

### Goal G-2: Enable Measurable Consumer Energy Savings

**Derived From Drivers**: SD-1 (investment return), SD-7 (consumer value), SD-3 (consumer protection), SD-9 (value for money)

**Goal Owner**: DESNZ Smart Metering Programme Director

**Goal Statement**: Active app users reduce their energy consumption by an average of 5% compared to their pre-app baseline within 6 months of first use, measured through smart meter data (with consent).

**Why This Matters**: Energy savings are the core benefit proposition — for consumers (lower bills), for government (justifying SMIP investment), and for Net Zero objectives. Demonstrable savings validate the entire programme rationale and create a virtuous cycle of word-of-mouth promotion.

**Success Metrics**:
- **Primary Metric**: Average percentage reduction in energy consumption for active users vs their own baseline
- **Secondary Metrics**:
  - Absolute kWh savings per household per month
  - Carbon reduction (tonnes CO2e) attributable to app-driven behaviour change
  - Consumer self-reported behaviour changes
  - Engagement with energy-saving recommendations (view rate, action rate)

**Baseline**: Average UK household consumption ~3,700 kWh electricity, ~12,000 kWh gas per year (Ofgem typical consumption values)

**Target**: 5% average reduction in active users = ~185 kWh electricity + ~600 kWh gas per household per year

**Measurement Method**: Compare 12-month rolling consumption before and after app adoption, controlling for weather and tariff changes. Requires consumer consent for research use of their data.

**Dependencies**:
- Accurate consumption data available from DCC/suppliers
- Personalised recommendation engine tuned to UK housing stock and energy patterns
- Consumer consent to use their data for measurement

**Risks to Achievement**:
- Rebound effect (awareness of low usage encourages increased consumption)
- External factors (weather, tariff changes) confounding measurement
- Recommendation quality insufficient to drive behaviour change
- Measurement methodology challenged by NAO or academics

---

### Goal G-3: Achieve Full Regulatory Compliance Before Processing Consumer Data

**Derived From Drivers**: SD-3 (Ofgem), SD-4 (ICO), SD-12 (NCSC), SD-11 (GDS)

**Goal Owner**: DESNZ Data Protection Officer / Programme Compliance Lead

**Goal Statement**: Achieve sign-off from ICO (DPIA), Ofgem (data access framework compliance), NCSC (security assessment), and GDS (Service Standard Beta assessment) before processing any real consumer energy data.

**Why This Matters**: Processing personal energy data without regulatory alignment would expose the programme to enforcement action, reputational damage, and political fallout. Compliance is a prerequisite, not a parallel workstream.

**Success Metrics**:
- **Primary Metric**: Binary — all four regulatory sign-offs achieved (Y/N)
- **Secondary Metrics**:
  - DPIA completed and accepted by ICO
  - Ofgem data access framework alignment confirmed in writing
  - NCSC security review completed with no critical findings
  - GDS Beta assessment passed with "met" on all 14 points

**Baseline**: No assessments completed (new service)

**Target**: All four sign-offs before Beta private access with real consumer data

**Measurement Method**: Formal sign-off letters/reports from each body

**Dependencies**:
- Architecture and design sufficiently mature for assessment
- Regulatory bodies have capacity to conduct assessments in the programme timeline
- No critical security vulnerabilities discovered during testing

**Risks to Achievement**:
- Regulatory review timelines extending beyond programme schedule
- Material findings requiring architectural rework
- GDS assessment resulting in "not met" requiring re-assessment
- ICO raising novel concerns about energy data processing not addressed in current DPIA

---

### Goal G-4: Integrate Successfully with DCC and Major Suppliers by Beta Launch

**Derived From Drivers**: SD-5 (DCC stability), SD-6 (supplier cooperation), SD-2 (delivery)

**Goal Owner**: Programme Technical Architect

**Goal Statement**: Achieve production-ready integration with DCC (SMETS2 data) and at least 6 major energy suppliers (covering 80% of smart meter installations) before Beta launch, with data retrieval success rate above 95%.

**Why This Matters**: Without reliable data from meters via DCC and suppliers, the app has nothing to show consumers. Integration quality directly determines consumer experience — intermittent data retrieval will drive negative reviews and abandonment.

**Success Metrics**:
- **Primary Metric**: Data retrieval success rate (% of half-hourly readings successfully ingested)
- **Secondary Metrics**:
  - Number of integrated suppliers (target: 6+ at Beta, covering 80% of smart meters)
  - Average data latency (time from meter reading to consumer visibility)
  - Integration test pass rate
  - DCC capacity headroom (% of allocated capacity used)

**Baseline**: 0 integrations (new service)

**Target**: DCC + 6 suppliers operational at Beta with >95% retrieval success rate

**Measurement Method**: Integration monitoring dashboards, DCC capacity reports, supplier API health metrics

**Dependencies**:
- DCC delivers API access within agreed timelines
- Suppliers develop and test APIs to agreed specification
- DCC has sufficient capacity for additional data access patterns
- SMETS1 data access pathway agreed (via suppliers, not DCC)

**Risks to Achievement**:
- Supplier API development delays (especially smaller suppliers)
- DCC capacity constraints limiting data retrieval frequency
- SMETS1/SMETS2 data inconsistencies requiring complex normalisation
- Supplier data quality issues (missing readings, incorrect units)

---

### Goal G-5: Deliver an Accessible Service Meeting WCAG 2.2 AA

**Derived From Drivers**: SD-10 (consumer organisations), SD-3 (Ofgem — vulnerable consumers), SD-11 (GDS — Point 5), SD-7 (all consumers)

**Goal Owner**: Head of Design

**Goal Statement**: Achieve WCAG 2.2 Level AA compliance across the entire mobile app, with usability testing by consumers with access needs confirming the app is genuinely usable (not just technically compliant), including for energy data visualisations.

**Why This Matters**: Energy data access is a utility service. Excluding consumers with disabilities, low digital confidence, or older devices from understanding their energy usage is both legally non-compliant and morally unacceptable. Consumer organisations will publicly challenge any failure here.

**Success Metrics**:
- **Primary Metric**: WCAG 2.2 AA audit pass (automated + manual)
- **Secondary Metrics**:
  - Usability testing success rate with consumers using assistive technology
  - Consumer satisfaction scores disaggregated by access needs
  - Accessibility statement published and up to date
  - Time to resolve accessibility defects (target: within sprint)

**Baseline**: N/A (new service)

**Target**: 100% WCAG 2.2 AA compliance at launch; usability testing with 20+ consumers with access needs

**Measurement Method**: Automated accessibility audit tools, manual expert review, user testing sessions with assistive technology users

**Dependencies**:
- Design system supports accessible patterns from the start
- Screen reader compatibility tested on both iOS (VoiceOver) and Android (TalkBack)
- Energy data visualisation alternatives (data tables, text summaries) designed alongside charts

**Risks to Achievement**:
- Complex energy visualisations (charts, graphs) inherently difficult to make accessible
- Mobile platform-specific accessibility quirks requiring extra development
- Accessibility testing compressed due to delivery timeline pressure

---

### Goal G-6: Establish a Sustainable Operating Model

**Derived From Drivers**: SD-9 (HM Treasury — value for money), SD-2 (SRO — delivery), SD-1 (ministerial — no embarrassment)

**Goal Owner**: DESNZ Commercial / Finance Lead

**Goal Statement**: Define and validate an operating model where the ongoing cost of running the service (hosting, support, development) is funded through a sustainable mechanism — either industry levy, consumer value proposition, or justified ongoing government expenditure — within 24 months of launch.

**Why This Matters**: Treasury will not fund an open-ended subsidy. The programme must demonstrate either a path to cost recovery (via industry funding or commercial model) or justify ongoing expenditure against quantified public benefits. An unsustainable model will result in service decline or closure.

**Success Metrics**:
- **Primary Metric**: Ratio of annual operating cost to quantified annual benefits (must be below 1.0)
- **Secondary Metrics**:
  - Annual operating cost (target: defined and controlled)
  - Funding mechanism agreed and operational
  - Benefits realisation report submitted to Treasury annually

**Baseline**: Operating cost TBD pending architecture and hosting decisions

**Target**: Operating cost-benefit ratio below 1.0 by Month 24; funding mechanism agreed by Month 12

**Measurement Method**: Financial reporting, benefits realisation tracking against SOBC commitments

**Dependencies**:
- Architecture decisions that minimise ongoing operational cost
- Adoption rates sufficient to justify costs at scale
- Industry willingness to contribute to funding (if levy model chosen)
- SOBC approved by Treasury with agreed benefits framework

**Risks to Achievement**:
- Hosting and operation costs higher than estimated
- Adoption rates lower than needed to justify costs
- Industry resistance to levy-based funding
- Political pressure to add features that increase operating costs without proportionate benefits

---

### Goal G-7: Support UK Net Zero Objectives Through Data-Driven Behaviour Change

**Derived From Drivers**: SD-1 (strategic policy alignment), SD-7 (consumer savings), SD-8 (engagement)

**Goal Owner**: DESNZ Net Zero Strategy Team

**Goal Statement**: Contribute a measurable reduction in residential carbon emissions by enabling consumers to understand and reduce their energy consumption, with app-attributable carbon savings reported annually to the Climate Change Committee.

**Why This Matters**: The smart metering programme is justified partly on its contribution to Net Zero. The consumer app is the mechanism that converts meter data into behaviour change. Quantified carbon savings strengthen the case for continued investment and contribute to the UK's legally binding Net Zero targets.

**Success Metrics**:
- **Primary Metric**: Tonnes of CO2e saved annually, attributable to app-driven behaviour change
- **Secondary Metrics**:
  - Number of consumers who switched to lower-carbon tariffs via app information
  - Engagement with carbon footprint features
  - Consumer awareness of energy-carbon link (survey measure)

**Baseline**: UK residential emissions ~65 MtCO2e per year

**Target**: Measurable contribution reported from Year 2 onwards (scale dependent on adoption)

**Measurement Method**: Aggregated (anonymised) consumption reduction data combined with grid carbon intensity factors

**Dependencies**:
- Goal G-2 achieved (measurable energy savings)
- Consumer consent for anonymised aggregate analysis
- Carbon intensity data available from National Grid ESO

**Risks to Achievement**:
- Attribution challenge — difficult to isolate app impact from other factors
- Grid decarbonisation masking real consumption changes
- Academic challenge to methodology undermining claims

---

## Goal-to-Outcome Mapping

### Outcome O-1: Demonstrable Consumer Value — "The App That Saves You Money"

**Supported Goals**: G-1 (adoption), G-2 (energy savings), G-7 (Net Zero)

**Outcome Statement**: Consumers who actively use the app save an average of £80-£120 per year on energy bills, with 5 million households benefiting within 18 months of launch, generating aggregate annual savings of £400M-£600M.

**Measurement Details**:
- **KPI**: Average annual bill savings per active user (£)
- **Current Value**: £0 (service doesn't exist)
- **Target Value**: £80-£120 per household per year
- **Measurement Frequency**: Quarterly
- **Data Source**: Consumption data comparison (with consent) + tariff switching tracking
- **Report Owner**: DESNZ Programme Analytics Team

**Business Value**:
- **Financial Impact**: £400M-£600M aggregate annual consumer savings (at 5M users)
- **Strategic Impact**: Validates SMIP investment, supports Net Zero narrative
- **Operational Impact**: Reduced call centre volumes for energy supplier basic queries
- **Customer Impact**: Tangible financial benefit driving trust and continued engagement

**Timeline**:
- **Phase 1 (Months 1-6 post-launch)**: Early adopters, limited savings data, focus on adoption
- **Phase 2 (Months 7-12)**: First savings data available, initial benefit quantification
- **Phase 3 (Months 13-18)**: 5M users, robust savings data, annual benefit reporting
- **Sustainment (Year 2+)**: Growing user base, refined recommendations, compounding savings

**Stakeholder Benefits**:
- **DESNZ Minister**: "The smart meter app saved British households £X million last year"
- **Citizens**: Lower energy bills, actionable understanding of energy usage
- **HM Treasury**: Quantified benefits exceeding programme costs
- **Smart Energy GB**: Evidence supporting their consumer engagement campaigns

**Leading Indicators**: Download rates, meter linkage completion, recommendation engagement
**Lagging Indicators**: Measured kWh reduction, bill savings calculated, NPS score

---

### Outcome O-2: Regulatory Confidence — "A Trusted, Compliant Service"

**Supported Goals**: G-3 (regulatory compliance), G-5 (accessibility)

**Outcome Statement**: The service operates with zero data protection enforcement actions, zero critical security incidents, and passes all GDS Service Standard assessments on first attempt — establishing it as an exemplar of UK Government digital service delivery.

**Measurement Details**:
- **KPI**: Regulatory compliance score (composite: ICO, Ofgem, GDS, NCSC)
- **Current Value**: N/A (new service)
- **Target Value**: Full compliance maintained continuously
- **Measurement Frequency**: Quarterly self-assessment, annual external audit
- **Data Source**: Regulatory correspondence, assessment reports, incident logs
- **Report Owner**: Programme Compliance Lead

**Business Value**:
- **Financial Impact**: Cost avoidance (ICO fines up to £17.5M; reputational damage costs)
- **Strategic Impact**: Government exemplar for data-driven consumer services
- **Operational Impact**: Reduced compliance firefighting, sustainable operations
- **Customer Impact**: Consumer trust maintained — essential for adoption

**Timeline**:
- **Phase 1 (Pre-launch)**: All regulatory sign-offs achieved
- **Phase 2 (Months 1-6)**: First operational compliance report
- **Phase 3 (Months 7-12)**: Annual compliance audit, GDS Live assessment
- **Sustainment (Year 2+)**: Continuous compliance monitoring, annual audits

**Stakeholder Benefits**:
- **ICO**: Exemplar of privacy by design in consumer energy services
- **Ofgem**: Consumer data access framework operating as intended
- **GDS**: Successful service demonstrating the Service Standard in action
- **NCSC**: Secure consumer service connected to critical infrastructure
- **DESNZ Minister**: No embarrassing headlines, no enforcement actions

**Leading Indicators**: DPIA sign-off, security assessment results, GDS assessment feedback
**Lagging Indicators**: Zero enforcement actions, zero data breaches, assessment pass rates

---

### Outcome O-3: Ecosystem Integration — "Connected Smart Metering"

**Supported Goals**: G-4 (DCC/supplier integration), G-1 (adoption — more suppliers = more consumers eligible)

**Outcome Statement**: The app successfully retrieves consumption data from 90%+ of Great Britain's smart meters through integrated DCC and supplier APIs, with data available to consumers within 24 hours of the meter reading.

**Measurement Details**:
- **KPI**: Smart meter population coverage (% of GB smart meters from which data can be retrieved)
- **Current Value**: 0%
- **Target Value**: 80% at Beta, 90% at Live
- **Measurement Frequency**: Monthly
- **Data Source**: Integration monitoring, supplier onboarding tracker
- **Report Owner**: Technical Architect

**Business Value**:
- **Financial Impact**: Higher coverage = more eligible users = better cost-benefit ratio
- **Strategic Impact**: Creates a de facto standard for consumer energy data access
- **Operational Impact**: Standardised integration reduces per-supplier support costs
- **Customer Impact**: Consumers can use the app regardless of their energy supplier

**Timeline**:
- **Phase 1 (Alpha)**: DCC sandbox integration, 2 supplier APIs in test
- **Phase 2 (Beta)**: DCC production + 6 suppliers (80% coverage)
- **Phase 3 (Live)**: 10+ suppliers (90% coverage)
- **Sustainment (Year 2+)**: All suppliers integrated, new market entrants onboarded routinely

**Stakeholder Benefits**:
- **DCC**: Demonstrates DCC value to consumers (not just industry)
- **Energy Suppliers**: Standardised API reduces bespoke integration requests
- **Citizens**: Works regardless of which supplier they use
- **Ofgem**: Data access framework operating at scale

**Leading Indicators**: Supplier API readiness assessments, integration test pass rates
**Lagging Indicators**: Population coverage percentage, data retrieval success rates

---

### Outcome O-4: Value for Money — "Justified Public Investment"

**Supported Goals**: G-6 (sustainable model), G-1 (adoption), G-2 (savings)

**Outcome Statement**: The programme delivers a benefit-cost ratio (BCR) above 2.0 over 10 years, with annual operating costs below £15M and a sustainable funding mechanism in place within 24 months.

**Measurement Details**:
- **KPI**: Benefit-cost ratio (BCR)
- **Current Value**: Estimated in SOBC (TBD)
- **Target Value**: BCR > 2.0 over 10 years
- **Measurement Frequency**: Annual
- **Data Source**: Programme financial reports, benefits realisation tracking
- **Report Owner**: DESNZ Finance / Programme Commercial Lead

**Business Value**:
- **Financial Impact**: Demonstrable return on public investment
- **Strategic Impact**: Justifies future government investment in consumer data services
- **Operational Impact**: Sustainable service not dependent on annual budget fights

**Timeline**:
- **Phase 1 (Pre-launch)**: SOBC approved with estimated BCR
- **Phase 2 (Months 1-12)**: Initial benefits data, funding mechanism design
- **Phase 3 (Months 13-24)**: Funding mechanism operational, first annual benefits report
- **Sustainment (Year 2+)**: Annual benefits realisation against SOBC commitments

**Stakeholder Benefits**:
- **HM Treasury**: Demonstrated return, sustainable model, no perpetual subsidy
- **DESNZ Minister**: Positive NAO/PAC narrative
- **NAO**: Clear audit trail from costs to benefits

**Leading Indicators**: SOBC approval, adoption trajectory vs plan, cost tracking vs budget
**Lagging Indicators**: Actual BCR calculated, NAO assessment, annual benefits report

---

## Complete Traceability Matrix

### Stakeholder → Driver → Goal → Outcome

| Stakeholder | Driver ID | Driver Summary | Goal ID | Goal Summary | Outcome ID | Outcome Summary |
|-------------|-----------|----------------|---------|--------------|------------|-----------------|
| DESNZ Minister | SD-1 | Demonstrate SMIP return | G-1 | 5M active users | O-1 | Consumer savings £400-600M/yr |
| DESNZ Minister | SD-1 | Demonstrate SMIP return | G-2 | 5% energy savings | O-1 | Consumer savings £400-600M/yr |
| DESNZ Minister | SD-1 | Demonstrate SMIP return | G-7 | Net Zero contribution | O-1 | Consumer savings £400-600M/yr |
| DESNZ SRO | SD-2 | Deliver on time/budget | G-3 | Regulatory compliance | O-2 | Trusted, compliant service |
| DESNZ SRO | SD-2 | Deliver on time/budget | G-4 | DCC/supplier integration | O-3 | 90% meter coverage |
| Ofgem | SD-3 | Protect consumer interests | G-3 | Regulatory compliance | O-2 | Trusted, compliant service |
| Ofgem | SD-3 | Protect consumer interests | G-5 | WCAG 2.2 AA compliance | O-2 | Trusted, compliant service |
| ICO | SD-4 | Lawful data processing | G-3 | Regulatory compliance | O-2 | Trusted, compliant service |
| DCC | SD-5 | Infrastructure stability | G-4 | DCC/supplier integration | O-3 | 90% meter coverage |
| Energy Suppliers | SD-6 | Manage customer relationship | G-4 | DCC/supplier integration | O-3 | 90% meter coverage |
| Citizens | SD-7 | Reduce energy costs | G-1 | 5M active users | O-1 | Consumer savings £400-600M/yr |
| Citizens | SD-7 | Reduce energy costs | G-2 | 5% energy savings | O-1 | Consumer savings £400-600M/yr |
| Smart Energy GB | SD-8 | Consumer engagement | G-1 | 5M active users | O-1 | Consumer savings £400-600M/yr |
| HM Treasury | SD-9 | Value for money | G-6 | Sustainable operating model | O-4 | BCR > 2.0, sustainable funding |
| Consumer Orgs | SD-10 | Inclusive and fair service | G-5 | WCAG 2.2 AA compliance | O-2 | Trusted, compliant service |
| GDS Assessors | SD-11 | Service Standard compliance | G-3 | Regulatory compliance | O-2 | Trusted, compliant service |
| NCSC | SD-12 | Cyber security | G-3 | Regulatory compliance | O-2 | Trusted, compliant service |

### Conflict Analysis

**Competing Drivers**:

- **Conflict 1**: DESNZ Minister (SD-1) wants **rapid launch and high adoption** but Ofgem/ICO/NCSC (SD-3/SD-4/SD-12) require **thorough regulatory review** before consumer data is processed.
  - **Resolution Strategy**: Phased launch — Alpha with synthetic data, private Beta with consenting volunteers under close monitoring, public Beta only after regulatory sign-offs. Ministerial comms can celebrate milestones at each phase without requiring mass-market launch.

- **Conflict 2**: Energy Suppliers (SD-6) want to **protect their customer relationship** but Citizens (SD-7) and Ofgem (SD-3) want **impartial tariff comparison** that may drive switching.
  - **Resolution Strategy**: Position the app as complementary to supplier apps (deeper data, not replacement), ensure tariff comparison methodology is Ofgem-endorsed and transparent, give suppliers visibility of comparison methodology before launch. Frame switching as a consumer right, not an attack on suppliers.

- **Conflict 3**: DCC (SD-5) wants to **limit new load on infrastructure** but consumer adoption goals (G-1) could drive **millions of data requests**.
  - **Resolution Strategy**: Design for batch retrieval (align with existing DCC data flows), implement aggressive caching so consumers view cached data by default, define capacity thresholds with DCC and agree scaling plan. Consumer-facing real-time data requests go to platform cache, not to DCC directly.

- **Conflict 4**: HM Treasury (SD-9) wants **minimal cost** but the service needs **investment in accessibility, security, and quality** (SD-10, SD-12, SD-11) that increases cost.
  - **Resolution Strategy**: Frame accessibility and security as risk avoidance (ICO fines, reputational damage, GDS failure) in the business case. Quantify the cost of non-compliance versus cost of doing it right. Use agile delivery to demonstrate value incrementally.

**Synergies**:

- **Synergy 1**: DESNZ Minister (SD-1) and Citizens (SD-7) both benefit from **high adoption and measurable savings** — achieving G-1 and G-2 satisfies both simultaneously.
- **Synergy 2**: Ofgem (SD-3) and ICO (SD-4) both require **robust consumer protection and data governance** — investing in compliance satisfies both regulators through a single governance framework.
- **Synergy 3**: Smart Energy GB (SD-8) and DESNZ (SD-1) both want **positive consumer engagement** — co-promotion reduces marketing costs and amplifies reach.
- **Synergy 4**: DCC (SD-5) and programme efficiency goals benefit from **batch retrieval and caching patterns** — reducing DCC load also improves platform performance and cost efficiency.

---

## Communication & Engagement Plan

### DESNZ Minister

**Primary Message**: The smart meter app is converting the £13.5bn smart metering investment into tangible benefits for millions of consumers — lower bills, less waste, contribution to Net Zero.

**Key Talking Points**:
- [Adoption number] consumers now using the app to manage their energy
- Average user saving £[X] per year — aggregate savings of £[Y] million
- App passed all GDS and security assessments — exemplar digital service

**Communication Frequency**: Monthly ministerial briefing; ad hoc for PQs and media

**Preferred Channel**: Ministerial submission (formal), briefing pack (dashboard + key metrics)

**Success Story**: "Minister announces 5 millionth user of smart meter app — households saving over £400M annually"

---

### Ofgem

**Primary Message**: The app operates fully within the Ofgem data access framework, with consumer consent at its core, impartial tariff information, and dedicated vulnerability features.

**Key Talking Points**:
- Consent framework exceeds minimum requirements — granular, revocable, auditable
- Tariff comparison methodology independently reviewed and transparent
- Prepayment meter features and assisted digital support for vulnerable consumers

**Communication Frequency**: Quarterly regulatory engagement meeting

**Preferred Channel**: Formal regulatory correspondence, quarterly compliance report

**Success Story**: "Ofgem commends the app's consumer protection approach as best practice for third-party energy data access"

---

### Energy Suppliers

**Primary Message**: The app complements (not replaces) your consumer offering, using a standardised API that reduces your integration burden and is built with full transparency on tariff comparison methodology.

**Key Talking Points**:
- Standardised API means you build once, not per-app
- Tariff comparison methodology available for review and feedback
- App drives engagement with energy data — benefits your customers too
- Your branding preserved where consumers interact with supplier-specific data

**Communication Frequency**: Monthly supplier forum; fortnightly technical integration calls during build

**Preferred Channel**: Supplier forum (multi-party), bilateral calls for integration issues

**Success Story**: "Major suppliers report 15% reduction in basic energy queries after consumers start using the app for self-service"

---

### Citizens / Energy Consumers

**Primary Message**: See exactly where your energy goes, find out if you're on the best deal, and get personalised tips to save money — all in one trusted app.

**Key Talking Points**:
- Your data is yours — you control who sees it and can delete it anytime
- Simple, jargon-free view of your gas and electricity usage
- Personalised saving recommendations based on your actual usage patterns
- Works with your existing smart meter — no new equipment needed

**Communication Frequency**: App store listing, in-app guidance, Smart Energy GB campaigns

**Preferred Channel**: App stores, social media, Smart Energy GB marketing channels, energy bills (supplier partnership)

**Success Story**: "I switched tariff based on the app's recommendation and I'm saving £15 a month" — real consumer testimonial

---

### HM Treasury

**Primary Message**: The programme is delivering quantified benefits exceeding costs, with a credible path to sustainable funding that does not require perpetual government subsidy.

**Key Talking Points**:
- BCR of [X] based on measured consumer savings
- Operating costs of £[Y]M per year against £[Z]M annual benefits
- Funding mechanism [agreed/under discussion] with industry
- On track against SOBC commitments

**Communication Frequency**: Annual benefits report; ad hoc for spend control and business case updates

**Preferred Channel**: Formal Treasury submission, supplemented by benefits dashboard

**Success Story**: "Smart meter app delivers BCR of 3.2 — every £1 spent generates £3.20 in consumer benefits"

---

## Change Impact Assessment

### Impact on Stakeholders

| Stakeholder | Current State | Future State | Change Magnitude | Resistance Risk | Mitigation Strategy |
|-------------|---------------|--------------|------------------|-----------------|---------------------|
| Citizens | View IHD or supplier app (if any) for energy data | New government-backed app offering unified view across meters | MEDIUM | LOW | Strong value proposition (savings), trusted branding |
| Energy Suppliers | Own the consumer data relationship | Share data via APIs; consumers get impartial tariff comparison | HIGH | HIGH | Position as complement, supplier forum, transparent methodology |
| DCC | Serves industry (suppliers, networks) | Also serves consumers indirectly via platform | MEDIUM | MEDIUM | Capacity planning, batch patterns, commercial agreement |
| DESNZ Digital Team | No consumer energy app in portfolio | Operating a mass-market mobile service | HIGH | LOW | Build/grow team, establish operating model early |
| Ofgem | Regulate supplier data access bilaterally | Oversee third-party consumer app data access at scale | MEDIUM | LOW | Early engagement, framework alignment confirmation |

### Change Readiness

**Champions** (Enthusiastic supporters):
- **Smart Energy GB** — App extends their consumer engagement mission
- **Octopus Energy / challenger suppliers** — App could drive switching to competitive tariffs
- **Consumer organisations** — If accessibility and vulnerability features are strong
- **DESNZ Minister** — Visible policy deliverable

**Fence-sitters** (Neutral, need convincing):
- **DCC** — Supportive in principle but concerned about capacity and cost impact. Convince with: clear capacity plan, batch patterns, commercial agreement
- **GDS Assessors** — Neutral until evidence presented. Convince with: genuine user research, working prototypes, operational metrics
- **HM Treasury** — Sceptical until business case proven. Convince with: strong SOBC, early benefit signals, credible operating model

**Resisters** (Opposed or sceptical):
- **Incumbent energy suppliers (Big Six)** — Concerned about switching acceleration and loss of customer relationship. Address with: complementary positioning, supplier forum engagement, transparent methodology, Ofgem regulatory mandate
- **Supplier app teams** — May see this as competitor to their own investment. Address with: differentiated positioning (government = trusted impartial source, supplier = personalised service)

---

## Risk Register (Stakeholder-Related)

### Risk R-1: Energy Supplier Non-Cooperation

**Related Stakeholders**: Energy Suppliers (SD-6), DCC (SD-5), Citizens (SD-7)

**Risk Description**: Major energy suppliers delay or provide poor-quality API integrations, resulting in the app being unable to retrieve data for a significant proportion of consumers. Suppliers may cite resource constraints, technical complexity, or commercial concerns.

**Impact on Goals**: G-4 (integration), G-1 (adoption — consumers can't use app without their supplier integrated)

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**: Ofgem regulatory mandate for supplier cooperation; supplier forum creating peer pressure; early pilot with willing suppliers (Octopus Energy known for API-first approach); standardised API spec reducing supplier burden; DESNZ senior engagement with supplier CEOs.

**Contingency Plan**: Launch with willing suppliers first, creating consumer pressure on remaining suppliers. Ofgem enforcement if necessary.

---

### Risk R-2: Consumer Data Breach

**Related Stakeholders**: ICO (SD-4), Citizens (SD-7), DESNZ Minister (SD-1), NCSC (SD-12)

**Risk Description**: A security incident results in unauthorised access to consumer energy consumption data, triggering ICO investigation, media coverage, and consumer trust collapse.

**Impact on Goals**: G-3 (compliance), G-1 (adoption — consumers abandon the app)

**Probability**: LOW (with proper controls)

**Impact**: CRITICAL

**Mitigation Strategy**: Security by Design (ARC-000-PRIN Principle 5), regular penetration testing, NCSC security review, bug bounty programme, encryption at rest and in transit, minimal data retention.

**Contingency Plan**: ICO notification within 72 hours, pre-prepared incident comms plan, consumer notification and remediation, independent security audit, ministerial lines to take.

---

### Risk R-3: Low Consumer Adoption

**Related Stakeholders**: DESNZ Minister (SD-1), HM Treasury (SD-9), Smart Energy GB (SD-8)

**Risk Description**: Consumer adoption falls significantly below the 5 million target due to low awareness, complex onboarding, competing supplier apps, or apathy. This undermines the value-for-money case and ministerial narrative.

**Impact on Goals**: G-1 (adoption), G-6 (sustainable model — costs without users)

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**: Co-marketing with Smart Energy GB, energy supplier bill inserts, simple onboarding (3 taps to value), immediate personalised savings estimate at sign-up, app store optimisation.

**Contingency Plan**: Pivot marketing strategy, simplify onboarding further, consider integration with supplier apps rather than standalone app, adjust targets and timelines.

---

### Risk R-4: DCC Capacity Constraints

**Related Stakeholders**: DCC (SD-5), DESNZ SRO (SD-2), Energy Suppliers (SD-6)

**Risk Description**: The additional data access load from the consumer app exceeds DCC capacity, causing degradation of service for existing smart metering operations (supplier reads, firmware updates, etc.).

**Impact on Goals**: G-4 (integration), G-1 (consumer experience degraded by slow data)

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**: Batch retrieval aligned with DCC low-traffic windows, aggressive platform-side caching, phased rollout with capacity monitoring, pre-agreed capacity allocation with DCC.

**Contingency Plan**: Throttle data retrieval frequency, prioritise DCC capacity for existing operations, extend data latency targets (e.g., 48 hours instead of 24).

---

### Risk R-5: GDS Assessment Failure

**Related Stakeholders**: GDS Assessors (SD-11), DESNZ SRO (SD-2), DESNZ Minister (SD-1)

**Risk Description**: The service fails a GDS Service Standard assessment, requiring a re-assessment and delaying the programme. A "not met" result becomes public and creates political embarrassment.

**Impact on Goals**: G-3 (compliance), G-1 (delayed launch impacts adoption targets)

**Probability**: LOW (with proper preparation)

**Impact**: MEDIUM

**Mitigation Strategy**: GDS engagement from Discovery phase, continuous user research, evidence portfolio maintained throughout, pre-assessment mock reviews, address GDS feedback iteratively.

**Contingency Plan**: Address assessment findings rapidly, request re-assessment at earliest opportunity, manage communications to frame as "doing it right" not "failure."

---

### Risk R-6: Political or Machinery-of-Government Changes

**Related Stakeholders**: DESNZ Minister (SD-1), DESNZ SRO (SD-2), HM Treasury (SD-9)

**Risk Description**: Cabinet reshuffle, departmental restructuring, or change of government priorities defunds or deprioritises the programme. Energy policy is politically sensitive and subject to ministerial change.

**Impact on Goals**: All goals at risk if funding or political support withdrawn

**Probability**: MEDIUM (over the programme lifecycle)

**Impact**: CRITICAL

**Mitigation Strategy**: Cross-party appeal of consumer empowerment and cost savings, embed in departmental delivery plan, build broad stakeholder support beyond a single minister, demonstrate early value.

**Contingency Plan**: Articulate programme value in terms that transcend political allegiance (consumer savings, Net Zero), ensure contractual commitments with suppliers/DCC create momentum that's difficult to reverse.

---

## Governance & Decision Rights

### Decision Authority Matrix (RACI)

| Decision Type | Responsible | Accountable | Consulted | Informed |
|---------------|-------------|-------------|-----------|----------|
| Programme budget and scope | Programme Director | DESNZ SRO | HM Treasury, CDDO | All stakeholders |
| Architecture and technology choices | Technical Architect | DESNZ SRO | NCSC, DCC, GDS | Energy Suppliers, Delivery Team |
| Data processing and consent model | DPO / Privacy Lead | DESNZ SRO | ICO, Ofgem | Consumer Orgs, Citizens |
| Supplier API specification | Technical Architect | Programme Director | DCC, Energy Suppliers | Ofgem |
| Tariff comparison methodology | Product Owner | Programme Director | Ofgem, Consumer Orgs | Energy Suppliers |
| Go/no-go for Beta with real data | Programme Director | DESNZ SRO | ICO, Ofgem, NCSC, GDS | All stakeholders |
| Go/no-go for public launch | DESNZ SRO | DESNZ Minister | All key stakeholders | All stakeholders |
| Exception to architecture principles | Technical Architect | DESNZ SRO | Architecture Review Board | Delivery Team |
| Security incident response | Security Lead | DESNZ SRO | NCSC, ICO | Minister, DCC, Suppliers |
| Feature prioritisation | Product Owner | Programme Director | User researchers, GDS | All stakeholders |

### Escalation Path

1. **Level 1**: Product Owner / Technical Architect (day-to-day design and delivery decisions)
2. **Level 2**: Programme Director (scope, timeline, budget variances, supplier issues)
3. **Level 3**: DESNZ SRO (cross-departmental issues, regulatory conflicts, major risk decisions)
4. **Level 4**: DESNZ Minister (political decisions, inter-ministerial issues, public announcements)

---

## Validation & Sign-off

### Stakeholder Review

| Stakeholder | Review Date | Comments | Status |
|-------------|-------------|----------|--------|
| DESNZ SRO | PENDING | | PENDING |
| Ofgem Representative | PENDING | | PENDING |
| DCC Representative | PENDING | | PENDING |
| Supplier Forum Chair | PENDING | | PENDING |
| Consumer Org Representative | PENDING | | PENDING |
| ICO (informal) | PENDING | | PENDING |

### Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Programme SRO | | | |
| DESNZ Digital Lead | | | |
| Enterprise Architect | | | |

---

## Appendices

### Appendix A: Stakeholder Interview Plan

Interviews should be conducted with the following stakeholders to validate and enrich this analysis:

| Stakeholder | Contact | Priority | Status |
|-------------|---------|----------|--------|
| DESNZ Smart Metering Programme Director | TBC | HIGH | NOT STARTED |
| Ofgem Data Access Policy Lead | TBC | HIGH | NOT STARTED |
| DCC Technical Architecture Lead | TBC | HIGH | NOT STARTED |
| Octopus Energy API Team (willing pioneer) | TBC | HIGH | NOT STARTED |
| British Gas Digital Director | TBC | MEDIUM | NOT STARTED |
| Citizens Advice Energy Policy Lead | TBC | MEDIUM | NOT STARTED |
| ICO Technology Policy Team | TBC | MEDIUM | NOT STARTED |
| Smart Energy GB Campaign Director | TBC | MEDIUM | NOT STARTED |
| GDS Assessment Lead (informal pre-engagement) | TBC | MEDIUM | NOT STARTED |
| Consumer representative panel (user research) | TBC | HIGH | NOT STARTED |

### Appendix B: Key Assumptions

1. DESNZ will fund the programme through Spending Review allocation
2. DCC will provide API access under existing or amended SEC arrangements
3. Energy suppliers are legally obligated to share consumer data (with consent) under Ofgem licence conditions
4. The app will be delivered as a government service subject to the GDS Service Standard
5. Consumer energy consumption data is classified as OFFICIAL under UK Government security classification
6. The app will be published on Apple App Store and Google Play Store
7. Smart Energy GB will co-promote the app through existing consumer engagement channels

### Appendix C: References

| Document | Reference |
|----------|-----------|
| Architecture Principles | ARC-000-PRIN-v1.0 |
| Smart Energy Code (SEC) | smartenergycodecompany.co.uk |
| Ofgem Data Access Framework | ofgem.gov.uk |
| DCC Technical Architecture | smartdcc.co.uk |
| GDS Service Standard | service-manual.service.gov.uk |
| UK GDPR / DPA 2018 | legislation.gov.uk |
| NCSC Secure by Design | ncsc.gov.uk |
| HM Treasury Green Book | gov.uk/government/publications/the-green-book-appraisal-and-evaluation-in-central-government |

---

**Generated by**: ArcKit `/arckit.stakeholders` command
**Generated on**: 2026-01-31
**ArcKit Version**: 1.0.3
**Project**: UK Smart Meter Data Consumer Mobile App (Project 001)
**AI Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
