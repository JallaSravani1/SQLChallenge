📘 Day 15 (19/11): Multiple Joins
Topics: Joining more than two tables, complex relationships

Today I learned how to combine data from three or more tables using multiple joins.
Multiple joins help us build real-world analytical reports that need data from several related tables.

📚 Reading & Notes

🔹 Basic Syntax
SELECT columns
FROM table1
JOIN table2 ON table1.key = table2.key
JOIN table3 ON table2.key = table3.key
LEFT JOIN table4 ON table3.key = table4.key;

🔹 Join Order

SQL evaluates joins left → right

Each join layer builds on the previous result

You can mix INNER JOIN, LEFT JOIN, RIGHT JOIN based on the requirement

💡 Tips & Tricks

✔ Start with the main table
✔ Use LEFT JOIN when you want all rows from the left table
✔ Join order matters—this:

FROM table1
LEFT JOIN table2 ON ...
INNER JOIN table3 ON ...


is NOT the same as:

FROM table1
INNER JOIN table3 ON ...
LEFT JOIN table2 ON ...


✔ Join conditions can refer to earlier tables
✔ Use DISTINCT or GROUP BY to avoid duplicate rows
✔ Add joins one-by-one to validate results

Question:

Create a comprehensive service analysis report for week 20 showing: service name, total patients admitted that week, total patients refused, average patient satisfaction, count of staff assigned to service, and count of staff present that week. Order by patients admitted descending.
GROUP BY 

Query:

SELECT
  sw.service,
  sw.patients_admitted,
  sw.patients_refused,
  sw.patient_satisfaction        AS avg_patient_satisfaction,
  COUNT(DISTINCT s.staff_id)     AS total_staff_assigned,
  SUM(CASE WHEN ss.present = 1 THEN 1 ELSE 0 END) AS staff_present_count
FROM services_weekly sw
LEFT JOIN staff s
  ON sw.service = s.service
LEFT JOIN staff_schedule ss
  ON s.staff_id = ss.staff_id
  AND ss.week = sw.week
WHERE sw.week = 20
GROUP BY
  sw.service,
  sw.patients_admitted,
  sw.patients_refused,
  sw.patient_satisfaction
ORDER BY sw.patients_admitted DESC;

Output:

![WhatsApp Image 2025-11-19 at 19 12 03_aa8c0ef4](https://github.com/user-attachments/assets/da48d96f-273c-4c72-af48-3c4d598ebf01)

✅ Key Learnings

Understood how multiple joins help combine data from 3+ tables.

Learned the importance of join order (left → right execution).

Practiced using INNER JOIN and LEFT JOIN together for real reports.

Explored how to avoid duplicates using DISTINCT and GROUP BY.

Saw how multiple joins help build complex analytics like service reports, staff availability, and weekly summaries.

Improved confidence in writing clean, structured SQL queries with aliases.

#100DaysOfSQL #Day15 #SQLJoins 
#SQLLearning #DatabaseManagement 
#WomenInTech #CodersCommunity 
#LearnSQL #DataEngineering 
#TechJourney #MultipleJoins 
#SQLPractice #GitHubLearning

