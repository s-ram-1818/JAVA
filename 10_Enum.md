# Enum in Java

# What is Enum?

Enum stands for:
```java
Enumeration
```

Enum is a special type in Java used to represent:
```java
fixed set of constants
```

---

# Real Life Examples

- Days of week
- Months
- Traffic signals
- Directions
- Status values

Because these values are limited and fixed.

---

# Why Use Enum?

Without enum:
```java
String day = "MONDAY";
```

Problem:
- spelling mistakes possible
- invalid values possible

Example:
```java
day = "MONDYA";
```

No compile-time error.

---

# Using Enum

```java
Day day = Day.MONDAY;
```

Only predefined values allowed.

So:
- type safety
- readability
- maintainability

improve.

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

# Important Point

Enum constants are:
```java
public static final
```

by default.

---

# Internal Understanding

```java
MONDAY
```

internally behaves like:
```java
public static final Day MONDAY
```

---

# Enum is a Special Class

Enum internally behaves like a class.

---

# Example

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

# Important Rules

- Enum cannot be instantiated using new
- Enum constants are fixed
- Enum constructors are private by default

---

# Invalid Example

```java
Day d = new Day();
```

Compile-time error.

---

# Why?

Because:
```java
enum objects are created automatically by JVM
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
                System.out.println("Start of week");
                break;

            case TUESDAY:
                System.out.println("Second day");
                break;

            case WEDNESDAY:
                System.out.println("Mid week");
                break;
        }
    }
}
```

## Output
```java
Start of week
```

---

# Enum Methods

Every enum automatically gets useful methods.

---

# Important Enum Methods

| Method | Purpose |
|---|---|
| values() | Returns all constants |
| ordinal() | Returns index |
| valueOf() | Converts string to enum |
| name() | Returns constant name |

---

# values()

Returns array of all enum constants.

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
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY
}

class Main {

    public static void main(String[] args) {

        System.out.println(Day.MONDAY.ordinal());
        System.out.println(Day.TUESDAY.ordinal());
    }
}
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
WEDNESDAY -> index 2
```

---

# name()

Returns enum constant name as String.

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

# Enum Constructor

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

# Why Constructor Called Multiple Times?

Because:
```java
all enum constants are objects
```

Objects created when enum loads.

---

# Important Point

Enum constructors are:
```java
private
```

by default.

---

# Explicit Enum Constructor

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

# Enum with Variables and Methods

Enums can contain:
- variables
- methods
- constructors

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

# Internal Understanding

```java
HP(50000)
```

Means:
```java
create object using constructor
```

---

# Enum and if-else

Enums can be compared safely.

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

Because:
```java
enum constants are singleton objects
```

Only one object exists.

---

# Enum Implements Interfaces

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

# Important Restriction

Enum cannot extend another class.

Because internally:
```java
enum already extends java.lang.Enum
```

---

# Example

```java
enum Demo extends Test
```

Compile-time error.

---

# Internal Inheritance

Every enum internally extends:
```java
java.lang.Enum
```

---

# Enum and Singleton

Enum is best way to create:
```java
Singleton class
```

---

# Example

```java
enum Singleton {

    INSTANCE;
}
```

---

# Why Enum Singleton Better?

Prevents:
- reflection attacks
- serialization issues

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
- harder maintenance

---

# With Enum

```java
enum Day {

    MONDAY
}
```

Safer and cleaner.

---

# Advantages of Enum

- Type safety
- Fixed constants
- Readable code
- Switch support
- Better maintainability

---

# Disadvantages

- Slightly more memory
- Cannot extend class

---

# Important Interview Questions

1. What is enum?
2. Why enums are used?
3. Can enum have constructor?
4. Why enum constructor is private?
5. Can enum extend class?
6. Can enum implement interface?
7. Difference between enum and constants?
8. What does values() do?
9. What is ordinal()?
10. Why == works with enums?
11. Can enum have methods?
12. What is enum singleton?

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
| Enum | Fixed set of constants |
| values() | All constants |
| ordinal() | Index of constant |
| valueOf() | String → Enum |
| name() | Constant name |
| Enum Constructor | Initializes constants |

---

# Final Conclusion

Enums in Java provide:
- fixed constant values
- type safety
- cleaner code
- better readability

Enums are widely used for:
- status values
- configurations
- switch cases
- singleton patterns
