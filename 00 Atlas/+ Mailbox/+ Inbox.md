---
modified: 2025-07-12T14:04:22-04:00
---
up:: [[+ Home]]
tags:: #map/view

# The Inbox
``` dataview
TABLE WITHOUT ID
 file.link as "Encounters and new notes",
 (date(today) - file.cday).day as "Days alive"

FROM "+ Encounters" and -#readme

SORT file.cday asc

LIMIT 100
```

