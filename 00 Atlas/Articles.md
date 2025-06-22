---
modified: 2025-06-22T12:17:49-04:00
---
up:: [[+ Home]] / [[Sources]] 

## Articles

```dataview
TABLE WITHOUT ID
	status as Status,
	rows.file.link as Article
FROM  #source/article 
WHERE !contains(file.path, "Templates")
GROUP BY status
SORT status ASC
```
