## Java Exception Handling Summary

Java’s exception handling mechanism provides a robust way to deal with runtime errors, ensuring that programs can handle unexpected situations gracefully. Here’s a structured summary covering key aspects of Java exception handling:

----------

### 1. **What is an Exception?**

An **exception** is an event that disrupts the normal flow of a program’s execution. In Java, exceptions are objects representing these errors, allowing the program to “catch” and handle them instead of abruptly terminating.

----------

### 2. **Exception Class Hierarchy**

In Java, exceptions are organized in a hierarchy under the `Throwable` class:
![image](https://github.com/user-attachments/assets/88a5ff35-81eb-4dea-9ae1-38d1ac459ea9)

-   **`Throwable`**: The root class for all errors and exceptions.
    -   **`Error`**: Represents serious problems that an application shouldn’t try to handle (e.g., `OutOfMemoryError`).
    -   **`Exception`**: Represents recoverable errors that applications can handle.
        -   **`RuntimeException`**: Unchecked exceptions that occur during runtime (can be handled by programlogic without exception class) (e.g., `NullPointerException`, `ArithmeticException`).
        -   **`IOException`**: Checked exceptions, such as `FileNotFoundException`, which are expected issues needing handling.

----------

### 3. **Categories of Exceptions**

-   **Checked Exceptions**: Must be declared or handled in the code. They are subclasses of `Exception` (except `RuntimeException`) and often represent expected problems (e.g., `IOException`).
-   **Unchecked Exceptions**: Don’t need explicit handling can be handled by programlogic without exception class. They are subclasses of `RuntimeException`, representing programming errors (e.g., `IndexOutOfBoundsException`).
-   **Errors**: Uncontrolled and serious issues usually related to system resources (e.g., `StackOverflowError`).

----------

### 4. **Throwing Exceptions with `throw`**

The `throw` keyword is used to explicitly throw an exception in Java.
```java
public void validateAge(int age) throws IllegalArgumentException{
    // if this condition occours, this method will throw IllegalArgumentException
    if (age < 18) {
        throw new IllegalArgumentException("Age must be 18 or above.");
    }
}
```

### 5. **Declaring Exceptions with `throws`**

The `throws` keyword declares exceptions a method may throw, allowing them to be handled by the caller.
```java
//this method may throw IOException when called
public void readFile(String fileName) throws IOException {
    FileReader file = new FileReader(fileName);
}
```

### 6. **`try-catch-finally` Block**

-   **`try`**: Block containing code that might throw an exception.
-   **`catch`**: Block to handle the specific exception.
-   **`finally`**: Block that always executes after `try` and `catch`, used for cleanup.

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero.");
} finally {
    System.out.println("Execution finished.");
}
``` 

----------

### 7. **Printing the Call Stack**

`e.printStackTrace()` prints the exception's call stack, helping trace the origin of the error.
![image](https://github.com/user-attachments/assets/68670426-2579-40a2-a5f6-ecf8c1b7bc09)

----------

### 8. **Exception Handling Scenarios**

### 1. **Ignoring Exceptions**

Ignoring exceptions is generally not recommended, as it may lead to unexpected program termination or instability. Here’s how it looks in code:

#### Using `throws` in `main` (Leads to Program Termination)

If `main()` uses `throws` without handling an exception, the program will terminate upon encountering an unhandled exception.

```java
import java.io.FileReader;
import java.io.IOException;

public class ExceptionExample {

    public static void main(String[] args) throws IOException {
        readFile("non_existent_file.txt"); // This will throw an IOException and terminate
    }

    public static void readFile(String fileName) throws IOException {
        FileReader file = new FileReader(fileName); // FileNotFoundException will occur here
    }
}
``` 

#### Using `try` Without `catch` (Worst Case)

Using `try` without `catch` doesn’t handle the exception. It only delays the error until the method completes, resulting in termination if `throws` is not handled higher up.

```java
import java.io.FileReader;
import java.io.IOException;

public class ExceptionExample {

