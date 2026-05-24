# Complete Exception Handling Notes in Java

# What is Exception?

An exception is:
```java
an unwanted event that occurs during program execution
```

It interrupts:
```java
normal flow of the program
```

---

# Example

```java
int x = 10 / 0;
```

## Output
```java
ArithmeticException
```

Because:
```java
division by zero is not possible
```

---

# Why Exception Handling Needed?

Without exception handling:
```java
program terminates abnormally
```

With exception handling:
- program continues safely
- errors are handled properly
- application becomes robust

---

# Exception Hierarchy

```java
Object
   |
Throwable
   |
--------------------------------
|                              |
Error                      Exception
                                  |
                   --------------------------------
                   |                              |
        Checked Exception             RuntimeException
                                                |
                                   Unchecked Exceptions
```

---

# Throwable Class

Parent class of:
- Exception
- Error

---

# Difference Between Error and Exception

| Error | Exception |
|---|---|
| Serious problem | Recoverable problem |
| JVM related | Application related |
| Hard to recover | Can be handled |

---

# Examples of Error

```java
StackOverflowError
OutOfMemoryError
```

---

# Examples of Exception

```java
ArithmeticException
IOException
NullPointerException
```

---

# Types of Exceptions

Java exceptions are mainly divided into:
1. Checked Exceptions
2. Unchecked Exceptions

---

# 1. Checked Exceptions

# Definition

Exceptions checked by compiler during:
```java
compile time
```

are called:
```java
Checked Exceptions
```

---

# Important Rule

Checked exceptions must be:
- handled using try-catch
OR
- declared using throws

---

# Why Called Checked?

Because:
```java
compiler checks them
```

before execution.

---

# Parent Class

Checked exceptions are children of:
```java
Exception
```

but NOT children of:
```java
RuntimeException
```

---

# Examples

| Exception | Cause |
|---|---|
| IOException | File problem |
| SQLException | Database issue |
| FileNotFoundException | File missing |
| ClassNotFoundException | Class missing |

---

# Example Without Handling

```java
import java.io.*;

class Main {

    public static void main(String[] args) {

        FileReader fr =
            new FileReader("abc.txt");
    }
}
```

## Result
```java
Compile-time Error
```

---

# Why Error?

Because:
```java
file may not exist
```

Compiler forces handling.

---

# Handling Checked Exception

```java
import java.io.*;

class Main {

    public static void main(String[] args) {

        try {

            FileReader fr =
                new FileReader(
                    "abc.txt"
                );
        }

        catch(IOException e) {

            System.out.println(
                "File Not Found"
            );
        }
    }
}
```

---

# 2. Unchecked Exceptions

# Definition

Exceptions checked during:
```java
runtime
```

are called:
```java
Unchecked Exceptions
```

---

# Important Point

Compiler does NOT force handling.

---

# Parent Class

Unchecked exceptions are children of:
```java
RuntimeException
```

---

# Examples

| Exception | Cause |
|---|---|
| ArithmeticException | Divide by zero |
| NullPointerException | Null reference |
| ArrayIndexOutOfBoundsException | Invalid array index |
| NumberFormatException | Invalid conversion |

---

# Example

```java
int x = 10 / 0;
```

## Output
```java
ArithmeticException
```

---

# Why?

Because:
```java
division by zero not possible
```

---

# Example

```java
String s = null;

System.out.println(s.length());
```

## Output
```java
NullPointerException
```

---

# Why?

Because:
```java
null has no methods
```

---

# Difference Between Checked and Unchecked Exceptions

| Checked Exception | Unchecked Exception |
|---|---|
| Compile-time checked | Runtime checked |
| Handling mandatory | Handling optional |
| Child of Exception | Child of RuntimeException |
| Recoverable | Mostly coding mistakes |

---

# Exception Handling Keywords

