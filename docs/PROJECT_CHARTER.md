# Project Charter - Marketplace Data Platform

| | |
|---|---|
| Project | `marketplace-data-platform` |
| Project reference | MDP-001 |
| Document | docs/PROJECT_CHARTER.md |
| Approved version | 1.0 |
| Updated | 19 November 2026 |
| Approver | Project Lead / Senior Data Engineer |
| Decision | Approved |
| Approval date | 19 November 2026 |

## 1. What I'm building

I want to build a data platform that takes information from different marketplace-related sources, processes it in a reliable way and turns it into useful insights through dashboards.

I'm starting with the Irish property market because there are real datasets available to work with. The Property Price Register has recorded property transactions, while the CSO publishes an official Residential Property Price Index (RPPI). The two datasets tell different parts of the story. I want to bring them into one product without treating them as interchangeable.

The longer-term plan is to expand the platform to other marketplace areas, such as vehicles and second-hand goods, and potentially adapt it for India. That's a future direction, **not** a commitment to deliver everything in the first release.

This project is also a way for me to work through the full data engineering lifecycle: understanding requirements, assessing sources, designing the solution, building pipelines, testing them and making the results accessible.

## 2. What I want to achieve

1. Build repeatable ingestion and transformation pipelines using approved datasets.
2. Use Databricks, PySpark, SQL and Delta tables to create reliable Bronze, Silver and Gold layers.
3. Define metrics clearly and show how each published result can be traced back to its source.
4. Build a public, read-only dashboard that makes the data useful without exposing raw addresses or infrastructure credentials.
5. Follow a structured delivery process with requirements, design decisions, testing, documentation and release checks.
6. Keep the core platform reusable so new countries and marketplace domains can be added without redesigning everything.

## 3. Release 1 - Ireland Property Intelligence

**Included in Release 1**

- PSRA Property Price Register transaction data, once source access and permitted reuse have been confirmed.
- A selected CSO Residential Property Price Index series, with exact dimensions confirmed during data discovery.
- Controlled data ingestion, source snapshots and batch tracking.
- Databricks Delta Bronze, Silver and Gold layers, with validation and reconciliation checks.
- Agreed transaction counts, median recorded sale prices and a **separate** official RPPI view.
- Approved, versioned aggregate exports for the dashboard.
- A public dashboard on GitHub Pages, plus source code, tests and documentation in GitHub.
- A runbook that explains how to process, validate and publish a new dataset version.

**Not included in Release 1**

- Direct listing feeds that require permission or unauthorised extraction from third-party sites.
- Asking-price, rental, listing-demand or click/conversion metrics without suitable data.
- Vehicle and second-hand-goods datasets, an India rollout, streaming, live Databricks queries or machine-learning predictions.
- Paid cloud infrastructure, authenticated accounts or a second mandatory dashboard.
- Publishing raw property addresses or unapproved record-level data.

## 4. How I'm running the project

I'm acting as the **Project Lead and Data Engineer**. I'll make the final decisions on scope and design, write the PySpark and SQL, test the pipelines and maintain the repository.

I'll use structured reviews for business requirements, architecture and QA. ChatGPT can take different review roles during those discussions. Codex can help me review code and build the dashboard against the agreed requirements and data contract. I'll still review and validate the results before accepting them.

I don't want to start implementation just because a tool or dataset is available. Requirements and design should guide the engineering work. If something needs to change later, I'll record why and what else it affects.

| Stakeholder | Role in the product | Responsibility |
|---|---|---|
| Product Sponsor / Product Owner | ChatGPT | Define business value, prioritise capabilities, evaluate business acceptance |
| Property Market Analyst | Property Market Analyst | Analyse residential property transaction trends and regional differences |
| Public Researcher / Prospective Buyer | Secondary target user persona | Explore Irish property market trends through an accessible dashboard |
| Senior Data Engineer / Project Lead | gautamibhat | Lead technical implementation and make final project decisions |
| Data Architect / Solution Architect | ChatGPT | Architecture, modelling standards, data contracts and design reviews |
| Business Analyst | ChatGPT | Business requirements, KPI definitions, use cases and traceability |
| QA Lead | ChatGPT | Test strategy, acceptance criteria, quality and release evidence |

## 5. Delivery phases and review gates

