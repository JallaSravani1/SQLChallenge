🌼 Day 19 (25/11): Window Functions – ROW_NUMBER, RANK, DENSE_RANK

Today I explored Window Functions, one of the most powerful features in SQL for performing calculations across rows without reducing or grouping the dataset. These functions help assign rankings, generate row numbers, and analyze data within logical partitions.

📘 What I Learned Today

🔹 Window Functions:
Window functions operate on a set of rows related to the current row while keeping all rows in the output. They work using the OVER clause.

🔹 PARTITION BY:
Divides data into groups. The window function is applied separately to each group.

🔹 ORDER BY:
Defines the order in which numbering or ranking is applied inside each partition.

🏆 Ranking Functions Explored

⭐ ROW_NUMBER

Assigns a unique sequential number to each row.
No duplicates; numbering always increases by one.

⭐ RANK

Assigns the same rank to matching values.
Leaves gaps in ranking when ties exist.
Example pattern: 1, 2, 2, 4…

⭐ DENSE_RANK

Similar to RANK, but does not leave gaps.
Example pattern: 1, 2, 2, 3…

📊 How These Functions Are Used

Ranking patients within each service based on satisfaction.

Assigning unique row numbers to patients or staff.

Getting top N records from each category (like top 3 weeks per service).

Comparing services based on admissions or satisfaction.

Analyzing trends without losing any rows, unlike GROUP BY.


💡 Key Insights & Tips

PARTITION BY is optional — without it, ranking applies to the entire dataset.
Use:
ROW_NUMBER when you need unique identifiers.

RANK when equal values should share a rank.

DENSE_RANK when equal values should not create gaps.

Window functions cannot be directly filtered — use a subquery to filter top results.

ORDER BY inside OVER controls ranking;

ORDER BY in the query controls the final output.

Window functions preserve all rows — they do not collapse data like aggregate functions.

🎯 Daily Challenge
For each service, determine the top three weeks with the highest patient satisfaction. Display the service, week, satisfaction score, admission count, and the ranking of each week.

Query & Output:

![WhatsApp Image 2025-11-25 at 18 52 45_e004ebee](https://github.com/user-attachments/assets/b5d8421c-6323-4bb8-bca2-8efeb0331575)

Key Learnings:

Understood the difference between ROW_NUMBER, RANK, and DENSE_RANK.

Learned how to analyze grouped data using PARTITION BY.

Gained clarity on real-world applications like top-N reports and performance ranking.

Strengthened my ability to think analytically about ordered and partitioned data.




#100DaysOfSQL #Day19 #SQLWindowFunctions 
#DataAnalytics #SQLLearning #WomenInTech
#TechJourney #DatabaseEngineering
#LearnSQL #DataScienceBasics
