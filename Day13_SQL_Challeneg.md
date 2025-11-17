📘 Day 13 of #21DaysOfSQL — INNER JOIN

Today I explored INNER JOIN, one of the most essential SQL concepts for combining data from multiple tables. INNER JOIN helps in bringing relational data together and extracting meaningful insights.

🔍 What I Learned Today
🔹 INNER JOIN Basics

INNER JOIN returns only the rows that have matching values in both tables.

Syntax:

SELECT columns
FROM table1
INNER JOIN table2
    ON table1.column = table2.column;

🔹 How it works

Looks at each row in the first table

Finds matching rows in the second table based on the join condition

Returns only matching rows

Rows without matches are excluded

🔹 Why INNER JOIN is powerful

Connects related data

Avoids duplicates

Improves data quality

Helps build real-world reports & dashboards

💡 Tips I Learned

✔ Use aliases (p, s, etc.) to keep queries clean
✔ Always qualify column names: p.service, s.service
✔ INNER JOIN is the default for JOIN
✔ You can chain multiple joins
✔ Put extra filters in WHERE, not ON, unless they affect join logic

Daily Challenge:

Question:

Create a comprehensive report showing patient_id, patient name, age, service, and the total number of staff members available in their service. Only include patients from services that have more than 5 staff members. Order by number of staff descending, then by patient name.

Query:

SELECT
   p.patient_id, p.name AS patient_name, p.age,
   p.service, COUNT(s.staff_id) AS total_staff
   FROM patients p
   JOIN staff s
   ON p.service = s.service
   GROUP BY p.patient_id, p.name, p.age, p.service
   HAVING COUNT(s.staff_id)>5
   ORDER BY total_staff DESC, patient_name;

Output:

PATIENT_ID           PATIENT_NAME                                                                                       AGE SERVICE                                             TOTAL_STAFF
-------------------- ---------------------------------------------------------------------------------------------------- ---------- -------------------------------------------------- -----------
PAT-1cc7c1b5         Adam Vaughan                                                                                         2 ICU                                                  32
PAT-bf1b13b6         Alejandro Deleon                                                                                    14 ICU                                                  32
PAT-d78122d6         Alexa Buck                                                                                          73 ICU                                                  32
PAT-f316dd98         Alexander Collins                                                                                   17 ICU                                                  32
PAT-615c986b         Alexandra Dominguez                                                                                 80 ICU                                                  32
PAT-ddd92df7         Alison Brown                                                                                        50 ICU                                                  32
PAT-c012faab         Allison Hickman                                                                                      6 ICU                                                  32
PAT-d4fc50d8         Allison Spencer                                                                                     84 ICU                                                  32
PAT-4275a12b         Alyssa Day                                                                                          69 ICU                                                  32
PAT-c1717ebc         Alyssa Haynes                                                                                       82 ICU                                                  32
PAT-12523d2c         Amanda Sullivan MD                                                                                  65 ICU                                                  32
PAT-91fbb614         Amy Kelley                                                                                          79 ICU                                                  32
PAT-20043fb2         Amy Miller                                                                                          30 ICU                                                  32

📝 Key Takeaways

INNER JOIN is essential for connecting relational tables

Subqueries can be used to apply conditions before joining

This challenge helped me understand real reporting logic:
“Only show patients from services with sufficient staff strength.”


#SQLWithIDC #21DaysSQLChallenge #DataAnalytics #SQL #LearningJourney #GitHubJourney #DPDzero #IndianDataClub
