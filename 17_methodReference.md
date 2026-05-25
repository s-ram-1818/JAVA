# Java Method Reference Complete Notes

---

# 1. Introduction to Method Reference

Method Reference was introduced in:
```text
Java 8
```

Method Reference is:
```text
Shorter and cleaner way
to write lambda expressions
```

Used for:
```text
Referring existing methods
```

instead of writing lambda expressions manually.

---

# Why Method Reference Needed?

---

# Lambda Expression

```java
x -> System.out.println(x)
```

---

# Method Reference

```java
System.out::println
```

Both do same work.

Method reference makes code:
- Cleaner
- Shorter
- More readable

---

# Syntax of Method Reference

```java
ClassName::methodName
```

OR

```java
objectReference::methodName
```

---

# Real Meaning

Method reference means:
```text
Pass method as argument
```

---

# 2. Functional Interface Requirement

Method reference works only with:
```text
Functional Interfaces
```

Because internally:
```text
Lambda expression conversion happens
```

---

# Example Functional Interface

```java
interface A {

    void show();
}
```

Contains only:
```text
One abstract method
```

---

# 3. Types of Method References

There are:
```text
4 Types
```

---

# Types

1. Reference to Static Method
2. Reference to Instance Method of Particular Object
3. Reference to Instance Method of Arbitrary Object
4. Reference to Constructor

---

# 4. Reference to Static Method

---

# Lambda Version

```java
x -> Math.sqrt(x)
```

---

# Method Reference Version

```java
Math::sqrt
```

---

# Example

```java
import java.util.function.Function;

public class Main {

    public static void main(String[] args) {

        Function<Integer, Double> f =
                Math::sqrt;

        System.out.println(f.apply(25));
    }
}
```

Output:
```text
5.0
```

---

# Another Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(1,2,3,4);

        list.forEach(System.out::println);
    }
}
```

---

# 5. Reference to Instance Method of Particular Object

Using:
```text
Specific object
```

---

# Example

```java
import java.util.function.Consumer;

class Test {

    public void display(String s) {

        System.out.println(s);
    }
}

public class Main {

    public static void main(String[] args) {

        Test t = new Test();

        Consumer<String> c =
                t::display;

        c.accept("Java");
    }
}
```

Output:
```text
Java
```

---

# Explanation

```java
t::display
```

means:
```text
Call display() using object t
```

---

# 6. Reference to Instance Method of Arbitrary Object

Used when:
```text
Method belongs to object type,
not specific object
```

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<String> list =
                Arrays.asList("java","python","c++");

        list.stream()
            .map(String::toUpperCase)
            .forEach(System.out::println);
    }
}
```

Output:
```text
JAVA
PYTHON
C++
```

---

# Explanation

```java
String::toUpperCase
```

means:
```text
For every String object,
call toUpperCase()
```

---

# Another Example

```java
List<String> list =
        Arrays.asList("A","B","C");

list.forEach(System.out::println);
```

---

# 7. Constructor Reference

Used to refer:
```text
Constructor
```

Syntax:
```java
ClassName::new
```

---

# Example

```java
interface A {

    Student get();
}

class Student {

    Student() {

        System.out.println("Constructor Called");
    }
}

public class Main {

    public static void main(String[] args) {

        A a = Student::new;

        a.get();
    }
}
```

Output:
```text
Constructor Called
```

---

# Constructor Reference with Parameters

---

# Example

```java
interface A {

    Student get(String name);
}

class Student {

    Student(String name) {

        System.out.println(name);
    }
}

public class Main {

    public static void main(String[] args) {

        A a = Student::new;

        a.get("Ram");
    }
}
```

Output:
```text
Ram
```

---

# 8. Method Reference vs Lambda Expression

| Lambda | Method Reference |
|---|---|
| More code | Less code |
| Explicit implementation | Direct method usage |
| Flexible | Cleaner |
| x -> System.out.println(x) | System.out::println |

---

# Example Comparison

---

# Lambda

```java
list.forEach(x -> System.out.println(x));
```

---

# Method Reference

```java
list.forEach(System.out::println);
```

---

# 9. Common Functional Interfaces Used

| Interface | Method |
|---|---|
| Consumer | accept() |
| Supplier | get() |
| Function | apply() |
| Predicate | test() |

---

# Example with Predicate

```java
import java.util.function.Predicate;

public class Main {

    public static void main(String[] args) {

        Predicate<String> p =
                String::isEmpty;

        System.out.println(p.test(""));

        System.out.println(p.test("Java"));
    }
}
```

Output:
```text
true
false
```

---

# Example with Function

```java
import java.util.function.Function;

public class Main {

    public static void main(String[] args) {

        Function<String, Integer> f =
                String::length;

        System.out.println(f.apply("Java"));
    }
}
```

Output:
```text
4
```

---

# 10. Method Reference with Streams

---

# Example

```java
import java.util.*;
import java.util.stream.*;

public class Main {

    public static void main(String[] args) {

        List<String> list =
                Arrays.asList("java","python");

        list.stream()
            .map(String::toUpperCase)
            .forEach(System.out::println);
    }
}
```

---

# Explanation

| Part | Meaning |
|---|---|
| String::toUpperCase | Convert to uppercase |
| System.out::println | Print values |

---

# 11. Internal Working

Method reference internally converted into:
```text
Lambda expression
```

Example:
```java
System.out::println
```

internally behaves like:
```java
x -> System.out.println(x)
```

---

# 12. Advantages of Method Reference

1. Cleaner code
2. Better readability
3. Less boilerplate
4. Easy functional programming
5. Works well with streams

---

# 13. Disadvantages

1. Sometimes confusing
2. Hard for beginners
3. Cannot use custom logic directly

---

# Example Where Lambda Better

```java
list.forEach(x -> {

    x = x * 2;

    System.out.println(x);
});
```

Complex logic difficult with method reference.

---

# 14. Important Interview Questions

---

# What is Method Reference?

A shorthand form of lambda expression
to refer existing methods.

---

# Why Method Reference Used?

To:
- Reduce code
- Improve readability

---

# Can Method Reference Replace All Lambdas?

No.

Only when lambda:
```text
Directly calls existing method
```

---

# Difference Between Lambda and Method Reference

| Lambda | Method Reference |
|---|---|
| Defines implementation | Refers existing method |
| More flexible | More concise |

---

# Types of Method References

1. Static Method Reference
2. Particular Object Method Reference
3. Arbitrary Object Method Reference
4. Constructor Reference

---

# Why Functional Interface Required?

Because method references work through:
```text
Lambda implementation mechanism
```

---

# 15. Complete Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<String> list =
                Arrays.asList(
                        "java",
                        "python",
                        "c++"
                );

        list.stream()
            .map(String::toUpperCase)
            .sorted()
            .forEach(System.out::println);
    }
}
```

Output:
```text
C++
JAVA
PYTHON
```

---

# 16. Summary

## Method Reference
- Shorter lambda expression

## Syntax
```java
ClassName::methodName
```

## Types
1. Static method
2. Particular object method
3. Arbitrary object method
4. Constructor

## Benefits
- Cleaner code
- Better readability

## Used With
- Streams
- Functional interfaces
- Lambda expressions

---
