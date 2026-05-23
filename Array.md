# Java Arrays Notes


# Arrays in Java

## What is an Array?
- An array is a collection of similar type of elements stored in contiguous memory locations.
- Arrays are used to store multiple values in a single variable.
- Indexing starts from `0`.

Example:
```java
int[] arr = {10, 20, 30, 40};
````

| Index | Value |
| ----- | ----- |
| 0     | 10    |
| 1     | 20    |
| 2     | 30    |
| 3     | 40    |

---

# Why Use Arrays?

* Store multiple values of same type
* Easy access using index
* Faster retrieval
* Useful in loops and algorithms

Without Array:

```java
int a = 10;
int b = 20;
int c = 30;
```

With Array:

```java
int[] arr = {10, 20, 30};
```

---

# Syntax of Array Declaration

## 1. Declaration

```java
datatype[] arrayName;
```

Example:

```java
int[] arr;
```

---

## 2. Memory Allocation

```java
arr = new int[5];
```

---

## 3. Initialization

```java
arr[0] = 10;
arr[1] = 20;
```

---

# Complete Example

```java
int[] arr = new int[5];

arr[0] = 10;
arr[1] = 20;
arr[2] = 30;
arr[3] = 40;
arr[4] = 50;
```

---

# Shortcut Initialization

```java
int[] arr = {10, 20, 30, 40, 50};
```

---

# Accessing Elements

```java
System.out.println(arr[0]);
System.out.println(arr[2]);
```

Output:

```java
10
30
```

---

# Updating Elements

```java
arr[1] = 100;
```

---

# Array Length

```java
arr.length
```

Example:

```java
System.out.println(arr.length);
```

---

# Traversing Array

## Using for loop

```java
for(int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

---

## Using Enhanced for loop (for-each)

```java
for(int value : arr) {
    System.out.println(value);
}
```

---

# Default Values in Arrays

| Data Type     | Default Value |
| ------------- | ------------- |
| int           | 0             |
| double        | 0.0           |
| boolean       | false         |
| char          | '\u0000'      |
| String/Object | null          |

Example:

```java
int[] arr = new int[3];

System.out.println(arr[0]); // 0
```

---

# Types of Arrays

## 1. Single Dimensional Array

```java
int[] arr = {1, 2, 3};
```

---

## 2. Multidimensional Array

### 2D Array

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};
```

Access:

```java
System.out.println(matrix[1][2]);
```

Output:

```java
6
```

---

# Traversing 2D Array

```java
for(int i = 0; i < matrix.length; i++) {
    for(int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

---

# Jagged Array

* Array with different column sizes.

Example:

```java
int[][] arr = {
    {1, 2},
    {3, 4, 5},
    {6}
};
```

---

# Important Points

* Arrays store same datatype elements only.
* Arrays have fixed size.
* Once created, size cannot be changed.
* Arrays are objects in Java.
* Stored in heap memory.
* Array index starts from 0.

---

# Array Memory Representation

Example:

```java
int[] arr = {10, 20, 30};
```

Memory:

```text
Index:   0    1    2
Value:  10   20   30
```

---

# Common Array Exceptions

## ArrayIndexOutOfBoundsException

Occurs when index is invalid.

Example:

```java
int[] arr = {10, 20};

System.out.println(arr[5]);
```

---

## NullPointerException

Occurs when array reference is null.

Example:

```java
int[] arr = null;

System.out.println(arr[0]);
```

---

# Copying Arrays

## Manual Copy

```java
int[] arr1 = {1, 2, 3};

int[] arr2 = new int[arr1.length];

for(int i = 0; i < arr1.length; i++) {
    arr2[i] = arr1[i];
}
```

---

## Using clone()

```java
int[] arr2 = arr1.clone();
```

---

## Using Arrays.copyOf()

```java
import java.util.Arrays;

int[] arr2 = Arrays.copyOf(arr1, arr1.length);
```

---

# Sorting Arrays

```java
import java.util.Arrays;

int[] arr = {5, 2, 1, 4};

Arrays.sort(arr);
```

---

# Printing Arrays

## Using Loop

```java
for(int num : arr) {
    System.out.println(num);
}
```

---

## Using Arrays.toString()

```java
import java.util.Arrays;

System.out.println(Arrays.toString(arr));
```

---

# Passing Array to Method

```java
public static void printArray(int[] arr) {
    for(int num : arr) {
        System.out.println(num);
    }
}
```

Calling:

```java
printArray(arr);
```

---

# Returning Array from Method

```java
public static int[] getArray() {
    return new int[]{1, 2, 3};
}
```

---

# Anonymous Array

* Array without reference variable.

Example:

```java
printArray(new int[]{1, 2, 3});
```

---

# Command Line Arguments

```java
public static void main(String[] args)
```

Example:

```java
java Test hello world
```

Output:

```java
args[0] -> hello
args[1] -> world
```

---

# Advantages of Arrays

* Fast access using index
* Easy traversal
* Memory efficient
* Useful for storing bulk data

---

# Disadvantages of Arrays

* Fixed size
* Stores only same datatype
* Insertion/deletion difficult
* Memory wastage possible

---

# Important Utility Methods (Arrays Class)

| Method            | Use               |
| ----------------- | ----------------- |
| Arrays.sort()     | Sorting           |
| Arrays.toString() | Convert to string |
| Arrays.equals()   | Compare arrays    |
| Arrays.fill()     | Fill values       |
| Arrays.copyOf()   | Copy array        |

Example:

```java
Arrays.fill(arr, 0);
```

---

# Difference Between Array and ArrayList

| Array             | ArrayList       |
| ----------------- | --------------- |
| Fixed size        | Dynamic size    |
| Faster            | Slightly slower |
| Primitive allowed | Objects only    |
| Length property   | size() method   |

---

# Interview Questions

## Q1. Why array index starts from 0?

* Because array address calculation becomes faster and simpler.

---

## Q2. Can array size change dynamically?

* No.

---

## Q3. Are arrays objects in Java?

* Yes.

---

## Q4. Where are arrays stored?

* Heap memory.

---

## Q5. Can arrays store different datatypes?

* No.

---

# Practice Programs

## Sum of Array Elements

```java
int[] arr = {1, 2, 3, 4};

int sum = 0;

for(int num : arr) {
    sum += num;
}

System.out.println(sum);
```

---

## Find Maximum Element

```java
int[] arr = {5, 1, 9, 2};

int max = arr[0];

for(int num : arr) {
    if(num > max) {
        max = num;
    }
}

System.out.println(max);
```

---

## Reverse Array

```java
int[] arr = {1, 2, 3, 4};

for(int i = arr.length - 1; i >= 0; i--) {
    System.out.print(arr[i] + " ");
}
```

---

# Final Quick Revision

* Array = collection of same datatype
* Index starts from 0
* Fixed size
* Stored in heap memory
* Access using index
* length gives size
* Arrays class provides utility methods
* 1D, 2D, Jagged arrays possible
* Default values assigned automatically

```
```
