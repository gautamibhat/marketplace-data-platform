# Initial Risk & Assumption Register - Marketplace Data Platform (MDP-001)

Version 1.0 · 19 November 2026

| ID | Risk / assumption | Impact | Mitigation / planned control | Responsible role |
|---|---|---|---|---|
| R-01 | PSRA national extract licensing/republication rights not verified | High | Source-specific terms review at G2; publish aggregates only after clearance; keep exports unpublished if unresolved | Project Lead / BA |
| R-02 | Source record errors or later corrections alter historical metrics | High | Snapshot fingerprints, correction tests, versioned publication, reconciliation | Data Engineer |
| R-03 | Raw addresses or other identifiable fields leak publicly | High | Explicit export allowlist, privacy review, repo scans, aggregate/small-cell policy | Data Engineer / QA |
| R-04 | PSRA median misrepresented as official price index | High | Independent KPI families, mandatory labels/methodology, UAT review | Project Lead / BA |
| R-05 | CSO dimension compatibility or temporal granularity differs from assumptions | Medium | Confirm exact published series and grain during profiling; no unsupported joins | Data Architect |
| R-06 | Databricks Free Edition quotas/network restrictions block automation | Medium | Controlled data acquisition and manual export fallback; quota-aware runbook | Data Engineer |
| R-07 | Public frontend displays failed/stale publication | Medium | Publish validation, keep previous snapshot, freshness indicator and rollback | QA / Data Engineer |
| R-08 | Streamlit hibernation makes public portfolio experience unreliable | Medium | Prefer static GitHub Pages in R1; reassess Streamlit with explicit tradeoff | Project Lead |
| R-09 | Scope expands across other domains or countries before a usable R1 product | High | Baseline scope, formal change requests, future release backlog | Project Lead |
| R-10 | Free GitHub Actions/runtime allowances exceeded | Medium | Minimise workflow schedules, use budgets/alerts, review usage | Project Lead |
| R-11 | Metrics with tiny group sizes mislead or disclose details | Medium | Minimum cohort size, suppression or coarser aggregation in data contract | BA / QA |
| R-12 | Unclear methodology undermines portfolio credibility | High | Versioned KPI catalogue, evidence-based QA, clear source provenance and transparent methodology | Project Lead |
| R-13 | Future India expansion requires different source rights, geography, currency and metric conventions | Medium | Reassess at new-release discovery; avoid assuming Irish business rules can be reused unchanged | Project Lead / Data Architect |

## Initial assumptions to test

- Source formats are machine-readable without prohibited automated access.
- PSRA and CSO datasets can support a useful overlapping history, but **not** necessarily the same geographic breakdown.
- An export-based public dashboard is sufficiently interactive for the approved business use cases.
- Core data processing and manual publication can be operated within free quotas.

Risk acceptance and responsible roles are provisional until G0/G2 reviews.
