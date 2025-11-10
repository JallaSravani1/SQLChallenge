📘 Day 7 (10/11): HAVING Clause

💻 Topics Covered:

Filtering grouped results using the HAVING clause

🧩 Concept Overview

The HAVING clause filters groups created by GROUP BY, much like how WHERE filters individual rows.

| Clause | Used For         | Works On        | Supports Aggregates |
| :----- | :--------------- | :-------------- | :------------------ |
| WHERE  | Filtering rows   | Before grouping | ❌ No               |
| HAVING | Filtering groups | After grouping  | ✅ Yes              |


💡 Tips & Tricks

- Execution Order: WHERE → GROUP BY → HAVING → ORDER BY
- Use WHERE for row filtering (faster), HAVING for group filtering
- HAVING requires GROUP BY
- You can reference aliases in HAVING (depends on database)
- Combine multiple conditions with AND / OR

🧭 Daily Challenge

Question:
Identify services that refused more than 100 patients in total and had an average patient satisfaction below 80.
Show service name, total refused, and average satisfaction.

Query:

select service, sum(patients_Refused) as total_refused, avg(patient_satisfaction) as average_satisfaction from services_weekly group by service having sum(patients_refused) > 100 and avg(patient_satisfaction) < 80;

Output:

<img width="1471" height="189" alt="Screenshot 2025-11-10 191531" src="https://github.com/user-attachments/assets/17347120-ad1f-4328-a49c-5f06d35950ed" />

🌱 What I Learned Today

Understood the difference between WHERE and HAVING clauses.

Learned that HAVING is used to filter aggregated data.

Practiced combining multiple conditions with AND and OR.

Realized the importance of execution order in SQL queries.

#SQLWithIDC #LearnSQL #DataAnalytics #DPDZero #IndianDataClub #SQLDailyChallenge
