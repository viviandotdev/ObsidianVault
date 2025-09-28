---
modified: 2025-06-24T07:32:27-04:00
---
up:: [[+ Home]]
tags:: #map/view  

# Life Map 🗺
I'm amazed at how many people don't zoom out and consider how to live a good life.

## Compass 🧭
These are the dials that determine where I go.

- My Direction & Drivers

**Reflection**
	01 - [[My Values]] | [[My Perspectives]] | [[My Interests]] | [[My Purpose]]  | [[My Vision]] | [[My Happiness]] | [[My Health]] |
**Action**
	02 - [[Tools]] | [[My Workflows]] | [[My Finances]] | [[My Goals]] | [[My Systems]] |  [[My Routines]]
	03 - [[My Experiences]] |  [[Life Reflections]]
	04 - [[My Manifesto]] | [[My Career]]
	05 - [[My Obituary]]


### Notes
```dataview
LIST
FROM "50 Spaces" AND [[#]]
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