---
modified: 2025-07-12T08:33:42-04:00
---
up:: [[Life Map]]

[[My Journal]]

[[My Happiness]]

[[My Vision]]

[[My Purpose]]

[[My Interests]]


[[My Values]]


### Notes
```dataview
LIST
FROM "40 Outputs" AND [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "Outbox")
WHERE !contains(file.name, "+ Home")
WHERE !contains(file.name, "Queue")

SORT file.link asc
```