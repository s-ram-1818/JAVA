# Complete Interface Notes in Java

# What is an Interface?

An interface in Java is a mechanism used to achieve:
```java
abstraction
```

It defines:
- what a class should do
- not how it should do

---

# Simple Definition

Interface is a:
```java
blueprint of a class
```

It contains:
- abstract methods
- constants
- default methods
- static methods
- private methods (Java 9)

---

# Real Life Example

# Remote Control Example

Remote contains buttons like:
- power
- volume
- channels

But:
```java
internal implementation is hidden
```

Different TV companies implement buttons differently.

This is interface concept.

---

# Why Interface is Needed?

Interfaces are used for:
- abstraction
- loose coupling
- flexibility
- multiple inheritance
- standardization

---

# Important Idea

Interface defines:
```java
RULES / CONTRACT
```

Implementing class must follow those rules.

---

# Syntax

```java
interface Animal {

    void sound();
}
```

---

# Internal Understanding

By default:
```java
all interface methods are:
public abstract
```

So internally:

```java
interface Animal {

    public abstract void sound();
}
```

---

# Important Rule

You do NOT need to write:
```java
public abstract
```

because Java adds it automatically.

---

# Implementing Interface

A class uses:
```java
implements
```

keyword.

---

# Example

```java
interface Animal {

    void sound();
}

class Dog implements Animal {

    public void sound() {
        System.out.println("Dog Barks");
    }
}

class Main {

    public static void main(String[] args) {

        Dog d = new Dog();

        d.sound();
    }
}
```

## Output
```java
Dog Barks
```

---

# Why public Needed in Child Class?

Interface methods are:
```java
public
```

Child cannot reduce visibility.

---

# Wrong Example

```java
interface A {

    void show();
}

class B implements A {

    void show() {

    }
}
```

Compile-time error.

---

# Correct Example

```java
class B implements A {

    public void show() {

    }
}
```

---

# Can We Create Object of Interface?

## NO

---

# Example

```java
interface A {

}

// A obj = new A(); // ERROR
```

---

# Why?

Because:
```java
interface is incomplete
```

No implementation exists.

---

# Interface Reference Variable

Parent interface reference can hold child object.

---

# Example

```java
interface Animal {

    void sound();
}

class Dog implements Animal {

    public void sound() {
        System.out.println("Bark");
    }
}

class Main {

    public static void main(String[] args) {

        Animal a = new Dog();

        a.sound();
    }
}
```

## Output
```java
Bark
```

---

# Internal Understanding

```java
Animal a = new Dog();
```

Means:
- reference type = Animal
- object type = Dog

---

# Why Use Parent Reference?

Used for:
```java
runtime polymorphism
```

---

# Method Call Process

```java
a.sound();
```

At runtime JVM checks:
```java
actual object type
```

which is:
```java
Dog
```

So Dog's sound() executes.

---

# Interface Variables

All variables inside interface are:
```java
public static final
```

by default.

---

# Example

```java
interface Demo {

    int x = 10;
}
```

Internally:

```java
public static final int x = 10;
```

---

# Important Point

Interface variables become:
```java
constants
```

So:
```java
x = 20;
```

not allowed.

---

# Accessing Interface Variables

```java
System.out.println(Demo.x);
```

---

# Why Variables are static?

Because:
```java
interface object cannot be created
```

So variables belong to interface itself.

---

# Why final?

Because:
```java
constants should not change
```

---

# Multiple Inheritance Using Interface

Java does NOT support:
```java
multiple inheritance using classes
```

But supports:
```java
multiple inheritance using interfaces
```

---

# Example

```java
interface A {

    void show();
}

interface B {

    void display();
}

class Test implements A, B {

    public void show() {
        System.out.println("Show");
    }

    public void display() {
        System.out.println("Display");
    }
}
```

---

# Why Java Avoids Multiple Inheritance with Classes?

Because of:
```java
Diamond Problem
```

---

# Diamond Problem

```java
class A {

    void show() {
        System.out.println("A");
    }
}

class B extends A {

}

class C extends A {

}

// class D extends B, C
```

