# Project Requirements: UK Smart Meter Data Consumer Mobile App

> **Template Status**: Live | **Version**: 1.0.3 | **Command**: `/arckit.requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-REQ-v1.0 |
| **Document Type** | Business and Technical Requirements |
| **Project** | UK Smart Meter Data Consumer Mobile App (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-01-31 |
| **Last Modified** | 2026-01-31 |
| **Review Cycle** | Monthly |
| **Next Review Date** | 2026-03-02 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Programme Board, Delivery Team, Architecture Team, DCC, Ofgem, GDS Assessors |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-31 | ArcKit AI | Initial creation from `/arckit.requirements` command | PENDING | PENDING |

## Document Purpose

This document defines the comprehensive business, functional, non-functional, integration, and data requirements for the UK Smart Meter Data Consumer Mobile App. It serves as the basis for architecture design, vendor procurement (SOW/RFP), development, testing, and acceptance. All requirements trace to stakeholder goals (ARC-001-STKE-v1.0) and are governed by architecture principles (ARC-000-PRIN-v1.0).

---

## Executive Summary

### Business Context

The Smart Metering Implementation Programme (SMIP) has deployed over 34 million smart meters across Great Britain at a cost of £13.5 billion. While this infrastructure enables half-hourly energy consumption data collection, most consumers do not actively engage with their smart meter data beyond the In-Home Display (IHD). There is no single, trusted, supplier-neutral mobile application that empowers consumers to understand their energy usage, compare tariffs using actual consumption data, and take action to reduce their bills.

This project delivers a cross-platform mobile application that connects to the Data Communications Company (DCC) smart metering infrastructure and energy supplier APIs to retrieve, visualise, and act upon consumer energy consumption data. It is a UK Government initiative subject to the GDS Service Standard, Technology Code of Practice, and NCSC Secure by Design requirements.

The app addresses a market failure: individual energy suppliers have incentives to retain customers rather than facilitate switching, and no independent party currently provides consumers with trusted, impartial access to their own smart meter data in a single, accessible mobile experience.

### Objectives

- Enable 34 million smart meter households to access their half-hourly energy consumption data via a trusted mobile application
- Deliver measurable energy savings of 5% average reduction for active users through personalised recommendations and consumption visibility
- Achieve 5 million monthly active users within 18 months of public launch
- Establish a supplier-neutral tariff comparison capability using actual consumption data
- Demonstrate compliance with UK GDPR, Smart Energy Code, GDS Service Standard, and NCSC Secure by Design

### Expected Outcomes

- £400M-£600M aggregate annual consumer energy bill savings (at 5 million active users) — traces to Outcome O-1 (ARC-001-STKE)
- Zero data protection enforcement actions, zero critical security incidents — traces to Outcome O-2
- 90%+ smart meter population coverage through DCC and supplier integrations — traces to Outcome O-3
- Benefit-cost ratio above 2.0 over 10 years — traces to Outcome O-4

### Project Scope

**In Scope**:
- Cross-platform mobile app (iOS and Android)
- Consumer authentication and smart meter linking
- Half-hourly electricity and gas consumption data retrieval (SMETS1 via suppliers, SMETS2 via DCC)
- Real-time and historical energy usage visualisation
- Personalised energy-saving recommendations
- Tariff comparison using actual consumption data
- Consumption alerts and budget tracking
- Prepayment meter features (balance, top-up reminders)
- Consumer consent management (granular, revocable)
- Backend platform for data ingestion, processing, and storage
- Integration with DCC and energy supplier APIs
- Anonymised aggregate data publishing (with consent) for energy research

**Out of Scope**:
- In-Home Display (IHD) firmware updates or replacement
- Direct energy switching/purchasing within the app (Phase 2)
- Smart home device integration (e.g., smart thermostats) (Phase 2)
- Non-GB markets (Northern Ireland uses a different smart metering system)
- Microbusiness or commercial smart meters
- Solar/battery storage export monitoring (Phase 2)
- Open Banking integration for bill payments (Phase 2)

---

## Stakeholders

| Stakeholder | Role | Organisation | Involvement Level |
|-------------|------|--------------|-------------------|
| DESNZ Minister | Ministerial accountability | DESNZ | Decision authority on public launch |
| DESNZ SRO | Senior Responsible Owner | DESNZ | Programme accountability |
| Programme Director | Delivery lead | DESNZ | Day-to-day programme decisions |
| Technical Architect | Architecture authority | Programme | Architecture and technology decisions |
| DPO / Privacy Lead | Data protection | DESNZ | DPIA, consent, data processing |
| Ofgem | Energy regulator | Ofgem | Data access framework, consumer protection |
| ICO | Data protection regulator | ICO | DPIA review, data processing oversight |
| DCC | Infrastructure partner | DCC | SMETS2 data access, capacity planning |
| Energy Suppliers | Data providers | Multiple | API integration, data quality |
| GDS Assessors | Service Standard | GDS | Phase assessments |
| NCSC | Cyber security | NCSC | Security review, threat assessment |
| Consumer Representatives | End user voice | Citizens Advice, Which? | User research, accessibility, vulnerability |
| Citizens / Consumers | End users | Public | App usage, feedback, user research |

*Full stakeholder analysis: ARC-001-STKE-v1.0*

---

## Business Requirements

### BR-001: Consumer Energy Data Access

**Description**: The service MUST enable energy consumers with smart meters to access their half-hourly gas and electricity consumption data through a mobile application, regardless of their energy supplier.

**Rationale**: Consumers have a right to access their energy data under Ofgem licence conditions. Currently there is no single, trusted, supplier-neutral channel for this access. This addresses stakeholder driver SD-7 (Citizens — understand and reduce energy costs) and goal G-1 (5M active users).

**Success Criteria**:
- Consumers can view their half-hourly consumption data for electricity and gas
- Data available from both SMETS1 (via supplier) and SMETS2 (via DCC) meters
- Data accessible regardless of which energy supplier the consumer uses (minimum 80% smart meter coverage at Beta, 90% at Live)

**Priority**: MUST_HAVE

**Stakeholder**: Citizens (SD-7), DESNZ Minister (SD-1), Ofgem (SD-3)

**Traces To**: Goal G-1, Goal G-4, Outcome O-1, Outcome O-3

**Principles**: Principle 1 (User-Centred Design), Principle 4 (Interoperability)

---

### BR-002: Consumer Energy Cost Reduction

**Description**: The service MUST provide consumers with actionable information that enables them to reduce their energy consumption and costs, targeting an average 5% energy reduction for active users.

**Rationale**: Demonstrable energy savings justify the £13.5bn SMIP investment and address the cost-of-living crisis impact on household energy bills. This addresses stakeholder driver SD-1 (DESNZ Minister — demonstrate SMIP return) and goal G-2 (measurable energy savings).

**Success Criteria**:
- Active users reduce energy consumption by an average of 5% within 6 months of first use
- Consumers can view estimated savings in pounds sterling
- Personalised recommendations provided based on actual consumption patterns
- Tariff comparison shows potential savings from switching supplier

**Priority**: MUST_HAVE

**Stakeholder**: DESNZ Minister (SD-1), Citizens (SD-7), HM Treasury (SD-9)

**Traces To**: Goal G-2, Outcome O-1, Outcome O-4

**Principles**: Principle 1 (User-Centred Design)

---

### BR-003: Regulatory Compliance

**Description**: The service MUST achieve regulatory approval from ICO, Ofgem, NCSC, and GDS before processing any real consumer energy data, and maintain continuous compliance throughout operation.

**Rationale**: Energy consumption data is personal data under UK GDPR. The smart metering ecosystem is critical national infrastructure. Processing without regulatory alignment risks enforcement action (ICO fines up to £17.5M), political fallout, and consumer trust collapse. Addresses goal G-3 (regulatory compliance).

**Success Criteria**:
- DPIA completed and accepted by ICO before Beta with real data
- Ofgem data access framework alignment confirmed in writing
- NCSC security review passed with no critical findings
- GDS Service Standard assessment passed at each phase gate
- Zero data protection enforcement actions in operation

**Priority**: MUST_HAVE

**Stakeholder**: ICO (SD-4), Ofgem (SD-3), NCSC (SD-12), GDS (SD-11)

**Traces To**: Goal G-3, Outcome O-2

**Principles**: Principle 5 (Security by Design), Principle 7 (Privacy by Design), Principle 20 (GDS Service Standard)

---

### BR-004: Mass Consumer Adoption

**Description**: The service MUST be designed to achieve 5 million monthly active users within 18 months of public launch, with a 30-day retention rate above 40%.

**Rationale**: Adoption is the threshold for programme viability — without users, there are no benefits, no value for money, and no justification for the investment. The 5M target represents 15% of smart meter households, sufficient to demonstrate national impact.

**Success Criteria**:
- 5 million MAU by Month 18 post-launch
- 30-day retention rate above 40%
- App store rating of 4.2 or above on both platforms
- Meter linkage completion rate above 60% (downloads → linked meters)

**Priority**: MUST_HAVE

**Stakeholder**: DESNZ Minister (SD-1), DESNZ SRO (SD-2), Smart Energy GB (SD-8)

**Traces To**: Goal G-1, Outcome O-1, Outcome O-4

**Principles**: Principle 1 (User-Centred Design), Principle 15 (Accessibility)

---

### BR-005: Inclusive and Accessible Service

**Description**: The service MUST be accessible to all consumers including those with disabilities, low digital confidence, prepayment meters, or vulnerable circumstances, meeting WCAG 2.2 Level AA.

**Rationale**: Energy data access is a utility service. Excluding consumers with access needs is legally non-compliant under the Accessibility Regulations 2018 and will be publicly challenged by consumer organisations. Addresses goal G-5.

**Success Criteria**:
- WCAG 2.2 AA compliance verified by automated and manual audit
- Usability tested with 20+ consumers with access needs
- Prepayment meter features included at launch
- Assisted digital support channel available for consumers who cannot use the app independently
- Energy data visualisations have accessible alternatives (data tables, text summaries)

**Priority**: MUST_HAVE

**Stakeholder**: Consumer Orgs (SD-10), Ofgem (SD-3), GDS (SD-11), Citizens (SD-7)

**Traces To**: Goal G-5, Outcome O-2

**Principles**: Principle 15 (Accessibility), Principle 1 (User-Centred Design)

---

### BR-006: Sustainable Operating Model

**Description**: The programme MUST establish a sustainable funding mechanism for the ongoing operation of the service within 24 months of launch, with a benefit-cost ratio above 2.0 over 10 years.

**Rationale**: HM Treasury will not fund an open-ended subsidy. The programme must demonstrate either cost recovery or justified ongoing expenditure against quantified benefits. Addresses goal G-6.

**Success Criteria**:
- Annual operating cost defined and controlled
- Funding mechanism agreed (industry levy, justified government expenditure, or hybrid) by Month 12
- BCR above 2.0 validated against measured benefits by Month 24
- Annual benefits realisation report submitted to Treasury

**Priority**: MUST_HAVE

**Stakeholder**: HM Treasury (SD-9), DESNZ SRO (SD-2)

**Traces To**: Goal G-6, Outcome O-4

---

### BR-007: Net Zero Contribution

**Description**: The service SHOULD contribute measurably to UK residential carbon emission reduction by enabling consumers to understand and reduce their energy consumption.

**Rationale**: The smart metering programme is partially justified by its contribution to Net Zero targets. Quantified carbon savings strengthen the case for continued investment. Addresses goal G-7.

**Success Criteria**:
- Carbon savings calculated and reported annually using grid carbon intensity data
- Consumer engagement with carbon footprint features tracked
- Annual report to Climate Change Committee from Year 2

**Priority**: SHOULD_HAVE

**Stakeholder**: DESNZ Minister (SD-1), DESNZ SRO (SD-2)

**Traces To**: Goal G-7, Outcome O-1

---

## Functional Requirements

### User Personas

#### Persona 1: Sarah — Cost-Conscious Family

- **Role**: Homeowner, dual-fuel smart meter, credit payment
- **Goals**: Understand monthly energy costs, find ways to reduce bills, compare tariffs
- **Pain Points**: Energy bill confusing, doesn't know what uses most energy, IHD too basic
- **Technical Proficiency**: Medium (uses smartphone daily, comfortable with apps)
- **Meter Type**: SMETS2 (electricity + gas)

#### Persona 2: James — Eco-Conscious Renter

- **Role**: Private renter, electricity-only smart meter, switching frequently
- **Goals**: Minimise carbon footprint, find greenest tariff, understand usage patterns
- **Pain Points**: Previous supplier app lost data on switch, wants consistent view across suppliers
- **Technical Proficiency**: High (tech-savvy, expects good UX)
- **Meter Type**: SMETS1 (electricity only, migrated meter)

#### Persona 3: Margaret — Digitally Cautious Pensioner

- **Role**: Homeowner, prepayment meter, living alone on fixed income
- **Goals**: Avoid running out of credit, keep warm affordably, understand if she's overpaying
- **Pain Points**: IHD numbers meaningless, worried about data privacy, small screen difficult
- **Technical Proficiency**: Low (has smartphone via family, limited app experience)
- **Meter Type**: SMETS2 prepayment (electricity + gas)

#### Persona 4: Aisha — Accessibility User

- **Role**: Homeowner, visual impairment, uses VoiceOver on iPhone
- **Goals**: Understand energy usage independently, set budget alerts, compare tariffs
- **Pain Points**: Most energy apps are inaccessible, charts don't work with screen readers
- **Technical Proficiency**: Medium (proficient with assistive technology)
- **Meter Type**: SMETS2 (electricity + gas)

---

### Use Cases

#### UC-1: Consumer Onboarding and Meter Linking

**Actor**: New consumer (all personas)

**Preconditions**:
- Consumer has a smart meter installed (SMETS1 or SMETS2)
- Consumer has a smartphone with iOS 15+ or Android 10+
- Consumer has downloaded the app from the App Store or Google Play

**Main Flow**:
1. Consumer opens app and views value proposition (estimated savings, data security assurances)
2. Consumer creates account using email or government identity service
3. System sends verification code to consumer's email/phone
4. Consumer verifies identity
5. Consumer enters their energy supplier and meter serial number (or scans QR code from IHD/bill)
6. System validates meter exists via DCC/supplier lookup
7. System requests consumer consent for data access (granular: viewing, recommendations, tariff comparison, research)
8. Consumer grants consent
9. System initiates meter data retrieval via DCC or supplier API
10. System displays initial consumption data within 24 hours
11. Consumer sees personalised dashboard with first insights

**Postconditions**:
- Consumer account created and verified
- Smart meter linked to consumer account
- Consent recorded with timestamp and scope
- Historical data retrieval initiated

**Alternative Flows**:
- **Alt 5a**: Consumer doesn't know meter serial number — system offers lookup via supplier account number or postcode
- **Alt 6a**: Meter not found — system shows troubleshooting guidance and support contact
- **Alt 9a**: SMETS1 meter — system routes data request to supplier API instead of DCC

**Exception Flows**:
- **Ex 1**: DCC/supplier API unavailable — system informs consumer and schedules retry, shows estimated wait time
- **Ex 2**: Consumer denies consent — system explains which features require consent and allows partial consent

**Business Rules**:
- Consumer must explicitly consent before any meter data is retrieved
- Meter ownership must be verified (consumer is the account holder at that address)
- Maximum 3 meters linkable per consumer account (electricity + gas + secondary)

**Priority**: CRITICAL

---

#### UC-2: View Energy Consumption Dashboard

**Actor**: Authenticated consumer (all personas)

**Preconditions**:
- Consumer has linked at least one smart meter
- Consumption data has been retrieved

**Main Flow**:
1. Consumer opens app (cached data displayed immediately)
2. System shows summary dashboard: today's usage, this week, this month
3. Consumer views electricity and gas usage displayed in kWh and estimated cost (£)
4. Consumer switches between daily, weekly, monthly, and annual views
5. System shows consumption trends with comparison to previous periods
6. Consumer taps on a specific day to see half-hourly breakdown
7. System displays half-hourly bar chart with accessible data table alternative

**Postconditions**:
- Consumer has viewed their energy consumption data
- View event logged for analytics (no PII)

**Alternative Flows**:
- **Alt 1a**: No network — system shows cached data with "Last updated: [timestamp]" indicator
- **Alt 3a**: Gas data in m³ — system converts to kWh using standard calorific value and displays in kWh

**Priority**: CRITICAL

---

#### UC-3: Receive Energy-Saving Recommendations

**Actor**: Authenticated consumer (Sarah, James, Margaret)

**Preconditions**:
- At least 2 weeks of consumption data available
- Consumer has consented to recommendation features

**Main Flow**:
1. System analyses consumption patterns (peak usage times, baseline load, heating patterns)
2. System generates personalised recommendations based on usage profile
3. Consumer views recommendations ranked by estimated savings (£ per year)
4. Consumer marks recommendations as "done", "not relevant", or "save for later"
5. System tracks which recommendations are acted upon

**Business Rules**:
- Recommendations must be actionable and specific (not generic advice)
- Estimated savings must be based on the consumer's actual data, not averages
- Recommendations refreshed monthly as more data accumulates

**Priority**: HIGH

---

#### UC-4: Compare Tariffs

**Actor**: Authenticated consumer (Sarah, James)

**Preconditions**:
- At least 3 months of consumption data available
- Consumer has consented to tariff comparison features
- Tariff data sourced from authoritative provider

**Main Flow**:
1. Consumer navigates to tariff comparison section
2. System calculates estimated annual cost on current tariff using actual consumption
3. System shows alternative tariffs with estimated annual cost based on actual half-hourly usage
4. Consumer compares tariffs sorted by estimated cost or green energy credentials
5. Consumer can see how much they would save (or spend more) on each tariff
6. System provides link to supplier website for switching (does not switch within app — Phase 2)

**Business Rules**:
- Tariff comparison methodology must be Ofgem-endorsed and transparent
- All available tariffs shown impartially — no supplier preference or commercial bias
- Comparison uses actual half-hourly data, not estimated annual consumption
- Tariff data refreshed at least weekly

**Priority**: MUST_HAVE

---

#### UC-5: Set and Monitor Budget Alerts

**Actor**: Authenticated consumer (Sarah, Margaret)

**Preconditions**:
- Smart meter linked and data available

**Main Flow**:
1. Consumer sets a monthly energy budget (£ or kWh)
2. System tracks consumption against budget in real-time
3. System sends push notification at 50%, 75%, and 90% of budget
4. Consumer views budget progress on dashboard
5. At month end, system shows actual vs budget with variance explanation

**Alternative Flows**:
- **Alt 1a**: Prepayment consumer — system shows remaining credit instead of budget, with low-credit alerts

**Priority**: SHOULD_HAVE

---

#### UC-6: Prepayment Meter Management

**Actor**: Margaret (prepayment meter consumer)

**Preconditions**:
- Consumer has a prepayment smart meter linked

**Main Flow**:
1. Consumer views current credit balance on dashboard
2. System shows estimated days of credit remaining based on recent usage
3. System sends push notification when credit falls below configurable threshold
4. Consumer views top-up history and consumption since last top-up
5. System provides nearest top-up location or online top-up link (supplier-dependent)

**Business Rules**:
- Credit balance data subject to DCC/supplier API availability
- Low credit alerts default to £5 remaining, configurable by consumer
- Emergency credit status displayed if applicable

**Priority**: MUST_HAVE

---

#### UC-7: Manage Data Consent

**Actor**: All consumers

**Preconditions**:
- Consumer has an active account

**Main Flow**:
1. Consumer navigates to privacy settings
2. System displays current consent status for each data use (viewing, recommendations, tariff comparison, research)
3. Consumer toggles individual consents on or off
4. System confirms change and explains feature impact ("Turning off recommendations consent will disable personalised tips")
5. If consent withdrawn, system stops processing for that purpose and schedules data deletion per retention policy
6. All consent changes recorded with timestamp

**Business Rules**:
- Consent withdrawal must take effect immediately for new processing
- Data deletion for withdrawn consent completed within 30 days
- Consumer can export their data before deletion (right to portability)
- Consent record retained for audit even after consent withdrawn (legal requirement)

**Priority**: MUST_HAVE

---

#### UC-8: Delete Account and Data

**Actor**: All consumers

**Preconditions**:
- Consumer has an active account

**Main Flow**:
1. Consumer requests account deletion from settings
2. System explains what will be deleted and what will be retained (audit logs)
3. Consumer confirms deletion
4. System deletes personal data, consumption data, and consent records (except audit trail)
5. System confirms deletion within 30 days per UK GDPR Article 17
6. Consumer receives email confirmation of deletion

**Business Rules**:
- Audit logs retained for 7 years per SEC and ICO requirements (anonymised)
- Deletion is irreversible — consumer informed before confirmation
- Subject Access Request (SAR) process available for data portability before deletion

**Priority**: MUST_HAVE

---

### Functional Requirements Detail

#### FR-001: Consumer Account Registration

**Description**: The system MUST allow consumers to create an account using email address with verification, supporting multi-factor authentication.

**Relates To**: BR-001, UC-1

**Acceptance Criteria**:
- [ ] Given a consumer with a valid email address, when they register, then they receive a verification code within 60 seconds
- [ ] Given a consumer completing registration, when they set up MFA, then they can use authenticator app or SMS
- [ ] Given a consumer with an existing account for the same email, when they try to register, then they are directed to sign-in

**Priority**: MUST_HAVE
**Complexity**: MEDIUM
**Dependencies**: None

---

#### FR-002: Smart Meter Discovery and Linking

**Description**: The system MUST enable consumers to discover and link their smart meter(s) using meter serial number (MPAN for electricity, MPRN for gas), supplier account number, or postcode-based lookup.

**Relates To**: BR-001, UC-1

**Acceptance Criteria**:
- [ ] Given a valid MPAN/MPRN, when the consumer submits it, then the system verifies the meter exists via DCC or supplier lookup within 10 seconds
- [ ] Given a consumer who doesn't know their meter serial number, when they enter their supplier account number and postcode, then the system looks up the associated meter(s)
- [ ] Given a SMETS1 meter, when detected, then the system routes data requests to the appropriate supplier API
- [ ] Given a SMETS2 meter, when detected, then the system routes data requests to DCC

**Priority**: MUST_HAVE
**Complexity**: HIGH
**Dependencies**: INT-001 (DCC integration), INT-002 (Supplier APIs)

---

#### FR-003: Granular Consent Management

**Description**: The system MUST provide granular consent controls allowing consumers to independently consent to or withdraw consent from each data processing purpose: data viewing, personalised recommendations, tariff comparison, and anonymised research sharing.

**Relates To**: BR-003, UC-7

**Acceptance Criteria**:
- [ ] Given a new consumer, when they complete onboarding, then they are presented with each consent purpose independently with clear plain-English explanations
- [ ] Given a consumer who withdraws consent for a specific purpose, when the change is saved, then processing for that purpose stops immediately and data deletion is scheduled
- [ ] Given any consent change, when it occurs, then the change is recorded with timestamp, scope, and audit trail

**Priority**: MUST_HAVE
**Complexity**: MEDIUM
**Dependencies**: DR-003 (Consent data model)

---

#### FR-004: Half-Hourly Consumption Data Retrieval

**Description**: The system MUST retrieve half-hourly electricity and gas consumption data from smart meters via DCC (SMETS2) and energy supplier APIs (SMETS1), making data available to consumers within 24 hours of the meter reading.

**Relates To**: BR-001, UC-2

**Acceptance Criteria**:
- [ ] Given a linked SMETS2 meter, when DCC processes the data request, then half-hourly readings are ingested within the DCC SLA window
- [ ] Given a linked SMETS1 meter, when the supplier API is queried, then available consumption data is retrieved within the supplier SLA
- [ ] Given successfully retrieved data, when a consumer opens the app, then yesterday's data is visible within 24 hours of the meter reading
- [ ] Given missing readings, when data gaps exist, then the system flags gaps to the consumer with an explanation

**Priority**: MUST_HAVE
**Complexity**: HIGH
**Dependencies**: INT-001, INT-002

---

#### FR-005: Energy Consumption Dashboard

**Description**: The system MUST display energy consumption data with daily, weekly, monthly, and annual views showing usage in kWh and estimated cost in £, with comparison to previous periods.

**Relates To**: BR-001, BR-002, UC-2

**Acceptance Criteria**:
- [ ] Given consumption data exists, when the consumer opens the dashboard, then they see today's usage, this week, and this month summaries
- [ ] Given half-hourly data, when the consumer taps on a specific day, then they see a half-hourly breakdown
- [ ] Given gas data in m³, when displayed, then it is converted to kWh using standard calorific value
- [ ] Given a screen reader is active, when viewing the dashboard, then all data is accessible via text alternatives and data tables
- [ ] Given no network connection, when the consumer opens the app, then cached data is displayed with a freshness indicator

**Priority**: MUST_HAVE
**Complexity**: HIGH
**Dependencies**: FR-004, DR-001

---

#### FR-006: Personalised Energy-Saving Recommendations

**Description**: The system MUST generate personalised energy-saving recommendations based on the consumer's actual consumption patterns, with estimated savings in £ per year.

**Relates To**: BR-002, UC-3

**Acceptance Criteria**:
- [ ] Given at least 2 weeks of consumption data, when the recommendation engine runs, then at least 3 personalised recommendations are generated
- [ ] Given a recommendation, when displayed, then it shows estimated annual savings in £ based on the consumer's actual consumption
- [ ] Given generic recommendations identical for all users, when reviewed, then they are rejected — recommendations must be personalised
- [ ] Given the consumer has not consented to recommendations, when they view the recommendations section, then they see an explanation and consent prompt

**Priority**: MUST_HAVE
**Complexity**: HIGH
**Dependencies**: FR-004, FR-003

---

#### FR-007: Tariff Comparison

**Description**: The system MUST calculate and display estimated annual costs for available energy tariffs using the consumer's actual half-hourly consumption data, presented impartially.

**Relates To**: BR-002, UC-4

**Acceptance Criteria**:
- [ ] Given at least 3 months of consumption data, when the consumer views tariff comparison, then estimated annual cost is calculated for all available tariffs using their actual half-hourly profile
- [ ] Given tariff results, when displayed, then they are sorted by estimated annual cost by default with option to sort by green credentials
- [ ] Given tariff comparison, when examined for bias, then no supplier is preferentially positioned — ordering is strictly by calculated cost or consumer-selected sort
- [ ] Given tariff data, when checked, then it is no more than 7 days old

**Priority**: MUST_HAVE
**Complexity**: HIGH
**Dependencies**: FR-004, INT-003, DR-005

---

#### FR-008: Consumption Alerts and Notifications

**Description**: The system MUST send configurable push notifications for consumption alerts including budget thresholds, unusual usage, and prepayment low credit.

**Relates To**: BR-002, UC-5, UC-6

**Acceptance Criteria**:
- [ ] Given a consumer has set a monthly budget, when consumption reaches 50%, 75%, and 90% thresholds, then a push notification is sent
- [ ] Given an unusual consumption spike (>2x daily average), when detected, then an alert is sent within 4 hours
- [ ] Given a prepayment meter with credit below the configured threshold, when detected, then a low-credit alert is sent
- [ ] Given a consumer has disabled notifications, when an alert triggers, then no notification is sent

**Priority**: SHOULD_HAVE
**Complexity**: MEDIUM
**Dependencies**: FR-004, FR-005

---

#### FR-009: Prepayment Meter Support

**Description**: The system MUST display prepayment meter credit balance, estimated days remaining, top-up history, and low-credit alerts for consumers with prepayment smart meters.

**Relates To**: BR-005, UC-6

**Acceptance Criteria**:
- [ ] Given a linked prepayment meter, when the consumer views the dashboard, then current credit balance is displayed prominently
- [ ] Given current credit and recent daily usage, when calculated, then estimated days of credit remaining is displayed
- [ ] Given credit below configurable threshold (default £5), when detected, then a push notification is sent
- [ ] Given prepayment top-up history, when requested, then the last 6 months of top-ups are displayed with amounts and dates

**Priority**: MUST_HAVE
**Complexity**: MEDIUM
**Dependencies**: INT-001, INT-002

---

#### FR-010: Data Export and Portability

**Description**: The system MUST allow consumers to export their consumption data and personal data in machine-readable formats (CSV, JSON) to support UK GDPR right to portability.

**Relates To**: BR-003, UC-8

**Acceptance Criteria**:
- [ ] Given a consumer requests data export, when processed, then they receive a download within 24 hours
- [ ] Given exported consumption data, when opened, then it is in CSV or JSON format with documented schema
- [ ] Given a Subject Access Request, when received, then all personal data is compiled and delivered within 30 days

**Priority**: MUST_HAVE
**Complexity**: LOW
**Dependencies**: DR-001, DR-002

---

#### FR-011: Multi-Meter Support

**Description**: The system MUST support consumers with multiple meters (electricity + gas, or multiple properties) and display consumption data for each meter independently and as an aggregate.

**Relates To**: BR-001

**Acceptance Criteria**:
- [ ] Given a consumer with electricity and gas meters, when viewing the dashboard, then they can see each fuel independently or combined
- [ ] Given a consumer with meters at multiple addresses, when linked, then each address is shown separately
- [ ] Given a maximum of 3 linked meters per account, when a 4th is attempted, then the system informs the consumer and offers support

**Priority**: MUST_HAVE
**Complexity**: MEDIUM
**Dependencies**: FR-002

---

#### FR-012: Carbon Footprint Display

**Description**: The system SHOULD display the carbon footprint associated with the consumer's energy consumption, using real-time grid carbon intensity data.

**Relates To**: BR-007

**Acceptance Criteria**:
- [ ] Given electricity consumption data, when carbon footprint is displayed, then it uses National Grid ESO carbon intensity data for the consumer's region
- [ ] Given the consumer views their monthly summary, when carbon data is shown, then it includes kg CO2e and comparison to UK household average
- [ ] Given carbon data, when viewed by screen reader, then a text summary is available

**Priority**: SHOULD_HAVE
**Complexity**: MEDIUM
**Dependencies**: FR-004, INT-004

---

#### FR-013: IHD Data Synchronisation

**Description**: The system SHOULD synchronise with In-Home Display data where available to provide immediate consumption readings alongside the half-hourly historical data.

**Relates To**: BR-001

**Acceptance Criteria**:
- [ ] Given a consumer with a SMETS2 IHD, when IHD data is available via DCC, then near-real-time readings supplement the half-hourly batch data
- [ ] Given IHD data and half-hourly data, when displayed, then the data sources are clearly distinguished with appropriate freshness labels

**Priority**: SHOULD_HAVE
**Complexity**: HIGH
**Dependencies**: INT-001

---

#### FR-014: Offline Mode

**Description**: The system MUST provide offline access to previously retrieved consumption data, cached recommendations, and cached tariff comparisons, with clear freshness indicators.

**Relates To**: BR-004, BR-005

**Acceptance Criteria**:
- [ ] Given no network connection, when the consumer opens the app, then the most recently cached dashboard, history, and recommendations are displayed
- [ ] Given offline mode, when the consumer views data, then a visible "Last updated: [timestamp]" indicator is shown
- [ ] Given the consumer returns online, when data syncs, then the display updates automatically without manual refresh

**Priority**: MUST_HAVE
**Complexity**: MEDIUM
**Dependencies**: FR-005

---

#### FR-015: In-App Feedback and Support

**Description**: The system MUST provide in-app feedback submission and help content, with escalation paths for data access issues.

**Relates To**: BR-004, BR-005

**Acceptance Criteria**:
- [ ] Given a consumer needs help, when they tap the help button, then contextual help is displayed
- [ ] Given a consumer wants to report an issue, when they submit feedback, then it is captured with app version, device type, and optional screenshot (no PII auto-collected)
- [ ] Given a data access issue (meter not found, data not loading), when encountered, then specific troubleshooting guidance is shown with escalation to DCC/supplier support

**Priority**: SHOULD_HAVE
**Complexity**: LOW
**Dependencies**: None

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-001: Mobile App Response Time

**Requirement**:
- App launch to usable dashboard: < 3 seconds on mid-range device (e.g., 2023-era Android, £150-£200) over 4G
- Dashboard data render (from cache): < 1 second
- Dashboard data refresh (from backend): < 5 seconds
- Half-hourly detail view load: < 2 seconds
- Screen navigation transitions: < 300ms

**Measurement Method**: Automated performance testing on representative device matrix; real-user monitoring in production

**Load Conditions**:
- Peak concurrent users: 500,000 (morning/evening peaks, energy price cap announcement days)
- Average daily active users: 2 million (at steady state)
- Peak API requests: 10,000 per second

**Priority**: MUST_HAVE

**Traces To**: Goal G-1, Goal G-4, Principle 13 (Performance)

---

#### NFR-P-002: Backend API Response Time

**Requirement**:
- Platform API response time: p50 < 200ms, p95 < 500ms, p99 < 1,000ms
- Data ingestion pipeline: Half-hourly batch processing completed within 4-hour window
- Recommendation engine: Results generated within 30 seconds of request
- Tariff comparison calculation: < 10 seconds for a 12-month profile

**Measurement Method**: Application Performance Monitoring (APM) in production; synthetic monitoring from UK locations

**Priority**: MUST_HAVE

**Traces To**: Goal G-1, Principle 13 (Performance)

---

#### NFR-P-003: Mobile App Resource Efficiency

**Requirement**:
- App download size: < 50 MB (iOS and Android)
- Background data usage: < 10 MB per day
- Battery impact: < 2% daily battery drain from background activity
- On-device storage: < 200 MB for 12 months of cached consumption data

**Measurement Method**: App store size reporting; device-level monitoring during testing

**Priority**: SHOULD_HAVE

**Traces To**: Goal G-1 (adoption — resource-constrained devices), Principle 13

---

### Availability and Resilience Requirements

#### NFR-A-001: Platform Availability

**Requirement**: Backend platform services MUST achieve 99.9% uptime (43.8 minutes maximum unplanned downtime per month), measured on a rolling 30-day basis.

**Maintenance Windows**: Planned maintenance permitted between 02:00-05:00 GMT, maximum 4 hours per month, with 72 hours advance notice.

**Priority**: MUST_HAVE

**Traces To**: Goal G-1, Principle 14 (Availability), Principle 3 (Resilience)

---

#### NFR-A-002: Disaster Recovery

**RPO**: Zero data loss for confirmed consumption readings (all ingested data must be durably stored before acknowledgement)

**RTO**: 1 hour for platform services; 4 hours for non-critical services (recommendation engine, tariff comparison)

**Backup Requirements**:
- Continuous replication for consumption data
- Daily backups for all other data
- Backup retention: 90 days for operational backups; 7 years for audit data
- Backups stored in a separate UK availability zone

**Failover Requirements**:
- Automatic failover to secondary availability zone: YES
- Failover time: < 5 minutes for stateless services, < 15 minutes for stateful services

**Priority**: MUST_HAVE

**Traces To**: Principle 14 (Availability), Principle 3 (Resilience)

---

#### NFR-A-003: Fault Tolerance and Graceful Degradation

**Requirement**: The system MUST gracefully degrade when external dependencies fail. Consumers MUST always be able to view cached consumption data even when DCC, supplier APIs, or recommendation services are unavailable.

**Degradation Hierarchy** (in order of criticality):
1. **Core**: Authentication, cached data viewing — always available
2. **Important**: Data refresh, alerts — degraded if backend unavailable
3. **Enhanced**: Recommendations, tariff comparison — disabled if services down
4. **Optional**: Carbon footprint, IHD sync — disabled if external APIs down

**Resilience Patterns Required**:
- [ ] Circuit breakers for DCC and supplier API calls (trip after 5 consecutive failures, retry after 60 seconds)
- [ ] Retry with exponential backoff (initial 1s, max 60s, max 5 retries)
- [ ] Timeout on all network calls (API calls: 10s, data ingestion: 60s)
- [ ] Bulkhead isolation between DCC integration, supplier integrations, and consumer-facing APIs
- [ ] Mobile app offline-first architecture with local data cache

**Priority**: MUST_HAVE

**Traces To**: Principle 3 (Resilience), Principle 11 (Loose Coupling)

---

### Scalability Requirements

#### NFR-S-001: Horizontal Scaling

**Requirement**: All platform components MUST support horizontal scaling without code changes or downtime.

**Growth Projections**:
- Year 1: 5 million MAU, 500,000 peak concurrent, 100 million consumption readings/day
- Year 2: 10 million MAU, 1 million peak concurrent, 200 million consumption readings/day
- Year 3: 15 million MAU, 1.5 million peak concurrent, 300 million consumption readings/day

**Scaling Triggers**: Auto-scale when CPU > 70% or request queue depth > threshold (component-specific)

**Priority**: MUST_HAVE

**Traces To**: Principle 2 (Scalability)

---

#### NFR-S-002: Data Volume Scaling

**Requirement**: The platform MUST handle data growth to 50 TB within 3 years, with automated data lifecycle management.

**Data Volume Projections**:
- Year 1: ~10 TB (5M users × 48 readings/day × 2 fuels × 365 days)
- Year 2: ~25 TB (cumulative)
- Year 3: ~50 TB (cumulative)

**Data Archival Strategy**:
- Hot storage: Last 3 months of half-hourly data (fast query)
- Warm storage: 3-24 months (query within seconds)
- Cold storage: 24+ months (query within minutes, for SAR and dispute resolution)
- Deletion: Per consent and retention policy

**Priority**: MUST_HAVE

**Traces To**: Principle 2 (Scalability), Principle 8 (Data Sovereignty)

---

### Security Requirements

#### NFR-SEC-001: Consumer Authentication

**Requirement**: All consumers MUST authenticate via secure, industry-standard mechanisms with multi-factor authentication.

**Authentication Requirements**:
- Email + password with enforced complexity (NCSC guidance: minimum 8 characters, no arbitrary complexity rules, breach password check)
- MFA: Authenticator app (primary) or SMS (fallback). Biometric (Face ID, fingerprint) as device-level convenience factor
- Social sign-in: NOT supported (government service — no dependency on commercial identity providers)

**Session Management**:
- Session timeout: 30 minutes of inactivity
- Absolute session timeout: 12 hours
- Re-authentication required for: consent changes, data deletion, account modification
- Session tokens: Opaque, short-lived, rotated on each request

**Priority**: MUST_HAVE

**Traces To**: Principle 5 (Security by Design), BR-003

---

#### NFR-SEC-002: Authorisation and Access Control

**Requirement**: Role-based access control with strict enforcement — consumers can only access their own data; no consumer can access another's consumption data.

**Access Control Rules**:
- Consumer: Read own consumption data, manage own consent, export own data
- System admin: Operational access only (no consumer data access without explicit authorisation and audit)
- Support staff: View consumer account metadata (name, email, linked meters) only with consumer-initiated support request and audit logging
- DCC/Supplier APIs: Service-to-service authentication, scoped to authorised data access per consumer consent

**Priority**: MUST_HAVE

**Traces To**: Principle 5 (Security by Design)

---

#### NFR-SEC-003: Data Encryption

**Requirement**: All data MUST be encrypted in transit and at rest. No plaintext storage of personal or consumption data.

**Encryption Standards**:
- Data in transit: TLS 1.2+ (prefer 1.3) with strong cipher suites for all communications
- Data at rest: AES-256 or equivalent for all data stores containing personal or consumption data
- Mobile app local storage: Encrypted using platform-native secure storage (iOS Keychain, Android Keystore)
- Key management: Managed key service with automatic rotation (90-day cycle)

**Encryption Scope**:
- [ ] Database encryption at rest (all tables containing personal/consumption data)
- [ ] Backup encryption (all backups)
- [ ] Object/file storage encryption
- [ ] Mobile app local cache encryption
- [ ] DCC/supplier API communication (mutual TLS where supported)

**Priority**: MUST_HAVE

**Traces To**: Principle 5 (Security by Design)

---

#### NFR-SEC-004: Secrets Management

**Requirement**: No secrets (API keys, database passwords, encryption keys, DCC certificates) in source code, configuration files, or mobile app bundles. Ever.

**Requirements**:
- All secrets stored in a managed secrets vault
- Secrets rotated automatically on defined schedule
- Mobile app: No embedded secrets; use OAuth token exchange patterns
- Build pipeline: Secrets injected at deployment time, never committed
- DCC security certificates: Managed per SEC requirements

**Priority**: MUST_HAVE

**Traces To**: Principle 5 (Security by Design)

---

#### NFR-SEC-005: Vulnerability Management

**Requirement**: Continuous vulnerability management across all components including mobile app, backend services, and third-party dependencies.

**Security Testing**:
- SAST (static analysis) in CI/CD pipeline — zero critical findings before merge
- DAST (dynamic analysis) against staging environment — weekly
- Dependency scanning (SCA) in CI/CD — no known critical/high vulnerabilities in production
- Penetration testing: Annual by external firm, including mobile app (OWASP MASVS)
- Mobile-specific: App binary analysis, certificate pinning validation, reverse engineering resistance

**Remediation SLAs**:
- Critical: 24 hours
- High: 7 days
- Medium: 30 days
- Low: 90 days

**Priority**: MUST_HAVE

**Traces To**: Principle 5 (Security by Design), BR-003

---

#### NFR-SEC-006: Mobile App Security

**Requirement**: The mobile application MUST implement platform-specific security controls to protect consumer data on-device and resist common mobile attack vectors.

**Mobile Security Requirements**:
- [ ] Certificate pinning for all API communications
- [ ] Root/jailbreak detection with appropriate response (warn, not block)
- [ ] No sensitive data in app logs or crash reports
- [ ] Secure local storage using platform keychain/keystore
- [ ] No third-party analytics SDKs that transmit PII
- [ ] App transport security enforced (no HTTP, no weak TLS)
- [ ] Obfuscation of app binary to resist reverse engineering

**Priority**: MUST_HAVE

**Traces To**: Principle 5 (Security by Design)

---

### Compliance and Regulatory Requirements

#### NFR-C-001: UK GDPR and Data Protection Act 2018

**Requirement**: Full compliance with UK GDPR including all data subject rights, privacy by design, and lawful basis for each processing activity.

**Compliance Requirements**:
- [ ] Lawful basis identified and documented for each processing activity (consent for data viewing, recommendations, tariff comparison, research sharing; legitimate interest for service operation and security)
- [ ] Privacy notice in plain English, accessible, and prominently displayed
- [ ] Right of access (Article 15): SAR response within 30 days
- [ ] Right to rectification (Article 16): Correct inaccurate personal data
- [ ] Right to erasure (Article 17): Delete account and data within 30 days
- [ ] Right to data portability (Article 20): Export in machine-readable format
- [ ] Right to object (Article 21): Opt out of specific processing
- [ ] Data breach notification to ICO within 72 hours, consumer notification without undue delay
- [ ] DPIA completed and maintained as living document

**Data Residency**: All personal and consumption data stored in UK data centres only

**Data Retention**:
- Active account consumption data: Duration of account plus 12 months
- Deleted account: Personal data deleted within 30 days; anonymised audit logs retained 7 years
- Consent records: 7 years (for regulatory audit)

**Priority**: MUST_HAVE

**Traces To**: BR-003, Principle 7 (Privacy by Design), Principle 8 (Data Sovereignty)

---

#### NFR-C-002: Smart Energy Code (SEC) Compliance

**Requirement**: All interactions with DCC infrastructure and smart meter data MUST comply with the Smart Energy Code technical and security requirements.

**SEC Requirements**:
- [ ] Authorised third-party status obtained under SEC (or operating under DCC user status)
- [ ] SEC security controls implemented for DCC-facing integration
- [ ] Consumer consent obtained per SEC data access provisions
- [ ] DCC interface specifications followed for data retrieval
- [ ] SEC governance and change management processes followed

**Priority**: MUST_HAVE

**Traces To**: BR-003, INT-001

---

#### NFR-C-003: Ofgem Data Access Framework

**Requirement**: Consumer data access, consent, and tariff comparison MUST align with Ofgem's regulatory framework for third-party energy data access.

**Ofgem Requirements**:
- [ ] Consumer consent mechanism aligned with Ofgem guidance
- [ ] Tariff comparison methodology transparent and non-discriminatory
- [ ] Vulnerable consumer protections in place
- [ ] Complaint handling process established per Ofgem expectations
- [ ] Regular reporting to Ofgem on data access volumes and consumer protection metrics

**Priority**: MUST_HAVE

**Traces To**: BR-003, Goal G-3

---

#### NFR-C-004: Audit Logging

**Requirement**: Comprehensive, tamper-evident audit trail for all security-relevant and consent-related events.

**Audit Log Contents**:
- Who: User ID or service identity (no PII in log entries — use opaque identifiers)
- What: Action performed (login, consent change, data access, export, deletion)
- When: UTC timestamp, millisecond precision
- Where: Component and endpoint
- Why: Correlation ID linking to user session or batch job
- Result: Success/failure with error classification

**Log Retention**: 7 years for compliance logs (immutable storage, append-only)

**Log Integrity**: Cryptographic hash chain for tamper evidence

**Priority**: MUST_HAVE

**Traces To**: Principle 6 (Observability), NFR-C-001, NFR-C-002

---

#### NFR-C-005: GDS Service Standard

**Requirement**: The service MUST pass GDS Service Standard assessment at each phase gate (Alpha, Beta, Live) across all 14 points.

**Key Evidence Requirements**:
- Point 1: User research with real energy consumers at every phase
- Point 5: WCAG 2.2 AA compliance with assistive technology testing
- Point 9: Security assessment by NCSC
- Point 12: Source code published in the open (or documented exception)
- Point 13: Open standards used for APIs and data formats
- Point 14: SLOs defined and monitored; operational runbooks in place

**Priority**: MUST_HAVE

**Traces To**: BR-003, Goal G-3, Principle 20 (GDS Service Standard)

---

### Usability Requirements

#### NFR-U-001: Accessibility — WCAG 2.2 AA

**Requirement**: All consumer-facing screens and features MUST meet WCAG 2.2 Level AA. Energy data visualisations MUST have accessible alternatives.

**Accessibility Requirements**:
- [ ] All content perceivable by screen readers (VoiceOver on iOS, TalkBack on Android)
- [ ] Charts/graphs have text alternatives and accessible data tables
- [ ] Colour never the sole means of conveying information
- [ ] Touch targets minimum 44×44 CSS pixels
- [ ] Dynamic text sizing support (up to 200%)
- [ ] High contrast mode supported
- [ ] Keyboard/switch navigation on mobile
- [ ] Plain English — energy jargon avoided or explained with contextual help
- [ ] Accessibility statement published and maintained

**Testing**: Automated WCAG audit in CI/CD pipeline + manual testing with assistive technology + user testing with consumers who have access needs

**Priority**: MUST_HAVE

**Traces To**: BR-005, Goal G-5, Principle 15 (Accessibility)

---

#### NFR-U-002: Language and Localisation

**Requirement**: The app MUST be in English (UK). Welsh language support SHOULD be provided for consumers in Wales.

**Localisation Requirements**:
- [ ] All UI text in British English
- [ ] Welsh language option for consumers who select Wales as their location
- [ ] Date format: DD/MM/YYYY
- [ ] Currency: £ (GBP)
- [ ] Units: kWh, m³ (gas volume), £/kWh

**Priority**: English: MUST_HAVE; Welsh: SHOULD_HAVE

---

### Maintainability and Supportability Requirements

#### NFR-M-001: Observability

**Requirement**: Comprehensive telemetry for all platform components. Telemetry MUST NOT contain PII or consumption data.

**Telemetry Requirements**:
- **Logging**: Structured JSON logs with correlation IDs; PII-free
- **Metrics**: Request rate, error rate, latency distribution per endpoint and integration
- **Tracing**: Distributed traces across platform services and external integrations
- **Dashboards**: Real-time operational dashboards for each service tier
- **Alerting**: SLO-based alerts with actionable runbooks; PagerDuty or equivalent integration

**Business Metrics** (also via telemetry):
- Daily active users, meter linkage rate, recommendation engagement, tariff comparison usage
- DCC/supplier API success rates and latency per supplier
- Data freshness (time from meter reading to consumer visibility)

**Priority**: MUST_HAVE

**Traces To**: Principle 6 (Observability)

---

#### NFR-M-002: Operational Runbooks

**Requirement**: Runbooks for all anticipated operational scenarios, maintained alongside code.

**Runbook Coverage**:
- [ ] Deployment and rollback procedures
- [ ] Backup and restore procedures
- [ ] DCC integration failure response
- [ ] Supplier API degradation response
- [ ] Consumer data breach incident response (including ICO notification procedure)
- [ ] Scaling procedures (manual override if auto-scaling fails)
- [ ] DR failover and failback procedures

**Priority**: MUST_HAVE

**Traces To**: Principle 6 (Observability), Principle 14 (Availability)

---

### Portability and Interoperability Requirements

#### NFR-I-001: API Standards

**Requirement**: All platform APIs MUST be documented using open specifications with versioning and backward compatibility.

**API Design Principles**:
- RESTful design with standard HTTP methods (or GraphQL where appropriate)
- JSON request/response format
- API versioning via URL path (e.g., /v1/, /v2/)
- Consistent error response format with machine-readable error codes
- OpenAPI 3.0 specification published for all APIs
- AsyncAPI specification for event-driven interfaces

**Priority**: MUST_HAVE

**Traces To**: Principle 4 (Interoperability), Principle 21 (Open Source and Reuse)

---

#### NFR-I-002: Platform Independence

**Requirement**: The backend platform MUST avoid vendor lock-in through use of open standards, containerisation, and infrastructure as code. Migration to a different cloud provider SHOULD be achievable within 6 months.

**Requirements**:
- [ ] Containerised workloads using open standards
- [ ] Infrastructure defined as code in version control
- [ ] No proprietary cloud services for core business logic (managed databases acceptable with abstraction)
- [ ] Data export capability for all platform data in open formats

**Priority**: SHOULD_HAVE

**Traces To**: Principle 16 (Maintainability), Principle 17 (Infrastructure as Code), Principle 21 (Open Source)

---

## Integration Requirements

### INT-001: Integration with DCC (Data Communications Company)

**Purpose**: Retrieve SMETS2 smart meter half-hourly consumption data for linked consumers

**Integration Type**: Batch API (scheduled data retrieval) + on-demand lookup (meter validation)

**Data Exchanged**:
- **To DCC**: Meter data requests (MPAN/MPRN, date range, consumer consent reference)
- **From DCC**: Half-hourly consumption readings (kWh for electricity, m³ for gas), meter technical details, IHD data

**Integration Pattern**: Request/response for meter lookup; asynchronous batch for data retrieval aligned with DCC scheduling windows

**Authentication**: DCC-prescribed authentication (certificates, SEC-compliant security)

**Error Handling**: Circuit breaker (trip after 5 failures), retry with backoff, dead letter queue for failed requests, manual escalation for persistent failures

**SLA**: Data retrieval within DCC-defined SLA window; meter lookup < 10 seconds; 99.9% availability for scheduled batch windows

**Capacity Constraints**: Batch retrieval designed to align with DCC low-traffic windows to minimise infrastructure impact. Capacity allocation pre-agreed with DCC.

**Owner**: DCC Technical Architecture Team

**Priority**: MUST_HAVE

---

### INT-002: Integration with Energy Supplier APIs

**Purpose**: Retrieve SMETS1 consumption data and supplement SMETS2 data; meter validation and consumer verification

**Integration Type**: RESTful APIs (supplier-specific, abstracted via adapter layer)

**Data Exchanged**:
- **To Suppliers**: Data retrieval requests (account number or MPAN/MPRN, date range, consent token)
- **From Suppliers**: Half-hourly consumption data, account metadata, tariff information, prepayment balance

**Integration Pattern**: Request/response with per-supplier adapters behind a common interface

**Authentication**: OAuth 2.0 or API key (supplier-dependent); mutual TLS where supported

**Error Handling**: Per-supplier circuit breakers, retry logic, degraded mode (consumer informed if their supplier API is unavailable)

**SLA**: Supplier-dependent; target < 5 seconds for data retrieval; minimum 95% success rate per supplier

**Supplier Coverage**:
- Beta: 6 major suppliers (British Gas, EDF, E.ON, Octopus Energy, SSE, Scottish Power) covering ~80% of smart meters
- Live: 10+ suppliers covering ~90% of smart meters

**Owner**: Programme Integration Team (with supplier bilateral relationships)

**Priority**: MUST_HAVE

---

### INT-003: Integration with Tariff Data Provider

**Purpose**: Source current energy tariff information for all suppliers to enable impartial comparison

**Integration Type**: API (scheduled refresh) or data feed (daily file)

**Data Exchanged**:
- **From Provider**: All available domestic energy tariffs (unit rates, standing charges, green credentials, contract terms) across all suppliers

**Integration Pattern**: Batch ingestion (daily or more frequent); cached in platform for consumer queries

**Authentication**: API key or mutual TLS

**Error Handling**: Stale data alerting (if data > 7 days old, tariff comparison flagged as potentially outdated)

**SLA**: Data refresh within 24 hours; tariff comparison available 99.9% of the time (from cache)

**Owner**: Programme Commercial Team (source: Ofgem-endorsed data provider or direct from suppliers)

**Priority**: MUST_HAVE

---

### INT-004: Integration with National Grid ESO Carbon Intensity API

**Purpose**: Provide regional carbon intensity data for electricity to calculate consumer carbon footprint

**Integration Type**: RESTful API (real-time and forecast)

**Data Exchanged**:
- **From National Grid ESO**: Regional carbon intensity (gCO2/kWh), generation mix, forecast

**Integration Pattern**: Periodic refresh (every 30 minutes) cached in platform

**Authentication**: Public API (no authentication required)

**Error Handling**: Graceful degradation — if carbon data unavailable, carbon features hidden; no impact on core consumption features

**SLA**: Best effort (public API); cached data used if API unavailable

**Owner**: National Grid ESO (external, public API)

**Priority**: SHOULD_HAVE

---

### INT-005: Integration with Push Notification Service

**Purpose**: Deliver consumption alerts, budget notifications, and prepayment low-credit warnings to consumer devices

**Integration Type**: Platform push notification services (Apple Push Notification Service, Firebase Cloud Messaging)

**Data Exchanged**:
- **To Consumer Devices**: Alert notifications (no consumption data in notification payload — notification prompts app to fetch from backend)

**Integration Pattern**: Event-driven (alert triggers notification dispatch)

**Authentication**: Platform certificates (APNS, FCM)

**Error Handling**: Retry failed deliveries; respect consumer notification preferences

**SLA**: Notification delivery within 5 minutes of trigger event; 99% delivery rate

**Owner**: Programme Delivery Team

**Priority**: SHOULD_HAVE

---

## Data Requirements

### DR-001: Consumer Profile Entity

**Description**: Consumer account and authentication information

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| consumer_id | UUID | Yes | Unique consumer identifier | Primary key, system-generated |
| email | String(255) | Yes | Consumer email address | Unique, validated format |
| display_name | String(100) | No | Consumer's chosen name | Sanitised input |
| created_at | Timestamp | Yes | Account creation | UTC, immutable |
| last_login | Timestamp | No | Last authentication | UTC |
| status | Enum | Yes | Account status | active, suspended, deleted |
| mfa_enabled | Boolean | Yes | MFA status | Default: true |

**Data Classification**: CONFIDENTIAL
**Data Retention**: Account lifetime + 12 months; deleted within 30 days of deletion request
**Data Volume**: Year 1: 8M records (downloads > active users); Year 3: 20M records

---

### DR-002: Linked Meter Entity

**Description**: Association between consumer and their smart meter(s)

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| link_id | UUID | Yes | Unique link identifier | Primary key |
| consumer_id | UUID | Yes | Consumer reference | FK to DR-001 |
| mpan | String(21) | Conditional | Electricity meter point | Required for electricity |
| mprn | String(15) | Conditional | Gas meter point | Required for gas |
| meter_type | Enum | Yes | SMETS1 or SMETS2 | |
| payment_type | Enum | Yes | Credit or prepayment | |
| supplier_id | String(50) | Yes | Energy supplier identifier | |
| linked_at | Timestamp | Yes | When meter was linked | UTC |
| status | Enum | Yes | Link status | active, unlinked, error |

**Data Classification**: CONFIDENTIAL
**Data Retention**: Duration of active link + 12 months post-unlink
**Data Volume**: Year 1: 10M records (avg 2 meters per consumer); Year 3: 30M records

---

### DR-003: Consent Record Entity

**Description**: Consumer consent decisions for each data processing purpose

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| consent_id | UUID | Yes | Unique consent record | Primary key |
| consumer_id | UUID | Yes | Consumer reference | FK to DR-001 |
| purpose | Enum | Yes | Processing purpose | viewing, recommendations, tariff_comparison, research |
| status | Enum | Yes | Consent status | granted, withdrawn |
| granted_at | Timestamp | Conditional | When consent granted | UTC |
| withdrawn_at | Timestamp | Conditional | When consent withdrawn | UTC |
| version | String(10) | Yes | Privacy notice version consented to | |

**Data Classification**: RESTRICTED (regulatory audit requirement)
**Data Retention**: 7 years from last change (regulatory audit)
**Data Volume**: Year 1: 40M records (8M consumers × ~5 consent decisions); Year 3: 100M records

---

### DR-004: Consumption Reading Entity

**Description**: Half-hourly energy consumption readings from smart meters

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| reading_id | UUID | Yes | Unique reading identifier | Primary key |
| link_id | UUID | Yes | Meter link reference | FK to DR-002 |
| reading_timestamp | Timestamp | Yes | Half-hour period start | UTC, 30-minute aligned |
| value_kwh | Decimal(10,4) | Yes | Consumption in kWh | ≥ 0 |
| fuel_type | Enum | Yes | Electricity or gas | |
| source | Enum | Yes | DCC or supplier name | |
| quality | Enum | Yes | Data quality flag | actual, estimated, missing |
| ingested_at | Timestamp | Yes | When data was ingested | UTC |

**Data Classification**: CONFIDENTIAL (personal data — reveals household behaviour)
**Data Retention**: Hot: 3 months; Warm: 3-24 months; Cold: 24+ months; Delete per retention policy
**Data Volume**: Year 1: ~36 billion readings (5M users × 48/day × 2 fuels × 365 days); Year 3: ~150 billion cumulative
**Access Patterns**: Primary: consumer_id + date range; Secondary: aggregate by time period for analytics

---

### DR-005: Tariff Entity

**Description**: Energy tariff information from all suppliers

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| tariff_id | UUID | Yes | Unique tariff identifier | Primary key |
| supplier_id | String(50) | Yes | Supplier reference | |
| tariff_name | String(255) | Yes | Tariff display name | |
| fuel_type | Enum | Yes | Electricity, gas, or dual | |
| unit_rate_pence | Decimal(8,4) | Yes | Unit rate in p/kWh | |
| standing_charge_pence | Decimal(8,4) | Yes | Daily standing charge in pence | |
| payment_type | Enum | Yes | Direct debit, prepayment, etc. | |
| green_percentage | Integer | No | Renewable energy % | 0-100 |
| valid_from | Date | Yes | Tariff start date | |
| valid_to | Date | No | Tariff end date | Null = ongoing |
| last_updated | Timestamp | Yes | When tariff data was refreshed | |

**Data Classification**: INTERNAL (publicly available information)
**Data Retention**: Current + 24 months historical (for comparison accuracy)
**Data Volume**: ~5,000 active tariffs; ~50,000 historical records

---

### Data Quality Requirements

**Data Accuracy**: Missing half-hourly readings flagged to consumers. Range validation on ingestion (negative values rejected, values > 100 kWh per half-hour flagged for review). Gas m³ to kWh conversion using published calorific value.

**Data Completeness**: Target 95% completeness for half-hourly readings per meter per day. Gaps communicated to consumer with explanation.

**Data Consistency**: Reconciliation against supplier billing data where available. SMETS1 and SMETS2 data normalised to common format.

**Data Timeliness**: Yesterday's data available to consumers by 10:00 GMT. Alerts triggered within 4 hours of anomaly detection.

**Data Lineage**: Full lineage from meter → DCC/supplier → ingestion → processing → consumer display. All transformations (unit conversion, cost calculation, carbon estimation) version-controlled.

---

### Data Migration Requirements

**Migration Scope**: No legacy data migration required — this is a new service. Consumers start with data retrieval from their meter's history (up to 13 months via DCC for SMETS2).

**Historical Data Retrieval**: On meter linking, request up to 13 months of historical half-hourly data from DCC/supplier to provide immediate value.

---

## Constraints and Assumptions

### Technical Constraints

**TC-1**: DCC infrastructure capacity and scheduling windows constrain the volume and timing of data retrieval requests. Batch processing must align with DCC operational windows.

**TC-2**: SMETS1 meter data is only accessible via the consumer's current energy supplier, not via DCC. Each supplier has different API formats and capabilities.

**TC-3**: All personal and consumption data MUST be hosted in UK data centres to comply with UK GDPR and programme data residency requirements.

**TC-4**: Mobile app must support iOS 15+ and Android 10+ to reach 95%+ of UK smartphone users.

**TC-5**: The app must work on 4G networks and degrade gracefully on 3G in rural areas.

### Business Constraints

**BC-1**: Regulatory sign-offs (ICO, Ofgem, NCSC, GDS) must be obtained before processing real consumer data. This is a hard gate, not negotiable for delivery timeline.

**BC-2**: Energy suppliers are required by Ofgem licence conditions to provide consumer data access, but the timeline and API quality of their implementations is not directly controlled by the programme.

**BC-3**: The programme operates within DESNZ departmental expenditure limits approved through Spending Review.

**BC-4**: The app must position itself as complementary to (not competing with) energy supplier consumer apps.

### Assumptions

**A-1**: DCC will provide API access for consumer-initiated data retrieval under existing or amended SEC arrangements within the programme timeline.

**A-2**: At least 6 major energy suppliers will deliver APIs meeting the agreed specification within the Beta launch timeline.

**A-3**: Consumers will have smartphones capable of running the app (iOS 15+ or Android 10+). Assisted digital provision covers those who do not.

**A-4**: Smart Energy GB will co-promote the app through existing consumer engagement channels at no cost to the programme.

**A-5**: An Ofgem-endorsed tariff data source is available for impartial tariff comparison.

**A-6**: Consumer energy consumption data classification remains OFFICIAL (not uplifted to OFFICIAL-SENSITIVE) for the duration of the programme.

**Validation Plan**: Assumptions A-1 and A-2 validated through early DCC/supplier engagement in Alpha. A-5 validated through Ofgem consultation. A-3 validated through user research.

---

## Success Criteria and KPIs

### Business Success Metrics

| Metric | Baseline | Target | Timeline | Measurement Method |
|--------|----------|--------|----------|-------------------|
| Monthly Active Users | 0 | 5,000,000 | 18 months post-launch | Mobile analytics |
| Average energy savings (active users) | 0% | 5% reduction | 6 months of use | Consumption data comparison |
| App store rating | N/A | 4.2+ | Ongoing | App store reporting |
| Meter linkage completion rate | N/A | 60% | Ongoing | Funnel analytics |
| 30-day retention | N/A | 40% | Ongoing | Cohort analysis |
| Annual consumer bill savings | £0 | £80-£120 per user | 12 months of use | Consumption + tariff analysis |
| Benefit-cost ratio | N/A | >2.0 | 24 months | Treasury benefits framework |

### Technical Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Platform availability | 99.9% | Uptime monitoring |
| API response time (p95) | < 500ms | APM tooling |
| Data retrieval success rate | > 95% | Integration monitoring |
| Data freshness (meter→consumer) | < 24 hours | Pipeline monitoring |
| Error rate | < 0.1% | Log aggregation |
| Mean time to recovery (MTTR) | < 60 minutes | Incident tracking |
| WCAG 2.2 AA compliance | 100% | Automated + manual audit |
| Security vulnerability SLA adherence | 100% | Vulnerability management |

---

## Dependencies and Risks

### Dependencies

| Dependency | Description | Owner | Status | Impact if Delayed |
|------------|-------------|-------|--------|-------------------|
| DCC API access | DCC provides production API access for SMETS2 data | DCC | Not started | CRITICAL — no SMETS2 data without DCC |
| Supplier APIs (6 major) | Suppliers develop and test APIs to specification | Energy Suppliers | Not started | HIGH — reduces meter population coverage |
| ICO DPIA review | ICO reviews and accepts DPIA | ICO | Not started | CRITICAL — cannot process real data |
| Ofgem framework alignment | Ofgem confirms data access framework compliance | Ofgem | Not started | HIGH — regulatory risk |
| GDS assessment capacity | GDS assessors available for Beta assessment | GDS | Not started | MEDIUM — delays phase gate |
| NCSC security review | NCSC reviews architecture and threat model | NCSC | Not started | HIGH — security sign-off required |
| Tariff data source | Ofgem-endorsed tariff data provider contracted | Programme | Not started | HIGH — no tariff comparison |
| Smart Energy GB promotion | Co-marketing agreement for consumer awareness | Smart Energy GB | Not started | MEDIUM — impacts adoption rate |

### Risks

| Risk ID | Description | Probability | Impact | Mitigation Strategy | Owner |
|---------|-------------|-------------|--------|---------------------|-------|
| R-1 | Supplier API delays reduce meter coverage at Beta | MEDIUM | HIGH | Early supplier engagement, pilot with willing suppliers, Ofgem mandate | Programme Director |
| R-2 | DCC capacity constraints limit data retrieval | MEDIUM | HIGH | Batch patterns, caching, capacity pre-agreement | Technical Architect |
| R-3 | Consumer data breach | LOW | CRITICAL | Security by design, pen testing, incident response plan | Security Lead |
| R-4 | Low consumer adoption | MEDIUM | HIGH | Smart Energy GB co-promotion, simple onboarding, immediate value | Product Owner |
| R-5 | GDS assessment failure | LOW | MEDIUM | Continuous evidence collection, mock assessments, user research | Programme Director |
| R-6 | Political/machinery-of-government change | MEDIUM | CRITICAL | Cross-party appeal, early value demonstration, broad stakeholder support | SRO |
| R-7 | DPIA not accepted by ICO | LOW | HIGH | Early ICO engagement, conservative data processing approach | DPO |

*Full risk analysis: ARC-001-RISK-v1.0 (to be created via `/arckit.risk`)*

---

## Requirement Conflicts & Resolutions

### Conflict C-1: Delivery Speed vs Regulatory Rigour

**Conflicting Requirements**:
- **BR-004**: Achieve 5M active users within 18 months of launch (requires early public launch)
- **BR-003**: Achieve all regulatory sign-offs before processing consumer data (may delay launch)

**Stakeholders Involved**:
- **DESNZ Minister (SD-1)**: Wants rapid launch to demonstrate SMIP return and generate positive headlines
- **Ofgem/ICO/NCSC (SD-3/SD-4/SD-12)**: Require thorough review before consumer data is processed

**Nature of Conflict**: The 18-month adoption target starts from launch, but regulatory sign-offs may extend the pre-launch timeline, compressing the adoption window.

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Launch quickly, regulatory in parallel | Early market presence, faster adoption clock | Regulatory risk, potential ICO enforcement | Minister happy; regulators alarmed |
| **Option 2**: Wait for full sign-off, then launch | Zero regulatory risk, exemplar governance | Delayed adoption clock, political frustration | Regulators happy; Minister frustrated |
| **Option 3**: Phased launch with milestone comms | Celebrate Alpha/Beta milestones publicly; regulatory sign-offs before real data; public launch after all approvals | Neither fully satisfied on timing | Both somewhat satisfied |

**Resolution Strategy**: PHASE

**Decision**: Option 3 — Phased launch. Alpha with synthetic data (ministerial announcement of "app in development"). Private Beta with consenting volunteers after regulatory sign-offs. Public launch after GDS Live assessment. 18-month adoption target starts from public launch.

**Rationale**: Phased approach provides ministerial milestones for public communication while ensuring regulatory requirements are met. Adoption target adjusted to start from public launch, not from Alpha.

**Decision Authority**: DESNZ SRO with ministerial briefing

**Impact on Requirements**:
- **Modified**: BR-004 — 18-month clock starts from public launch, not programme start
- **Added**: Milestone communications plan for Alpha and Beta phases

**Stakeholder Management**:
- **Minister**: Monthly briefing with phase milestones to announce; "doing it right" narrative
- **Regulators**: Early engagement ensuring reviews are scheduled and resourced

---

### Conflict C-2: Impartial Tariff Comparison vs Supplier Cooperation

**Conflicting Requirements**:
- **FR-007**: Tariff comparison must be impartial and non-discriminatory
- **Goal G-4**: Requires supplier cooperation for API integration (suppliers may resist if the app drives switching away from them)

**Stakeholders Involved**:
- **Citizens/Ofgem (SD-7/SD-3)**: Want truly impartial tariff information
- **Energy Suppliers (SD-6)**: Wary of a tool that accelerates switching away from them

**Nature of Conflict**: Supplier cooperation is needed for data access, but the tariff comparison feature may motivate suppliers to delay or degrade their API implementations.

**Resolution Strategy**: COMPROMISE + PHASE

**Decision**: Position tariff comparison as helping consumers make informed decisions (Ofgem mandate), not as a switching accelerator. Phase 1: show estimated costs only (no direct switching); Phase 2 (post-launch, subject to evaluation): consider in-app switching. Share tariff comparison methodology with suppliers before launch for transparency.

**Impact on Requirements**:
- **Clarified**: FR-007 — Phase 1 shows cost comparison and links to supplier websites; no in-app switching
- **Added**: BC-4 — App positioned as complementary to supplier apps

**Stakeholder Management**:
- **Suppliers**: Monthly supplier forum, transparent methodology review, emphasis on regulatory mandate
- **Ofgem**: Methodology endorsed as aligned with consumer protection framework

---

### Conflict C-3: DCC Infrastructure Stability vs Consumer Adoption Scale

**Conflicting Requirements**:
- **NFR-S-001**: Scale to 15M users generating 300M readings/day by Year 3
- **INT-001**: DCC integration must not compromise existing smart metering infrastructure

**Stakeholders Involved**:
- **DCC (SD-5)**: Must protect critical infrastructure capacity
- **DESNZ SRO (SD-2)**: Needs the app to scale for adoption and value-for-money targets

**Resolution Strategy**: INNOVATE

**Decision**: Design platform to minimise DCC load through batch retrieval during low-traffic windows, aggressive platform-side caching, and consumer-facing queries served from platform cache (never from DCC directly). Consumer sees cached data; DCC only handles batch retrieval.

**Impact on Requirements**:
- **Clarified**: INT-001 — All consumer data requests served from platform cache; DCC integration is batch-only
- **Added**: NFR-P-002 — Data ingestion batch window alignment with DCC scheduling

**Stakeholder Management**:
- **DCC**: Pre-agreed capacity allocation, batch scheduling alignment, regular capacity reviews

---

### Conflict C-4: Cost Minimisation vs Accessibility Investment

**Conflicting Requirements**:
- **BR-006**: Sustainable operating model with minimal ongoing cost
- **BR-005**: WCAG 2.2 AA accessibility across all features including complex energy visualisations

**Stakeholders Involved**:
- **HM Treasury (SD-9)**: Wants cost minimisation
- **Consumer Orgs (SD-10)**: Demand full accessibility

**Resolution Strategy**: PRIORITIZE (accessibility wins)

**Decision**: Accessibility is a legal requirement under the Public Sector Bodies Accessibility Regulations 2018 and a non-negotiable GDS Service Standard point. The additional cost of accessible energy visualisations is justified as compliance cost, not optional enhancement.

**Impact on Requirements**:
- **No change**: BR-005 and BR-006 both stand. Accessibility costs included in operating model.

**Stakeholder Management**:
- **Treasury**: Accessibility costs framed as compliance/legal obligation (ICO fines up to £17.5M; GDS assessment failure delays programme). Included in SOBC as non-discretionary.

---

## Timeline and Milestones

### High-Level Milestones

| Milestone | Description | Target Date | Dependencies |
|-----------|-------------|-------------|--------------|
| Requirements Approval | Stakeholder sign-off on this document | 2026-03-31 | Stakeholder review |
| Discovery Complete | User research, technology exploration | 2026-04-30 | Team mobilisation |
| Alpha Assessment (GDS) | Prototype tested with users; GDS Alpha assessment | 2026-07-31 | Discovery findings |
| Beta Launch (Private) | Real data, consenting volunteers, regulatory sign-offs | 2026-12-31 | ICO, Ofgem, NCSC, GDS Beta assessment |
| Beta Launch (Public) | Open to all consumers, 6+ supplier integrations | 2027-03-31 | Supplier API readiness |
| Live Assessment (GDS) | Full operational service; GDS Live assessment | 2027-06-30 | Operational maturity |
| 5M Users Target | Adoption milestone | 2028-09-30 | 18 months post-public Beta |

---

## Budget

### Cost Estimate

| Category | Estimated Cost | Notes |
|----------|----------------|-------|
| Discovery & Alpha | £2-3M | Multidisciplinary team, user research, prototyping |
| Beta Development | £5-8M | Platform build, mobile app, DCC/supplier integration |
| Security & Compliance | £1-2M | DPIA, pen testing, NCSC review, GDS prep |
| Infrastructure (Year 1) | £1-2M | Cloud hosting (UK regions), scaling capacity |
| Marketing & Adoption | £1-2M | Smart Energy GB co-promotion, app store optimisation |
| **Total (to Live)** | **£10-17M** | Range reflects scope and integration complexity |

### Ongoing Operational Costs

| Category | Annual Cost | Notes |
|----------|-------------|-------|
| Infrastructure | £2-4M/year | Cloud hosting, scaling for growth |
| Support & Operations | £1-2M/year | L1/L2 support, incident response, on-call |
| Continuous Development | £2-3M/year | Feature iteration, supplier onboarding, security updates |
| DCC Data Access | TBD | Subject to DCC commercial agreement |
| **Total** | **£5-9M/year** | To be validated in SOBC |

---

## Approval

### Requirements Review

| Reviewer | Role | Status | Date | Comments |
|----------|------|--------|------|----------|
| DESNZ SRO | Programme accountability | [ ] Approved | PENDING | |
| Programme Director | Delivery lead | [ ] Approved | PENDING | |
| Technical Architect | Architecture authority | [ ] Approved | PENDING | |
| DPO / Privacy Lead | Data protection | [ ] Approved | PENDING | |
| Ofgem Representative | Regulatory alignment | [ ] Approved | PENDING | |
| DCC Representative | Integration feasibility | [ ] Approved | PENDING | |
| Consumer Representative | User needs | [ ] Approved | PENDING | |

### Sign-Off

By signing below, stakeholders confirm that requirements are complete, understood, and approved to proceed to design phase.

| Stakeholder | Signature | Date |
|-------------|-----------|------|
| DESNZ SRO | _________ | |
| Technical Architect | _________ | |
| DPO / Privacy Lead | _________ | |

---

## Appendices

### Appendix A: Glossary

| Term | Definition |
|------|-----------|
| DCC | Data Communications Company — operates the smart metering communications infrastructure |
| DESNZ | Department for Energy Security & Net Zero |
| DPIA | Data Protection Impact Assessment |
| GDS | Government Digital Service |
| IHD | In-Home Display — consumer device showing real-time energy usage |
| MAU | Monthly Active Users |
| MPAN | Meter Point Administration Number (electricity) |
| MPRN | Meter Point Reference Number (gas) |
| NCSC | National Cyber Security Centre |
| Ofgem | Office of Gas and Electricity Markets — energy regulator |
| SAR | Subject Access Request |
| SEC | Smart Energy Code |
| SMETS1 | Smart Metering Equipment Technical Specification 1 (first-generation meters, supplier-specific) |
| SMETS2 | Smart Metering Equipment Technical Specification 2 (second-generation meters, interoperable via DCC) |
| SMIP | Smart Metering Implementation Programme |
| SLO | Service Level Objective |
| TCoP | Technology Code of Practice |

### Appendix B: Reference Documents

| Document | ID | Relationship |
|----------|----|-------------|
| Architecture Principles | ARC-000-PRIN-v1.0 | Governing principles for all requirements |
| Stakeholder Analysis | ARC-001-STKE-v1.0 | Stakeholder drivers informing requirement prioritisation |
| Risk Register | ARC-001-RISK-v1.0 | Risk management (to be created) |
| Business Case | ARC-001-SOBC-v1.0 | Strategic business case (to be created) |
| Data Model | ARC-001-DATA-v1.0 | Detailed data model (to be created) |

### Appendix C: Requirements Traceability Summary

| Requirement | Stakeholder Goal | Architecture Principle | Priority |
|-------------|-----------------|----------------------|----------|
| BR-001 | G-1, G-4 | P1, P4 | MUST |
| BR-002 | G-2 | P1 | MUST |
| BR-003 | G-3 | P5, P7, P20 | MUST |
| BR-004 | G-1 | P1, P15 | MUST |
| BR-005 | G-5 | P15, P1 | MUST |
| BR-006 | G-6 | — | MUST |
| BR-007 | G-7 | — | SHOULD |
| FR-001–FR-015 | G-1, G-2, G-4, G-5 | P1, P4, P5, P7 | Mixed |
| NFR-P-001–003 | G-1 | P13 | MUST/SHOULD |
| NFR-A-001–003 | G-1, G-4 | P3, P14 | MUST |
| NFR-S-001–002 | G-1 | P2 | MUST |
| NFR-SEC-001–006 | G-3 | P5 | MUST |
| NFR-C-001–005 | G-3 | P5, P7, P20 | MUST |
| NFR-U-001–002 | G-5 | P15 | MUST |
| NFR-M-001–002 | G-3 | P6 | MUST |
| NFR-I-001–002 | G-4 | P4, P16, P21 | MUST/SHOULD |
| INT-001–005 | G-4 | P4, P11, P12 | MUST/SHOULD |
| DR-001–005 | G-1, G-3, G-4 | P7, P8, P9, P10 | MUST |

---

**Generated by**: ArcKit `/arckit.requirements` command
**Generated on**: 2026-01-31
**ArcKit Version**: 1.0.3
**Project**: UK Smart Meter Data Consumer Mobile App (Project 001)
**AI Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
**Generation Context**: Based on ARC-000-PRIN-v1.0 (21 architecture principles) and ARC-001-STKE-v1.0 (12 stakeholder drivers, 7 goals, 4 outcomes)
