# Java Streams API Complete Notes

---

# 1. Introduction to Streams API

Streams were introduced in:
```text
Java 8
```

Streams are used for:
- Processing collections
- Functional programming
- Filtering data
- Sorting
- Mapping
- Reducing
- Parallel processing

---

# What is Stream?

A Stream is:
```text
A sequence of objects that supports
functional-style operations.
```

Streams do NOT store data.

They process data from:
- Collections
- Arrays
- Files

---

# Real Life Analogy

```text
Collection = Data Storage
Stream = Data Processing Pipeline
```

Example:
```text
Collection -> Stream -> Filter -> Sort -> Output
```

---

# Features of Streams

1. Functional programming support
2. Less code
3. Internal iteration
4. Lazy execution
5. Parallel processing support
6. Does not modify original data

---

# Traditional Approach vs Stream

---

# Traditional Approach

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(10, 15, 20, 25, 30);

        List<Integer> even =
                new ArrayList<>();

        for(Integer n : list) {

            if(n % 2 == 0) {
                even.add(n);
            }
        }

        System.out.println(even);
    }
}
```

---

# Stream Approach

```java
import java.util.*;
import java.util.stream.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(10, 15, 20, 25, 30);

        List<Integer> even =
                list.stream()
                    .filter(n -> n % 2 == 0)
                    .collect(Collectors.toList());

        System.out.println(even);
    }
}
```

---

# 2. How Stream Works

```text
Source
  ↓
Intermediate Operations
  ↓
Terminal Operation
```

---

# Example

```java
list.stream()
    .filter(x -> x % 2 == 0)
    .map(x -> x * 2)
    .forEach(System.out::println);
```

---

# Explanation

| Part | Purpose |
|---|---|
| stream() | Create stream |
| filter() | Filter elements |
| map() | Transform |
| forEach() | Final operation |

---

# 3. Creating Streams

---

# From Collection

```java
List<Integer> list =
        Arrays.asList(1, 2, 3);

Stream<Integer> stream =
        list.stream();
```

---

# From Array

```java
int[] arr = {1, 2, 3};

IntStream stream =
        Arrays.stream(arr);
```

---

# Using Stream.of()

```java
Stream<Integer> stream =
        Stream.of(1, 2, 3, 4);
```

---

# 4. Intermediate Operations

Intermediate operations:
- Return Stream
- Lazy
- Chainable

---

# Common Intermediate Operations

| Method | Purpose |
|---|---|
| filter() | Select elements |
| map() | Transform |
| sorted() | Sorting |
| distinct() | Remove duplicates |
| limit() | Limit elements |
| skip() | Skip elements |

---

# filter()

Used to filter data.

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(10, 15, 20, 25);

        list.stream()
            .filter(n -> n % 2 == 0)
            .forEach(System.out::println);
    }
}
```

Output:
```text
10
20
```

---

# map()

Used to transform data.

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(1, 2, 3);

        list.stream()
            .map(n -> n * n)
            .forEach(System.out::println);
    }
}
```

Output:
```text
1
4
9
```

---

# sorted()

Used for sorting.

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(30, 10, 20);

        list.stream()
            .sorted()
            .forEach(System.out::println);
    }
}
```

---

# distinct()

Removes duplicates.

---

# Example

```java
List<Integer> list =
        Arrays.asList(1,1,2,2,3);

list.stream()
    .distinct()
    .forEach(System.out::println);
```

---

# limit()

Limits number of elements.

---

# Example

```java
Stream.of(1,2,3,4,5)
      .limit(3)
      .forEach(System.out::println);
```

---

# skip()

Skips elements.

---

# Example

```java
Stream.of(1,2,3,4,5)
      .skip(2)
      .forEach(System.out::println);
```

---

# 5. Terminal Operations

Terminal operations:
- Produce result
- End stream

---

# Common Terminal Operations

| Method | Purpose |
|---|---|
| forEach() | Print/process |
| collect() | Convert |
| count() | Count |
| reduce() | Reduce to single value |
| findFirst() | First element |
| anyMatch() | Match condition |

---

# collect()

Used to collect stream result.

---

# Example

```java
import java.util.*;
import java.util.stream.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> result =
                Stream.of(1,2,3,4)
                      .collect(Collectors.toList());

        System.out.println(result);
    }
}
```

---

# count()

```java
long count =
        Stream.of(1,2,3,4)
              .count();

System.out.println(count);
```

---

# reduce()

Used to combine elements into one value.

---

# Example

```java
import java.util.stream.*;

public class Main {

    public static void main(String[] args) {

        int sum =
                Stream.of(1,2,3,4)
                      .reduce(0,
                       (a,b) -> a+b);

        System.out.println(sum);
    }
}
```

Output:
```text
10
```

---

# 6. Predicate Interface

Predicate is:
```text
Functional Interface
```

Package:
```text
java.util.function
```

Used for:
```text
Condition checking
```

---

# Method of Predicate

```java
boolean test(T t)
```

---

# Example

