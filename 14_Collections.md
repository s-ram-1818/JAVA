# Java Collections Framework — Complete Notes

---

## Table of Contents
1. [Introduction](#1-introduction)
2. [Collection Hierarchy](#2-collection-hierarchy)
3. [Iterable & Iterator](#3-iterable--iterator)
4. [Collection Interface](#4-collection-interface)
5. [List Interface](#5-list-interface)
   - ArrayList
   - LinkedList
   - Vector
   - Stack
6. [Set Interface](#6-set-interface)
   - HashSet
   - LinkedHashSet
   - TreeSet
7. [Queue Interface](#7-queue-interface)
   - PriorityQueue
   - ArrayDeque
   - LinkedList as Queue
8. [Deque Interface](#8-deque-interface)
9. [Map Interface](#9-map-interface)
   - HashMap
   - LinkedHashMap
   - TreeMap
   - Hashtable
   - WeakHashMap
   - IdentityHashMap
   - EnumMap
10. [Sorted & Navigable Interfaces](#10-sorted--navigable-interfaces)
11. [Comparable vs Comparator](#11-comparable-vs-comparator)
12. [Collections Utility Class](#12-collections-utility-class)
13. [Arrays Utility Class](#13-arrays-utility-class)
14. [Fail-Fast vs Fail-Safe Iterators](#14-fail-fast-vs-fail-safe-iterators)
15. [Concurrent Collections](#15-concurrent-collections)
16. [Legacy Classes](#16-legacy-classes)
17. [Java 8+ Stream with Collections](#17-java-8-stream-with-collections)
18. [Generics in Collections](#18-generics-in-collections)
19. [Unmodifiable & Immutable Collections](#19-unmodifiable--immutable-collections)
20. [Performance Comparison Table](#20-performance-comparison-table)

---

## 1. Introduction

The **Java Collections Framework (JCF)** is a unified architecture for storing, manipulating, and processing groups of objects. It was introduced in Java 1.2 (1998) and is found in the `java.util` package.

### Why use Collections?
- Arrays have fixed size; collections are dynamic.
- Built-in algorithms (sort, search, shuffle).
- Type-safe via Generics (Java 5+).
- Thread-safe variants available.

### Core Components
| Component | Description |
|---|---|
| **Interfaces** | Abstract data types (List, Set, Map, Queue, Deque) |
| **Implementations** | Concrete classes (ArrayList, HashMap, etc.) |
| **Algorithms** | Static methods in `Collections` and `Arrays` utility classes |

---

## 2. Collection Hierarchy

```
java.lang.Iterable
    └── java.util.Collection
            ├── List
            │     ├── ArrayList
            │     ├── LinkedList
            │     ├── Vector
            │     │     └── Stack
            │     └── CopyOnWriteArrayList (concurrent)
            ├── Set
            │     ├── HashSet
            │     │     └── LinkedHashSet
            │     ├── TreeSet (implements SortedSet, NavigableSet)
            │     └── CopyOnWriteArraySet (concurrent)
            └── Queue
                  ├── PriorityQueue
                  ├── ArrayDeque (implements Deque)
                  ├── LinkedList (implements Deque)
                  └── BlockingQueue (concurrent)
                        ├── ArrayBlockingQueue
                        ├── LinkedBlockingQueue
                        └── PriorityBlockingQueue

java.util.Map (separate hierarchy)
    ├── HashMap
    │     └── LinkedHashMap
    ├── TreeMap (implements SortedMap, NavigableMap)
    ├── Hashtable
    │     └── Properties
    ├── WeakHashMap
    ├── IdentityHashMap
    └── EnumMap
```

---

## 3. Iterable & Iterator

### Iterable Interface
Any class implementing `Iterable<T>` can be used in a for-each loop.

```java
public interface Iterable<T> {
    Iterator<T> iterator();
}
```

### Iterator Interface
```java
public interface Iterator<T> {
    boolean hasNext();   // returns true if more elements exist
    T next();            // returns next element
    void remove();       // removes last element returned by next()
}
```

### Example
```java
import java.util.*;

List<String> list = new ArrayList<>(Arrays.asList("A", "B", "C"));
Iterator<String> it = list.iterator();

while (it.hasNext()) {
    String val = it.next();
    if (val.equals("B")) {
        it.remove(); // safe removal during iteration
    }
}
System.out.println(list); // Output: [A, C]
```

### ListIterator (bidirectional, only for List)
```java
public interface ListIterator<T> extends Iterator<T> {
    boolean hasPrevious();
    T previous();
    int nextIndex();
    int previousIndex();
    void set(T e);
    void add(T e);
}
```

```java
List<String> list = new ArrayList<>(Arrays.asList("X", "Y", "Z"));
ListIterator<String> lit = list.listIterator(list.size()); // start from end

while (lit.hasPrevious()) {
    System.out.print(lit.previous() + " ");
}
// Output: Z Y X
```

---

## 4. Collection Interface

All collection interfaces extend `Collection<E>` (except Map).

### Core Methods
| Method | Description |
|---|---|
| `add(E e)` | Adds element; returns true if changed |
| `addAll(Collection c)` | Adds all elements from another collection |
| `remove(Object o)` | Removes first occurrence |
| `removeAll(Collection c)` | Removes all elements present in c |
| `retainAll(Collection c)` | Keeps only elements in c (intersection) |
| `contains(Object o)` | Returns true if element exists |
| `containsAll(Collection c)` | Returns true if all elements of c exist |
| `size()` | Returns number of elements |
| `isEmpty()` | Returns true if size == 0 |
| `clear()` | Removes all elements |
| `toArray()` | Returns Object[] |
| `toArray(T[] a)` | Returns typed array |
| `iterator()` | Returns an Iterator |
| `stream()` | Returns a sequential Stream (Java 8+) |
| `parallelStream()` | Returns a parallel Stream (Java 8+) |
| `forEach(Consumer)` | Iterates with lambda (Java 8+) |
| `removeIf(Predicate)` | Removes elements matching condition (Java 8+) |

```java
Collection<Integer> col = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));

col.removeIf(n -> n % 2 == 0);
System.out.println(col); // Output: [1, 3, 5]

col.forEach(n -> System.out.print(n + " ")); // Output: 1 3 5
```

---

## 5. List Interface

- **Ordered** (insertion order maintained)
- **Allows duplicates**
- **Index-based access**

### Additional Methods (beyond Collection)
| Method | Description |
|---|---|
| `get(int index)` | Returns element at index |
| `set(int index, E e)` | Replaces element at index |
| `add(int index, E e)` | Inserts at specific index |
| `remove(int index)` | Removes element at index |
| `indexOf(Object o)` | First index of element (-1 if not found) |
| `lastIndexOf(Object o)` | Last index of element |
| `subList(int from, int to)` | View of list from `from` (inclusive) to `to` (exclusive) |
| `listIterator()` | Returns ListIterator |
| `sort(Comparator c)` | Sorts the list (Java 8+) |
| `replaceAll(UnaryOperator)` | Replaces each element (Java 8+) |

---

### 5.1 ArrayList

- **Backed by a dynamic array**
- **O(1)** random access, **O(n)** insert/delete in middle
- Default initial capacity: **10**
- Not synchronized

```java
import java.util.*;

ArrayList<String> al = new ArrayList<>();

// add
al.add("Mango");
al.add("Apple");
al.add("Banana");
al.add(1, "Grapes"); // insert at index 1

System.out.println(al); // [Mango, Grapes, Apple, Banana]

// get / set
System.out.println(al.get(0));     // Mango
al.set(0, "Papaya");
System.out.println(al.get(0));     // Papaya

// remove
al.remove("Apple");               // by value
al.remove(0);                     // by index
System.out.println(al);           // [Grapes, Banana]

// size, contains, isEmpty
System.out.println(al.size());           // 2
System.out.println(al.contains("Grapes")); // true
System.out.println(al.isEmpty());         // false

// indexOf / lastIndexOf
al.add("Banana");
System.out.println(al.indexOf("Banana"));     // 1
System.out.println(al.lastIndexOf("Banana")); // 2

// subList
List<String> sub = al.subList(0, 2);
System.out.println(sub); // [Grapes, Banana]

// sort
Collections.sort(al);
System.out.println(al); // [Banana, Banana, Grapes]

// toArray
Object[] arr = al.toArray();
String[] strArr = al.toArray(new String[0]);

// iterator
Iterator<String> it = al.iterator();
while (it.hasNext()) System.out.print(it.next() + " "); // Banana Banana Grapes

// replaceAll (Java 8+)
al.replaceAll(String::toUpperCase);
System.out.println(al); // [BANANA, BANANA, GRAPES]

// removeIf (Java 8+)
al.removeIf(s -> s.equals("BANANA"));
System.out.println(al); // [GRAPES]

// clear
al.clear();
System.out.println(al.isEmpty()); // true

// addAll
ArrayList<String> a1 = new ArrayList<>(Arrays.asList("X", "Y"));
ArrayList<String> a2 = new ArrayList<>(Arrays.asList("Y", "Z"));
a1.addAll(a2);
System.out.println(a1); // [X, Y, Y, Z]

// retainAll
a1.retainAll(a2);
System.out.println(a1); // [Y, Z]

// removeAll
a1.removeAll(a2);
System.out.println(a1); // []

// ensureCapacity / trimToSize (optimization)
ArrayList<Integer> nums = new ArrayList<>();
nums.ensureCapacity(100); // pre-allocate for 100 elements
for (int i = 0; i < 50; i++) nums.add(i);
nums.trimToSize(); // trim internal array to actual size
System.out.println(nums.size()); // 50
```

---

### 5.2 LinkedList

- **Doubly linked list** internally
- Implements both **List** and **Deque**
- **O(1)** insert/delete at head/tail, **O(n)** random access
- More memory than ArrayList (stores prev/next pointers)

```java
LinkedList<String> ll = new LinkedList<>();

// List methods
ll.add("B");
ll.add("C");
ll.add(0, "A");
System.out.println(ll); // [A, B, C]
System.out.println(ll.get(1)); // B
ll.set(1, "X");
System.out.println(ll); // [A, X, C]
ll.remove(1);
System.out.println(ll); // [A, C]

// Deque / Queue specific methods
ll.addFirst("START");
ll.addLast("END");
System.out.println(ll); // [START, A, C, END]

System.out.println(ll.getFirst()); // START
System.out.println(ll.getLast());  // END
System.out.println(ll.peekFirst()); // START (null if empty)
System.out.println(ll.peekLast());  // END   (null if empty)

ll.removeFirst();
ll.removeLast();
System.out.println(ll); // [A, C]

ll.offerFirst("FIRST"); // same as addFirst but Queue-style
ll.offerLast("LAST");
System.out.println(ll); // [FIRST, A, C, LAST]

System.out.println(ll.poll());      // FIRST (removes head, null if empty)
System.out.println(ll.pollFirst()); // A
System.out.println(ll.pollLast());  // LAST

// peek does NOT remove
System.out.println(ll.peek()); // C

// push / pop (stack operations)
ll.push("TOP");
System.out.println(ll); // [TOP, C]
System.out.println(ll.pop()); // TOP
```

---

### 5.3 Vector

- **Synchronized** version of ArrayList
- Legacy class (Java 1.0), prefer `ArrayList` + `Collections.synchronizedList`
- Growth: doubles size when full (ArrayList grows by 50%)

```java
Vector<Integer> v = new Vector<>(2, 3); // capacity=2, increment=3

v.add(10);
v.add(20);
v.add(30); // exceeds capacity, grows by 3

System.out.println(v);               // [10, 20, 30]
System.out.println(v.capacity());    // 5 (2 + 3)
System.out.println(v.size());        // 3

v.addElement(40);   // legacy method
v.insertElementAt(15, 1);
System.out.println(v); // [10, 15, 20, 30, 40]

System.out.println(v.elementAt(2));  // 20
v.setElementAt(99, 2);
System.out.println(v.elementAt(2)); // 99

System.out.println(v.firstElement()); // 10
System.out.println(v.lastElement());  // 40

v.removeElement(15);
v.removeElementAt(0);
System.out.println(v); // [99, 30, 40]

v.removeAllElements();
System.out.println(v.isEmpty()); // true

// Enumeration (legacy iteration)
Vector<String> sv = new Vector<>(Arrays.asList("P", "Q", "R"));
Enumeration<String> e = sv.elements();
while (e.hasMoreElements()) System.out.print(e.nextElement() + " "); // P Q R
```

---

### 5.4 Stack

- Extends **Vector** (LIFO - Last In First Out)
- Prefer `ArrayDeque` for stack operations in modern code

```java
Stack<String> stack = new Stack<>();

stack.push("First");
stack.push("Second");
stack.push("Third");

System.out.println(stack);          // [First, Second, Third]
System.out.println(stack.peek());   // Third (no removal)
System.out.println(stack.pop());    // Third (removes top)
System.out.println(stack);          // [First, Second]
System.out.println(stack.isEmpty()); // false
System.out.println(stack.search("First")); // 2 (1-based from top)
System.out.println(stack.search("NoExist")); // -1
```

---

## 6. Set Interface

- **No duplicates**
- `add()` returns `false` if element already exists
- No index-based access

---

### 6.1 HashSet

- **Backed by HashMap** internally
- **O(1)** add, remove, contains (average)
- **No ordering guaranteed**
- Allows one `null`

```java
HashSet<String> hs = new HashSet<>();

// add
hs.add("Dog");
hs.add("Cat");
hs.add("Bird");
boolean added = hs.add("Dog"); // duplicate
System.out.println(added);     // false
System.out.println(hs);        // [Dog, Cat, Bird] (order may vary)

// contains / remove
System.out.println(hs.contains("Cat")); // true
hs.remove("Cat");
System.out.println(hs.contains("Cat")); // false

// size / isEmpty
System.out.println(hs.size());    // 2
System.out.println(hs.isEmpty()); // false

// iteration
for (String s : hs) System.out.print(s + " "); // Dog Bird (order not guaranteed)

// addAll (union)
HashSet<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3));
HashSet<Integer> set2 = new HashSet<>(Arrays.asList(3, 4, 5));
HashSet<Integer> union = new HashSet<>(set1);
union.addAll(set2);
System.out.println(union); // [1, 2, 3, 4, 5]

// retainAll (intersection)
HashSet<Integer> inter = new HashSet<>(set1);
inter.retainAll(set2);
System.out.println(inter); // [3]

// removeAll (difference)
HashSet<Integer> diff = new HashSet<>(set1);
diff.removeAll(set2);
System.out.println(diff); // [1, 2]

// toArray
Object[] arr = hs.toArray();

// clear
hs.clear();
System.out.println(hs.isEmpty()); // true
```

---

### 6.2 LinkedHashSet

- Extends **HashSet**
- Maintains **insertion order**
- Slightly slower than HashSet due to linked list overhead
- Allows one `null`

```java
LinkedHashSet<String> lhs = new LinkedHashSet<>();

lhs.add("Zebra");
lhs.add("Apple");
lhs.add("Mango");
lhs.add("Apple"); // duplicate, ignored

System.out.println(lhs); // [Zebra, Apple, Mango] — insertion order preserved

lhs.remove("Apple");
System.out.println(lhs); // [Zebra, Mango]

System.out.println(lhs.contains("Zebra")); // true
System.out.println(lhs.size());             // 2

// All other methods same as HashSet
```

---

### 6.3 TreeSet

- Implements **SortedSet** and **NavigableSet**
- Backed by a **Red-Black Tree**
- Elements stored in **natural sorted order** (or custom Comparator)
- **O(log n)** for add, remove, contains
- Does **NOT** allow `null`

```java
TreeSet<Integer> ts = new TreeSet<>();

ts.add(50);
ts.add(10);
ts.add(30);
ts.add(20);
ts.add(10); // duplicate, ignored

System.out.println(ts); // [10, 20, 30, 50] — sorted

// SortedSet methods
System.out.println(ts.first());          // 10
System.out.println(ts.last());           // 50
System.out.println(ts.headSet(30));      // [10, 20]    — elements < 30
System.out.println(ts.tailSet(30));      // [30, 50]    — elements >= 30
System.out.println(ts.subSet(10, 40));   // [10, 20, 30] — 10 <= x < 40

// NavigableSet methods
System.out.println(ts.lower(30));        // 20 — greatest element < 30
System.out.println(ts.higher(30));       // 50 — smallest element > 30
System.out.println(ts.floor(30));        // 30 — greatest element <= 30
System.out.println(ts.ceiling(25));      // 30 — smallest element >= 25
System.out.println(ts.pollFirst());      // 10 — remove and return smallest
System.out.println(ts.pollLast());       // 50 — remove and return largest
System.out.println(ts);                  // [20, 30]

System.out.println(ts.descendingSet());  // [30, 20]

// headSet/tailSet/subSet with inclusive flag
TreeSet<Integer> ts2 = new TreeSet<>(Arrays.asList(10, 20, 30, 40, 50));
System.out.println(ts2.headSet(30, true));       // [10, 20, 30] (inclusive)
System.out.println(ts2.tailSet(30, false));      // [40, 50]     (exclusive)
System.out.println(ts2.subSet(20, true, 40, true)); // [20, 30, 40]

// Custom Comparator (reverse order)
TreeSet<String> ts3 = new TreeSet<>(Comparator.reverseOrder());
ts3.add("Banana");
ts3.add("Apple");
ts3.add("Cherry");
System.out.println(ts3); // [Cherry, Banana, Apple]

// contains / remove
System.out.println(ts2.contains(30)); // true
ts2.remove(30);
System.out.println(ts2); // [10, 20, 40, 50]
```

---

## 7. Queue Interface

- **FIFO** (First In First Out) by default
- Two sets of methods:
  - Throws exception: `add()`, `remove()`, `element()`
  - Returns special value: `offer()`, `poll()`, `peek()`

| Operation | Throws Exception | Returns Special Value |
|---|---|---|
| Insert | `add(e)` | `offer(e)` |
| Remove | `remove()` | `poll()` |
| Examine | `element()` | `peek()` |

---

### 7.1 PriorityQueue

- Elements ordered by **natural order** or **Comparator**
- Smallest element at head by default (min-heap)
- **Does NOT allow null**
- **Not thread-safe**

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();

// offer / add
pq.offer(30);
pq.offer(10);
pq.offer(20);
pq.add(5);

System.out.println(pq);          // [5, 10, 20, 30] (internal heap, may vary display)
System.out.println(pq.peek());   // 5  (head, no removal)
System.out.println(pq.element()); // 5 (same as peek but throws if empty)

System.out.println(pq.poll());   // 5  (removes head)
System.out.println(pq.remove()); // 10 (removes head, throws if empty)
System.out.println(pq);          // [20, 30]

System.out.println(pq.size());      // 2
System.out.println(pq.contains(20)); // true

// Max-Heap using Comparator
PriorityQueue<Integer> maxPQ = new PriorityQueue<>(Comparator.reverseOrder());
maxPQ.offer(30);
maxPQ.offer(10);
maxPQ.offer(50);

System.out.println(maxPQ.poll()); // 50 (max element first)
System.out.println(maxPQ.poll()); // 30

// Custom objects
PriorityQueue<String> strPQ = new PriorityQueue<>(Comparator.comparingInt(String::length));
strPQ.offer("Banana");
strPQ.offer("Hi");
strPQ.offer("Apple");

System.out.println(strPQ.poll()); // Hi (shortest string first)

// Iteration (does NOT guarantee sorted order)
PriorityQueue<Integer> pq2 = new PriorityQueue<>(Arrays.asList(4, 2, 8, 1));
for (int x : pq2) System.out.print(x + " "); // order not guaranteed

// toArray
Object[] arr = pq2.toArray();

// clear
pq2.clear();
System.out.println(pq2.isEmpty()); // true
```

---

### 7.2 ArrayDeque (as Queue)

- Resizable array-based **Deque**
- **Faster than LinkedList** for queue/stack operations
- Does **NOT allow null**

```java
ArrayDeque<String> adq = new ArrayDeque<>();

adq.offer("A");    // adds to tail
adq.offer("B");
adq.offer("C");

System.out.println(adq.peek());  // A
System.out.println(adq.poll());  // A
System.out.println(adq);         // [B, C]

// (See Deque section for full method list)
```

---

### 7.3 LinkedList as Queue

```java
Queue<String> q = new LinkedList<>();

q.offer("First");
q.offer("Second");
q.offer("Third");

System.out.println(q.peek());   // First
System.out.println(q.poll());   // First
System.out.println(q);          // [Second, Third]
```

---

## 8. Deque Interface

**Double-Ended Queue** — supports insert/remove at both ends.

| Operation | Head (throws) | Head (safe) | Tail (throws) | Tail (safe) |
|---|---|---|---|---|
| Insert | `addFirst(e)` | `offerFirst(e)` | `addLast(e)` | `offerLast(e)` |
| Remove | `removeFirst()` | `pollFirst()` | `removeLast()` | `pollLast()` |
| Examine | `getFirst()` | `peekFirst()` | `getLast()` | `peekLast()` |

### ArrayDeque — Full Methods

```java
ArrayDeque<Integer> dq = new ArrayDeque<>();

// Adding
dq.addFirst(1);
dq.addLast(2);
dq.offerFirst(0);
dq.offerLast(3);
System.out.println(dq); // [0, 1, 2, 3]

// Examining
System.out.println(dq.getFirst());   // 0 (throws NoSuchElementException if empty)
System.out.println(dq.getLast());    // 3
System.out.println(dq.peekFirst());  // 0 (null if empty)
System.out.println(dq.peekLast());   // 3 (null if empty)

// Removing
System.out.println(dq.removeFirst()); // 0
System.out.println(dq.removeLast());  // 3
System.out.println(dq.pollFirst());   // 1 (null if empty)
System.out.println(dq.pollLast());    // 2 (null if empty)
System.out.println(dq);               // []

// Stack operations (LIFO)
dq.push(10); // same as addFirst
dq.push(20);
dq.push(30);
System.out.println(dq);          // [30, 20, 10]
System.out.println(dq.pop());    // 30 (same as removeFirst)
System.out.println(dq.peek());   // 20 (same as peekFirst)

// contains / remove specific element
dq.add(10);
dq.add(20);
dq.add(10);
System.out.println(dq.contains(10)); // true
dq.removeFirstOccurrence(10);
System.out.println(dq);              // [20, 20, 10]
dq.removeLastOccurrence(10);
System.out.println(dq);              // [20, 20]

// size / isEmpty
System.out.println(dq.size());    // 2
System.out.println(dq.isEmpty()); // false

// descendingIterator
ArrayDeque<String> sdq = new ArrayDeque<>(Arrays.asList("A", "B", "C"));
Iterator<String> di = sdq.descendingIterator();
while (di.hasNext()) System.out.print(di.next() + " "); // C B A

// toArray / clear
Object[] arr = sdq.toArray();
sdq.clear();
System.out.println(sdq.isEmpty()); // true
```

---

## 9. Map Interface

- Stores **key-value pairs**
- Keys must be **unique**; values can repeat
- Does **NOT** extend `Collection`

### Core Map Methods
| Method | Description |
|---|---|
| `put(K key, V value)` | Inserts/updates key-value pair |
| `get(Object key)` | Returns value for key (null if absent) |
| `remove(Object key)` | Removes entry for key |
| `remove(Object key, Object value)` | Removes only if key maps to value |
| `containsKey(Object key)` | Checks if key exists |
| `containsValue(Object value)` | Checks if value exists |
| `size()` | Number of entries |
| `isEmpty()` | True if empty |
| `clear()` | Removes all entries |
| `keySet()` | Returns `Set<K>` of all keys |
| `values()` | Returns `Collection<V>` of all values |
| `entrySet()` | Returns `Set<Map.Entry<K,V>>` |
| `putAll(Map m)` | Copies all from m |
| `getOrDefault(key, def)` | Returns value or default (Java 8+) |
| `putIfAbsent(key, value)` | Inserts only if key absent (Java 8+) |
| `replace(key, value)` | Replaces if key present (Java 8+) |
| `replace(key, old, new)` | Replaces if maps to old (Java 8+) |
| `computeIfAbsent(key, fn)` | Compute & insert if absent (Java 8+) |
| `computeIfPresent(key, fn)` | Compute & update if present (Java 8+) |
| `compute(key, fn)` | Compute & update/insert (Java 8+) |
| `merge(key, value, fn)` | Merge with existing value (Java 8+) |
| `forEach(BiConsumer)` | Iterate entries (Java 8+) |
| `replaceAll(BiFunction)` | Replace all values (Java 8+) |

---

### 9.1 HashMap

- Key-value pairs backed by a **hash table**
- **O(1)** average for get/put/remove
- **No ordering** of keys
- Allows **one null key** and **multiple null values**
- Not synchronized
- Default capacity: **16**, load factor: **0.75**

```java
HashMap<String, Integer> hm = new HashMap<>();

// put
hm.put("Alice", 90);
hm.put("Bob", 85);
hm.put("Charlie", 92);
hm.put("Alice", 95); // overwrites existing
hm.put(null, 0);     // null key allowed

System.out.println(hm); // {null=0, Bob=85, Alice=95, Charlie=92}

// get
System.out.println(hm.get("Bob"));     // 85
System.out.println(hm.get("NoKey"));   // null

// getOrDefault
System.out.println(hm.getOrDefault("NoKey", -1)); // -1

// containsKey / containsValue
System.out.println(hm.containsKey("Alice"));   // true
System.out.println(hm.containsValue(999));     // false

// remove
hm.remove(null);
hm.remove("Bob", 99);  // won't remove — Bob maps to 85, not 99
hm.remove("Bob", 85);  // removes Bob
System.out.println(hm); // {Alice=95, Charlie=92}

// keySet
System.out.println(hm.keySet()); // [Alice, Charlie]

// values
System.out.println(hm.values()); // [95, 92]

// entrySet iteration
for (Map.Entry<String, Integer> e : hm.entrySet()) {
    System.out.println(e.getKey() + " -> " + e.getValue());
}
// Alice -> 95
// Charlie -> 92

// putIfAbsent
hm.putIfAbsent("Alice", 0);  // Alice already exists, no change
hm.putIfAbsent("Dave", 80);  // Dave added
System.out.println(hm.get("Alice")); // 95
System.out.println(hm.get("Dave"));  // 80

// replace
hm.replace("Dave", 88);
System.out.println(hm.get("Dave")); // 88

hm.replace("Dave", 88, 90);  // only replaces if current value is 88 — true, so 90
System.out.println(hm.get("Dave")); // 90

// computeIfAbsent — creates entry if missing
hm.computeIfAbsent("Eve", k -> k.length() * 10);
System.out.println(hm.get("Eve")); // 30 (length of "Eve" * 10)

// computeIfPresent — updates entry if present
hm.computeIfPresent("Eve", (k, v) -> v + 5);
System.out.println(hm.get("Eve")); // 35

// compute — insert or update
hm.compute("Frank", (k, v) -> v == null ? 1 : v + 1);
System.out.println(hm.get("Frank")); // 1

// merge — if key absent, put value; if present, apply function
hm.merge("Alice", 5, Integer::sum);
System.out.println(hm.get("Alice")); // 100 (95 + 5)

// forEach
hm.forEach((k, v) -> System.out.println(k + ": " + v));

// replaceAll
hm.replaceAll((k, v) -> v + 1);

// putAll
HashMap<String, Integer> hm2 = new HashMap<>();
hm2.put("X", 1);
hm.putAll(hm2);

// size / clear / isEmpty
System.out.println(hm.size());
hm.clear();
System.out.println(hm.isEmpty()); // true
```

---

### 9.2 LinkedHashMap

- Extends **HashMap**
- Maintains **insertion order** (or access order with constructor flag)
- Slightly slower than HashMap due to linked list overhead

```java
LinkedHashMap<String, Integer> lhm = new LinkedHashMap<>();

lhm.put("Banana", 2);
lhm.put("Apple", 1);
lhm.put("Cherry", 3);

System.out.println(lhm); // {Banana=2, Apple=1, Cherry=3} — insertion order

// Access-order (LRU cache behavior)
LinkedHashMap<String, Integer> lru = new LinkedHashMap<>(16, 0.75f, true);
lru.put("a", 1);
lru.put("b", 2);
lru.put("c", 3);
lru.get("a"); // access "a"
System.out.println(lru); // {b=2, c=3, a=1} — "a" moved to end

// Override removeEldestEntry for LRU Cache (max 2 entries)
LinkedHashMap<String, Integer> cache = new LinkedHashMap<>(16, 0.75f, true) {
    protected boolean removeEldestEntry(Map.Entry<String, Integer> eldest) {
        return size() > 2;
    }
};
cache.put("x", 1);
cache.put("y", 2);
cache.put("z", 3); // evicts "x" (least recently used)
System.out.println(cache); // {y=2, z=3}

// All other methods same as HashMap
```

---

### 9.3 TreeMap

- Implements **SortedMap** and **NavigableMap**
- Keys stored in **natural sorted order** (or custom Comparator)
- Backed by a **Red-Black Tree**
- **O(log n)** for get/put/remove
- Does **NOT** allow null keys (allows null values)

```java
TreeMap<String, Integer> tm = new TreeMap<>();

tm.put("Banana", 2);
tm.put("Apple", 1);
tm.put("Cherry", 3);
tm.put("Date", 4);

System.out.println(tm); // {Apple=1, Banana=2, Cherry=3, Date=4}

// SortedMap methods
System.out.println(tm.firstKey()); // Apple
System.out.println(tm.lastKey());  // Date
System.out.println(tm.headMap("Cherry"));      // {Apple=1, Banana=2}
System.out.println(tm.tailMap("Cherry"));      // {Cherry=3, Date=4}
System.out.println(tm.subMap("Banana", "Date")); // {Banana=2, Cherry=3}

// NavigableMap methods
System.out.println(tm.lowerKey("Cherry"));    // Banana
System.out.println(tm.higherKey("Cherry"));   // Date
System.out.println(tm.floorKey("Cherry"));    // Cherry
System.out.println(tm.ceilingKey("C"));       // Cherry

System.out.println(tm.firstEntry());  // Apple=1
System.out.println(tm.lastEntry());   // Date=4

System.out.println(tm.lowerEntry("Cherry"));  // Banana=2
System.out.println(tm.higherEntry("Cherry")); // Date=4
System.out.println(tm.floorEntry("Cherry"));  // Cherry=3
System.out.println(tm.ceilingEntry("Ca"));    // Cherry=3

System.out.println(tm.pollFirstEntry()); // Apple=1 (removes)
System.out.println(tm.pollLastEntry());  // Date=4  (removes)
System.out.println(tm);                  // {Banana=2, Cherry=3}

System.out.println(tm.descendingKeySet()); // [Cherry, Banana]
System.out.println(tm.descendingMap());    // {Cherry=3, Banana=2}

// subMap / headMap / tailMap with inclusive flag
TreeMap<Integer, String> tm2 = new TreeMap<>();
for (int i = 1; i <= 5; i++) tm2.put(i * 10, "v" + i);
System.out.println(tm2.subMap(20, true, 40, true));  // {20=v2, 30=v3, 40=v4}
System.out.println(tm2.headMap(30, true));             // {10=v1, 20=v2, 30=v3}
System.out.println(tm2.tailMap(30, false));            // {40=v4, 50=v5}

// Custom comparator (reverse order)
TreeMap<String, Integer> revTm = new TreeMap<>(Comparator.reverseOrder());
revTm.put("A", 1); revTm.put("C", 3); revTm.put("B", 2);
System.out.println(revTm); // {C=3, B=2, A=1}

// containsKey / containsValue / remove
System.out.println(tm2.containsKey(30));    // true
System.out.println(tm2.containsValue("v3")); // true
tm2.remove(30);
System.out.println(tm2); // {10=v1, 20=v2, 40=v4, 50=v5}

// navigableKeySet
System.out.println(tm2.navigableKeySet()); // [10, 20, 40, 50]
```

---

### 9.4 Hashtable

- Legacy synchronized map (Java 1.0)
- Does **NOT** allow null keys or null values
- Prefer `ConcurrentHashMap` in modern code

```java
Hashtable<String, Integer> ht = new Hashtable<>();

ht.put("A", 1);
ht.put("B", 2);
ht.put("C", 3);

System.out.println(ht);               // {A=1, B=2, C=3} (order varies)
System.out.println(ht.get("A"));      // 1
System.out.println(ht.contains(2));   // true (legacy method, checks value)
System.out.println(ht.containsKey("B"));   // true
System.out.println(ht.containsValue(3));   // true

ht.remove("C");
System.out.println(ht.size()); // 2

// Enumeration (legacy iteration)
Enumeration<String> keys = ht.keys();
while (keys.hasMoreElements()) System.out.print(keys.nextElement() + " ");

Enumeration<Integer> vals = ht.elements();
while (vals.hasMoreElements()) System.out.print(vals.nextElement() + " ");
```

---

### 9.5 WeakHashMap

- Keys are held with **weak references**
- If key has no other strong references, the GC can reclaim the entry
- Useful for **caching** where you don't want to prevent GC

```java
WeakHashMap<Object, String> whm = new WeakHashMap<>();

Object key1 = new Object();
Object key2 = new Object();

whm.put(key1, "Value1");
whm.put(key2, "Value2");

System.out.println(whm.size()); // 2

key1 = null; // remove strong reference
System.gc();  // suggest GC (not guaranteed)

// After GC, key1 entry may be removed
System.out.println(whm.size()); // may be 1

// All standard Map methods apply
System.out.println(whm.containsValue("Value2")); // true
```

---

### 9.6 IdentityHashMap

- Uses **reference equality** (`==`) instead of `.equals()` for key comparison
- Useful when you need to distinguish different object instances with same content

```java
IdentityHashMap<String, Integer> ihm = new IdentityHashMap<>();

String s1 = new String("key");
String s2 = new String("key"); // different object, same content

ihm.put(s1, 1);
ihm.put(s2, 2); // treated as DIFFERENT key (different reference)

System.out.println(ihm.size()); // 2 (both entries exist)
System.out.println(ihm.get(s1)); // 1
System.out.println(ihm.get(s2)); // 2

// Compare with HashMap
HashMap<String, Integer> hm = new HashMap<>();
hm.put(s1, 1);
hm.put(s2, 2); // overwrites s1 because "key".equals("key")
System.out.println(hm.size()); // 1
```

---

### 9.7 EnumMap

- Keys must be **enum constants**
- Internally backed by an **array** (extremely efficient)
- Keys stored in **enum declaration order**
- Does **NOT** allow null keys

```java
enum Day { MON, TUE, WED, THU, FRI, SAT, SUN }

EnumMap<Day, String> em = new EnumMap<>(Day.class);

em.put(Day.MON, "Monday");
em.put(Day.WED, "Wednesday");
em.put(Day.FRI, "Friday");

System.out.println(em); // {MON=Monday, WED=Wednesday, FRI=Friday}

System.out.println(em.get(Day.MON));        // Monday
System.out.println(em.containsKey(Day.TUE)); // false

em.remove(Day.WED);
System.out.println(em.size()); // 2

// keySet / values / entrySet
System.out.println(em.keySet()); // [MON, FRI]

em.putIfAbsent(Day.SUN, "Sunday");
em.forEach((k, v) -> System.out.println(k + " = " + v));
```

---

## 10. Sorted & Navigable Interfaces

### SortedSet Methods
| Method | Description |
|---|---|
| `first()` | Smallest element |
| `last()` | Largest element |
| `headSet(toElement)` | Elements strictly less than toElement |
| `tailSet(fromElement)` | Elements >= fromElement |
| `subSet(from, to)` | Elements: from <= x < to |
| `comparator()` | Returns Comparator, or null if natural ordering |

### NavigableSet Additional Methods
| Method | Description |
|---|---|
| `lower(e)` | Greatest element strictly < e |
| `higher(e)` | Smallest element strictly > e |
| `floor(e)` | Greatest element <= e |
| `ceiling(e)` | Smallest element >= e |
| `pollFirst()` | Remove and return smallest |
| `pollLast()` | Remove and return largest |
| `descendingSet()` | Returns reverse-order view |
| `descendingIterator()` | Iterator in descending order |
| `headSet(e, inclusive)` | Head with inclusive flag |
| `tailSet(e, inclusive)` | Tail with inclusive flag |
| `subSet(from, fromInc, to, toInc)` | Sub with inclusive flags |

### SortedMap Methods
| Method | Description |
|---|---|
| `firstKey()` | Smallest key |
| `lastKey()` | Largest key |
| `headMap(toKey)` | Keys strictly less than toKey |
| `tailMap(fromKey)` | Keys >= fromKey |
| `subMap(from, to)` | from <= keys < to |
| `comparator()` | Returns Comparator, or null |

### NavigableMap Additional Methods
| Method | Description |
|---|---|
| `lowerKey(key)` | Greatest key < key |
| `higherKey(key)` | Smallest key > key |
| `floorKey(key)` | Greatest key <= key |
| `ceilingKey(key)` | Smallest key >= key |
| `lowerEntry(key)` | Entry with greatest key < key |
| `higherEntry(key)` | Entry with smallest key > key |
| `floorEntry(key)` | Entry with greatest key <= key |
| `ceilingEntry(key)` | Entry with smallest key >= key |
| `pollFirstEntry()` | Remove and return first entry |
| `pollLastEntry()` | Remove and return last entry |
| `descendingKeySet()` | Keys in reverse order |
| `descendingMap()` | Map in reverse order |
| `navigableKeySet()` | NavigableSet view of keys |

---

## 11. Comparable vs Comparator

### Comparable (natural ordering)
- Implemented **by the class itself**
- Method: `int compareTo(T o)`
- Returns: negative (this < o), zero (this == o), positive (this > o)

```java
class Student implements Comparable<Student> {
    String name;
    int marks;

    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }

    @Override
    public int compareTo(Student other) {
        return this.marks - other.marks; // ascending by marks
    }

    @Override
    public String toString() {
        return name + "(" + marks + ")";
    }
}

List<Student> students = new ArrayList<>();
students.add(new Student("Alice", 90));
students.add(new Student("Bob", 75));
students.add(new Student("Charlie", 85));

Collections.sort(students);
System.out.println(students); // [Bob(75), Charlie(85), Alice(90)]

TreeSet<Student> ts = new TreeSet<>(students);
System.out.println(ts); // [Bob(75), Charlie(85), Alice(90)]
```

### Comparator (custom ordering)
- External class or lambda
- Method: `int compare(T o1, T o2)`
- Can define **multiple orderings**

```java
// Comparator by name
Comparator<Student> byName = Comparator.comparing(s -> s.name);

// Comparator by marks descending
Comparator<Student> byMarksDesc = Comparator.comparingInt((Student s) -> s.marks).reversed();

// Chained comparators
Comparator<Student> byMarksThenName = Comparator
    .comparingInt((Student s) -> s.marks)
    .thenComparing(s -> s.name);

List<Student> list = new ArrayList<>();
list.add(new Student("Alice", 90));
list.add(new Student("Bob", 75));
list.add(new Student("Charlie", 90));

list.sort(byMarksThenName);
System.out.println(list); // [Bob(75), Alice(90), Charlie(90)]

list.sort(byName);
System.out.println(list); // [Alice(90), Bob(75), Charlie(90)]

// Null-safe comparators
Comparator<String> nullSafe = Comparator.nullsFirst(Comparator.naturalOrder());
List<String> withNulls = Arrays.asList("B", null, "A", null, "C");
withNulls.sort(nullSafe);
System.out.println(withNulls); // [null, null, A, B, C]
```

---

## 12. Collections Utility Class

All methods are **static** in `java.util.Collections`.

```java
import java.util.*;

List<Integer> list = new ArrayList<>(Arrays.asList(3, 1, 4, 1, 5, 9, 2, 6));

// sort — natural order
Collections.sort(list);
System.out.println(list); // [1, 1, 2, 3, 4, 5, 6, 9]

// sort with comparator
Collections.sort(list, Comparator.reverseOrder());
System.out.println(list); // [9, 6, 5, 4, 3, 2, 1, 1]

// reverse
Collections.reverse(list);
System.out.println(list); // [1, 1, 2, 3, 4, 5, 6, 9]

// shuffle (random order)
Collections.shuffle(list);
System.out.println(list); // random order

// shuffle with seed (reproducible)
Collections.shuffle(list, new Random(42));

// min / max
System.out.println(Collections.min(list)); // 1
System.out.println(Collections.max(list)); // 9

// min / max with comparator
System.out.println(Collections.min(list, Comparator.reverseOrder())); // 9

// binarySearch (list must be sorted first)
Collections.sort(list);
int idx = Collections.binarySearch(list, 5);
System.out.println(idx); // index of 5

// frequency — count occurrences of element
List<String> sl = Arrays.asList("a", "b", "a", "c", "a");
System.out.println(Collections.frequency(sl, "a")); // 3

// fill — replace all elements with given value
List<String> fl = new ArrayList<>(Arrays.asList("X", "Y", "Z"));
Collections.fill(fl, "O");
System.out.println(fl); // [O, O, O]

// copy — copy src into dest (dest must have >= size)
List<Integer> src = Arrays.asList(1, 2, 3);
List<Integer> dest = new ArrayList<>(Arrays.asList(0, 0, 0, 0));
Collections.copy(dest, src);
System.out.println(dest); // [1, 2, 3, 0]

// nCopies — returns immutable list of n copies
List<String> copies = Collections.nCopies(5, "Hi");
System.out.println(copies); // [Hi, Hi, Hi, Hi, Hi]

// swap
List<String> swapList = new ArrayList<>(Arrays.asList("A", "B", "C", "D"));
Collections.swap(swapList, 0, 3);
System.out.println(swapList); // [D, B, C, A]

// rotate — rotate elements by distance
List<Integer> rList = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
Collections.rotate(rList, 2);
System.out.println(rList); // [4, 5, 1, 2, 3]

// disjoint — true if two collections have no elements in common
List<Integer> l1 = Arrays.asList(1, 2, 3);
List<Integer> l2 = Arrays.asList(4, 5, 6);
List<Integer> l3 = Arrays.asList(3, 4, 5);
System.out.println(Collections.disjoint(l1, l2)); // true
System.out.println(Collections.disjoint(l1, l3)); // false

// addAll — adds all specified elements to a collection
List<String> target = new ArrayList<>();
Collections.addAll(target, "X", "Y", "Z");
System.out.println(target); // [X, Y, Z]

// replaceAll (not Java 8+ method, this is Collections.replaceAll)
// Collections does not have replaceAll; use List.replaceAll() instead

// unmodifiableXxx — wraps collection to prevent modification
List<String> mutableList = new ArrayList<>(Arrays.asList("A", "B"));
List<String> immutableList = Collections.unmodifiableList(mutableList);
// immutableList.add("C"); // throws UnsupportedOperationException

Set<String> unmodSet = Collections.unmodifiableSet(new HashSet<>(Arrays.asList("X")));
Map<String, Integer> unmodMap = Collections.unmodifiableMap(new HashMap<>());

// synchronizedXxx — thread-safe wrappers
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Set<String> syncSet = Collections.synchronizedSet(new HashSet<>());
Map<String, Integer> syncMap = Collections.synchronizedMap(new HashMap<>());

// singleton — immutable collection with single element
Set<String> singleSet = Collections.singleton("Only");
List<String> singleList = Collections.singletonList("One");
Map<String, Integer> singleMap = Collections.singletonMap("key", 1);

// emptyXxx — immutable empty collection
List<String> emptyList = Collections.emptyList();
Set<String> emptySet = Collections.emptySet();
Map<String, Integer> emptyMap = Collections.emptyMap();

// checkedXxx — runtime type checking
List rawList = new ArrayList();
List<String> checkedList = Collections.checkedList(rawList, String.class);
// checkedList.add(42); // throws ClassCastException at runtime

// reverseOrder comparator
Comparator<Integer> rev = Collections.reverseOrder();
List<Integer> nums = new ArrayList<>(Arrays.asList(3, 1, 2));
nums.sort(rev);
System.out.println(nums); // [3, 2, 1]
```

---

## 13. Arrays Utility Class

```java
import java.util.Arrays;

// sort
int[] arr = {5, 2, 8, 1, 9};
Arrays.sort(arr);
System.out.println(Arrays.toString(arr)); // [1, 2, 5, 8, 9]

// partial sort
Arrays.sort(arr, 1, 4); // sort indices 1 to 3 only

// sort with comparator (Object arrays only)
String[] words = {"Banana", "Apple", "Cherry"};
Arrays.sort(words, Comparator.reverseOrder());
System.out.println(Arrays.toString(words)); // [Cherry, Banana, Apple]

// binarySearch (array must be sorted)
int[] sorted = {1, 3, 5, 7, 9};
System.out.println(Arrays.binarySearch(sorted, 5)); // 2
System.out.println(Arrays.binarySearch(sorted, 4)); // negative (not found)

// equals
int[] a = {1, 2, 3};
int[] b = {1, 2, 3};
System.out.println(Arrays.equals(a, b)); // true

// deepEquals (for multidimensional)
int[][] x = {{1, 2}, {3, 4}};
int[][] y = {{1, 2}, {3, 4}};
System.out.println(Arrays.deepEquals(x, y)); // true

// fill
int[] filled = new int[5];
Arrays.fill(filled, 7);
System.out.println(Arrays.toString(filled)); // [7, 7, 7, 7, 7]

// fill partial range
Arrays.fill(filled, 1, 4, 0); // fill index 1..3 with 0
System.out.println(Arrays.toString(filled)); // [7, 0, 0, 0, 7]

// copyOf
int[] original = {1, 2, 3, 4, 5};
int[] copy = Arrays.copyOf(original, 3);
System.out.println(Arrays.toString(copy)); // [1, 2, 3]

int[] extended = Arrays.copyOf(original, 8); // pads with 0s
System.out.println(Arrays.toString(extended)); // [1, 2, 3, 4, 5, 0, 0, 0]

// copyOfRange
int[] range = Arrays.copyOfRange(original, 1, 4);
System.out.println(Arrays.toString(range)); // [2, 3, 4]

// asList — converts array to List (fixed-size)
String[] strArr = {"A", "B", "C"};
List<String> list = Arrays.asList(strArr);
// list.add("D"); // throws UnsupportedOperationException
list.set(0, "Z"); // ok
System.out.println(list); // [Z, B, C]

// For mutable list from array:
List<String> mutableList = new ArrayList<>(Arrays.asList(strArr));

// toString / deepToString
System.out.println(Arrays.toString(original));     // [1, 2, 3, 4, 5]
System.out.println(Arrays.deepToString(x));        // [[1, 2], [3, 4]]

// parallelSort (uses Fork/Join for large arrays, Java 8+)
int[] big = {9, 7, 5, 3, 1, 2, 4, 6, 8};
Arrays.parallelSort(big);
System.out.println(Arrays.toString(big)); // [1, 2, 3, 4, 5, 6, 7, 8, 9]

// stream (Java 8+)
int sum = Arrays.stream(original).sum();
System.out.println(sum); // 15

// setAll / parallelSetAll (Java 8+)
int[] gen = new int[5];
Arrays.setAll(gen, i -> i * i);
System.out.println(Arrays.toString(gen)); // [0, 1, 4, 9, 16]

// spliterator (Java 8+)
Arrays.spliterator(original);
```

---

## 14. Fail-Fast vs Fail-Safe Iterators

### Fail-Fast
- Throws `ConcurrentModificationException` if collection is **structurally modified** during iteration
- Uses an internal **modCount** to detect changes
- Examples: `ArrayList`, `HashMap`, `HashSet`, `LinkedList`

```java
List<String> list = new ArrayList<>(Arrays.asList("A", "B", "C"));

try {
    for (String s : list) {
        if (s.equals("B")) {
            list.remove(s); // ConcurrentModificationException!
        }
    }
} catch (ConcurrentModificationException e) {
    System.out.println("ConcurrentModificationException caught!");
}

// Safe alternative: use Iterator.remove()
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    if (it.next().equals("A")) {
        it.remove(); // safe
    }
}
System.out.println(list); // [B, C]

// Or: use removeIf (Java 8+)
list.removeIf(s -> s.equals("C"));
System.out.println(list); // [B]
```

### Fail-Safe
- Works on a **snapshot/copy** of the collection
- Does **NOT** throw `ConcurrentModificationException`
- Changes during iteration are **not visible**
- Examples: `CopyOnWriteArrayList`, `ConcurrentHashMap`

```java
import java.util.concurrent.CopyOnWriteArrayList;

CopyOnWriteArrayList<String> cowList = new CopyOnWriteArrayList<>(Arrays.asList("A", "B", "C"));

for (String s : cowList) {
    System.out.print(s + " ");
    cowList.add("X"); // no exception, but X not visible in this iteration
}
// Output: A B C

System.out.println(cowList); // [A, B, C, X, X, X]
```

---

## 15. Concurrent Collections

Found in `java.util.concurrent`.

### ConcurrentHashMap
- Thread-safe map, **no locking on reads** (segment locking / CAS in Java 8+)
- Does **NOT** allow null keys or null values
- Preferred over `Hashtable` and `synchronizedMap`

```java
import java.util.concurrent.ConcurrentHashMap;

ConcurrentHashMap<String, Integer> chm = new ConcurrentHashMap<>();

chm.put("A", 1);
chm.put("B", 2);
chm.put("C", 3);

System.out.println(chm.get("A")); // 1
System.out.println(chm.getOrDefault("Z", 0)); // 0

chm.putIfAbsent("D", 4);
chm.remove("A", 1); // atomic conditional remove

chm.compute("B", (k, v) -> v + 10);
System.out.println(chm.get("B")); // 12

chm.merge("C", 5, Integer::sum);
System.out.println(chm.get("C")); // 8

// forEach (parallel-friendly)
chm.forEach(1, (k, v) -> System.out.println(k + "=" + v));

// search
String found = chm.search(1, (k, v) -> v > 10 ? k : null);
System.out.println(found); // B

// reduce
int total = chm.reduceValues(1, Integer::sum);
System.out.println(total); // sum of all values
```

### CopyOnWriteArrayList
```java
import java.util.concurrent.CopyOnWriteArrayList;

CopyOnWriteArrayList<String> cowList = new CopyOnWriteArrayList<>();

cowList.add("A");
cowList.add("B");
cowList.addIfAbsent("A"); // won't add (already exists)
cowList.addIfAbsent("C"); // adds
System.out.println(cowList); // [A, B, C]

// All List methods work; mutations create new copy internally
```

### CopyOnWriteArraySet
```java
import java.util.concurrent.CopyOnWriteArraySet;

CopyOnWriteArraySet<Integer> cowSet = new CopyOnWriteArraySet<>();
cowSet.add(1); cowSet.add(2); cowSet.add(1); // duplicate ignored
System.out.println(cowSet); // [1, 2]
```

### ArrayBlockingQueue
```java
import java.util.concurrent.ArrayBlockingQueue;

ArrayBlockingQueue<String> abq = new ArrayBlockingQueue<>(3); // bounded

abq.put("A");   // blocks if full
abq.put("B");
abq.offer("C"); // returns false if full (non-blocking)

System.out.println(abq.take());   // A — blocks if empty
System.out.println(abq.poll());   // B — null if empty (non-blocking)
System.out.println(abq.peek());   // C — doesn't remove
```

### LinkedBlockingQueue
```java
import java.util.concurrent.LinkedBlockingQueue;

LinkedBlockingQueue<Integer> lbq = new LinkedBlockingQueue<>(10); // optionally bounded

lbq.put(1);
lbq.offer(2);
System.out.println(lbq.take());  // 1
System.out.println(lbq.poll()); // 2
```

### PriorityBlockingQueue
```java
import java.util.concurrent.PriorityBlockingQueue;

PriorityBlockingQueue<Integer> pbq = new PriorityBlockingQueue<>();
pbq.offer(30);
pbq.offer(10);
pbq.offer(20);
System.out.println(pbq.take()); // 10 (smallest first, blocks if empty)
```

---

## 16. Legacy Classes

| Class | Modern Replacement | Notes |
|---|---|---|
| `Vector` | `ArrayList` | Synchronized, slower |
| `Stack` | `ArrayDeque` | LIFO |
| `Hashtable` | `HashMap` / `ConcurrentHashMap` | Synchronized, no null |
| `Properties` | — | Extends Hashtable, for key=value config |
| `Enumeration` | `Iterator` | Legacy iterator |

### Properties (Special Use Case)
```java
import java.util.Properties;
import java.io.*;

Properties props = new Properties();

// setProperty / getProperty
props.setProperty("host", "localhost");
props.setProperty("port", "8080");
props.setProperty("db", "mydb");

System.out.println(props.getProperty("host")); // localhost
System.out.println(props.getProperty("user", "admin")); // admin (default)

// list all
props.list(System.out);

// Save to file
props.store(new FileWriter("config.properties"), "App Config");

// Load from file
Properties loaded = new Properties();
loaded.load(new FileReader("config.properties"));
System.out.println(loaded.getProperty("port")); // 8080

// propertyNames (Enumeration of keys)
Enumeration<?> names = props.propertyNames();
while (names.hasMoreElements()) System.out.println(names.nextElement());

// stringPropertyNames (Set<String>)
System.out.println(props.stringPropertyNames()); // [host, port, db]
```

---

## 17. Java 8+ Stream with Collections

```java
import java.util.*;
import java.util.stream.*;

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// filter
List<Integer> evens = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
System.out.println(evens); // [2, 4, 6, 8, 10]

// map
List<Integer> squares = numbers.stream()
    .map(n -> n * n)
    .collect(Collectors.toList());
System.out.println(squares); // [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

// reduce
int sum = numbers.stream().reduce(0, Integer::sum);
System.out.println(sum); // 55

// collect to different structures
Set<Integer> set = numbers.stream().collect(Collectors.toSet());
Map<Integer, Integer> map = numbers.stream()
    .collect(Collectors.toMap(n -> n, n -> n * n));

// groupingBy
List<String> words = Arrays.asList("apple", "ant", "banana", "avocado", "blueberry");
Map<Character, List<String>> grouped = words.stream()
    .collect(Collectors.groupingBy(w -> w.charAt(0)));
System.out.println(grouped);
// {a=[apple, ant, avocado], b=[banana, blueberry]}

// counting
Map<Character, Long> counted = words.stream()
    .collect(Collectors.groupingBy(w -> w.charAt(0), Collectors.counting()));
System.out.println(counted); // {a=3, b=2}

// joining
String joined = words.stream().collect(Collectors.joining(", ", "[", "]"));
System.out.println(joined); // [apple, ant, banana, avocado, blueberry]

// sorted
List<Integer> sorted = numbers.stream().sorted(Comparator.reverseOrder())
    .collect(Collectors.toList());
System.out.println(sorted); // [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

// distinct
List<Integer> dupes = Arrays.asList(1, 2, 2, 3, 3, 3);
List<Integer> distinct = dupes.stream().distinct().collect(Collectors.toList());
System.out.println(distinct); // [1, 2, 3]

// flatMap
List<List<Integer>> nested = Arrays.asList(
    Arrays.asList(1, 2, 3),
    Arrays.asList(4, 5, 6)
);
List<Integer> flat = nested.stream()
    .flatMap(Collection::stream)
    .collect(Collectors.toList());
System.out.println(flat); // [1, 2, 3, 4, 5, 6]

// anyMatch / allMatch / noneMatch
System.out.println(numbers.stream().anyMatch(n -> n > 9));  // true
System.out.println(numbers.stream().allMatch(n -> n > 0));  // true
System.out.println(numbers.stream().noneMatch(n -> n > 10)); // true

// findFirst / findAny
Optional<Integer> first = numbers.stream().filter(n -> n > 5).findFirst();
System.out.println(first.get()); // 6

// min / max
Optional<Integer> min = numbers.stream().min(Integer::compareTo);
Optional<Integer> max = numbers.stream().max(Integer::compareTo);
System.out.println(min.get() + " " + max.get()); // 1 10

// count
long count = numbers.stream().filter(n -> n % 2 == 0).count();
System.out.println(count); // 5

// toUnmodifiableList / toUnmodifiableSet / toUnmodifiableMap (Java 10+)
List<Integer> unmodifiable = numbers.stream().collect(Collectors.toUnmodifiableList());

// Statistics
IntSummaryStatistics stats = numbers.stream()
    .mapToInt(Integer::intValue).summaryStatistics();
System.out.println(stats.getSum());     // 55
System.out.println(stats.getAverage()); // 5.5
System.out.println(stats.getMin());     // 1
System.out.println(stats.getMax());     // 10
System.out.println(stats.getCount());   // 10
```

---

## 18. Generics in Collections

Generics provide **compile-time type safety** and eliminate casting.

```java
// Without generics (raw type — avoid)
List list = new ArrayList();
list.add("hello");
String s = (String) list.get(0); // explicit cast needed

// With generics
List<String> typed = new ArrayList<>();
typed.add("hello");
String t = typed.get(0); // no cast needed

// Bounded type parameters
// <T extends Number> — T must be Number or subclass
public static <T extends Number> double sum(List<T> list) {
    double total = 0;
    for (T num : list) total += num.doubleValue();
    return total;
}

// Wildcards
// ? — unknown type
// ? extends T — upper bounded (T or subtype)
// ? super T — lower bounded (T or supertype)

// Upper bounded: read from list (covariant)
public static double sumList(List<? extends Number> list) {
    return list.stream().mapToDouble(Number::doubleValue).sum();
}

List<Integer> ints = Arrays.asList(1, 2, 3);
List<Double> doubles = Arrays.asList(1.1, 2.2, 3.3);
System.out.println(sumList(ints));    // 6.0
System.out.println(sumList(doubles)); // 6.6

// Lower bounded: write to list (contravariant)
public static void addNumbers(List<? super Integer> list) {
    list.add(1);
    list.add(2);
    list.add(3);
}

List<Number> numList = new ArrayList<>();
addNumbers(numList);
System.out.println(numList); // [1, 2, 3]

// PECS — Producer Extends, Consumer Super
// Use <? extends T> when reading (producing values)
// Use <? super T> when writing (consuming values)
```

---

## 19. Unmodifiable & Immutable Collections

### Unmodifiable (wraps existing)
```java
List<String> mutable = new ArrayList<>(Arrays.asList("A", "B", "C"));
List<String> unmod = Collections.unmodifiableList(mutable);

// unmod.add("D"); // UnsupportedOperationException
// BUT changes to mutable ARE reflected in unmod:
mutable.add("D");
System.out.println(unmod); // [A, B, C, D]
```

### Immutable (Java 9+ `List.of`, `Set.of`, `Map.of`)
```java
// List.of — truly immutable, no null allowed
List<String> immList = List.of("A", "B", "C");
// immList.add("D"); // UnsupportedOperationException
// immList.set(0, "Z"); // UnsupportedOperationException

// Set.of — truly immutable, no null, no duplicates
Set<String> immSet = Set.of("X", "Y", "Z");

// Map.of — up to 10 key-value pairs
Map<String, Integer> immMap = Map.of("a", 1, "b", 2, "c", 3);

// Map.ofEntries — for more than 10 pairs
Map<String, Integer> bigMap = Map.ofEntries(
    Map.entry("key1", 1),
    Map.entry("key2", 2)
);

// List.copyOf / Set.copyOf / Map.copyOf (Java 10+)
List<String> original = new ArrayList<>(Arrays.asList("A", "B"));
List<String> copied = List.copyOf(original);
// copied is immutable; changes to original don't affect copied
original.add("C");
System.out.println(copied); // [A, B]
```

---

## 20. Performance Comparison Table

### List Implementations
| Operation | ArrayList | LinkedList | Vector |
|---|---|---|---|
| get(i) | O(1) | O(n) | O(1) |
| add(end) | O(1) amortized | O(1) | O(1) amortized |
| add(middle) | O(n) | O(n) | O(n) |
| remove(end) | O(1) | O(1) | O(1) |
| remove(middle) | O(n) | O(n) | O(n) |
| search | O(n) | O(n) | O(n) |
| Memory | Low | High (pointers) | Low |
| Thread-safe | No | No | Yes |

### Set Implementations
| Operation | HashSet | LinkedHashSet | TreeSet |
|---|---|---|---|
| add | O(1) avg | O(1) avg | O(log n) |
| remove | O(1) avg | O(1) avg | O(log n) |
| contains | O(1) avg | O(1) avg | O(log n) |
| Ordering | None | Insertion | Sorted |
| Null | One | One | No |

### Map Implementations
| Operation | HashMap | LinkedHashMap | TreeMap | Hashtable |
|---|---|---|---|---|
| get | O(1) avg | O(1) avg | O(log n) | O(1) avg |
| put | O(1) avg | O(1) avg | O(log n) | O(1) avg |
| remove | O(1) avg | O(1) avg | O(log n) | O(1) avg |
| Ordering | None | Insertion | Sorted | None |
| Null key | Yes (1) | Yes (1) | No | No |
| Null value | Yes | Yes | Yes | No |
| Thread-safe | No | No | No | Yes |

### When to Use What
| Use Case | Best Choice |
|---|---|
| General list, fast random access | `ArrayList` |
| Frequent insertions at head/tail | `LinkedList` or `ArrayDeque` |
| LIFO stack | `ArrayDeque` |
| FIFO queue | `ArrayDeque` or `LinkedList` |
| Priority-based processing | `PriorityQueue` |
| Unique elements, fast lookup | `HashSet` |
| Unique elements, insertion order | `LinkedHashSet` |
| Unique elements, sorted | `TreeSet` |
| Key-value, fast lookup | `HashMap` |
| Key-value, insertion order | `LinkedHashMap` |
| Key-value, sorted keys | `TreeMap` |
| Thread-safe map | `ConcurrentHashMap` |
| Thread-safe list, rare writes | `CopyOnWriteArrayList` |
| Enum keys | `EnumMap` |
| Config/properties | `Properties` |

---

*End of Java Collections Framework Notes*
