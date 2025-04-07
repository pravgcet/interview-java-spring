# Functional Interface

There are 4 types of functional interfaces

1. **Consumer :** void accept(T t)
2. **Supplier :** T get()
3. **Function :** R apply(T t)
4. **Predicate :** boolean test(T t)

### Consumer

A `Consumer` is a functional interface that represents an operation that takes a single input and performs some action on it. It does not return any value.

```java
@FunctionalInterface
interface Consumer<T> {
    void accept(T t);
}
```

`accept(T t)`: This abstract method takes a parameter of type `T` and performs the desired action on it.

```java
public class ConsumerExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");

        Consumer<String> printName = name -> System.out.println(name);
        names.forEach(printName);
    }
}
```

### A `Supplier` is a functional interface that represents an operation that supplies (provides) a result. It does not take any input.

```java
@FunctionalInterface
interface Supplier<T> {
    T get();
}
```

`get()`: This abstract method returns a result of type `T`.

```java

public class SupplierExample {
    public static void main(String[] args) {
        // Using a Supplier to generate a random number
        Supplier<Double> randomNumberSupplier = () -> Math.random();
        System.out.println("Random Number: " + randomNumberSupplier.get());
    }
}
```

### Function

A `Function` is a functional interface that represents an operation that takes an input of type `T` and produces an output of type `R`.

```java
@FunctionalInterface
interface Function<T, R> {
    R apply(T t);
}
```

`apply(T t)`: This abstract method takes a parameter of type `T` and returns a result of type `R`.

```java
public class FunctionExample {
    public static void main(String[] args) {
        // Using a Function to convert a string to its length
        Function<String, Integer> stringLengthFunction = s -> s.length();
        int length = stringLengthFunction.apply("Java is awesome!");
        System.out.println("Length of the string: " + length);
    }
}
```

### Predicate

A `Predicate` is a functional interface that represents an operation that takes an input of type `T` and returns a boolean result.

```java
@FunctionalInterface
interface Predicate<T> {
    boolean test(T t);
}
```

`test(T t)`: This abstract method takes a parameter of type `T` and returns a boolean result.

```java
public class PredicateExample {
    public static void main(String[] args) {
        // Using a Predicate to check if a number is even
        Predicate<Integer> isEvenPredicate = number -> number % 2 == 0;
        boolean isEven = isEvenPredicate.test(10);
        System.out.println("Is the number even? " + isEven);
    }
}
```

[Source: Medium article](https://medium.com/@nagarjun_nagesh/functional-interfaces-in-java-fe5ebf5bafed#:~:text=These%20functional%20interfaces%20are%20categorized,Supplier%2C%20Function%2C%20and%20Predicate.)
