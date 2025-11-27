🌼 Day 21 (27/11): Common Table Expressions (CTEs)

Today I learned about Common Table Expressions (CTEs) — one of the best tools in SQL for organizing and simplifying complex queries. CTEs make queries more readable, reusable, and easier to debug.

📘 What I Learned Today

🔹 What is a CTE?

A CTE is a temporary, named result set defined using the WITH clause.
It exists only while the query is running and helps break down logic into smaller steps.

🔹 Why Use CTEs?

Makes long queries clean and structured

Helps avoid deeply nested subqueries

Allows reusing the same result set multiple times

Improves readability and debugging

🧩 Types of CTE Usage

⭐ Single CTE

Used to perform one logical step such as calculating averages or totals.

⭐ Multiple CTEs

Multiple blocks can be created and connected together to build dashboards or layered analysis.

⭐ CTEs Referencing Each Other

You can build CTEs in stages — each one using results from the previous one.

🏥 Real-World Use Cases I Learned

Creating service-level statistics such as average satisfaction and total patients.

Separating patient metrics, staff metrics, and weekly hospital metrics into different CTEs.

Combining multiple CTEs to generate a final performance dashboard.

Using descriptive names like patient_metrics, staff_summary, service_stats to make queries self-explanatory.

💡 Key Insights & Tips

Use CTEs to break big logic into small readable steps.

Subqueries are fine for small tasks, but CTEs are better for multi-step analysis.

CTEs can be referenced multiple times in the same query.

They are not stored permanently — they exist only during query execution.

Daily Challenge:

Question: Create a comprehensive hospital performance dashboard using CTEs. Calculate: 1) Service-level metrics (total admissions, refusals, avg satisfaction), 2) Staff metrics per service (total staff, avg weeks present), 3) Patient demographics per service (avg age, count). Then combine all three CTEs to create a final report showing service name, all calculated metrics, and an overall performance score (weighted average of admission rate and satisfaction). Order by performance score descending.

Query:

WITH
service_level AS (
    SELECT
        service,
        SUM(patients_admitted) AS total_admissions,
        SUM(patients_refused)  AS total_refusals,
        AVG(patient_satisfaction) AS avg_satisfaction,
        SUM(patients_request) AS total_requests,
        CASE
            WHEN SUM(patients_request) > 0 THEN
                SUM(patients_admitted) / SUM(patients_request)
            ELSE 0
        END AS admission_rate
    FROM services_weekly
    GROUP BY service
),
staff_metrics AS (
    SELECT
        s.service,
        COUNT(DISTINCT s.staff_id) AS total_staff,
        CASE 
            WHEN COUNT(DISTINCT s.staff_id) > 0 THEN
                COUNT(DISTINCT sw.week) / COUNT(DISTINCT s.staff_id)
            ELSE 0
        END AS avg_weeks_present
    FROM staff s
    LEFT JOIN services_weekly sw
        ON s.service = sw.service
    GROUP BY s.service
),
patient_demo AS (
    SELECT
        service,
        AVG(age) AS avg_age,
        COUNT(*) AS patient_count
    FROM patients
    GROUP BY service
)
SELECT
    sl.service AS service_name,
    sl.total_admissions,
    sl.total_refusals,
    sl.total_requests,
    sl.admission_rate,
    sl.avg_satisfaction,
    sm.total_staff,
    sm.avg_weeks_present,
    pd.avg_age,
    pd.patient_count,
    (
        0.7 * (sl.admission_rate * 100) +
        0.3 * sl.avg_satisfaction
    ) AS performance_score
FROM service_level sl
LEFT JOIN staff_metrics sm
    ON sl.service = sm.service
LEFT JOIN patient_demo pd
    ON sl.service = pd.service
ORDER BY performance_score DESC;


Output:

![WhatsApp Image 2025-11-27 at 17 49 22_4b207423](https://github.com/user-attachments/assets/695b693d-5d60-43c5-84a8-4987079cbdab)

🌟 Key Learnings

CTEs help structure and organise complex SQL logic

Easier to read, debug, and maintain than nested subqueries

Allow combining multiple analytical layers

Great for dashboards, reports, and multi-step calculations

Debugging becomes easier because each CTE can be tested independently.

Good naming improves clarity dramatically.

#100DaysOfSQL #Day21 #CTE #SQLWithIDC 
#IndianDataClub #DataAnalytics #TechLearning
#WomenInTech #SQLStudy #DatabaseSkills
