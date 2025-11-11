📘 Day 8 – SQL With IDC Challenge

🗓 Challenge Task:

Create a patient summary showing patient_id, full name in UPPERCASE, service in lowercase, age category (Senior, Adult, Minor), and name length — but only for patients whose name length is greater than 10 characters.

Query:

SELECT patient_id, UPPER(name), LOWER(service), age, CASE WHEN age>=65 THEN 'Senior' WHEN age>=18 THEN 'Adult' ELSE 'Minor' END AS age_category, LENGTH(name) as name_length FROM patients WHERE LENGTH(name) > 10

Output:

<img width="1324" height="612" alt="image" src="https://github.com/user-attachments/assets/d979da19-6503-420d-8c42-ed68874a914d" />

922 rows selected.

💡 Key Learnings:

Learned how to manipulate text using string functions like UPPER(), LOWER(), and LENGTH().

Practiced conditional logic using the CASE statement.

Understood how to combine multiple string and logical operations in a single query.

Discovered how to filter data based on string length.

🧩 Summary:
This challenge improved my understanding of SQL string manipulation and data presentation. It showed how small transformations can make reports cleaner and more meaningful.

#SQLWithIDC #21DaysSQLChallenge #DataAnalytics #LearningJourney #DPDzero #IndianDataClub
