---
created: 2025-09-27 12:19
modified: 2025-08-01T21:35:00-04:00
---

up:: [[writing]]

[[QEC Note-Taking]]
[[How to take book notes]]
[[How I Take Smart Notes- Books]]
[[Process for reading books and making notes]]
[[How to build a daily writing habit]]



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