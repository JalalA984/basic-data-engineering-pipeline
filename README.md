# Basic End-to-end Data Engineering Pipeline

This repo documents my learning process for data pipeline construction with Airflow.


### Structure 

We set up a multi-container application with 3 services:
- source_postgres:
    Purpose: Runs a PostgreSQL database container, which acts as the source database in the ELT pipeline

    `docker-entrypoint-initdb.d` is a special directory used by the PostgreSQL Docker image to automatically execute sql file

- destination_postgres:

    Purpose: Runs a PostgreSQL database container, which acts as the destination database for transformed data.

- elt_script:

    Purpose: Runs the custom script that implements the ELT pipeline logic. It reads data from `source_postgres`, performs transformations, and writes the results to `destination_postgres`

A shared docker network `elt_network` acts as a bridge between all 3 services

```lua
LOCAL
+--------------------+
| Host Machine       |
|                    |
|   +---------------------------+
|   | elt_network (bridge)      |
|   |                           |
|   | +-----------------------+ |
|   | | source_postgres       |<--------------------> Communicates using hostname
|   | +-----------------------+ |
|   | +-----------------------+ |
|   | | destination_postgres  |<--------------------> Communicates using hostname
|   | +-----------------------+ |
|   | +-----------------------+ |
|   | | elt_script            |<--------------------> Communicates using hostname
|   | +-----------------------+ |
|   +---------------------------+
+--------------------+
```

