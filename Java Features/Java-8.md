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
Java provides a new feature called method reference in Java 8. Method reference is used to refer method of functional interface. It is compact and easy form of lambda expression. Each time when you are using lambda expression to just referring a method, you can replace your lambda expression with method reference. In this tutorial, we are explaining method reference concept in detail.  
```java
import java.util.List;
import java.util.ArrayList;

public class Java8Tester {

   public static void main(String args[]) {
      List names = new ArrayList();
		
      names.add("Mahesh");
      names.add("Suresh");
      names.add("Ramesh");
      names.add("Naresh");
      names.add("Kalpesh");
		
      names.forEach(System.out::println);
   }
}
```
### Types of Method References
1. Reference to a static method.
2. Reference to an instance method.
3. Reference to a constructor.

### Reference to a static method.
Systex
    
    ContainingClass::staticMethodName  
You can refer to static method defined in the class. Following is the syntax and example which describe the process of referring static method in Java.
```java
interface Sayable{  
    void say();  
}  
public class MethodReference {  
    public static void saySomething(){  
        System.out.println("Hello, this is static method.");  
    }  
    public static void main(String[] args) {  
        // Referring static method  
        Sayable sayable = MethodReference::saySomething;  
        // Calling interface method  
        sayable.say();  
    }  
}
```

### Reference to an Instance Method
like static methods, you can refer instance methods also. In the following example, we are describing the process of referring the instance method.  

Syntax

    containingObject::instanceMethodName

```java
interface Sayable{  
    void say();  
}  
public class InstanceMethodReference {  
    public void saySomething(){  
        System.out.println("Hello, this is non-static method.");  
    }  
    public static void main(String[] args) {  
        InstanceMethodReference methodReference = new InstanceMethodReference(); // Creating object  
        // Referring non-static method using reference  
            Sayable sayable = methodReference::saySomething;  
        // Calling interface method  
            sayable.say();
    }  
} 
```

### Reference to a Constructor
Syntax

    ClassName::new 

```java
interface Messageable{  
    Message getMessage(String msg);  
}  
class Message{  
    Message(String msg){  
        System.out.print(msg);  
    }  
}  
public class ConstructorReference {  
    public static void main(String[] args) {  
        Messageable hello = Message::new;  
        hello.getMessage("Hello");  
    }  
}  
```

## 3. Java Functional Interfaces
An Interface that contains exactly one abstract method is known as functional interface. It can have any number of default, static methods but can contain only one abstract method. It can also declare methods of object class.

Functional Interface is also known as Single Abstract Method Interfaces or SAM Interfaces. It is a new feature in Java, which helps to achieve functional programming approach.  

```java
@FunctionalInterface  
interface sayable{  
    void say(String msg);  
}  
public class FunctionalInterfaceExample implements sayable{  
    public void say(String msg){  
        System.out.println(msg);  
    }  
    public static void main(String[] args) {  
        FunctionalInterfaceExample fie = new FunctionalInterfaceExample();  
        fie.say("Hello there");  
    }  
} 
```
---------------------------------------------------------------
    A functional interface can have methods of object class. See in the following example.
    
```java
@FunctionalInterface  
interface sayable{  
    void say(String msg);   // abstract method  
    // It can contain any number of Object class methods.  
    int hashCode();  
    String toString();  
    boolean equals(Object obj);  
}  
public class FunctionalInterfaceExample2 implements sayable{  
    public void say(String msg){  
        System.out.println(msg);  
    }  
    public static void main(String[] args) {  
        FunctionalInterfaceExample2 fie = new FunctionalInterfaceExample2();  
        fie.say("Hello there");  
    }  
}  
```
------------------------------------------------------------------
    A functional interface can extends another interface only when it does not have any abstract method.  

```java
interface sayable{  
    void say(String msg);   // abstract method  
}  
@FunctionalInterface  
interface Doable extends sayable{  
    // Invalid '@FunctionalInterface' annotation; Doable is not a functional interface  
    void doIt();  
}  
```

    A functional interface is extending to a non-functional interface.

```java
interface Doable{  
    default void doIt(){  
        System.out.println("Do it now");  
    }  
}  
@FunctionalInterface  
interface Sayable extends Doable{  
    void say(String msg);   // abstract method  
}  
public class FunctionalInterfaceExample3 implements Sayable{  
    public void say(String msg){  
        System.out.println(msg);  
    }  
    public static void main(String[] args) {  
        FunctionalInterfaceExample3 fie = new FunctionalInterfaceExample3();  
        fie.say("Hello there");  
        fie.doIt();  
    }  
}  
```

### Important Predefined Functional Interface
**BiConsumer<T,U>**: It represents an operation that accepts two input arguments and returns no result.  
**Consumer<T>**: It represents an operation that accepts a single argument and returns no result.  
**Function<T,R>**: It represents a function that accepts one argument and returns a result.  
**Predicate<T>**: Boolean valued function of 1 argument.  


