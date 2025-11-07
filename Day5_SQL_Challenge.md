📘 Day 5 – SQL With IDC Challenge

🗓 Challenge Task
Calculate the total number of patients admitted, total patients refused, and the average patient satisfaction across all services and weeks.
Round the average satisfaction to 2 decimal places.

💻 SQL Query

SELECT 
    SUM(patients_admitted) AS total_patients_admitted,
    SUM(patients_refused) AS total_patients_refused,
    ROUND(AVG(patient_satisfaction), 2) AS avg_satisfaction
FROM services_weekly;


![WhatsApp Image 2025-11-07 at 22 05 00_6d94851d](https://github.com/user-attachments/assets/cae848ae-32ad-4b93-bf2a-a83ffcf4fa83)

💡 Key Learnings

Learned to use aggregate functions (COUNT, SUM, AVG, MIN, MAX) for summarizing data.

Understood how to combine CASE with aggregates to apply conditional counting.

Practiced ROUND() function for cleaner numerical presentation.

Strengthened understanding of how SQL can generate insights from large datasets with minimal code.

🧩 Summary
This challenge enhanced skills in:

Performing data aggregation and summarization.

Using conditional logic within aggregate queries.

Making results more readable with rounding and aliases.

Interpreting real-world analytics use cases from hospital data.

#SQLWithIDC #21DaysSQLChallenge #DataAnalytics #LearningJourney #DPDzero #IndianDataClub
