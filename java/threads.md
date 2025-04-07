# Thread and Its Lifecycle in Java

In Java, a **thread** is a lightweight subprocess that enables **multitasking**. Threads run concurrently and share the same memory space.

---

## What is a Thread?

A thread represents a **path of execution** in a program. Java supports threads via:

- `Thread` class (extends)
- `Runnable` interface (implements)

---

## Thread Lifecycle in Java

A Java thread can exist in one of the following **states**:

### 1. `NEW`

- A thread is in this state after it is created using the `Thread` class but **not yet started**.

```java
Thread t = new Thread();
```

### 2. `RUNNABLE`

- After invoking `.start()`, the thread moves to **Runnable** state and is **ready to run**, but the actual execution depends on the thread scheduler.

```java
t.start();
```

### 3. `RUNNING`

- The thread is actually **executing**.

> Note: In Java, `RUNNING` is considered part of `RUNNABLE` by the Thread class.

### 4. `BLOCKED`

- A thread is waiting to acquire a lock on an object.

### 5. `WAITING`

- The thread is **waiting indefinitely** for another thread to perform a particular action (e.g., using `join()` or `wait()`).

### 6. `TIMED_WAITING`

- The thread is **waiting for a specified amount of time** (e.g., `sleep(time)` or `join(time)`).

### 7. `TERMINATED`

- The thread has **completed** its execution or was **abruptly stopped**.

---

## 🗺️ Thread Lifecycle Diagram

```text
        +-----------------+
        |     New         |
        +-----------------+
                 |
                 v
        +-----------------+
        |   Runnable      |<----+
        +-----------------+     |
                 |              |
                 v              |
        +-----------------+     |
        |   Running       |     |
        +-----------------+     |
          |     |     |         |
          v     v     v         |
   +--------+ +--------+ +------------+
   |Blocked| |Waiting | |TimedWaiting|
   +--------+ +--------+ +------------+
          \     |     //
           \    v    //
            +----------+
            | Terminated|
            +----------+
```

---

## Example

```java
public class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running...");
    }

    public static void main(String[] args) {
        MyThread t1 = new MyThread(); // New state
        t1.start();                   // Runnable -> Running
    }
}
```

---

## Summary

| State         | Description                           |
| ------------- | ------------------------------------- |
| NEW           | Thread is created but not yet started |
| RUNNABLE      | Thread is ready to run                |
| RUNNING       | Thread is executing                   |
| BLOCKED       | Thread is blocked, waiting for a lock |
| WAITING       | Thread waits indefinitely             |
| TIMED_WAITING | Thread waits for a specified time     |
| TERMINATED    | Thread has finished execution         |

---

## Thread API Highlights

- `start()` – Starts the thread
- `run()` – Defines thread behavior
- `sleep(ms)` – Pauses execution for `ms` milliseconds
- `join()` – Waits for the thread to die
- `interrupt()` – Interrupts the thread

## thread.run() will run the thread in calling thread.
