# Java Important Notes


## Java Memory Management

![Java Memory Management Overview](https://miro.medium.com/v2/resize:fit:717/1*sG2wIZg7SqyhKMKD1jxM9A.png)

Java's memory management is essential for efficient performance, dividing memory into different areas for managing dynamic allocation, method execution, and class metadata.

### 1. Heap
The **heap** is the primary memory area in the JVM for **dynamic memory allocation**, storing objects and instance variables.
- **Instance Variables**: These may reference other objects.
- **Object Allocation**: Objects created with `new` are allocated on the heap.
- **Garbage Collection (GC)**: When objects are no longer referenced, they become eligible for garbage collection, freeing up heap memory.
- **Shared Among Threads**: The heap is accessible across all threads and method call frames.
- **Size**: Generally larger than the stack, handling long-term data storage.

### 2. Stack
The **stack** manages **method execution** and stores **method call frames**, including local variables and references to heap objects.
- **Thread-Specific**: Each thread has its own stack to handle method calls and local variables.
- **Memory Management**: Allocated and deallocated automatically following Last-In-First-Out (LIFO) order as methods are called and completed.
- **Scoped Data**: Variables are scoped to the method in which they’re declared and accessible only within that method.
- **Speed**: Stack access is faster than heap access, as it follows LIFO order and requires no garbage collection.

### 3. Metaspace (Method Area / Class Area)
The **Metaspace** is a memory area in the JVM introduced in **Java 8** that stores metadata about classes and methods. It replaces the older PermGen space.
- **Class Metadata**: Contains structures for class information, methods, and fields.
- **Constant Pool**: Stores method names, constants, and other class-level information.
- **Static Variables**: Houses static variables and class-level data.
- **Garbage Collection of Metaspace**: The JVM garbage collector also cleans up unused classes in Metaspace when they are no longer referenced.

### 4. Garbage Collection
The **garbage collector** (GC) is a background process that manages memory cleanup:
- **Eligibility for Collection**: When objects are no longer referenced, they become eligible for garbage collection.
- **Phases**: Most garbage collectors work in stages:
  - **Marking**: Identifies live objects.
  - **Copying/Compacting**: Moves objects to reduce memory fragmentation.
  - **Sweeping**: Reclaims memory used by dead objects.
  
---

| Feature           | Heap                                   | Stack                                | Metaspace                              |
|-------------------|----------------------------------------|--------------------------------------|----------------------------------------|
| **Purpose**       | Stores objects, instance variables     | Holds method calls, local variables  | Stores class metadata and static data  |
| **Managed by**    | JVM Garbage Collector                  | JVM, automatically                   | JVM, partially managed by GC           |
| **Scope**         | Global (within JVM process)            | Limited to method/block scope        | Global                                 |
| **Lifetime**      | Until no references remain             | Until method completes               | Until class unloading                  |
| **Speed**         | Slower                                 | Faster                               | Moderate                               |
| **Error**         | OutOfMemoryError                       | StackOverflowError                   | OutOfMemoryError                       |
| **Accessibility** | Shared across threads                  | Each thread has its own stack        | Shared across threads                  |

![Stack, heap, Value types, Reference types, boxing, and unboxing | Guru N  Guns's](https://gurunguns.wordpress.com/wp-content/uploads/2012/10/valuereferencetype1.jpg)