Problem:
```java
Which show() should D inherit?
```

Confusion occurs.

---

# Why Interface Solves Diamond Problem?

Because traditional interface methods:
```java
do not contain body
```

So no ambiguity.

---

# Interface Extending Interface

An interface can inherit another interface using:
```java
extends
```

---

# Example

```java
interface A {

    void show();
}

interface B extends A {

    void display();
}
```

---

# Implementing Child Interface

```java
class Test implements B {

    public void show() {
        System.out.println("Show");
    }

    public void display() {
        System.out.println("Display");
    }
}
```

---

# Multiple Interface Inheritance

An interface can extend multiple interfaces.

---

# Example

```java
interface A {

    void show();
}

interface B {

    void display();
}

interface C extends A, B {

}
```

---

# Important Rule

Class implementing interface must implement:
```java
all abstract methods
```

---

# What if Methods Not Implemented?

Then class must become:
```java
abstract
```

---

# Example

```java
interface A {

    void show();
}

abstract class B implements A {

}
```

Valid.

---

# Interface vs Abstract Class

| Interface | Abstract Class |
|---|---|
| Full abstraction | Partial abstraction |
| implements keyword | extends keyword |
| Multiple inheritance possible | Single inheritance |
| No constructor | Constructor allowed |
| Variables are static final | Normal variables allowed |
| No instance variables | Instance variables allowed |

---

# Java 8 Features in Interface

Before Java 8:
```java
only abstract methods allowed
```

After Java 8:
- default methods
- static methods

added.

---

# Default Method

Method with body inside interface.

Uses:
```java
default
```

keyword.

---

# Why Default Methods Added?

To:
```java
add new methods without breaking old code
```

---

# Example

```java
interface A {

    default void show() {
        System.out.println("Default Method");
    }
}

class Test implements A {

}
```

---

# Calling Default Method

```java
class Main {

    public static void main(String[] args) {

        Test t = new Test();

        t.show();
    }
}
```

## Output
```java
Default Method
```

---

# Can Child Override Default Method?

## YES

---

# Example

```java
interface A {

    default void show() {
        System.out.println("A");
    }
}

class B implements A {

    public void show() {
        System.out.println("B");
    }
}
```

---

# Default Method Diamond Problem

---

# Example

```java
interface A {

    default void show() {
        System.out.println("A");
    }
}

interface B {

    default void show() {
        System.out.println("B");
    }
}

class Test implements A, B {

    public void show() {
        System.out.println("Resolved");
    }
}
```

---

# Why Override Mandatory?

Because JVM gets confused:
```java
which default method should execute?
```

So child must resolve ambiguity.

---

# Calling Specific Interface Default Method

---

# Syntax

```java
InterfaceName.super.method();
```

---

# Example

```java
interface A {

    default void show() {
        System.out.println("A");
    }
}

interface B {

    default void show() {
        System.out.println("B");
    }
}

class Test implements A, B {

    public void show() {

        A.super.show();
        B.super.show();
    }
}
```

---

# Static Methods in Interface

After Java 8:
```java
static methods allowed
```

---

# Example

```java
interface A {

    static void display() {
        System.out.println("Static Method");
    }
}
```

---

# Calling Static Method

```java
A.display();
```

---

# Important Point

Static interface methods:
```java
cannot be inherited
```

---

# Wrong

```java
Test.display();
```

Compile-time error.

---

# Why?

Because static methods belong to:
```java
interface itself
```

---

# Private Methods in Interface (Java 9)

Java 9 introduced:
```java
private methods
```

inside interfaces.

---

# Why Private Methods Added?

To:
```java
avoid code duplication
```

between default methods.

---

# Example

```java
interface A {

    default void show() {
        common();
    }

    default void display() {
        common();
    }

    private void common() {
        System.out.println("Common Logic");
    }
}
```

---

# Functional Interface

Interface containing:
```java
exactly one abstract method
```

---

# Example

```java
interface Demo {

    void show();
}
```

---

# @FunctionalInterface Annotation

Used to ensure:
```java
only one abstract method exists
```

---