| Keyword | Purpose |
|---|---|
| try | Risky code |
| catch | Handle exception |
| finally | Always executes |
| throw | Manually throw exception |
| throws | Declare exception |

---

# try Block

Contains:
```java
risky code
```

---

# Syntax

```java
try {

}
```

---

# Example

```java
try {

    int x = 10 / 0;
}
```

---

# catch Block

Handles exceptions.

---

# Syntax

```java
catch(ExceptionType e) {

}
```

---

# Example

```java
class Main {

    public static void main(String[] args) {

        try {

            int x = 10 / 0;
        }

        catch(ArithmeticException e) {

            System.out.println(
                "Cannot divide by zero"
            );
        }
    }
}
```

## Output
```java
Cannot divide by zero
```

---

# Internal Flow

1. Exception occurs
2. JVM creates exception object
3. JVM searches matching catch block
4. catch block executes
5. Program continues

---

# Important Rule

```java
try must be followed by:
catch OR finally
```

---

# Multiple catch Blocks

---

# Example

```java
try {

    int[] arr = {1,2};

    System.out.println(arr[5]);
}

catch(ArrayIndexOutOfBoundsException e) {

    System.out.println("Array Error");
}

catch(Exception e) {

    System.out.println("General Error");
}
```

## Output
```java
Array Error
```

---

# Why Second catch Not Execute?

Because:
```java
once exception handled,
remaining catch blocks skip
```

---

# Generic catch Block

```java
catch(Exception e)
```

handles all exceptions.

---

# Example

```java
try {

    int x = 10 / 0;
}

catch(Exception e) {

    System.out.println(e);
}
```

---

# Exception Object Methods

| Method | Purpose |
|---|---|
| getMessage() | Returns message |
| toString() | Type + message |
| printStackTrace() | Full error details |

---

# Example

```java
try {

    int x = 10 / 0;
}

catch(Exception e) {

    System.out.println(
        e.getMessage()
    );

    System.out.println(e);

    e.printStackTrace();
}
```

---

# finally Block

Block that:
```java
always executes
```

whether exception occurs or not.

---

# Why finally Used?

Used for:
- closing files
- database closing
- cleanup code
- releasing resources

---

# Example

```java
try {

    int x = 10 / 0;
}

catch(Exception e) {

    System.out.println("Handled");
}

finally {

    System.out.println("Finally");
}
```

## Output
```java
Handled
Finally
```

---

# finally Without Exception

```java
try {

    System.out.println("Try");
}

finally {

    System.out.println("Finally");
}
```

---

# When finally May Not Execute?

- JVM shutdown
- System.exit()
- power failure

---

# throw Keyword

Used to:
```java
manually throw exception
```

---

# Syntax

```java
throw new ExceptionType();
```

---

# Example

```java
throw new ArithmeticException(
    "Invalid"
);
```

---

# Complete Example

```java
class Main {

    public static void main(String[] args) {

        int age = 15;

        if(age < 18) {

            throw new ArithmeticException(
                "Not Eligible"
            );
        }
    }
}
```

---

# Internal Flow of throw

1. Exception object created
2. JVM receives object
3. Normal flow stops
4. JVM searches catch block

---

# Important Point

After:
```java
throw
```

remaining code generally does not execute.

---

# throws Keyword

Used to:
```java
declare exception
```

---

# Syntax

```java
returnType method()
    throws ExceptionType
```

---

# Example

```java
import java.io.*;

class Main {

    static void readFile()
        throws IOException {

        FileReader fr =
            new FileReader("abc.txt");
    }
}
```

---

# Internal Understanding

```java
throws IOException
```

means:
```java
this method may generate IOException
```

Caller must handle it.

---

# Multiple Exceptions

```java
void test()
throws IOException,
       SQLException {

}
```

---

# Difference Between throw and throws

| throw | throws |
|---|---|
| Used inside method | Used in method declaration |
| Throws manually | Declares exception |
| Followed by object | Followed by class name |

---

