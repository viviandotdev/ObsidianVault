---
created: <% tp.file.creation_date() %>
modified: 2025-06-15T12:58:22-04:00
alias: 
---
## <% tp.file.title %>

```dataview
LIST
FROM [[#]]
and !outgoing([[#]])

SORT file.link asc
```



