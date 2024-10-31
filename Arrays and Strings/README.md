### String Comparison

```java
public class Main {
    public static void main(String[] args) {
        String s = new String("Hi");
        String s2 = new String("Hi");
        System.out.println(s == s2); //false
    }
}
```
It compares references not the actual string content. Instead we can use:
```
public class Main {
    public static void main(String[] args) {
        String s = new String("Hi");
        String s2 = new String("Hi");
        System.out.println(s.equals(s2)); //true
    }
}
```

Note that if we define string without the new keyword it make the object in the string pool.
```
public class Main {
    public static void main(String[] args) {
        String s1 = "Hi";
        String s2 = "Hi"; //same reference as s1
        System.out.println(s1 == s2)); //true
        s2 = "hello";
        System.out.println(s1 == s2)); //false
    }
}
```

