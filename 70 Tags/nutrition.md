---
created: 2025-08-01 12:50
modified: 2025-08-01T21:35:45-04:00
---
up:: [[My Health]]
**My Diet**
- 2 Eggs

**Lunch**
- I like to skip lunch sometimes and go climbing instead

**Dinner**
- I will have a bigger dinner if I skip lunch

Slow Carb Diet


**Diet Protocol**
[[Slow Carb Diet]]

- eating more protein, try to drink protein before a meal
- exercis

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