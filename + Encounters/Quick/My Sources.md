
```dataview
TABLE WITHOUT ID
	type as Type,
	rows.file.link as Article
FROM  "20 Sources"
WHERE !contains(file.path, "Templates") AND length(split(file.path, "/")) = 2
GROUP BY status
SORT status ASC
```