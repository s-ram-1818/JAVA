# Hibernate in Java

## 1. What is Hibernate?

Hibernate ORM is a Java ORM (Object Relational Mapping) framework used to map Java objects to database tables.

It simplifies database operations by reducing manual SQL and JDBC code.

---

# 2. Why Hibernate?

Without Hibernate:

* Manual SQL queries
* Manual ResultSet handling
* More boilerplate code
* Hard maintenance

With Hibernate:

* Automatic table mapping
* Less code
* Faster development
* Database independence
* Better maintainability

---

# 3. Hibernate Architecture

```text
Java Application
       ↓
Hibernate ORM
       ↓
JDBC
       ↓
Database
```

---

# 4. Hibernate Features

* ORM support
* Automatic table mapping
* HQL support
* Caching
* Transaction management
* Lazy loading
* Relationship mapping
* Database independent

---

# 5. Hibernate vs JDBC

| JDBC               | Hibernate            |
| ------------------ | -------------------- |
| Manual SQL         | Automatic ORM        |
| More code          | Less code            |
| Manual mapping     | Object mapping       |
| Low-level          | High-level           |
| Database dependent | Database independent |

---

# 6. Hibernate vs JPA

| Hibernate               | JPA                  |
| ----------------------- | -------------------- |
| Framework               | Specification        |
| Provides implementation | Defines rules        |
| Can work directly       | Needs implementation |

## Important

```text
JPA = Rules
Hibernate = Implementation
```

---

# 7. Hibernate Dependencies (Maven)

```xml
<dependencies>

    <!-- Hibernate -->
    <dependency>
        <groupId>org.hibernate.orm</groupId>
        <artifactId>hibernate-core</artifactId>
        <version>6.x.x</version>
    </dependency>

    <!-- MySQL Driver -->
    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <version>9.x.x</version>
    </dependency>

</dependencies>
```

---

# 8. Hibernate Configuration File

## `hibernate.cfg.xml`

Used to configure:

* Database connection
* Dialect
* Username/password
* Mapping classes

Example:

```xml
<?xml version='1.0' encoding='utf-8'?>

<!DOCTYPE hibernate-configuration PUBLIC
"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
"http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">

<hibernate-configuration>

    <session-factory>

        <property name="hibernate.connection.driver_class">
            com.mysql.cj.jdbc.Driver
        </property>

        <property name="hibernate.connection.url">
            jdbc:mysql://localhost:3306/testdb
        </property>

        <property name="hibernate.connection.username">
            root
        </property>

        <property name="hibernate.connection.password">
            root
        </property>

        <property name="hibernate.dialect">
            org.hibernate.dialect.MySQLDialect
        </property>

        <property name="hibernate.hbm2ddl.auto">
            update
        </property>

        <property name="show_sql">
            true
        </property>

        <mapping class="com.entity.Student"/>

    </session-factory>

</hibernate-configuration>
```

---

# 9. Important Hibernate Classes

| Class          | Purpose              |
| -------------- | -------------------- |
| Configuration  | Loads config         |
| SessionFactory | Creates sessions     |
| Session        | DB operations        |
| Transaction    | Transaction handling |
| Query          | HQL queries          |

---

# 10. Entity Class in Hibernate

```java
import jakarta.persistence.*;

@Entity
@Table(name = "students")
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    private String name;

    private int age;

    public Student() {

    }

    // getters setters
}
```

---

# 11. Important Annotations

| Annotation      | Purpose              |
| --------------- | -------------------- |
| @Entity         | Marks entity         |
| @Table          | Table mapping        |
| @Id             | Primary key          |
| @GeneratedValue | Auto ID generation   |
| @Column         | Column mapping       |
| @OneToMany      | One to many relation |
| @ManyToOne      | Many to one relation |

---

# 12. Creating SessionFactory

```java
Configuration cfg = new Configuration();
cfg.configure("hibernate.cfg.xml");

SessionFactory factory =
        cfg.buildSessionFactory();
```

---

# 13. Creating Session

```java
Session session = factory.openSession();
```

---

# 14. Transactions

```java
Transaction tx = session.beginTransaction();
```

Commit transaction:

```java
tx.commit();
```

Rollback:

```java
tx.rollback();
```

---

# 15. CRUD Operations

## Save

```java
Student s = new Student();
s.setName("Ram");
s.setAge(22);

session.save(s);
```

---

## Read

```java
Student s = session.get(Student.class, 1);
```

---

## Update

```java
Student s = session.get(Student.class, 1);

s.setName("Updated");

session.update(s);
```

---

## Delete

```java
Student s = session.get(Student.class, 1);

session.delete(s);
```

---

# 16. Complete Example

