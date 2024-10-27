# PostgreSQL

## Table of Contents
  * 
  * [Basic Statements](#basic-statements)

## Using PostgreSQL with docker
You can download a docker image [from](https://hub.docker.com/_/postgres/). Once you do it you can start to running the container.
```bash
docker run -e POSTGRES_PASSWORD=lol --name=pg -d 5300:5432 postgres
```
To get into the container you can run:
```bash
docker exec -u postgres -it pg psql
```
## Commands
**Show list of databases**
```bash
\l
```
**Show all the tables**
```bash
\d
```
**Create a database**
```bash
CREATE DATABASE recipeguru;
```

Basic commands are:
  * **Data Definition Language (DDL)**
  * **Data Manipulation Language (DML)**


