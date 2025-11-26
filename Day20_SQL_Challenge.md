Day 20: Window Functions – Aggregate Window Functions

Topics

SUM() OVER, AVG() OVER, running totals, moving averages

Window functions allow calculating running totals, moving averages, and cumulative metrics without collapsing rows.

Common window aggregates: running totals, moving averages, running counts, cumulative min/max.

Window frame options include:
UNBOUNDED PRECEDING, N PRECEDING, CURRENT ROW, N FOLLOWING, UNBOUNDED FOLLOWING.

Key Ideas

Using ORDER BY inside OVER creates a default frame from the first row to the current row.

Without ORDER BY, the window frame is the full partition.

Moving averages use ROWS BETWEEN.

You can calculate differences from window aggregates (e.g., deviation from average).

Window functions cannot be nested, but you can have multiple in the same SELECT. 

Daily Challenge:

Question: Create a trend analysis showing for each service and week: week number, patients_admitted, running total of patients admitted (cumulative), 3-week moving average of patient satisfaction (current week and 2 prior weeks), and the difference between current week admissions and the service average. Filter for weeks 10-20 only.

Query:

SELECT
    service,
    week,
    patient_satisfaction,
    patients_admitted,
    rank_val AS rank
FROM (
    SELECT
        service,
        week,
        patient_satisfaction,
        patients_admitted,
        RANK() OVER (
            PARTITION BY service
            ORDER BY patient_satisfaction DESC
        ) AS rank_val
    FROM services_weekly
)
WHERE rank_val <= 3
ORDER BY service, rank_val, week;

Output:

<img width="1418" height="891" alt="image" src="https://github.com/user-attachments/assets/836a25fb-f685-4b3b-99ba-b81815c83dcb" />


Summary:
Day 20 focused on aggregate window functions like running totals, moving averages, cumulative statistics, and comparisons to group averages. We learned how ORDER BY and window frames shape results, how to use ROWS BETWEEN for moving calculations, and how window functions help analyze trends without losing row-level detail.

#100DaysOfSQL #Day19 #SQLWindowFunctions 
#DataAnalytics #SQLLearning #WomenInTech
#TechJourney #DatabaseEngineering
#LearnSQL #DataScienceBasics
