# Java Collection Framework (Collection API) Complete Notes

---

# 1. What is Collection Framework?

The **Java Collection Framework (JCF)** is a set of:
- Interfaces
- Classes
- Algorithms

used to store and manipulate groups of objects dynamically.

It provides:
- Dynamic memory allocation
- Built-in data structures
- Searching
- Sorting
- Traversing
- Data manipulation

---

# 2. Why Collection Framework Needed?

Before collections, arrays were used.

## Problems with Arrays
1. Fixed size
2. No built-in methods
3. Cannot easily grow/shrink
4. Poor memory utilization
5. Difficult insertion/deletion

Collections solve these problems.

---

# 3. Collection Framework Hierarchy

```text
                         Iterable
                             |
                        Collection
                  /            |            \
               List           Set          Queue
                 |             |
     --------------------------------
     |        |       |        |
 ArrayList LinkedList Vector  Stack

     Set Implementations:
     --------------------
     HashSet
     LinkedHashSet
     TreeSet

Map (Separate Hierarchy)
------------------------
HashMap
LinkedHashMap
TreeMap
Hashtable
```

---

# 4. Iterable Interface

The root interface of the Collection hierarchy.

It provides:
```java
iterator()
```

Used for traversing elements.

---

# 5. Collection Interface

`Collection` is the parent interface of:
- List
- Set
- Queue

It contains common methods for all collections.

---

# 6. Common Methods of Collection Interface

| Method | Description |
|---|---|
| add() | Add element |
| remove() | Remove element |
| contains() | Check existence |
| size() | Number of elements |
| isEmpty() | Checks empty |
| clear() | Removes all |
| iterator() | Returns iterator |

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        Collection<String> names = new ArrayList<>();

        names.add("Ram");
        names.add("Shyam");

        System.out.println(names);

        System.out.println(names.contains("Ram"));

        System.out.println(names.size());
    }
}
```

---

# 7. Difference Between Collection and Collections

| Collection | Collections |
|---|---|
| Interface | Utility class |
| Represents group of objects | Provides utility methods |
| Part of collection hierarchy | Helper methods |
| add(), remove() etc | sort(), reverse() etc |

---

# Example of Collections Class

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        ArrayList<Integer> list = new ArrayList<>();

        list.add(30);
        list.add(10);
        list.add(20);

        Collections.sort(list);

        System.out.println(list);
    }
}
```

---

# 8. List Interface

A List:
- Maintains insertion order
- Allows duplicates
- Allows indexing

---

# Properties of List

| Feature | Supported |
|---|---|
| Ordered | Yes |
| Duplicates | Yes |
| Indexing | Yes |
| Null values | Yes |

---

# Implementations of List

1. ArrayList
2. LinkedList
3. Vector
4. Stack

---

# 9. ArrayList

## Introduction

`ArrayList` is a dynamic array.

Internally uses:
```text
Resizable Array
```

---

# Features of ArrayList

1. Dynamic size
2. Fast random access
3. Allows duplicates
4. Maintains insertion order
5. Not thread-safe

---

# Internal Working

When capacity becomes full:
- New larger array created
- Old elements copied

Growth formula:
```text
newCapacity = oldCapacity + oldCapacity/2
```

---

# ArrayList Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        ArrayList<String> list = new ArrayList<>();

        list.add("Java");
        list.add("Python");
        list.add("C++");

        System.out.println(list);

        System.out.println(list.get(1));

        list.set(1, "JavaScript");

        System.out.println(list);

        list.remove("C++");

        System.out.println(list);
    }
}
```

---

# Important Methods of ArrayList

| Method | Description |
|---|---|
| add() | Add element |
| get() | Access element |
| set() | Update |
| remove() | Delete |
| indexOf() | Find index |
| contains() | Check existence |

---

# Time Complexity

| Operation | Complexity |
|---|---|
| Access | O(1) |
| Insert End | O(1) |
| Insert Middle | O(n) |
| Delete | O(n) |

---

# 10. LinkedList

## Introduction

Uses:
```text
Doubly Linked List
```

Each node stores:
- Data
- Previous pointer
- Next pointer

---

# Features

1. Fast insertion/deletion
2. Slow random access
3. Maintains order
4. Allows duplicates

---

# LinkedList Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        LinkedList<Integer> list = new LinkedList<>();

        list.add(10);
        list.add(20);

        list.addFirst(5);
        list.addLast(30);

        System.out.println(list);

        list.removeFirst();

        System.out.println(list);
    }
}
```

---

# Time Complexity

| Operation | Complexity |
|---|---|
| Access | O(n) |
| Insert | O(1) |
| Delete | O(1) |

---

# Difference Between ArrayList and LinkedList

| ArrayList | LinkedList |
|---|---|
| Dynamic Array | Doubly Linked List |
| Fast access | Slow access |
| Slow insertion | Fast insertion |
| Less memory | More memory |

---

# 11. Vector

## Introduction

Legacy class.

Similar to ArrayList but:
```text
Thread-safe
```

---

# Features

