# Java Method References

Method references in Java provide a shorthand notation for lambda expressions, making the code more readable and concise. Instead of writing a full lambda expression, you can reference an existing method.

---

## 1. What is a Method Reference?
A method reference is a way to **refer** to a method **without executing it**. It is often used to replace lambda expressions when they call an existing method.

### Syntax
```
ClassName::methodName
```
or
```java
object::methodName
```

---

## 2. Types of Method References
There are **four types** of method references in Java:

1. **Reference to a Static Method**  
2. **Reference to an Instance Method of a Particular Object**  
3. **Reference to an Instance Method of an Arbitrary Object of a Particular Type**  
4. **Reference to a Constructor**  

---

## 3. Examples of Method References

### 1. Reference to a Static Method
You can refer to a static method using `ClassName::staticMethodName`.

#### Example
```java
import java.util.function.Function;

class MathUtil {
    public static int square(int x) {
        return x * x;
    }
}

public class MethodReferenceExample {
    public static void main(String[] args) {
        // Lambda expression
        Function<Integer, Integer> lambda = (x) -> MathUtil.square(x);
        
        // Method reference (shorter)
        Function<Integer, Integer> methodRef = MathUtil::square;

        System.out.println(lambda.apply(5));    // 25
        System.out.println(methodRef.apply(5)); // 25
    }
}
```

---

### 2. Reference to an Instance Method of a Particular Object
You can refer to an instance method of an **existing object**.

#### Example
```java
import java.util.function.Supplier;

class Message {
    public String getMessage() {
        return "Hello, Java!";
    }
}

public class InstanceMethodReference {
    public static void main(String[] args) {
        Message message = new Message();

        // Lambda expression
        Supplier<String> lambda = () -> message.getMessage();

        // Method reference
        Supplier<String> methodRef = message::getMessage;

        System.out.println(lambda.get());    // Hello, Java!
        System.out.println(methodRef.get()); // Hello, Java!
    }
}
```

---

### 3. Reference to an Instance Method of an Arbitrary Object of a Particular Type
You can refer to an **instance method of a class**, but without specifying an object.  
This is mostly used in **streams**.

#### Example
```java
import java.util.Arrays;
import java.util.List;

public class ArbitraryObjectMethodReference {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Lambda expression
        names.forEach(name -> System.out.println(name));

        // Method reference (shorter)
        names.forEach(System.out::println);
    }
}
```

---

### 4. Reference to a Constructor
You can refer to a constructor using `ClassName::new`.  
This is mostly used when creating objects.

#### Example
```java
import java.util.function.Supplier;

class Car {
    public Car() {
        System.out.println("Car is created!");
    }
}

public class ConstructorReference {
    public static void main(String[] args) {
        // Lambda expression
        Supplier<Car> lambda = () -> new Car();

        // Method reference
        Supplier<Car> methodRef = Car::new;

        lambda.get();    // Car is created!
        methodRef.get(); // Car is created!
    }
}
```

---

## 4. Why Use Method References?
Method references make code **shorter** and **more readable**. Use them when:
✅ The lambda **only calls** an existing method.  
✅ You want **cleaner, more readable** code.

---

## 5. Summary Table

| Type                           | Syntax Example        | Example Usage |
|--------------------------------|----------------------|---------------|
| **Static Method Reference**    | `ClassName::method` | `Math::abs`   |
| **Instance Method (Object)**   | `object::method`    | `str::length` |
| **Instance Method (Class)**    | `ClassName::method` | `String::length` |
| **Constructor Reference**      | `ClassName::new`    | `ArrayList::new` |

---

## 6. Final Thoughts
- Method references are **shortcuts** for lambda expressions.
- They improve **code readability**.
- Use them when your lambda **only calls** an existing method.
