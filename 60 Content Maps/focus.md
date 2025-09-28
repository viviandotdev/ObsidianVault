---
created: 2025-09-27 19:53
modified: 2025-08-01T18:24:06-04:00
---
up::
type:: #map/content
tags::

[[flow state]]

**Books**
[[Flow by Mihaly Csikszentmihalyi]]
[[Deep Work]]
**Youtube**
[Rian Doris - YouTube](https://www.youtube.com/@riandoris)



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