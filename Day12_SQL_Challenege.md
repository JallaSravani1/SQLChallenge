📘 Day 12 of #21DaysOfSQL — NULL Values & Handling Missing Data

Today I learned how SQL deals with NULL, which represents missing or unknown information. Understanding NULLs is essential for cleaning data, building accurate queries, and avoiding logical errors.

🔍 What I Learned Today

🔹 What is NULL?

Not zero

Not an empty string

Represents missing / unknown data

Cannot be compared using = or !=

🔹 Correct NULL Handling

IS NULL

IS NOT NULL

🔹 Replacing NULL → COALESCE

COALESCE(column, 'Default') returns the first non-NULL value—very useful in reporting.

🔹 COUNT behaviour

COUNT(*) → counts all rows

COUNT(column) → skips NULL values

💻 Daily Challenge

Question:

Analyze the event impact by comparing weeks with events vs weeks without events. Show: event status ('With Event' or 'No Event'), count of weeks, average patient satisfaction, and average staff morale. Order by average patient satisfaction descending.

Query:

select case when lower(trim(event)) = 'none' or event is NULL THEN 'No Event'
else 'With Event' end as event_count,
count(distinct week) as week_count,
round(avg(patient_satisfaction),2) as average_satisfaction,
round(avg(staff_morale),2) as average_morale
from services_weekly
group  by
case when lower(trim(event)) = 'none' or event is NULL THEN 'No Event'
else 'With Event' end
order by
round(avg(patient_satisfaction),2) desc;

Output:

![WhatsApp Image 2025-11-15 at 17 03 13_030041a0](https://github.com/user-attachments/assets/a954a46c-b9d4-4e8c-b07f-5195875927e9)


💡 Key Takeaways Today

NULL handling is crucial for clean and accurate results.

COALESCE is powerful for replacing missing data.

COUNT behaves differently with NULL values—important for analytics.

Always check both NULL and empty strings when working with text fields.

📝 Summary

Day 12 helped me understand how to correctly identify, replace, and analyze missing values. Handling NULLs effectively improves the accuracy of any SQL data analysis.

#SQL #DataCleaning #21DaysOfSQL #SQLWithIDC #DataAnalytics #LearningJourney #GitHubJourney
