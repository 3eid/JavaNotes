# Functional Interface vs Anonymous Class in Java

Java provides multiple ways to implement behavior, especially when dealing with functional programming. Two common approaches are **Functional Interfaces** and **Anonymous Classes**. This guide will explore the differences, advantages, use cases, and performance implications of each.

---

## 1. Functional Interface

A **functional interface** is an interface that contains exactly one abstract method. It can have multiple default or static methods but only one abstract method.

### 1.1 Characteristics
- Contains a **single abstract method** (SAM), which makes it eligible for lambda expressions.
- Can have **default** and **static methods**.
- Marked with the `@FunctionalInterface` annotation (optional but recommended).
- Used extensively in Java's **lambda expressions** and **method references**.

### 1.2 Example

#### **Defining a Functional Interface**
```java
@FunctionalInterface
interface MyFunctionalInterface {
    void display();
}
```


#### **Using Lambda Expression**
```java
public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        MyFunctionalInterface obj = () -> System.out.println("Hello from Functional Interface");
        obj.display();
    }
}
```

### 1.3 Advantages of Functional Interface
✔ **More readable** and concise than an anonymous class.  
✔ **Encourages functional programming**, making code simpler and more maintainable.  
✔ **Improves performance** by avoiding the overhead of creating an additional anonymous class.  
✔ **Works seamlessly** with lambda expressions and method references.  

### 1.4 Common Examples in Java
- `Runnable` → `void run();`
- `Callable` → `V call();`
- `Comparator<T>` → `int compare(T o1, T o2);`
- `Consumer<T>` → `void accept(T t);`
- `Predicate<T>` → `boolean test(T t);`
- `Function<T, R>` → `R apply(T t);`

---

## 2. Anonymous Class

An **anonymous class** is a class without a name that is used for creating an instance on the fly. It is mainly used for implementing interfaces or extending classes when you need a quick implementation.

### 2.1 Characteristics
- Defined **inside another expression** (e.g., inside a method).
- Can **implement multiple methods** (not limited to a single abstract method).
- Generates a separate class file (`.class`) at runtime.
- Cannot have constructors (as it has no name).

### 2.2 Example
```java
public class AnonymousClassExample {
    public static void main(String[] args) {
        MyFunctionalInterface obj = new MyFunctionalInterface() {
            @Override
            public void display() {
                System.out.println("Hello from Anonymous Class");
            }
        };
        obj.display();
    }
}
```

### 2.3 Advantages of Anonymous Class
✔ Can **implement multiple methods** from an interface (unlike lambda expressions).  
✔ Can be used when **you need to override behavior** or extend a class quickly.  
✔ Useful for **event handling** in GUI applications (e.g., Swing, JavaFX).  

---

## 3. Key Differences Between Functional Interface and Anonymous Class

| Feature               | Functional Interface | Anonymous Class |
|-----------------------|---------------------|----------------|
| **Definition**        | An interface with a single abstract method | A class without a name that is declared and instantiated in a single expression |
| **Syntax**           | Uses lambda expressions (concise) | Uses the traditional class declaration (more verbose) |
| **Usage**            | Works best for functional programming | Best for implementing multiple methods or extending a class |
| **Performance**      | More efficient due to direct method reference | Slightly slower due to additional class generation |
| **Multiple Methods** | Only one abstract method (though can have default methods) | Can implement multiple methods |
| **Instance Behavior**| Does not create a new instance per usage | Creates a new instance every time it is used |
| **Access to Outer Variables** | Can access only **effectively final** variables | Can access and modify local variables |

---

## 4. When to Use What?

| Scenario | Best Choice |
|----------|------------|
| Need a simple, single-method implementation | **Functional Interface (Lambda)** |
| Need to implement multiple methods | **Anonymous Class** |
| Need performance optimization | **Functional Interface** |
| Need to extend a class | **Anonymous Class** |
| Need a concise, readable implementation | **Functional Interface** |
| Need to modify local variables | **Anonymous Class** |

---

## 5. Practical Example: Comparator Implementation

### **Using Functional Interface (Lambda)**
```java
import java.util.*;

public class ComparatorLambdaExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 3);

        // Sorting using a Functional Interface (Lambda)
        numbers.sort((a, b) -> Integer.compare(a, b));

        System.out.println(numbers);
    }
}
```

### **Using Anonymous Class**
```java
import java.util.*;

public class ComparatorAnonymousClassExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 3);

        // Sorting using an Anonymous Class
        numbers.sort(new Comparator<Integer>() {
            @Override
            public int compare(Integer a, Integer b) {
                return Integer.compare(a, b);
            }
        });

        System.out.println(numbers);
    }
}
```

### **Which One is Better?**
- **Lambda Expression (Functional Interface)** → Shorter, cleaner, and **better performance**.
- **Anonymous Class** → Useful if you need to add **extra logic** inside the `compare` method.

---

## 6. Performance Considerations

1. **Lambda (Functional Interface) is faster**  
   - Compiled to a method reference at runtime.
   - Uses `invokedynamic` to reduce memory footprint.
   - No extra class creation.

2. **Anonymous Class has a small performance overhead**  
   - Creates a new instance for every use.
   - Generates an additional `.class` file.

### **Benchmarking Example**
```java
import java.util.*;

public class PerformanceTest {
    public static void main(String[] args) {
        int iterations = 1_000_000;

        // Functional Interface (Lambda)
        long start1 = System.nanoTime();
        Runnable lambdaRunnable = () -> {};
        for (int i = 0; i < iterations; i++) {
            lambdaRunnable.run();
        }
        long end1 = System.nanoTime();
        System.out.println("Lambda Execution Time: " + (end1 - start1) + " ns");

        // Anonymous Class
        long start2 = System.nanoTime();
        Runnable anonymousRunnable = new Runnable() {
            @Override
            public void run() {}
        };
        for (int i = 0; i < iterations; i++) {
            anonymousRunnable.run();
        }
        long end2 = System.nanoTime();
        System.out.println("Anonymous Class Execution Time: " + (end2 - start2) + " ns");
    }
}
```

📌 **Result:** Lambda execution is generally **faster** than an anonymous class.

---

## 7. Conclusion

- Use **Functional Interfaces (Lambda Expressions)** when working with **single-method logic**, especially in functional programming.
- Use **Anonymous Classes** when you need to **implement multiple methods** or **extend a class**.
- Functional interfaces are more **efficient, readable, and modern**, while anonymous classes provide **flexibility for more complex logic**.

🔹 **Best Practice:** Prefer **functional interfaces** unless you need to implement multiple methods or extend an existing class.
