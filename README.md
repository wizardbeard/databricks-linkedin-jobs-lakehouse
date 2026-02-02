# LinkedIn Jobs Lakehouse on Databricks

## Overview
This project demonstrates a small but production-aligned lakehouse pipeline built on Databricks using PySpark and Databricks SQL.  
It ingests a Marketplace dataset of LinkedIn job listings, applies data quality and normalization logic, and exposes analytics-ready marts for dashboards.

The focus is on correctness, reproducibility, and clear separation between compute, storage, and presentation layers.

---

## Dataset
- Source: Bright Data LinkedIn Jobs Listing dataset (Databricks Marketplace)
- Access method: Delta Sharing
- Characteristics:
  - Job postings with company, role, location, and human-readable posting times
  - UX-oriented fields requiring normalization for analytics

---

## Architecture
- Platform: Databricks Free Edition
- Storage format: Delta Lake
- Processing: PySpark
- Presentation: Databricks SQL dashboards

### Medallion structure
- Bronze: Raw ingestion from shared Marketplace tables
- Silver: Cleaned, normalized, and deduplicated job postings
- Gold: Aggregated analytics marts for reporting

---

## Data Pipeline

### Bronze
- Reads shared Delta tables from the Marketplace catalog
- Adds ingestion metadata
- Persists raw records as Delta tables owned by the project

### Silver
- Normalizes text fields such as company and title
- Handles relative time strings like "1 week ago"
- Deduplicates postings using stable identifiers
- Enforces basic data quality rules

### Gold
- Hiring volume trends by posting date
- Top companies by job posting volume
- Optional enrichment signals such as remote-friendly roles

---

## Analytics and Dashboards
- Gold tables are consumed via Databricks SQL
- Dashboards query tables or saved SQL queries, not notebooks
- Ranking and sorting logic is enforced in SQL for deterministic visuals

Recommended visualizations:
- Horizontal bar chart for top companies
- Line chart for hiring trends over time

---

## Reproducibility
The entire project can be rebuilt from this repository:
1. Run Bronze notebook
2. Run Silver notebook
3. Run Gold notebook
4. Execute SQL files to recreate views and dashboard queries

No data files are committed. All artifacts are defined as code.

---

## Skills Demonstrated
- PySpark data engineering
- Delta Lake and medallion architecture
- Databricks Marketplace and Delta Sharing
- Data quality and time normalization
- SQL-first dashboard design
- Version control with Databricks Repos and GitHub

---

## Notes
This project is intentionally scoped for clarity and signal rather than scale.  
The same patterns apply directly to larger datasets and production Databricks environments.
