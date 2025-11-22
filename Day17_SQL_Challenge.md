📌 Day 17 – Subqueries in SELECT & FROM (SQL Learning Journey)

🔍 Overview

Today I learned how subqueries can be used inside the SELECT clause and the FROM clause to create calculated fields and derived tables. These help break complex logic into smaller, understandable parts.

🧠 Key Concepts

Subqueries in SELECT:
Used to add extra calculated columns, such as averages, totals, or comparisons.
Must always return a single value.

Derived Tables (Subqueries in FROM):
A powerful way to build temporary result sets.
Useful for organizing multi-step calculations.

Why use them?
✔️ Cleaner logic
✔️ Avoids huge nested queries
✔️ Makes analytics easier
✔️ Helps compare values across groups

Question : Create a report showing each service with: service name, total patients admitted, the difference between their total admissions and the average admissions across all services, and a rank indicator ('Above Average', 'Average', 'Below Average'). Order by total patients admitted descending.

Query:

SELECT 
    service,
    SUM(patients_admitted) AS total_admissions,
    SUM(patients_admitted) 
      - (SELECT AVG(patients_admitted) FROM services_weekly) AS diff_from_avg,
    CASE 
        WHEN SUM(patients_admitted) > (SELECT AVG(patients_admitted) FROM services_weekly)
            THEN 'Above Average'
        WHEN SUM(patients_admitted) = (SELECT AVG(patients_admitted) FROM services_weekly)
            THEN 'Average'
        ELSE 'Below Average'
    END AS rank_indicator
FROM services_weekly
GROUP BY service
ORDER BY total_admissions DESC;

Output:

![WhatsApp Image 2025-11-22 at 20 10 47_a3b90df8](https://github.com/user-attachments/assets/3fac4b4e-5844-4342-80b3-afd6083a0e2b)

📝 What I Practiced

Calculated each service’s total admissions using grouping.

Derived the average admissions across all services using a subquery.

Compared each service with the average and labeled them as:
Above Average, Average, or Below Average.

Returned the final report sorted by total admissions.

#SQLWithIDC #21DaysSQLChallenge #DataAnalytics #SQL #LearningJourney #DPDzero #IndianDataClub #GitHubJourney
