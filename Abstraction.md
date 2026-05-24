# Abstraction in Java

# What is Abstraction?

Abstraction means:
```java
show only essential details and hide internal implementation
```

User only knows:
- what an object does
- not how it works internally

---

# Real Life Example

## Car

You know:
- steering
- brake
- accelerator

But internally:
- engine mechanism
- fuel injection
- wiring

are hidden.

This is abstraction.

---

# ATM Example

You:
- insert card
- enter PIN
- withdraw money

But internal banking process is hidden.

---

# Why Abstraction?

Abstraction is used to:
- reduce complexity
- increase security
- hide implementation details
- focus only on functionality

---

# Ways to Achieve Abstraction in Java

Java provides abstraction using:

1. Abstract Class
2. Interface

---

# 1. Abstract Class

A class declared using:
```java
abstract
```
keyword.

---

# Syntax

```java
abstract class A {

}
```

---

# Important Rules of Abstract Class

- Cannot create object directly
- Can contain:
  - abstract methods
  - normal methods
  - constructors
  - static methods
  - variables

---

# Abstract Method

A method without body.

---

# Syntax

```java
abstract void show();
```

---

# Example

```java
abstract class Animal {

    abstract void sound();
}
```

---

# Complete Example

```java
abstract class Animal {

    abstract void sound();
}

class Dog extends Animal {

    void sound() {
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

# Internal Understanding

## Abstract Class Says:
```java
Every animal must have sound()
```

But:
```java
how sound comes depends on child class
```

---

# Why Abstract Method?

To force child classes to provide implementation.

---

# Important Rule

If a class contains abstract method:
```java
class must also be abstract
```

---

# Example

## Wrong

```java
class A {

    abstract void show();
}
```

Compile-time error.

---

# Correct

```java
abstract class A {

    abstract void show();
}
```

---

# Can We Create Object of Abstract Class?

## No

Because:
```java
abstract class is incomplete
```

---

# Example

```java
abstract class A {

}

class Main {

    public static void main(String[] args) {

        // A obj = new A(); // ERROR
    }
}
```

---

# Abstract Class Can Have Normal Methods

---

# Example

```java
abstract class Vehicle {

    abstract void start();

    void stop() {
        System.out.println("Vehicle Stopped");
    }
}

class Car extends Vehicle {

    void start() {
        System.out.println("Car Started");
    }
}

class Main {

    public static void main(String[] args) {

        Car c = new Car();

        c.start();
        c.stop();
    }
}
```

## Output
```java
Car Started
Vehicle Stopped
```

---

# Abstract Class Can Have Constructor

---

# Example

```java
abstract class A {

    A() {
        System.out.println("Abstract Constructor");
    }
}

class B extends A {

}

class Main {

    public static void main(String[] args) {

        B obj = new B();
    }
}
```

## Output
```java
Abstract Constructor
```

---

# Why Constructor in Abstract Class?

Used to initialize common properties.

---

# Abstract Class Reference

Parent abstract class reference can hold child object.

---

# Example

```java
abstract class Animal {

    abstract void sound();
}

class Dog extends Animal {

    void sound() {
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

# Why Use Parent Reference?

Because:
```java
runtime polymorphism
```

happens using parent reference.

---

# Important Point

```java
Animal a = new Dog();
```

Means:
- reference type = Animal
- object type = Dog

Method call decided at runtime.

---

# What Happens if Child Does Not Implement Abstract Method?

Then child class must also become abstract.

---

# Example

```java
abstract class A {

    abstract void show();
}

abstract class B extends A {

}
```

Valid.

---

# Concrete Class

A normal class with complete implementation.

---

# Example

```java
class Demo {

    void show() {

    }
}
```

---

# Difference Between Abstract Class and Concrete Class

| Abstract Class | Concrete Class |
|---|---|
| Incomplete | Complete |
| Cannot create object | Object can be created |
| May contain abstract method | No abstract method required |

---

# 2. Interface

Interface provides:
```java
100% abstraction
```

(Traditional concept before Java 8)

---

# Syntax

```java
interface Animal {

    void sound();
}
```

---

# Important Points About Interface

- Cannot create object
- Methods are:
```java
public abstract
```
by default

- Variables are:
```java
public static final
```
by default

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

# implements Keyword

Used to inherit interface.

---

# Difference Between extends and implements

| Keyword | Used For |
|---|---|
| extends | Class inheritance |
| implements | Interface inheritance |

---

# Why Interface?

Used for:
- full abstraction
- multiple inheritance
- loose coupling

---

# Multiple Inheritance Using Interface

Java does not support:
```java
multiple inheritance with classes
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

# Why Java Does Not Support Multiple Inheritance with Classes?

Because of:
```java
Diamond Problem
```

---

# Diamond Problem Example

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

Confusion:
```java
which show() should D inherit?
```

So Java avoids it.

---

# Interface Variables

All interface variables are:
```java
public static final
```

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

# Interface Methods Internally

```java
void show();
```

Internally:
```java
public abstract void show();
```

---

# Java 8 Features in Interface

After Java 8:
- default methods
- static methods

allowed in interface.

---

# Default Method Example

```java
interface A {

    default void show() {
        System.out.println("Default Method");
    }
}
```

---

# Static Method Example

```java
interface A {

    static void display() {
        System.out.println("Static Method");
    }
}
```

Call using:
```java
A.display();
```

---

# Java 9 Feature

Private methods allowed in interface.

---

# Abstraction vs Encapsulation

| Abstraction | Encapsulation |
|---|---|
| Hides implementation | Hides data |
| Focus on functionality | Focus on security |
| Achieved using abstract/interface | Achieved using private |

---

# Example

## Abstraction
```java
ATM machine
```

## Encapsulation
```java
Bank account data hidden
```

---

# Advantages of Abstraction

- Reduces complexity
- Improves maintainability
- Increases security
- Provides flexibility
- Supports loose coupling

---

# Disadvantages

- More complex design
- Extra classes/interfaces required

---

# Important Interview Questions

1. What is abstraction?
2. Difference between abstraction and encapsulation?
3. How abstraction achieved in Java?
4. Difference between abstract class and interface?
5. Can abstract class have constructor?
6. Can abstract class have static method?
7. Why abstract class object cannot be created?
8. What is multiple inheritance?
9. Why Java does not support multiple inheritance with classes?
10. What is diamond problem?
11. Difference between extends and implements?
12. Can interface have methods with body?
13. What are default methods?
14. Can interface contain variables?

---

# Abstract Class vs Interface

| Abstract Class | Interface |
|---|---|
| Uses extends | Uses implements |
| Can have normal methods | Mostly abstract methods |
| Can have constructors | No constructor |
| Supports partial abstraction | Full abstraction |
| Single inheritance | Multiple inheritance |

---

# Quick Revision

# Abstract Class
```java
abstract class A {

    abstract void show();
}
```

---

# Interface
```java
interface A {

    void show();
}
```

---

# Final Summary

| Concept | Meaning |
|---|---|
| Abstraction | Hiding implementation details |
| Abstract Class | Incomplete class |
| Abstract Method | Method without body |
| Interface | Full abstraction |
| implements | Used with interface |
| extends | Used with class inheritance |

---

# Final Conclusion

Abstraction helps:
- hide complexity
- expose only essential features
- improve security and maintainability

In Java, abstraction is mainly achieved using:
- abstract classes
- interfaces
