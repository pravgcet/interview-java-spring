# 🗑️ Garbage Collection in Java (Latest - Java 17+)

Java provides **automatic memory management** through a process called **Garbage Collection (GC)**. The GC is responsible for freeing up memory used by objects that are no longer reachable in the program.

---

## What Is Garbage Collection?

Garbage Collection is the process of:

- **Identifying** unused (unreachable) objects
- **Reclaiming** memory used by those objects
- **Compacting** the heap to reduce fragmentation (in some collectors)

---

## How Java GC Works (High-Level)

1. **Heap Memory** is where objects are stored.
2. The heap is divided into:
   - **Young Generation** (new objects)
     - Eden
     - Survivor Spaces (S0 and S1)
   - **Old Generation** (long-lived objects)
3. When memory is full in the **Young Gen**, a **Minor GC** occurs.
4. When memory is full in the **Old Gen**, a **Major GC (Full GC)** occurs.

---

## GC Process Flow

1. **Allocation**: New objects are created in the **Eden** space.
2. **Minor GC**: Moves surviving objects to **Survivor spaces**, then to **Old Gen** if they age enough.
3. **Major GC / Full GC**: Cleans up **Old Gen** and possibly compacts the heap.

---

## Latest GC Algorithms (Java 17+)

### 1. **G1 (Garbage-First) Collector**

- Default in Java 9–16
- Divides the heap into regions (not fixed generations)
- Performs concurrent and incremental collection
- Tries to avoid long pause times

### 2. **ZGC (Z Garbage Collector)**

- Ultra-low pause time GC
- Scales to multi-terabyte heaps
- Most of the GC runs concurrently with the application

```sh
# Enable ZGC
-XX:+UseZGC
```

### 3. **Shenandoah GC**

- Low-pause-time collector similar to ZGC
- Also concurrent and pause-optimized

```sh
# Enable Shenandoah
-XX:+UseShenandoahGC
```

### 4. **Serial & Parallel GC (Legacy)**

- Serial: Single-threaded, for small apps
- Parallel: Multi-threaded, focuses on throughput

---

## 🔍 Reference Types in GC

| Type              | Description                    | Eligible for GC?            |
| ----------------- | ------------------------------ | --------------------------- |
| Strong Reference  | Default reference (`new`)      | ❌ Not eligible             |
| Weak Reference    | Collected during next GC cycle | ✅ Yes                      |
| Soft Reference    | Collected if memory is low     | ✅ Yes                      |
| Phantom Reference | Used for post-mortem cleanup   | ✅ Yes (after finalization) |

---

## GC Monitoring Tools

- `jstat` - GC stats from CLI
- `jvisualvm` - GUI monitoring tool
- `Java Flight Recorder` + `Mission Control`

---

## Example: Forcing GC

```java
public class GCExample {
    public static void main(String[] args) {
        Object obj = new Object();
        obj = null; // Remove strong reference

        System.gc(); // Suggests JVM to perform GC
    }
}
```

> Note: `System.gc()` is only a suggestion. The JVM may ignore it.

---

## Summary

- Java automatically reclaims memory using GC.
- Modern GCs (like G1, ZGC, Shenandoah) are optimized for low pause and high throughput.
- Choose a GC based on app size, pause sensitivity, and performance goals.

---

## Helpful GC JVM Flags

```sh
-XX:+UseG1GC              # Use G1 GC
-XX:+UseZGC               # Use Z Garbage Collector
-XX:+UseShenandoahGC      # Use Shenandoah GC
-XX:+PrintGCDetails       # Print GC details to console
-verbose:gc               # Print basic GC logs
-Xlog:gc*                 # Java 9+ unified logging for GC
```
