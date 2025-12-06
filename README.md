## 📧 Email Campaign & User Engagement Analysis (SQL)

### 📌 Overview
This SQL script analyzes the relationship between email marketing campaigns and user engagement on the platform. It integrates data from multiple sources (email logs, user accounts, and web sessions) to track the funnel from **Email Sent → Open → Visit** and correlates it with active user sessions.

The query is designed to identify the **Top 10 performing markets (countries)** based on email volume and user activity, providing a daily breakdown of key metrics.

### 🧠 Key Techniques Used
This query demonstrates advanced SQL capabilities, including:
* **Common Table Expressions (CTEs):** Used to modularize logic (separating email metrics from account metrics) for better readability and maintainability.
* **UNION ALL:** Employed to combine datasets with different granularities (Email Events vs. Account Sessions) into a single analytical view.
* **Window Functions:**
    * `SUM() OVER(PARTITION BY ...)`: To calculate country-level totals while preserving row-level daily detail.
    * `DENSE_RANK()`: To create a ranking system for countries based on performance.
* **Date Manipulation:** Using `DATE_ADD` to align event dates.
* **Filtering & Aggregation:** Complex `JOINs` across 6+ tables and filtering for top performers.

### ⚙️ Logic Breakdown
1.  **`emails` CTE:** Aggregates email metrics (Sent, Opened, Visited) joined with session data.
2.  **`accounts` CTE:** Calculates daily active account sessions per country.
3.  **`union_data`:** Merges both datasets to allow for a unified aggregation.
4.  **`totals` & `totals_country`:** Aggregates metrics by dimensions (Date, Country, Verification Status) and calculates total volumes per country.
5.  **`ranks`:** Assigns a rank to each country based on `sent_msg_total` and `account_cnt_total`.
6.  **Final Output:** Returns daily statistics only for the **Top 10 countries** by volume and engagement.
