---
modified: 2025-06-16T09:33:44-04:00
---
up:: [[+ Home]]
type:: #map/view 

# Sources MOC
This is where I keep tabs on some of the sources I have encountered.

What "sources" should you track? Check out the tags pane. Find "source" and twirl it down. The sources I have decided to include tracking over the years include: *books, movies, songs, research papers, plays, paintings, quotes, videos, speeches, poems, tweets, articles, and newsletters*.

Not included here, but in my personal vault, I enjoy checking out the comprehensive [[Bookshelf]] And to honor the old ones, I also keep a [[Commonplace Book]] based on tags.

## A data view from the Sources folder
This is a simple data view pulling anything from the **Sources** folder.

```dataview
table tags
from "20 Sources"
where !contains(file.path, "20 Sources/Course")
sort file.name asc
```
