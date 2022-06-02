### JPA
It's a popular Spring Data project.
JPA is available to Spring Boot applications with the JPA starter

#### Define an JPA entity
We have an example who to use tags to define JPA entities and mapping these.

We define a relationship between three POJOs Book, Author and Publisher, after we added the following tags.
```java
@Entity // This define de POJO as a JPA entity
public class Author {}

@Entity
public class Book {}

@Entity
public class Publisher {}
```
After add the tag above you need to define the Id identify each entity and specify how this value is generated and add the attribute that it will be the Id. We need to add a way to make this object unique that means add some methods like equals, for example for the Author POJO
```java
@Entity
public class Author {
  ...
  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Long Id;
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

We added the following tags for the POJOS
```java
@Entity
public class Author {

  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Long id;

  ...

  // this side is mapping the other side is going to declare the mid table this mappedBy means
  // map the attribute for the other side in this case Book that has private Set<Author> authors(this last one)
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

  // Definde the relationship
  @ManyToMany
  // Create this is going to hold the relationship between records on the author table
  // and records on the book table
  @JoinTable(name = "author_book", joinColumns = @JoinColumn(name = "book_id"),
    inverseJoinColumns = @JoinColumn(name = "author_id"))
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