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


## Types
**Reference**
* [Chapter 8. Data Types](https://www.postgresql.org/docs/current/datatype.html)

## Practice
* [SQLPad](https://sqlpad.io/)
* [Mode](https://mode.com/sql-tutorial/sql-in-mode)
* [sqlbolt](https://sqlbolt.com/lesson/introduction)
* [sqlzoo](https://www.sqlzoo.net/wiki/SQL_Tutorial)
* [datalemur](https://datalemur.com/)
* [SQLCourse](https://www.sqlcourse.com/)
* [sql-practice](https://www.sql-practice.com/)
* [stratascratch](https://platform.stratascratch.com/coding?code_type=1)
* [Introduction to SQL](https://livesql.oracle.com/ords/livesql/file/tutorial_D39T3OXOCOQ3WK9EWZ5JTJA.html)
