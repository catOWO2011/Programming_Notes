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
Stop container
```
docker stop demo-postgres
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
#### Building queries
```java
private final RowMapper<Actor> actorRowMapper = (resultSet, rowNum) -> {
    Actor actor = new Actor();
    actor.setFirstName(resultSet.getString("first_name"));
    actor.setLastName(resultSet.getString("last_name"));
    return actor;
};

public List<Actor> findAllActors() {
    return this.jdbcTemplate.query("select first_name, last_name from t_actor", actorRowMapper);
}
```

#### Add Record to the student table with mockaroo
```sql
insert into student (id, first_name, last_name, email, gender) values (1, 'Margot', 'Piatto', 'mpiatto0@addthis.com', 'AGENDER');
insert into student (id, first_name, last_name, email, gender) values (2, 'Rourke', 'Willshire', 'rwillshire1@google.cn', 'MALE');
insert into student (id, first_name, last_name, email, gender) values (3, 'Stanfield', 'Sutherel', 'ssutherel2@last.fm', 'MALE');
insert into student (id, first_name, last_name, email, gender) values (4, 'Tynan', 'Leaburn', 'tleaburn3@bloglines.com', 'MALE');
insert into student (id, first_name, last_name, email, gender) values (5, 'Avictor', 'Martin', 'amartin4@discuz.net', 'MALE');
insert into student (id, first_name, last_name, email, gender) values (6, 'Elvera', 'Deamer', 'edeamer5@microsoft.com', 'FEMALE');
insert into student (id, first_name, last_name, email, gender) values (7, 'Joannes', 'Bowart', 'jbowart6@google.ca', 'FEMALE');
insert into student (id, first_name, last_name, email, gender) values (8, 'Gwen', 'Kharchinski', 'gkharchinski7@icio.us', 'FEMALE');
insert into student (id, first_name, last_name, email, gender) values (9, 'Bertie', 'Jizhaki', 'bjizhaki8@slashdot.org', 'MALE');
insert into student (id, first_name, last_name, email, gender) values (10, 'Sherry', 'Munton', 'smunton9@answers.com', 'FEMALE');
```

#### Add a student
To create the new student with the api we need to add this method to the controller along with the `@PostMapping` annotation.
Use `@RequestBody` to tell spring convert the json information into a student object through a matching process with the attributes.
```java
@PostMapping
public void addNewStudent(@RequestBody Student student) {
    System.out.println(student);
}
```

#### Links
* [Data Access - Configure a Custom DataSource](https://docs.spring.io/spring-boot/docs/3.0.2/reference/htmlsingle/#howto.data-access.configure-custom-datasource)
* [Configuration Properties](https://docs.spring.io/spring-boot/docs/3.0.2/api/org/springframework/boot/context/properties/ConfigurationProperties.html)
* [PostgreSQL Commands](https://www.postgresql.org/docs/15/app-psql.html)
* [Data Acces with JDBC](https://docs.spring.io/spring-framework/docs/current/reference/html/data-access.html#jdbc-JdbcTemplate-examples-query)
* [Mockup your data with postgres](https://www.mockaroo.com/)