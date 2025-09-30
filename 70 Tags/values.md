---
modified: 2025-08-01T21:35:00-04:00
---
tags:: [[happiness]]

**What are values?**
They are principles and beliefs that guide our actions, decisions.
Similar to morals, they help you decide what is right your wrong and what your beliefs are

In order to be [[happiness|happy]] you need to live true to your values and surround yourself with people with similar values as you.

I have created a list of my values here [[My Values]]


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