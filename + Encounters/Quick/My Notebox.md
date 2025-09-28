---
modified: 2025-06-22T13:24:40-04:00
---
up:: [[+ Home]]
tags:: #map/view 

# The Notebox 🗃
**Prompts**



```dataview 
TABLE WITHOUT ID
 file.link as "Prompts ",
 (date(today) - file.cday).day as "Days alive"
from #note/prompt 
WHERE !contains(file.name, "How to Write Lecture Notes")
WHERE !contains(file.name, "How to Write Atomic Notes")
sort file.name asc
```

```dataview 
TABLE WITHOUT ID
 file.link as "Notes 🟥 ",
 (date(today) - file.cday).day as "Days alive"
from #🟥  
WHERE !contains(file.name, "How to Write Lecture Notes")
WHERE !contains(file.name, "How to Write Atomic Notes")
sort file.name asc
```

```dataview
TABLE WITHOUT ID
 file.link as "Notes 🟨 ",
 (date(today) - file.cday).day as "Days alive"
from #🟨 
WHERE !contains(file.name, "How to Write Lecture Notes")
WHERE !contains(file.name, "How to Write Atomic Notes")
sort file.name asc
```


