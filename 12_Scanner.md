# Taking Input in Java

# Why Input is Needed?

Input allows user to:
```java
enter data during program execution
```

Example:
- name
- age
- marks
- numbers

---

# Ways to Take Input in Java

Java provides multiple ways:

| Method | Package |
|---|---|
| Scanner | java.util |
| BufferedReader | java.io |
| Console | java.io |
| Command Line Arguments | JVM arguments |

---

# Most Common Method

```java
Scanner
```

because:
- easy to use
- beginner friendly

---

# 1. Scanner Class

# What is Scanner?

Scanner is a class used to:
```java
take input from user
```

---

# Package

```java
import java.util.Scanner;
```

---

# Creating Scanner Object

```java
Scanner sc = new Scanner(System.in);
```

---

# Internal Understanding

## Scanner
Class name.

## sc
Reference variable.

## new Scanner()
Creates object.

## System.in
Input stream connected to keyboard.

---

# Complete Example

```java
import java.util.Scanner;

class Main {

    public static void main(String[] args) {

        Scanner sc =
            new Scanner(System.in);

        System.out.println(
            "Enter Number:"
        );

        int x = sc.nextInt();

        System.out.println(x);
    }
}
```

---

# Flow of Program

1. Scanner object created
2. Program waits for input
3. User enters value
4. nextInt() reads integer
5. Value stored in variable

---

# Scanner Methods

| Method | Input Type |
|---|---|
| nextInt() | int |
| nextLong() | long |
| nextFloat() | float |
| nextDouble() | double |
| next() | single word |
| nextLine() | complete line |
| nextBoolean() | boolean |
| nextByte() | byte |
| nextShort() | short |

---

# Taking Integer Input

```java
int x = sc.nextInt();
```

---

# Example

```java
import java.util.Scanner;

class Main {

    public static void main(String[] args) {

        Scanner sc =
            new Scanner(System.in);

        int age = sc.nextInt();

        System.out.println(age);
    }
}
```

---

# Taking Double Input

```java
double d = sc.nextDouble();
```

---

# Taking Float Input

```java
float f = sc.nextFloat();
```

---

# Taking Long Input

```java
long l = sc.nextLong();
```

---

# Taking Boolean Input

```java
boolean b = sc.nextBoolean();
```

Input:
```java
true
false
```

---

# Taking Single Word Input

```java
String s = sc.next();
```

---

# Example

```java
Scanner sc =
    new Scanner(System.in);

String name = sc.next();

System.out.println(name);
```

Input:
```java
Ram
```

---

# Important Point

```java
next()
```

reads:
```java
only one word
```

Stops at:
- space
- tab
- newline

---

# Example

Input:
```java
Ram Kumar
```

Code:
```java
String s = sc.next();
```

Output:
```java
Ram
```

---

# Taking Full Line Input

```java
String s = sc.nextLine();
```

---

# Example

```java
Scanner sc =
    new Scanner(System.in);

String s = sc.nextLine();

System.out.println(s);
```

Input:
```java
Ram Kumar
```

Output:
```java
Ram Kumar
```

---

# Difference Between next() and nextLine()

| next() | nextLine() |
|---|---|
| Reads one word | Reads complete line |
| Stops at space | Reads spaces also |

---

# Important Scanner Problem

# Problem with nextLine()

---

# Example

```java
Scanner sc =
    new Scanner(System.in);

int x = sc.nextInt();

String s = sc.nextLine();

System.out.println(s);
```

---

# Why Problem Happens?

After:
```java
nextInt()
```

newline character:
```java
\n
```

remains in buffer.

Then:
```java
nextLine()
```

reads leftover newline.

---

# Solution

Add extra:
```java
sc.nextLine();
```

---

# Correct Example

```java
Scanner sc =
    new Scanner(System.in);

int x = sc.nextInt();

sc.nextLine();

String s = sc.nextLine();

System.out.println(s);
```

---

# Taking Character Input

Scanner has NO:
```java
nextChar()
```

method.

---

# Solution

Use:
```java
char ch =
    sc.next().charAt(0);
```

---

# Example

```java
Scanner sc =
    new Scanner(System.in);

char ch =
    sc.next().charAt(0);

System.out.println(ch);
```

---

# Internal Understanding

```java
sc.next()
```

returns String.

Then:
```java
charAt(0)
```

returns first character.

---

# Taking Array Input

---

# Example

