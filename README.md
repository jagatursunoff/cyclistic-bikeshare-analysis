# Cyclistic Bike-Share Case Study: Operational Analysis & Subscription Conversion Strategy

## Project Overview
This repository hosts a comprehensive end-to-end data analysis project executed under the official Google Data Analytics Capstone framework (Ask, Prepare, Process, Analyze, Share, Act). 

The purpose of this project is to analyze 12 months of historical trip data (spanning June 2025 to May 2026) for Cyclistic—a fictional bike-share company in Chicago. By leveraging SQL (Google BigQuery) and interactive data visualizations (Tableau Public), this analysis isolates the distinct behavioral patterns between casual riders and annual members to formulate three targeted, data-backed conversion strategies for the Director of Marketing.

---

## 🔗 Quick Project Links
*   **Interactive Tableau Dashboard:** [👉 Click Here to View on Tableau Public](https://public.tableau.com/views/CyclisticBike-ShareConversionAnalysis/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
*   **Kaggle Aggregated Dataset:** [👉 Click Here to View on Kaggle](https://www.kaggle.com/code/jafarmashura/cyclistic-bike-share-executive-case-study)

---

## 📁 Repository Structure
*   `SQL_scripts/01_bulk_ingestion.sql` - Consolidates 12 individual raw CSV files (over 5M+ rows) into a single master database.
*   `SQL_scripts/02_data_cleaning.sql` - Details the quality assurance filters, time calculations, and metadata extractions.
*   `SQL_scripts/03_exploratory_analysis.sql` - Houses the business query scripts used to isolate macro-trends, weekly rhythms, and hourly peaks.
*   `SQL_scripts/04_data_aggregation.sql` - Condenses the multi-million row table into a 336-row aggregated summary optimize for Tableau rendering.

---

## 1. Ask (The Business Case)
The ultimate objective of this program is to drive long-term business profitability. Cyclistic's finance analysts have determined that while pricing flexibility attracts a high volume of customers, annual members generate significantly higher profit margins than casual riders. 

### The Core Problem Statement
*   **How do annual members and casual riders use Cyclistic bikes differently?**

### Primary Stakeholders
*   **Lily Moreno (Director of Marketing):** Responsible for executing the digital campaign campaigns based on these findings.
*   **Cyclistic Executive Team:** Highly detail-oriented executive committee requiring clear, visual, and data-backed proof of concept before approving strategic program shifts.

---

## 2. Prepare (Data Integrity & Governance)
The underlying dataset consists of public first-party operational data collected by Motivate International Inc.

### Data Quality (ROCCC Assessment)
*   **Reliable:** High. Captured directly from the physical bike-share geotracking and docking network.
*   **Original:** High. First-party primary data source.
*   **Comprehensive:** High. Millions of rows capturing complete seasonal, weekly, and hourly variations over a 12-month sequence.
*   **Current:** High. Covers a continuous 12-month block up to May 2026.
*   **Cited:** High. Officially licensed and stored in a public AWS S3 repository.

### Compliance, Privacy, and Constraints (PII)
In strict compliance with data-privacy regulations, all personally identifiable information (PII) has been omitted from the source data. Credit card numbers, names, and accounts are completely restricted. 
*   **The Programmatic Impact:** We cannot track unique individual users across multiple separate trips or verify if casual riders are recurring local travelers or one-off tourists.

---

## 3. Process (Data Engineering & Cleaning)
To manage a dataset of this size (exceeding 5 million rows), standard spreadsheet tools were bypassed in favor of **Google BigQuery (SQL)** to preserve processing power and maintain an auditable data pipeline.

### Key Cleaning & Transformation Steps
1.  **Unified Schema Union:** Consolidated 12 separate monthly database files into a singular table `combined_raw_trips`.
2.  **Ride Length Calculations:** Extracted exact trip durations in minutes and seconds using `TIMESTAMP_DIFF`.
3.  **Calendar Extractions:** Mapped date parameters to Day of the Week (1 = Sunday, 7 = Saturday) and hour of the day using `EXTRACT`.
4.  **Operational QA Filters:** 
    *   Removed negative/zero-duration trips under 60 seconds (system tests/accidental unlocks).
    *   Removed trips exceeding 24 hours (potential bike loss vectors/docking errors).
    *   Removed null primary identifiers to maintain absolute relational integrity.

---

## 4. Analyze & Share (Insights)
Interrogating the cleaned dataset in BigQuery and visualizing the summaries in Tableau revealed an explicit divergence in user intent: **Utility vs. Leisure**.

### Core Discoveries

| Metric / Dimension | Annual Members (The Commuters) | Casual Riders (The Weekend Warriors) |
| :--- | :--- | :--- |
| **Weekly Pattern** | Uniform volume Monday through Friday. Drastic dip on weekends. | Massive volume spikes on Saturdays and Sundays. |
| **Hourly Pattern** | Sharp, binary peaks at 8:00 AM and 5:00 PM (Corporate transit windows). | Gradual, bell-shaped afternoon curve peaking between 12:00 PM and 3:00 PM (Leisure peak). |
| **Trip Duration** | Brief, highly efficient rides averaging 12.73 minutes. | Prolonged rides averaging 23.14 minutes (frequently >2x longer than members). |

### The Data Narrative
*   **Members treat the system as a critical utility.** Their usage is highly structured, predictable, and directly aligned with corporate work schedules.
*   **Casuals treat the system as a recreational activity.** Their usage is experiential, flexible, concentrated on leisure days, and characterized by significantly longer ride lengths.

---

## 5. Act (Strategic Recommendations)
Based on these findings, we recommend three targeted program interventions to Lily Moreno and the executive team:

### 1. Launch a "Weekend Warrior" Subscription Package
*   **Justification:** Casual riders dominate weekend traffic but have low incentive to buy a full 365-day commuter membership. 
*   **Action:** Introduce a seasonal, weekend-only membership tier. Use geofenced digital ads near coastal and park docking stations on weekends to promote this option to active casual riders.

### 2. Implement In-App Commuter Trials
*   **Justification:** A distinct subset of casual riders utilizes the system during weekday rush hours (8 AM / 5 PM). These are local commuters currently paying premium single-ride rates.
*   **Action:** Trigger automatic promotions for a "7-Day Free Commuter Trial" to any casual account that unlocks a bike during weekday commuter windows more than twice in a single month.

### 3. Cost-Savings Comparison Push Notifications
*   **Justification:** Casual riders take trips that are more than double the duration of members, resulting in high single-trip costs. 
*   **Action:** Program the Cyclistic app to send a push notification immediately following any casual ride exceeding 25 minutes. Show a personalized financial breakdown: *"This single ride cost you $X. With an Annual Membership, you would have saved $Y. Click here to convert now."*
  
