
# Complete Java String Notes

# 1. Introduction to String

## Definition
- A **String** is a sequence of characters.
- In Java, String is an object of `String` class.

```java
String name = "Ram";
````

---

# Package

```java
java.lang.String
```

* Automatically imported.

---

# Important Characteristics

| Feature       | Description                      |
| ------------- | -------------------------------- |
| Immutable     | Cannot be changed after creation |
| Object        | String is a class                |
| Thread Safe   | Because immutable                |
| Stored in SCP | String Constant Pool             |

---

# 2. Ways to Create String

---

## A. String Literal

```java
String s = "Java";
```

### Features

* Stored in String Constant Pool (SCP)
* Memory efficient

---

## B. Using new Keyword

```java
String s = new String("Java");
```

### Features

* Object created in heap memory
* Separate object every time

---

# 3. String Constant Pool (SCP)

* Special area inside heap memory.
* Stores string literals.

Example:

```java
String a = "Java";
String b = "Java";
```

Both point to same object.

---

## Memory Diagram

```text
a -----> "Java" <----- b
```

---

# 4. Why String is Immutable?

## Immutable Meaning

Once created, value cannot be changed.

Example:

```java
String s = "Hello";

s.concat(" World");

System.out.println(s);
```

Output:

```java
Hello
```

---

## Reasons for Immutability

### 1. Security

Used in:

* URL
* Database
* File paths
* Network connections

---

### 2. Thread Safety

Multiple threads can use safely.

---

### 3. Memory Optimization

SCP works because strings are immutable.

---

### 4. Hashcode Caching

Efficient in collections like:

* HashMap
* HashSet

---

# 5. String Methods

---

# length()

Returns number of characters.

```java
String s = "Programming";

System.out.println(s.length());
```

Output:

```java
11
```

---

# charAt(index)

Returns character at given index.

```java
String s = "Java";

System.out.println(s.charAt(2));
```

Output:

```java
v
```

---

# indexOf()

Returns first occurrence index.

```java
String s = "Programming";

System.out.println(s.indexOf('g'));
```

---

# lastIndexOf()

Returns last occurrence index.

```java
String s = "Programming";

System.out.println(s.lastIndexOf('g'));
```

---

# toUpperCase()

```java
String s = "java";

System.out.println(s.toUpperCase());
```

Output:

```java
JAVA
```

---

# toLowerCase()

```java
String s = "JAVA";

System.out.println(s.toLowerCase());
```

---

# trim()

Removes spaces from both sides.

```java
String s = "   Java   ";

System.out.println(s.trim());
```

---

# isEmpty()

Checks if string length is 0.

```java
String s = "";

System.out.println(s.isEmpty());
```

---

# isBlank() (Java 11)

Checks empty or spaces only.

```java
String s = "   ";

System.out.println(s.isBlank());
```

---

# equals()

Compares content.

```java
String a = "Java";
String b = "Java";

System.out.println(a.equals(b));
```

Output:

```java
true
```

---

# equalsIgnoreCase()

Ignores case sensitivity.

```java
String a = "JAVA";
String b = "java";

System.out.println(a.equalsIgnoreCase(b));
```

---

# == vs equals()

## ==

* Compares references

## equals()

* Compares content

Example:

```java
String a = new String("Java");
String b = new String("Java");

System.out.println(a == b);
System.out.println(a.equals(b));
```

Output:

```java
false
true
```

---

# compareTo()

Lexicographical comparison.

```java
String a = "Apple";
String b = "Banana";

System.out.println(a.compareTo(b));
```

---

# compareToIgnoreCase()

Ignores case sensitivity.

---

# contains()

Checks substring exists.

```java
String s = "Java Programming";

System.out.println(s.contains("Java"));
```

---

# startsWith()

```java
String s = "Java";

System.out.println(s.startsWith("Ja"));
```

---

# endsWith()

```java
String s = "Java";

System.out.println(s.endsWith("va"));
```

---

# substring()

Extracts part of string.

```java
String s = "Programming";

System.out.println(s.substring(3));
System.out.println(s.substring(3, 7));
```

Output:

```java
gramming
gram
```

---

# replace()

```java
String s = "Java";

System.out.println(s.replace('a', 'o'));
```

Output:

```java
Jovo
```

---

# replaceAll()

Uses regex.

```java
String s = "abc123";

System.out.println(s.replaceAll("[0-9]", ""));
```

---

# split()

Splits string into array.

```java
String s = "Java,Python,C++";

String[] arr = s.split(",");

for(String x : arr)
{
    System.out.println(x);
}
```

---

# concat()

Joins strings.

```java
String a = "Hello";

System.out.println(a.concat(" World"));
```

---

# valueOf()

Converts data to string.

```java
int n = 10;

String s = String.valueOf(n);
```

---

# join() (Java 8)

```java
String s = String.join("-", "Java", "Python", "C++");

