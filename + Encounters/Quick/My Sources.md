


```dataview
TABLE WITHOUT ID
	status as Status,
	rows.file.link as Article
FROM  "20 Sources"
WHERE !contains(file.path, "Templates")
GROUP BY status
SORT status ASC
```