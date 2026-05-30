# Spring Data JPA Complete Notes

---

# 1. What is Spring Data JPA?

Spring Data JPA is a module of Spring Framework that simplifies database operations using JPA.

Instead of writing JDBC code manually, Spring Data JPA automatically generates queries and database operations.

It sits on top of:

Spring Boot
    ↓
Spring Data JPA
    ↓
JPA Specification
    ↓
Hibernate (Implementation)
    ↓
Database (MySQL, PostgreSQL, Oracle etc.)

---

# 2. What is JPA?

JPA (Java Persistence API) is a specification.

It defines rules for:

- Saving data
- Updating data
- Deleting data
- Fetching data

JPA itself contains only interfaces.

Example:

```java
public interface EntityManager {
    void persist(Object entity);
}
```

JPA does not contain implementation.

---

# 3. What is Hibernate?

Hibernate is the most popular implementation of JPA.

JPA = Rules

Hibernate = Actual Implementation

Example:

```java
EntityManager.persist(user);
```

Internally Hibernate converts it to:

```sql
insert into users values(...)
```

---

# 4. Why Spring Data JPA?

Without Spring Data JPA:

```java
Connection con = DriverManager.getConnection(...);

PreparedStatement ps =
con.prepareStatement("insert into users values(?)");
```

Too much boilerplate code.

With Spring Data JPA:

```java
userRepository.save(user);
```

Done.

Advantages:

- Less code
- Faster development
- Auto Query Generation
- Pagination
- Sorting
- Transactions
- Custom Queries

---

# 5. Required Dependencies

Maven:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
</dependency>
```

For MySQL:

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
</dependency>
```

---

# 6. application.properties

PostgreSQL

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/ecom

spring.datasource.username=postgres
spring.datasource.password=password

spring.jpa.hibernate.ddl-auto=update

spring.jpa.show-sql=true

spring.jpa.properties.hibernate.format_sql=true
```

---

# 7. What is Entity?

Entity = Java Class mapped to database table.

```java
@Entity
public class User {

}
```

Table created automatically.

```sql
user
```

---

# 8. @Entity Annotation

Marks class as database table.

```java
@Entity
public class Student {

}
```

---

# 9. @Table Annotation

Used to customize table name.

```java
@Entity
@Table(name="students")
public class Student {

}
```

Generated table:

```sql
students
```

---

# 10. Primary Key

Every table requires a primary key.

```java
@Id
private Long id;
```

---

# 11. @GeneratedValue

Auto generates primary key.

```java
@Id
@GeneratedValue
private Long id;
```

---

# 12. Generation Strategies

## AUTO

```java
@GeneratedValue(strategy=GenerationType.AUTO)
```

Hibernate decides.

---

## IDENTITY

```java
@GeneratedValue(strategy=GenerationType.IDENTITY)
```

Database generates value.

Example:

```sql
serial
auto_increment
```

---

## SEQUENCE

```java
@GeneratedValue(strategy=GenerationType.SEQUENCE)
```

Uses database sequence.

---

## TABLE

```java
@GeneratedValue(strategy=GenerationType.TABLE)
```

Uses separate table for ids.

Rarely used.

---

# 13. Complete Entity Example

```java
@Entity
@Table(name="users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    private String email;

    private int age;
}
```

---

# 14. Lombok with JPA

```java
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;
}
```

---

# 15. Repository Layer

Repository communicates with database.

```java
public interface UserRepository
extends JpaRepository<User, Long> {

}
```

---

# 16. JpaRepository

```java
JpaRepository<Entity, PrimaryKeyType>
```

Example:

```java
JpaRepository<User, Long>
```

---

# 17. Built-In Methods

---

## save()

Insert or Update

```java
repository.save(user);
```

---

## findById()

```java
repository.findById(1L);
```

Returns:

```java
Optional<User>
```

---

## findAll()

```java
repository.findAll();
```

Returns:

```java
List<User>
```

---

## deleteById()

```java
repository.deleteById(1L);
```

---

## delete()

```java
repository.delete(user);
```

---

## count()

```java
repository.count();
```

---

## existsById()

```java
repository.existsById(1L);
```

Returns:

```java
true
false
```

---

# 18. Service Layer Example

```java
@Service
public class UserService {

    @Autowired
    UserRepository repository;

    public User save(User user){
        return repository.save(user);
    }

    public List<User> getAll(){
        return repository.findAll();
    }
}
```

---

# 19. Controller Example

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @Autowired
    UserService service;

    @PostMapping
    public User save(@RequestBody User user){
        return service.save(user);
    }

    @GetMapping
    public List<User> getAll(){
        return service.getAll();
    }
}
```

---

# 20. Derived Query Methods

Spring creates query automatically from method name.

---

## Find By Name

```java
List<User> findByName(String name);
```

Generated SQL:

```sql
select * from users where name=?
```

---

## Find By Email

```java
User findByEmail(String email);
```

---

## Find By Age

```java
List<User> findByAge(int age);
```

---

## Find By Name And Email

```java
List<User> findByNameAndEmail(
String name,
String email
);
```

---

## Find By Name Or Email

```java
List<User> findByNameOrEmail(
String name,
String email
);
```

---

# 21. Comparison Queries

## Greater Than

```java
findByAgeGreaterThan(int age)
```

SQL:

```sql
where age > ?
```

---

## Less Than

```java
findByAgeLessThan(int age)
```

---

## Between

```java
findByAgeBetween(int start,int end)
```

---

# 22. Like Queries

## Contains

```java
findByNameContaining(String name)
```

SQL:

```sql
like %value%
```

---

## Starts With

```java
findByNameStartingWith(String name)
```

---

## Ends With

```java
findByNameEndingWith(String name)
```

