# Java Optional Complete Notes

---

# 1. Introduction to Optional

`Optional` was introduced in:
```text
Java 8
```

Package:
```java
java.util.Optional
```

Optional is a container object used to:
```text
Avoid NullPointerException
```

It may:
- Contain value
OR
- Be empty

---

# Why Optional Needed?

Before Optional:

```java
String name = null;

System.out.println(name.length());
```

Output:
```text
NullPointerException
```

This is one of the most common exceptions in Java.

Optional helps avoid this problem.

---

# 2. What is NullPointerException?

Occurs when:
```text
Trying to access methods/fields
on null reference
```

---

# Example

```java
String s = null;

System.out.println(s.length());
```

Output:
```text
Exception in thread "main"
java.lang.NullPointerException
```

---

# 3. Creating Optional Objects

---

# 1. Optional.of()

Used when value:
```text
Definitely NOT null
```

---

# Example

```java
import java.util.Optional;

public class Main {

    public static void main(String[] args) {

        Optional<String> op =
                Optional.of("Java");

        System.out.println(op);
    }
}
```

Output:
```text
Optional[Java]
```

---

# Important

If null passed:
```java
Optional.of(null)
```

It throws:
```text
NullPointerException
```

---

# 2. Optional.ofNullable()

Used when value:
```text
May be null
```

---

# Example

```java
import java.util.Optional;

public class Main {

    public static void main(String[] args) {

        String name = null;

        Optional<String> op =
                Optional.ofNullable(name);

        System.out.println(op);
    }
}
```

Output:
```text
Optional.empty
```

---

# 3. Optional.empty()

Creates empty Optional.

---

# Example

```java
Optional<String> op =
        Optional.empty();

System.out.println(op);
```

Output:
```text
Optional.empty
```

---

# 4. Checking Value Presence

---

# isPresent()

Checks whether value exists.

---

# Example

```java
import java.util.Optional;

public class Main {

    public static void main(String[] args) {

        Optional<String> op =
                Optional.of("Java");

        System.out.println(op.isPresent());
    }
}
```

Output:
```text
true
```

---

# Example with Empty

```java
Optional<String> op =
        Optional.empty();

System.out.println(op.isPresent());
```

Output:
```text
false
```

---

# 5. Getting Value from Optional

---

# get()

Returns value inside Optional.

---

# Example

```java
Optional<String> op =
        Optional.of("Java");

System.out.println(op.get());
```

Output:
```text
Java
```

---

# Important

Calling get() on empty Optional throws:
```text
NoSuchElementException
```

---

# Wrong Example

```java
Optional<String> op =
        Optional.empty();

System.out.println(op.get());
```

Output:
```text
NoSuchElementException
```

---

# Safe Way

```java
if(op.isPresent()) {

    System.out.println(op.get());
}
```

---

# 6. orElse()

Returns:
- Actual value if present
- Default value if empty

---

# Example

```java
import java.util.Optional;

public class Main {

    public static void main(String[] args) {

        Optional<String> op =
                Optional.empty();

        String result =
                op.orElse("Default");

        System.out.println(result);
    }
}
```

Output:
```text
Default
```

---

# Example with Value

```java
Optional<String> op =
        Optional.of("Java");

System.out.println(
        op.orElse("Default")
);
```

Output:
```text
Java
```

---

# 7. orElseGet()

Works like:
```text
orElse()
```

But accepts:
```text
Supplier
```

Value created only if needed.

---

# Example

```java
Optional<String> op =
        Optional.empty();

String result =
        op.orElseGet(() -> "Generated Value");

System.out.println(result);
```

---

# Difference Between orElse and orElseGet

| orElse() | orElseGet() |
|---|---|
| Always creates object | Creates only if needed |
| Less efficient sometimes | More efficient |

---

# 8. orElseThrow()

Throws exception if value absent.

---

# Example

```java
Optional<String> op =
        Optional.empty();

String result =
        op.orElseThrow(
            () -> new RuntimeException("No Value")
        );
```

Output:
```text
RuntimeException: No Value
```

---

# 9. ifPresent()

Executes code only if value exists.

---

# Example

```java
Optional<String> op =
        Optional.of("Java");

op.ifPresent(
        x -> System.out.println(x)
);
```

