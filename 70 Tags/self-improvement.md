---
created: 2025-08-01 12:46
modified: 2025-08-01T21:30:17-04:00
---
## self-improvement

[[success]]

[[habits]]

[[happiness]]

[[productivity]]

[[goals]]

# Notes
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "Outbox")
WHERE !contains(file.name, "+ Home")
WHERE !contains(file.name, "Queue")

SORT file.link asc
```