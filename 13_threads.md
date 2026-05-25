# Threads in Java – Complete Notes

---

# 1. What is a Thread?

A Thread is a lightweight sub-process.

It allows multiple tasks to execute concurrently inside a program.

Example:
- Music player running while downloading files
- Browser opening multiple tabs

Java supports multithreading using:

```java
java.lang.Thread
```

---

# 2. Why Multithreading?

Advantages:
- Better CPU utilization
- Faster execution
- Concurrent operations
- Responsive applications
- Background processing

---

# 3. Process vs Thread

| Process | Thread |
|---|---|
| Heavyweight | Lightweight |
| Separate memory | Shared memory |
| Slower | Faster |
| Independent | Part of process |

---

# 4. Ways to Create Thread

There are 2 main ways:

1. Extending Thread class
2. Implementing Runnable interface

---

# 5. Creating Thread by Extending Thread Class

```java
class MyThread extends Thread {

    public void run() {

        System.out.println("Thread running");
    }

    public static void main(String[] args) {

        MyThread t = new MyThread();

        t.start();
    }
}
```

---

# 6. Creating Thread using Runnable Interface

Runnable is preferred approach.

```java
class MyRunnable implements Runnable {

    public void run() {

        System.out.println("Runnable thread");
    }

    public static void main(String[] args) {

        MyRunnable obj = new MyRunnable();

        Thread t = new Thread(obj);

        t.start();
    }
}
```

---

# 7. Runnable Interface

Runnable is a Functional Interface.

Package:

```java
java.lang
```

Method:

```java
public abstract void run();
```

Advantages:
- Better design
- Supports multiple inheritance
- Loose coupling

---

# 8. Functional Interface

Interface with only one abstract method.

Example:

```java
Runnable
Callable
Comparator
```

Because Runnable is functional,
Lambda Expression can be used.

---

# 9. run() Method

`run()` contains thread task.

Example:

```java
public void run() {

    System.out.println("Inside run");
}
```

Important:
- Calling `run()` directly does NOT create new thread

---

# 10. start() Method

`start()` creates new thread internally.

Syntax:

```java
t.start();
```

Flow:

```text
start()
   ↓
new thread created
   ↓
run() executed
```

Important:
- Thread can start only once
- Calling again causes:

```java
IllegalThreadStateException
```

---

# 11. run() vs start()

| run() | start() |
|---|---|
| Normal method | Creates new thread |
| No concurrency | Concurrent execution |
| Current thread executes | New thread executes |
| No scheduler | Uses scheduler |

Example:

```java
t.run();   // normal call
t.start(); // new thread
```

---

# 12. Thread Life Cycle / States

Thread passes through different states.

States:

1. NEW
2. RUNNABLE
3. RUNNING
4. BLOCKED
5. WAITING
6. TIMED_WAITING
7. TERMINATED

---

# 13. NEW State

Thread object created but not started.

```java
Thread t = new Thread();
```

State:

```java
NEW
```

---

# 14. RUNNABLE State

After calling:

```java
start()
```

Thread becomes ready for execution.

```text
NEW → RUNNABLE
```

---

# 15. RUNNING State

Scheduler selects thread for execution.

```text
RUNNABLE → RUNNING
```

Thread executes `run()`.

---

# 16. BLOCKED State

Thread waiting for monitor lock.

Occurs with synchronized methods/blocks.

Example:

```java
synchronized void display() {

}
```

---

# 17. WAITING State

Thread waits indefinitely.

Methods:
- join()
- wait()

Example:

```java
t.join();
```

---

# 18. TIMED_WAITING State

Thread waits for specified time.

Methods:
- sleep()
- join(time)
- wait(time)

Example:

```java
Thread.sleep(1000);
```

---

# 19. TERMINATED State

Thread execution completed.

```text
RUNNING → TERMINATED
```

Thread cannot restart.

---

# 20. Thread Lifecycle Diagram

```text
                start()
NEW ----------------------------> RUNNABLE
                                     |
                                     |
                              CPU Scheduler
                                     |
                                     v
                                 RUNNING
                              /    |      \
                             /     |       \
                            v      v        v
                      BLOCKED WAITING TIMED_WAITING
                             \      |      /
                              \     |     /
                                   v
                               RUNNABLE
                                   |
                                   v
                              TERMINATED
```

---

# 21. sleep()

Pauses current thread for specified time.

Syntax:

```java
Thread.sleep(milliseconds);
```

Example:

```java
for(int i=1;i<=5;i++) {

    System.out.println(i);

    Thread.sleep(1000);
}
```

Important:
- Static method
- Throws checked exception

```java
InterruptedException
```

---

# 22. join()

Waits for another thread completion.

Example:

```java
t1.join();
```

Meaning:
Main thread waits until `t1` completes.

---

# 23. Thread Priority

Priority gives scheduling preference.

Range:

| Constant | Value |
|---|---|
| MIN_PRIORITY | 1 |
| NORM_PRIORITY | 5 |
| MAX_PRIORITY | 10 |

Example:

```java
t1.setPriority(10);
```

Get priority:

```java
t1.getPriority();
```

Important:
Higher priority does not guarantee execution first.

---

# 24. currentThread()

Returns currently executing thread.

Example:

```java
Thread t = Thread.currentThread();

System.out.println(t.getName());
```

---

# 25. Thread Naming

Set name:

```java
t.setName("Worker");
```

Get name:

```java
t.getName();
```

---

# 26. Lambda Expression with Threads

Runnable is functional interface,
so Lambda can be used.

Example:

