---
modified: 2025-02-19T07:00:46-05:00
---
Articles


#🟨  
#🟥 
```dataview
TABLE file.name, tags AS "Tags"
FROM "20 Sources/Raindrops"
WHERE contains(status, "#🟥")
SORT modified DESC
```