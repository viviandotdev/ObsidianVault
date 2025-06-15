---
created: 2025-06-15 18:31 
modified: Sunday 15th June 2025 18:31:11
alias: 
---
tags:: [[docker]]
## useful docker commands

Remove image
```
docker image rm image-id -- force
```
See all image
```
docker image ls
```
Troubleshooting
```
dokku trace:off
```

**List all containers**
```
docker ps -a
```

**Access a running container**
```
docker exec -it <container_id_or_name> /bin/bash
```



### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



