# Nested Classes in Java

# What are Nested Classes?

A class declared inside another class is called:
```java
Nested Class
```

---

# Why Use Nested Classes?

Nested classes are used to:
- logically group classes
- improve readability
- increase security
- access outer class members easily
- reduce unnecessary object creation

---

# Syntax

```java
class Outer {

    class Inner {

    }
}
```

---

# Types of Nested Classes

Java has two main types:

| Type | Description |
|---|---|
| Static Nested Class | Declared using static keyword |
| Inner Class | Non-static nested class |

---

# Types of Inner Classes

| Type | Description |
|---|---|
| Member Inner Class | Normal inner class |
| Local Inner Class | Declared inside method |
| Anonymous Inner Class | Class without name |

---

# Complete Hierarchy

```java
Nested Classes
│
├── Static Nested Class
│
└── Inner Classes
     ├── Member Inner Class
     ├── Local Inner Class
     └── Anonymous Inner Class
```

---

# 1. Member Inner Class

A non-static class declared inside another class.

---

# Example

```java
class Outer {

    int x = 10;

    class Inner {

        void show() {
            System.out.println(x);
        }
    }
}

class Main {

    public static void main(String[] args) {

        Outer obj = new Outer();

        Outer.Inner in = obj.new Inner();

        in.show();
    }
}
```

## Output
```java
10
```

---

# Important Point

Inner class can directly access:
```java
all members of outer class
```

including:
- private members

---

# Example with Private Variable

```java
class Outer {

    private int x = 100;

    class Inner {

        void display() {
            System.out.println(x);
        }
    }
}
```

Valid.

---

# Object Creation Syntax

```java
Outer obj = new Outer();

Outer.Inner in = obj.new Inner();
```

---

# Internal Understanding

Inner class object is connected to:
```java
outer class object
```

So outer object required.

---

# Why?

Because member inner class is:
```java
non-static
```

---

# 2. Static Nested Class

A nested class declared using:
```java
static
```

---

# Syntax

```java
class Outer {

    static class Inner {

    }
}
```

---

# Example

```java
class Outer {

    static int x = 50;

    static class Inner {

        void show() {
            System.out.println(x);
        }
    }
}

class Main {

    public static void main(String[] args) {

        Outer.Inner obj = new Outer.Inner();

        obj.show();
    }
}
```

## Output
```java
50
```

---

# Important Point

Static nested class:
- cannot directly access non-static members
- can access static members directly

---

# Example

```java
class Outer {

    int x = 10;

    static class Inner {

        void show() {

            // System.out.println(x); // ERROR
        }
    }
}
```

---

# Why?

Because:
```java
static class does not depend on outer object
```

---

# Difference Between Member Inner Class and Static Nested Class

| Member Inner Class | Static Nested Class |
|---|---|
| Non-static | Static |
| Needs outer object | No outer object needed |
| Can access all members | Can access only static directly |
| Memory heavy | More memory efficient |

---

# 3. Local Inner Class

A class declared inside a method.

---

# Example

```java
class Outer {

    void display() {

        class Local {

            void show() {
                System.out.println("Local Inner Class");
            }
        }

        Local obj = new Local();

        obj.show();
    }
}

class Main {

    public static void main(String[] args) {

        Outer o = new Outer();

        o.display();
    }
}
```

## Output
```java
Local Inner Class
```

---

# Important Point

Local inner class:
```java
can be used only inside that method
```

---

# Accessing Local Variables

Local inner class can access:
```java
final or effectively final variables
```

---

# Example

```java
class Outer {

    void show() {

        int x = 10;

        class Inner {

            void display() {
                System.out.println(x);
            }
        }

        Inner obj = new Inner();

        obj.display();
    }
}
```

Valid because:
```java
x is effectively final
```

---

# Effectively Final

Variable whose value never changes after initialization.

---

# Invalid Example

```java
int x = 10;

x++;

class Inner {

    void show() {
        System.out.println(x);
    }
}
```

Compile-time error.

---

# Why?

Because local variables stored in stack memory.

Method may finish before inner class uses variable.

So Java copies final/effectively final value safely.

---

# 4. Anonymous Inner Class

Inner class without name.

Used for:
```java
one-time implementation
```

---

# Example

```java
abstract class Animal {

    abstract void sound();
}

class Main {

    public static void main(String[] args) {

        Animal a = new Animal() {

            void sound() {
                System.out.println("Dog Barks");
            }
        };

        a.sound();
    }
}
```

## Output
```java
Dog Barks
```

---

# Internal Understanding

```java
new Animal() {

}
```

Means:
```java
create unnamed child class object
```

---

# Example with Interface

```java
interface Demo {

    void show();
}

class Main {

    public static void main(String[] args) {

        Demo d = new Demo() {

            public void show() {
                System.out.println("Anonymous Class");
            }
        };

        d.show();
    }
}
```

---

# Why Anonymous Class?

Used when:
- implementation needed only once
- avoid creating separate class

---

# Common Use

Used heavily in:
- event handling
- GUI programming
- threading

---

# Example with Thread

```java
class Main {

    public static void main(String[] args) {

        Thread t = new Thread() {

            public void run() {
                System.out.println("Thread Running");
            }
        };

        t.start();
    }
}
```

---

# Advantages of Nested Classes

- Better code organization
- More readable
- Encapsulation
- Increased security
- Easy access to outer members

---

# Disadvantages

- More complex syntax
- Can reduce readability if overused

---

# Memory Understanding

## Member Inner Class

Each inner object stores:
```java
reference of outer object
```

So more memory used.

---

# Static Nested Class

No outer reference stored.

So:
```java
more memory efficient
```

---

# Important Interview Questions

1. What are nested classes?
2. Difference between nested class and inner class?
3. Types of nested classes?
4. Difference between static nested class and member inner class?
5. Why outer object required for inner class?
6. What is local inner class?
7. What is anonymous inner class?
8. Why local variables must be effectively final?
9. Can inner class access private members?
10. Which nested class is memory efficient?

---

# Quick Revision

# Member Inner Class

```java
class Outer {

    class Inner {

    }
}
```

Needs outer object.

---

# Static Nested Class

```java
class Outer {

    static class Inner {

    }
}
```

No outer object needed.

---

# Local Inner Class

```java
void show() {

    class Inner {

    }
}
```

Inside method.

---

# Anonymous Inner Class

```java
new Demo() {

}
```

No class name.

---

# Final Summary Table

| Type | Declared Where | Needs Outer Object |
|---|---|---|
| Member Inner | Inside class | Yes |
| Static Nested | Inside class | No |
| Local Inner | Inside method | Yes |
| Anonymous Inner | Inside expression | Yes |

---

# Final Conclusion

Nested classes help:
- organize related classes
- improve encapsulation
- reduce unnecessary exposure

Java provides:
- static nested classes
- member inner classes
- local inner classes
- anonymous inner classes

for different use cases.
