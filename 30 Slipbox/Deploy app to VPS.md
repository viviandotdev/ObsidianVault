---
modified: 2025-02-05T20:02:16-05:00
---
[[How to build and deploy a sass]]

**Digital Ocean**
[[Initialize digital ocean droplet]]

[[How to deploy an api using Digital Ocean and Dokku]]

[[Deploying nest.js app to dokku]]


**AWS**
[[How to deploy backend using AWS EC2]]

```bash
pnpm run build
# docker build -t vivianlin61/bookshelf:latest .
docker buildx create --use
# docker buildx build --platform linux/amd64 -t vivianlin61/bookshelf:3 .
# docker push vivianlin61/bookshelf:3 .

docker buildx build --platform linux/amd64 --push -t vivianlin61/bookshelf:2 .

ssh root@138.197.77.102 "docker pull vivianlin61/bookshelf:1 && docker tag vivianlin61/bookshelf:1 dokku/bookshelf-api:latest && dokku deploy bookshelf-api latest"

```