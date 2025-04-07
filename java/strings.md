# String, StringBuffer, and StringBuilder in Java

Java provides three main classes to handle and manipulate strings: `String`, `StringBuffer`, and `StringBuilder`. Each serves a different purpose with respect to **mutability**, **performance**, and **thread safety**.

---

## 1️⃣ String

### Overview

- **Immutable**: Once a `String` object is created, it **cannot be changed**.
- Any operation that modifies the string (e.g., concatenation) returns a **new object**.

### Usage

```java
String str = "Hello";
str = str + " World";  // Creates a new String object
```

### Characteristics

- Stored in the **String Pool**
- Thread-safe due to immutability
- Slow for frequent modifications

---

## 2️⃣ StringBuffer

### Overview

- **Mutable**: Content can be changed after creation.
- **Thread-safe**: All methods are synchronized, so it is **safe to use in multi-threaded environments**.

### Usage

```java
StringBuffer sb = new StringBuffer("Hello");
sb.append(" World");  // Modifies the same object
System.out.println(sb);  // Output: Hello World
```

### Characteristics

- Slightly slower than `StringBuilder` due to synchronization
- Best suited for **multi-threaded applications** requiring safe string manipulation

---

## 3️⃣ StringBuilder

### Overview

- Also **mutable**, like `StringBuffer`
- **Not thread-safe**, but **faster** than `StringBuffer`
- Ideal for **single-threaded applications** or local string manipulations

### Usage

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
System.out.println(sb);  // Output: Hello World
```

### Characteristics

- High performance in non-concurrent scenarios
- Recommended for **local string modifications**

---

## Comparison Table

| Feature     | `String`            | `StringBuffer`         | `StringBuilder`         |
| ----------- | ------------------- | ---------------------- | ----------------------- |
| Mutability  | Immutable           | Mutable                | Mutable                 |
| Thread-safe | Yes (implicitly)    | Yes (synchronized)     | No                      |
| Performance | Slow (for changes)  | Slower (due to sync)   | Fastest (no sync)       |
| Use Case    | Fixed/constant data | Multi-threaded updates | Single-threaded updates |
| Package     | `java.lang`         | `java.lang`            | `java.lang`             |

---

## Quick Example Comparison

```java
public class StringComparison {
    public static void main(String[] args) {
        String s = "Hello";
        s = s.concat(" World");  // New object created

        StringBuffer sbf = new StringBuffer("Hello");
        sbf.append(" World");    // Same object modified

        StringBuilder sbd = new StringBuilder("Hello");
        sbd.append(" World");    // Same object modified

        System.out.println(s);   // Hello World
        System.out.println(sbf); // Hello World
        System.out.println(sbd); // Hello World
    }
}
```

---

## Summary

- Use `String` when content doesn't change.
- Use `StringBuffer` when working with strings in **multi-threaded environments**.
- Use `StringBuilder` for **better performance in single-threaded** environments.
