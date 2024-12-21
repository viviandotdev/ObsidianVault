```dataview
TABLE URL AS "Link"
FROM #source/article
WHERE contains(status, "#❤️") AND !contains(file.path, "Templates")
SORT file.name ASC
```
