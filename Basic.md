# Java Data Types and Literals - Short Notes

---

# Data Types in Java

A data type defines:
- Type of value variable can store
- Memory size
- Operations allowed

---

# Types of Data Types

1. Primitive Data Types  
2. Non-Primitive Data Types  

---

# Primitive Data Types

These store actual values.

| Data Type | Size | Example |
|---|---|---|
| byte | 1 byte | `byte b = 10;` |
| short | 2 bytes | `short s = 100;` |
| int | 4 bytes | `int a = 500;` |
| long | 8 bytes | `long l = 9999L;` |
| float | 4 bytes | `float f = 5.5f;` |
| double | 8 bytes | `double d = 10.25;` |
| char | 2 bytes | `char ch = 'A';` |
| boolean | JVM dependent | `boolean flag = true;` |

---

# Non-Primitive Data Types

These store references/addresses.

Examples:
- String
- Array
- Class
- Object

Example:

```java
String name = "Ram";

int[] arr = {1,2,3};
```

---

# Primitive vs Non-Primitive

| Primitive | Non-Primitive |
|---|---|
| Stores actual value | Stores reference |
| Fixed size | Dynamic size |
| Faster | Slightly slower |

---

# Type Conversion

## 1. Widening (Automatic)

Small → Large

```java
int x = 10;
double y = x;
```

---

## 2. Narrowing (Manual)

Large → Small

```java
double p = 10.5;
int q = (int)p;
```

---

# Literals in Java

A literal is a fixed value written directly in code.

Example:

```java
int num = 10;
```

Here `10` is literal.

---

# Types of Literals

| Literal Type | Example |
|---|---|
| Integer Literal | `10` |
| Float Literal | `5.5f` |
| Double Literal | `3.14` |
| Character Literal | `'A'` |
| String Literal | `"Java"` |
| Boolean Literal | `true` |
| Null Literal | `null` |

---

# Integer Literal Types

## Decimal

```java
int dec = 10;
```

## Binary

Starts with `0b`

```java
int bin = 0b1010;
```

## Octal

Starts with `0`

```java
int oct = 012;
```

## Hexadecimal

Starts with `0x`

```java
int hex = 0xA;
```

---

# Escape Sequences

| Escape Sequence | Meaning |
|---|---|
| `\n` | New Line |
| `\t` | Tab |
| `\\` | Backslash |
| `\"` | Double Quote |

Example:

```java
System.out.println("Hello\nWorld");
```

---

# Important Interview Points

1. Java has 8 primitive data types

2. `float` requires `f` suffix

3. `double` is default decimal type

4. `char` uses 2 bytes because Java uses Unicode

5. Primitive stores value, non-primitive stores reference

6. `null` cannot be assigned to primitive types

---

# Quick Revision

```text
byte    -> 1 byte
short   -> 2 bytes
int     -> 4 bytes
long    -> 8 bytes

float   -> 4 bytes
double  -> 8 bytes

char    -> 2 bytes
boolean -> true/false

10      -> Integer Literal
5.5f    -> Float Literal
'A'     -> Character Literal
"Java"  -> String Literal
true    -> Boolean Literal
```
