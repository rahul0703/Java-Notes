# Java 8 Features
Oracle released a new version of Java as Java 8 on March 18, 2014. It was a revolutionary release of the Java for software development platform. It includes various upgrades to the Java programming, JVM, Tools and libraries.

## Java 8 Programming Language Enhancements
Java 8 provides following features for Java Programming:
* Lambda expressions
* Method references
* Functional interfaces
* Stream API
* ForEach() method
* Parallel Array Sorting
* Default methods
* Base64 Encode Decode
* Static methods in interface
* Optional class
* Collectors class
* Nashorn JavaScript Engine
* Type and Repating Annotations
* IO Enhancements
* Concurrency Enhancements
* JDBC Enhancements etc

## 1. Lambda Expressions
    (argument-list) -> {body}  

Java lambda expression is consisted of three components.
1. **Argument-list**: It can be empty or non-empty as well.
2. **Arrow-token**: It is used to link arguments-list and body of expression.
3. **Body**: It contains expressions and statements for lambda expression.  

   
    -------------------------------------------------------
    () -> {  
    //Body of no parameter lambda  
    }  
    -------------------------------------------------------
    (p1) -> {  
    //Body of single parameter lambda  
    }  
    -------------------------------------------------------
    (p1, p2) -> {  
    //Body of single parameter lambda  
    }  
    --------------------------------------------------------

Lambda examples:
    
    Use a lamba expression in the ArrayList's forEach() method to print every item in the list:
    
```java
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(5);
    numbers.add(9);
    numbers.add(8);
    numbers.add(1);
    numbers.forEach( (n) -> { System.out.println(n); } );
  }
}
```
------------------------------------------------------------------------
    Use Java's Consumer interface to store a lambda expression in a variable:
```java
import java.util.ArrayList;
import java.util.function.Consumer;

public class Main {
  public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(5);
    numbers.add(9);
    numbers.add(8);
    numbers.add(1);
    Consumer<Integer> method = (n) -> { System.out.println(n); };
    numbers.forEach( method );
  }
}
```
-------------------------------------------------------------------
    Create a method which takes a lambda expression as a parameter:
```java
interface StringFunction {
  String run(String str);
}

public class Main {
  public static void main(String[] args) {
    StringFunction exclaim = (s) -> s + "!";
    StringFunction ask = (s) -> s + "?";
    printFormatted("Hello", exclaim);
    printFormatted("Hello", ask);
  }
  public static void printFormatted(String str, StringFunction format) {
    String result = format.run(str);
    System.out.println(result);
  }
}
```
-----------------------------------------------------------------
    Sorting using lambda function
```java
//sort using java 7
class sort{
    private void sortUsingJava7(List<String> names) {
        Collections.sort(names, new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                return s1.compareTo(s2);
            }
        });
    }

    //sort using java 8
    private void sortUsingJava8(List<String> names) {
        Collections.sort(names, (s1, s2) -> s1.compareTo(s2));
    }   
}
```

## 2. Method References


    