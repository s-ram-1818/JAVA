# Wrapper Classes in Java

# What are Wrapper Classes?

Wrapper classes are classes that convert primitive data types into objects.

Java provides a separate wrapper class for every primitive type.

---

# Why Wrapper Classes are Needed?

Primitive data types:
- are not objects
- cannot store methods
- cannot be used directly in collections/generics

Many Java APIs work only with objects.

So Java introduced wrapper classes.

---

# Primitive Types and Their Wrapper Classes

| Primitive Type | Wrapper Class |
|---|---|
| byte | Byte |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
| char | Character |
| boolean | Boolean |

---

# Important Point

All wrapper classes are available in:
```java
java.lang package
```

So no need to import.

---

# Example

```java
int x = 10;

Integer obj = Integer.valueOf(x);

System.out.println(obj);
```

## Output
```java
10
```

---

# Primitive vs Wrapper Object

| Primitive | Wrapper Object |
|---|---|
| Stores direct value | Stores object |
| Faster | Slower |
| Less memory | More memory |
| No methods | Has methods |

---

# Memory Concept

## Primitive Variable
```java
int x = 10;
```

Value stored directly in stack memory.

---

## Wrapper Object
```java
Integer obj = 10;
```

- Reference stored in stack
- Object stored in heap

---

# Boxing

# What is Boxing?

Converting primitive data type into wrapper object manually.

---

# Example

```java
int x = 100;

Integer obj = Integer.valueOf(x);

System.out.println(obj);
```

## Internal Working

```java
Integer obj = new Integer(100);
```

(Older style)

---

# Autoboxing

# What is Autoboxing?

Automatic conversion of primitive into wrapper object by JVM.

---

# Example

```java
int x = 50;

Integer obj = x;

System.out.println(obj);
```

## Internal Working

```java
Integer obj = Integer.valueOf(x);
```

Automatically done by compiler.

---

# Unboxing

# What is Unboxing?

Converting wrapper object into primitive manually.

---

# Example

```java
Integer obj = Integer.valueOf(200);

int x = obj.intValue();

System.out.println(x);
```

---

# Auto-Unboxing

# What is Auto-Unboxing?

Automatic conversion of wrapper object into primitive.

---

# Example

```java
Integer obj = 300;

int x = obj;

System.out.println(x);
```

## Internal Working

```java
int x = obj.intValue();
```

---

# Complete Conversion Flow

```java
int x = 10;

Integer obj = x;   // Autoboxing

int y = obj;       // Auto-Unboxing
```

---

# Important Wrapper Class Methods

| Method | Purpose |
|---|---|
| valueOf() | Primitive/String → Object |
| parseInt() | String → Primitive |
| toString() | Value → String |
| intValue() | Object → int |
| doubleValue() | Object → double |
| compareTo() | Compare objects |
| equals() | Compare values |

---

# valueOf()

Used to create wrapper object.

---

# Example

```java
Integer obj = Integer.valueOf(100);

System.out.println(obj);
```

## Output
```java
100
```

---

# parseInt()

Used to convert String into primitive int.

---

# Example

```java
String s = "123";

int x = Integer.parseInt(s);

System.out.println(x);
```

## Output
```java
123
```

---

# Important Difference

| valueOf() | parseInt() |
|---|---|
| Returns object | Returns primitive |
| Integer | int |

---

# Example

```java
Integer a = Integer.valueOf("10");

int b = Integer.parseInt("10");

System.out.println(a);
System.out.println(b);
```

---

# toString()

Converts value/object into String.

---

# Example

```java
Integer x = 100;

String s = x.toString();

System.out.println(s);
```

## Output
```java
100
```

---

# compareTo()

Used to compare two wrapper objects.

---

# Rules of compareTo()

| Condition | Return |
|---|---|
| First > Second | Positive |
| First < Second | Negative |
| Equal | 0 |

---

# Example 1

```java
Integer a = 10;
Integer b = 20;

System.out.println(a.compareTo(b));
```

## Internal Working

```java
10 < 20
```

So output:
```java
-1
```

Meaning:
```java
a is smaller than b
```

---

# Example 2

```java
Integer a = 50;
Integer b = 20;

System.out.println(a.compareTo(b));
```

## Internal Working

```java
50 > 20
```

So output:
```java
1
```

Meaning:
```java
a is greater than b
```

---

# Example 3

```java
Integer a = 100;
Integer b = 100;

System.out.println(a.compareTo(b));
```

## Internal Working

```java
100 == 100
```

So output:
```java
0
```

Meaning:
```java
Both are equal
```

---

# Important Interview Point

compareTo() does not strictly return:
```java
-1, 0, 1
```

It returns:
- Any negative value
- 0
- Any positive value

---

# equals()

Used to compare actual values.

---

# Example

```java
Integer a = 100;
Integer b = 100;

System.out.println(a.equals(b));
```

