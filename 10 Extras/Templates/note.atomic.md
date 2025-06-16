---
created: <% tp.file.creation_date() %>
modified: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
alias:
---
up::
type:: #note/atomic🌳
source::
## <% tp.file.title %>



### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```
