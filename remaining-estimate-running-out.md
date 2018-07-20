# The remaining estimate is running out
This jql indicates the issues that their time tracking was spent at least 85%.
This could imply that the tasks will need re-estimation or will be done soon.
```sql
resolution is EMPTY
AND (
  assignee in membersOf("TEAM_NAME")
  OR reporter in membersof("TEAM_NAME")
)
AND category in (PROJECT_CATEGORY_LIST)
AND workratio >= 85 
ORDER BY priority, duedate ASC
```
