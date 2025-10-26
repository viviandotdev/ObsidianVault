---
created: 2025-09-27 17:18
modified: 2025-08-01T18:24:06-04:00
---

**Personality**
[[Which attachment style are you?]]
[[Why am I introverted?]]
[[What are your interests?]]
[[What is your purpose?]]
[[What is your vision?]]

**Happiness**
[[What makes you happy?]]
[[What makes me unhappy?]]

**Relationships**
[[do you care more to be loved or loved?]]
[[Why have you never been in a relationship?]]


**Mind**


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
