# Complete Enum Notes in Java

# What is Enum?

Enum stands for:
```java
Enumeration
```

Enum is a special data type in Java used to represent:
```java
fixed set of constants
```

---

# Real Life Examples

- Days of week
- Traffic signals
- Months
- Directions
- Status values

Because these values are predefined and limited.

---

# Why Enum?

Without enum:

```java
String day = "MONDAY";
```

Problems:
- spelling mistakes possible
- invalid values possible
- no type safety

Example:
```java
day = "MONDYA";
```

No compile-time error.

---

# Using Enum

```java
Day d = Day.MONDAY;
```

Only predefined constants allowed.

So:
- safer
- cleaner
- more readable

---

# Syntax

```java
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY
}
```

---

# Creating Enum Variable

```java
Day d = Day.MONDAY;
```

---

# Complete Example

```java
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY
}

class Main {

    public static void main(String[] args) {

        Day d = Day.MONDAY;

        System.out.println(d);
    }
}
```

## Output
```java
MONDAY
```

---

# Important Internal Concept

Enum constants are:
```java
public static final
```

by default.

---

# Internally

```java
MONDAY
```

behaves like:

```java
public static final Day MONDAY
```

---

# Enum is a Special Class

Enum internally behaves like a class.

---

# Internal Representation

```java
enum Day {

    MONDAY,
    TUESDAY
}
```

Internally similar to:

```java
class Day {

    static final Day MONDAY = new Day();
    static final Day TUESDAY = new Day();
}
```

---

# Important Rules of Enum

- Enum cannot be instantiated using new
- Enum constants are fixed
- Enum constructor is private
- Enum cannot extend another class
- Enum can implement interfaces

---

# Invalid Object Creation

```java
Day d = new Day();
```

Compile-time error.

---

# Why?

Because:
```java
JVM automatically creates enum objects
```

---

# Enum and switch Statement

Enums work perfectly with switch.

---

# Example

```java
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY
}

class Main {

    public static void main(String[] args) {

        Day d = Day.MONDAY;

        switch(d) {

            case MONDAY:
                System.out.println("Start");
                break;

            case TUESDAY:
                System.out.println("Second");
                break;

            case WEDNESDAY:
                System.out.println("Middle");
                break;
        }
    }
}
```

## Output
```java
Start
```

---

# Enum Methods

Every enum automatically gets methods from:
```java
java.lang.Enum
```

---

# Important Enum Methods

| Method | Purpose |
|---|---|
| values() | Returns all constants |
| ordinal() | Returns index |
| valueOf() | String → Enum |
| name() | Returns constant name |
| compareTo() | Compare ordinal values |

---

# values()

Returns array of all constants.

---

# Example

```java
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY
}

class Main {

    public static void main(String[] args) {

        Day[] arr = Day.values();

        for(Day d : arr) {
            System.out.println(d);
        }
    }
}
```

## Output
```java
MONDAY
TUESDAY
WEDNESDAY
```

---

# ordinal()

Returns position/index of constant.

Index starts from:
```java
0
```

---

# Example

```java
System.out.println(Day.MONDAY.ordinal());
System.out.println(Day.TUESDAY.ordinal());
```

## Output
```java
0
1
```

---

# Internal Understanding

```java
MONDAY -> index 0
TUESDAY -> index 1
```

---

# name()

Returns constant name as String.

---

# Example

```java
System.out.println(Day.MONDAY.name());
```

## Output
```java
MONDAY
```

---

# valueOf()

Converts String into enum constant.

---

# Example

```java
Day d = Day.valueOf("MONDAY");

System.out.println(d);
```

## Output
```java
MONDAY
```

---

# Invalid valueOf()

```java
Day d = Day.valueOf("FRIDAY");
```

## Result
```java
IllegalArgumentException
```

---

# compareTo()

Compares ordinal values.

---

# Example

```java
System.out.println(
    Day.MONDAY.compareTo(Day.TUESDAY)
);
```

## Output
```java
-1
```

---

# Why?

Because:
```java
MONDAY ordinal = 0
TUESDAY ordinal = 1
```

So:
```java
0 - 1 = -1
```

---

# Enum Constructor

# Can Enum Have Constructor?

## YES

Enums can have constructors.

---

# Example

```java
enum Laptop {

    HP,
    DELL,
    LENOVO;

    Laptop() {
        System.out.println("Constructor Called");
    }
}

class Main {

    public static void main(String[] args) {

        Laptop l = Laptop.HP;
    }
}
```

## Output
```java
Constructor Called
Constructor Called
Constructor Called
```

---

# Why Constructor Called 3 Times?

Because:
```java
HP, DELL, LENOVO
```

all are objects.

