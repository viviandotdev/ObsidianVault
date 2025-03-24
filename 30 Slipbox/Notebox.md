up:: [[+ Home]]
tags:: #map/view 

# The Notebox 🗃

## Seedling 
Notes that need to be processed

```dataview
List
from #note/seedling🌱 
WHERE !contains(file.name, "How to Write Lecture Notes")
WHERE !contains(file.name, "How to Write Atomic Notes")
sort file.name asc
```

## Budding 
Notes that you were in the middle of processing

```dataview
LIST
FROM #note/budding🌿
WHERE !contains(file.name, "How to Write Atomic Notes")
SORT file.name asc
```
