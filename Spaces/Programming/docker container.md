---
created: 2024-06-08 15:54
modified: 2025-06-15T18:31:50-04:00

---
tags:: [[docker]]
 An instance of an [[docker image]] that runs as an isolated process on the host machine. Lightweight executable package with everything you need to run an application.
Containers are **mutable** and can be changed

```
docker run -d --name my-container ubuntu:latest  # Runs a container from the Ubuntu image
docker stop my-container                         # Stops the running container
docker rm my-container                           # Removes the container
```

**Container Lifecycle**
Created from images, run, stopped, and removed.
### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```
