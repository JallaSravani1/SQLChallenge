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

Output:

💡 Key Takeaways Today

NULL handling is crucial for clean and accurate results.

COALESCE is powerful for replacing missing data.

COUNT behaves differently with NULL values—important for analytics.

Always check both NULL and empty strings when working with text fields.

📝 Summary

Day 12 helped me understand how to correctly identify, replace, and analyze missing values. Handling NULLs effectively improves the accuracy of any SQL data analysis.

#SQL #DataCleaning #21DaysOfSQL #SQLWithIDC #DataAnalytics #LearningJourney #GitHubJourney
