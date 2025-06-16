---
modified: 2025-06-16T07:09:57-04:00
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


---
Thoughts come in hot 🌶. But after a few days, they cool down ❄️.

This view looks at the 20 newest notes in your **+ Encounters** folder. As you process each note, make connections, add details, move them to the best folder,  and delete everything that no longer sparks ✨.
If you want to encounter some new things, check out: [🐦](https://www.twitter.com) or [📚](https://readwise.io/lyt/)
