# Carrier Class in Java Complete Notes

---

# 1. Introduction to Carrier Class

In Java, a **Carrier Class** is a class whose main purpose is:
```text
To carry/store data
```

with little or no business logic.

It is commonly used to:
- Transfer data
- Hold values
- Represent objects
- Pass grouped data between layers

---

# Other Names of Carrier Class

Carrier classes are also known as:
- POJO (Plain Old Java Object)
- DTO (Data Transfer Object)
- Bean Class
- Model Class
- Entity Class (sometimes)

---

# Real Life Analogy

Suppose a student form contains:
- name
- age
- rollNo

A class used only to store this data is:
```text
Carrier Class
```

---

# Example

```java
class Student {

    int id;
    String name;
}
```

This class only carries data.

---

# 2. Characteristics of Carrier Class

---

# Features

1. Stores data
2. Minimal logic
3. Private fields usually used
4. Uses getters/setters
5. Reusable object structure
6. Easy data transfer

---

# 3. Basic Carrier Class Example

```java
class Student {

    private int id;
    private String name;

    public void setId(int id) {

        this.id = id;
    }

    public int getId() {

        return id;
    }

    public void setName(String name) {

        this.name = name;
    }

    public String getName() {

        return name;
    }
}
```

---

# Using Carrier Class

```java
public class Main {

    public static void main(String[] args) {

        Student s = new Student();

        s.setId(101);
        s.setName("Ram");

        System.out.println(s.getId());
        System.out.println(s.getName());
    }
}
```

Output:
```text
101
Ram
```

---

# 4. Why Carrier Class Needed?

---

# Problem Without Carrier Class

Without carrier class:
```java
String name = "Ram";
int age = 20;
```

Managing multiple variables becomes difficult.

---

# Solution

Group related data:
```java
Student s = new Student();
```

---

# Advantages

1. Better organization
2. Easy data passing
3. Reusability
4. Encapsulation
5. Cleaner code

---

# 5. Carrier Class with Constructor

---

# Example

```java
class Student {

    private int id;
    private String name;

    Student(int id, String name) {

        this.id = id;
        this.name = name;
    }

    public int getId() {

        return id;
    }

    public String getName() {

        return name;
    }
}
```

---

# Using Constructor

```java
public class Main {

    public static void main(String[] args) {

        Student s =
                new Student(101, "Ram");

        System.out.println(s.getId());
        System.out.println(s.getName());
    }
}
```

---

# 6. Carrier Class in Real Applications

Used heavily in:
- Spring Boot
- Hibernate
- REST APIs
- JDBC
- Microservices

---

# Example in Backend

Suppose API returns:
```json
{
  "id": 1,
  "name": "Ram"
}
```

Java object used:
```java
class User {

    private int id;
    private String name;
}
```

This acts as:
```text
Carrier Class
```

---

# 7. DTO (Data Transfer Object)

DTO is a special type of carrier class.

Purpose:
```text
Transfer data between layers
```

Example:
```text
Frontend ↔ Backend
```

---

# DTO Example

```java
class UserDTO {

    private String name;
    private String email;

    // getters setters
}
```

---

# 8. POJO (Plain Old Java Object)

Simple Java class with:
- Private variables
- Public getters/setters

Usually acts as carrier class.

---

# POJO Example

```java
class Employee {

    private int id;
    private String name;

    public int getId() {

        return id;
    }

    public void setId(int id) {

        this.id = id;
    }
}
```

---

# 9. Java Bean vs Carrier Class

---

# Java Bean Rules

1. Private variables
2. Public getters/setters
3. No-arg constructor
4. Serializable (optional)

---

# Example

```java
import java.io.Serializable;

class StudentBean
implements Serializable {

    private int id;

    public StudentBean() {

    }

    public int getId() {

        return id;
    }

    public void setId(int id) {

        this.id = id;
    }
}
```

---

# 10. Immutable Carrier Class

Immutable means:
```text
Cannot change after creation
```

---

# Example

