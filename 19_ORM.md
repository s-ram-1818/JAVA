
# ORM in Java (Object Relational Mapping)

# 1. What is ORM?

ORM (Object Relational Mapping) is a technique used to map Java objects (classes) with database tables.

It allows developers to interact with the database using Java objects instead of writing raw SQL queries everywhere.

## Simple Meaning

| Java World | Database World |
|------------|----------------|
| Class      | Table          |
| Object     | Row            |
| Field      | Column         |

Example:

```java
class Student {
    int id;
    String name;
}
````

Mapped to:

| id | name |
| -- | ---- |
| 1  | Ram  |

---

# 2. Why ORM is Needed?

Without ORM:

* Need to write SQL manually
* Need to convert ResultSet → Objects manually
* More boilerplate code
* Database dependent

With ORM:

* Less SQL
* Faster development
* Object-oriented approach
* Cleaner code
* Easier maintenance

---

# 3. Popular ORM Frameworks in Java

| Framework       | Description                |
| --------------- | -------------------------- |
| Hibernate       | Most popular ORM framework |
| JPA             | Specification/API for ORM  |
| Spring Data JPA | Simplifies JPA operations  |
| EclipseLink     | JPA implementation         |
| MyBatis         | SQL Mapper framework       |

---

# 4. Difference Between JDBC and ORM

| JDBC              | ORM                |
| ----------------- | ------------------ |
| Manual SQL        | Automatic mapping  |
| More code         | Less code          |
| Manual conversion | Object mapping     |
| Low-level         | High-level         |
| Hard maintenance  | Easier maintenance |

---

# 5. ORM Architecture

```text
Java Application
       ↓
 ORM Framework (Hibernate/JPA)
       ↓
 JDBC
       ↓
 Database
```

---

# 6. What is JPA?

JPA = Java Persistence API

It is NOT a framework.

It is a specification that defines rules for ORM.

Hibernate is an implementation of JPA.

## Example

```text
JPA → Rules/Specification
Hibernate → Implementation
```

---

# 7. What is Hibernate?

Hibernate is an ORM framework used to:

* Map Java classes to database tables
* Perform CRUD operations
* Reduce SQL code
* Handle relationships

---

# 8. ORM Terminologies

| Term          | Meaning                    |
| ------------- | -------------------------- |
| Entity        | Java class mapped to table |
| Persistence   | Storing objects in DB      |
| EntityManager | Performs DB operations     |
| Session       | Hibernate DB session       |
| Primary Key   | Unique identifier          |
| Mapping       | Class ↔ Table relation     |

---

# 9. Entity Class

Entity class represents a database table.

## Rules

* Must have default constructor
* Must have primary key
* Uses `@Entity`
* Uses `@Id`

---

# 10. Important ORM Annotations

## @Entity

Marks class as database entity.

```java
@Entity
public class Student {

}
```

---

## @Table

Specifies table name.

```java
@Table(name="students")
```

---

## @Id

Defines primary key.

```java
@Id
private int id;
```

---

## @GeneratedValue

Auto generates ID.

```java
@GeneratedValue(strategy = GenerationType.IDENTITY)
```

---

## @Column

Maps field to column.

```java
@Column(name="student_name")
private String name;
```

---

## Complete Example

```java
import jakarta.persistence.*;

