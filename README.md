# Internship at CadetX — Heavy Supplier & Warehouse Analytics

This repository documents my personal work and learning from a 3-month virtual data analytics internship with **CadetX**, where I was assigned to the **Heavy Supplier & Warehouse Analytics** project.

## About the Project
The project analyzes historical warehouse and supply-chain data (12 relational tables covering suppliers, products, inventory, purchase orders, sales orders, invoices, payments, and stock movements) to help warehouse teams move from reactive, manual decision-making toward a data-driven analytics framework — covering inventory optimization, warehouse performance, and supplier/customer analytics.

## My Role
I worked as a Data Analyst on this project, handling data profiling, quality checks, and relationship mapping across the full dataset. This repo contains only my own individually completed work and personal records; team submissions live in a separate shared repository.

## Key Work Completed (Sprint 1)
- **Data Profiling** — checked all 12 tables for nulls, duplicates, referential integrity, and date consistency
- **Entity Relationship Diagram (ERD)** — mapped primary/foreign keys and relationships across all 12 tables using dbdiagram.io
- **Anomaly Investigation** — discovered `current_stock` values inflated 100–850x realistic levels; traced the root cause to cumulative IN (purchase order) movements exceeding OUT (sales order) movements over 2019–2025
- **Data Quality Review** — cross-checked a teammate's data quality report and independently confirmed genuine ID collisions in `invoice_id` and `payment_id` fields (not reliably unique keys), plus calculated an unpaid invoice rate (~10.2%) and late payment rate (~42.6%) as candidate KPIs

## Tools Used
- Python (Google Colab, pandas)
- dbdiagram.io (ERD design)
- Git / GitHub

## Structure
- `notebooks/` — data profiling and analysis notebooks
- `docs/` — findings reports, ERD, and review notes

---
*This is a personal learning and portfolio record. Team deliverables were submitted through a separate shared repository as required by the CadetX program.*