```java
Runnable r = () -> {

    System.out.println("Thread running");
};

Thread t = new Thread(r);

t.start();
```

Short form:

```java
new Thread(() -> {

    System.out.println("Hello");

}).start();
```

---

# 27. Thread Scheduler

Scheduler decides:
- Which thread executes
- When thread executes

Depends on:
- JVM
- Operating System

Execution order is unpredictable.

---

# 28. Race Condition

Occurs when:
Multiple threads modify shared data simultaneously.

Causes inconsistent results.

Example:

```java
class Counter {

    int count = 0;

    void increment() {

        count++;
    }
}
```

Two threads updating same variable may produce wrong output.

---

# 29. Shared Mutable State

Mutable means data can change.

Example:

```java
count++;
list.add(10);
name = "Ram";
```

Shared mutable state causes:
- Race conditions
- Data inconsistency

---

# 30. Thread Safe

Thread-safe means:
Multiple threads access resource safely.

No inconsistent data.

---

# 31. Synchronization

Synchronization controls access to shared resource.

Purpose:
- Prevent race condition
- Ensure consistency

---

# 32. synchronized Method

```java
synchronized void increment() {

    count++;
}
```

Only one thread executes at a time.

---

# 33. synchronized Block

```java
synchronized(this) {

    count++;
}
```

---

# 34. Race Condition Example

```java
class Counter {

    int count = 0;

    synchronized void increment() {

        count++;
    }
}

public class Demo {

    public static void main(String[] args)
            throws Exception {

        Counter c = new Counter();

        Thread t1 = new Thread(() -> {

            for(int i=0;i<1000;i++) {

                c.increment();
            }
        });

        Thread t2 = new Thread(() -> {

            for(int i=0;i<1000;i++) {

                c.increment();
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println(c.count);
    }
}
```

---

# 35. Immutable Objects

Immutable object cannot change after creation.

Example:

```java
String
```

Benefits:
- Automatically thread-safe
- No synchronization needed

---

# 36. Daemon Thread

Background thread.

Example:
- Garbage Collector

Set daemon:

```java
t.setDaemon(true);
```

Check:

```java
t.isDaemon();
```

---

# 37. yield()

Temporarily pauses current thread.

```java
Thread.yield();
```

Gives chance to other threads.

No guarantee.

---

# 38. interrupt()

Interrupts sleeping/waiting thread.

```java
t.interrupt();
```

---

# 39. Deadlock

Deadlock occurs when:
Two threads wait for each other forever.

Example:

```text
Thread-1 waiting for Thread-2 lock
Thread-2 waiting for Thread-1 lock
```

Program freezes.

---

# 40. Inter Thread Communication

Threads communicate using:

- wait()
- notify()
- notifyAll()

---

# 41. wait()

Releases lock and waits.

```java
wait();
```

Must be inside synchronized block.

---

# 42. notify()

Wakes one waiting thread.

```java
notify();
```

---

# 43. notifyAll()

Wakes all waiting threads.

```java
notifyAll();
```

---

# 44. Executor Framework

Modern way to manage threads.

Package:

```java
java.util.concurrent
```

Example:

```java
ExecutorService service =
    Executors.newFixedThreadPool(3);
```

Benefits:
- Better thread management
- Reusable threads
- Performance improvement

---

# 45. Callable Interface

Similar to Runnable but:
- Returns value
- Can throw exception

Example:

```java
Callable<Integer>
```

Method:

```java
call()
```

---

# 46. Future Interface

Used to get result from Callable.

Example:

```java
Future<Integer> result
```

---

# 47. Thread Pool

Collection of reusable threads.

Advantages:
- Faster
- Less memory usage
- Better performance

---

# 48. Important Interview Questions

## Q1. Difference between Thread and Runnable?

| Thread | Runnable |
|---|---|
| Class | Interface |
| Single inheritance issue | Better approach |
| Tight coupling | Loose coupling |

---

## Q2. Difference between start() and run()?

| start() | run() |
|---|---|
| Creates new thread | Normal method |
| Concurrent execution | Sequential execution |

---

## Q3. What is race condition?

Multiple threads modifying shared data simultaneously causing inconsistent results.

---

## Q4. What is thread-safe?

Safe concurrent access by multiple threads.

---

## Q5. Why String is thread-safe?

Because String is immutable.

---

## Q6. Can we restart thread?

No.

Calling `start()` again causes:

```java
IllegalThreadStateException
```

---

# 49. Important Exceptions

| Exception | Reason |
|---|---|
| InterruptedException | sleep(), join(), wait() |
| IllegalThreadStateException | starting thread again |

---

# 50. Important Methods Summary

| Method | Purpose |
|---|---|
| start() | Starts thread |
| run() | Thread task |
| sleep() | Pause thread |
| join() | Wait for thread |
| yield() | Pause temporarily |
| interrupt() | Interrupt thread |
| setPriority() | Set priority |
| getPriority() | Get priority |
| currentThread() | Current thread |

---

# 51. Real World Examples

| Concept | Example |
|---|---|
| Multithreading | Browser tabs |
| Daemon Thread | Garbage Collector |
| Race Condition | Multiple ATM withdrawals |
| Synchronization | Banking system |
| Thread Pool | Web servers |

---

# 52. Final Summary

Java Threads are used for concurrent programming.

Most Important Topics:
- Thread creation
- Runnable
- start()
- run()
- sleep()
- join()
- thread states
- synchronization
- race condition
- thread safety
- lambda threads
- daemon thread
- deadlock
- executor framework

These concepts are important for:
- Interviews
- Backend development
- Java applications
- High-performance systems