---

# 23. Order By

```java
findByAgeOrderByNameAsc(int age)
```

---

```java
findByAgeOrderByNameDesc(int age)
```

---

# 24. Custom Queries using @Query

```java
@Query("select u from User u")
List<User> getAllUsers();
```

JPQL Query.

---

# 25. JPQL

JPQL uses Entity names.

Not table names.

Example:

```java
@Query("select u from User u")
```

Here:

User = Entity Class

NOT Database Table

---

# 26. Parameterized Query

```java
@Query("select u from User u where u.email=:email")
User getByEmail(
    @Param("email") String email
);
```

---

# 27. Multiple Parameters

```java
@Query("""
select u
from User u
where u.name=:name
and u.age=:age
""")
List<User> getUser(
 @Param("name") String name,
 @Param("age") int age
);
```

---

# 28. Native Query

Actual SQL query.

```java
@Query(
value="select * from users",
nativeQuery=true
)
List<User> getUsers();
```

---

# 29. Why Native Query?

When JPQL cannot do something easily.

Example:

- Database specific functions
- Complex joins
- Stored procedures

---

# 30. createNativeQuery()

Used with EntityManager.

```java
@Autowired
EntityManager em;
```

Example:

```java
Query query=
em.createNativeQuery(
"select * from users",
User.class
);

List<User> users=
query.getResultList();
```

This is commonly used in many companies.

---

# 31. EntityManager

Main JPA interface.

Used internally by repositories.

Can also be used manually.

```java
@Autowired
EntityManager em;
```

Methods:

```java
persist()
merge()
remove()
find()
createQuery()
createNativeQuery()
```

---

# 32. persist()

Insert

```java
em.persist(user);
```

Equivalent:

```java
repository.save(user);
```

---

# 33. merge()

Update

```java
em.merge(user);
```

---

# 34. remove()

Delete

```java
em.remove(user);
```

---

# 35. find()

Get By Id

```java
User user=
em.find(User.class,1L);
```

---

# 36. Pagination

Useful when millions of records exist.

---

## Pageable

```java
Pageable pageable=
PageRequest.of(0,5);
```

---

## Repository

```java
Page<User> findAll(Pageable pageable);
```

---

## Service

```java
repository.findAll(pageable);
```

---

# 37. Sorting

```java
Sort sort=
Sort.by("name");
```

---

Ascending:

```java
Sort.by("name").ascending();
```

---

Descending:

```java
Sort.by("name").descending();
```

---

Example:

```java
repository.findAll(
Sort.by("name").ascending()
);
```

---

# 38. Pagination + Sorting

```java
PageRequest.of(
0,
10,
Sort.by("name")
);
```

---

# 39. Transactions

Used to maintain data consistency.

```java
@Transactional
public void saveUser(){
}
```

---

Example:

```java
@Transactional
public void transferMoney(){

    deduct();

    add();
}
```

If one fails:

Everything rollback.

---

# 40. Fetch Types

---

## EAGER

Loads immediately.

```java
FetchType.EAGER
```

---

## LAZY

Loads when needed.

```java
FetchType.LAZY
```

Preferred.

---

# 41. Relationships

Most Important Interview Topic.

---

# One To One

Example:

User → Aadhaar

```java
@OneToOne
private Aadhaar aadhaar;
```

---

# One To Many

Example:

Department → Employees

```java
@OneToMany
private List<Employee> employees;
```

---

# Many To One

Example:

Many Employees belong to one Department

```java
@ManyToOne
private Department department;
```

---

# Many To Many

Example:

Students ↔ Courses

```java
@ManyToMany
private List<Course> courses;
```

---

# 42. Cascade Types

Automatically performs operation on child entity.

```java
cascade = CascadeType.ALL
```

Types:

```java
PERSIST
MERGE
REMOVE
REFRESH
DETACH
ALL
```

---

# 43. Auditing

Automatically stores:

- Created Date
- Updated Date

```java
@CreatedDate

@LastModifiedDate
```

Enable:

```java
@EnableJpaAuditing
```

---

# 44. Hibernate DDL Auto

## create

```properties
spring.jpa.hibernate.ddl-auto=create
```

Drops and recreates table.

---

## update

```properties
spring.jpa.hibernate.ddl-auto=update
```

Most used during development.

---

## validate

```properties
spring.jpa.hibernate.ddl-auto=validate
```

Only validates schema.

---

## create-drop

```properties
spring.jpa.hibernate.ddl-auto=create-drop
```

Drops table on shutdown.

---

# 45. Important Interview Questions

1. Difference between JPA and Hibernate?
2. Why Spring Data JPA?
3. What is EntityManager?
4. Difference between save() and persist()?
5. JPQL vs Native Query?
6. Why use createNativeQuery()?
7. What is Lazy Loading?
8. What is Eager Loading?
9. Cascade Types?
10. Pagination vs Sorting?
11. findById() returns Optional why?
12. Difference between CrudRepository, PagingAndSortingRepository, JpaRepository?
13. @Transactional use?
14. OneToMany vs ManyToOne?
15. GenerationType strategies?
16. What happens internally when save() is called?

---

# Quick Revision

Entity -> Table

@Id -> Primary Key

@GeneratedValue -> Auto Id

Repository -> Database Layer

JpaRepository -> Ready-made CRUD

@Query -> Custom Query

JPQL -> Uses Entity Names

Native Query -> Uses SQL

EntityManager -> Core JPA API

Pageable -> Pagination

Sort -> Sorting

@Transactional -> Transaction Management

@OneToOne -> One ↔ One

@OneToMany -> One ↔ Many

@ManyToOne -> Many ↔ One

@ManyToMany -> Many ↔ Many

Hibernate -> JPA Implementation
