---
modified: 2025-06-16T09:28:12-04:00
---
ep:: [[+ Home]] / [[Sources]] 

## Articles

```dataview
TABLE WITHOUT ID
	status as Status,
	rows.file.link as Book
FROM  #source/article 
WHERE !contains(file.path, "Templates")
GROUP BY status
SORT status ASC
```
