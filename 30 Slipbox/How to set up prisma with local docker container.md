---
created: 2024-07-01 06:36 
modified: Monday 1st July 2024 06:36:28
alias: 
---
up::  
type:: #note/atomic🌳 
links:: [How to set up Prisma with a local Docker Postgres container | by Alessandro Baccini | Nerd For Tech | Medium](https://medium.com/nerd-for-tech/how-to-set-up-prisma-with-a-local-docker-postgres-container-9e0958d08544#id_token=eyJhbGciOiJSUzI1NiIsImtpZCI6IjBlNzJkYTFkZjUwMWNhNmY3NTZiZjEwM2ZkN2M3MjAyOTQ3NzI1MDYiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJhenAiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJhdWQiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJzdWIiOiIxMDg2MTc3NTkyMTA1NTQyOTc5OTkiLCJlbWFpbCI6ImxpbnZpdmlhbjYxQGdtYWlsLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJuYmYiOjE3MDExMTQ4OTUsIm5hbWUiOiJWaXZpYW4gTGluIiwicGljdHVyZSI6Imh0dHBzOi8vbGgzLmdvb2dsZXVzZXJjb250ZW50LmNvbS9hL0FDZzhvY0pjWnBMQXd4Y2lUUTRpazhZNEVZMkRmVXNjUzNrbFl4NnZLeWRsLW55NXpyMD1zOTYtYyIsImdpdmVuX25hbWUiOiJWaXZpYW4iLCJmYW1pbHlfbmFtZSI6IkxpbiIsImxvY2FsZSI6ImVuIiwiaWF0IjoxNzAxMTE1MTk1LCJleHAiOjE3MDExMTg3OTUsImp0aSI6ImNhNDMzYzVkNmRjN2NlNDAzZTM0MzA2NDNlY2ZkNjU5M2JkYzk0NzEifQ.kctBDuC8ae3d0Qze7-d-8oCZZIMWBpnLVdnO4DrszhrlEtEy7wIRSo3ce6MNQKhmWoEAw4VR0XDIIqLpj6mC5CJXufQeoX-Lcd-WAev6LnqXRW5-nRXRNWUaOlR9NwhgTCAyVRwRSFLYQB6cxpDIYcuxMcYSR_7csAh_BeiRQuO6Ja3nqV8vPy8oXdmrcAz7UtPW7jjd2ix_XCTn4J2IB5Q55zSFPb8HnIwsGlhxu8BkqO0_DJklom4S92L57pmVklY3qggrKrbDbVTwUXnCe1_2gqk5huPIIDpaYs6mcfXjuPPuQLNbTYvIjnXsYQO9_nCoBn3WDa-Tr6dGZxY8nw)
## How to set up prisma with local docker container



**Create a container called postgres-db from the postgres image**
Ensure the ports are correctly mapped, you should see an output similar to 0.0.0.0:6500->5432/tcp or localhost:6500->5432/tcp in the PORTS column. This indicates that port 5432 on the container is mapped to port 6500 on the host.

**download postgres container and then run the container**
```
docker run -e POSTGRES_DB=bookcue -e POSTGRES_PASSWORD=test -e POSTGRES_USER=postgres -p 6500:5432 -d postgres
```

**connect to the container**
```
DATABASE_URL="postgresql://postgres:test@localhost:6500/bookcue?schema=public"
```

Access the container named **postgres-db** as root user
```
docker exec -it keen_antonelli bash
```

Switch to postgres user
```
su - postgres
```
Create database called bookcue
```
createdb bookcue
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



