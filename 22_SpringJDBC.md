
# Spring JDBC Complete Notes

## What is Spring JDBC?

Spring JDBC is a module of Spring Framework that simplifies database operations using JDBC.

Without Spring JDBC:
- Load Driver
- Create Connection
- Create Statement
- Execute Query
- Handle Exceptions
- Close Resources

Spring JDBC handles most of these tasks automatically.

Benefits:
- Less boilerplate code
- Better exception handling
- Easy CRUD operations
- Integration with Spring Boot

---

# JDBC Architecture

Client
   |
Spring JDBC
   |
JdbcTemplate
   |
JDBC Driver
   |
Database

---

# Required Dependencies

## Maven Dependency

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>

<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
</dependency>
````

---

# Database Configuration

## application.properties

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/studentdb
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

---

# Sample Table

```sql
CREATE TABLE student(
    id INT PRIMARY KEY,
    name VARCHAR(50),
    city VARCHAR(50)
);
```

---

# Entity Class

```java
public class Student {

    private int id;
    private String name;
    private String city;

    public Student() {}

    public Student(int id, String name, String city) {
        this.id = id;
        this.name = name;
        this.city = city;
    }

    // Getters and Setters
}
```

---

# JdbcTemplate

JdbcTemplate is the main class in Spring JDBC.

It provides methods for:

* Insert
* Update
* Delete
* Select
* Aggregate Queries

```java
@Autowired
private JdbcTemplate jdbcTemplate;
```

---

# INSERT DATA

Method:

```java
int update(String sql,Object... args)
```

Example:

```java
String sql =
"INSERT INTO student(id,name,city) VALUES(?,?,?)";

int rows = jdbcTemplate.update(
        sql,
        student.getId(),
        student.getName(),
        student.getCity()
);

return rows;
```

Generated SQL:

```sql
INSERT INTO student VALUES(1,'Ram','Pune');
```

---

# UPDATE DATA

Method:

```java
int update(String sql,Object... args)
```

Example:

```java
String sql =
"UPDATE student SET city=? WHERE id=?";

int rows =
jdbcTemplate.update(sql,"Mumbai",1);
```

Generated SQL:

```sql
UPDATE student
SET city='Mumbai'
WHERE id=1;
```

---

# DELETE DATA

Method:

```java
int update(String sql,Object... args)
```

Example:

```java
String sql =
"DELETE FROM student WHERE id=?";

int rows =
jdbcTemplate.update(sql,1);
```

Generated SQL:

```sql
DELETE FROM student WHERE id=1;
```

---

# FETCH SINGLE RECORD

Method:

```java
queryForObject()
```

Used when exactly one row is expected.

Example:

```java
String sql =
"SELECT * FROM student WHERE id=?";

Student student =
jdbcTemplate.queryForObject(
    sql,
    new BeanPropertyRowMapper<>(Student.class),
    1
);
```

Output:

```java
Student(
 id=1,
 name="Ram",
 city="Pune"
)
```

---

# FETCH MULTIPLE RECORDS

Method:

```java
query()
```

Example:

```java
String sql =
"SELECT * FROM student";

List<Student> students =
jdbcTemplate.query(
    sql,
    new BeanPropertyRowMapper<>(Student.class)
);
```

Returns:

```java
List<Student>
```

---

# FETCH SINGLE COLUMN

Method:

```java
queryForObject()
```

Example:

```java
String sql =
"SELECT COUNT(*) FROM student";

Integer count =
jdbcTemplate.queryForObject(
    sql,
    Integer.class
);
```

Output:

```java
5
```

---

# FETCH STRING VALUE

Example:

```java
String sql =
"SELECT name FROM student WHERE id=?";

String name =
jdbcTemplate.queryForObject(
    sql,
    String.class,
    1
);
```

Output:

```java
Ram
```

---

# RowMapper

Used to convert database rows into Java objects.

Interface:

```java
public interface RowMapper<T>
```

Example:

```java
public class StudentRowMapper
implements RowMapper<Student> {

    @Override
    public Student mapRow(
        ResultSet rs,
        int rowNum
    ) throws SQLException {

        Student s = new Student();

        s.setId(rs.getInt("id"));
        s.setName(rs.getString("name"));
        s.setCity(rs.getString("city"));

        return s;
    }
}
```

Usage:

```java
List<Student> students =
jdbcTemplate.query(
    "SELECT * FROM student",
    new StudentRowMapper()
);
```

---

# BeanPropertyRowMapper

Automatically maps:

Database Column → Java Field

Example:

| Column | Field |
| ------ | ----- |
| id     | id    |
| name   | name  |
| city   | city  |

Usage:

```java
new BeanPropertyRowMapper<>(Student.class)
```

No need to manually create RowMapper.

---

# Student Repository