| Gate | Phase | What needs to be agreed or demonstrated |
|---|---|---|
| G0 | Initiation | Project scope, objectives and charter agreed |
| G1 | Requirements | Business questions, metric rules, dashboard requirements and acceptance criteria agreed |
| G2 | Data discovery | Sample data profiled; source access, licensing, availability, grain and limitations confirmed |
| G3 | Solution design | Architecture, models, mappings, quality rules, recovery approach and publishing contract reviewed |
| G4 | Implementation | Agreed pipelines and tests delivered, with run evidence |
| G5 | Testing and acceptance | Data reconciliation, rerun, correction, failure recovery, privacy and dashboard checks passed |
| G6 | Release | Public dashboard, documentation, runbook and release checks completed |

I will not start the main implementation until G0–G3 are complete. Decisions can be revisited, but changes should be documented rather than silently changing scope.

## 6. High-level design

Approved sources → controlled landing and batch metadata → Databricks Bronze → Silver → Gold → validated, versioned aggregate export → public dashboard.

**Databricks** is where data is processed and validated. **GitHub** is where I manage source code, documentation, issues, reviews and releases. **GitHub Pages** is the preferred hosting option for the first public dashboard. Streamlit Community Cloud stays on the options list for a later release, or if we identify a clear need for server-side Python.

The dashboard will use published datasets; it won't connect directly to Databricks or contain business logic that should live in the data pipelines.

The design must also account for logging, source versions, data-quality failures, reruns, historical corrections and keeping the previous valid dashboard data available if a new publication fails.

## 7. Making the platform reusable

The first release uses Irish property data, but the platform name and core design won't be tied to Ireland or property alone.

Future sources should be introduced through source-specific ingestion and transformation rules. Common capabilities - batch tracking, data quality, storage layers, published data contracts and monitoring - should be reusable.

Before adding India or another market, I'll review its data availability and rights, geography conventions, currency, date formats, reporting definitions and any market-specific rules. I won't assume that Irish datasets or KPIs map directly onto Indian ones.

**An India release is a future roadmap item, not part of Release 1 acceptance.**

## 8. Key decisions for Release 1

- GitHub Pages is the preferred public host. Streamlit Community Cloud remains an alternative to evaluate when the requirements justify it.
- The Gold layer is the source for published analytics. The UI uses an agreed, versioned data contract.
- PSRA transaction metrics and CSO index metrics remain separate and clearly labelled.
- Publication starts as a controlled, reviewed process. Automation can be added after feasibility and security checks.
- The project should run within free-service limits, with no guaranteed production SLA.
- I write the PySpark and SQL. Codex may review that work and help with the frontend; I validate the output.

These are working decisions. Detailed technical choices will be recorded in the architecture decision register and approved at G3.

## 9. How I'll know Release 1 is complete

- The agreed source files can be loaded, checked and reprocessed without double-counting.
- Bronze, Silver and Gold outputs have documented schemas and reconciliation results.
- The main metrics match the approved business definitions and have clear source references.
- I can demonstrate how the pipeline handles invalid records, corrections and a failed run.
- The dashboard is publicly accessible, works with approved aggregate data and explains what the numbers mean.
- No credentials or raw address-level records are exposed publicly.
- The repository contains the requirements, design decisions, tests, data model, release notes and runbook.
- Release evidence has been reviewed and the release has been explicitly accepted.

## 10. Assumptions and constraints

- Databricks Free Edition and free dashboard hosting have usage limits and do not provide production service guarantees.
- Source formats, geographic coverage and refresh schedules must be confirmed by examining real data.
- Data reuse and publication rights must be checked for **each selected source or extract** before publishing.
- Property register records may contain errors or retrospective corrections.
- A median of recorded sale prices is **not** the same as an official mix-adjusted house-price index.
- Publishing manually validated snapshots is acceptable for Release 1; real-time updates are not required.

## 11. Current status and next steps

**Charter status: draft for my approval (G0).**

Once the charter is agreed, the next step is to finalise the business questions, KPI rules and dashboard acceptance criteria (G1). After that I'll profile the data and confirm what can actually be used (G2), then work through the detailed design (G3). Coding starts after those decisions are documented.

## Source references

- PSRA Property Price Register: https://www.propertypriceregister.ie/
- CSO Residential Property Price Index methodology: https://www.cso.ie/en/methods/prices/residentialpropertypriceindex/
- CSO data portal: https://data.cso.ie/
- Databricks Free Edition limitations: https://docs.databricks.com/aws/en/getting-started/free-edition-limitations
- GitHub Pages: https://docs.github.com/en/pages
- Streamlit Community Cloud: https://docs.streamlit.io/deploy/streamlit-community-cloud
