# Expiring Open tasks
Similar to [Expirign Tasks](https://github.com/subhajai/jira-jql/blob/master/expiring-tasks.md), but only list the no progress issue (`Sttaus=Open`).
So, they could be delegated to other teams.

```sql
status in (Open) AND assignee in membersOf("TEAM_NAME")
AND category in (PROJECT_CATEGPRY_LISTS)
AND duedate <= 1d 
AND timespent is EMPTY 
ORDER BY priority, duedate ASC
```