@Entity
@Table(name = "students")
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    @Column(name = "student_name")
    private String name;

    private int age;

    public Student() {

    }

    // getters setters
}
```

---

# 11. ORM Mapping Types

## 1) One-to-One

One object related to one object.

Example:

* Person ↔ Passport

```java
@OneToOne
private Passport passport;
```

---

## 2) One-to-Many

One object related to multiple objects.

Example:

* Department → Employees

```java
@OneToMany
private List<Employee> employees;
```

---

## 3) Many-to-One

Many objects related to one object.

Example:

* Many Students → One College

```java
@ManyToOne
private College college;
```

---

## 4) Many-to-Many

Many objects related to many objects.

Example:

* Students ↔ Courses

```java
@ManyToMany
private List<Course> courses;
```

---

# 12. Fetch Types

Defines when related data should load.

## EAGER

Loads immediately.

```java
@OneToMany(fetch = FetchType.EAGER)
```

## LAZY

Loads only when needed.

```java
@OneToMany(fetch = FetchType.LAZY)
```

---

# 13. Cascade Types

Used to apply operations automatically.

## Example

```java
@OneToMany(cascade = CascadeType.ALL)
```

## Types

| Cascade Type | Meaning           |
| ------------ | ----------------- |
| PERSIST      | Save child also   |
| REMOVE       | Delete child also |
| MERGE        | Update child also |
| ALL          | All operations    |

---

# 14. Hibernate Lifecycle States

## 1) Transient

Object created but not saved.

```java
Student s = new Student();
```

---

## 2) Persistent

Object connected to DB session.

```java
session.save(s);
```

---

## 3) Detached

Session closed but object exists.

---

## 4) Removed

Object marked for deletion.

---

# 15. CRUD Operations in ORM

## Save

```java
entityManager.persist(student);
```

---

## Read

```java
Student s = entityManager.find(Student.class, 1);
```

---

## Update

```java
entityManager.merge(student);
```

---

## Delete

```java
entityManager.remove(student);
```

---

# 16. HQL (Hibernate Query Language)

Object-oriented query language.

Works on entities, not tables.

## Example

```java
String hql = "FROM Student";
```

---

# 17. JPQL (Java Persistence Query Language)

Similar to HQL.

Works with entities.

```java
SELECT s FROM Student s
```

---

# 18. Native SQL Query

Direct SQL query.

```java
@Query(value = "SELECT * FROM students", nativeQuery = true)
```

---

# 19. First Level Cache

Enabled by default.

Session-level cache.

Same object request does not hit DB repeatedly.

---

# 20. Second Level Cache

Shared across sessions.

Needs external cache provider.

Example:

* EhCache

---

# 21. Lazy Initialization Exception

Occurs when lazy-loaded data accessed after session closed.

## Example

```java
LazyInitializationException
```

## Solution

* Use EAGER carefully
* Use JOIN FETCH
* Access before closing session

---

# 22. N+1 Query Problem

Very common ORM issue.

## Problem

One query loads parent data,
then additional queries load child data repeatedly.

### Example

```text
1 query for students
N queries for courses
```

## Solution

* JOIN FETCH
* Batch fetching

---

# 23. Transactions in ORM

Transaction ensures:

* Atomicity
* Consistency

## Example

```java
@Transactional
public void saveStudent() {

}
```

---

# 24. Benefits of ORM

* Faster development
* Reduced SQL
* Better maintainability
* Object-oriented coding
* Database independence
* Relationship handling

---

# 25. Disadvantages of ORM

* Learning curve
* Performance overhead
* Complex queries harder
* Hidden SQL generation

---

# 26. Hibernate vs JPA

| Hibernate               | JPA               |
| ----------------------- | ----------------- |
| Framework               | Specification     |
| Provides implementation | Defines rules     |
| Can work without JPA    | Cannot work alone |

---

# 27. Spring Boot + ORM

Spring Boot mainly uses:

* Spring Data JPA
* Hibernate internally

## Flow

```text
Spring Boot
   ↓
Spring Data JPA
   ↓
Hibernate
   ↓
Database
```

---

# 28. application.properties Example

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/testdb
spring.datasource.username=root
spring.datasource.password=root

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

---

# 29. Repository Layer

Spring Data JPA simplifies DB operations.

## Example

```java
public interface StudentRepository
       extends JpaRepository<Student, Integer> {

}
```

---

# 30. Common Methods in JpaRepository

| Method       | Purpose         |
| ------------ | --------------- |
| save()       | Insert/update   |
| findById()   | Find by ID      |
| findAll()    | Get all         |
| deleteById() | Delete          |
| existsById() | Check existence |

---

# 31. Custom Query Methods

```java
List<Student> findByName(String name);
```

Spring automatically generates query.

---

# 32. ORM Best Practices

* Use LAZY loading mostly
* Avoid unnecessary relationships
* Use DTOs for APIs
* Use pagination
* Avoid N+1 problem
* Keep transactions small
* Use indexes in DB

---

# 33. Important Interview Questions

## Basic

* What is ORM?
* Difference between JDBC and Hibernate?
* What is JPA?
* What is Entity?

## Intermediate

* Difference between LAZY and EAGER?
* What is Cascade?
* What is HQL?
* Lifecycle states?

## Advanced

* N+1 problem?
* First level cache?
* Second level cache?
* Difference between persist and merge?

---

# 34. ORM Flow in Real Project

```text
Controller
   ↓
Service
   ↓
Repository (JPA)
   ↓
Hibernate ORM
   ↓
Database
```

---

# 35. Most Important Topics for Spring Boot Developer

Must Know:

* JPA
* Hibernate basics
* Entity mapping
* Relationships
* CRUD
* Repository
* JPQL
* Transactions
* Lazy vs Eager
* Cascade
* Pagination

Very Important for Interviews:

* N+1 problem
* Caching
* Entity lifecycle
* Difference between save/persist/merge

---

# 36. Quick Revision Sheet

## Core Annotations

```java
@Entity
@Table
@Id
@GeneratedValue
@Column
@OneToMany
@ManyToOne
@JoinColumn
```

---

## CRUD

```java
save()
findById()
findAll()
delete()
```

---

## Relationship Types

```text
OneToOne
OneToMany
ManyToOne
ManyToMany
```

---

## Fetch Types

```text
LAZY
EAGER
```

---

## Query Types

```text
JPQL
HQL
Native SQL
```

---

# 37. Conclusion

ORM in Java simplifies database interaction by mapping Java objects to database tables.

Most modern Java backend development with Spring Boot uses:

* JPA
* Hibernate
* Spring Data JPA

Mastering ORM is essential for becoming a Java Spring Boot Developer.

```
```
