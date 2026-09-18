# Commonwealth Bank Data Science Job Simulation (Forage)

A summary of my work on the Commonwealth Bank Data Science virtual experience, focusing on transactional analysis and data privacy.

---

## Task 1: Retail Transaction Analysis

**Objective:** Extract specific business insights from three years of Australian supermarket records (`supermarket_transactions.csv`) for partner team InsightSpark.

**How I Did It:**
* Used Excel filters and formulas to isolate specific subsets of transactional data based on criteria like product type, store location, payment type, and customer membership status.
* Applied `SUM` functions on filtered subsets to compute exact volume and revenue figures.

**Results:**
* **Apple Cash Purchases:** 117 apples bought with cash across all locations.
* **Apple Cash Revenue:** $537.03 total spent on cash apple transactions.
* **Bakershire Non-Member Revenue:** $2,857.51 spent at the Bakershire store by non-member customers across all payment methods.

---

## Task 2: Data Anonymization & Privacy Protection

**Objective:** Clean and anonymize a 3-year mobile app dataset (`mobile_customers.csv`) to remove PII (Personally Identifiable Information) before sharing it with data scientists at InsightSpark.

**How I Did It:**
* **Deletion:** Dropped unnecessary identifier columns (like names and card numbers) to permanently eliminate direct identity risks.
* **Masking:** Applied masking to sensitive individual fields (like phone numbers) so records couldn't be traced back to real people.
* **Categorization:** Grouped continuous numerical data (like exact age and income) into bracketed categories to retain demographic patterns while hiding precise individual numbers.

**Deliverable:** Exported a clean, anonymized CSV dataset ready for safe external review.
