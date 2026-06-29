# Dox9+ Solution Design Template

| | |
|---|---|
| **Template Version** | 1.0.3 |
| **Dox Version** | [Dox v1.8.0](./Dox.md) |

## Table of Contents

1. [About This Template](#about-this-template)
1. [Solution Design (Dox9+ SD Template)](#solution-design)
1. [Appendix A. Maturity](#appendix-a-maturity)

---

## About This Template

**Dox9+** is a solution design template inspired by [arc42](https://arc42.org), designed to support agentic, agile, incremental, and open-ended solutioning. While particularly suited to enterprise contexts, it adapts well to projects of any scale, from startups to large organizations. Its primary audience is solution architects and technical leads, though each chapter is scoped to a specific stakeholder perspective.

Unlike arc42, Dox9+ is organized around a **chronological flow** that mirrors the design process: from business context to functional definition, from technical strategy to implementation specification. Reading the document from beginning to end should tell a coherent story of how a problem was understood and how a solution was shaped to address it.

Dox9+ is primarily focused on the technical dimension of the solution. Business and functional aspects are treated as prerequisites and are included to provide context, but the primary design effort documented here is architectural and systemic.

The nine core chapters form the backbone of a complete solution design document. Additional chapters are available to extend the template when deeper coverage of specific concerns is needed. Moreover, we define a specification [maturity model](#appendix-a-maturity) to handle scenarios where more agility is required.

Dox9+ is based on the Dox notation: type, priority, and color annotations should be used to add semantic value to assertions — see [Dox v1.8.0](./Dox.md) for the notation specification.

Dox9+ is distributed under CC BY-SA 4.0 — see [LICENSE.md](./LICENSE.md) file.

---

# Solution Design

| | |
|---|---|
| **Project** | *Project Name* |
| **Team** | *Team Name* |
| **SD Version** | *0.0.1* |
| **SD Status** | *`Draft`* |
| **Template Version** | *[Dox9+ v1.0.3](./Dox9+.md)* |
| **Maturity Model** | *`Top-Down` `Bottom-Up`* |
| **Current Maturity** | *Dox0* |
| **Target Maturity** | *Dox9* |

## Table of Contents

*This is the ToC of your Solution Design document. Choose which chapters are required according to your project type and needs. Use the Dox9+ [maturity model](#appendix-a-maturity) as a reference for measuring specification completeness.*

### Core Chapters

|  | Title | Purpose | Code | Required | Status |
|---|---|---|---|---|---|
| 1 | [Overview](#1-overview) | Introduction | `OVE` | ✅ | `Draft` |
| 2 | [Glossary](#2-glossary) | Introduction | `GLO` | ✅ | `Draft` |
| 3 | [Business View](#3-business-view) | Problem | `BUV` | ✅ | `Draft` |
| 4 | [Product View](#4-product-view) | Problem | `PRV` | ✅ | `Draft` |
| 5 | [Technical Strategy](#5-technical-strategy) | Solution | `TST` | ✅ | `Draft` |
| 6 | [Technical View](#6-technical-view) | Solution | `TEV` | ✅ | `Draft` |
| 7 | [Technical Debt & Risks](#7-technical-debt--risks) | Solution | `TDR` | ✅ | `Draft` |
| 8 | [Bill of Materials](#8-bill-of-materials) | Specification | `BOM` | ✅ | `Draft` |
| 9 | [Interface View](#9-interface-view) | Specification | `INV` | ✅ | `Draft` |
| Y | [Requirements Index](#y-requirements-index) | Governance | `RIX` | ✅ | `Draft` |
| Z | [Changelog](#z-changelog) | Governance | `CHL` | ✅ | `Draft` |

### Additional Chapters

|  | Title | Purpose | Code | Required | Status |
|---|---|---|---|---|---|
| 3a | [Business Strategy](#3a-business-strategy) | Problem | `BST` | ⬜ | `Draft` |
| 4a | [Product Strategy](#4a-product-strategy) | Problem | `PST` | ⬜ | `Draft` |
| 10 | [Quality Appendix](#10-quality) | Appendix | `AQU` | ⬜ | `Draft` |
| 11 | [Security Appendix](#11-security) | Appendix | `ASE` | ⬜ | `Draft` |
| 12 | [Privacy Appendix](#12-privacy) | Appendix | `APR` | ⬜ | `Draft` |
| 13 | [Testing Appendix](#13-testing) | Appendix | `ATE` | ⬜ | `Draft` |
| 14 | [Delivery Appendix](#14-delivery) | Appendix | `ADE` | ⬜ | `Draft` |
| 15 | [Cross-Cutting Concerns](#15-cross-cutting-concerns) | Appendix | `AC3` | ⬜ | `Draft` |
| | *Custom Chapter* | *Custom Section* | | | |

## Legend

| Field | Values |
|---|---|
| Required | ✅ Yes ⬜ No :x: Omitted |
| Status | `Draft` `Proposal` `Validated` or `N/A` if Omitted |

---

# 1. Overview

✅ `OVE`

*This chapter is the entry point of the document. It provides a project-level summary accessible to all stakeholders, regardless of their technical background. A reader who only reads this chapter should walk away with a clear understanding of why this project exists, who is involved, what it aims to achieve, and how the work is being conducted.*

## Project Description

*Briefly describe the project in non-technical language, accessible to all stakeholders. Include the problem statement, the project context, and a high-level indication of the intended solution.*

## Stakeholders

*List the stakeholders involved in or affected by this project. Include both internal and external parties. For each, briefly note their role and their relationship to the solution.*

| Name | Company | Role | Interest | Contact | Notes |
|---|---|---|---|---|---|
| *John Doe* | *MegaCorp ™* | *Project Sponsor* | *Budget approval and outcomes* | *john.doe@megacorp.com* |  |
| | | | | | |

## Methodology & Process

*Describe the design and delivery methodology in use: agile frameworks, architectural processes, governance models, or any organizational constraints that shape how the project is conducted.*

## References

*List general references relevant to the project: code repositories, external documentation, internal guidelines, related projects, standards, and so on.*

| References | Notes |
|---|---|
| *[Link 1](#)* |  |
| | |

---

# 2. Glossary

✅ `GLO`

*This chapter establishes the project's Ubiquitous Language as a shared vocabulary that eliminates ambiguity across business, product, and technical conversations. It is relevant to all stakeholders: a common language is a prerequisite for effective collaboration.*

*Every term defined here should be used consistently throughout this document and in all related communications. The glossary serves as a bridge between the language of business stakeholders and the language of the technical team: when a domain concept carries different meanings for different audiences, or when a technical term might obscure a business concept, it belongs here.*

:bulb: *Both business domain and technical terms can be defined here.*

| Term | Type | Definition | Notes |
|---|---|---|---|
| *Order* | *`Domain`* | *In our context, an Order is...* |  |
| *XSS* | *`Technical`* | *A vulnerability where...* | [OWASP](https://owasp.org/www-community/attacks/xss/) |
| | | | |

---

# 3. Business View

✅ `BUV`

*This chapter establishes the business context of the solution and is primarily addressed to business stakeholders and project sponsors. Its central concern is scope: what is inside the boundary of this solution, and what is explicitly outside. The requirements produced here — goals, business requirements, and business constraints — are the starting point for all subsequent design work.*

## Solution Context & Scope

*Describe the business context of the solution. State the solution boundary clearly: any ambiguity here propagates throughout the entire document. The language should remain accessible to business stakeholders and project sponsors, avoiding unnecessary technical detail.*

### Business Context Diagram

*Provide a Business Context Diagram to visually represent the system boundary and its relationships with external actors. This is meant to be a first-impact view for stakeholders. Focus on operations and I/O data flows at a business level, not on technical aspects.*

## Business Strategy

*Rationale and decisions, in the form of Business Decision Records (BDRs), that gave birth to the requirements below. This section focuses on how assumptions and options get promoted into business requirements. Unresolved open points, if any, should also be mentioned here.*

> **[D 1]** *Example business decision.*

:bulb: *Keep this section concise: if the business design process is articulated enough to warrant more depth, promote this section to a standalone prepended chapter — see [3a. Business Strategy](#3a-business-strategy).*

## Requirements

### Assumptions & Facts

*Explicit business assumptions that have not yet been validated but are being treated as true for the purposes of this design. Indicate proper facts that originated from validating business assumptions.*

> **[A 1]** *Example business assumption.*

> **[F 1]** *Example business fact.*

### Business Constraints

*Explicit constraints that originate at the business level and limit degrees of freedom for the entire design process.*

> **[C 1]** *Example business constraint.*

### Business Requirements & Project Goals

*Include the goals of the project as explicit assertions, along with the business requirements that define what the organization expects from the solution. Surface quality requirements that originate at the business level. Where possible, enrich requirements with explicit priority annotation, emphasizing what falls inside and what outside the scope of this solution.*

> **[G 1 !M]** *Example goal.*

> **[BR 1 !S]** *Example business requirement.*

> **[QBR 1 !C]** *Example business quality requirement.*

## References

*Link relevant business documentation such as BRDs, process maps, regulatory references, stakeholder presentations, and so on.*

| References | Notes |
|---|---|
| *[Link 1](#)* |  |
| | |

---

# 4. Product View

✅ `PRV`

*This chapter describes the product identified to satisfy the business requirements. It is primarily addressed to product designers, business analysts, and stakeholders who need to understand what the system does and for whom. The requirements produced here — functional requirements and related quality requirements — are the direct input for the technical design.*

## Overview

*Briefly describe the product identified to satisfy the business requirements. State its functional boundary: what the product does and, where useful, what it explicitly does not do.*

## Product Strategy

*Rationale and decisions, in the form of Product Decision Records (PDRs), that gave birth to the requirements below. This section focuses on how assumptions and options get promoted into functional requirements. Unresolved open points, if any, should also be mentioned here.*

> **[D 1]** *Example product decision.*

:bulb: *Keep this section concise: if the product design process is articulated enough to warrant more depth, promote this section to a standalone prepended chapter — see [4a. Product Strategy](#4a-product-strategy).*

## Actors

*List all actors that interact with the solution. We consider actors both humans and systems. Specify their nature and their interest, giving an overview of their role and permitted operations.*

| Actor | Type | Interest | Notes |
|---|---|---|---|
| *Employee* | *`User`* | *Resolve issues that...* |  |
| *ERP* | *`System`* | *Provide business data...* |  |
| *Invoice Analyzer* | *`Agent`* | *Process documents containing...* |  |
| *Administrator* | *`User`* | *Manage the system...* |  |
| | | | |

## Domain Model

*Conceptual representation of the domain entities, relationships and events, as they emerge from the functional analysis. Use Entity-Relationship (E/R) diagrams or other domain modelling notations such as UML. This model should be consistent with the Ubiquitous Language defined in `GLO` and support the functional requirements below.*

*For each concept, highlight whether it involves personal, sensitive or confidential data: this information feeds the Data Protection section in `TEV` and the optional `APR` chapter.*

## Requirements

### Assumptions & Facts

*Explicit product assumptions that have not yet been validated but are being treated as true for the purposes of this design. Indicate proper facts that originated from validating product assumptions.*

> **[A 1]** *Example product assumption.*

> **[F 1]** *Example product fact.*

### Product Constraints

*Explicit constraints that originate at a functional level and must be respected by all product requirements.*

> **[C 1]** *Example product constraint.*

### Product Requirements

*Functional requirements and related quality requirements are the focus of this chapter. Gherkin BDD notation is encouraged for behavioral specifications. Where possible, enrich requirements with explicit priority annotation, emphasizing what falls inside and what outside the scope of this solution. Include here Use Case diagrams or other representations if useful.*

> **[FR 1]** *Example functional requirement. **Given** [context] | **when** [event] | **then** [outcome].*

> **[QFR 2]** *Example functional quality requirement.*

### Interactions Detail

:bulb: *This section can be omitted if the representation made above through requirements is clear and detailed enough. You can avoid unnecessary redundancy as a general rule.*

 *Include here activity diagrams, state diagrams or other workflow diagrams to clarify complex interactions. UI prototypes, wireframes, and mockups are also appropriate here to describe the user behavior and expectations.*
 
 *For requirements that benefit from a structured narrative, when diagrams are not available or when a diagram alone does not capture the necessary detail, you can use the Story Card format below.*

| Story Card | *`Card 1`* |
|---|---|
| **Requirements** | *`FR 1` `FR 2` `BR 1`* |
| **Actors** | *User, Administrator, ...* |
| **Preconditions** | *The User must have...* |
| **Postconditions** | *The system must have...* |
| **Event Flow** | *The User will...* |
| **Notes** | *Some useful notes...* |

## References

*Link relevant product documentation such as FRDs/FSDs, product briefs, user research, product acceptance criteria, and so on.*

| References | Notes |
|---|---|
| *[Link 1](#)* |  |
| | |

---

# 5. Technical Strategy

✅ `TST`

*This chapter is the core of the solution design process from a technical standpoint. It documents how the team reasoned from product requirements to technical decisions: starting from options and open points, navigating constraints and quality requirements, and arriving at a coherent set of architectural decisions. It is primarily addressed to solution architects and technical leads.*

*Technical options are evaluated and decisions are recorded as standalone Architectural Decision Records (ADRs), referenced here. Along the way, technical constraints and quality requirements are surfaced and made explicit. These decisions and information collectively produce the technical requirements that drive the Technical View.*

## Assumptions & Facts

*Explicit technical assumptions that have not yet been validated but are being treated as true for the purposes of this technical design. Indicate proper facts that originated from validating technical assumptions.*

> **[A 1]** *Example technical assumption.*

> **[F 1]** *Example technical fact.*

## Options & Open Points

*Explicit here options still under evaluation and open points not yet resolved. These represent the current design frontier: decisions that have not been reached yet. Promote to decisions once resolved.*

> **[O 1]** *Example option.*

> **[Opn 1]** *Example open point to resolve.*

## Technical Decisions

*Record each significant architectural decision. Decisions can be documented inline here or backed by a standalone ADR for cases that warrant full documentation: complex trade-offs, high-impact choices, and so on. In either case, reference the relevant constraints, options, and open points that led to the decision.*

> **[D 1]** *Example inline decision.*

> **[D 2]** *Example complex decision. See ADR 1.*

### Decision Records

*Index of standalone decision records produced during the technical design process. Full documentation for each record is maintained outside of this chapter.*

| Record | Title | Status | Notes |
|---|---|---|---|
| *[ADR 1](./adr/ADR-1.md)* | *Choose the solution stack* | *`Pending` `Open` `Closed` `Reopened`* |  |

## Requirements

### Technical Constraints

*Explicit constraints that bound the solution space. These may originate from infrastructure, security policy, compliance, organizational standards, inherited system dependencies, etc.*

> **[C 1]** *Example technical constraint.*

### Technical Requirements

*Explicit Technical Requirements produced by the decisions and constraints above. These represent the technical obligations that the system must fulfill, as derived from the strategy. Surface relevant technical quality requirements here as well.*

> **[TR 1]** *Example technical requirement.*

> **[QTR 1]** *Example technical quality requirement.*

## References

*Link relevant documentation that the designers used to support design choices, such as technology radars, vendor assessments, benchmark results, and proof-of-concept reports.*

| References | Notes |
|---|---|
| *[Link 1](#)* |  |
| | |

---

# 6. Technical View

✅ `TEV`

*This chapter translates the strategy from `TST` into a concrete structural and behavioral picture of the system: what components exist, how they relate, where they run, and how they interact at runtime. It is the primary reference for developers, architects and infrastructure engineers.*

*The technical boundary must be stated explicitly. The C4 model is recommended for context and container diagrams. Drilling down to component or code level is not mandatory in general: it should be done only for mature or critical subsystems that present architectural peculiarities worth documenting.*

## Building Blocks

:bulb: *This section can be omitted if the representation made inside the following Technical Context section is clear and detailed enough. You can avoid unnecessary redundancy as a general rule.*

*Applications, components, services, and modules that make up the solution. List here logical entities such as systems, microservices, managed services (PaaS), third-party platforms (SaaS), and so on, with their responsibilities and interdependencies.*

:bulb: *Feel free to define your own BB types and other conventions based on your organization.*

| ID | Name | Type | Responsibility | Inside Of | Consumed By | Depends On | Status | Notes |
|---|---|---|---|---|---|---|---|---|
| *`BB 1`* | **_MegaApp_** | *`Application`* | *Our app allows to...* | *-* | *Employee* | *ERP* | *`Existing` from R 1.0.0* |  |
| *`BB 2`* | *Frontend* | *`SPA`* | *Expose web UI for...* | *MegaApp* | *Employee* | *Backend* | *`New` in R 2.0.0* |  |
| *`BB 3`* | *Backend* | *`Microservice` `PaaS`* | *Manage workflows for...* | *MegaApp* | *Frontend* | *Storage* | *`Existing` from R 1.0.0* |  |
| *`BB 4`* | *Storage* | *`Database` `DBaaS`* | *Store user data in...* | *MegaApp* | *Backend* | *-* | *`New` in R 2.0.0* |  |
| *`BB 5`* | *ERP* | *`External` `SaaS`* | *Provide data to...* | *-* | *MegaApp* | `Unknown` | *`Existing`* |  |
| | | | | | | | | |

## Integrations Map

:bulb: *This section can be omitted if the Building Blocks section above is omitted, or if the representation made in the Technical Context section below is clear and detailed enough. Avoid unnecessary redundancy as a general rule.*

*Inbound and outbound interactions or integrations between this solution and external users or systems. Reference the building blocks defined above. For each integration, describe the direction, protocol, and nature of the data exchange.*

:bulb: *Feel free to define your own values and conventions based on your organization.*

| ID | Direction | Actor | Description | Type | Protocol | Security | Status | Notes |
|---|---|---|---|---|---|---|---|---|
| *`ITG 1`* | *`Inbound`* | *Employee* | *User interacts with...* | *`sync`* | *`https`* | *`OAuth2.1`* | *`New` in R 2.0.0* |  |
| *`ITG 2`* | *`Outbound`* | *ERP* | *Fetch business data from...* | *`async`* | *`rest api`* | *`Basic Auth`* | *`Existing` from R 1.0.0* |  |
| | | | | | | | | |

## Technical Context

### Technical Context Diagram

*C4 System Context and Container diagrams. Explicitly mark the system boundary: what is inside and what is outside this solution. Drill down to deeper levels of detail (Component, Code) if useful.*

#### Deployment Diagram

:bulb: *This section can be omitted. Provide a dedicated diagram if the deployment topology is non-trivial or not fully captured by the context diagram. A textual description is acceptable when the topology is straightforward.*

#### Networking & Routing Diagram

:bulb: *This section can be omitted. Provide a dedicated diagram if network topology or boundary components require dedicated representation, not fully captured by the context diagram. A textual description is acceptable when the configuration is straightforward. Consider documenting here proxies, reverse proxies, API gateways etc, making relevant configuration explicit across every layer of the network stack.*

### Security & Privacy

*Describe the security model of the solution and its integrations, in prose or through appropriate diagrams. Security information should always be present in the core document. If the project involves complex security requirements the full treatment belongs in the optional [11. Security Appendix](#11-security) chapter.*

#### Authentication & Identity Management

*Describe how actors authenticate. Reference the identity provider(s) in use, the authentication protocols, and any relevant flows.*

#### Authorization & Access Policies

*Describe the authorization model for users and machines: role-based, attribute-based, policy-based, or other. Identify which components enforce access control and on what basis. Where applicable, describe user profile management.*

#### Data Protection

*Describe which personal, sensitive or confidential data the system processes, where it flows, and how it is protected. If the project requires a full privacy impact assessment or involves complex data residency requirements, the full treatment belongs in the optional [12. Privacy Appendix](#12-privacy) chapter.*

### Interactions Matrix

:bulb: *This section can be omitted if the representation made in the sections above is clear and detailed enough. You can avoid unnecessary redundancy as a general rule.*

*A matrix covering all exchanges within the solution boundary, including internal block-to-block interactions not captured in the Integrations Map above (which focuses on external integrations only).*

:bulb: *Feel free to define your own values and conventions based on your organization.*

| ID | Source | Target | Description | Type | Protocol | Security | Status | Notes |
|---|---|---|---|---|---|---|---|---|
| *`INT 1`* | *Employee* | *Frontend* | *User interacts with...* | *`async`* | *`https`* | *`OAuth2.1`* | *`New` in R 2.0.0* |  |
| *`INT 2`* | *Frontend* | *Backend* | *Frontend delegates to...* | *`sync`* | *`rest api`* | *`OAuth2.1`* | *`New` in R 2.0.0* |  |
| *`INT 3`* | *Backend* | *Storage* | *Read and write user data...* | *`sync`* | *`jdbc`* | *`None`* | *`New` in R 2.0.0* |  |
| *`INT 4`* | *Backend* | *ERP* | *Fetch business data from...* | *`async`* | *`rest api`* | *`Basic Auth`* | *`Existing` from R 1.0.0* |  |
| | | | | | | | | |

## Runtime Views

:bulb: *This section can be omitted if the runtime flows can be easily inferred from the diagrams above. You can avoid unnecessary redundancy as a general rule.*

*Include here key runtime interactions between components for the most significant technical flows, using sequence or activity diagrams in a technical level of detail.*

## References

*Link relevant documentation that can help to clarify building blocks, integrations, runtime flows or any other aspect treated in the previous sections.*

| References | Notes |
|---|---|
| *[Link 1](#)* |  |
| | |

---

# 7. Technical Debt & Risks

✅ `TDR`

*Register of all known debt and risks identified during the design process. Entries represent situations that are accepted, deferred, or unresolved at the time of writing, and should be traceable to information in the preceding chapters. This chapter is primarily addressed to technical leads, architects and project managers.*

## Technical Debt

:bulb: *Feel free to define your own values and conventions based on your organization.*

| ID | Name | Type | Source | Description | Detail |
|---|---|---|---|---|---|
| *`Dbt 1`* | *Hardcoded credentials* | *`Security`* | *Backend* | *API keys stored in...* | *[Dbt 1](./dbt/Dbt-1.md)* |
| *`Dbt 2`* | *Missing documentation* | *`Docs`* | *`TST`* | *Some choices were not documented...* |  |
| | | | | | |

## Risks

:bulb: *Feel free to define your own values and conventions based on your organization.*

| ID | Name | Type | Source | Description | Likelihood | Impact | Detail |
|---|---|---|---|---|---|---|---|
| *`Rsk 1`* | *Credential exposure* | *`Security`* | *[Dbt 1](#)* | *Hardcoded credentials may...* | *`Medium`* | *`High`* |  |
| *`Rsk 2`* | *ERP API discontinuation* | *`Cost`* | *ERP* | *The ERP vendor may...* | *`Low`* | *`Medium`* | *[Rsk 2](./rsk/Rsk-2.md)* |
| | | | | | | | |

---

# 8. Bill of Materials

✅ `BOM`

*Internal operational specification of the system: everything needed to run, operate, and maintain the solution across all environments.* 

*In enterprise contexts, this chapter feeds the provisioning process: it is the interface between the solution design and the departments responsible for infrastructure, CI/CD, security, and so on. It is primarily addressed to infrastructure engineers, DevOps teams, etc.*

:bulb: *Keep this document current and maintain consistency as the solution evolves: highlight as-is, to-be and dismissed resources.*

## Environments

*All environments required by the solution (e.g. development, staging, production) and their key characteristics.*

| Name | Status | Notes |
|---|---|---|
| `development` | *`Existing` from R 1.0.0* |  |
| `staging` | *`Existing` from R 1.0.0* |  |
| `production` | *`New` in R 2.0.0* |  |
| | | |

## External Dependencies

*External systems and services that this solution consumes (outbound integrations). This list should be consistent with the Integrations Map in `TEV`.*

:bulb: *Feel free to define your own values and conventions based on your organization.*

| Actor | Owner | Type | Protocol | Security | Environments | Configuration | Usage | SLAs | Status | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| *ERP* | *Some Corp.* | *`External` `SaaS`* | *`rest api`* | *`Basic Auth`* | *`dev` `staging` `production`* | *Base URL, API endpoints...* | *~200 calls/day* | *99.5% uptime* | *`Existing` from R 1.0.0* |  |
| | | | | | | | | | | |

## Internal Resources & Configuration

*Internal components, services and configurations that must be provisioned or managed. Include configuration rules and parameters specific to each environment.*

:bulb: *Feel free to define your own values and conventions based on your organization.*

| Name | Type | Environments | Configuration | Status | Notes |
|---|---|---|---|---|---|
| *Frontend* | *`SPA`* | *`dev` `staging` `production`* | *Base URL, API endpoints...* | *`New` in R 2.0.0* |  |
| *Backend* | *`Microservice` `PaaS`* | *`dev` `staging` `production`* | *DB connection string, timeout...* | *`Existing` from R 1.0.0* |  |
| *Storage* | *`Database` `DBaaS`* | *`dev` `staging` `production`* | *Retention policy, backup schedule...* | *`New` in R 2.0.0* |  |
| *Firewall Rule* | *`Configuration`* | *`dev` `staging` `production`* | *Allow access from... to IP...* | *`Existing` from R 1.0.0* |  |
| | | | | | |

## Expected Consumers

*Users or systems that consume this solution's interfaces or services (inbound integrations). This list should be consistent with the Integrations Map in `TEV`.*

:bulb: *Note that new consumers can always emerge after the initial design: use judgment to decide the appropriate level of detail here. Documenting individual consumers makes more sense for point-to-point integrations, while a solution with many generic consumers (e.g. a platform API or a shared service) may only need to document broader actor categories.* 

:bulb: *Feel free to define your own values and conventions based on your organization.*

| Consumer | Type | Protocol | Security | Environments | Usage | SLAs | Status | Notes |
|---|---|---|---|---|---|---|---|---|
| *Employee* | *`User`* | *`https`* | *`OAuth2.1`* | *`dev` `staging` `production`* | *~500 users/day* | *99.9% uptime* | *`New` in R 2.0.0* |  |
| | | | | | | | | |

## References

*Link relevant documentation that can help to clarify operational aspects to all stakeholders involved in solution provisioning and delivery.*

| References | Notes |
|---|---|
| *[Link 1](#)* |  |
| | |

---

# 9. Interface View

✅ `INV`

*External specification of the solution: what others need in order to use it. Where the Bill of Materials describes what is needed to run the system, this chapter describes what the system exposes to the outside world. It is primarily addressed to consuming teams and integration partners.*

*Provide API contracts (e.g. OpenAPI/Swagger references), communication protocols, integration conventions, and inter-team agreements. Address authentication requirements, versioning policies, quotas, rate limits, SLAs, and any conventions that consumers must follow.*

:bulb: *Feel free to define your own values and conventions based on your organization.*

| Name | Version | Owner | Type | Protocol | Security | Environments | Usage | SLAs | Status | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| *MegaApp API* | *`v1.0`* | *Team Name* | *`REST API`* | *`https`* | *`OAuth2.1`* | *`dev` `staging` `production`* | *Rate limit 100 req/s* | *99.9% uptime* | *`Existing` from R 1.0.0* |  |
| | | | | | | | | | | |

## References

*Link relevant documentation such as integration guides, additional onboarding documentation, etc.*

| References | Notes |
|---|---|
| *[Link 1](#)* |  |
| | |

---

# Y. Requirements Index

✅ `RIX`

*Consolidated, searchable index of all requirements and significant assertions recorded across this document. Maintained as a living summary: whenever the spec is updated, this index should be updated to remain consistent. Its purpose is rapid lookup. Constraints and quality requirements may appear in any section below, classified by the primary type they qualify.*

## Assumptions, Options & Facts

> **[A]** *Example assumption.*

> **[O]** *Example option.*

> **[F]** *Example fact.*

## Business Requirements & Goals

> **[C]** *Example business constraint.*

> **[BR]** *Example business requirement.*

> **[QR]** *Example business quality requirement.*

> **[G]** *Example business goal.*

## Product Requirements

> **[C]** *Example product constraint.*

> **[FR]** *Example functional requirement.*

> **[QR]** *Example functional quality requirement.*

## Technical Requirements

> **[C]** *Example technical constraint.*

> **[TR]** *Example technical requirement.*

> **[QR]** *Example technical quality requirement.*

## Other Requirements

> **[R]** *Example generic requirement.*

> **[QR]** *Example generic quality requirement.*

## Open Points

*Treat this section as a backlog of unresolved issues. Remove entries when resolved.*

> **[Opn]** *Example open point.*

---

# Z. Changelog

✅ `CHL`

*Records the evolution of the solution design over time.*

*Granularity is not that of a Git commit log: this chapter tracks changes that are significant in terms of solution meaning — decisions made, strategies revised, requirements promoted or deprecated, scope changes. The goal is to make the reasoning behind the current state of the document reconstructable at any future point. Each entry should be self-contained enough to understand what changed and why.*

:bulb: *Possible values for Type are `Decision`, `Requirement`, `Scope`, `Strategy`, `Correction`, `Deprecation`, `Other` and so on. Feel free to define your own values and conventions based on your organization.*

| SD Version | Date | Author | Type | Chapters | Description |
|---|---|---|---|---|---|
| *`1.1.0`* | *2026-01-15* | *M. Poppins* | *`Scope`* | *`BUV` `PRV`* | *Narrowed solution scope to exclude...* |
| *`1.0.1`* | *2026-01-20* | *M. Poppins* | *`Decision`* | *`TST` `TEV`* | *Adopted DBaaS for storage. See [ADR 1](./adr/ADR-1.md).* |
| *`1.0.0`* | *2025-06-01* | *M. Poppins* | *`Requirement`* | *`TEV`* | *Added TR for OAuth2.1 login flow.* |
| | | | | | |

---

# 3a. Business Strategy

⬜ `BST`

*Standalone expansion of the Business Strategy section in `BUV`. Use this chapter when the business design process is articulated enough to warrant dedicated documentation: multiple competing options, complex stakeholder alignment, significant assumptions requiring validation, or explicit Business Decision Records (BDRs) that need to be traceable over time.*

*This chapter focuses on how assumptions and options get promoted into business requirements. Document options, open points and decisions using BDRs. When this chapter is present, the Business Strategy section in `BUV` should contain a reference here and keep only a brief summary. The structure and approach of this chapter mirror those of `TST`.*

---

# 4a. Product Strategy

⬜ `PST`

*Standalone expansion of the Product Strategy section in `PRV`. Use this chapter when the functional design process is complex enough to require dedicated documentation: significant product decisions with competing alternatives, user research outcomes, or Product Decision Records (PDRs) that need to be preserved for traceability.*

*This chapter focuses on how assumptions and options get promoted into product requirements. Document options, open points and decisions as PDRs. When this chapter is present, the Product Strategy section in `PRV` should contain a reference here and keep only a brief summary. The structure and approach of this chapter mirror those of `TST`.*

---

# 10. Quality

⬜ `AQU`

*Drill-down on quality requirements that warrant more structured treatment. For each requirement, document the relevant ISO 25010 characteristic, the acceptance criteria, and the specific business, functional, or technical requirement it serves. Typical areas include: performance, usability and accessibility, fault tolerance and resilience, maintainability and testability, and observability.*

---

# 11. Security

⬜ `ASE`

*Drill-down on security, intended for projects that involve complex security models. Expands on the Security Overview in `TEV` without replacing it. This chapter is primarily addressed to security architects and compliance officers.*

*Cover the following areas as relevant to the project, among others:*

- *Threat modeling: attack surface analysis, network exposure, and entry points.*
- *Authentication and authorization architecture: flows, token lifecycle, permissions, privilege escalation controls.*
- *Data protection: encryption at rest and in transit, key management.*
- *Compliance obligations: e.g. ISO 27001, SOC 2, NIS2, and their specific requirements.*
- *Security-specific design decisions and their rationale (ADRs).*

---

# 12. Privacy

⬜ `APR`

*Drill-down on privacy, intended for projects that process personal or sensitive data under regulatory obligations (e.g. GDPR, CCPA, HIPAA). Expands on the Privacy Overview in `TEV` without replacing it. This chapter is primarily addressed to privacy officers, legal teams, and data governance stakeholders.*

*Cover the following areas as relevant to the project, among others:*

- *Data inventory: what personal or sensitive data is collected, where it is stored, how it flows through the system.*
- *Consent management: how consent is collected, recorded, and propagated.*
- *Retention and deletion policies: lifecycle of personal data across all storage systems.*
- *Compliance obligations: e.g. GDPR, CCPA, HIPAA, and their specific requirements.*
- *Privacy-specific design decisions and their rationale (ADRs).*

---

# 13. Testing

⬜ `ATE`

*Drill-down on the testing strategy for the solution. This chapter covers all relevant testing concerns, from low-level unit tests to end-to-end validation. Define here the testing approach for each layer: unit testing conventions, integration testing strategy (including interactions with external systems and consumers), user acceptance testing (UAT), and performance and load testing. Where applicable, document product experimentation practices such as A/B testing or feature flagging. For each area, specify the tools, environments, and success criteria in use.*

---

# 14. Delivery

⬜ `ADE`

*Drill-down on the delivery mechanisms and DevOps practices that support the solution lifecycle. Document here the CI/CD pipeline design, branching and release management strategies, environment promotion flows, and infrastructure provisioning approaches — including Infrastructure as Code tooling and conventions. Where applicable, cover deployment patterns (blue/green, canary, rolling), rollback procedures, and any automation relevant to the day-to-day operation of the solution.*

---

# 15. Cross-Cutting Concerns

⬜ `AC3`

*Drill-down on aspects that cut across multiple components and layers of the solution and do not belong naturally to any single chapter. Use this chapter to document decisions and conventions that apply globally and must be consistent across the entire codebase and architecture. Typical examples include: architecture and software patterns, coding and naming conventions, error handling strategies, and shared styling or structural guidelines. When a concern is significant enough to warrant its own dedicated chapter, consider promoting it to a standalone appendix.*

---

*— End of Dox9+ Template —*

---

# Appendix A. Maturity

This appendix defines Dox9+ *specification maturity models*: two grading systems for measuring the completeness of a Solution Design document and calibrating the documentation effort to the actual needs of a project.

Feel free to choose which model to adopt and what target maturity level to set, on a per-project basis, according to your organization's needs.

## Top-Down Maturity Model

### Rationale

The top-down model reflects the ideal design sequence: business context first, then functional definition, then technical strategy, then implementation detail. This is the order in which a well-structured project would naturally produce documentation, and the order in which Dox9+ chapters are organized.

This model suits projects where the design process is front-loaded: requirements are articulated before development begins, stakeholders are aligned early, and architectural decisions are made deliberately rather than reactively. It is also the natural fit for regulated or high-stakes contexts where documentation is a prerequisite for approval rather than a retrospective artifact.

### Levels

The model defines ten levels, from Dox0 (empty) to Dox9 (full specification). Each level is cumulative: it includes all chapters from all preceding levels.

| Level | Chapters | Description |
|---|---|---|
| Dox0 | — | Document scaffolding is in place. `CHL` is initialized with a setup record. No content has been produced yet. |
| Dox1 | `OVE` | The project has a name, a stakeholder list, and a high-level description. Enough to orient any reader. |
| Dox2 | + `GLO` | A shared vocabulary is established. The document can now communicate unambiguously across disciplines. |
| Dox3 | + `BUV` | The business context is documented: goals, constraints, and scope are explicit. `RIX` becomes meaningful from this level. |
| Dox4 | + `PRV` | The functional scope is documented: actors, domain model, and product requirements are in place. |
| Dox5 | + `TST` | Technical decisions are recorded and requirements are formally stated. |
| Dox6 | + `TEV` | The architecture is documented: building blocks, integrations, and the technical boundary are defined. |
| Dox7 | + `TDR` | Known debt and risks are tracked explicitly. The solution is honest about its current limitations. |
| Dox8 | + `BOM` | The solution can be provisioned: environments, dependencies, and consumers are fully specified. |
| Dox9 | + `INV` | The solution exposes a documented interface: consuming teams have everything they need to integrate. |

#### Notes on Level Ordering

The progression from Dox2 to Dox4 follows the top-down narrative: shared language, business context, then functional scope. These chapters establish *why* the solution exists and *what* it should do, before any technical decisions are made.

From Dox5 onward, the model progressively adds technical depth: strategy, structure, risk, and finally the operational detail required to provision, run and integrate with the solution. A document at Dox9 should read as a coherent narrative from business intent to implementation detail, reflecting the full chronological flow that Dox9+ is designed to support.

Optional chapters (10–15, 3a, 4a) and even custom chapters can be added in any order, driven by project needs. In that case, the document is simply considered Dox9+.

### Summary Table

| Level | OVE | GLO | BUV | PRV | TST | TEV | TDR | BOM | INV | RIX | CHL |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Dox0 | | | | | | | | | | | ✅ |
| Dox1 | ✅ | | | | | | | | | | ✅ |
| Dox2 | ✅ | ✅ | | | | | | | | | ✅ |
| Dox3 | ✅ | ✅ | ✅ | | | | | | | ✅ | ✅ |
| Dox4 | ✅ | ✅ | ✅ | ✅ | | | | | | ✅ | ✅ |
| Dox5 | ✅ | ✅ | ✅ | ✅ | ✅ | | | | | ✅ | ✅ |
| Dox6 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | | | | ✅ | ✅ |
| Dox7 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | | | ✅ | ✅ |
| Dox8 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | | ✅ | ✅ |
| Dox9 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

## Bottom-Up Maturity Model

### Rationale

In an ideal world, a solution design would be written top-down: business context first, then functional definition, then technical strategy, then implementation detail. The chronological structure of Dox9+ reflects exactly this flow.

In practice, developers tend to start from the operational end — provisioning environments, defining interfaces, sketching the architecture — and defer higher-level documentation until the solution is more stable. This is not necessarily a problem: it reflects how real teams work, especially in agile contexts. What matters is that, as the document matures, its contents converge toward a coherent and traceable narrative, even if the chapters were not filled in chronological order.

The maturity model accommodates this reality. It allows a team to start with the bare minimum and grow the documentation incrementally, without prescribing when each chapter must be written. What it does prescribe is a meaningful order of *value*: which chapters unlock the most utility at each stage.

The model is also useful in regulated environments, where governance processes require a minimum level of technical documentation before a solution can be approved or deployed. In those contexts, the maturity level can serve as a formal gate, allowing work to begin without requiring a complete specification upfront.

### Levels

The model defines ten levels, from Dox0 (empty) to Dox9 (full specification). Each level is cumulative: it includes all chapters from all preceding levels.

| Level | Chapters | Description |
|---|---|---|
| Dox0 | — | Document scaffolding is in place. `CHL` is initialized with a setup record. No content has been produced yet. |
| Dox1 | `OVE` | The project has a name, a stakeholder list, and a high-level description. Enough to orient any reader. |
| Dox2 | + `BOM` | A *proof-of-concept* or *early-stage solution* can be provisioned: environments, dependencies, and consumers are specified. |
| Dox3 | + `TEV` | An *high-level architecture* is documented: building blocks, integrations, and the technical boundary are defined. |
| Dox4 | + `INV` | The solution exposes a documented interface: consuming teams have everything they need to integrate. |
| Dox5 | + `TST` | Technical decisions are recorded and requirements are formally stated. `RIX` becomes meaningful from this level. |
| Dox6 | + `TDR` | Known debt and risks are tracked explicitly. The solution is honest about its current limitations. |
| Dox7 | + `PRV` | The functional scope is *retroactively* documented: actors, domain model, and product requirements are in place. |
| Dox8 | + `BUV` | The business context is also *retroactively* documented: goals, constraints, and scope are made explicit. |
| Dox9 | + `GLO` | The solution design is complete. A shared vocabulary is established and the document tells a coherent end-to-end story. |

#### Notes on Level Ordering

The progression from Dox2 to Dox6 follows a bottom-up order: from operational detail (BOM) up to technical strategy (TST). This is intentional. These are the chapters that developers typically write first, and they can stand alone as a useful technical record even without business or product context.

From Dox7 onward, the model adds context: the product and business chapters that explain *why* the technical choices were made. A document at Dox9 should read as a coherent narrative from business intent to implementation detail, regardless of the order in which its chapters were actually written.

Optional chapters (10–15, 3a, 4a) and even custom chapters can be added in any order, driven by project needs. In that case, the document is simply considered Dox9+.

### Summary Table

| Level | OVE | BOM | TEV | INV | TST | TDR | PRV | BUV | GLO | RIX | CHL |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Dox0 | | | | | | | | | | | ✅ |
| Dox1 | ✅ | | | | | | | | | | ✅ |
| Dox2 | ✅ | ✅ | | | | | | | | | ✅ |
| Dox3 | ✅ | ✅ | ✅ | | | | | | | | ✅ |
| Dox4 | ✅ | ✅ | ✅ | ✅ | | | | | | | ✅ |
| Dox5 | ✅ | ✅ | ✅ | ✅ | ✅ | | | | | ✅ | ✅ |
| Dox6 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | | | | ✅ | ✅ |
| Dox7 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | | | ✅ | ✅ |
| Dox8 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | | ✅ | ✅ |
| Dox9 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
