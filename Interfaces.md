# Interfaces in Java

# What is an Interface?

An interface in Java is used to achieve:
```java
abstraction
```

It defines:
- what a class should do
- not how it should do

---

# Simple Definition

Interface is a blueprint of a class.

It contains:
- abstract methods
- constants

---

# Real Life Example

## Remote Control

Remote has:
- buttons

But internal implementation:
- hidden

TV companies implement buttons differently.

This is interface concept.

---

# Why Use Interface?

Interfaces are used for:
- abstraction
- multiple inheritance
- loose coupling
- standardization
- flexibility

---

# Syntax

```java
interface Animal {

    void sound();
}
```

---

# Important Point

By default:
```java
all methods inside interface are:
public abstract
```

So internally:

```java
interface Animal {

    public abstract void sound();
}
```

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

# Important Rule

When implementing interface:
```java
method must be public
```

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

# Why?

Because interface method is:
```java
public
```

Child cannot reduce visibility.

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

## No

Because:
```java
interface is incomplete
```

---

# Example

```java
interface A {

}

// A obj = new A(); // ERROR
```

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

Method call decided at runtime.

---

# Why Use Interface Reference?

For:
```java
runtime polymorphism
```

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

Variables become constants.

So:

```java
x = 20;
```

Not allowed.

---

# Accessing Interface Variables

```java
System.out.println(Demo.x);
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

So Java avoids it.

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

# Class Implementing Child Interface

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

# Interface vs Abstract Class

| Interface | Abstract Class |
|---|---|
| Full abstraction | Partial abstraction |
| Uses implements | Uses extends |
| No constructor | Constructor allowed |
| Multiple inheritance possible | Single inheritance |
| Variables are static final | Normal variables allowed |

---

# Java 8 Features in Interface

Before Java 8:
```java
only abstract methods allowed
```

After Java 8:
- default methods
- static methods

allowed.

---

# Default Method

Method with body inside interface.

Uses:
```java
default
```

keyword.

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

# Why Default Methods Added?

To add new functionality without breaking old code.

---

# Static Method in Interface

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

# Java 9 Feature

Private methods allowed inside interface.

---

# Example

```java
interface A {

    private void show() {
        System.out.println("Private Method");
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
- Lambda Expressions
- Stream API
- Functional Programming

---

# Common Functional Interfaces

| Interface | Package |
|---|---|
| Runnable | java.lang |
| Comparator | java.util |
| Callable | java.util.concurrent |

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
```

---

# Why Marker Interface?

Used to provide special information to JVM.

---

# Loose Coupling Using Interface

Interface helps:
```java
reduce dependency between classes
```

---

# Example

```java
interface Payment {

    void pay();
}
```

Different classes:
- UPI
- Card
- NetBanking

can implement same interface.

---

# Advantages of Interface

- Achieves abstraction
- Supports multiple inheritance
- Improves flexibility
- Loose coupling
- Better maintainability

---

# Disadvantages

- More classes/interfaces needed
- Can increase complexity

---

# Important Interview Questions

1. What is interface?
2. Why interfaces are used?
3. Difference between interface and abstract class?
4. Why interface methods are public?
5. Can interface have constructor?
6. Can interface have variables?
7. What are default methods?
8. What are static methods in interface?
9. What is functional interface?
10. What is marker interface?
11. Why Java does not support multiple inheritance with classes?
12. Difference between extends and implements?
13. Can we create object of interface?
14. Can interface contain private methods?

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

# Functional Interface

```java
@FunctionalInterface
interface Demo {

    void show();
}
```

---

# Final Summary Table

| Concept | Meaning |
|---|---|
| Interface | Blueprint of class |
| implements | Used to inherit interface |
| Default Method | Method with body |
| Static Method | Static interface method |
| Functional Interface | One abstract method |
| Marker Interface | No methods |

---

# Final Conclusion

Interfaces are one of the most important concepts in Java.

They help achieve:
- abstraction
- loose coupling
- multiple inheritance
- flexibility

Modern Java heavily uses interfaces in:
- collections
- streams
- lambda expressions
- frameworks
