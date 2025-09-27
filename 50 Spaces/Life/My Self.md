---
modified: 2025-07-12T08:33:42-04:00
---
up:: [[Life Map]]
# My Self

**Table of Contents**



[[My Personality]]
[[what is your MBTI personality type?]]

[[My Happiness|What makes me happy]]


[[My Vision]]


[[My Interests]]


**My **
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