# Anomaly Detection (SQL)

**Overview**  
A SQL based approach to detect spikes, drops, and unusual activity patterns in financial and operational datasets. This model helps identify outliers early and supports fraud detection, reconciliation, and performance monitoring.

**Business Problem**  
Teams needed a way to automatically flag unusual trends in revenue, transactions, or activity metrics without waiting for manual review.

**Data Used**  
- Daily transaction summaries  
- Revenue tables  
- Cost and margin tables  
- Operational logs  

**Approach**  
- Built moving average and rolling window logic  
- Implemented z score and threshold based anomaly detection  
- Identified outliers by comparing actuals vs expected ranges  
- Generated a clean table of flagged anomalies for visual dashboards  
- Designed reusable SQL views for reporting and monitoring  

**Example SQL Logic**  
SELECT
    date,
    revenue,
    AVG(revenue) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS moving_avg,
    STDEV(revenue) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS std_dev,
    CASE 
        WHEN revenue > moving_avg + 2 * std_dev THEN 'High Spike'
        WHEN revenue < moving_avg - 2 * std_dev THEN 'Abnormal Drop'
        ELSE 'Normal'
    END AS anomaly_flag
FROM daily_revenue;

**Impact**  
- Helped finance catch unusual revenue drops early  
- Strengthened fraud and risk detection  
- Reduced time spent manually reviewing daily trends