    public static void main(String[] args) {
        try {
            readFile("non_existent_file.txt");
        } finally {
            System.out.println("This message prints, but exception is still unhandled.");
        }
    }

    public static void readFile(String fileName) throws IOException {
        FileReader file = new FileReader(fileName); // Exception occurs here
    }
}
```
 

### 2. **Handling Where It Occurs**

In this approach, we handle the exception directly within the method where it arises using `try-catch`.

```java
import java.io.FileReader;
import java.io.IOException;

public class ExceptionExample {

    public static void main(String[] args) {
        readFile("non_existent_file.txt");
    }

    public static void readFile(String fileName) {
        try {
            FileReader file = new FileReader(fileName);
            System.out.println("File read successfully.");
        } catch (IOException e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}
``` 

This example catches the `IOException` right where it occurs, allowing the program to continue without terminating. This is often a good approach when the error can be resolved at the point of occurrence.

### 3. **Handling in Another Part of the Program**

By declaring an exception with `throws`, we allow a method to defer exception handling to its caller. This approach promotes separation of concerns, as the responsibility of handling the exception is moved to a higher level in the program.

#### Declaring Exception with `throws` and Handling at a Higher Level

```java
import java.io.FileReader;
import java.io.IOException;

public class ExceptionExample {

    public static void main(String[] args) {
        try {
            readFile("non_existent_file.txt");
        } catch (IOException e) {
            System.out.println("An error occurred while reading the file: " + e.getMessage());
        }
    }

    public static void readFile(String fileName) throws IOException {
        FileReader file = new FileReader(fileName); // Exception will be thrown to main() to handle
    }
}
```
 

In this example, `readFile()` declares `throws IOException`, allowing `main()` to handle it. This method is especially useful in complex applications, as it allows the code to defer exception handling to a part of the program that may have better context for resolving the error.
    
----------

### 9. **Compilation Errors for Unhandled Exceptions**

If checked exceptions are neither caught nor declared with `throws`, the program won’t compile.
```java
import java.io.FileReader;

public class UnhandledExceptionExample {

    public static void main(String[] args) {
        readFile("non_existent_file.txt");  // Compilation error: IOException is unhandled
    }
    public static void readFile(String fileName) {
        FileReader file = new FileReader(fileName);  // IOException can be thrown here
    }
}

```
----------

### 10. **Using `finally` Without `catch`**

You can have a `try-finally` block without `catch` when you need cleanup code but don’t need specific error handling.

``` java
try {
    FileInputStream file = new FileInputStream("file.txt");
} finally {
    System.out.println("Cleanup code.");
} 
```
----------

### 11. **Creating a Custom Exception**

Custom exceptions can provide meaningful error messages specific to your application logic.

```java
public class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}` 
```
----------

### 12. **Using `|` Operator with Exceptions**

From Java 7 onward, you can catch multiple exceptions in a single `catch` block using `|` (multi-catch).

```java
try {
    int[] arr = new int[5];
    System.out.println(arr[10]);
} catch (ArrayIndexOutOfBoundsException | NullPointerException e) {
    System.out.println("Array index or null exception occurred.");
}
``` 

----------

### 13. **Considerations in Exception Handling**

-   **Catch Child Classes Before Parent**: Always catch specific exceptions (like `IOException`) before generic ones (`Exception`) in a `catch` chain to prevent unreachable code.
-   **Overriding Methods with Exceptions**: When overriding a method that throws an exception, the overridden method can only:-
	-  throw the same exception 
	- throw a subclass of the same exception 
	- don't throw exceptions

----------

### 14. **`try-with-resources` (Auto-Closeable Resources)**

`try-with-resources` automatically closes resources (e.g., files) after execution, even if an exception occurs.

``` java
try (FileInputStream file = new FileInputStream("file.txt")) {
    // Read from file
} catch (IOException e) {
    System.out.println("File handling error.");
}
``` 
----------

Using exception handling effectively is crucial to building resilient and user-friendly Java applications, allowing for error management and resource cleanup in a structured, maintainable way.
