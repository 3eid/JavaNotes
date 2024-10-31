## Packages

to specify a package to a file add the foollowing code at the begining:
``` java
package pkgname;
```
but when you compile and run the file you must use:
```sh
javac -d . Hello.java
java ./pkgname.Hello
```
![image](https://github.com/user-attachments/assets/dd6a09cf-e5f8-46eb-ba15-06a3e68ca12c)

to import a package you have these options:
```java
import java.util.StringTokenizer; // class in the package
import java.util.*; // all classes in the package
import java.util; //error
```
we can import classes only.
