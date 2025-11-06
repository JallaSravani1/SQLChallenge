📘 Day 4 – SQL With IDC Challenge

🗓 Challenge Task
Find the 3rd to 7th highest patient satisfaction scores from the patients table, showing patient_id, name, service, and satisfaction. Display only these 5 records.

Query

SELECT patient_id, name, service, satisfaction
FROM patients
ORDER BY satisfaction DESC
OFFSET 2 ROWS FETCH NEXT 5 ROWS ONLY;

output:
![WhatsApp Image 2025-11-06 at 12 33 58_32fbe1ac](https://github.com/user-attachments/assets/70783fa7-f740-48fa-82ff-0545ac47e62b)

💡 Key Learnings

-Understood the use of LIMIT and OFFSET for pagination and selective data retrieval.

-Learned how to fetch a specific range of records (e.g., 3rd to 7th) efficiently.

-Practiced combining ORDER BY with LIMIT to produce predictable and sorted results.

-Realized how pagination helps manage large datasets for user-friendly data display.

🧩 Summary
-This challenge reinforced concepts like:

-Pagination logic using LIMIT and OFFSET

-The importance of ORDER BY for consistent query outputs

#SQLWithIDC #21DaysSQLChallenge #DataAnalytics #LearningJourney #DPDzero #IndianDataClub

Practical techniques to extract subsets of ordered data
