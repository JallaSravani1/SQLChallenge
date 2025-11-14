Daily Challenge (Day 11): 

DISTINCT + Handling Duplicates

Question:

Find all unique combinations of service and event type from the services_weekly table where events are not null or none, along with the count of occurrences for each combination. Order by count descending.

Query:

select distinct service, event, count(service) as count
  from services_weekly
  group by service, event
  order by count(service) desc;

  Output:

  ![WhatsApp Image 2025-11-14 at 18 52 46_b66326e2](https://github.com/user-attachments/assets/81a87b66-1fa8-4139-b209-6918a2b4e288)

  💡 Key Learnings Today

DISTINCT considers all selected columns together.

GROUP BY is more powerful for deduplication + aggregation.

Use COUNT(DISTINCT column) when you need unique counts.

Always filter out unwanted values (like NULL or 'none') before grouping.

📝 Summary

Day 11 was all about identifying unique patterns in data and handling duplicates effectively using DISTINCT and GROUP BY. Understanding these techniques will help in building cleaner datasets and writing better analytical queries. 

#SQL #SQLWithIDC #21DaysOfSQL #DataAnalytics #LearningJourney #GitHubJourney
