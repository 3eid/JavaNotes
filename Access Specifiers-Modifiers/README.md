
## Java Access Specifiers and Modifiers

![image](https://github.com/user-attachments/assets/823aa0c0-b216-4652-884d-94d49c6efdea)
![image](https://github.com/user-attachments/assets/7ceaedf3-f9d5-4be1-87d2-b122a1dc58aa)

### Class Specifiers

**`public class:`**  
A class marked with the `public` keyword **can be accessed from any package**. This means it’s visible throughout the entire application. You can import and use a `public` class in other packages.

**`default class (Package-Private):`**  
A class without any access modifier (neither `public`, `protected`, nor `private`) is a default or package-private class. It’s **only accessible within the same package**, so you can't directly import and use it in classes outside its package.

**Important Note:**  
You can import a public class that contains methods or fields using default classes, but the default classes themselves are not directly accessible from outside their package. This allows you to hide implementation details within a package, enhancing abstraction by exposing only the public API.

**`final class:`**  
A `final` class cannot be extended (no subclass can inherit from it). This is commonly used to prevent modification or inheritance of sensitive or critical classes. For example, the `String` class is final in Java.

**`abstract class:`**  
An `abstract` class cannot be instantiated. It contains one or more abstract methods (methods without a body) which must be implemented by subclasses. Abstract classes are used to define a template for subclasses. For example, if you want to enforce certain methods in subclasses, you can define those methods as abstract in an abstract class.
Note: we use abstract class without abstract methods at all, instead we may have static methods that return the object, we may want to preserve the data in someway, etc.

----------

### Method Specifiers

**`public:`**  
A `public` method can be accessed from any class in any package, providing the broadest level of access.

**`private:`**  
A `private` method is only accessible within its own class. This is used to encapsulate the functionality, so it's not exposed outside the class.

**`protected:`**  
A `protected` method can be accessed by classes in the same package and by subclasses, even if they are in different packages.

**`default (Package-Private):`**  
A method with no access modifier (default access) is accessible only within its own package. It cannot be accessed from classes in different packages.

**`final:`**  
A `final` method cannot be overridden by subclasses. This is often used to prevent modification of essential behavior in a base class.

**`static:`**  
A `static` method belongs to the class rather than to any instance of the class. It can be called without creating an instance of the class. It cannot access instance variables or methods directly.

**`abstract:`**  
An `abstract` method has no body and must be implemented by subclasses of an abstract class.

**`synchronized:`**  
A `synchronized` method can only be accessed by one thread at a time. This is commonly used to prevent race conditions in concurrent applications.

**`native:`**  
A `native` method is implemented in another language, like C or C++. It’s used when Java alone cannot provide certain functionalities, for example, interacting with OS-specific features. It's SUPER USEFUL in dynamic binding.

----------

### Variable Specifiers

**`public:`**  
A `public` variable can be accessed from any class in any package.

**`private:`**  
A `private` variable is only accessible within its own class. This is typically used to enforce encapsulation, only allowing access via getters and setters.

**`protected:`**  
A `protected` variable can be accessed by classes in the same package and by subclasses in different packages.

**`default (Package-Private):`**  
A variable with no access modifier (default access) is accessible only within its own package.

**`final:`**  
A `final` variable can only be assigned once, making it a constant after it has been assigned. This is often used for constants.

**`static:`**  
A `static` variable belongs to the class itself rather than to any instance. This means all instances of the class share the same value for that variable.

**`transient:`**  
A `transient` variable is ignored during serialization. It’s used when certain variables do not need to be saved.

**`volatile:`**  
A `volatile` variable is stored in main memory and is visible to all threads. It ensures that any change to this variable is immediately reflected across all threads.

## Additional Notes

#### Common Constructor body

In Java, you can define a block of code outside of any method, known as common constructor body, which get executed before instantiating any object, whatever which constructor is used.
```java
public class Example {
    {
        // Common Constructor body: runs with each instance creation
        System.out.println("Instance created!");
    }
}
```

#### Free-Floating Block

In Java, you can define a block of code outside of any method, known as common constructor body, which get executed before instantiating any object, whatever which constructor is used.
```java
public class Example {
    static {
        // Free-Floating Block: runs once in class lifetime when loaded to memory
        System.out.println("Class loaded!");
    }
}
```
To understand the differences:

```java
public class Person {
	// Free-Floating Block: runs once in class lifetime when loaded to memory
    static {
	        System.out.println("Class loaded!");
	}
    private String name;
    private int age;
	

    // Common Constructor body: runs with each instance creation (Instance initializer block)
    
    {
        // This block runs with each instance creation, before the constructor body
        System.out.println("An instance of Person is being created!");
    }

    // Constructor 1
    public Person() {
        this.name = "Unknown";
        this.age = 0;
        System.out.println("Default constructor called.");
    }

    // Constructor 2
    public Person(String name) {
        this.name = name;
        this.age = 0;
        System.out.println("Constructor with name parameter called.");
    }


    public static void main(String[] args) {
        
        // prints "Class loaded!" one time from the Free-Floating Block when class loaded to memory       
        Person person1 = new Person(); // prints "An instance of Person is being created!"
								       //"Default constructor called."
        Person person2 = new Person("Alice");   // prints "An instance of Person is being created!"
										       //"Constructor with name parameter called."
        
    }
}

```