1. Synchronized
2. Slower
3. Dynamic array

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        Vector<Integer> v = new Vector<>();

        v.add(10);
        v.add(20);

        System.out.println(v);
    }
}
```

---

# Vector vs ArrayList

| Vector | ArrayList |
|---|---|
| Thread-safe | Not thread-safe |
| Slow | Faster |
| Legacy | Modern |

---

# 12. Stack

## Introduction

Stack follows:
```text
LIFO
(Last In First Out)
```

---

# Methods

| Method | Description |
|---|---|
| push() | Insert |
| pop() | Remove top |
| peek() | View top |
| empty() | Check empty |

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        Stack<Integer> st = new Stack<>();

        st.push(10);
        st.push(20);
        st.push(30);

        System.out.println(st);

        System.out.println(st.pop());

        System.out.println(st.peek());
    }
}
```

---

# 13. Set Interface

A Set:
- Does NOT allow duplicates
- No indexing

---

# Features of Set

| Feature | Supported |
|---|---|
| Duplicates | No |
| Ordered | Depends |
| Null | Yes |

---

# Implementations

1. HashSet
2. LinkedHashSet
3. TreeSet

---

# 14. HashSet

## Introduction

Uses:
```text
Hashing
```

Internally uses:
```text
HashMap
```

---

# Features

1. No duplicates
2. Unordered
3. Fast operations

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        HashSet<Integer> set = new HashSet<>();

        set.add(10);
        set.add(20);
        set.add(10);

        System.out.println(set);
    }
}
```

Output:
```text
[10, 20]
```

---

# Time Complexity

| Operation | Complexity |
|---|---|
| Add | O(1) |
| Remove | O(1) |
| Search | O(1) |

---

# 15. LinkedHashSet

## Features

1. Maintains insertion order
2. No duplicates
3. Uses LinkedHashMap internally

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        LinkedHashSet<Integer> set = new LinkedHashSet<>();

        set.add(30);
        set.add(10);
        set.add(20);

        System.out.println(set);
    }
}
```

Output:
```text
[30, 10, 20]
```

---

# 16. TreeSet

## Features

1. Sorted order
2. No duplicates
3. Uses Red-Black Tree

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        TreeSet<Integer> set = new TreeSet<>();

        set.add(50);
        set.add(10);
        set.add(30);

        System.out.println(set);
    }
}
```

Output:
```text
[10, 30, 50]
```

---

# HashSet vs LinkedHashSet vs TreeSet

| Feature | HashSet | LinkedHashSet | TreeSet |
|---|---|---|---|
| Order | No | Insertion | Sorted |
| Duplicate | No | No | No |
| Speed | Fastest | Medium | Slow |

---

# 17. Iterator

Iterator is used to traverse collections.

---

# Methods

| Method | Description |
|---|---|
| hasNext() | Checks next |
| next() | Returns next |
| remove() | Removes current |

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        ArrayList<Integer> list = new ArrayList<>();

        list.add(10);
        list.add(20);
        list.add(30);

        Iterator<Integer> it = list.iterator();

        while(it.hasNext()) {

            System.out.println(it.next());
        }
    }
}
```

---

# Why Iterator Needed?

1. Universal traversal
2. Safer removal during iteration
3. Avoid ConcurrentModificationException

---

# 18. ConcurrentModificationException

Occurs when collection modified during iteration.

---

# Wrong Way

```java
for(Integer n : list) {

    list.remove(n);
}
```

---

# Correct Way

```java
Iterator<Integer> it = list.iterator();

while(it.hasNext()) {

    Integer n = it.next();

    if(n == 10) {
        it.remove();
    }
}
```

---

# 19. Map Interface

Map stores:
```text
Key -> Value
```

---

# Features

1. Keys unique
2. Values duplicate allowed
3. Separate hierarchy

---

# Implementations

1. HashMap
2. LinkedHashMap
3. TreeMap
4. Hashtable

---

# 20. HashMap

## Features

1. Fast retrieval
2. Unordered
3. One null key allowed

---

# Internal Working

Uses:
```text
Hashing
```

Stores data in:
```text
Buckets
```

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        HashMap<Integer, String> map = new HashMap<>();

        map.put(1, "Ram");
        map.put(2, "Shyam");

        System.out.println(map);

        System.out.println(map.get(1));
    }
}
```

---

# Important Methods

| Method | Description |
|---|---|
| put() | Insert |
| get() | Retrieve |
| remove() | Delete |
| containsKey() | Check key |
| containsValue() | Check value |
| keySet() | Get keys |
| values() | Get values |

---

# Traversing HashMap

```java
for(Integer key : map.keySet()) {

    System.out.println(key + " " + map.get(key));
}
```

---

# 21. LinkedHashMap

## Features

1. Maintains insertion order
2. Slightly slower

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        LinkedHashMap<Integer, String> map =
                new LinkedHashMap<>();

        map.put(3, "C");
        map.put(1, "A");

        System.out.println(map);
    }
}
```

---

# 22. TreeMap

## Features

