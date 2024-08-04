---
created: 2023-09-15 07:22
modified: Friday 15th September 2023 07:22:41
alias:
---
up::
tags:: #docker

## How to export folder from a docker image?


``` bash
docker cp <container id>:/source/file/path/in/container /destination/on/host # copying /etc directory to host location /tmp docker
cp <contianer id>:/etc/ /tmp
```

### Example
```
docker pull vivianlin61/lireddit:1.0.6
docker images
docker run -it --entrypoint /bin/bash 3a3252e04a23(imageid)
docker ps
docker cp 4a01ef079bfe:/usr/src/app /Users/vivianlin
```


`docker images` : view images
`docker ps` : view running containers

### Resources
[How can I export a folder from a docker image? Tarballs won't open "Unable to export..(Error 1 - Operation not permitted)" - General Discussions / General - Docker Community Forums](https://forums.docker.com/t/how-can-i-export-a-folder-from-a-docker-image-tarballs-wont-open-unable-to-export-error-1-operation-not-permitted/3845)