```java
import java.util.function.Predicate;

public class Main {

    public static void main(String[] args) {

        Predicate<Integer> isEven =
                n -> n % 2 == 0;

        System.out.println(isEven.test(10));

        System.out.println(isEven.test(7));
    }
}
```

Output:
```text
true
false
```

---

# Predicate with Streams

```java
import java.util.*;
import java.util.function.Predicate;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(10,15,20,25);

        Predicate<Integer> even =
                n -> n % 2 == 0;

        list.stream()
            .filter(even)
            .forEach(System.out::println);
    }
}
```

---

# Predicate Chaining

---

# and()

```java
Predicate<Integer> p1 =
        n -> n > 10;

Predicate<Integer> p2 =
        n -> n % 2 == 0;

System.out.println(
        p1.and(p2).test(20)
);
```

---

# or()

```java
System.out.println(
        p1.or(p2).test(9)
);
```

---

# negate()

```java
System.out.println(
        p1.negate().test(5)
);
```

---

# 7. Parallel Stream

Parallel Stream allows:
```text
Parallel processing
```

Uses:
```text
Multiple CPU cores
```

---

# Sequential Stream

Default stream processing.

Processes:
```text
One by one
```

---

# Parallel Stream

Processes:
```text
Multiple tasks simultaneously
```

---

# Creating Parallel Stream

---

# Method 1

```java
list.parallelStream()
```

---

# Method 2

```java
list.stream().parallel()
```

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(1,2,3,4,5);

        list.parallelStream()
            .forEach(System.out::println);
    }
}
```

---

# Output Order

Output may be:
```text
Random order
```

because threads run simultaneously.

---

# Example

Possible output:
```text
3
5
1
4
2
```

---

# 8. Sequential Stream vs Parallel Stream

| Sequential Stream | Parallel Stream |
|---|---|
| Single thread | Multiple threads |
| Slower for huge data | Faster for huge data |
| Ordered | Unordered possible |
| Simple processing | Parallel processing |
| Uses one CPU core | Uses multiple CPU cores |

---

# Sequential Stream Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(1,2,3,4,5);

        list.stream()
            .forEach(System.out::println);
    }
}
```

Output:
```text
1
2
3
4
5
```

---

# Parallel Stream Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        List<Integer> list =
                Arrays.asList(1,2,3,4,5);

        list.parallelStream()
            .forEach(System.out::println);
    }
}
```

Possible Output:
```text
3
5
2
1
4
```

---

# 9. Difference Between forEach and forEachOrdered

---

# forEach()

Order not guaranteed in parallel stream.

---

# Example

```java
list.parallelStream()
    .forEach(System.out::println);
```

---

# forEachOrdered()

Maintains order.

---

# Example

```java
list.parallelStream()
    .forEachOrdered(System.out::println);
```

---

# 10. Parallel Stream Internal Working

Internally uses:
```text
ForkJoinPool
```

Tasks divided into:
```text
Subtasks
```

Then processed in parallel.

---

# 11. Advantages of Streams

1. Less code
2. Better readability
3. Functional programming
4. Easy filtering
5. Parallel processing
6. Better productivity

---

# 12. Disadvantages of Streams

1. Debugging difficult
2. Not ideal for small tasks
3. Parallel streams may create overhead
4. Cannot reuse stream

---

# 13. Stream Cannot Be Reused

---

# Wrong

```java
Stream<Integer> stream =
        Stream.of(1,2,3);

stream.forEach(System.out::println);

stream.forEach(System.out::println);
```

---

# Exception

```text
java.lang.IllegalStateException
```

---

# 14. Lazy Evaluation

Intermediate operations execute only when terminal operation called.

---

# Example

```java
Stream.of(1,2,3)
      .filter(x -> {
          System.out.println(x);
          return true;
      });
```

Nothing printed because:
```text
No terminal operation
```

---

# 15. Method References

Shorter lambda syntax.

---

# Example

```java
list.stream()
    .forEach(System.out::println);
```

Equivalent to:
```java
list.stream()
    .forEach(x -> System.out.println(x));
```

---

# 16. Important Interview Questions

---

# Difference Between Collection and Stream

| Collection | Stream |
|---|---|
| Stores data | Processes data |
| Eager | Lazy |
| Reusable | Non-reusable |

---

# Why Streams Introduced?

To support:
```text
Functional Programming
```

and reduce boilerplate code.

---

# When to Use Parallel Stream?

Use when:
- Huge data
- CPU intensive tasks
- Independent operations

Avoid when:
- Small data
- Shared mutable state
- Order important

---

# Difference Between map() and filter()

| map() | filter() |
|---|---|
| Transform data | Select data |
| Returns modified element | Returns boolean-based result |

---

# Difference Between Intermediate and Terminal Operation

| Intermediate | Terminal |
|---|---|
| Returns stream | Returns result |
| Lazy | Executes stream |

---

# 17. Summary

## Stream
- Process data
- Functional programming
- Lazy operations

## Predicate
- Functional interface
- Used for conditions

## Parallel Stream
- Multi-threaded processing

## Sequential Stream
- Single-threaded processing

## filter()
- Select elements

## map()
- Transform elements

## reduce()
- Combine elements

## collect()
- Convert stream result

---
