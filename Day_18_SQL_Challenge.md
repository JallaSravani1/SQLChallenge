🌼 Day 18 (24/11): UNION and UNION ALL

Topics: Combining result sets using UNION & UNION ALL

Today I explored how SQL allows us to combine multiple result sets into a single output using UNION and UNION ALL. These operators are powerful when working with data spread across multiple tables.

📘 Understanding UNION & UNION ALL
UNION

Combines results from multiple SELECT statements

Removes duplicate rows

Slightly slower because it performs a distinct check

UNION ALL

Combines results and keeps duplicates

Faster and preferred when duplicates are acceptable

💡 Tips & Tricks

Use UNION ALL when you know duplicates won't occur or when you need all rows — it's faster.

Column names from the first SELECT are used in the final output.

Always place ORDER BY at the end of the entire UNION block.

Question: Create a comprehensive personnel and patient list showing: identifier (patient_id or staff_id), full name, type ('Patient' or 'Staff'), and associated service. Include only those in 'surgery' or 'emergency' services. Order by type, then service, then name.

Query:

SELECT 
    identifier,
    full_name,
    person_type,
    service
FROM (
    SELECT 
        patient_id AS identifier,
        name AS full_name,
        'Patient' AS person_type,
        service
    FROM patients
    WHERE LOWER(service) IN ('surgery', 'emergency')
    UNION ALL
    SELECT 
        staff_id AS identifier,
        staff_name AS full_name,
        'Staff' AS person_type,
        service
    FROM staff
    WHERE LOWER(service) IN ('surgery', 'emergency')
)
ORDER BY 
    person_type,
    service,
    full_name;

Output:

![WhatsApp Image 2025-11-23 at 12 11 30_47cb38ac](https://github.com/user-attachments/assets/a97cd506-45ab-4717-9b3d-9d87a8c8b046)

🌟 Key Learnings

Learned the difference between UNION and UNION ALL.

Understood how to merge data with matching columns and compatible types.

Practiced adding identifiers/literals to understand source tables.

Improved understanding of sorting and combining multiple queries.

Strengthened skills in building combined reports from multiple tables.

#100DaysOfSQL #Day18 #SQLUnion 
#SQLLearning #DatabaseQueries 
#LearnSQL #DataEngineering 
#WomenInTech #TechJourney 
#UNIONvsUNIONALL #SQLPractice 
#CodeEveryday #GitHubLearning


    
