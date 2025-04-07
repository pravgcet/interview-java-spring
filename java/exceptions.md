# Exceptions in Java

In Java, **exceptions** are events that disrupt the normal flow of a program. They are used to handle errors gracefully during runtime.

---

## What is an Exception?

An exception is an **object** that represents an error or abnormal condition.

All exceptions are subclasses of the `Throwable` class.

---

## Checked vs Unchecked Exceptions

### Checked Exceptions

- Checked at **compile-time**
- Must be either **caught** using `try-catch` or **declared** with `throws`
- Typically represent **recoverable** conditions

**Examples**:

- `IOException`
- `SQLException`
- `FileNotFoundException`

```java
public void readFile(String path) throws IOException {
    FileReader fr = new FileReader(path);
}
```

### Unchecked Exceptions

- Checked at **runtime**
- Subclass of RuntimeException
- No need to declare or catch explicitly
- Typically represent programming errors

**Examples:**

- NullPointerException
- ArrayIndexOutOfBoundsException
- ArithmeticException

```java
int a = 10 / 0;  // ArithmeticException
```

### Exception Hierarchy

- Object
  - Throwable
    - Error (e.g., OutOfMemoryError)
    - Exception
      - IOException (Checked)
      - SQLException (Checked)
      - RuntimeException (Unchecked)
        - NullPointerException
        - ArithmeticException
        - IndexOutOfBoundsException

### Example

```java
// Checked Exception
try {
    FileReader fr = new FileReader("file.txt");
} catch (FileNotFoundException e) {
    e.printStackTrace();
}

// Unchecked Exception
String s = null;
System.out.println(s.length());  // Throws NullPointerException

```

---

### Common Exception Handling Keywords

| Keyword | Purpose                                    |
| ------- | ------------------------------------------ |
| try     | Defines a block of code to test for errors |
| catch   | Handles the exception                      |
| finally | Executes after try/catch regardless        |
| throw   | Throws an exception explicitly             |
| throws  | Declares exceptions a method may throw     |

---

### Summary

| Feature            | Checked Exception      | Unchecked Exception |
| ------------------ | ---------------------- | ------------------- |
| Checked at         | Compile-time           | Runtime             |
| Inherits from      | Exception              | RuntimeException    |
| Handling required? | Yes                    | No                  |
| Use Case           | Recoverable conditions | Programming bugs    |
