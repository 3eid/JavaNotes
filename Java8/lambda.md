# **Java Lambda Expressions**  

---

## **1. Introduction to Lambda Expressions**  
Lambda expressions were introduced in **Java 8** as a way to write **concise, readable, and functional** code. They enable functional-style programming and provide a **shorter way** to represent **anonymous functions**.

- **Before Java 8**, we had to use anonymous inner classes to implement functional interfaces.
- **With Java 8**, we can use lambda expressions to write cleaner and more readable code.

### **Syntax of a Lambda Expression**
```java
(parameters) -> { // Function body }
```

**Example:**
```java
() -> System.out.println("Hello, Lambda!");
```

---

## **2. Why Use Lambda Expressions?**  

### **Advantages of Lambda Expressions:**
1. **Eliminates Boilerplate Code:** Reduces verbosity by removing unnecessary class definitions.
2. **Improves Readability:** Code becomes cleaner and more expressive.
3. **Enhances Functional Programming:** Enables the use of functions as first-class citizens.
4. **Works Well with Java Collections:** Simplifies sorting and filtering operations.
5. **Better Multithreading:** Makes multithreading with functional interfaces easier.

---

## **3. Functional Interfaces and Lambda Expressions**  
### **Definition of a Functional Interface**
A **functional interface** is an interface that contains **exactly one abstract method**. Lambda expressions can only be used with functional interfaces.

### **Example of a Functional Interface**
```java
@FunctionalInterface
interface MyFunctionalInterface {
    void myMethod();
}
```

---

## **4. Implementing Functional Interfaces with Lambda Expressions**
### **Example 1: Lambda Without Parameters**
```java
@FunctionalInterface
interface Greeting {
    void sayHello();
}

public class LambdaDemo {
    public static void main(String[] args) {
        Greeting greeting = () -> System.out.println("Hello, Lambda!");
        greeting.sayHello(); // Output: Hello, Lambda!
    }
}
```

### **Example 2: Lambda with Parameters**
```java
@FunctionalInterface
interface MathOperation {
    int operate(int a, int b);
}

public class LambdaExample {
    public static void main(String[] args) {
        MathOperation addition = (a, b) -> a + b;
        MathOperation multiplication = (a, b) -> a * b;

        System.out.println("Addition: " + addition.operate(5, 3)); // Output: 8
        System.out.println("Multiplication: " + multiplication.operate(5, 3)); // Output: 15
    }
}
```

---

## **5. Lambda Expressions with Java Collections**
Lambda expressions are often used to **sort, filter, and manipulate collections**.

### **Example 1: Sorting a List Using Lambda**
```java
import java.util.*;

public class LambdaSort {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("John", "Alex", "Brian", "Charles");

        // Sorting using Lambda
        Collections.sort(names, (a, b) -> a.compareTo(b));

        System.out.println(names); // Output: [Alex, Brian, Charles, John]
    }
}
```

### **Example 2: Filtering a List Using Streams and Lambda**
```java
import java.util.*;

public class LambdaStream {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        // Filtering even numbers using Lambda
        numbers.stream()
               .filter(n -> n % 2 == 0)
               .forEach(System.out::println);  // Output: 2 4 6
    }
}
```

---

## **6. Using Lambda Expressions with Threads**
Before Java 8, we had to use anonymous classes to implement `Runnable`.

### **Without Lambda (Using Anonymous Class)**
```java
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Thread is running...");
    }
}).start();
```

### **With Lambda Expression**
```java
new Thread(() -> System.out.println("Thread is running...")).start();
```

---

## **7. Method References (Shortcut for Lambdas)**
If a lambda expression **calls a single method**, we can replace it with a **method reference**.

### **Example 1: Using Lambda**
```java
import java.util.*;

public class MethodRefExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Using lambda
        names.forEach(name -> System.out.println(name));
    }
}
```

### **Example 2: Using Method Reference**
```java
import java.util.*;

public class MethodRefExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Using method reference
        names.forEach(System.out::println);
    }
}
```

---

## **8. Built-in Functional Interfaces in Java**
Java provides several **built-in functional interfaces** in the `java.util.function` package.

| Interface  | Parameters | Return Type | Example Usage |
|------------|-----------|-------------|--------------|
| `Predicate<T>` | 1 | `boolean` | `filter(x -> x > 10)` |
| `Function<T, R>` | 1 | 1 | `map(x -> x * 2)` |
| `Consumer<T>` | 1 | `void` | `forEach(System.out::println)` |
| `Supplier<T>` | None | 1 | `() -> new Random().nextInt()` |

### **Example: Using Predicate**
```java
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        Predicate<Integer> isEven = x -> x % 2 == 0;
        
        System.out.println(isEven.test(4)); // Output: true
        System.out.println(isEven.test(7)); // Output: false
    }
}
```

---

## **9. Lambda Expression Best Practices**
1. **Use Lambda Expressions for Simple Implementations**  
   - If the implementation is complex, use a separate method instead.

2. **Use Method References Where Possible**  
   - Instead of `(x) -> System.out.println(x)`, use `System.out::println`.

3. **Prefer Built-in Functional Interfaces**  
   - Instead of creating your own interface, use `Predicate`, `Consumer`, `Function`, etc.

4. **Avoid Modifying Local Variables in Lambda Expressions**  
   - Lambda expressions cannot modify local variables **unless they are effectively final**.

---

## **10. Conclusion**
- Lambda expressions **simplify Java programming** by reducing boilerplate code.
- They work with **functional interfaces**.
- They are widely used in **Streams, Collections, and Multithreading**.
- **Method references** provide a further shortcut.