Each constant calls constructor once.

---

# Important Internal Concept

```java
HP,
DELL,
LENOVO
```

internally behaves like:

```java
new Laptop();
new Laptop();
new Laptop();
```

---

# Important Rule

Enum constructors are:
```java
private
```

by default.

---

# Why Private?

To prevent object creation outside enum.

Because enum objects should remain fixed.

---

# Explicit Private Constructor

```java
enum Demo {

    A;

    private Demo() {

    }
}
```

Valid.

---

# Public Constructor Not Allowed

```java
enum Demo {

    A;

    public Demo() {

    }
}
```

Compile-time error.

---

# Why Public Constructor Not Allowed?

Because:
```java
new object creation must not happen
```

outside enum.

---

# Enum with Variables

Enums can have instance variables.

---

# Example

```java
enum Laptop {

    HP(50000),
    DELL(60000),
    LENOVO(70000);

    int price;

    Laptop(int price) {
        this.price = price;
    }
}
```

---

# Internal Understanding

```java
HP(50000)
```

means:

```java
new Laptop(50000)
```

---

# Accessing Enum Variables

```java
class Main {

    public static void main(String[] args) {

        System.out.println(Laptop.HP.price);
    }
}
```

## Output
```java
50000
```

---

# Enum with Methods

Enums can contain methods.

---

# Example

```java
enum Laptop {

    HP(50000),
    DELL(60000);

    int price;

    Laptop(int price) {
        this.price = price;
    }

    void display() {
        System.out.println(price);
    }
}

class Main {

    public static void main(String[] args) {

        Laptop.HP.display();
    }
}
```

## Output
```java
50000
```

---

# Enum and if-else

Enums can be safely compared using:
```java
==
```

---

# Example

```java
Day d = Day.MONDAY;

if(d == Day.MONDAY) {
    System.out.println("Correct");
}
```

---

# Why == Works?

Because enum constants are:
```java
singleton objects
```

Only one object exists for each constant.

---

# Enum Implements Interface

Enums can implement interfaces.

---

# Example

```java
interface Demo {

    void show();
}

enum Test implements Demo {

    A;

    public void show() {
        System.out.println("Show");
    }
}
```

---

# Enum Cannot Extend Class

---

# Example

```java
enum Test extends A
```

Compile-time error.

---

# Why?

Because every enum already extends:
```java
java.lang.Enum
```

Java does not support multiple inheritance.

---

# Internal Inheritance

```java
enum Day
```

internally becomes:

```java
class Day extends Enum
```

---

# Enum Singleton

Best way to create singleton class.

---

# Example

```java
enum Singleton {

    INSTANCE;
}
```

---

# Why Enum Singleton is Best?

Prevents:
- reflection attack
- serialization issue
- multiple object creation

---

# Enum vs Constants

## Without Enum

```java
class Day {

    static final int MONDAY = 1;
}
```

Problems:
- no type safety
- difficult maintenance

---

# With Enum

```java
enum Day {

    MONDAY
}
```

Better and safer.

---

# Advantages of Enum

- Type safety
- Fixed constants
- Cleaner code
- Better readability
- Switch support
- Singleton support

---

# Disadvantages

- Slight memory overhead
- Cannot extend another class

---

# Important Interview Questions

1. What is enum?
2. Why enums are used?
3. Can enum have constructor?
4. Why enum constructor is private?
5. Can enum extend class?
6. Can enum implement interface?
7. What is ordinal()?
8. Difference between enum and constants?
9. Why == works with enum?
10. Can enum have variables and methods?
11. What is enum singleton?
12. Why enum object creation not allowed?

---

# Quick Revision

# Enum Declaration

```java
enum Day {

    MONDAY,
    TUESDAY
}
```

---

# Enum Constructor

```java
Laptop(int price) {

}
```

---

# values()

```java
Day.values();
```

Returns all constants.

---

# ordinal()

```java
Day.MONDAY.ordinal();
```

Returns index.

---

# valueOf()

```java
Day.valueOf("MONDAY");
```

String → Enum.

---

# name()

```java
Day.MONDAY.name();
```

Returns constant name.

---

# Final Summary Table

| Concept | Meaning |
|---|---|
| Enum | Fixed constants |
| values() | All constants |
| ordinal() | Index |
| valueOf() | String → Enum |
| name() | Constant name |
| Enum Constructor | Initializes constants |
| Enum Variable | Data inside enum |
| Enum Method | Behavior inside enum |

---

# Final Conclusion

Enums in Java are powerful because they:
- represent fixed constants safely
- improve readability
- reduce bugs
- support methods, constructors, variables
- work like special classes

Enums are widely used in:
- status handling
- configurations
- switch cases
- singleton design patterns
