## Notes on Data Types in java:

### Wrapper classes
![image](https://i.ibb.co/0tksktr/image.png)

* It allows you access some constants defined by class such: MIN_VALUE, MAX_VALUE
    ```java
    public class Main {

        public static void main(String[] args){
            System.out.println("Integer.MIN_VALUE= "+ Integer.MIN_VALUE);
        }
    }
    ```
* Can pass it to a method expecting an Object
*  to use class methods for:
    * convert values to/from other primitive type
    * convert to/from strings
    * convert number system (bin-oct-hex-dec)
    ```java
    Integer i = new Integer(42);
    byte b = i.byteValue();
    double d = i.doubleValue();
    String S = Integer.toString(254);
    ```
* To use special representations such: Double.POSITIVE_INFINITY
    ```java
    Double positiveInfinity = Double.POSITIVE_INFINITY;
    Double negativeInfinity = Double.NEGATIVE_INFINITY;
    
    assertEquals(Double.NaN, (positiveInfinity + negativeInfinity));
    assertEquals(Double.NaN, (positiveInfinity / negativeInfinity));
    assertEquals(Double.POSITIVE_INFINITY, (positiveInfinity - negativeInfinity));
    assertEquals(Double.NEGATIVE_INFINITY, (negativeInfinity - positiveInfinity));
    assertEquals(Double.NEGATIVE_INFINITY, (positiveInfinity * negativeInfinity));
    ```
* To use Special methods such: Double.isInfinite, Double.isNan:
    ```java
    public class Main {
        public static void main(String[] args) {
            System.out.println( Double.isInfinite(-1.0/0.0)); // Output: true
        }
    }
    ```
### Literals
![](https://i.ibb.co/DRgW5gZ/image.png)
```java
    int i = 0x1A;
    int b = 0b0111;
    System.out.println( i); // Output: 26
    System.out.println( b); // Output: 7
```

### lossy operation
```java
public class Main {
    public static void main(String[] args) {
        int i = 11;
        double b = 2;
        int c = b * i; //compilation error (lossy) should
        // correct double c = b*i
        System.out.println(c);
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        byte a = 11;
        byte b = 2;
        byte c = b + i; //compilation error (lossy) should
        // int c = b + i  //correct
        System.out.println(c);
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        int i = Integer.MAX_VALUE;
        int b = 2;
        int c = b * i; // -2 (logical error)
        // should be:
        /*
        double i = Integer.MAX_VALUE;
        int b = 2;
        double c = b * i; //
        */
        System.out.println(c);
    }
}
```

### modulo signed
![image](https://i.ibb.co/fDJ29yV/image.png)

takes the sign of the Numerator 


    
