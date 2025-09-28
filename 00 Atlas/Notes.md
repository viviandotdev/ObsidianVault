--
modified: 2025-06-23T06:40:43-04:00
---
up:: [[+ Home]] 
type:: #map/view 
### Here is a view of  the notes folder

```dataview
TABLE tags, type as "Type"
FROM "30 Notes" and -#x/index and -#x/readme
WHERE type = null OR type = ""
SORT file.name ASC

```

``` dataview
table tags, type as "Type"
FROM "30 Notes" and -#x/index and -#x/readme

SORT file.name ASC
```
