📘 Day 10 – SQL With IDC Challenge

🗓 Topic: CASE Statements (Conditional Logic)

💭 Concepts Covered: CASE WHEN, conditional aggregation, derived columns

Question:

Question: Create a service performance report showing service name, total patients admitted, and a performance category based on the following: 'Excellent' if avg satisfaction >= 85, 'Good' if >= 75, 'Fair' if >= 65, otherwise 'Needs Improvement'. Order by average satisfaction descending.

💻 SQL Query:

select service, sum(patients_admitted) as total_patients_admitted,
  case
  when avg(patient_satisfaction) >= 85 then 'Excellent'
  when avg(patient_satisfaction) >= 75 then 'Good'
  when avg(patient_satisfaction) >= 65 then 'Fair'
  else 'Need Improvement'
  end as satisfaction_level
  from services_weekly
  group by service
  order by avg(patient_satisfaction) desc;

  Output:

  ![WhatsApp Image 2025-11-13 at 19 58 16_152499d7](https://github.com/user-attachments/assets/b239e9a2-2f13-4ca5-9a02-77ae3715416f)

  💡 Key Learnings:

Understood how to use CASE for conditional logic in SQL — similar to if-else in programming.

Learned to perform conditional aggregation with SUM(CASE WHEN … END).

Discovered that CASE can be used anywhere a column can appear — even in ORDER BY.

Realized the importance of including an ELSE clause to handle unexpected cases.

🧩 Summary:

Today’s challenge enhanced my analytical SQL skills by introducing decision-making logic within queries. Using CASE made it easy to categorize, group, and label data — a vital step in creating insightful reports.

#SQLWithIDC #21DaysSQLChallenge #IndianDataClub #DPDzero #DataAnalytics #SQLLearning


  
