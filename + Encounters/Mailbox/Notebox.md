---
modified: 2025-06-16T09:27:35-04:00
---
up:: [[+ Home]]
tags:: #map/view 

# The Notebox 🗃

```dataview
TABLE WITHOUT ID
 file.link as "Notes to be processed",
 (date(today) - file.cday).day as "Days alive"
from #🟨 
WHERE !contains(file.name, "How to Write Lecture Notes")
WHERE !contains(file.name, "How to Write Atomic Notes")
sort file.name asc
```

## Budding 
Notes that you were in the middle of processing

```dataview
LIST
FROM #note/budding🌿
WHERE !contains(file.name, "How to Write Atomic Notes")
SORT file.name asc
```