```java
Configuration cfg = new Configuration();
cfg.configure();

SessionFactory factory =
        cfg.buildSessionFactory();

Session session = factory.openSession();

Transaction tx =
        session.beginTransaction();

Student s = new Student();
s.setName("Ram");
s.setAge(22);

session.save(s);

tx.commit();

session.close();
factory.close();
```

---

# 17. get() vs load()

| get()                     | load()           |
| ------------------------- | ---------------- |
| Immediately fetches data  | Lazy loading     |
| Returns null if not found | Throws exception |
| Hits DB immediately       | Proxy object     |

---

# 18. Hibernate Lifecycle States

## 1) Transient

Object not connected to DB.

```java
Student s = new Student();
```

---

## 2) Persistent

Object connected to session.

```java
session.save(s);
```

---

## 3) Detached

Session closed.

---

## 4) Removed

Marked for deletion.

---

# 19. HQL (Hibernate Query Language)

Works with entities instead of tables.

## Example

```java
String hql = "FROM Student";

Query q = session.createQuery(hql);

List<Student> students = q.list();
```

---

# 20. Parameterized Query

```java
Query q = session.createQuery(
    "FROM Student WHERE name=:n"
);

q.setParameter("n", "Ram");
```

---

# 21. Pagination

```java
Query q = session.createQuery("FROM Student");

q.setFirstResult(0);
q.setMaxResults(5);
```

---

# 22. Relationship Mapping

## One-to-One

```java
@OneToOne
private Passport passport;
```

---

## One-to-Many

```java
@OneToMany
private List<Student> students;
```

---

## Many-to-One

```java
@ManyToOne
private College college;
```

---

## Many-to-Many

```java
@ManyToMany
private List<Course> courses;
```

---

# 23. Fetch Types

## EAGER

Loads immediately.

```java
fetch = FetchType.EAGER
```

## LAZY

Loads only when needed.

```java
fetch = FetchType.LAZY
```

---

# 24. Cascade Types

```java
cascade = CascadeType.ALL
```

| Type    | Meaning        |
| ------- | -------------- |
| PERSIST | Save child     |
| REMOVE  | Delete child   |
| MERGE   | Update child   |
| ALL     | All operations |

---

# 25. Caching in Hibernate

## First Level Cache

* Default
* Session level

## Second Level Cache

* Shared across sessions
* External provider needed

Example:

* EhCache

---

# 26. LazyInitializationException

Occurs when lazy data accessed after session closed.

## Solution

* Use JOIN FETCH
* Access before session close
* Use DTO

---

# 27. N+1 Query Problem

## Problem

```text
1 query for parent
N queries for child
```

## Solution

* JOIN FETCH
* Batch fetching

---

# 28. hbm2ddl.auto Values

| Value       | Meaning            |
| ----------- | ------------------ |
| create      | Creates table      |
| update      | Updates schema     |
| create-drop | Creates then drops |
| validate    | Validates schema   |

---

# 29. Hibernate in Spring Boot

Spring Boot internally uses:

* JPA
* Hibernate

## application.properties

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/testdb

spring.jpa.hibernate.ddl-auto=update

spring.jpa.show-sql=true
```

---

# 30. Advantages of Hibernate

* Less boilerplate code
* Faster development
* Database independent
* Automatic mapping
* Better maintainability
* Relationship handling

---

# 31. Disadvantages

* Learning curve
* Performance overhead
* Complex queries harder
* Hidden SQL generation

---

# 32. Important Interview Questions

## Basic

* What is Hibernate?
* Difference between JDBC and Hibernate?
* What is SessionFactory?

## Intermediate

* Difference between get() and load()?
* What is HQL?
* What is lazy loading?

## Advanced

* N+1 problem?
* First vs second level cache?
* Entity lifecycle states?

---

# 33. Most Important Topics for Spring Boot Developer

Must Know:

* Entity mapping
* CRUD
* Relationships
* HQL/JPQL
* Transactions
* Fetch types
* Cascade
* Repository
* Pagination

Very Important:

* N+1 problem
* Caching
* Lazy loading
* Entity lifecycle

---

# 34. Quick Revision

## Core Classes

```java
Configuration
SessionFactory
Session
Transaction
Query
```

---

## Core Annotations

```java
@Entity
@Table
@Id
@GeneratedValue
@OneToMany
@ManyToOne
```

---

## CRUD

```java
save()
get()
update()
delete()
```

---

# 35. Conclusion

Hibernate is the most widely used ORM framework in Java backend development.

It is heavily used with:

* Spring Boot
* JPA
* MySQL/PostgreSQL

Mastering Hibernate is essential for becoming a Java Backend or Spring Boot Developer.
