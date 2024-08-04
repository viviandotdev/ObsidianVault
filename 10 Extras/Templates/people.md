---
created: <% tp.file.creation_date() %> 
modified: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
---
<% await tp.file.move("/20 Sources/People/" + tp.file.title) %>
up:: [[Sources]]
tags:: #person
dates:: 

## <% tp.file.title %>

### Info


## Extra
### Wiki





