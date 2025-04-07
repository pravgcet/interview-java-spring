# Wrapper Classes in Java

In Java, **wrapper classes** are used to convert **primitive data types** into **objects**. This is especially useful when working with **collections** that only work with objects (like `ArrayList`, `HashMap`, etc.).

---

## Primitive Types vs Wrapper Classes

| Primitive Type | Wrapper Class |
| -------------- | ------------- |
| `byte`         | `Byte`        |
| `short`        | `Short`       |
| `int`          | `Integer`     |
| `long`         | `Long`        |
| `float`        | `Float`       |
| `double`       | `Double`      |
| `char`         | `Character`   |
| `boolean`      | `Boolean`     |

---

## Autoboxing & Unboxing

### Autoboxing

- Automatic conversion of **primitive to wrapper object**.

```java
int a = 10;
Integer obj = a;  // Autoboxing
```

### Unboxing

Automatic conversion of wrapper object to primitive.

```java
Integer obj = 20;
int b = obj;  // Unboxing
```

### Example: Wrapper in Collections

```java
public class WrapperDemo {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(10);  // Autoboxing int to Integer
        list.add(20);

        int a = list.get(0);  // Unboxing Integer to int
        System.out.println(a);  // Output: 10
    }
}
```

### Why Use Wrapper Classes?

- Required for working with collections (like ArrayList, HashMap)
- Provide utility methods (e.g., Integer.parseInt())
- Useful in generics (which work with objects, not primitives)

### Common Methods

#### Integer

```java
Integer.parseInt("123"); // Converts String to int
Integer.toString(100); // Converts int to String
```

#### Boolean

```java
Boolean.parseBoolean("true"); // Converts String to boolean
```

###Summary
Feature |Wrapper Classes
---|---
Purpose |Convert primitives to objects
Use Cases |Collections, Generics, APIs
Key Concepts |Autoboxing & Unboxing
Extra Functionality |Utility methods (parse, valueOf, etc)

### Note

- Wrapper classes are immutable
- Use primitive types when performance is critical
