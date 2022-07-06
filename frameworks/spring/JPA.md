# JPA
JPA (Java Persistent API)
It's a popular **Spring Data** project.
JPA is available to Spring Boot applications with the JPA starter

## Define an JPA entity
We have an example who to use tags to define JPA entities and mapping these.

We define a relationship between three POJOs Book, Author and Publisher, after we added the following constraints:

* The Author, Book and Publisher classes are annotated with **@Entity** indicating that it is a JPA entity.
```java
@Entity // This define de POJO as a JPA entity
public class Author {
  ...
}
```

* JPA does require a zero args constructor(The default constructor exists only for the sake of JPA, You do not use it directly, so it is designated as protected).

* The object's *Id* property is annotated with **@Id** so that JPA recognizes it as the object's ID, also the *Id* property is annotated with @GenerateValue to indicate the *Id* should be generated automatically, this tells hibernate how it is getting generated.

```java
@Entity
public class Author {
  ...
  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Long Id;
  ...
  public Author() {
    //We need a zero args constructor
  }
  ...
  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;

    Author author = (Author) o;

    return id != null ? id.equals(author.id) : author.id == null;
  }

  @Override
  public int hashCode() {
    return id != null ? id.hashCode() : 0;
  }
}
```
For the mapping we have the following:
* Author has many Book(s)
* Book has many Author(s)
* Publisher has many Book(s)
* Book has one Publisher

For Author Books relationship the owning side is going to be Author and the non-owning side is Author. So the **join table is specified on the owning side**(Book) and the **mappedBy** element must be use on the non-owning(Author).

We added the following tags for the POJOS
```java
@Entity
public class Author {

  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Long id;

  ...

  // mappedBy used on the non-owning side
  @ManyToMany(mappedBy = "authors")
  private Set<Book> books = new HashSet<>();

  ...
}
```
```java
@Entity
public class Book {
  @Id
  @GeneratedValue(strategy =  GenerationType.AUTO)
  private Long Id;

  // These books to one publisher
  // 
  @ManyToOne
  private Publisher publisher;

  // Definde the relationship on the owning side
  @ManyToMany
  // Create this is going to hold the relationship between records on the author table
  // and records on the book table
  @JoinTable(
    name = "author_book",
    joinColumns = @JoinColumn(name = "book_id"),
    inverseJoinColumns = @JoinColumn(name = "author_id")
  )
  private Set<Author> authors = new HashSet<>();
  ...
}
```
```java
@Entity
public class Publisher {
  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Long id;

  @OneToMany
  @JoinColumn(name = "publisher_id")
  private Set<Book> books = new HashSet<>();
  ...
}
```

## More information
* [Spring Data projects](https://spring.io/projects/spring-data)
* [Accessing Data with JPA](https://spring.io/guides/gs/accessing-data-jpa/)
* [Hibernate User Guide Annotations](https://docs.jboss.org/hibernate/orm/6.1/userguide/html_single/Hibernate_User_Guide.html#annotations)
* [Annotation Type ManyToMany](https://javaee.github.io/javaee-spec/javadocs/javax/persistence/ManyToMany.html)