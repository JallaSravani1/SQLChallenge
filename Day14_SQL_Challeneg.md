📘 Day 14 – SQL With IDC Challenge

Topic: LEFT JOIN & RIGHT JOIN – Working With Unmatched Records

Daily Challenge:

Question:Create a staff utilisation report showing all staff members (staff_id, staff_name, role, service) and the count of weeks they were present (from staff_schedule). Include staff members even if they have no schedule records. Order by weeks present descending.

SQL Query:

SELECT
    s.staff_id,
    s.staff_name,
    s.role,
    s.service,
    COALESCE(SUM(ss.present), 0) AS weeks_present
FROM staff s
LEFT JOIN staff_schedule ss
    ON s.staff_id = ss.staff_id
GROUP BY
    s.staff_id, s.staff_name, s.role, s.service
ORDER BY
    weeks_present DESC;

OUTPUT:

<img width="1280" height="657" alt="image" src="https://github.com/user-attachments/assets/0ba1cca0-aa73-4150-a942-1e36850cf031" />

💡 What I Learned Today

LEFT JOIN and RIGHT JOIN help bring together rows from two tables *even when some records don’t match*.

🧩 Summary

Today’s challenge improved my understanding of:

Handling missing data with LEFT/RIGHT JOIN

Exploring relationships between tables

Writing analytical queries involving unmatched rows

Real-world SQL reporting scenarios

#DPDzero#IndianDataClub#SQLWithIDC#21DaysSQLChallenge #DataAnalytics

This is extremely useful for real-world data analysis where missing data is common.

