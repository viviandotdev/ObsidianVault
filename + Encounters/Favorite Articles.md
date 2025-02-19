---
modified: 2025-02-19T06:38:11-05:00
---
```dataview
TABLE URL AS "Link"
FROM #source/article
WHERE contains(status, "#❤️") AND !contains(file.path, "Templates")
SORT file.name ASC
```
