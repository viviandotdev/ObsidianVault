---
created: 2025-06-24 06:48
modified: 2025-06-24T07:29:59-04:00
---
up:: [[language]]
tags::
## chinese


```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "+ Home")
SORT file.link asc
```