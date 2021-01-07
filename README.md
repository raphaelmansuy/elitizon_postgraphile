# Run Postgres using "docker-compose"

## This document explains how to run a Postgres SQL Database with Docker

### Create a local directory called "postgres"

```shell
$ mkdir postgres
$ cd ./postgres
```

### Create a "pgdata" directory inside "postgres" directory

```shell
$ cd ./postgres
$ mkdir ./pgdata
```

As a docker container is "stateless" we must create the directory "pgdata" to keep the data when the container is shut down.

### Create a file called "docker-compose.yml" in "postgres" directory

```shell
$ touch ./docker-compose.yml
```

#### docker-compose.yml file

```yml
version: "3.8"
services:
  db:
    image: "postgres:13"
    ports:
      - "5432:5432"
    volumes:
      - ./pgdata:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=dbuser
      - POSTGRES_PASSWORD=admin2021
      - POSTGRES_DB=todoapp
```

- This file create a host called "db" from a Postgres version 13 image. The TCP port 5432 (postgres) of the host "db" is exposed externally as the TCP port 5432.

- The local directory "./pgdata" is mapped as the "/var/lib/postgressql/data" inside the "db" host

- The user, password and database name are exposed as an environment variable



## Run the container in detached mode

```shell
$ docker-compose up -d
```

## List docker

```shell
$ docker-compose ps
```

## Run command inside the container

```shell
$ docker-compose run db bash
```

## Connect postgres inside the host

```shell
$ psql  --host=db --username=dbuser --dbname=todoapp
```

### Connect to "postgres" from outside

```shell
$ psql --host=localhost --username=dbuser --dbname=todoapp
```

### stop container

```shell
$ docker-compose down
```