System.out.println(s);
```

Output:

```java
Java-Python-C++
```

---

# repeat() (Java 11)

```java
String s = "Hi ";

System.out.println(s.repeat(3));
```

---

# 6. Escape Characters

| Escape | Meaning      |
| ------ | ------------ |
| \n     | New Line     |
| \t     | Tab          |
| "      | Double Quote |
| '      | Single Quote |
| \      | Backslash    |

Example:

```java
System.out.println("Hello\nWorld");
```

---

# 7. String Concatenation

---

## Using +

```java
String a = "Hello";
String b = "World";

System.out.println(a + " " + b);
```

---

## Using concat()

```java
String a = "Hello";

System.out.println(a.concat(" World"));
```

---

# 8. String Interning

```java
String s1 = new String("Java");
String s2 = s1.intern();
```

* `intern()` moves string to SCP.

---

# 9. StringBuffer

## Definition

Mutable sequence of characters.

```java
StringBuffer sb = new StringBuffer("Java");
```

---

## Features

| Feature      | Value |
| ------------ | ----- |
| Mutable      | Yes   |
| Thread Safe  | Yes   |
| Synchronized | Yes   |

---

## Methods

### append()

```java
sb.append(" Programming");
```

---

### insert()

```java
sb.insert(4, " Language");
```

---

### delete()

```java
sb.delete(1, 3);
```

---

### reverse()

```java
sb.reverse();
```

---

# 10. StringBuilder

## Definition

Mutable character sequence.

```java
StringBuilder sb = new StringBuilder("Java");
```

---

## Features

| Feature     | Value |
| ----------- | ----- |
| Mutable     | Yes   |
| Thread Safe | No    |
| Faster      | Yes   |

---

# String vs StringBuffer vs StringBuilder

| Feature     | String | StringBuffer | StringBuilder |
| ----------- | ------ | ------------ | ------------- |
| Mutable     | No     | Yes          | Yes           |
| Thread Safe | Yes    | Yes          | No            |
| Performance | Slow   | Medium       | Fast          |

---

# 11. Mutable vs Immutable

| Mutable       | Immutable     |
| ------------- | ------------- |
| Can change    | Cannot change |
| StringBuilder | String        |

---

# 12. Common Interview Questions

---

# Why String is Immutable?

* Security
* Thread safety
* SCP optimization
* Hashcode caching

---

# Difference Between == and equals()

| ==                   | equals()           |
| -------------------- | ------------------ |
| Reference comparison | Content comparison |

---

# Difference Between StringBuffer and StringBuilder

| StringBuffer | StringBuilder   |
| ------------ | --------------- |
| Thread Safe  | Not Thread Safe |
| Slower       | Faster          |

---

# What is SCP?

* Special memory area storing string literals.

---

# Why StringBuffer is Thread Safe?

* Methods are synchronized.

---

# What is Interning?

* Storing string into SCP.

---

# 13. Common Programs

---

# Reverse String

```java
String s = "Java";
String rev = "";

for(int i = s.length() - 1; i >= 0; i--)
{
    rev += s.charAt(i);
}

System.out.println(rev);
```

---

# Palindrome String

```java
String s = "madam";
String rev = "";

for(int i = s.length() - 1; i >= 0; i--)
{
    rev += s.charAt(i);
}

if(s.equals(rev))
{
    System.out.println("Palindrome");
}
else
{
    System.out.println("Not Palindrome");
}
```

---

# Count Vowels

```java
String s = "Programming";
int count = 0;

for(int i = 0; i < s.length(); i++)
{
    char ch = Character.toLowerCase(s.charAt(i));

    if(ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u')
    {
        count++;
    }
}

System.out.println(count);
```

---

# Count Words

```java
String s = "Java is powerful";

String[] arr = s.split(" ");

System.out.println(arr.length);
```

---

# Remove Spaces

```java
String s = "J a v a";

System.out.println(s.replace(" ", ""));
```

---

# Frequency of Characters

```java
String s = "programming";

for(char ch = 'a'; ch <= 'z'; ch++)
{
    int count = 0;

    for(int i = 0; i < s.length(); i++)
    {
        if(s.charAt(i) == ch)
        {
            count++;
        }
    }

    if(count > 0)
    {
        System.out.println(ch + " : " + count);
    }
}
```

---

# Anagram Check

```java
import java.util.Arrays;

String a = "listen";
String b = "silent";

char[] x = a.toCharArray();
char[] y = b.toCharArray();

Arrays.sort(x);
Arrays.sort(y);

System.out.println(Arrays.equals(x, y));
```

---

# 14. Important Points to Remember

* String is immutable.
* String objects are stored in SCP.
* Index starts from 0.
* `==` compares references.
* `equals()` compares values.
* StringBuffer is thread-safe.
* StringBuilder is faster.
* Use StringBuilder for frequent modifications.

```
```
