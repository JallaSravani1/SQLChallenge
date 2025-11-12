📘 Day 9 – SQL With IDC Challenge

🗓 Challenge Task:

Calculate the average length of stay (in days) for each hospital service, showing only those services where the average stay is more than 7 days. Also, display the count of patients and order the results by average stay (descending).

Query:

 SELECT
     service,
        AVG(DEPARTURE_DATE - ARRIVAL_DATE) AS avg_stay,
        COUNT(patient_id) AS patient_count
    FROM patients
    GROUP BY service
    HAVING AVG(DEPARTURE_DATE - ARRIVAL_DATE) > 7
    ORDER BY avg_stay DESC;

  output:
  ![WhatsApp Image 2025-11-12 at 19 45 30_30dc82c3](https://github.com/user-attachments/assets/03cac91a-7b56-49a8-b334-16ca3f738ec2)

💡 Key Learnings:

Learned how to calculate date differences using the JULIANDAY() function.

Understood how to aggregate date calculations with AVG() and filter them using HAVING.

Practiced rounding averages for better readability.

Observed how date-based analytics reveal hospital service efficiency and patient trends.

🧩 Summary:

This challenge deepened my understanding of date manipulation and aggregation in SQL. I explored how to derive time-based insights such as average stay duration, which are vital in real-world data analysis.

#SQLWithIDC #21DaysSQLChallenge #DataAnalytics #LearningJourney #DPDzero #IndianDataClub
