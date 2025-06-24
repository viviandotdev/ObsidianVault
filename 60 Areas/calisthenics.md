---
created: 2025-06-24 07:06
modified: 2025-06-24T07:29:46-04:00
---
## calisthenics


```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "+ Home")
SORT file.link asc
```