# Notes for SQL with Docker

### Local Postgres
Get image 
pull - self explanatory

```bash
docker pull postgres
```
Run container with the image
--name tag: specifies container name 
-e: sets environment variables
-d: runs container in the background rather than in your terminal

```bash
docker run --name data-engineering-postgres -e POSTGRES_PASSWORD=secret -d postgres
```

We want to create new DB inside container
exec: Runs the following command inside a running container 
-u: specifies user in our case postgres
createdb: is specific to postgres not docker and creates new DB

```bash
docker exec -u postgres data-engineering-postgres createdb postgres-db
```

**Important:**
Connect to postgres shell

-it: -i keeps container stdin open so we can use shell and -t enables the terminal 
psql: postgres command line client

-u is same as -U?
-d: specifies the database

```bash
docker exec -it data-engineering-postgres psql -U postgres -d postgres-db
```

