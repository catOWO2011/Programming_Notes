# Student Management System

[Project Link](https://github.com/catOWO2011/student-management-system)

1. [Generate the project with spring initializr](#1-generate-the-project-with-spring-initializr)
2. [Run the project](#run-the-project)
3. [Create the POJO Student](#create-the-pojo-student)
4. [Create a Student Controller](#create-a-student-controller)
5. [Add WebMvcConfigurer to expose the API](#5-add-webmvcconfigurer-to-expose-the-api)
6. [Working with Application Properties](#6-working-with-application-properties)
7. [Creating a docker container to host our records with postgresql](#7-creating-a-docker-container-to-host-our-records-with-postgresql)

[Reference](#reference)

## 1. Generate the project with spring initializr

Go to this [link](https://start.spring.io/), we'll use some dependencies, it'll look like this, the name of the project is `student-management-system`.
![sprint-initializr](./spring-initializr.png)
After this we generate the project.

Open the project on intellij after unzip the file select the `pom.xml`.

## 2. Run the project

* Remember reload `pom.xml` file every time you update the file, below you have the following options to update.
![pom.xml](./reload-maven.png)

* After run this file.
![Spring Boot Entry Point](./entry-point-run.png)

## 3. Create the POJO Student

Create a student pojo class:
```java
package com.nanocat.studentmanagementsystem.student;

import java.util.UUID;

public class Student {
  private final UUID studentId;
  private final String firstName;
  private final String lastName;
  private final String email;
  private final Gender gender;

  enum Gender {
    MALE, FEMALE
  }

  public Student(UUID studentId, String firstName, String lastName, String email, Gender gender) {
    this.studentId = studentId;
    this.firstName = firstName;
    this.lastName = lastName;
    this.email = email;
    this.gender = gender;
  }

  public UUID getStudentId() {
    return studentId;
  }

  public String getFirstName() {
    return firstName;
  }

  public String getLastName() {
    return lastName;
  }

  public Gender getGender() {
    return gender;
  }

  public String getEmail() {
    return email;
  }
}
```
## 4. Create a Student Controller

```java
package com.nanocat.studentmanagementsystem.student;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;
import java.util.UUID;

@RestController
public class StudentController {
  @GetMapping("/students")
  public List<Student> getAllStudents() {
    return List.of(
            new Student(
                    UUID.randomUUID(),
                    "James",
                    "Bond",
                    "jamesbond@gmai.com",
                    Student.Gender.MALE),
            new Student(
                    UUID.randomUUID(),
                    "Elisa",
                    "Tamara",
                    "elisaTamara@gmail.com",
                    Student.Gender.FEMALE
            )
    );
  }
}
```
## 5. Add WebMvcConfigurer to expose the API
We need to add this `WebMvcConfigurer` Bean to avoid a problem with CORS `No 'Access-Control-Allow-Origin' header is present on the requested resource`. [More..](https://spring.io/guides/gs/rest-service-cors/#global-cors-configuration)

Add the following method in the `StudentManagementSystemApplication` class.
```java
...
@SpringBootApplication
public class StudentManagementSystemApplication {
  ...

  // Code to allow access to the following domain http://localhost:3000/ in this case our frontend side
  @Bean
  public WebMvcConfigurer corsConfigurer() {
    return new WebMvcConfigurer() {
      @Override
      public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/students").allowedOrigins("http://localhost:3000/");
      }
    };
  }
}
```
After this if you open a browser to [localhost:8080/students](http://localhost:8080/students), you should see the following output:
```json
[
  {
    "studentId": "c9b89145-baec-4ebb-86a2-1593ba7a32da",
    "firstName": "James",
    "lastName": "Bond",
    "email": "jamesbond@gmai.com",
    "gender": "MALE"
  },
  {
    "studentId": "8187acb8-853b-4320-bb2b-13f83136ad39",
    "firstName": "Elisa",
    "lastName": "Tamara",
    "email": "elisaTamara@gmail.com",
    "gender": "FEMALE"
  }
]
```

## 6. Working with Application Properties
We want to work with this format `application.yml` instead of `application.properties`, so we delete the last one and add the first one. [More+](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties.core).

We'll add the following property to add a custom path like `api` in `localhost:8080/api/students`:

```yml
server:
  # Add /api as a prefix for every request in the server properties
  servlet:
    context-path: /api
  # Set the default port from 8080 to 5000
  port: 5000
```
Property info [server.servlet.context-path](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.server.server.servlet.context-path).

After this we need to change our url request to [localhost:5000/api/students](http://localhost:5000/api/students).

## 7. Creating a docker container to host our records with postgresql
We can have an instance of a `postgres
 image` [image link](https://hub.docker.com/_/postgres), we need to execute the following command:
```bash
docker run --name student-system-postgres -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres:alpine
```
We can go inside the container by terminal:
```bash
docker exec -it student-system-postgres /bin/bash
```
Get inside postgres:
```bash
psql -U postgres -W
```
If you want to go out from postgres:
```bash
\q
```
List databases:
```bash
\l
```
You can see general options with:
```bash
\?
```
Also if you choose to create a new database you can see options:
```bash
\h CREATE DATABASE
```
So we're going to execute the following command:
```bash
CREATE DATABASE studentsystem;
```
We can connect to this database:
```bash
\c studentsystem;
```
## 8. Connect our app with postgres
Enable the following dependency:
```xml
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jdbc</artifactId>
  </dependency>
```
Run the application, we expect to get this error:
```bash
***************************
APPLICATION FAILED TO START
***************************

Description:

Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured.
```

So we need a `DataSource Configuration` in the `application.yml`, for the `jdbc-url` we have this format `jdbc:postgres://<<urlDatabase:databaseName>>`:
```yml
server:
  # Add /api as a prefix for every request in the server properties
  servlet:
    context-path: /api
  # Set the default port from 8080 to 5000
  port: 5000

app:
  # DataSource Configuration
  datasource:
    jdbc-url: jdbc:postgresql://${URL_DATABASE}
    username: ${STUDENT_SYSTEM_DATABASE_USER}
    password: ${STUDENT_SYSTEM_DATABASE_PASSWORD}
    pool-size: 30
```

We need to set the environment variable so for intellij you need to add them in the following place:
![env-config](/frameworks/java-spring/projects/student-management-system/environment-variables-intellij-1.png)
![env-config-1](/frameworks/java-spring/projects/student-management-system/environment-variables-intellij-2.png)

We create a new package named `datasource` and inside we add this class `Datasource`, we are going to add the `@Configuration` annotation for this class, we use to bind properties from `application.yml` [more](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/properties/ConfigurationProperties.html).

```java
@Configuration
public class Datasource {

  @Bean
  @ConfigurationProperties("app.datasource")
  public HikariDataSource hikariDataSource() {
    return DataSourceBuilder
      .create()
      .type(HikariDataSource.class)
      .build();
  }
}
```
After this we need to create a new migration file for flywaydb on `src -> main-> resources -> db.migration` directory, we are going to add the `V1__CreateStudentTable.sql` file and add inside the following code:
```sql
CREATE TABLE IF NOT EXISTS student (
    student_id UUID PRIMARY KEY NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    gender VARCHAR(6) NOT NULL
        CHECK (
            gender = 'MALE' OR
            gender = 'male' OR
            gender = 'FEMALE' OR
            gender = 'female'
        )
);
```
After running the application we can see this new student table:
```bash
postgres=# \c studentsystem 
Password: 
You are now connected to database "studentsystem" as user "postgres".
studentsystem=# \x
Expanded display is on.
studentsystem=# \d
                 List of relations
 Schema |         Name          | Type  |  Owner   
--------+-----------------------+-------+----------
 public | flyway_schema_history | table | postgres
 public | student               | table | postgres
(2 rows)

studentsystem=#
```



## Reference
* [Flyway API (Java)](https://documentation.red-gate.com/fd/api-java-184127629.html)
* [Tutorial - Baseline Migrations](https://documentation.red-gate.com/fd/tutorial-baseline-migrations-184127615.html)