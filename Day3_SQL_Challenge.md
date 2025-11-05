📘 Day 3 – SQL With IDC Challenge
🗓 Date: 05/11 – Sorting Data with ORDER BY

Topics Covered:
ORDER BY clause
Sorting with ASC and DESC
Multi-column sorting
Using ORDER BY for Top-N queries

💻 Challenge Task

Question:
Retrieve the top 5 weeks with the highest patient refusals across all services, showing week, service, patients_refused, and patients_request. Sort by patients_refused in descending order.

Query:

SELECT 
    TO_CHAR(arrival_date, 'IW') AS week,
    service,
    COUNT(patient_id) AS patients_requested,
    SUM(CASE WHEN satisfaction = 0 THEN 1 ELSE 0 END) AS patients_refused
FROM 
    patients
GROUP BY 
    TO_CHAR(arrival_date, 'IW'), service
ORDER BY 
    patients_refused DESC
FETCH FIRST 5 ROWS ONLY;

Output:
<img width="1102" height="534" alt="Screenshot 2025-11-05 192111" src="https://github.com/user-attachments/assets/5b25c6e5-1ec5-4feb-8cc5-cdcf7dab2c45" />

💡 Key Learnings

Learned how to sort query results using ORDER BY with multiple columns.
Understood the difference between ASC (ascending) and DESC (descending) order.
Practiced how to extract week numbers using TO_CHAR(date, 'IW') in Oracle.
Learned to find Top N results using FETCH FIRST n ROWS ONLY.

🧩 Summary

This challenge helped in:
Strengthening understanding of sorting and ranking data in SQL.
Combining aggregation, grouping, and sorting to derive insights.
Getting familiar with Oracle’s date functions and ORDER BY logic.

#SQLWithIDC #21DaysSQLChallenge #DataAnalytics #LearningJourney #DPDzero #IndianDataClub