## Output
```java
true
```

Because values are same.

---

# == vs equals()

| == | equals() |
|---|---|
| Compares references | Compares values |
| Checks memory address | Checks actual content |

---

# Example

```java
Integer a = new Integer(100);
Integer b = new Integer(100);

System.out.println(a == b);
System.out.println(a.equals(b));
```

## Output

```java
false
true
```

---

# Why?

## a == b

Checks:
```java
Do both references point to same object?
```

No.

So:
```java
false
```

---

## equals()

Checks:
```java
Do both objects contain same value?
```

Yes.

So:
```java
true
```

---

# Integer Caching

Java caches Integer objects from:
```java
-128 to 127
```

---

# Example

```java
Integer a = 100;
Integer b = 100;

System.out.println(a == b);
```

## Output
```java
true
```

---

# Why?

Because:
```java
100 lies inside cache range
```

So same object reused.

---

# Example Outside Cache Range

```java
Integer a = 200;
Integer b = 200;

System.out.println(a == b);
```

## Output
```java
false
```

---

# Why?

Because:
```java
200 is outside cache range
```

Separate objects created.

---

# Collections and Wrapper Classes

Collections store objects only.

Primitive types are not allowed.

---

# Wrong

```java
ArrayList<int> list = new ArrayList<>();
```

Compile-time error.

---

# Correct

```java
ArrayList<Integer> list = new ArrayList<>();
```

---

# Example

```java
import java.util.*;

class Demo {

    public static void main(String[] args) {

        ArrayList<Integer> list = new ArrayList<>();

        list.add(10);
        list.add(20);

        System.out.println(list);
    }
}
```

## Output
```java
[10, 20]
```

---

# Wrapper Classes and Strings

---

# String → Primitive

```java
String s = "50";

int x = Integer.parseInt(s);

System.out.println(x + 10);
```

## Output
```java
60
```

---

# Primitive → String

```java
int x = 100;

String s = String.valueOf(x);

System.out.println(s);
```

---

# Wrapper Object → String

```java
Integer x = 200;

String s = x.toString();

System.out.println(s);
```

---

# NumberFormatException

Occurs when invalid String converted into number.

---

# Example

```java
String s = "abc";

int x = Integer.parseInt(s);
```

## Result
```java
NumberFormatException
```

---

# Why Wrapper Classes are Immutable?

Wrapper objects cannot change once created.

---

# Example

```java
Integer a = 10;

a = 20;
```

This does NOT modify old object.

Instead:
- old object remains
- new object created

---

# Wrapper Classes are Final

Most wrapper classes are final.

Meaning:
```java
cannot inherit them
```

---

# Example

```java
final class Integer
```

So:
```java
class A extends Integer // ERROR
```

---

# Performance Issue

Wrapper classes are slower because:
- object creation required
- heap memory used
- autoboxing/unboxing overhead

---

# Primitive is Faster

```java
int x = 10;
```

Faster than:
```java
Integer x = 10;
```

---

# Null Problem in Wrapper Classes

Wrapper objects can store:
```java
null
```

Primitive cannot.

---

# Example

```java
Integer x = null;

System.out.println(x);
```

Valid.

---

# But Primitive Cannot

```java
int x = null;
```

Compile-time error.

---

# NullPointerException Example

```java
Integer x = null;

int y = x;
```

## Why Error?

Because:
```java
auto-unboxing tries x.intValue()
```

But x is null.

So:
```java
NullPointerException
```

---

# Important Interview Questions

1. What are wrapper classes?
2. Why wrapper classes needed?
3. Difference between primitive and wrapper?
4. What is boxing?
5. What is autoboxing?
6. What is unboxing?
7. Difference between valueOf() and parseInt()?
8. Difference between == and equals()?
9. What is Integer caching?
10. Why collections use wrapper classes?
11. Why wrapper classes are immutable?
12. What is auto-unboxing?
13. Can wrapper object store null?
14. Why wrapper classes are slower?

---

# Quick Revision

# Boxing
```java
Integer obj = Integer.valueOf(10);
```

---

# Autoboxing
```java
Integer obj = 10;
```

---

# Unboxing
```java
int x = obj.intValue();
```

---

# Auto-Unboxing
```java
int x = obj;
```

---

# Final Summary Table

| Concept | Meaning |
|---|---|
| Wrapper Class | Primitive as object |
| Boxing | Primitive → Object |
| Unboxing | Object → Primitive |
| Autoboxing | Automatic boxing |
| Auto-Unboxing | Automatic unboxing |
| parseInt() | String → int |
| valueOf() | String/Primitive → Object |
| equals() | Compare values |
| == | Compare references |

---

# Final Conclusion

Wrapper classes:
- convert primitives into objects
- help collections and generics work
- provide utility methods
- support autoboxing/unboxing
- are immutable and mostly final
- use heap memory
- are slower than primitives
