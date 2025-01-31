---
created: 2023-09-24 07:20
modified: 2025-01-30T19:09:49-05:00
alias: 
share_link: https://file.obsidianshare.com/e6/5527cd862eda3430ff30e64b6a273c41.html#MXyetY1S7YeSwvHgcTA1M4H4VwVuuT4gesZS3mcTLJI
share_updated: 2023-09-25T21:33:15-04:00
---
up:: [[Deploying nest.js app to dokku]]
type: #note/how-to 
tags:: #deploy #backend #api #docker 
**sources**
[Deploying a PostgresQL, Redis, GraphQL backend and frontend the easiest way! - DEV Community](https://dev.to/lastnameswayne/deploying-a-postgresql-redis-graphql-backend-and-frontend-the-easiest-way-4gob)
[Setup Dokku on Digital Ocean](https://robertcooper.me/post/setup-dokku-digital-ocean)
[How To Host Applications using DigitalOcean and Dokku](https://auth0.com/blog/hosting-applications-using-digitalocean-and-dokku/)

**most important update this**
**next steps, decrease the build size**
[Deploying a Typescript Server to Digital Ocean with Dokku - Part 11 - YouTube](https://www.youtube.com/watch?v=AdHwBKKQHZ4&list=PLN3n1USn4xlnfJIQBa6bBjjiECnk6zL6s&index=13)
## How to deploy an api using Digital Ocean and Dokku

1. [[Set up a custom domain name for your web application]]
2. [[Initialize digital ocean droplet]]
3. Create dokku app
```
dokku apps:create bookcue-api
```
8. Install postgres and redis plugin
```
sudo dokku plugin:install https://github.com/dokku/dokku-postgres.git
sudo dokku plugin:install https://github.com/dokku/dokku-redis.git redis
```
9. Create and link Postgres and Redis database to the app
```
dokku postgres:create bookcue-api-psql
dokku postgres:link bookcue-api-psql bookcue-api
```

```
dokku redis:create retwitter-api-redis
dokku redis:link retwitter-api-redis retwitter-api
```
### Containerize the application
[[Set up local and prod environment variables]] (optional)
[[How to dockerize backend app]]

```
postgres://postgres:594310709d5c947d3bbd4a1736081a74@dokku-postgres-bookcue-api-psql:5432/bookcue_api_psql
```
### Build the docker file and push to docker hub
1. On the local machine, creates a Docker image from the set of instructions defined in the `Dockerfile`
```
docker buildx create --use
docker buildx build --platform linux/amd64 --push -t vivianlin61/bookcue:1 .
```

### Dokku Image Tag Deployment
[Image Tag Deployment - Dokku Documentation](https://dokku.com/docs~v0.8.2/deployment/methods/images/)
[Why can't i pull the newest image by using the latest tag?](https://cloud.ibm.com/docs/Registry?topic=Registry-troubleshoot-docker-latest)
1. Pull the latest image from docker hub
```
docker pull vivianlin61/bookcue:1
```
2. Retag the image to match the created at the start
```
docker tag vivianlin61/bookcue:1 dokku/bookcue-api:latest
```
3. Deploy the app
```
dokku deploy bookcue-api latest
```
**Deploy Changes Script**
``` bash
#!/bin/bash

echo What should the version be?
read VERSION

docker buildx create --use
docker buildx build --platform linux/amd64 --push -t vivianlin61/bookcue:$VERSION .
docker push vivianlin61/bookcue:$VERSION
ssh -i ~/.ssh/id_rsa root@134.209.38.244 "docker pull vivianlin61/bookcue:$VERSION && docker tag vivianlin61/bookcue:$VERSION dokku/api:$VERSION && dokku deploy api $VERSION"

```
### Set up DNS
[Docker DNS Configuration](https://dokku.com/docs~v0.11.6/configuration/domains/)
```
dokku domains:set-global retwittter.co
```

```
dokku domains:report bookcue-api
```

```
dokku domains:add bookcue-api api.retwitter.co
```

```
dokku domains:remove bookcue-api bookcue-api.134.209.64.204.sslip.io
```

![[Screenshot 2024-05-15 at 11.50.52 AM.png]]


**Global vs App Domain**
•Global Domain: Applies to all applications on the Dokku server.
 •App-Specific Domain: Applies only to a specific application.

 Priority:
 •Global Domain: Acts as a fallback domain. If an application does not have a specific domain set, it will use the global domain.
 •App-Specific Domain: Takes precedence over the global domain for the specific application.
### Set up Dokku Let's Encrypt
[GitHub - dokku/dokku-letsencrypt: Automatic Let's Encrypt TLS Certificate installation for dokku](https://github.com/dokku/dokku-letsencrypt)
```
sudo dokku plugin:install https://github.com/dokku/dokku-letsencrypt.git
```

```
dokku letsencrypt:set bookcue-api email linvivian61@gmail.com
```

```
dokku letsencrypt:enable retwitter-api
```


### Finally test the API
```
https://lireddit-api.rereddit.site/graphql
```
![[Screenshot 2023-09-24 at 10.40.45 AM.png]]
