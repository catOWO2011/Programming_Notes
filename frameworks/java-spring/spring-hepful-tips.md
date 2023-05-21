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
##### Bug
If you have problems with CORS `No 'Access-Control-Allow-Origin' header is present on the requested resource`, you can solve it by adding the following configuration on the Application class:
```java
...
@SpringBootApplication
public class DemoApplication {

  public static void main(String[] args) {
    SpringApplication.run(DemoApplication.class, args);
  }

    // CORS Configuration
  @Bean
  public WebMvcConfigurer corsConfigurer() {
    return new WebMvcConfigurer() {
        @Override
        public void addCorsMappings(CorsRegistry registry) {
            registry.addMapping("/students").allowedOrigins("http://localhost:3000");
        }
    };
  }
}
```
Remember in the `registry.addMapping("/students")` you need to add the path of the `@RequestMapping("students")` or `@GetMapping("students")` whichever is the route in this case is `student`.
#### Include custom messages when the server throws an error

When we throw an exception from a controller like this: `throw new IllegalStateException("Oops cannot get all students");` if we want to get the message `Oops cannot get all students` for spring boot `3.0` we need to do the following configuration in the `yml` file
```yml
server:
  servlet:
    context-path: /api
  # The configuration to include in the response the custom message is below
  error:
    include-message: always #By default this is set as false
    include-binding-errors: always # By default this is set as never
```
#### Custom Exceptions
If you want to throw a custom exception you can add these three classes:
```java
public class ApiRequestException extends RuntimeException {
  public ApiRequestException(String message) {
    super(message);
  }

  public ApiRequestException(String message, Throwable cause) {
    super(message, cause);
  }
}
```
```java
@ControllerAdvice
public class ApiExceptionHandler {

  @ExceptionHandler(ApiRequestException.class)
  public ResponseEntity<Object> handleApiRequestException(ApiRequestException e) {

    HttpStatus badRequest = HttpStatus.BAD_REQUEST;

    ApiException apiException = new ApiException(
            e.getMessage(),
            badRequest,
            ZonedDateTime.now(ZoneId.of("Z"))
    );

    return new ResponseEntity<>(e, badRequest);
  }
}
```
```java
public class ApiException {
  private final String message;
  private final HttpStatus httpStatus;
  private final ZonedDateTime timestamp;

  public ApiException(String message, HttpStatus httpStatus, ZonedDateTime timestamp) {
    this.message = message;
    this.httpStatus = httpStatus;
    this.timestamp = timestamp;
  }

  public String getMessage() {
    return message;
  }

  public HttpStatus getHttpStatus() {
    return httpStatus;
  }

  public ZonedDateTime getTimestamp() {
    return timestamp;
  }
}
```
We need to be awere to these two new annotations `@ControllerAdvice` and `@ExceptionHandler`, you can check the documentation as well on the links below.
#### Validation on fields
If we want to validate if we have all the fields and they aren't empty we can add the following annotations `@NotBlank`, ``
Before you start to using this annotations, you need to add the following dependency in the `pom.xml` file and reload the project:
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```
And below the example:
```java
...
public class Student {
  private final UUID studentId;
  @NotBlank
  private final String firstName;
  @NotBlank
  private final String lastName;
  @NotBlank
  private final String email;
  @NotNull
  private final Gender gender;
  ...
}
```
```java
...
public class StudentController {
  ...
  @PostMapping
  public void addNewStudent(@RequestBody @Validated Student student) {
    studentService.addNewStudent(student);
  }
}
```
#### Links
* [Data Access - Configure a Custom DataSource](https://docs.spring.io/spring-boot/docs/3.0.2/reference/htmlsingle/#howto.data-access.configure-custom-datasource)
* [Configuration Properties](https://docs.spring.io/spring-boot/docs/3.0.2/api/org/springframework/boot/context/properties/ConfigurationProperties.html)
* [PostgreSQL Commands](https://www.postgresql.org/docs/15/app-psql.html)
* [Data Acces with JDBC](https://docs.spring.io/spring-framework/docs/current/reference/html/data-access.html#jdbc-JdbcTemplate-examples-query)
* [Mockup your data with postgres](https://www.mockaroo.com/)
* [CORS global configuration](https://spring.io/guides/gs/rest-service-cors/#global-cors-configuration)
* [Include message attribute for errors, allowing the client side having more information](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.server.server.error.include-message)
* [Custom Error Handling](https://docs.spring.io/spring-boot/docs/3.0.2/reference/htmlsingle/#web.servlet.spring-mvc.error-handling)
* [Validation in Spring Boot - validate fields on server side](https://www.baeldung.com/spring-boot-bean-validation)