```java
final class Student {

    private final int id;
    private final String name;

    Student(int id, String name) {

        this.id = id;
        this.name = name;
    }

    public int getId() {

        return id;
    }

    public String getName() {

        return name;
    }
}
```

---

# Advantages of Immutable Carrier Class

1. Thread-safe
2. Secure
3. No accidental modification

---

# 11. Record Class (Modern Carrier Class)

Java introduced:
```text
Records
```

in Java 14 (preview)
and Java 16 officially.

Records are:
```text
Special carrier classes
```

designed specifically for:
```text
Holding data
```

---

# Record Syntax

```java
record Student(int id, String name) {}
```

Automatically provides:
- Constructor
- Getter methods
- toString()
- equals()
- hashCode()

---

# Example

```java
record Student(int id, String name) {}

public class Main {

    public static void main(String[] args) {

        Student s =
                new Student(101, "Ram");

        System.out.println(s.id());
        System.out.println(s.name());
    }
}
```

Output:
```text
101
Ram
```

---

# Why Records Introduced?

To reduce boilerplate code.

---

# Traditional Class

```java
class Student {

    private int id;
    private String name;

    // constructor
    // getters
    // toString
    // equals
    // hashCode
}
```

Too much code.

---

# Record Version

```java
record Student(int id, String name) {}
```

Very concise.

---

# 12. Record Features

1. Immutable
2. Final class
3. Auto-generated methods
4. Cleaner syntax
5. Ideal carrier class

---

# 13. Record Internal Working

This:
```java
record Student(int id, String name){}
```

internally behaves almost like:

```java
final class Student {

    private final int id;
    private final String name;

    public Student(int id, String name) {

        this.id = id;
        this.name = name;
    }

    public int id() {

        return id;
    }

    public String name() {

        return name;
    }
}
```

---

# 14. Difference Between Normal Class and Record

| Normal Class | Record |
|---|---|
| More boilerplate | Less code |
| Mutable possible | Immutable |
| Manual methods | Auto-generated |
| Flexible | Data-focused |

---

# 15. When to Use Carrier Class?

Use when:
- Need object to hold data
- Passing data between layers
- API request/response
- Database entity
- Model representation

---

# 16. Advantages of Carrier Class

1. Better code structure
2. Encapsulation
3. Reusable
4. Easier maintenance
5. Cleaner architecture

---

# 17. Disadvantages

1. Too many classes possible
2. Boilerplate code in traditional classes
3. Memory overhead

---

# 18. Important Interview Questions

---

# What is Carrier Class?

A class mainly used to:
```text
Store and transfer data
```

---

# Is Record a Carrier Class?

Yes.

Records are:
```text
Modern compact carrier classes
```

---

# Why Records Introduced?

To reduce:
```text
Boilerplate code
```

for data-carrying classes.

---

# Are Records Immutable?

Yes.

Record fields are:
```text
final
```

---

# Difference Between POJO and Record

| POJO | Record |
|---|---|
| Manual code | Auto-generated |
| Mutable possible | Immutable |
| More code | Less code |

---

# Can Record Extend Class?

No.

Because records are implicitly:
```text
final
```

---

# Can Record Implement Interface?

Yes.

---

# Example

```java
interface A {

    void show();
}

record Student(int id)
implements A {

    public void show() {

        System.out.println(id);
    }
}
```

---

# 19. Complete Example

```java
record Employee(
        int id,
        String name,
        double salary
) {}

public class Main {

    public static void main(String[] args) {

        Employee e =
                new Employee(
                        101,
                        "Ram",
                        50000
                );

        System.out.println(e);

        System.out.println(e.name());
    }
}
```

Output:
```text
Employee[id=101, name=Ram, salary=50000.0]
Ram
```

---

# 20. Summary

## Carrier Class
- Stores/transfers data

## POJO
- Simple Java object

## DTO
- Data transfer object

## Java Bean
- Standardized POJO

## Record
- Modern compact carrier class

## Benefits
- Cleaner code
- Better architecture
- Easy data handling

---
