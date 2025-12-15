---
created: 2025-12-15 07:49
modified: 2025-06-22T19:16:10-04:00
---
type:: #source/course 
tags::


**Introduction**
==4 Points that influenced our design==
- Component failures are the norm rather than the exception
- Files are huge, Multi-GB is common
- Most files are mutated by appending new data rather than overwriting existing data
- Increase flexibility by co-designing applications the file-system [[API]]
	- They relaxed the consistency model to simply the file system to prevent burden on the applications
	- [[Atomic]] append operation so that multiple clients can append concurrently to a file without application synchronization

**Design Overview**
==Assumptions==
- Components will fail often so the system must constantly monitor itself to detect and resolve this failures
- Multi-GB files are common and should be optimized, Small files will also be supported but they don't need to optimized.
- 


watch the paper explained google file system
watch the google file system lecture
then reverse engineer from the source, finding all the points that they were important

go through their doc and your doc and make sure all the important points are included
**Related Sources**
[Paper Explained The Google File System](https://www.youtube.com/watch?v=LXhgFAZroG8)
[The Google File System](https://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf)
### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```

