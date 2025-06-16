---
created: <% tp.file.creation_date() %>
modified: 2025-06-16T08:35:06-04:00
---
## <% tp.file.title %>

```dataview
table file.mtime.year + "-" + file.mtime.month + "-" + file.mtime.day as Modified
FROM [[#]]
and !outgoing([[#]])

SORT file.link asc
```
