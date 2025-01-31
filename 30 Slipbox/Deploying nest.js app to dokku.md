---
created: 2024-07-12 10:12
modified: 2025-01-30T20:04:10-05:00
alias: 
---
up::  [[How to deploy an api using Digital Ocean and Dokku]]
type:: #note/atomic🌳 
links::
## Deploying nest.js app to dokku

Here's the updated markdown with smaller font sizes and only H3 headings:

### Dokku Deployment Guide

### SSH Access
```bash
ssh -i ~/.ssh/id_rsa root@138.197.77.102
```
Connect to server via SSH

### Docker Installation
```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker
```
Install Docker on Ubuntu

### Dokku Installation
```bash
wget -NP . https://dokku.com/install/v0.34.4/bootstrap.sh
sudo DOKKU_TAG=v0.34.4 bash bootstrap.sh
cat ~/.ssh/authorized_keys | dokku ssh-keys:add admin
```
Install Dokku and add SSH key

### Domain Configuration
```bash
dokku domains:set-global retwitter.co
dokku domains:add bookcue-api api.retwitter.co

```
Set global domain and add app-specific domain

### Remove Domain (if needed)
```bash
dokku domains:remove bookcue-api ubuntu-s-1vcpu-1gb-35gb-intel-nyc3-01
```
Remove a domain from the app

### SSL Configuration
```bash
sudo dokku plugin:install https://github.com/dokku/dokku-letsencrypt.git
dokku letsencrypt:set bookcue-api email linvivian61@gmail.com
dokku letsencrypt:enable bookcue-api
```
Install Let's Encrypt plugin and enable SSL
**Create .env.production file** and copy the contents over

```
**Create and build a docker image**
```Dockerfile
# Use an official Node.js runtime as the base image
FROM node:20

# Install pnpm globally
RUN npm install -g pnpm

# Set the working directory
WORKDIR /app

# Copy the entire application
COPY . .

# Copy the environment configuration file
COPY .env.production .env

# Install app-specific dependencies
RUN pnpm install

# Generate Prisma client
RUN npx prisma generate

# Build the application
RUN pnpm run build

# Copy schema.gql to dist/src/config
RUN mkdir -p dist/src/config && cp dist/schema.gql dist/src/config/schema.gql

# Expose the application port
EXPOSE 8080

# Set NODE_ENV to production
ENV NODE_ENV=production

# Use a non-root user for better security
USER node

# Run the application
CMD [ "npm", "run", "start:migrate:prod" ]
```

### Docker Build (for multi-platform)
```bash
docker buildx create --use
docker buildx build --platform linux/amd64 --push -t vivianlin61/bookcue:1 .
```
Build Docker image for AMD64 platform


**Create app, 
```bash
dokku apps:create bookcue-api
```


**endpoint**
```
https://api.retwitter.co/graphql
```



### Deployment Steps
```bash
docker pull vivianlin61/bookcue:3
docker tag vivianlin61/bookcue:3 dokku/bookcue-api:latest
dokku deploy bookcue-api latest
```
Pull, tag, and deploy the latest image

```
curl -X POST http://localhost:8080/graphql \
-H "Content-Type: application/json" \
-d '{"query": "{ healthCheck { status message timestamp } }"}'
```

### Health Check Query
```graphql
query {
  healthCheck {
    status
    message
    timestamp
  }
}
```
GraphQL query for health check

### Known Issues
- .env variables not loading
- Generated types from db:generate
- Schema file (generated when you start the app development) needs to be copied to build
- Check port mappings


[Proxy Management - Dokku Documentation](https://dokku.com/docs/networking/proxy-management/#__tabbed_4_1)
**Check port mappings**
```
 dokku ports:report bookcue-api
```
**Default mapping**
```
=====> bookcue-api ports information
       Ports map:
       Ports map detected:            http:80:5000 https:443:5000
```
http:80:5000
HTTP traffic coming to port 80 on your host (the server where Dokku is running) is being forwarded to port 5000 in your application container.
**When someone accesses your application via HTTP (usually by just typing your domain name in a browser), they're hitting port 80, and Dokku is forwarding that to your application running on port 5000.**

We need to update this to make it point to the port the application is actually running on.

Ports 80 and 443 are the standard ports for HTTP and HTTPS traffic respectively.


**Fix mapping**
```'
root@ubuntu-s-1vcpu-1gb-35gb-intel-nyc3-01:~# 
dokku ports:add bookcue-api http:80:8080
dokku ports:add bookcue-api https:443:8080
```

**redeploy**
```
dokku deploy bookcue-api latest
```
**Next steps**
- use multi build steps, so only the dist file contents is copied over and not the whole app, simplifies the build process


### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```


