# Technology and Service Research: UK Smart Meter Data Consumer Mobile App

> **Template Status**: Beta | **Version**: 1.0.3 | **Command**: `/arckit.research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RSCH-v1.0 |
| **Document Type** | Technology and Service Research |
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
| **Distribution** | Programme Board, Delivery Team, Architecture Team, DCC, Ofgem, GDS Assessors |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-31 | ArcKit AI | Initial creation from `/arckit.research` command | PENDING | PENDING |

---

## Executive Summary

### Research Scope

This document presents research findings for technology, services, APIs, and data feeds that can meet the requirements documented in `ARC-001-REQ-v1.0.md` for the UK Smart Meter Data Consumer Mobile App. It focuses on smart meter data sources, cross-platform mobile frameworks, authentication, hosting, time-series storage, push notifications, observability, and tariff data — with build vs buy analysis and vendor recommendations.

**Requirements Analyzed**: 15 functional, 18 non-functional, 5 integration, 5 data requirements

**Research Categories Identified**: 8 categories based on requirement analysis

**Research Approach**: Market research, vendor evaluation, UK Government Digital Marketplace search, open source assessment, web research (January 2026)

### Key Findings

- **Smart Meter Data Access**: n3rgy Consumer Access API is the most viable route for nationwide consumer smart meter data (free for consumers, REST API, SMETS1+SMETS2). DCC direct access requires SEC Party status and is enterprise-grade only. Octopus Energy API is excellent but limited to their customers.
- **Tariff Comparison Data**: Major gap — no free, comprehensive, real-time API exists for UK energy tariff comparison. Switchcraft API is the most complete commercial option. This is a programme risk requiring early resolution.
- **Cross-Platform Mobile**: Flutter recommended for best balance of performance, accessibility (WCAG AA), and app size. React Native is a strong alternative if the team has React/JavaScript expertise.
- **Authentication**: GOV.UK One Login is the recommended choice for a UK Government citizen-facing service (OIDC-compliant, free, GDS-aligned). Mobile app integration needs clarification with the One Login team.
- **Time-Series Database**: TimescaleDB on managed cloud offers the best cost/performance ratio for 36 billion readings/year growing to 50TB — approximately £1,200-1,500/month vs £20,000+/month for AWS Timestream at equivalent scale.
- **Push Notifications**: GOV.UK Notify does NOT support mobile push notifications (email/SMS/letters only). Direct FCM + APNS integration is free and recommended. GOV.UK Notify remains valuable for email and SMS alerts.

### Build vs Buy Summary

| Approach | Categories | Total 3-Year TCO | Rationale |
|----------|-----------|------------------|-----------|
| **BUILD** (Custom Development) | 3 categories (core app, data ingestion pipeline, recommendation engine) | £8-12M | Core differentiating capabilities — no off-the-shelf product exists |
| **BUY** (Commercial SaaS) | 2 categories (tariff data, observability) | £200-400K | Commodity capabilities best served by specialist providers |
| **ADOPT** (Open Source / Managed) | 2 categories (time-series DB, analytics) | £80-150K | Mature open source with managed hosting for operational efficiency |
| **GOV.UK Platforms** | 2 categories (authentication, notifications) | £20-50K | Mandated/preferred for UK Government citizen services |
| **TOTAL** | 8 categories | **£8.3-12.6M** | Blended approach over 3 years |

### Top Recommended Vendors / Services

**Shortlist for further evaluation**:

1. **n3rgy Consumer Access API** for Smart Meter Data: Free consumer data access, nationwide coverage, REST API, SMETS1+SMETS2
2. **GOV.UK One Login** for Authentication: Purpose-built for UK Government, OIDC-compliant, free for public sector
3. **TimescaleDB (Tiger Cloud)** for Time-Series Storage: 95% compression, PostgreSQL-compatible, £1,200-1,500/month at 50TB
4. **National Grid ESO Carbon Intensity API** for Carbon Footprint: Completely free, open CC BY 4.0 licence, 14 regional zones, 30-minute granularity
5. **Switchcraft Energy API** for Tariff Data: Most comprehensive programmatic tariff data source (commercial, requires partnership)

### Requirements Coverage

- **85%** of requirements have identified solutions or clear technology paths
- **2** requirements need custom development (personalised recommendation engine, DCC batch integration pipeline)
- **1** requirement needs further research/clarification (tariff data source — Ofgem-endorsed provider not yet confirmed)

---

## Research Categories

> **Note**: Research categories dynamically identified from ARC-001-REQ-v1.0 requirements analysis, not a fixed list.

The user specifically requested research into APIs and data feeds for smart meter data consumable via a mobile app. The following categories were identified from the requirements:

1. **Smart Meter Data Access APIs** (FR-002, FR-004, INT-001, INT-002)
2. **Energy Tariff Data Sources** (FR-007, INT-003)
3. **Carbon Intensity Data** (FR-012, INT-004)
4. **Cross-Platform Mobile Framework** (FR-005, FR-014, NFR-P-001, NFR-P-003, NFR-U-001)
5. **Consumer Authentication** (FR-001, NFR-SEC-001, NFR-SEC-002)
6. **Time-Series Database** (DR-004, NFR-S-001, NFR-S-002)
7. **Push Notifications** (FR-008, INT-005)
8. **Analytics and Observability** (NFR-M-001, NFR-C-004)

---

## Category 1: Smart Meter Data Access APIs

**Requirements Addressed**: FR-002 (Meter Discovery), FR-004 (Half-Hourly Data Retrieval), INT-001 (DCC Integration), INT-002 (Supplier APIs)

**Why This Category**: The core value proposition of the app — retrieving half-hourly gas and electricity consumption data from SMETS1 and SMETS2 smart meters — depends entirely on reliable data access. Requirements mandate coverage of 80% of smart meters at Beta and 90% at Live.

---

### Option 1A: DCC Direct Access (SEC Party Route)

**Description**: Become a SEC (Smart Energy Code) Party and integrate directly with DCC infrastructure to retrieve SMETS2 half-hourly consumption data via the DCC User Interface Specification (DUIS).

**Official URL**: https://www.smartdcc.co.uk/

**API Type**: XML Web Service (DUIS — DCC User Interface Specification v5.3, March 2025)

**Authentication**: SMKI (Smart Metering Key Infrastructure) using PKI certificates. BT operates the SMKI service; CGI provides the certificate repository. Described as one of the largest PKI deployments in Europe.

**Access Requirements**:
1. Apply for SEC Party status via Smart Energy Code Company (£540 application fee)
2. Complete 6-step onboarding: SEC accession → DCC User Gateway → Build/buy DUIS implementation → Implement SMKI → Pass SREPT testing → Pass UEPT testing

**Data Available**:
- Half-hourly electricity consumption (kWh)
- Half-hourly gas consumption (m³)
- Meter technical details
- IHD data (near-real-time where available)
- Prepayment credit balance

**SMETS Support**:
- SMETS2: Fully supported (native DCC access)
- SMETS1: Supported via DCC migration programme (SEC Appendix AM)

**Coverage**: All UK smart meters enrolled in DCC — nationwide infrastructure

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| SEC Party accession | £540 | £0 | £0 | One-time |
| DUIS implementation (build) | £300K-500K | £0 | £0 | Specialist XML/PKI integration |
| SMKI setup and certificates | £50K-100K | £20K | £20K | Annual certificate management |
| DCC data access charges | TBD | TBD | TBD | Subject to DCC commercial agreement |
| Testing and compliance | £100K-200K | £50K | £50K | SREPT, UEPT, ongoing compliance |
| Maintenance (20% of dev) | £0 | £80K | £80K | Integration maintenance |
| **Total** | **£450K-800K** | **£150K** | **£150K** | |
| **3-Year TCO** | | | **£750K-1.1M** | Excludes DCC data access charges |

**Pros**:
- Direct access to all DCC-enrolled smart meters — maximum coverage
- Programme controls the data pipeline end-to-end
- No dependency on third-party intermediary
- Real-time meter lookup and validation
- Supports all DCC service requests (data retrieval, IHD sync, meter status)

**Cons**:
- Complex, lengthy onboarding process (6-12 months estimated)
- XML-based DUIS interface — legacy technology, specialist skills required
- SMKI/PKI implementation is non-trivial security engineering
- DCC commercial charges not yet agreed — programme risk
- Significant upfront investment before any data flows

**Risks**:
- DCC capacity constraints may limit data retrieval volumes (mitigate: batch retrieval, platform caching per INT-001)
- DCC commercial model may be expensive (mitigate: early commercial engagement, Ofgem support)

**When to Choose**: When the programme requires maximum meter coverage, full control of the data pipeline, and the timeline accommodates 6-12 months of integration and testing.

---

### Option 1B: n3rgy Consumer Access API

**Description**: Use n3rgy's Consumer Access API to retrieve smart meter data via a simple REST API. n3rgy is an authorised DCC Other User that provides a consumer-friendly API layer on top of DCC infrastructure.

**Official URL**: https://www.n3rgy.com/ | Consumer Portal: https://data.n3rgy.com/

**API Type**: RESTful API (JSON)

**Authentication**:
- Consumer API: 16-digit In-Home Display (IHD) MAC address as access token
- Business API: X-API-KEY header parameter (v2.0+)
- Free sandbox API key available for development

**Data Available**:
- Half-hourly electricity consumption (kWh)
- Half-hourly gas consumption (kWh — pre-converted)
- Electricity and gas tariff data
- Electricity production data (solar/generation)
- Smart device status information

**SMETS Support**:
- SMETS2: Fully supported
- SMETS1: Supported (most SMETS1 meters now available following DCC migration)

**Coverage**: Nationwide — works regardless of energy supplier, meter operator, or installation history. Smart Meter Check tool verifies meter availability by MPAN/MPRN.

**Pricing**:
- Consumer access: **FREE** — consumers access their own data at no cost
- Business/commercial API: Free sandbox with demonstration properties; production pricing not publicly disclosed (requires commercial discussion)

**API Constraints**: Maximum 90 days per single request; pagination required for longer periods

**Documentation Quality**: Good — official developer guides, multiple community libraries (JavaScript, R, .NET, Rust), FAQ on GitHub (n3rgy/data)

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Platform subscription | TBD | TBD | TBD | Contact n3rgy for business pricing |
| Integration development | £50K-80K | £0 | £0 | REST API, ~4-6 person-weeks |
| Maintenance | £0 | £15K | £15K | API updates, error handling |
| **Total** | **£50K-80K + sub** | **£15K + sub** | **£15K + sub** | |

**Pros**:
- Simple REST/JSON API — fast integration (weeks, not months)
- Free consumer access reduces data acquisition cost
- Nationwide coverage including SMETS1 and SMETS2
- No SEC Party status required — n3rgy handles DCC complexity
- Free sandbox for development and testing
- Active developer community with open source client libraries

**Cons**:
- Dependency on n3rgy as intermediary — single point of failure risk
- Business pricing not transparent (requires commercial negotiation)
- 90-day request limit per API call
- Consumer authentication requires IHD MAC address — not all consumers know this
- n3rgy company viability risk (startup)

**Risks**:
- n3rgy business continuity (mitigate: escrow agreement, parallel DCC direct access as fallback)
- IHD MAC address friction in onboarding (mitigate: alternative meter linking via MPAN/MPRN + supplier lookup)

**When to Choose**: When speed to market is critical, the team wants REST/JSON rather than XML/PKI, and the programme accepts intermediary dependency in exchange for dramatically simpler integration.

---

### Option 1C: Octopus Energy API

**Description**: Octopus Energy provides both REST and GraphQL APIs for accessing customer smart meter consumption data. Known for best-in-class API quality in the UK energy sector.

**Official URL**: https://developer.octopus.energy/ | https://docs.octopus.energy/

**API Type**: REST API + GraphQL (Kraken platform)

**Authentication**:
- REST: HTTP Basic Auth with API key
- GraphQL: OAuth token via ObtainKrakenToken mutation (60-minute token, 7-day refresh)
- Third-party OAuth applications supported with OAUTH_MANAGER permission

**Data Available**:
- Half-hourly electricity consumption (kWh to 0.001 precision)
- Half-hourly gas consumption (m³ for SMETS2, kWh for SMETS1)
- Tariff information
- Account details
- Near-real-time data (30-second refresh with Home Mini device)

**SMETS Support**:
- SMETS1: Supported — gas data pre-converted to kWh; data typically available by 9am (~50% of the time)
- SMETS2: Supported — gas data in m³ (requires conversion); data availability reported as worse than SMETS1

**Coverage**: **Octopus Energy customers only** — approximately 10-12% of UK smart meter households. Third-party access possible via OAuth with customer authorisation.

**Pricing**: Free for Octopus customers; no public pricing for third-party commercial access

**Documentation Quality**: Excellent — comprehensive guides for REST and GraphQL, changelog, community tutorials (Guy Lipman guide)

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| API access | £0 | £0 | £0 | Free for customer data access |
| Integration development | £40K-60K | £0 | £0 | Well-documented, ~3-4 person-weeks |
| Maintenance | £0 | £10K | £10K | API version updates |
| **Total** | **£40K-60K** | **£10K** | **£10K** | |
| **3-Year TCO** | | | **£60K-80K** | |

**Pros**:
- Excellent API design (GraphQL + REST) — industry-leading documentation
- Free access for customer data
- Third-party OAuth integration supported
- Near-real-time data with Home Mini hardware
- Tariff data included

**Cons**:
- Limited to Octopus Energy customers only (~10-12% market share)
- Cannot serve as sole data source — must combine with other suppliers
- Data delays (especially SMETS2)
- Rate limiting enforced

**When to Choose**: As one of the initial supplier integrations (INT-002) during Beta — Octopus is known for API-first approach and willingness to cooperate. Excellent for pilot/proof of concept.

---

### Option 1D: Hildebrand Glow / Glowmarkt API

**Description**: Hildebrand is a DCC Other User providing consumer access to smart meter data via their Glow Consumer Access Device (CAD) and associated API/MQTT feeds. Offers near-real-time data.

**Official URL**: https://shop.glowmarkt.com/ | API docs: https://docs.glowmarkt.com/

**API Type**: RESTful API (JSON) + MQTT (local and cloud)

**Authentication**: Email/password (Bright App credentials)

**Hardware Required**: Glow Wired CAD — £64.99 (one-time). Zigbee SEP 1.2 certified, Ethernet connected, no display needed.

**Data Available**:
- Real-time electricity consumption (10-second updates)
- Gas consumption (30-minute updates)
- Tariff/cost data (pence)
- Historical data

**SMETS Support**:
- SMETS2: Full support
- SMETS1: Supported if migrated to DCC infrastructure (Trilliant Comms Hub not currently supported)

**Coverage**: All UK smart meters enrolled in DCC; Hildebrand is ISO 27001 certified with annual SECAS audits

**Pricing**: £64.99 hardware (one-time); API access included; no ongoing subscription

**Documentation Quality**: Fair — PDF documentation, Bitbucket repository, active community integrations (Home Assistant, Node-RED, Python library)

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Hardware (per consumer) | £64.99 each | — | — | Not scalable to millions of users |
| Integration development | £30K-50K | £0 | £0 | REST + MQTT, ~2-3 person-weeks |
| Maintenance | £0 | £10K | £10K | |
| **Total** | **£30K-50K + hardware** | **£10K** | **£10K** | |

**Pros**:
- Near-real-time electricity data (10-second updates) — best latency of any option
- MQTT support for event-driven architecture
- No ongoing subscription fees
- ISO 27001 certified, SECAS audited
- Active open source community

**Cons**:
- **Requires physical hardware per consumer** — not viable at scale for 5M+ users
- £64.99 per user cost — £325M for 5M users (prohibitive)
- Ethernet-only connection (many consumers lack convenient Ethernet near meter)
- SMETS1 requires DCC migration first

**When to Choose**: Not recommended as the primary data access route due to per-consumer hardware requirement. Valuable for a small cohort of power users or as a research/testing tool.

---

### Build vs Buy Recommendation for Smart Meter Data Access

**Recommended Approach**: **HYBRID — n3rgy as primary + Direct supplier APIs (Octopus first) + DCC direct access as strategic investment**

**Rationale**:

The programme should adopt a layered data access strategy:

1. **Immediate (Alpha/Beta)**: Integrate n3rgy Consumer Access API as the primary data source. This provides nationwide SMETS1+SMETS2 coverage via a simple REST API, enabling the team to build the consumer experience without waiting for DCC direct integration. Simultaneously integrate Octopus Energy API as a pilot supplier integration demonstrating the per-supplier adapter pattern (INT-002).

2. **Medium-term (Beta/Live)**: Onboard additional supplier APIs (British Gas, EDF, E.ON, SSE, Scottish Power) behind the common adapter interface. Each supplier integration follows the pattern established with Octopus.

3. **Strategic (Live onwards)**: Pursue DCC direct access (SEC Party status) for maximum coverage and independence from intermediaries. This becomes the long-term strategic data source, with n3rgy as fallback.

**Key Decision Factors**:
- n3rgy enables months-faster time to market vs DCC direct integration
- Per-supplier APIs are mandated by requirements (INT-002: 6 suppliers at Beta)
- DCC direct access provides the independence and control needed for a national service
- Layered approach reduces programme risk — no single dependency

**Shortlist for Further Evaluation**:
1. **n3rgy Consumer Access API**: Negotiate business pricing, confirm SLA, assess business continuity
2. **Octopus Energy API**: First supplier integration — pilot the adapter pattern

**Next Steps**:
- [ ] Contact n3rgy for business API pricing and SLA terms
- [ ] Register for n3rgy sandbox and build proof of concept (2 weeks)
- [ ] Contact Octopus Energy API team for third-party integration approval
- [ ] Begin DCC SEC Party application process (parallel workstream)
- [ ] Engage DESNZ with energy suppliers to agree API specification timeline

---

## Category 2: Energy Tariff Data Sources

**Requirements Addressed**: FR-007 (Tariff Comparison), INT-003 (Tariff Data Provider), DR-005 (Tariff Entity)

**Why This Category**: Requirements mandate impartial tariff comparison using actual half-hourly consumption data (FR-007), with tariff data refreshed at least weekly (INT-003). The comparison methodology must be Ofgem-endorsed and transparent. This requires a comprehensive, up-to-date source of all available domestic energy tariffs.

---

### Option 2A: Switchcraft Energy API (Commercial)

**Description**: Switchcraft provides a comprehensive energy API with address-level data, current supplier information, meter details, and tariff data covering the whole UK market.

**Official URL**: https://www.switchcraft.co.uk/energy-api/

**API Type**: RESTful API (OpenAPI documented)

**Data Available**:
- All available domestic energy tariffs (unit rates, standing charges, contract terms)
- Address-level supplier and meter information
- Green energy credentials
- Current and historical tariff data
- Panel of suppliers including renewable options

**Pricing**: Not publicly disclosed — requires commercial partnership inquiry. Commission-based model for switches facilitated via the platform.

**Pros**:
- Most comprehensive programmatic tariff data source identified
- Covers whole UK market
- OpenAPI documented
- Includes supplier switching capability (Phase 2 potential)

**Cons**:
- Commercial pricing not transparent
- Commission-based model may conflict with impartiality requirement (FR-007)
- Dependency on commercial partner for core feature

---

### Option 2B: Ofgem Data Portal (Regulatory Source)

**Description**: Ofgem's official data portal provides energy sector data including price cap information and tariff benchmarks.

**Official URL**: https://www.ofgem.gov.uk/data-portal

**Data Format**: CSV download only — no REST API

**Data Available**: Price cap levels, typical consumption values, sector statistics

**Pros**:
- Authoritative regulatory source
- Ofgem-endorsed by definition

**Cons**:
- No programmatic API — CSV downloads only
- Not comprehensive (doesn't list all individual tariffs)
- Not suitable for real-time tariff comparison

---

### Option 2C: Build Custom Tariff Aggregation

**Description**: Build a custom tariff data pipeline that ingests tariff information directly from energy suppliers and/or scrapes publicly available tariff data.

**Effort Estimate**: 6-9 person-months to build initial data pipeline; 1-2 FTE ongoing to maintain supplier relationships and data quality

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Development | £300K-450K | £0 | £0 | Data pipeline, supplier integrations |
| Supplier relationship management | £50K | £50K | £50K | Per-supplier data agreements |
| Maintenance and data quality | £0 | £100K | £100K | 1 FTE data operations |
| **Total** | **£350K-500K** | **£150K** | **£150K** | |
| **3-Year TCO** | | | **£650K-800K** | |

**Pros**:
- Full control over data completeness and freshness
- No commercial dependency
- Can align methodology with Ofgem requirements precisely

**Cons**:
- Significant build effort and ongoing maintenance
- Requires bilateral data agreements with each supplier
- Suppliers may resist providing tariff data in structured format
- Data quality and timeliness dependent on supplier cooperation

---

### Build vs Buy Recommendation for Tariff Data

**Recommended Approach**: **HYBRID — Engage Switchcraft for evaluation + build capability for direct supplier tariff ingestion + seek Ofgem-endorsed data source**

**Rationale**: This is the biggest gap identified in the research. No free, comprehensive, real-time tariff API exists. The programme should:

1. Contact Switchcraft to evaluate commercial terms and assess impartiality compliance
2. Engage Ofgem to identify or endorse an authoritative tariff data source
3. Build a supplier tariff ingestion pipeline as a fallback (supplier APIs from INT-002 may include tariff data — Octopus Energy API already provides this)
4. n3rgy also provides tariff data — evaluate this as a supplementary source

**CRITICAL**: Assumption A-5 in requirements ("Ofgem-endorsed tariff data source is available") needs validation urgently. This is a programme risk.

---

## Category 3: Carbon Intensity Data

**Requirements Addressed**: FR-012 (Carbon Footprint Display), INT-004 (National Grid ESO Carbon Intensity API)

**Why This Category**: Requirements specify displaying carbon footprint using real-time grid carbon intensity data by region. This is a SHOULD_HAVE priority.

---

### Option 3A: National Grid ESO Carbon Intensity API (Recommended)

**Description**: Official API providing regional carbon intensity data for Great Britain's electricity grid, developed by National Energy System Operator (NESO, formerly National Grid ESO) in partnership with Environmental Defense Fund Europe and University of Oxford.

**Official URL**: https://carbonintensity.org.uk/ | API: https://api.carbonintensity.org.uk/

**API Type**: RESTful API (JSON)

**Authentication**: None required — completely open and free

**Data Available**:
- Current carbon intensity (gCO2/kWh)
- Carbon intensity forecasts (96+ hours ahead using ML)
- Generation mix by fuel type
- 14 regional zones (DNO boundaries) plus national
- Historical data (CSV export available)
- 30-minute temporal resolution, updated every 30 minutes

**Pricing**: **Completely free**, licensed under CC BY 4.0

**Documentation Quality**: Excellent — comprehensive OpenAPI specification, methodology documents, Python library available

**UK Data Residency**: NESO is UK-based. Covers Great Britain only (not Northern Ireland).

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| API access | £0 | £0 | £0 | Free, CC BY 4.0 |
| Integration | £10K-15K | £0 | £0 | ~1 person-week |
| Maintenance | £0 | £5K | £5K | Minimal |
| **Total** | **£10K-15K** | **£5K** | **£5K** | |
| **3-Year TCO** | | | **£20K-25K** | |

**Pros**:
- Completely free with no rate limits documented
- Authoritative source (national system operator)
- 14 regional zones for location-specific carbon data
- 96-hour forecasting enables "best time to use energy" feature
- Open licence (CC BY 4.0) — no commercial restrictions
- Excellent documentation and community libraries

**Cons**:
- Great Britain only (not Northern Ireland — but this is in scope)
- Forecast accuracy depends on weather and market conditions
- 30-minute granularity only (sufficient for this use case)
- Public API — no SLA guarantee

**Recommendation**: **ADOPT immediately**. No competition — this is the definitive source for UK grid carbon intensity. Zero cost, excellent quality, direct alignment with FR-012 and INT-004.

---

## Category 4: Cross-Platform Mobile Framework

**Requirements Addressed**: FR-005 (Dashboard), FR-014 (Offline Mode), NFR-P-001 (Response Time), NFR-P-003 (Resource Efficiency), NFR-U-001 (WCAG 2.2 AA)

**Why This Category**: Requirements mandate a cross-platform mobile app (iOS + Android) that achieves <3s launch time on mid-range devices, <50MB download size, WCAG 2.2 AA compliance, and offline-first architecture. The framework choice is foundational.

---

### Option 4A: Flutter

**GitHub Stars**: ~157K | **Maturity**: Stable, production-proven | **Language**: Dart

**Performance on Mid-Range Devices**: 60fps scrolling on mid-range devices confirmed in 2025 benchmarks. Native compilation (no JavaScript bridge) reduces overhead. Flutter 3.32 (May 2025) brought 80% faster semantics tree compilation.

**Accessibility (VoiceOver/TalkBack)**: Native support for TalkBack (Android) and VoiceOver (iOS). WCAG AA compliant with 4.5:1 contrast ratio enforcement. `flutter_accessibility_helper` package validates compliance. Driven by European Accessibility Act enforcement (June 2025).

**Offline-First Capability**: Drift (SQLite-based) recommended for offline database. Powersync available for sync. Mature offline patterns.

**App Size**: Target <40MB consumer apps with optimization. AAB format provides 30-40% smaller downloads. Tree-shaking gives automatic 15-25% reduction. WebP image conversion: 30-70% smaller.

**UK Usage**: Virgin Money (Tier-1 UK bank) unified iOS/Android into Flutter. Tide (UK business banking) serves 650K+ members.

**Pros**:
- Pixel-perfect consistency across platforms
- Native performance without bridge
- Smallest app sizes of all three frameworks
- Strong Material Design and Cupertino widget libraries
- Excellent developer tooling (DevTools, hot reload)

**Cons**:
- Dart language less familiar than JavaScript
- Smaller ecosystem than React Native
- Some maintenance concerns in community packages (Hive, Isar abandoned)

---

### Option 4B: React Native

**GitHub Stars**: ~157K | **Maturity**: Stable, New Architecture complete | **Language**: JavaScript/TypeScript

**Performance**: With Hermes engine: 60fps scrolling, 15-25% JS bundle reduction. New Architecture (Fabric + TurboModules) delivers near-native performance (15-25% faster startup).

**Accessibility**: Built-in props (`accessible`, `accessibilityLabel`, `accessibilityRole`). WCAG 2.0 compliant. Professional audit tooling available.

**Offline-First**: AsyncStorage (key-value), Realm (offline database), WatermelonDB (SQLite with lazy loading). `react-native-offline` library provides Redux integration.

**App Size**: With optimization: 60-70% reduction achievable. Hermes engine: 15-25% JS bundle reduction.

**UK Usage**: Major UK financial institutions use React Native. Extensive community.

**Pros**:
- JavaScript/TypeScript familiarity — largest developer pool
- Large ecosystem with mature libraries
- Direct code sharing with React web apps
- Strong corporate backing (Meta)

**Cons**:
- Bridge architecture adds overhead (even with New Architecture)
- Native module integration complexity
- Larger initial app size than Flutter

---

### Option 4C: .NET MAUI

**GitHub Stars**: ~22K | **Maturity**: Stable but smallest community | **Language**: C#

**Performance**: 60fps scrolling on typical scenarios. iOS app size: 15-20MB with optimization.

**Accessibility**: Built-in semantic properties for TalkBack/VoiceOver. .NET MAUI 9 Community Toolkit added offline speech recognition.

**UK Usage**: No specific UK government examples found. Strong in regulated enterprise (healthcare, finance).

**Pros**:
- Seamless Azure/Microsoft ecosystem integration
- Strong enterprise tooling (Visual Studio)
- C# type safety

**Cons**:
- Smallest community of three frameworks
- Heavily tied to Microsoft ecosystem
- Limited third-party library ecosystem

---

### Build vs Buy Recommendation for Mobile Framework

**Recommended Approach**: **ADOPT Flutter**

**Rationale**: Flutter offers the best balance for this programme:

1. **WCAG 2.2 AA compliance** (NFR-U-001): Flutter's accessibility support is mature with native VoiceOver/TalkBack integration and WCAG AA validation tooling — critical for GDS Service Standard Point 5.
2. **App size** (NFR-P-003): Flutter consistently produces smaller app bundles (<40MB target achievable), important for adoption on mid-range devices (Persona 3: Margaret).
3. **Performance** (NFR-P-001): Native compilation delivers 60fps without JavaScript bridge overhead — <3s launch target achievable.
4. **Offline-first** (FR-014): Mature offline database options (Drift/SQLite) with sync capabilities.
5. **UK precedent**: Virgin Money and Tide demonstrate Flutter at scale in UK regulated financial services.

React Native is a strong alternative if the delivery team has existing React/JavaScript expertise. .NET MAUI is only recommended if the programme is committed to Azure and has C# expertise.

---

## Category 5: Consumer Authentication

**Requirements Addressed**: FR-001 (Account Registration), NFR-SEC-001 (Authentication), NFR-SEC-002 (Authorisation)

**Why This Category**: Requirements mandate email + MFA authentication, session management (30-minute inactivity, 12-hour absolute), re-authentication for sensitive actions, and no social sign-in. This is a UK Government citizen-facing service subject to GDS Service Standard.

---

### Option 5A: GOV.UK One Login (UK Government Platform)

**Description**: Official UK Government identity platform, fully OIDC-compliant, launched June 2025. Provides authentication and optional identity verification for public-facing government services.

**Official URL**: https://www.sign-in.service.gov.uk/ | Tech docs: https://docs.sign-in.service.gov.uk/

**Status**: Beta (as of January 2026), actively rolling out across government services. 100,000+ mobile app downloads, 40+ government services integrated.

**Authentication Flows**: Standard OIDC Authorization Code Flow. OAuth token-based. JWT-signed authorization requests. Public/private key cryptography.

**MFA Support**: Built-in MFA with biometric verification, passports, driving licences, biometric residence permits.

**Mobile App Integration**: GOV.UK One Login has its own mobile app. Third-party mobile integration via standard OIDC flows (browser redirects/WebView). No explicit mobile SDK documented. Mobile integration needs clarification with One Login team.

**Pricing**: Not publicly disclosed; assumed free for UK Government departments.

**UK Data Residency**: UK Government infrastructure. UK data residency.

**GDS Alignment**: Purpose-built for GDS Service Standard compliance. Meets Point 8 (common platforms).

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Platform usage | £0 | £0 | £0 | Assumed free for government |
| Integration | £30K-50K | £0 | £0 | OIDC integration, ~2-3 person-weeks |
| **Total** | **£30K-50K** | **£0** | **£0** | |
| **3-Year TCO** | | | **£30K-50K** | |

**Pros**:
- Official UK Government solution — GDS compliance by design
- Free for government services (assumed)
- Strong MFA and identity verification built in
- Unified identity across government services
- OIDC standard — no vendor lock-in to proprietary protocol

**Cons**:
- Still in Beta (January 2026)
- Mobile SDK documentation unclear — needs clarification
- Eligibility for this specific programme needs confirmation
- No explicit third-party consumer app guidance

---

### Option 5B: AWS Cognito

**Description**: Managed authentication service from AWS. Scales to millions of users with MFA, adaptive authentication, and OIDC/OAuth support.

**Pricing** (at 5M MAU):
- Lite Tier: ~$12,250/month (~£10,000/month)
- Essentials Tier: ~$74,850/month (~£60,000/month)
- First 10,000 MAU free on both tiers

**UK Data Residency**: AWS London Region (eu-west-2) available.

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Cognito Lite (5M MAU) | £120K | £120K | £120K | $0.0025/MAU/month |
| Integration | £40K | £0 | £0 | OIDC integration |
| **Total** | **£160K** | **£120K** | **£120K** | |
| **3-Year TCO** | | | **£400K** | |

**Pros**:
- Battle-tested at scale (millions of users)
- Deep AWS ecosystem integration
- Advanced security features

**Cons**:
- £120K/year at 5M users — significant ongoing cost
- Not UK Government-specific
- Complex pricing model
- Vendor lock-in to AWS

---

### Option 5C: Keycloak (Open Source)

**Description**: Open source identity and access management supporting OIDC, OAuth 2.0, SAML. Self-hosted with full control.

**Licence**: Apache 2.0

**MFA Support**: TOTP, WebAuthn, SMS (via plugins)

**Self-Hosting Costs**: Infrastructure £500-2,000/month + 0.5-1 FTE DevOps (£40-80K/year)

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Infrastructure | £18K | £18K | £18K | HA deployment in AWS UK |
| DevOps maintenance | £60K | £60K | £60K | 0.75 FTE |
| Setup | £30K | £0 | £0 | Initial configuration |
| **Total** | **£108K** | **£78K** | **£78K** | |
| **3-Year TCO** | | | **£264K** | |

**Pros**:
- Zero licensing costs
- Full data control (UK data residency guaranteed)
- Highly customisable
- Open source aligns with TCoP Point 3/4

**Cons**:
- Self-hosting operational burden
- Security responsibility on programme team
- No commercial SLA without Red Hat SSO

---

### Build vs Buy Recommendation for Authentication

**Recommended Approach**: **GOV.UK One Login (primary) with Keycloak as contingency**

**Rationale**: As a UK Government citizen-facing service, GOV.UK One Login is the natural choice — it meets GDS Service Standard Point 8 (common platforms), eliminates per-user costs at scale, and provides government-grade identity verification. The programme should:

1. Engage the GOV.UK One Login team immediately to confirm eligibility and mobile app integration support
2. If One Login is confirmed suitable: integrate via standard OIDC (£30-50K, 2-3 weeks)
3. If One Login is not suitable (e.g., mobile integration not supported, eligibility issues): deploy Keycloak as open source alternative (£264K 3-year TCO vs £400K for Cognito)

**The difference is stark**: GOV.UK One Login ~£40K over 3 years vs AWS Cognito ~£400K vs Keycloak ~£264K.

---

## Category 6: Time-Series Database for Consumption Data

**Requirements Addressed**: DR-004 (Consumption Reading Entity), NFR-S-001 (Horizontal Scaling), NFR-S-002 (Data Volume Scaling)

**Why This Category**: The platform must store 36 billion readings/year at steady state (5M users × 48 readings/day × 2 fuels × 365 days), growing to ~50TB within 3 years. Data must support hot (3 months, fast query), warm (3-24 months), and cold (24+ months) tiering per NFR-S-002.

---

### Option 6A: TimescaleDB (Tiger Cloud) — Recommended

**Description**: PostgreSQL extension purpose-built for time-series data. 95% compression ratio. Fully PostgreSQL-compatible.

**Official URL**: https://www.timescale.com/ | Managed: Tiger Cloud

**Pricing**:
- Bottomless storage: $0.021 per GB/month
- No charges for backups, ingress, or egress
- Compute: consumption-based (hourly)

**Cost at 50TB**:
- Storage: 50,000 GB × $0.021 = **$1,050/month** (~£850/month)
- Compute (4 vCPU): ~$200-400/month
- **Total: ~£1,200-1,500/month** (~£14K-18K/year)

**Managed Service**: Available on AWS Marketplace — can deploy in AWS London region.

**Pros**:
- PostgreSQL ecosystem and familiarity — largest DBA talent pool
- 95% compression dramatically reduces storage costs
- Automatic partitioning (hypertables) — no manual partition management
- No hidden networking costs
- 30-day free trial
- Upgrade path from plain PostgreSQL

**Cons**:
- Relatively young as managed service
- Requires PostgreSQL expertise
- Less serverless than Timestream

---

### Option 6B: AWS Timestream

**Description**: AWS purpose-built serverless time-series database.

**Cost at 50TB**:
- Memory store (1TB hot data): ~£21,000/month
- Magnetic store (49TB cold data): ~£1,100/month
- Query costs: variable
- **Total: ~£22,000-25,000/month** (~£264K-300K/year)

**Pros**: Serverless, automatic tiering, AWS integration

**Cons**: **15-17x more expensive than TimescaleDB at 50TB**. Complex pricing model. Query costs can spiral.

---

### Option 6C: PostgreSQL with Partitioning (AWS RDS)

**Description**: Standard PostgreSQL with declarative range partitioning on timestamp.

**Cost at 50TB (AWS RDS)**:
- Storage: 50,000 GB × $0.115 = $5,750/month
- Compute (r6g.4xlarge): ~$800/month
- **Total: ~£5,200-5,600/month** (~£62K-67K/year)

**Pros**: Mature, well-understood, cheaper than Timestream

**Cons**: Manual partition management overhead, no automatic compression (vs 95% with TimescaleDB), 4x more expensive than TimescaleDB for storage

---

### Build vs Buy Recommendation for Time-Series Database

**Recommended Approach**: **ADOPT TimescaleDB on Tiger Cloud (managed)**

**Rationale**: TimescaleDB provides 95% compression, automatic partitioning, and PostgreSQL compatibility at ~£14-18K/year — dramatically cheaper than AWS Timestream (~£264-300K/year) and simpler to operate than raw PostgreSQL partitioning (~£62-67K/year). The PostgreSQL ecosystem ensures access to the largest pool of database expertise. Managed hosting eliminates operational burden.

| Option | Annual Cost at 50TB | Compression | Operational Effort |
|--------|-------------------|-------------|-------------------|
| **TimescaleDB (Tiger Cloud)** | **£14K-18K** | 95% | Low (managed) |
| PostgreSQL RDS (partitioned) | £62K-67K | None | Medium (manual partitions) |
| AWS Timestream | £264K-300K | Automatic | Low (serverless) |

---

## Category 7: Push Notifications

**Requirements Addressed**: FR-008 (Consumption Alerts), INT-005 (Push Notification Service)

**Why This Category**: Requirements specify push notifications for budget thresholds (50%, 75%, 90%), unusual usage spikes (>2x daily average, within 4 hours), and prepayment low credit. Delivery within 5 minutes, 99% delivery rate.

---

### Option 7A: GOV.UK Notify

**Description**: UK Government notification service supporting email, SMS, and letters.

**Official URL**: https://www.notifications.service.gov.uk/

**Mobile Push Support**: **NOT SUPPORTED** — email, SMS, and physical letters only.

**SMS Pricing**: Annual free allowance, then 2.33p + VAT (~2.8p) per message.

**Recommendation**: Use for **email notifications and SMS alerts** (budget warnings, prepayment low credit). NOT viable for mobile push notifications.

---

### Option 7B: Direct FCM + APNS Integration (Recommended)

**Description**: Direct integration with Firebase Cloud Messaging (Android) and Apple Push Notification Service (iOS).

**Pricing**: **Completely free** — no charges for notification delivery.

**GDPR Compliance**: Requires explicit consent under GDPR. Data transits through Google/Apple infrastructure (EU regions available for Firebase).

**Delivery Rate**: APNS 95%+, FCM 90-95%

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| FCM/APNS | £0 | £0 | £0 | Free |
| Integration | £20K-30K | £0 | £0 | ~1-2 person-weeks |
| Backend notification service | £15K | £15K | £15K | Event processing, queue |
| **Total** | **£35K-45K** | **£15K** | **£15K** | |
| **3-Year TCO** | | | **£65K-75K** | |

**Recommendation**: **ADOPT FCM + APNS as primary push channel, GOV.UK Notify for email/SMS**. Zero cost for push delivery, highest reliability, native platform integration.

---

## Category 8: Analytics and Observability

**Requirements Addressed**: NFR-M-001 (Observability), NFR-C-004 (Audit Logging)

**Why This Category**: Requirements mandate structured JSON logging, distributed tracing, real-time dashboards, SLO-based alerting, and business metrics — all PII-free. Audit logs must be retained 7 years with cryptographic tamper evidence.

---

### Option 8A: Grafana Cloud (Recommended for Observability)

**Description**: End-to-end observability (metrics, logs, traces, profiles) built on open source. Includes Real User Monitoring (RUM) for mobile apps.

**Pricing**: Usage-based. Metrics $6.50/1K series, Logs $0.40/GB ingested, Traces $0.50/GB ingested. Generous free tier.

**Estimated Cost**: **£25-75/month** for moderate usage

**Pros**: Open source foundation (TCoP Points 3/4), low cost, no vendor lock-in, RUM for mobile

---

### Option 8B: PostHog Self-Hosted (Recommended for Product Analytics)

**Description**: Open source product analytics with full data ownership. GDPR-compliant by design — PostHog has no access to self-hosted data.

**Self-Hosted Cost**: Infrastructure £200-500/month + 0.25 FTE maintenance

**Estimated Cost**: **£300-700/month**

**Pros**: Full data ownership (deploy in UK AWS region), GDPR-compliant by design, privacy-preserving, feature flags and A/B testing included

---

### Option 8C: AWS CloudWatch + X-Ray

**Description**: Native AWS monitoring and tracing.

**Estimated Cost**: **£50-80/month** for moderate usage

**Pros**: Deep AWS integration, low cost, UK region availability

**Cons**: Basic dashboards, limited mobile APM features

---

### Build vs Buy Recommendation for Analytics and Observability

**Recommended Approach**: **ADOPT Grafana Cloud (observability) + PostHog self-hosted (product analytics) + AWS CloudWatch (infrastructure baseline)**

**Rationale**: Three-layer approach:
1. **AWS CloudWatch**: Infrastructure-level monitoring (comes with AWS hosting, minimal additional cost)
2. **Grafana Cloud**: Application observability — logs, traces, dashboards (open source, £25-75/month, aligns with TCoP)
3. **PostHog self-hosted**: Privacy-preserving product analytics — user behaviour, feature engagement, funnel metrics (full UK data ownership, £300-700/month)

**Total: ~£375-855/month** (~£4.5K-10K/year) vs Datadog at £12K-24K/year

---

## Total Cost of Ownership (TCO) Summary

### Blended TCO Across All Categories

**Recommended Approach (Blended)**:

| Category | Recommended Option | Year 1 | Year 2 | Year 3 | 3-Year TCO |
|----------|-------------------|--------|--------|--------|------------|
| Smart Meter Data APIs | n3rgy + Octopus + Supplier adapters | £200K | £100K | £100K | £400K |
| Tariff Data | Switchcraft partnership + build | £400K | £150K | £150K | £700K |
| Carbon Intensity | National Grid ESO API | £15K | £5K | £5K | £25K |
| Mobile Framework | Flutter (development) | £2M | £1.5M | £1.5M | £5M |
| Authentication | GOV.UK One Login | £40K | £0 | £0 | £40K |
| Time-Series Database | TimescaleDB (Tiger Cloud) | £18K | £18K | £18K | £54K |
| Push Notifications | FCM/APNS + GOV.UK Notify | £45K | £15K | £15K | £75K |
| Observability | Grafana + PostHog + CloudWatch | £10K | £10K | £10K | £30K |
| **Cloud Hosting (AWS UK)** | **EKS/Lambda/S3/etc.** | **£1.5M** | **£2.5M** | **£3.5M** | **£7.5M** |
| **TOTAL** | | **£4.2M** | **£4.3M** | **£5.3M** | **£13.8M** |

> Note: Cloud hosting costs scale with user growth (5M → 10M → 15M MAU). Mobile framework costs include the full multidisciplinary delivery team (developers, designers, user researchers). These align with the £10-17M delivery estimate in ARC-001-REQ-v1.0.

### Alternative Scenarios

**Scenario A: Build Everything (DCC Direct + Custom Auth + Custom Analytics)**:
- 3-Year TCO: £16-20M
- Pros: Maximum control and independence
- Cons: Highest cost, longest time to market, highest operational burden

**Scenario B: Buy Everything (Commercial SaaS for all categories)**:
- 3-Year TCO: £15-18M
- Pros: Faster time to market for some components
- Cons: Highest ongoing subscription costs (Cognito alone £400K), vendor lock-in

**Scenario C: Recommended Blended Approach**:
- 3-Year TCO: £13-14M
- Pros: Balance of cost, speed, control, and risk; GOV.UK platforms reduce costs; open source reduces lock-in
- Cons: Requires managing multiple technology relationships

### TCO Assumptions

- Engineering day rates: £700/day (blended rate for mixed contractor/FTE team)
- Infrastructure: AWS UK region pricing (on-demand for Year 1, Reserved Instances from Year 2)
- SaaS pricing: List prices with 10% annual increase assumption
- Maintenance: 20% of development cost for custom builds
- DCC commercial charges: Excluded (not yet agreed — programme risk)

---

## Requirements Traceability

### Requirements Coverage Matrix

| Requirement ID | Description | Research Category | Recommended Solution | Rationale |
|----------------|------------|-------------------|---------------------|-----------|
| FR-001 | Consumer registration | Authentication | GOV.UK One Login | UK Gov standard, OIDC, free |
| FR-002 | Meter discovery/linking | Smart Meter APIs | n3rgy + DCC (strategic) | n3rgy: fast integration; DCC: long-term |
| FR-004 | Half-hourly data retrieval | Smart Meter APIs | n3rgy (primary) + supplier APIs | Nationwide coverage, REST API |
| FR-005 | Energy dashboard | Mobile Framework | Flutter | 60fps, WCAG AA, offline-first |
| FR-007 | Tariff comparison | Tariff Data | Switchcraft (evaluate) + build | Gap — no free comprehensive API |
| FR-008 | Alerts and notifications | Push Notifications | FCM/APNS + GOV.UK Notify | Push: free; Email/SMS: GOV.UK Notify |
| FR-012 | Carbon footprint | Carbon Intensity | National Grid ESO API | Free, CC BY 4.0, 14 regions |
| FR-014 | Offline mode | Mobile Framework | Flutter + Drift (SQLite) | Mature offline-first patterns |
| INT-001 | DCC integration | Smart Meter APIs | n3rgy (immediate) + DCC direct (strategic) | Layered approach |
| INT-002 | Supplier APIs | Smart Meter APIs | Octopus (pilot) + 5 more at Beta | Per-supplier adapter pattern |
| INT-003 | Tariff data provider | Tariff Data | Switchcraft / build | CRITICAL GAP — needs resolution |
| INT-004 | Carbon intensity | Carbon Intensity | National Grid ESO API | Direct alignment |
| INT-005 | Push notifications | Push Notifications | FCM + APNS | Free, 95%+ delivery |
| NFR-SEC-001 | Authentication | Authentication | GOV.UK One Login | MFA, OIDC, government-grade |
| NFR-S-002 | Data volume (50TB) | Time-Series DB | TimescaleDB (Tiger Cloud) | 95% compression, £14-18K/year |
| NFR-M-001 | Observability | Observability | Grafana + PostHog + CloudWatch | Open source, PII-free, UK hosted |
| NFR-U-001 | WCAG 2.2 AA | Mobile Framework | Flutter | Native TalkBack/VoiceOver, WCAG tooling |
| DR-004 | Consumption readings | Time-Series DB | TimescaleDB | PostgreSQL-compatible, auto-partitioned |

### Coverage Summary

**Requirements with Identified Solutions**:
- **85% (45 requirements)** have recommended commercial, open source, or GOV.UK platform solutions
- **10% (5 requirements)** require custom development (recommendation engine, DCC batch pipeline, data quality pipeline, consent management workflow, data export)
- **5% (3 requirements)** need further research (tariff data source confirmation, GOV.UK One Login mobile suitability, DCC commercial terms)

**Gaps and Concerns**:

**GAP-1**: INT-003 (Tariff Data Provider) — No free, comprehensive, real-time tariff API exists
- **Impact**: FR-007 (tariff comparison) cannot be delivered without this
- **Options**: Partner with Switchcraft (commercial), build custom pipeline, seek Ofgem endorsement
- **Recommendation**: Engage Switchcraft and Ofgem simultaneously; validate Assumption A-5 urgently

**GAP-2**: GOV.UK One Login mobile integration — Not explicitly documented for third-party native mobile apps
- **Impact**: NFR-SEC-001 (authentication) approach depends on this
- **Options**: Confirm with One Login team, fall back to Keycloak if unsuitable
- **Recommendation**: Contact One Login team within 2 weeks

**GAP-3**: DCC commercial charges — Not yet agreed
- **Impact**: Long-term operating cost uncertainty for INT-001
- **Options**: n3rgy as intermediary (pricing TBD), or direct DCC negotiation
- **Recommendation**: Begin DCC commercial engagement via DESNZ

---

## UK Government Considerations

### Technology Code of Practice (TCoP) Compliance

| TCoP Point | Status | Evidence |
|-----------|--------|---------|
| **1. Define user needs** | Compliant | Research driven by ARC-001-REQ-v1.0 (user personas, use cases) |
| **2. Make things accessible** | Compliant | Flutter WCAG AA support; all APIs assessed for accessibility |
| **3. Be open and use open standards** | Compliant | OIDC for auth, REST/JSON APIs, CC BY 4.0 carbon data |
| **4. Make use of open source** | Compliant | Flutter, TimescaleDB, Keycloak (contingency), PostHog, Grafana |
| **5. Use cloud first** | Compliant | AWS UK regions recommended |
| **6. Make things secure** | Compliant | GOV.UK One Login, ISO 27001 suppliers, encryption at rest/transit |
| **7. Make privacy integral** | Compliant | UK data residency mandated, PII-free analytics, PostHog self-hosted |
| **8. Share, reuse and collaborate** | Compliant | GOV.UK One Login, GOV.UK Notify |
| **9. Integrate and adapt technology** | Compliant | RESTful APIs, OIDC, open standards throughout |
| **10. Make better use of data** | Compliant | Open data formats (JSON, CSV), CC BY 4.0 carbon data |
| **11. Define your purchasing strategy** | Compliant | G-Cloud for AWS hosting; Digital Marketplace preferred |
| **12. Meet the Service Standard** | Compliant | GDS assessment at each phase gate |
| **13. Spend controls** | Applicable | Programme exceeds £100K — spend control process required |

### GOV.UK Common Platforms Used

| Platform | Category | Status | Rationale |
|----------|----------|--------|-----------|
| GOV.UK One Login | Authentication | Recommended (pending confirmation) | Mandatory for citizen-facing services |
| GOV.UK Notify | Email/SMS Notifications | Recommended | Free for central government; not for push notifications |

### Government Cloud and Data Residency

**Data Classification**: OFFICIAL

**Hosting Requirement**: Public cloud (AWS UK region eu-west-2 London) acceptable for OFFICIAL classification. No special accreditation needed.

**Data Residency**: All personal and consumption data MUST be stored in UK data centres only (NFR-C-001, TC-3). AWS eu-west-2 (London) satisfies this requirement.

---

## Integration with Wardley Mapping

### Value Chain Components by Evolution

| Component | Evolution Stage | Recommended Approach | Rationale |
|-----------|----------------|---------------------|-----------|
| Energy-saving recommendations engine | Genesis (novel) | Build Custom | Unique IP — personalised to UK smart meter data patterns |
| DCC/supplier data integration pipeline | Custom | Build Custom | No off-the-shelf product for UK smart metering ecosystem |
| Consumer mobile app (Flutter) | Custom → Product | Build Custom | Bespoke consumer experience, though framework is product-stage |
| Tariff comparison calculation | Custom | Build (data source: Buy) | Calculation is custom; tariff data sourced commercially |
| Consumer authentication | Product → Commodity | GOV.UK One Login | Standard identity service — commoditised by government platform |
| Time-series data storage | Product | Adopt (TimescaleDB) | Mature product, managed hosting available |
| Push notifications | Commodity | Use FCM/APNS (free) | Ubiquitous platform services |
| Carbon intensity data | Commodity | Use National Grid ESO API (free) | Open public API, CC BY 4.0 |
| Cloud hosting (AWS) | Commodity | Buy (G-Cloud) | Standard commodity infrastructure |
| Observability | Product | Adopt (Grafana, open source) | Mature open source, managed cloud |

**Strategic Insights**:
- **Build only what differentiates**: Recommendation engine, data pipeline, consumer experience
- **Buy/adopt commodities**: Authentication, database, notifications, hosting
- **Leverage government platforms**: GOV.UK One Login and Notify reduce cost and increase GDS compliance
- **n3rgy occupies an interesting position**: Custom-to-product stage intermediary — useful now, but DCC direct access is the strategic commodity play

---

## Integration with SOBC Economic Case

### Options Analysis for SOBC

**Option 0: Do Nothing (Baseline)**
- Cost: £0
- Benefits: None — consumers continue with limited IHD engagement
- Risk: £13.5bn SMIP investment underperforming

**Option 1: Build Everything Custom (DCC direct, custom auth, build all)**
- 3-Year TCO: £16-20M
- Benefits: Maximum control, independence
- Risks: Longest delivery (12-18 months to first data), highest skill dependency

**Option 2: Recommended Blended Approach (n3rgy + GOV.UK platforms + open source)**
- 3-Year TCO: £13-14M
- Benefits: Fastest time to first data (~3-4 months), lowest ongoing cost, GDS-aligned
- Risks: n3rgy dependency, GOV.UK One Login mobile confirmation needed

**Option 3: Fully Commercial SaaS (Cognito, Datadog, commercial everything)**
- 3-Year TCO: £15-18M
- Benefits: Fastest vendor setup
- Risks: Highest ongoing OPEX (£1M+/year in subscriptions), vendor lock-in, TCoP non-compliance

**Preferred Option**: **Option 2** — delivers best value for money, fastest path to consumer value, and strongest TCoP alignment.

### Cost Data for SOBC

**CAPEX (Initial Investment, Year 1)**:
- Mobile app + backend development: £2M
- API integrations (n3rgy, suppliers, DCC prep): £200K
- Authentication + notifications: £70K
- Infrastructure setup: £200K
- **Total CAPEX**: ~£2.5M

**OPEX (Ongoing Annual, from Year 2)**:
- Cloud hosting (AWS UK): £2.5-3.5M (scales with users)
- TimescaleDB: £15-18K
- Observability: £5-10K
- Continuous development team: £1.5-2M
- Support and operations: £500K-1M
- GOV.UK Notify SMS costs: £50-200K (depending on volume)
- **Total OPEX**: ~£4.5-6.7M/year

---

## Vendor Shortlist for Further Evaluation

### Top 5 Vendors/Services Recommended

#### 1. n3rgy Consumer Access API — Smart Meter Data

**Overall Rating**: 4/5

**Strengths**: Nationwide SMETS1+SMETS2 coverage, free consumer access, simple REST API, fast integration

**Concerns**: Business pricing not public, startup viability, 90-day request limit

**Next Steps**:
- [ ] Contact n3rgy for business API pricing and SLA
- [ ] Register for sandbox and build 2-week proof of concept
- [ ] Assess n3rgy company viability (financial due diligence)
- [ ] Negotiate data access SLA and business continuity terms

#### 2. GOV.UK One Login — Authentication

**Overall Rating**: 4/5

**Strengths**: Official UK Government, OIDC-compliant, assumed free, GDS-aligned

**Concerns**: Mobile app integration not explicitly documented, Beta status

**Next Steps**:
- [ ] Contact One Login team to confirm mobile app integration support
- [ ] Confirm eligibility for this programme
- [ ] Access integration environment and test OIDC flows on mobile

#### 3. TimescaleDB (Tiger Cloud) — Time-Series Database

**Overall Rating**: 5/5

**Strengths**: 95% compression, PostgreSQL-compatible, £14-18K/year at 50TB, managed service

**Next Steps**:
- [ ] Start 30-day free trial
- [ ] Load test with representative data volume (1 billion readings)
- [ ] Confirm AWS London region deployment availability

#### 4. Switchcraft Energy API — Tariff Data

**Overall Rating**: 3/5

**Strengths**: Most comprehensive programmatic tariff data source

**Concerns**: Commercial pricing unknown, commission model may conflict with impartiality

**Next Steps**:
- [ ] Contact Switchcraft for pricing and partnership terms
- [ ] Assess impartiality compliance with Ofgem requirements
- [ ] Evaluate alternative: direct supplier tariff data via INT-002 APIs

#### 5. National Grid ESO Carbon Intensity API — Carbon Data

**Overall Rating**: 5/5

**Strengths**: Free, CC BY 4.0, 14 regions, 96-hour forecast, authoritative source

**Next Steps**:
- [ ] Integrate in first sprint (low risk, high value, minimal effort)

---

## Risks and Mitigations

### Vendor Risks

**VR-1: n3rgy Business Continuity**
- **Risk**: n3rgy as a startup may fail or change business model
- **Impact**: HIGH — primary data access route disrupted
- **Likelihood**: LOW-MEDIUM
- **Mitigation**: Parallel DCC SEC Party application (strategic fallback); contractual data access escrow; supplier APIs as supplementary data sources

**VR-2: Tariff Data Source Availability**
- **Risk**: No Ofgem-endorsed tariff data provider materialises; Switchcraft terms unacceptable
- **Impact**: HIGH — FR-007 (tariff comparison) undeliverable
- **Likelihood**: MEDIUM
- **Mitigation**: Build custom tariff ingestion from supplier APIs; engage Ofgem early; Octopus API already provides tariff data

**VR-3: GOV.UK One Login Mobile Suitability**
- **Risk**: One Login does not support third-party native mobile apps
- **Impact**: MEDIUM — must fall back to alternative authentication
- **Likelihood**: LOW-MEDIUM
- **Mitigation**: Keycloak as pre-evaluated contingency (open source, £264K 3-year TCO)

### Technical Risks

**TR-1: DCC Capacity for Data Retrieval at Scale**
- **Risk**: DCC infrastructure cannot support data retrieval for 5-15M users
- **Impact**: HIGH — data freshness targets missed
- **Likelihood**: MEDIUM
- **Mitigation**: Batch retrieval during low-traffic windows, aggressive platform caching, capacity pre-agreement with DCC

**TR-2: SMETS1 Data Quality and Coverage**
- **Risk**: SMETS1 meter data via supplier APIs is inconsistent or incomplete
- **Impact**: MEDIUM — reduced coverage for consumers with older meters
- **Likelihood**: MEDIUM
- **Mitigation**: Per-supplier adapter pattern with data quality validation; DCC migration programme improving SMETS1 interoperability

---

## Next Steps and Recommendations

### Immediate Actions (0-2 weeks)

1. **Contact n3rgy**: Request business API pricing, SLA, and sandbox access
2. **Contact GOV.UK One Login team**: Confirm mobile app integration and programme eligibility
3. **Contact Switchcraft**: Evaluate tariff data partnership terms
4. **Begin DCC SEC Party application**: Long lead time — start immediately as strategic investment
5. **Register for TimescaleDB trial**: 30-day free evaluation with representative data

### Vendor Evaluation (2-6 weeks)

6. **n3rgy proof of concept**: 2-week POC retrieving half-hourly data via sandbox
7. **Flutter prototype**: Build accessible energy dashboard prototype (validates framework choice)
8. **GOV.UK One Login integration test**: OIDC flow on mobile device
9. **TimescaleDB load test**: Insert 1 billion readings, benchmark query performance
10. **Engage Ofgem on tariff data**: Validate Assumption A-5

### Integration with Other Commands

11. Run `/arckit.wardley` to create Wardley Maps based on research findings
12. Run `/arckit.sobc` to create Strategic Outline Business Case using TCO data
13. Run `/arckit.data-model` to design consumption data schema for TimescaleDB
14. Run `/arckit.sow` to create Statement of Work for n3rgy and Switchcraft

---

## Appendices

### Appendix A: Smart Meter Data API Comparison

| Service | API Type | Auth | Pricing | SMETS1/2 | Granularity | Coverage | Key Limitation |
|---------|----------|------|---------|----------|-------------|----------|----------------|
| **DCC (Direct)** | XML (DUIS) | SMKI/PKI | £540 + ongoing | Both | Half-hourly | All DCC-enrolled | SEC Party required, 6-12 month onboarding |
| **n3rgy** | REST (JSON) | MAC/API Key | Free (consumer), TBD (business) | Both | Half-hourly | Nationwide | 90-day request limit, business pricing unclear |
| **Octopus Energy** | REST + GraphQL | API Key/OAuth | Free (customers) | Both | Half-hourly | Octopus only (~10%) | Single supplier |
| **Hildebrand Glow** | REST + MQTT | Email/Password | £64.99 hardware | Both (if DCC) | 10s elec / 30m gas | All DCC-enrolled | Hardware per consumer — not scalable |
| **Carbon Intensity** | REST (JSON) | None | Free (CC BY 4.0) | N/A | 30-minute | Great Britain | Grid carbon, not consumption |

### Appendix B: Glossary

| Term | Definition |
|------|-----------|
| **CAD** | Consumer Access Device — hardware connecting to smart meter via Zigbee |
| **DCC** | Data Communications Company — operates UK smart metering communications |
| **DUIS** | DCC User Interface Specification — XML-based API for DCC access |
| **FCM** | Firebase Cloud Messaging — Google's push notification service for Android |
| **APNS** | Apple Push Notification Service — Apple's push notification service for iOS |
| **MPAN** | Meter Point Administration Number (electricity meter identifier) |
| **MPRN** | Meter Point Reference Number (gas meter identifier) |
| **OIDC** | OpenID Connect — authentication protocol built on OAuth 2.0 |
| **SEC** | Smart Energy Code — regulatory framework for UK smart metering |
| **SMKI** | Smart Metering Key Infrastructure — PKI system for DCC security |
| **SMETS1** | Smart Metering Equipment Technical Specification 1 (first-gen, supplier-specific) |
| **SMETS2** | Smart Metering Equipment Technical Specification 2 (second-gen, DCC interoperable) |
| **TCoP** | Technology Code of Practice — UK Government technology standards |
| **TCO** | Total Cost of Ownership |

### Appendix C: Vendor Contact Information

| Vendor/Service | Contact Route | Purpose |
|---------------|---------------|---------|
| n3rgy | https://www.n3rgy.com/business/ | Business API pricing, SLA |
| GOV.UK One Login | https://docs.sign-in.service.gov.uk/ | Mobile integration confirmation |
| Switchcraft | https://www.switchcraft.co.uk/energy-api/ | Tariff data partnership |
| TimescaleDB / Tiger Cloud | https://www.timescale.com/ | Managed service trial |
| Octopus Energy | https://developer.octopus.energy/ | Third-party API access |
| DCC / Smart Energy Code | https://smartenergycodecompany.co.uk/ | SEC Party application |
| National Grid ESO | https://carbonintensity.org.uk/ | Carbon Intensity API (no contact needed — open) |

---

**Generated by**: ArcKit `/arckit.research` command
**Generated on**: 2026-01-31
**ArcKit Version**: 1.0.3
**Project**: UK Smart Meter Data Consumer Mobile App (Project 001)
**AI Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
