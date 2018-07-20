# Expiring Task
This jql will list all the working expiring issues, which the due date field set.
The `membersOf` function is for grouping the task assignee of a given team; e.g. TEAM_NAME = 'Team 1'.
The PROJECT_CATEGORY_LISTS is optional, this is to filter out only some project from preferred category
```sql
(
  status not in (Resolved, Closed)  
  AND timespent is not EMPTY 
  OR status = "In Progress" AND timespent is EMPTY
)
AND assignee in membersOf("TEAM_NAME") 
AND category in (PROJECT_CATEGORY_LISTS) 
AND duedate <= 1d
ORDER BY priority, duedate ASC
```
