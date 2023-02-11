# Sprint Helpful Topics

### Content:
* [Spring Properties](#spring-properties)


## Spring Properties

 Use this [reference](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties.server) to setup the  `aplication.properties` or `application.yml` file at your project.

 To edit this properties use [also](https://docs.spring.io/spring-boot/docs/1.2.0.M1/reference/html/howto-properties-and-configuration.html) and [this](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.spring-application).

## Projects To Learn

### Student System


#### Docker Container
Create a docker container with postgres user:
```
docker run --name demo-postgres -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres:alpine
```
Run the container
```
docker start demo-postgres
```
Get into the container
```
docker exec -it demo-postgres /bin/bash
```
Log in postgres
```
psql -U postgres -W
```
List databases
```
\l
```
Connect a database
```
\c amigoscodedemo
```
List of Tables
```
\d
```
Describe a table
```
\d student
```
Enable show display expanded table
```
\x
```
Show all record on `student` table
```
SELECT * FROM student;
```

#### Links
* [Data Access - Configure a Custom DataSource](https://docs.spring.io/spring-boot/docs/3.0.2/reference/htmlsingle/#howto.data-access.configure-custom-datasource)
* [Configuration Properties](https://docs.spring.io/spring-boot/docs/3.0.2/api/org/springframework/boot/context/properties/ConfigurationProperties.html)
* [PostgreSQL Commands](https://www.postgresql.org/docs/15/app-psql.html)