1. Sorted by keys
2. Uses Red-Black Tree

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        TreeMap<Integer, String> map =
                new TreeMap<>();

        map.put(30, "Java");
        map.put(10, "Python");

        System.out.println(map);
    }
}
```

Output:
```text
{10=Python, 30=Java}
```

---

# 23. Hashtable

## Features

1. Thread-safe
2. No null key/value
3. Legacy class

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        Hashtable<Integer, String> ht =
                new Hashtable<>();

        ht.put(1, "Java");

        System.out.println(ht);
    }
}
```

---

# Difference Between HashMap and Hashtable

| HashMap | Hashtable |
|---|---|
| Not synchronized | Synchronized |
| Faster | Slower |
| Allows null | No null |

---

# 24. Sorting in Collections

Java provides:
```java
Collections.sort()
```

---

# Sorting ArrayList

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        ArrayList<Integer> list = new ArrayList<>();

        list.add(40);
        list.add(10);
        list.add(30);

        Collections.sort(list);

        System.out.println(list);
    }
}
```

Output:
```text
[10, 30, 40]
```

---

# Reverse Sorting

```java
Collections.sort(list,
        Collections.reverseOrder());
```

---

# Example

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        ArrayList<Integer> list = new ArrayList<>();

        list.add(10);
        list.add(50);
        list.add(20);

        Collections.sort(list,
                Collections.reverseOrder());

        System.out.println(list);
    }
}
```

---

# 25. Comparable Interface

Used for:
```text
Natural Sorting
```

Method:
```java
compareTo()
```

Package:
```text
java.lang
```

---

# Example

```java
import java.util.*;

class Student implements Comparable<Student> {

    int age;
    String name;

    Student(int age, String name) {

        this.age = age;
        this.name = name;
    }

    public int compareTo(Student s) {

        return this.age - s.age;
    }

    public String toString() {

        return age + " " + name;
    }
}

public class Main {

    public static void main(String[] args) {

        ArrayList<Student> list =
                new ArrayList<>();

        list.add(new Student(22, "Ram"));
        list.add(new Student(18, "Shyam"));
        list.add(new Student(25, "Aman"));

        Collections.sort(list);

        System.out.println(list);
    }
}
```

---

# 26. Comparator Interface

Used for:
```text
Custom Sorting
```

Method:
```java
compare()
```

Package:
```text
java.util
```

---

# Example

```java
import java.util.*;

class Student {

    int age;
    String name;

    Student(int age, String name) {

        this.age = age;
        this.name = name;
    }

    public String toString() {

        return age + " " + name;
    }
}

class NameComparator
        implements Comparator<Student> {

    public int compare(Student a, Student b) {

        return a.name.compareTo(b.name);
    }
}

public class Main {

    public static void main(String[] args) {

        ArrayList<Student> list =
                new ArrayList<>();

        list.add(new Student(22, "Ram"));
        list.add(new Student(18, "Shyam"));
        list.add(new Student(25, "Aman"));

        Collections.sort(list,
                new NameComparator());

        System.out.println(list);
    }
}
```

---

# Comparator using Lambda

```java
Collections.sort(list,
        (a, b) -> a.age - b.age);
```

---

# Comparable vs Comparator

| Comparable | Comparator |
|---|---|
| Natural sorting | Custom sorting |
| compareTo() | compare() |
| java.lang | java.util |
| Inside class | Separate class |

---

# 27. Thread Safety in Collections

## Thread-safe Collections

1. Vector
2. Hashtable

---

# Non Thread-safe Collections

1. ArrayList
2. HashMap
3. HashSet

---

# 28. Synchronized Collections

```java
List<Integer> list =
Collections.synchronizedList(
        new ArrayList<>());
```

---

# 29. forEach Loop

```java
for(Integer n : list) {

    System.out.println(n);
}
```

---

# 30. Important Interview Questions

---

# Why Map is not part of Collection?

Because Collection stores individual objects.

Map stores:
```text
Key -> Value
```

So it has separate hierarchy.

---

# Why HashSet does not allow duplicates?

Because internally it uses:
```text
HashMap
```

Keys in HashMap are unique.

---

# Why ArrayList faster than LinkedList in access?

Because ArrayList uses:
```text
Direct indexing
```

LinkedList requires traversal.

---

# Why TreeSet sorted?

Because it uses:
```text
Red-Black Tree
```

---

# Difference Between fail-fast and fail-safe iterator

| Fail Fast | Fail Safe |
|---|---|
| Throws exception | No exception |
| Original collection | Clone collection |

---

# 31. Best Collection to Use

| Requirement | Best Choice |
|---|---|
| Fast access | ArrayList |
| Fast insertion/deletion | LinkedList |
| No duplicates | HashSet |
| Sorted data | TreeSet |
| Key-value | HashMap |
| Thread-safe | Vector/Hashtable |

---

# 32. Summary

## List
- Ordered
- Duplicates allowed
- Indexing supported

## Set
- No duplicates

## Map
- Key-value pairs

## HashMap
- Fastest map

## TreeSet / TreeMap
- Sorted

## Collections Class
- Utility methods

## Comparable
- Natural sorting

## Comparator
- Custom sorting

---
