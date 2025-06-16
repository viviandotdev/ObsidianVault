---
created: 2024-07-11 18:01
modified: Thursday 11th July 2024 18:01:16

---
up::
type:: [[docker]]
source::
[6 ways to debug an exploding Docker container | by Tim Perry | Medium](https://medium.com/@pimterry/5-ways-to-debug-an-exploding-docker-container-4f729e2c0aa8#id_token=eyJhbGciOiJSUzI1NiIsImtpZCI6IjBlMzQ1ZmQ3ZTRhOTcyNzFkZmZhOTkxZjVhODkzY2QxNmI4ZTA4MjciLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJhenAiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJhdWQiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJzdWIiOiIxMDg2MTc3NTkyMTA1NTQyOTc5OTkiLCJlbWFpbCI6ImxpbnZpdmlhbjYxQGdtYWlsLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJuYmYiOjE3MjA3NDEzMDYsIm5hbWUiOiJWaXZpYW4gTGluIiwicGljdHVyZSI6Imh0dHBzOi8vbGgzLmdvb2dsZXVzZXJjb250ZW50LmNvbS9hL0FDZzhvY0o0VlJ0akZ2N29aR2NhdG00VFBieDZmQnlTZ040MkJGZmZRSUFERXZJeXlzMGxyaTlKPXM5Ni1jIiwiZ2l2ZW5fbmFtZSI6IlZpdmlhbiIsImZhbWlseV9uYW1lIjoiTGluIiwiaWF0IjoxNzIwNzQxNjA2LCJleHAiOjE3MjA3NDUyMDYsImp0aSI6ImYxZjI5YTVmYjY5YmE4MTNmYjQyZTQ2MWY4YjQyNjM2YTk5ZjJiYmYifQ.aajErK9f_K8Tgy5IhUVU6F33pl6RaMBUOXsD_EF7zE0ofcbsAFxGYp3vr1tzhiUVmctXFvotiW6Mwr-IjqNLVdI3M1aoNuZdXJeftCPgnVcjSeFNXyRU9y6LDjs2EigocOXRFNJ_ujbEe-kImg1uiM-fRCdaJi6o6MiAUU1I7gNoNgfQuifBYE-ropqTua0lDeohfTaTEKLAFce7mGMAQuoaZoMY3NpEQnfBOcEKKYXdkDbY84YLUIMq_GgOAeXhjuMAuu51oTDwbeGtFDtbJyV-ow_V8yiCABVNcQIjqLYjq3ebo_SFSlLKV2B1Nt-nzOb-VvZQ-isuIrmW-LJ4XQ)
[How to put a Yarn Workspace in a Docker Image - Part 10 - YouTube](https://www.youtube.com/watch?v=aYF90AKjVfY&list=PLN3n1USn4xlnfJIQBa6bBjjiECnk6zL6s&index=12)
## How to debug docker files?
run bash commands to see the contents of a file
```Dockerfile
# Use an official Node.js runtime as a parent image
FROM node:20 AS builder

RUN npm install -g pnpm
# Set the working directory
WORKDIR /app

# Copy the API app dependencies
COPY package*.json ./
COPY prisma ./prisma/

# Copy the environment configuration file
COPY .env.production .env

# Install app-specific dependencies
RUN pnpm install
RUN npx prisma generate

# Copy the API app source code
COPY . .

# Build the application
RUN pnpm run build

# Debug: List contents of /app directory
RUN echo "Contents of /app:" && ls -la /app

# Debug: Check if .env file exists and display its contents
RUN if [ -f /app/.env ]; then \
    echo ".env file found. Contents:"; \
    cat /app/.env; \
    else \
    echo ".env file not found in /app directory"; \
    fi

FROM node:20

COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/prisma ./prisma
COPY --from=builder /app/.env ./.env

# Debug: List contents of current directory
RUN echo "Contents of current directory:" && ls -la

# Debug: Check if .env file exists and display its contents
RUN if [ -f .env ]; then \
    echo ".env file found. Contents:"; \
    cat .env; \
    else \
    echo ".env file not found in current directory"; \
    fi

# Expose the application port, 8080 is the default port used for many web servers
EXPOSE 8080

# Run the application
CMD [ "npm", "run", "start:migrate:prod" ]

# Use a non-root user for better security
USER node

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
