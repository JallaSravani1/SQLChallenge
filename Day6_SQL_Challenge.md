📘 Day 6 (09/11): GROUP BY Clause

💻 Topics Covered:

GROUP BY — Aggregating rows by categories

🧩 Concept Overview

The GROUP BY clause divides rows into groups based on column values and applies aggregate functions (COUNT, SUM, AVG, etc.) to each group.

🔹 Key Points

Every non-aggregated column in SELECT must appear in GROUP BY

Each group produces one result row

Use WHERE before GROUP BY, and HAVING after it

💡 Tips & Tricks

 Think “one row per group”
 
 Execution order: FROM → WHERE → GROUP BY → SELECT → ORDER BY
 
 Use GROUP BY service, month for combined grouping
 
 You can ORDER BY aggregated columns
 
 Alias aggregates for readability

🧭 Daily Challenge

Question:
 For each hospital service, calculate the total number of patients admitted, total patients refused, and the admission rate (percentage of requests that were admitted). Order by admission rate descending.

 Query:
 
 SELECT 
    service,
    COUNT(patients_admitted) AS patients_admitted,
    COUNT(patients_refused) AS patients_refused,
    ROUND(
        (COUNT(patients_admitted) * 100.0) / 
        (COUNT(patients_admitted) + COUNT(patients_refused)),
        2
    ) AS admission_rate
FROM services_weekly
GROUP BY service
ORDER BY admission_rate DESC;

output

![WhatsApp Image 2025-11-09 at 18 49 26_8b0997c1](https://github.com/user-attachments/assets/b269e59a-4035-4f2f-8148-995a1dd861b2)

🌱 What I Learned Today

Learned how GROUP BY aggregates data into categories.

Understood the difference between row-wise and group-wise aggregations.

Calculated percentages using aggregate functions.

Practiced real-world queries like finding admission rates by service.

#SQLWithIDC #LearnSQL #DataAnalytics #DPDZero #IndianDataClub #SQLDailyChallenge

