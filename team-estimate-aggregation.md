# Team tasks estimate aggregation.
This jql lists all the tasks of a TEAM_NAME.
It will includes the summarize of the Original Estimate, Remainin Estimate and Time Spent.
The jql functions `aggregateExpression` require [Adaptive Script Runner addon](https://scriptrunner.adaptavist.com/latest/jira/quickstart.html)
```sql
assignee in membersOf("TEAM_NAME") 
AND category in (PROJECT_CATEGORY_LIST) 
AND resolution is EMPTY 
AND issueFunction in aggregateExpression(
                       "Original Estimate", "originalEstimate.sum()", 
                       "Time spent", " timespent.sum()",
                       "Remaining Estimate", "remainingEstimate.sum()",
                       "Actual Remaining Hours", "originalEstimate.sum() - timespent.sum()"
                      )
ORDER BY priority, duedate ASC
```

**Example**: https://scriptrunner.adaptavist.com/latest/jira/jql-functions.html#_aggregateexpression
