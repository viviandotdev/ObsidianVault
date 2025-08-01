---
created: 2025-08-01 12:46
modified: 2025-08-01T12:46:55-04:00
---
## self-improvement

[[success]]

[[ha]]

[[productivity]]

```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "Outbox")
SORT file.link asc
```
