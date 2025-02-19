---
modified: 2025-02-19T08:16:29-05:00
---
To Read Articles
#🟩 
#🟥 
#🟨  

```dataview
TABLE tags AS "Tags", Status as "Status"
FROM "20 Sources/Raindrops"
WHERE contains(Status, "#🟥") AND !contains(file.path, "Templates")
```