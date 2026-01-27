---
modified: 2025-06-22T13:24:40-04:00
---
up:: [[+ Home]]
tags:: #map/view 

# The Notebox 🗃
-**process your sources**
- add links to the source
- like a source  (if it is a article you like) 
- create ideas from the source (perspectives/ideas/mental-models/methods/action)
	- [[How to Write Notes]]
	- [[How to Write an Mini Essay]]
	- [[How to write a newsletter]]
- create action notes from the source
- 




```dataview
TABLE WITHOUT ID
 file.link as "Notes 🟨 ",
 (date(today) - file.cday).day as "Days alive"
from #🟨 
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


