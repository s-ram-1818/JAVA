
# Final Keyword in Java

## What is `final` in Java?
`final` is a keyword in Java used to restrict modification.

It can be used with:
1. Variable
2. Method
3. Class

---

# 1. Final Variable

A final variable cannot be changed once assigned.

## Syntax
```java
final int x = 10;
````

## Example

```java
class Demo {
    public static void main(String[] args) {

        final int x = 10;

        // x = 20; // ERROR

        System.out.println(x);
    }
}
```

## Important Points

* Value can be assigned only once.
* Acts like a constant.
* Convention: constant names are written in UPPER_CASE.

## Example

```java
final double PI = 3.14;
```

---

# Blank Final Variable

A final variable declared but not initialized immediately.

It must be initialized before constructor ends.

## Example

```java
class Student {

    final int rollNo;

    Student(int r) {
        rollNo = r;
    }

    void display() {
        System.out.println(rollNo);
    }

    public static void main(String[] args) {

        Student s = new Student(101);
        s.display();
    }
}
```

---

# Final Reference Variable

If reference is final:

* Reference cannot point to another object.
* But object data can still change.

## Example

```java
class Test {

    int x = 10;

    public static void main(String[] args) {

        final Test t = new Test();

        t.x = 20; // allowed

        // t = new Test(); // ERROR

        System.out.println(t.x);
    }
}
```

## Important

* Object becomes mutable.
* Only reference becomes fixed.

---

# 2. Final Method

A final method cannot be overridden.

## Example

```java
class Parent {

    final void show() {
        System.out.println("Parent show");
    }
}

class Child extends Parent {

    // void show() {} // ERROR
}
```

## Why use final method?

* To prevent overriding.
* For security.
* To keep original implementation unchanged.

---

# 3. Final Class

A final class cannot be inherited.

## Example

```java
final class Animal {

    void sound() {
        System.out.println("Animal Sound");
    }
}

// class Dog extends Animal {} // ERROR
```

## Real Example

```java
String
```

`String` class is final in Java.

## Why String is final?

* Security
* Immutability
* Performance

---

# Final vs Finally vs Finalize

| Keyword    | Purpose                                 |
| ---------- | --------------------------------------- |
| final      | Restrict modification                   |
| finally    | Block used in exception handling        |
| finalize() | Method called before garbage collection |

---

# Important Interview Points

## Can final variable be initialized later?

Yes, using:

* Constructor
* Static block

---

# Final Static Variable

Used to create constants.

## Example

```java
class Demo {

    static final int MAX = 100;

    public static void main(String[] args) {
        System.out.println(MAX);
    }
}
```

---

# Final Parameter

A method parameter declared final cannot be modified.

## Example

```java
class Demo {

    void display(final int x) {

        // x = 20; // ERROR

        System.out.println(x);
    }
}
```

---

# Final and Constructors

Constructors cannot be final because:

* Constructors are not inherited.
* Overriding constructors is impossible.

---

# Memory Related Notes

## final Primitive Variable

* Value stored cannot change.

## final Reference Variable

* Reference stored in stack cannot change.
* Object in heap can still change.

---

# Advantages of final

* Prevents unwanted modification
* Provides security
* Helps create immutable classes
* Improves readability
* Used for constants

---

# Disadvantages

* Reduces flexibility
* Cannot override/inherit when needed

---

# Quick Revision

## Final Variable

```java
final int x = 10;
```

Cannot change value.

---

## Final Method

```java
final void show(){}
```

Cannot override.

---

## Final Class

```java
final class A{}
```

Cannot inherit.

---

# Output Based Question

## Question 1

```java
class Test {

    final int x = 10;

    public static void main(String[] args) {

        Test t = new Test();

        // t.x = 20;

        System.out.println(t.x);
    }
}
```

## Output

```java
10
```

---

## Question 2

```java
final class A {}

// class B extends A {}
```

## Result

```java
Compile Time Error
```

---

# Key Interview Questions

1. What is final keyword in Java?
2. Difference between final, finally, finalize?
3. Can final variable be changed?
4. Can final class be inherited?
5. Can constructors be final?
6. Why is String final?
7. Difference between final variable and final reference variable?
8. Can final method be overloaded?
   → YES

---

# Important Point

## final method CAN be overloaded

Because overloading is different from overriding.

## Example

```java
class Demo {

    final void show() {
        System.out.println("A");
    }

    void show(int x) {
        System.out.println(x);
    }
}
```

---

# Summary

| Used With | Meaning             |
| --------- | ------------------- |
| Variable  | Cannot change value |
| Method    | Cannot override     |
| Class     | Cannot inherit      |

```
```
