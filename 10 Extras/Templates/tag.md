---
created: <% tp.file.creation_date() %>
modified: 2025-06-16T09:50:14-04:00
---
## <% tp.file.title %>

```dataview
LIST
FROM [[#]]
and !outgoing([[#]])

SORT file.link asc
```
