---
created: 2023-09-24 06:21
modified: 2025-06-15T07:13:25-04:00
alias: 
---
up::
tags:: [[docker]]
## Docker

What is docker?
Is a platform designed to help developers build, test and deploy containerized applications

### Useful docker commands
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

[How To Remove Docker Images, Containers, and Volumes | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)


[Step-by-Step Guide: Setting Up a NestJS Application with Docker and PostgreSQL - DEV Community](https://dev.to/chukwutosin_/step-by-step-guide-setting-up-a-nestjs-application-with-docker-and-postgresql-5hei)


[[How to debug docker files?]]







### Unmentioned notes, with related tag
These notes have the tag `#` and are not mentioned above.
```dataview
LIST 

FROM #docker
and !outgoing([[#]])

SORT file.link asc
```