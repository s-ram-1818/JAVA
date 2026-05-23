# Java Data Types, Literals, Type Conversion & Casting - Complete Notes

---

# Data Types in Java

## Definition
A data type defines:
- Type of value a variable can store
- Memory allocated to variable
- Operations that can be performed

---

# Types of Data Types

```text
1. Primitive Data Types
2. Non-Primitive (Reference) Data Types
```

---

# 1. Primitive Data Types

Primitive data types store actual values.

Java has 8 primitive data types.

| Data Type | Size | Range | Default Value | Wrapper Class |
|---|---|---|---|---|
| byte | 1 byte | -128 to 127 | 0 | Byte |
| short | 2 bytes | -32,768 to 32,767 | 0 | Short |
| int | 4 bytes | -2^31 to 2^31-1 | 0 | Integer |
| long | 8 bytes | Very Large Integer | 0L | Long |
| float | 4 bytes | Decimal | 0.0f | Float |
| double | 8 bytes | Decimal | 0.0d | Double |
| char | 2 bytes | Unicode Character | '\u0000' | Character |
| boolean | JVM dependent | true/false | false | Boolean |

---

# Integer Data Types

## byte

```java
byte age = 25;
```

Range:

```text
-128 to 127
```

---

## short

```java
short salary = 20000;
```

---

## int

Most commonly used integer type.

```java
int marks = 95;
```

---

## long

Used for very large values.

Must end with `L`.

```java
long population = 8000000000L;
```

---

# Floating Point Data Types

## float

- Less precision
- Must end with `f`

```java
float price = 99.5f;
```

---

## double

- More precision
- Default decimal type

```java
double pi = 3.14159;
```

---

# Character Data Type

## char

Stores single character.

```java
char grade = 'A';
```

ASCII example:

```java
char ch = 65;
System.out.println(ch);
```

Output:

```text
A
```

---

# Boolean Data Type

## boolean

Stores:
- true
- false

```java
boolean isJavaEasy = true;
```

---

# Why char Uses 2 Bytes?

Because Java uses Unicode character set.

---

# 2. Non-Primitive Data Types

Store references/addresses.

Examples:
- String
- Array
- Class
- Object
- Interface

---

# String Example

```java
String name = "Ram";
```

---

# Array Example

```java
int[] arr = {1,2,3};
```

---

# Primitive vs Non-Primitive

| Primitive | Non-Primitive |
|---|---|
| Stores actual value | Stores reference |
| Fixed size | Dynamic size |
| Faster | Slightly slower |
| Stored in stack | Objects stored in heap |

---

# Memory Allocation

| Memory Area | Stored Data |
|---|---|
| Stack Memory | Primitive variables & references |
| Heap Memory | Objects & arrays |

---

# Literals in Java

## Definition

A literal is a fixed value directly written in code.

Example:

```java
int x = 10;
```

Here `10` is literal.

---

# Types of Literals

```text
1. Integer Literals
2. Floating-Point Literals
3. Character Literals
4. String Literals
5. Boolean Literals
6. Null Literal
```

---

# Integer Literals

```java
int a = 100;
```

---

# Types of Integer Literals

## Decimal Literal

```java
int a = 25;
```

---

## Binary Literal

Starts with `0b`

```java
int b = 0b1010;
```

---

## Octal Literal

Starts with `0`

```java
int c = 012;
```

---

## Hexadecimal Literal

Starts with `0x`

```java
int d = 0xA;
```

---

# Underscore in Numeric Literals

Improves readability.

```java
int amount = 1_00_000;
```

---

# Floating-Point Literals

## float Literal

```java
float f = 5.5f;
```

---

## double Literal

```java
double d = 10.25;
```

---

# Scientific Notation

```java
double num = 1.2e3;
```

Output:

```text
1200.0
```

---

# Character Literals

```java
char ch = 'A';
```

---

# Escape Sequences

| Escape Sequence | Meaning |
|---|---|
| `\n` | New Line |
| `\t` | Tab |
| `\\` | Backslash |
| `\'` | Single Quote |
| `\"` | Double Quote |
| `\b` | Backspace |
| `\r` | Carriage Return |

Example:

```java
System.out.println("Hello\nWorld");
```

---

# Unicode Character Literal

```java
char ch = '\u0041';
```

Output:

```text
A
```

---

# String Literals

```java
String name = "Java";
```

Important:
- String literals are objects
- Stored in String Constant Pool

---

# String Constant Pool (SCP)

