# Commonwealth Bank Data Science Virtual Experience (Forage)

A comprehensive tracking repository documenting my data analysis, data privacy compliance, and social media business strategy work during the Commonwealth Bank Data Science program on Forage.

---

## Overview

This project simulates core data science and analytical workflows at Commonwealth Bank. It spans transactional database querying, data privacy compliance for external sharing, and real-time social media analytics designed to drive strategic business decisions.

---

## Completed Tasks

### Task 1: Retail Transaction Analysis
**Goal:** Extract specific business metrics from a 3-year Australian supermarket dataset (`supermarket_transactions.csv`) for partner team InsightSpark.

* **How I Did It:**
  * Applied multi-level filters and data aggregation formulas in Excel based on product categories, store locations, payment methods, and customer loyalty status.
  * Executed `SUM` aggregations on filtered subsets to determine volume and spending metrics.
* **Key Findings:**
  * **Cash Apple Purchases:** 117 apples purchased using cash across all store locations.
  * **Cash Revenue on Apples:** $537.03 total spent on cash apple transactions.
  * **Bakershire Non-Member Revenue:** $2,857.51 total spent at the Bakershire location by non-member customers across all payment methods.

---

### Task 2: Data Anonymization & Privacy Protection
**Goal:** Clean and anonymize a 3-year mobile app customer dataset (`mobile_customers.csv`) to remove Personally Identifiable Information (PII) before sharing with external data science teams at InsightSpark.

* **How I Did It:**
  * **Deletion:** Stripped out direct identifiers (e.g., full names, credit card details) that offered no utility for analytical models.
  * **Masking:** Obfuscated high-risk personal identifiers (e.g., mobile numbers, passport numbers) to eliminate identity tracking.
  * **Categorization / Binning:** Segmented exact continuous metrics (e.g., exact age, income) into categorical brackets to preserve macro demographic trends while protecting personal identity.
* **Deliverable:** Produced a fully anonymized, privacy-compliant CSV file ready for secure external review.

---

### Task 3: Social Media Analytics & InsightSpark Proposal
**Goal:** Analyze 60 simulated CommBank social media interactions (`commonwealth_bank_social_media_dataset.xlsx`) to uncover engagement drivers, customer pain points, and sentiment trends, followed by an API integration proposal for InsightSpark.

* **How I Did It:**
  * Built dynamic Excel Pivot Tables across topic volume distributions, total engagements, engagement rates by content format, and sentiment trends across days of the week.
  * Isolated customer service escalation cases by filtering for `response_needed = Yes` to uncover critical support drivers.
  * Mapped X (Twitter) API endpoints (`text`, `created_at`, `public_metrics`, `conversation_id`) to database fields to outline automated pipeline ingestion.
* **Key Findings:**
  * **Primary Discussion Drivers:** **Digital Banking** (13 posts / 21.6%) and **Fraud & Scams** (11 posts / 18.3%) accounted for over 40% of all conversation items.
  * **Content Performance:** Posts featuring **Text + Video** achieved the highest average engagement rate (**5.13%**), closely followed by **Text + Image** (**4.37%**), compared to plain **Text** (**1.72%**).
  * **Operational & Escalation Risks:** 10 out of 11 posts flagged as `response_needed = Yes` carried negative sentiment, heavily concentrated around **Branch/ATM closures**, **Digital banking glitches**, and **Outage/service disruptions**.

---

## Technologies & Skills Applied

* **Data Analysis & Modeling:** Microsoft Excel (Pivot Tables, Multi-criteria Filtering, Aggregation), Python (Pandas)
* **Data Governance & Privacy:** PII Identification, Data Masking, Field Deletion, Categorical Binning
* **Analytics Strategy:** Social Media Sentiment Analysis, NLP Data Mapping, X (Twitter) v2 API Pipeline Mapping, Executive Proposal Writing
