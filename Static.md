
# Complete Notes of Static Keyword in Java

# 1. Introduction to Static Keyword

The `static` keyword in Java is used for memory management.

- Static members belong to the **class**, not objects.
- They can be accessed without creating objects.

---

# Syntax

```java
static dataType variableName;
````

---

# Where Static Keyword Can Be Used?

`static` keyword can be used with:

1. Variable
2. Method
3. Block
4. Nested Class

---

# 2. Static Variable

## Definition

A variable declared using `static` keyword is called static variable.

* Shared among all objects
* Only one copy exists

---

# Example

```java id="2m1y49"
class Student
{
    int roll;
    String name;

    static String college = "GECA";
}
```

---

# Accessing Static Variable

## Using Class Name (Recommended)

```java id="ct7yit"
System.out.println(Student.college);
```

---

## Using Object

```java id="6lj17h"
Student s = new Student();

System.out.println(s.college);
```

Possible but not recommended.

---

# Memory Allocation of Static Variable

* Stored in:

  * Method Area / Class Area

* Memory allocated only once.

---

# Example of Shared Static Variable

```java id="q8g2do"
class Counter
{
    static int count = 0;

    Counter()
    {
        count++;
        System.out.println(count);
    }
}

public class Main
{
    public static void main(String[] args)
    {
        new Counter();
        new Counter();
        new Counter();
    }
}
```

Output:

```text id="ap2zqf"
1
2
3
```

Explanation:

* Same `count` variable shared among all objects.

---

# Static vs Non-Static Variable

| Feature      | Static Variable | Non-Static Variable |
| ------------ | --------------- | ------------------- |
| Belongs To   | Class           | Object              |
| Copies       | One             | Separate per object |
| Shared       | Yes             | No                  |
| Access Using | Class name      | Object              |

---

# 3. Static Method

## Definition

A method declared using `static` keyword is called static method.

* Belongs to class
* Can be called without object

---

# Example

```java id="mhtfcb"
class Demo
{
    static void show()
    {
        System.out.println("Static Method");
    }

    public static void main(String[] args)
    {
        Demo.show();
    }
}
```

Output:

```text id="x3xtef"
Static Method
```

---

# Features of Static Method

* Can access only static members directly
* Cannot use `this`
* Cannot use `super`

---

# Example

```java id="p5mjlwm"
class Test
{
    int x = 10;
    static int y = 20;

    static void display()
    {
        // System.out.println(x); // Error
        System.out.println(y);
    }
}
```

---

# Why Main Method is Static?

```java id="cah9gl"
public static void main(String[] args)
```

Reason:

* JVM calls `main()` without object creation.

---

# 4. Static Block

## Definition

A block declared using `static` keyword.

Used for:

* Static initialization
* Runs automatically during class loading

---

# Syntax

```java id="l8i7p9"
static
{
    
}
```

---

# Example

```java id="0drkrv"
class Demo
{
    static int x;

    static
    {
        x = 100;
        System.out.println("Static Block Executed");
    }

    public static void main(String[] args)
    {
        System.out.println(x);
    }
}
```

Output:

```text id="gmz8r6"
Static Block Executed
100
```

---

# Important Features of Static Block

* Executes before main()
* Executes only once
* Automatically called by JVM

---

# 5. When Does Static Block Execute?

Static block executes when JVM loads the class.

---

# 6. When Does JVM Load a Class?

JVM loads class in these situations:

1. Object creation
2. Static variable access
3. Static method call
4. Using `Class.forName()`

---

# Important Point

## Object creation is NOT mandatory to load a class.

Creating object is only one way to load class.

Static block can execute even without object creation.

---

# Example Without Object Creation

```java id="jlwmg8"
class Demo
{
    static int x = 10;

    static
    {
        System.out.println("Static Block");
    }

    public static void main(String[] args)
    {
        System.out.println(Demo.x);
    }
}
```

Output:

```text id="75l9o4"
Static Block
10
```

Explanation:

* No object created
* Static variable access loaded class
* Static block executed

---

# Example Using Static Method

```java id="ddjth5"
class Demo
{
    static
    {
        System.out.println("Static Block");
    }

    static void show()
    {
        System.out.println("Static Method");
    }

    public static void main(String[] args)
    {
        Demo.show();
    }
}
```

Output:

```text id="q0u2xa"
Static Block
Static Method
```

---

# Static Block Executes Only Once

```java id="exczb0"
class Demo
{
    static
    {
        System.out.println("Static Block");
    }

    Demo()
    {
        System.out.println("Constructor");
    }

    public static void main(String[] args)
    {
        Demo d1 = new Demo();
        Demo d2 = new Demo();
    }
}
```

Output:

```text id="7o4m7y"
Static Block
Constructor
Constructor
```

---

# Can We Call Static Block Manually?

No.

❌ Wrong:

```java id="vrz9wl"
Demo.staticBlock();
```

Reason:

* Static block is not a method
* JVM executes it automatically

---

# 7. Static Nested Class

## Definition

A class declared static inside another class.

---

# Example

```java id="qk5pq0"
class Outer
{
    static class Inner
    {
        void show()
        {
            System.out.println("Static Nested Class");
        }
    }
}

public class Main
{
    public static void main(String[] args)
    {
        Outer.Inner obj = new Outer.Inner();

        obj.show();
    }
}
```

---

# 8. Static vs Non-Static Members

| Feature           | Static     | Non-Static |
| ----------------- | ---------- | ---------- |
| Belongs To        | Class      | Object     |
| Memory Allocation | Once       | Per object |
| Shared            | Yes        | No         |
| Access            | Class name | Object     |

---

# 9. Important Rules

---

# Static Method Cannot Access Non-Static Members Directly

```java id="h4c4d7"
class Test
{
    int x = 10;
    static int y = 20;

    static void show()
    {
        // System.out.println(x); // Error
        System.out.println(y);
    }
}
```

Reason:

* Static belongs to class
* Non-static belongs to object

---

# Static Method Cannot Use this Keyword

```java id="j0n23p"
static void show()
{
    // System.out.println(this.x); // Error
}
```

Reason:

* `this` refers to current object
* Static methods belong to class

---

# Static Method Cannot Use super Keyword

Because:

* `super` refers to parent object

---

# 10. Real Life Example

```java id="kwv5m5"
class Employee
{
    int id;
    String name;

    static String company = "TCS";
}
```

Explanation:

* Every employee has different:

  * id
  * name

* Same:

  * company

So company should be static.

---

# 11. Advantages of Static Keyword

* Memory efficient
* Shared data handling
* Easy access without object
* Useful for utility methods

---

# 12. Common Interview Questions

---

# What is Static Keyword?

`static` keyword makes members belong to class instead of objects.

---

# Why Main Method is Static?

Because JVM calls it without creating object.

---

# Can Static Method Access Non-Static Variables?

No, directly it cannot.

---

# Can We Override Static Methods?

No.

Static methods are method hidden, not overridden.

---

# What is Static Block?

A block executed automatically when class loads.

---

# Why Static Variable is Memory Efficient?

Because only one copy is created.

---

# What is Static Nested Class?

A nested class declared using static keyword.

---

# 13. Important Points to Remember

* Static belongs to class.
* Static members are shared.
* Static methods can be called without objects.
* Static block executes automatically.
* Static block runs only once.
* Main method is static.
* Object creation is not mandatory for class loading.
* Static methods cannot use `this` or `super`.
* Static variables are memory efficient.

```
```