Output:
```text
Java
```

---

# 10. map() with Optional

Used to transform value.

---

# Example

```java
Optional<String> op =
        Optional.of("java");

Optional<String> upper =
        op.map(String::toUpperCase);

System.out.println(upper.get());
```

Output:
```text
JAVA
```

---

# 11. filter() with Optional

Filters value based on condition.

---

# Example

```java
Optional<String> op =
        Optional.of("Java");

Optional<String> result =
        op.filter(
            x -> x.startsWith("J")
        );

System.out.println(result);
```

Output:
```text
Optional[Java]
```

---

# Condition Fails

```java
Optional<String> result =
        op.filter(
            x -> x.startsWith("P")
        );

System.out.println(result);
```

Output:
```text
Optional.empty
```

---

# 12. Optional with Streams

---

# Example

```java
import java.util.*;
import java.util.stream.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(10,20,30);

        Optional<Integer> result =
                list.stream()
                    .filter(x -> x > 15)
                    .findFirst();

        System.out.println(result.get());
    }
}
```

Output:
```text
20
```

---

# findFirst()

Returns:
```text
Optional
```

because result may not exist.

---

# 13. Real World Example

---

# Without Optional

```java
String name = getName();

if(name != null) {

    System.out.println(name.toUpperCase());
}
```

---

# With Optional

```java
Optional<String> name =
        getName();

name.map(String::toUpperCase)
    .ifPresent(System.out::println);
```

---

# 14. Optional in Method Return Type

---

# Example

```java
public Optional<String> getName() {

    return Optional.of("Java");
}
```

---

# Why Good?

Caller forced to:
```text
Handle missing value
```

---

# 15. Optional Best Practices

---

# Good Practices

1. Use as return type
2. Use for nullable values
3. Use map/filter methods
4. Prefer orElse/orElseGet

---

# Bad Practices

1. Do NOT use Optional in fields
2. Do NOT use Optional in constructor params
3. Avoid get() without checking
4. Avoid Optional for every variable

---

# Wrong Practice

```java
class Student {

    Optional<String> name;
}
```

Not recommended.

---

# 16. Optional Methods Summary

| Method | Purpose |
|---|---|
| of() | Create non-null Optional |
| ofNullable() | Nullable Optional |
| empty() | Empty Optional |
| isPresent() | Check value |
| get() | Get value |
| orElse() | Default value |
| orElseGet() | Lazy default |
| orElseThrow() | Throw exception |
| ifPresent() | Execute if exists |
| map() | Transform |
| filter() | Condition check |

---

# 17. Optional vs Null

| Null | Optional |
|---|---|
| Unsafe | Safe |
| Causes NPE | Avoids NPE |
| Manual checks | Built-in handling |
| Hard to understand | Explicit |

---

# 18. Important Interview Questions

---

# Why Optional Introduced?

To reduce:
```text
NullPointerException
```

and improve code readability.

---

# Is Optional Serializable?

No.

---

# Can Optional Contain Null?

No.

Optional either:
- Contains value
OR
- Empty

---

# Difference Between of() and ofNullable()

| of() | ofNullable() |
|---|---|
| Null not allowed | Null allowed |
| Throws exception | Returns empty |

---

# Difference Between orElse and orElseGet

| orElse | orElseGet |
|---|---|
| Always evaluates | Lazy evaluation |
| Less efficient | More efficient |

---

# Why get() Dangerous?

Because empty Optional causes:
```text
NoSuchElementException
```

---

# 19. Complete Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        Optional<String> op =
                Optional.ofNullable("Java");

        op.map(String::toUpperCase)
          .filter(x -> x.startsWith("J"))
          .ifPresent(System.out::println);

        String result =
                op.orElse("Default");

        System.out.println(result);
    }
}
```

Output:
```text
JAVA
Java
```

---

# 20. Summary

## Optional
- Container object
- Avoids NullPointerException

## of()
- Non-null values

## ofNullable()
- Nullable values

## empty()
- Empty Optional

## orElse()
- Default value

## map()
- Transform value

## filter()
- Apply condition

## ifPresent()
- Execute if value exists

## Best Use
- Method return type

---
