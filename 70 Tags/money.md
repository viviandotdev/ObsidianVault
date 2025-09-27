---
created: 2025-06-15 07:07
modified: 2025-08-01T12:55:15-04:00
---
up:: [[economics]]

```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "+ Home")
WHERE !contains(file.name, "Outbox")
SORT file.link asc
```
