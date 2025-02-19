---
modified: 2025-02-19T06:40:11-05:00
---
```dataview
TABLE tags AS "Tags"
FROM #source/article
WHERE contains(status, "#❤️") AND !contains(file.path, "Templates")
SORT file.name ASC
```
