## Interview Questions

**1. Explain the internals of HashMap.**

A `HashMap<K, V>` stores key-value pairs and offers **O(1)** average time complexity for `put()`, `get()`, and `remove()` operations. It allows `null` keys and values.

---

#### Internal Structure

- HashMap uses an **array of buckets**
- Each bucket can contain a **linked list** or a **Red-Black Tree** (Java 8+)
- Each entry is stored in a `Node` object

---

#### Hashing

1. **Hash Code Calculation and index calculation**
   ```java
   int hash = key.hashCode();
   int index = (n - 1) & hash;
   ```

#### Collision Handling

1. Linked List (Java 7 or small buckets)
   If two keys map to the same index, they're stored in a list.

2. Tree (Java 8+, bucket size > 8)
   Bucket converts to a Red-Black Tree to improve performance from O(n) to O(log n).

#### Resizing

- Triggered when size >= capacity \* load factor (default load factor = 0.75)

- HashMap doubles its size and rehashes all entries

- This is an expensive operation

#### How put() and get() Work

**1. put(key, value)**

1.  Compute hash
2.  Find bucket index
3.  Add node to bucket (or update if key exists)
4.  If bucket size > 8, convert to tree

**2. get(key)**

1. Compute hash
2. Go to the corresponding bucket
3. Search for key in list/tree

#### Importance of equals() and hashCode()

To work correctly, key objects must override:

- hashCode(): for bucket selection
- equals(): for key comparison within a bucket

**2. Explain default Methods in Java.**

Introduced in **Java 8**, default methods allow **interfaces** to have **concrete methods with a body**.

This helps interfaces evolve without breaking existing implementations.

---

#### Syntax

```java
public interface MyInterface {
    void abstractMethod(); // still abstract

    default void defaultMethod() {
        System.out.println("This is a default method.");
    }
}
```

#### Key Features

- Use the default keyword
- Can be overridden by implementing classes
- Can call other methods (even private methods in Java 9+)
- Work alongside abstract methods

#### Multiple Inheritance Conflict

If a class implements two interfaces with the same default method, it must override the method to resolve ambiguity:

```java
interface A {
    default void sayHello() {
        System.out.println("Hello from A");
    }
}

interface B {
    default void sayHello() {
        System.out.println("Hello from B");
    }
}

class C implements A, B {
    public void sayHello() {
        A.super.sayHello(); // or B.super.sayHello();
    }
}

```

**3. Difference between Interface and abstract class.**

Interfaces provides a contract that implementing classes have to adhere to whereas abstract classes provide basic functionality to the implementing classes.

**4. Explain method overloading and overriding with example.**

Java supports both **method overloading** and **method overriding** as part of polymorphism. Here's a breakdown of both concepts with examples.

#### Method Overloading

Method Overloading means defining **multiple methods with the same name** in the same class but with **different parameters** (type, number, or order).

#### Rules

- Must have **different parameter lists**
- Can have different return types
- Happens **within the same class**
- Is resolved at **compile time** (static polymorphism)

#### Example

```java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

#### Method Overriding

Method Overriding means redefining a method in a subclass that already exists in the superclass with the same signature (name + parameters).

#### Rules

- Must have the same method name, parameters, and return type

- The method in the subclass must have the same or more accessible modifier

- The method in the superclass must not be private, final, or static

- Happens across inheritance hierarchy

- Is resolved at runtime (dynamic polymorphism)

**5. Can constructors be marked as Final?**

No, constructors cannot be declared final.

The final keyword in Java is used to prevent method overriding in subclasses.

But:

- Constructors are never inherited, and
- They are not subject to overriding like methods are.
- So marking them final has no meaning, and Java does not allow it.

```java
class Example {
    final Example() {  // Compilation error
        System.out.println("Constructor");
    }
}
```

**6. Can static methods be overriden?**

Short Answer: No, static methods **cannot** be overridden.

In Java, static methods belong to the **class**, not the instance. That means they are **not part of the object's dynamic behavior** and are **not polymorphic**.

If you define a static method in a subclass with the same signature as in the parent class, it's called **method hiding**, not overriding.

---

#### Method Hiding vs Overriding

| Feature          | Static Method (`hidden`) | Instance Method (`overridden`) |
| ---------------- | ------------------------ | ------------------------------ |
| Belongs to       | Class                    | Object (instance)              |
| Polymorphism     | No                       | Yes                            |
| Resolution time  | Compile-time             | Runtime                        |
| Keywords allowed | `static` only in hiding  | `@Override` in overriding      |

---

#### Example

```java
class Parent {
    static void display() {
        System.out.println("Static method in Parent");
    }
}

class Child extends Parent {
    static void display() {
        System.out.println("Static method in Child");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent obj = new Child();
        obj.display();  // Output: Static method in Parent
    }
}
```

**7. Difference between == and .equals().**

# Difference Between `==` and `.equals()` in Java

In Java, both `==` and `.equals()` are used to compare values, but they behave differently depending on **whether you're dealing with primitives or objects**.

---

## `==` Operator

### Definition:

- Compares **primitive values** or **object references** (memory addresses).

### Use Cases:

- Use with **primitive types** (int, float, char, etc.)
- Use with objects only when you want to check if **both references point to the same object**.

### Example:

```java
int a = 5;
int b = 5;
System.out.println(a == b); // true (value comparison)

String s1 = new String("hello");
String s2 = new String("hello");
System.out.println(s1 == s2); // false (different objects)
```

### .equals() Method

- Defined in Object class and overridden by many classes (e.g., String, List, etc.)

- Compares object content or logical equality.

#### Use Cases:

Use when comparing the contents of objects.

#### Example:

```java
String s1 = new String("hello");
String s2 = new String("hello");
System.out.println(s1.equals(s2)); // true (content is same)
```

---

### Summary Table

| Feature          | ==                   | .equals()                |
| ---------------- | -------------------- | ------------------------ |
| Type             | Operator             | Method                   |
| Checks           | Reference equality   | Content/logical equality |
| Works on         | Primitives & Objects | Objects only             |
| Overridable      | No                   | Yes (can be overridden)  |
| Example (String) | s1 == s2 → false     | s1.equals(s2) → true     |

### Note:

If .equals() is not overridden in a class, it behaves like == (default implementation in Object compares references).
