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






# Database Design Proposal for Commonwealth Bank Social Media Intelligence

## 1. Overview & Proposed Table Structure

To store CommBank tweets, customer replies, quote retweets, and direct mentions at scale, the database architecture is divided into four normalized tables:

1. **`Users`**: Stores profile information for authors (CommBank official accounts and individual users).
2. **`Tweets`**: Stores core content, timestamps, and thread relationships for posts, replies, quotes, and mentions.
3. **`Tweet_Metrics`**: Stores dynamic, time-series engagement performance data (likes, reposts, views).
4. **`Sentiment_Analysis`**: Stores enriched NLP classifications, customer intent, and support triage flags.

---

## 2. Table Schemas & Variable Definitions

### Table 1: `Users`
Stores account metadata to avoid duplicating user details across multiple posts.

| Variable Name | Data Type | Key Type | Description |
| :--- | :--- | :--- | :--- |
| `user_id` | VARCHAR(50) | **Primary Key** | Unique identifier for the social media account (from API `author_id`) |
| `username` | VARCHAR(50) | None | Account handle (e.g., @CommBank or customer handle) |
| `author_type` | VARCHAR(20) | None | Account category (`CommBank`, `Customer`) |
| `follower_bucket`| VARCHAR(20) | None | Audience size bracket (e.g., `0-500`, `50k+`) |

---

### Table 2: `Tweets`
Stores post content, metadata, and structural interaction relationships.

| Variable Name | Data Type | Key Type | Description |
| :--- | :--- | :--- | :--- |
| `tweet_id` | VARCHAR(50) | **Primary Key** | Unique identifier for the tweet |
| `author_id` | VARCHAR(50) | **Foreign Key** | Links to `Users.user_id` (identifies the post author) |
| `post_datetime` | DATETIME | None | Exact timestamp when published (`created_at`) |
| `post_type` | VARCHAR(20) | None | Category: `Original post`, `Reply`, `Mention`, `Quote post` |
| `post_text` | TEXT | None | Raw text content of the tweet |
| `topic` | VARCHAR(50) | None | Curated topic category (e.g., `Digital banking`, `Fraud & scams`) |
| `content_format` | VARCHAR(30) | None | Media format (`Text`, `Text + image`, `Text + video`, `Link`) |
| `in_reply_to_tweet_id` | VARCHAR(50) | **Foreign Key** | Self-referencing FK linking to `Tweets.tweet_id` if this is a reply |
| `quoted_tweet_id` | VARCHAR(50) | **Foreign Key** | Self-referencing FK linking to `Tweets.tweet_id` if this is a quote tweet |

---

### Table 3: `Tweet_Metrics`
Stores quantitative engagement data for tracking interaction performance.

| Variable Name | Data Type | Key Type | Description |
| :--- | :--- | :--- | :--- |
| `metric_id` | INT | **Primary Key** | Unique auto-increment identifier for the metric entry |
| `tweet_id` | VARCHAR(50) | **Foreign Key** | Links to `Tweets.tweet_id` |
| `likes` | INT | None | Total count of likes |
| `replies` | INT | None | Total count of direct reply comments |
| `reposts` | INT | None | Total count of reposts / retweets |
| `quote_posts` | INT | None | Total count of quote posts |
| `views` | INT | None | Impression/view count |
| `total_engagements`| INT | None | Computed sum of all user interactions |
| `engagement_rate` | DECIMAL(5,4) | None | Engagement rate formula (`total_engagements / views`) |

---

### Table 4: `Sentiment_Analysis`
Stores machine learning and operational triage flags generated from text processing.

| Variable Name | Data Type | Key Type | Description |
| :--- | :--- | :--- | :--- |
| `analysis_id` | INT | **Primary Key** | Unique auto-increment identifier for the analysis record |
| `tweet_id` | VARCHAR(50) | **Foreign Key** | Links to `Tweets.tweet_id` |
| `sentiment_label` | VARCHAR(15) | None | NLP classification (`Positive`, `Negative`, `Neutral`, `Mixed`) |
| `sentiment_score` | DECIMAL(3,2) | None | Numerical score ranging from -1.00 to +1.00 |
| `customer_intent` | VARCHAR(50) | None | Operational category (e.g., `Scam report`, `Praise`, `App complaint`) |
| `response_needed` | VARCHAR(3) | None | Support escalation flag (`Yes` / `No`) |

---

## 3. Database Table Relationships

* **`Users` to `Tweets` (One-to-Many):** One user can publish multiple tweets. `Users.user_id` links to `Tweets.author_id`.
* **`Tweets` to `Tweet_Metrics` (One-to-One):** Each tweet has one performance metric entry. `Tweets.tweet_id` links to `Tweet_Metrics.tweet_id`.
* **`Tweets` to `Sentiment_Analysis` (One-to-One):** Each tweet has one sentiment evaluation entry. `Tweets.tweet_id` links to `Sentiment_Analysis.tweet_id`.
* **`Tweets` to `Tweets` (Self-Referencing / Recursive Relationships):**
  * **Replies:** `Tweets.in_reply_to_tweet_id` references `Tweets.tweet_id` of the parent post to track discussion threads.
  * **Quote Retweets:** `Tweets.quoted_tweet_id` references `Tweets.tweet_id` of the original post being quoted.
