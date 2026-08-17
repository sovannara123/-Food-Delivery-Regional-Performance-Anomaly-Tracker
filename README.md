# Food Delivery Regional Performance & Anomaly Tracker

## Executive Summary
An end-to-end analytics solution that tracks regional food-delivery performance, detects operational anomalies (e.g., spikes in late deliveries or cancellations), and automates weekly reporting — built with SQL, Python, and Google Sheets. The project mirrors the daily workflow of a Performance Analyst at high-volume, low-margin, hyper-local delivery companies like Foodpanda/Delivery Hero, demonstrating strength in **unit economics, operational efficiency, and stakeholder communication**.

## Why This Project
This portfolio piece targets the Performance Analyst JD by proving competence across every core requirement:

| JD Requirement | How This Project Proves It |
| :--- | :--- |
| Monitor KPIs across business functions | Tracks OTD, AOV, cancellation rate, and delivery-time variance across regions/zones/times |
| Automated Google Sheets dashboards | Live G-Sheet dashboard updated by Python (`gspread`) on schedule |
| Write / optimize SQL queries | Uses window functions (`LAG()`) to compute day-over-day OTD and variance |
| Trend & anomaly root-cause analysis | Flags cancellation/late-delivery spikes and traces them to category, time-of-day, or zone |
| Cross-functional support | Mock WBR deck built for Ops/Commercial stakeholders |
| Automate manual work with Python | Scripted ETL pipeline eliminates manual copy-pasting |

## Data & Architecture
- **Data source:** synthetic, realistic food-delivery dataset (orders, riders, restaurants, deliveries, cancellations) with engineered anomalies for the pipeline to discover
- **Database:** SQLite local DB (SQL portable to PostgreSQL)
- **Analysis:** Python (Pandas/NumPy), rolling 7-day mean ± 2σ anomaly detection, z-score/IQR, optional Isolation Forest
- **Reporting:** Google Sheets dashboard (gspread) + automated push
- **Deliverables:** charts, root-cause summaries, and a 3-slide Weekly Business Review (WBR) deck

## Core Metrics (SQL Layer)
- **On-Time Delivery Rate (OTD)** — day-over-day via `LAG()`
- **Average Order Value (AOV)** — by region & week
- **Cancellation Rate** — split by restaurant vs. rider
- **Delivery Time Variance** — actual vs. estimated

## Anomaly Detection Workflow
1. Calculate rolling 7-day baseline for each KPI
2. Flag any day exceeding 2 standard deviations
3. Drill down for root cause → zone / category / time-of-day
4. Output visual chart + 3-bullet Root Cause Breakdown

## Automation (Google Sheets)
- gspread pushes cleaned KPI tables weekly (scheduled)
- Data Validation dropdowns: filter by Region / Week / Restaurant Category
- Screen recording of the automated update as a portfolio artifact

## WBR Mock Review (Stakeholder Communication)
- **Slide 1:** Executive Summary — KPI health
- **Slide 2:** The Anomaly & Root Cause
- **Slide 3:** Actionable Recommendation (e.g., *"Incentivize riders in Zone B during Friday peak hours to reduce OTD variance by 12%"*)

## Repository Structure
```
foodpanda-performance-analytics/
├── data/
│   ├── raw/         # raw source CSVs
│   └── cleaned/     # cleaned/processed datasets
├── sql/             # schema, KPI queries, root-cause drills
├── python/          # ETL, analytics, anomaly detection, Google Sheets push
├── dashboard/       # Streamlit preview
├── report/          # charts, WBR PDF, exports
└── README.md        # case-study writeup
```