```java
import java.util.Scanner;

class Main {

    public static void main(String[] args) {

        Scanner sc =
            new Scanner(System.in);

        int n = sc.nextInt();

        int[] arr = new int[n];

        for(int i = 0; i < n; i++) {

            arr[i] = sc.nextInt();
        }

        for(int x : arr) {

            System.out.print(x + " ");
        }
    }
}
```

---

# Taking 2D Array Input

---

# Example

```java
Scanner sc =
    new Scanner(System.in);

int r = sc.nextInt();
int c = sc.nextInt();

int[][] arr =
    new int[r][c];

for(int i = 0; i < r; i++) {

    for(int j = 0; j < c; j++) {

        arr[i][j] =
            sc.nextInt();
    }
}
```

---

# Closing Scanner

```java
sc.close();
```

---

# Why close() Used?

Releases system resources.

---

# Example

```java
Scanner sc =
    new Scanner(System.in);

int x = sc.nextInt();

sc.close();
```

---

# Important Point

Do NOT close Scanner frequently when using:
```java
System.in
```

especially in competitive programming.

---

# InputMismatchException

Occurs when wrong type entered.

---

# Example

```java
int x = sc.nextInt();
```

Input:
```java
abc
```

## Output
```java
InputMismatchException
```

---

# Why?

Because:
```java
abc is not integer
```

---

# 2. BufferedReader

# What is BufferedReader?

Used for:
```java
fast input
```

Especially useful in:
- competitive programming
- large input

---

# Package

```java
import java.io.*;
```

---

# Creating Object

```java
BufferedReader br =
    new BufferedReader(
        new InputStreamReader(
            System.in
        )
    );
```

---

# Example

```java
import java.io.*;

class Main {

    public static void main(String[] args)
        throws Exception {

        BufferedReader br =
            new BufferedReader(
                new InputStreamReader(
                    System.in
                )
            );

        String s = br.readLine();

        System.out.println(s);
    }
}
```

---

# Important Point

```java
readLine()
```

always returns:
```java
String
```

---

# Converting to Integer

```java
int x =
    Integer.parseInt(
        br.readLine()
    );
```

---

# Why BufferedReader Faster?

Because:
```java
Scanner uses parsing internally
```

BufferedReader reads raw text faster.

---

# Difference Between Scanner and BufferedReader

| Scanner | BufferedReader |
|---|---|
| Slow | Fast |
| Easy syntax | Complex syntax |
| Parses automatically | Manual conversion |
| Beginner friendly | Competitive programming |

---

# 3. Console Class

Used mainly for:
```java
password input
```

---

# Example

```java
Console c = System.console();
```

---

# Important Point

Usually not supported in IDEs.

Works mainly in terminal.

---

# 4. Command Line Arguments

Input passed while running program.

---

# Example

```java
class Main {

    public static void main(String[] args) {

        System.out.println(args[0]);
    }
}
```

Run:
```java
java Main Ram
```

Output:
```java
Ram
```

---

# Type Conversion in Input

---

# String to int

```java
int x =
    Integer.parseInt("10");
```

---

# String to double

```java
double d =
    Double.parseDouble("3.14");
```

---

# Important Interview Questions

1. What is Scanner class?
2. Difference between next() and nextLine()?
3. Why nextLine() issue occurs after nextInt()?
4. Difference between Scanner and BufferedReader?
5. Why BufferedReader faster?
6. How to take char input?
7. What is InputMismatchException?
8. Why close() used?
9. What is System.in?
10. How command line arguments work?

---

# Quick Revision

# Scanner Object

```java
Scanner sc =
    new Scanner(System.in);
```

---

# Integer Input

```java
int x = sc.nextInt();
```

---

# String Input

```java
String s = sc.next();
```

---

# Full Line Input

```java
String s = sc.nextLine();
```

---

# Character Input

```java
char ch =
    sc.next().charAt(0);
```

---

# BufferedReader

```java
BufferedReader br =
    new BufferedReader(
        new InputStreamReader(
            System.in
        )
    );
```

---

# Final Summary Table

| Method | Purpose |
|---|---|
| nextInt() | int input |
| next() | one word |
| nextLine() | full line |
| charAt(0) | char input |
| readLine() | BufferedReader input |

---

# Final Conclusion

Java provides multiple ways to take input:
- Scanner
- BufferedReader
- Console
- Command line arguments

Most beginners use:
```java
Scanner
```

while competitive programmers prefer:
```java
BufferedReader
```

because of better performance.
