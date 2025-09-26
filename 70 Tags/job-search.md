---
created: 2024-06-30 21:05
modified: 2025-07-11T19:40:09-04:00
---
source::
type:: #area 
## job-search




### Links to this page
```dataview
table file.mtime.year + "-" + file.mtime.month + "-" + file.mtime.day as Modified
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```
