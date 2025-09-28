---
created: 2024-06-30 21:05
modified: 2025-06-28T07:47:29-04:00
---
type:: #map/area
source::



### Links to this page
```dataview
table file.mtime.year + "-" + file.mtime.month + "-" + file.mtime.day as Modified
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```