```java
@Repository
public class StudentRepository {

    @Autowired
    JdbcTemplate jdbcTemplate;

    public int save(Student student){

        String sql =
        "INSERT INTO student VALUES(?,?,?)";

        return jdbcTemplate.update(
            sql,
            student.getId(),
            student.getName(),
            student.getCity()
        );
    }

    public int updateCity(
        int id,
        String city
    ){

        String sql =
        "UPDATE student SET city=? WHERE id=?";

        return jdbcTemplate.update(
            sql,
            city,
            id
        );
    }

    public int delete(int id){

        String sql =
        "DELETE FROM student WHERE id=?";

        return jdbcTemplate.update(
            sql,
            id
        );
    }

    public Student getById(int id){

        String sql =
        "SELECT * FROM student WHERE id=?";

        return jdbcTemplate.queryForObject(
            sql,
            new BeanPropertyRowMapper<>(
                Student.class
            ),
            id
        );
    }

    public List<Student> getAll(){

        String sql =
        "SELECT * FROM student";

        return jdbcTemplate.query(
            sql,
            new BeanPropertyRowMapper<>(
                Student.class
            )
        );
    }
}
```

---

# Service Layer

```java
@Service
public class StudentService {

    @Autowired
    StudentRepository repository;

    public int addStudent(Student student){
        return repository.save(student);
    }

    public int updateStudent(
        int id,
        String city
    ){
        return repository.updateCity(id,city);
    }

    public int deleteStudent(int id){
        return repository.delete(id);
    }

    public Student getStudent(int id){
        return repository.getById(id);
    }

    public List<Student> getStudents(){
        return repository.getAll();
    }
}
```

---

# Controller Layer

```java
@RestController
@RequestMapping("/students")
public class StudentController {

    @Autowired
    StudentService service;

    @PostMapping
    public String addStudent(
        @RequestBody Student student
    ){
        service.addStudent(student);
        return "Student Added";
    }

    @PutMapping("/{id}")
    public String updateStudent(
        @PathVariable int id,
        @RequestParam String city
    ){
        service.updateStudent(id,city);
        return "Student Updated";
    }

    @DeleteMapping("/{id}")
    public String deleteStudent(
        @PathVariable int id
    ){
        service.deleteStudent(id);
        return "Student Deleted";
    }

    @GetMapping("/{id}")
    public Student getStudent(
        @PathVariable int id
    ){
        return service.getStudent(id);
    }

    @GetMapping
    public List<Student> getStudents(){
        return service.getStudents();
    }
}
```

---

# Important JdbcTemplate Methods

## update()

Used For:

* Insert
* Update
* Delete

```java
jdbcTemplate.update(sql,args);
```

Returns:

```java
int
```

(Number of rows affected)

---

## query()

Used For:

* Multiple rows

```java
jdbcTemplate.query(
    sql,
    rowMapper
);
```

Returns:

```java
List<T>
```

---

## queryForObject()

Used For:

* Single row
* Single value

```java
jdbcTemplate.queryForObject(
    sql,
    rowMapper
);
```

Returns:

```java
T
```

---

## queryForList()

Returns list of rows.

```java
List<Map<String,Object>> list =
jdbcTemplate.queryForList(
    "SELECT * FROM student"
);
```

---

## queryForMap()

Returns single row as Map.

```java
Map<String,Object> row =
jdbcTemplate.queryForMap(
    "SELECT * FROM student WHERE id=1"
);
```

---

## queryForRowSet()

Returns SqlRowSet.

```java
SqlRowSet rs =
jdbcTemplate.queryForRowSet(
    "SELECT * FROM student"
);
```

---

# Exceptions

## EmptyResultDataAccessException

Occurs when no record found.

```java
try{

}
catch(
 EmptyResultDataAccessException e
){

}
```

---

# Spring JDBC Flow

Request
↓
Controller
↓
Service
↓
Repository
↓
JdbcTemplate
↓
Database

Response
↑
Controller
↑
Client

---

# Interview Questions

### What is JdbcTemplate?

JdbcTemplate is the core class of Spring JDBC used to execute SQL queries and perform database operations.

---

### Why use Spring JDBC?

* Reduces JDBC boilerplate code
* Automatic resource management
* Better exception handling
* Easy CRUD operations

---

### Difference between JDBC and Spring JDBC?

JDBC:

* More code
* Manual connection handling
* Manual exception handling

Spring JDBC:

* Less code
* Automatic connection handling
* Spring exceptions

---

### Difference between query() and queryForObject()?

query()

* Multiple records
* Returns List

queryForObject()

* Single record/value
* Returns Object

---

### Which method is used for Insert, Update and Delete?

```java
update()
```

---

### Which method returns List?

```java
query()
queryForList()
```

---

### Which method returns one object?

```java
queryForObject()
```

---

### What is RowMapper?

Used to convert ResultSet rows into Java objects.

---

### What is BeanPropertyRowMapper?

Automatically maps database columns to Java fields based on matching names.

```

### JdbcTemplate Methods Quick Revision

| Method | Purpose | Return Type |
|----------|----------|----------|
| update() | Insert/Update/Delete | int |
| query() | Multiple Rows | List<T> |
| queryForObject() | Single Row/Value | T |
| queryForList() | List of Rows | List<Map> |
| queryForMap() | Single Row | Map |
| queryForRowSet() | RowSet | SqlRowSet |

This covers the complete Spring JDBC CRUD workflow (Insert, Update, Delete, Get One, Get All) along with all commonly used `JdbcTemplate` methods and interview questions.
```
