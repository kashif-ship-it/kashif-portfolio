# Retention Analysis (SQL)

**Overview**  
A structured SQL based analytical model used to compute retention cohorts, churn rates, and active user trends for product and CX teams.

**Business Problem**  
The team needed clarity on how long users stayed active, when they were dropping off, and which segments had the highest churn risk.

**Data Used**  
- User activity logs  
- First active date  
- Last active date  
- User metadata  
- Engagement metrics  

**Approach**  
- Built cohort tables grouped by user signup date  
- Calculated rolling retention using DATEDIFF and activity windows  
- Generated churn flags using inactivity thresholds  
- Created aggregated tables for Power BI and reporting  
- Designed reusable SQL views for retention, cohorts, and active users

**Example SQL Logic**  
```sql
SELECT 
    user_id,
    MIN(activity_date) AS cohort_date,
    activity_date,
    DATEDIFF(day, MIN(activity_date) OVER (PARTITION BY user_id), activity_date) AS days_since_signup
FROM user_activity;
