# UK Smart Meter Data Consumer Mobile App

**Architecture governance project for a mobile application enabling citizens to access and visualise their smart meter energy consumption data.**

Built with [ArcKit](https://tractorjuice.github.io/arc-kit/) — 80+ AI-driven slash commands for architecture governance, installed as a plugin for Claude Code.

## Project Context

The **Smart Metering Implementation Programme (SMIP)** has deployed over 34 million smart meters across Great Britain. The **Data Communications Company (DCC)** operates the communications infrastructure connecting smart meters to energy suppliers and authorised third parties.

This project designs a consumer-facing mobile application that:

- **Authenticates** consumers and links to their smart meter(s)
- **Retrieves** half-hourly gas and electricity consumption data from SMETS1 and SMETS2 meters
- **Visualises** real-time and historical energy usage with intuitive charts and dashboards
- **Recommends** personalised energy-saving actions based on consumption patterns
- **Compares** tariffs using actual consumption data to help consumers switch
- **Alerts** consumers to unusual consumption, budget thresholds, and prepayment reminders

## Key Stakeholders

| Stakeholder | Interest |
|-------------|----------|
| Department for Energy Security & Net Zero (DESNZ) | Smart metering policy |
| Ofgem | Energy regulation, consumer data access rights |
| Data Communications Company (DCC) | Smart meter communications infrastructure |
| Energy Suppliers | Data providers, consumer relationship owners |
| Citizens / Energy Consumers | App users seeking to understand and reduce energy costs |
| Smart Energy GB | Consumer engagement and awareness |
| ICO | Data protection for personal energy consumption data |

## Regulatory Context

- **Smart Energy Code (SEC)** - Governs data access and security for smart metering
- **Ofgem Supplier Licence Conditions** - Consumer rights to access their energy data
- **UK GDPR / Data Protection Act 2018** - Energy consumption is personal data
- **Privacy and Electronic Communications Regulations (PECR)** - Electronic communications
- **GDS Service Standard** - 14-point assessment for government digital services
- **Technology Code of Practice (TCoP)** - 13-point UK Government technology standards
- **Accessibility Regulations (Public Sector Bodies) 2018** - Mobile accessibility

## Getting Started

1. Start Claude Code in this repository — the `arckit` plugin loads automatically via the marketplace configured in `.claude/settings.json`
2. Run `/arckit:start` for guided onboarding and workflow selection
3. Run `/arckit:principles` to establish architecture governance
4. Run `/arckit:stakeholders` to analyze stakeholder drivers and goals
5. Run `/arckit:requirements` to define requirements for the smart meter app

Run `/arckit:health` at any time to scan for stale artifacts, missing traceability, and governance gaps. Run `/arckit:pages` to regenerate the `docs/` site.

## Available Commands

The plugin currently provides 80+ slash commands across architecture, procurement, compliance, and operations. A representative subset:

#### Discovery & Planning
- `/arckit:start` — Guided project onboarding and workflow selection
- `/arckit:plan` — Create project plan with timeline, phases, and gates
- `/arckit:principles` — Create or update architecture principles
- `/arckit:stakeholders` — Analyse stakeholder drivers, goals, and outcomes
- `/arckit:risk` — Risk register following HM Treasury Orange Book
- `/arckit:sobc` — Strategic Outline Business Case (Green Book 5-case)
- `/arckit:requirements` — Business and technical requirements
- `/arckit:data-model` — Data model with ERD, GDPR compliance, and governance
- `/arckit:research` — Market research with build vs buy analysis
- `/arckit:datascout` — Discover external data sources, APIs, and open data portals
- `/arckit:wardley` — Strategic Wardley Maps (plus `.value-chain`, `.climate`, `.doctrine`, `.gameplay`)
- `/arckit:adr` — Architectural decisions with options analysis

#### Cloud & Code Research
- `/arckit:aws-research` — AWS services via AWS Knowledge MCP
- `/arckit:azure-research` — Azure services via Microsoft Learn MCP
- `/arckit:gcp-research` — Google Cloud services via Google Developer Knowledge MCP
- `/arckit:gov-reuse` / `/arckit:gov-code-search` / `/arckit:gov-landscape` — UK government code reuse and landscape mapping

#### Procurement
- `/arckit:sow` — Statement of Work / RFP
- `/arckit:dos` — Digital Outcomes and Specialists procurement
- `/arckit:gcloud-search` / `/arckit:gcloud-clarify` — G-Cloud discovery and supplier clarifications
- `/arckit:evaluate` / `/arckit:score` — Vendor evaluation framework and scoring
- `/arckit:grants` — UK government grants, charitable funding, and accelerators

#### Design & Delivery
- `/arckit:diagram` — Mermaid / PlantUML C4 architecture diagrams
- `/arckit:dfd` — Yourdon-DeMarco Data Flow Diagrams
- `/arckit:hld-review` / `/arckit:dld-review` — High- and Detailed-Level Design reviews
- `/arckit:backlog` / `/arckit:trello` — Prioritised product backlog and Trello export
- `/arckit:devops` / `/arckit:finops` / `/arckit:mlops` — DevOps, FinOps, MLOps strategies
- `/arckit:operationalize` — Operational readiness pack with runbooks and DR/BCP
- `/arckit:roadmap` / `/arckit:strategy` — Architecture roadmap and executive strategy
- `/arckit:platform-design` — Platform Design Toolkit canvases
- `/arckit:data-mesh-contract` — Federated data product contracts

#### Governance & Quality
- `/arckit:traceability` — Requirements traceability matrix
- `/arckit:principles-compliance` — Principles compliance scorecard
- `/arckit:conformance` — ADR implementation and architecture drift assessment
- `/arckit:analyze` — Comprehensive governance quality analysis
- `/arckit:health` — Scan for stale artifacts, forgotten ADRs, orphan requirements
- `/arckit:impact` — Blast-radius analysis for requirement or design changes
- `/arckit:maturity-model` — Capability maturity model

#### UK Government Compliance
- `/arckit:service-assessment` — GDS Service Standard (14 points)
- `/arckit:tcop` — Technology Code of Practice
- `/arckit:ai-playbook` / `/arckit:atrs` — AI Playbook and Algorithmic Transparency Record
- `/arckit:dpia` — UK GDPR Article 35 Data Protection Impact Assessment
- `/arckit:secure` / `/arckit:mod-secure` / `/arckit:jsp-936` — Secure by Design (civilian, MOD, JSP 936)
- `/arckit:servicenow` — ServiceNow service design with CMDB and SLAs

#### EU & French Community Compliance
- `/arckit:eu-rgpd`, `/arckit:eu-nis2`, `/arckit:eu-ai-act`, `/arckit:eu-dora`, `/arckit:eu-cra`, `/arckit:eu-dsa`, `/arckit:eu-data-act`
- `/arckit:fr-rgpd`, `/arckit:fr-anssi`, `/arckit:fr-secnumcloud`, `/arckit:fr-dinum`, `/arckit:fr-dr`, `/arckit:fr-ebios`, `/arckit:fr-pssi`, `/arckit:fr-anssi-carto`, `/arckit:fr-marche-public`, `/arckit:fr-code-reuse`, `/arckit:fr-algorithme-public`

#### Reporting & Publishing
- `/arckit:story` — Project narrative with timeline and governance achievements
- `/arckit:presentation` — MARP slide deck for governance boards
- `/arckit:glossary` / `/arckit:search` — Consolidated glossary and artifact search
- `/arckit:framework` — Transform artifacts into phased framework with executive guide
- `/arckit:pages` — Generate documentation site with dashboard, viewer, and Mermaid rendering

## Project Structure

```
smart-meter-app/
├── .claude/
│   └── settings.json         # Plugin marketplace + MCP enablement
├── .mcp.json                 # Microsoft Learn and AWS Knowledge MCP servers
├── docs/
│   ├── index.html            # Generated documentation site
│   ├── manifest.json         # Document index
│   ├── health.json           # Governance health scan
│   ├── llms.txt              # LLM/agent discovery index
│   └── guides/               # Command usage guides (synced from plugin)
├── projects/
│   ├── 000-global/
│   │   ├── ARC-000-PRIN-v1.0.md   # Architecture Principles
│   │   ├── policies/              # Organisation-wide policies
│   │   └── external/              # Enterprise reference documents
│   └── 001-smart-meter-app/
│       ├── ARC-001-REQ-v1.0.md    # Requirements
│       ├── ARC-001-STKE-v1.0.md   # Stakeholder Drivers
│       ├── ARC-001-RISK-v1.0.md   # Risk Register
│       ├── ARC-001-PLAN-v1.0.md   # Project Plan
│       ├── ARC-001-DATA-v1.0.md   # Data Model
│       ├── ARC-001-DPIA-v1.0.md   # DPIA
│       ├── ARC-001-SECD-v1.0.md   # Secure by Design
│       ├── ARC-001-DSCT-v1.0.md   # Data Source Discovery
│       ├── ARC-001-RSCH-v*.md     # Research findings
│       ├── research/              # AWS/Azure/GCP research, gov reuse
│       ├── decisions/             # ADRs
│       ├── diagrams/              # Architecture diagrams
│       ├── wardley-maps/          # Wardley Maps
│       ├── reviews/               # HLD / DLD reviews
│       ├── vendors/               # Vendor profiles and submissions
│       └── external/              # External documents (PDFs, specs)
└── CLAUDE.md                 # Project instructions for Claude Code
```

ArcKit templates, scripts, commands, and agents are now provided by the [`arckit` plugin](https://tractorjuice.github.io/arc-kit/) rather than being copied into the repository.

## Documentation

- [ArcKit Documentation](https://tractorjuice.github.io/arc-kit/)
- [Smart Energy Code (SEC)](https://smartenergycodecompany.co.uk/)
- [DCC - Data Communications Company](https://www.smartdcc.co.uk/)
- [Ofgem - Smart Metering](https://www.ofgem.gov.uk/energy-policy-and-regulation/policy-and-regulatory-programmes/smart-metering)
- [Smart Energy GB](https://www.smartenergygb.org/)