# Custom Exception

# What is Custom Exception?

User-defined exception.

---

# Why Create Custom Exception?

Used for:
- invalid age
- invalid salary
- invalid account

business validations.

---

# Creating Custom Exception

Extend:
```java
Exception
```

for checked exception.

---

# Example

```java
class InvalidAgeException
    extends Exception {

    InvalidAgeException(String msg) {

        super(msg);
    }
}
```

---

# Using Custom Exception

```java
class Main {

    static void validate(int age)
        throws InvalidAgeException {

        if(age < 18) {

            throw new InvalidAgeException(
                "Not Eligible"
            );
        }
    }

    public static void main(String[] args) {

        try {

            validate(15);
        }

        catch(Exception e) {

            System.out.println(
                e.getMessage()
            );
        }
    }
}
```

---

# Exception Propagation

Exception travels:
```java
method to method
```

until handled.

---

# Example

```java
class Main {

    static void m1() {

        int x = 10 / 0;
    }

    static void m2() {

        m1();
    }

    public static void main(String[] args) {

        try {

            m2();
        }

        catch(Exception e) {

            System.out.println("Handled");
        }
    }
}
```

---

# try-with-resources

Introduced in:
```java
Java 7
```

Automatically closes resources.

---

# Example

```java
import java.io.*;

class Main {

    public static void main(String[] args)
        throws Exception {

        try(
            FileReader fr =
                new FileReader(
                    "abc.txt"
                )
        ) {

            System.out.println(
                "Reading File"
            );
        }
    }
}
```

---

# Multi-catch Block

One catch handles multiple exceptions.

---

# Example

```java
try {

}

catch(ArithmeticException |
      NullPointerException e) {

}
```

---

# Important Catch Order Rule

Child exception first.

Parent exception later.

---

# Wrong Example

```java
catch(Exception e) {

}

catch(ArithmeticException e) {

}
```

Compile-time error.

---

# Correct Example

```java
catch(ArithmeticException e) {

}

catch(Exception e) {

}
```

---

# Difference Between final, finally, finalize()

| Keyword | Purpose |
|---|---|
| final | Restrict modification |
| finally | Always executes |
| finalize() | Before garbage collection |

---

# Common Runtime Exceptions

| Exception | Cause |
|---|---|
| ArithmeticException | Divide by zero |
| NullPointerException | Null object |
| NumberFormatException | Invalid conversion |
| ArrayIndexOutOfBoundsException | Invalid index |

---

# Advantages of Exception Handling

- Prevents abnormal termination
- Improves readability
- Separates error logic
- Maintains program flow

---

# Disadvantages

- More code
- Slight performance overhead

---

# Important Interview Questions

1. What is exception?
2. Difference between Error and Exception?
3. Difference between checked and unchecked exceptions?
4. Difference between throw and throws?
5. What is custom exception?
6. What is exception propagation?
7. Why finally used?
8. What is try-with-resources?
9. Why catch order matters?
10. Difference between final, finally, finalize()?

---

# Quick Revision

# try-catch

```java
try {

}
catch(Exception e) {

}
```

---

# finally

```java
finally {

}
```

Always executes.

---

# throw

```java
throw new Exception();
```

---

# throws

```java
void show() throws IOException
```

---

# Custom Exception

```java
class MyException
    extends Exception
```

---

# Final Summary Table

| Concept | Meaning |
|---|---|
| try | Risky code |
| catch | Handle exception |
| finally | Always executes |
| throw | Throw manually |
| throws | Declare exception |
| Checked Exception | Compile-time checked |
| Unchecked Exception | Runtime checked |
| Custom Exception | User-defined |

---

# Final Conclusion

Exception handling in Java helps:
- manage runtime problems
- avoid abnormal termination
- maintain smooth execution

Java provides:
- try
- catch
- finally
- throw
- throws

to build:
- robust
- reliable
- fault-tolerant applications
