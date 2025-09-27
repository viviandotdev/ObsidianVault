---
modified: 2025-08-01T21:36:12-04:00
---
tags::

### **People**
Writers/Authors
- [[Sam Altman]]
- [[Tim Ferris]]
- [[Cal Newport]]
- [[James Clear]]
- [[Thomas Frank]]
- [[Paul Graham]]

**Youtubers**
- [[Ali Aabal]]
- [[Dan Koe]]
- [[Reysu]]
- [[James Scholz]]


**Books**
- [[Getting Things Done]]
- [[Deep work]]
- [[Ultralearning by Scott Young]]
- [[Atomic Habits by James Clear]]
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


**Books**
```dataview
LIST
FROM "20 Sources" AND [[#]]AND #source/book 
and !outgoing([[#]])
WHERE !contains(file.name, "Outbox")
WHERE !contains(file.name, "+ Home")
WHERE !contains(file.name, "Queue")

SORT file.link asc
```



```dataview
LIST
FROM "20 Sources" AND [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "Outbox")
WHERE !contains(file.name, "+ Home")
WHERE !contains(file.name, "Queue")

SORT file.link asc

```
