---
created: 2025-08-24 14:43
modified: 2025-08-01T21:35:00-04:00
---
[[Perfect friend]]

**quotes**
"A friend is a single soul dwelling in two bodies."
Aristotle
### Notes
```dataview
LIST
FROM "30 Notes" AND [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "Outbox")
WHERE !contains(file.name, "+ Home")
WHERE !contains(file.name, "Queue")

SORT file.link asc
```

### Sources
```dataview
LIST
FROM "20 Sources" AND [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "Outbox")
WHERE !contains(file.name, "+ Home")
WHERE !contains(file.name, "Queue")

SORT file.link asc
```