# Example

```java
@FunctionalInterface
interface Demo {

    void show();
}
```

---

# Invalid Functional Interface

```java
@FunctionalInterface
interface Demo {

    void show();

    void display();
}
```

Compile-time error.

---

# Why Functional Interfaces Important?

Used in:
- lambda expressions
- stream API
- functional programming

---

# Common Functional Interfaces

| Interface | Package |
|---|---|
| Runnable | java.lang |
| Comparator | java.util |
| Callable | java.util.concurrent |
| Predicate | java.util.function |
| Consumer | java.util.function |

---

# Lambda Expression with Interface

---

# Example

```java
@FunctionalInterface
interface Demo {

    void show();
}

class Main {

    public static void main(String[] args) {

        Demo d = () -> {
            System.out.println("Lambda");
        };

        d.show();
    }
}
```

---

# Marker Interface

Interface with:
```java
no methods
```

---

# Example

```java
Serializable
Cloneable
Remote
```

---

# Why Marker Interface?

Provides:
```java
special information to JVM
```

---

# Example

```java
Serializable
```

means:
```java
object can be converted into stream
```

---

# Loose Coupling Using Interface

Interface reduces dependency between classes.

---

# Example

```java
interface Payment {

    void pay();
}
```

Different implementations:
- UPI
- Card
- NetBanking

---

# Benefits

You can change implementation:
```java
without changing client code
```

---

# Real World Example

```java
List list = new ArrayList();
```

Why use List reference?

Because:
```java
implementation can change easily
```

Example:
```java
List list = new LinkedList();
```

---

# Nested Interface

Interface inside another class/interface.

---

# Example

```java
class A {

    interface Demo {

        void show();
    }
}
```

---

# Anonymous Interface Implementation

---

# Example

```java
interface Demo {

    void show();
}

class Main {

    public static void main(String[] args) {

        Demo d = new Demo() {

            public void show() {
                System.out.println("Anonymous");
            }
        };

        d.show();
    }
}
```

---

# Memory Understanding

Interface itself:
```java
does not store object state
```

Only implementing classes create objects.

---

# Important Restrictions

- Cannot create interface object
- Interface constructors not allowed
- Variables are constants
- Methods are public
- Multiple inheritance allowed

---

# Important Interview Questions

1. What is interface?
2. Why interfaces are used?
3. Difference between abstract class and interface?
4. Why interface methods are public?
5. Why interface variables are static final?
6. Can interface have constructor?
7. What are default methods?
8. Why default methods added?
9. What are static methods in interface?
10. What are private methods in interface?
11. What is functional interface?
12. What is marker interface?
13. What is loose coupling?
14. Difference between extends and implements?
15. Why Java does not support multiple inheritance with classes?
16. What is diamond problem?
17. Can interface extend interface?
18. Can interface implement interface?
19. Can interface contain nested interface?
20. Why interfaces are heavily used in frameworks?

---

# Quick Revision

# Interface

```java
interface A {

    void show();
}
```

---

# Implement Interface

```java
class B implements A {

    public void show() {

    }
}
```

---

# Default Method

```java
default void show() {

}
```

---

# Static Method

```java
static void display() {

}
```

---

# Private Method

```java
private void common() {

}
```

---

# Functional Interface

```java
@FunctionalInterface
interface Demo {

    void show();
}
```

---

# Marker Interface

```java
Serializable
```

---

# Final Summary Table

| Concept | Meaning |
|---|---|
| Interface | Blueprint/contract |
| implements | Used by class |
| extends | Used by interface |
| Default Method | Method with body |
| Static Method | Interface static method |
| Functional Interface | One abstract method |
| Marker Interface | No methods |
| Loose Coupling | Reduce dependency |
| Diamond Problem | Multiple inheritance ambiguity |

---

# Final Conclusion

Interfaces are one of the most powerful concepts in Java.

They provide:
- abstraction
- flexibility
- loose coupling
- multiple inheritance
- functional programming support

Modern Java frameworks heavily depend on interfaces because they make code:
- scalable
- maintainable
- reusable
- loosely coupled