Special heap memory area storing string literals.

```java
String s1 = "Java";
String s2 = "Java";
```

Both references point to same object.

---

# Boolean Literals

```java
boolean isPass = true;
```

---

# Null Literal

```java
String s = null;
```

Important:
- Only for reference variables
- Cannot assign to primitive types

---

# Default Values of Primitive Types

| Data Type | Default Value |
|---|---|
| byte | 0 |
| short | 0 |
| int | 0 |
| long | 0L |
| float | 0.0f |
| double | 0.0d |
| char | '\u0000' |
| boolean | false |

---

# Wrapper Classes

| Primitive | Wrapper Class |
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

# Autoboxing

Primitive → Object

```java
int a = 10;
Integer obj = a;
```

---

# Unboxing

Object → Primitive

```java
Integer obj = 20;
int x = obj;
```

---

# Type Conversion in Java

## Definition

Converting one data type into another data type.

Two types:
1. Implicit Conversion
2. Explicit Conversion

---

# 1. Implicit Type Conversion

Also called:
- Automatic Conversion
- Widening Casting

Small data type automatically converts into larger data type.

```java
int a = 10;
double d = a;
```

Output:

```text
10.0
```

---

# Widening Casting Flow

```text
byte → short → int → long → float → double
                  ↑
                char
```

---

# Features of Widening Casting

- Automatic
- Safe conversion
- No data loss

---

# Example of Widening Casting

```java
byte b = 10;
int a = b;

System.out.println(a);
```

---

# 2. Explicit Type Conversion

Also called:
- Manual Conversion
- Narrowing Casting

Larger data type converts into smaller data type manually.

---

# Narrowing Casting Example

```java
double d = 10.5;
int a = (int)d;

System.out.println(a);
```

Output:

```text
10
```

---

# Features of Narrowing Casting

- Manual conversion
- Possible data loss
- Not completely safe

---

# Narrowing Casting Flow

```text
double → float → long → int → short → byte
```

---

# Another Example

```java
int x = 130;
byte b = (byte)x;

System.out.println(b);
```

Output:

```text
-126
```

Reason:
Overflow occurs because byte range is only -128 to 127.

---

# Type Promotion in Expressions

Small data types automatically convert into int during arithmetic operations.

```java
byte a = 10;
byte b = 20;

int c = a + b;
```

---

# char Type Conversion

```java
char ch = 'A';
int x = ch;

System.out.println(x);
```

Output:

```text
65
```

---

# Explicit char Conversion

```java
int x = 66;
char ch = (char)x;

System.out.println(ch);
```

Output:

```text
B
```

---

# Important Interview Questions

## Q1. How many primitive data types are there in Java?

8 primitive data types.

---

## Q2. Difference between float and double?

| float | double |
|---|---|
| 4 bytes | 8 bytes |
| Less precision | More precision |
| Requires `f` | Default decimal type |

---

## Q3. Why char uses 2 bytes?

Because Java uses Unicode.

---

## Q4. Difference between primitive and non-primitive?

Primitive stores actual value.  
Non-primitive stores reference.

---

## Q5. Can null be assigned to primitive types?

No.

---

## Q6. Difference between widening and narrowing casting?

| Widening | Narrowing |
|---|---|
| Small → Large | Large → Small |
| Automatic | Manual |
| No data loss | Possible data loss |

---

## Q7. What is type casting?

Converting one data type into another.

---

## Q8. What is type promotion?

Smaller data types convert into int during expressions.

---

## Q9. What is autoboxing?

Primitive → Wrapper object conversion.

---

## Q10. What is unboxing?

Wrapper object → Primitive conversion.

---

# Quick Revision Sheet

```text
PRIMITIVE TYPES

byte    -> 1 byte
short   -> 2 bytes
int     -> 4 bytes
long    -> 8 bytes

float   -> 4 bytes
double  -> 8 bytes

char    -> 2 bytes
boolean -> true/false

--------------------------------

LITERALS

10      -> Integer Literal
5.5f    -> Float Literal
3.14    -> Double Literal
'A'     -> Character Literal
"Java"  -> String Literal
true    -> Boolean Literal
null    -> Null Literal

--------------------------------

TYPE CONVERSION

Widening:
int -> double

Narrowing:
double -> int

--------------------------------

CASTING FLOW

byte -> short -> int -> long -> float -> double
                  ↑
                char

--------------------------------

MEMORY

Stack -> Primitive variables & references
Heap  -> Objects & arrays
```
