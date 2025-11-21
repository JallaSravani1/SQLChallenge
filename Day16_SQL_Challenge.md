📘Day 16 – SQL With IDC Challenge

Topic: Subqueries in WHERE Clause

Daily Challenge:

Question: Find all patients who were admitted to services that had at least one week where patients were refused AND the average patient satisfaction for that service was below the overall hospital average satisfaction. Show patient_id, name, service, and their personal satisfaction score.

SQL Query:

SELECT 
    p.patient_id,
    p.name,
    p.service,
    p.satisfaction
FROM patients p
WHERE p.service IN (
    SELECT service
    FROM services_weekly
    WHERE patients_refused > 0
)
AND p.service IN (
    SELECT service
    FROM services_weekly
    GROUP BY service
    HAVING AVG(patient_satisfaction) < (
        SELECT AVG(patient_satisfaction)
        FROM services_weekly
    )
);

OUTPUT:

<img width="587" height="662" alt="image" src="https://github.com/user-attachments/assets/27e964a5-19cc-4a6e-811e-495e1355d4e6" />

517 rows selected

🧠Key Learnings

How to use IN, NOT IN, EXISTS, and single-value subqueries

Difference between IN vs EXISTS

Using correlated subqueries

Avoiding NULL issues with NOT IN

Subqueries returning single vs multiple values

How subqueries run for each row (important for perform

#SQLWithIDC #21DaysSQLChallenge #DataAnalytics #LearningJourney #DPDzero #IndianDataClub
