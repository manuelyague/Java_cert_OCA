# Unit 1 - Java Building Blocks

## 1. Java Building Blocks

#### 1.1. Understanding the Java Class Structure

An object is a runtime instance of a class in memory. All the various 
objects of all the different classes represent the state of your program.

##### 1.1.1. Fields and Methods
---
Java classes have two primary elements: **methods**, often called functions 
or procedures in other languages, and **fields**, more generally known as 
variables. Together these are called the members of the class. Variables 
hold the state of the program, and methods operate on that state.

```java
public class Animal { }
```

```java
public class Animal {
	String name;
}
```

```java
public class Animal {
	String name;
	public String getName() {
		return name;
	}
	public void setName(String newName) {
		name = newName;
	}
}
```

##### 1.1.2 Comments
---
There are three types of comments in Java. The fi rst is called a
single-line comment:

```java
// comment until end of line
```

```java
/* Multiple
* line comment
*/
```

```java
/**
* Javadoc multiple-line comment
* @author Jeanne and Scott
*/
```


##### 1.1.3. Classes vs. Files
---
Each Java class is defi ned in its own * .java file.   
Java does not require that the class be public.  
```java
class Animal {
	String name;
}
```
You can even put two classes in the same file.
```java
public class Animal {
	private String name;
}

class Animal2 { //would not compile in a fi le named Animal.
}
```
If you do have a public class, it needs to match the fi lename.

#### 1.2. Writing a main() Method

main() method is the gateway between the startup of a Java process, which is managed by the JVM, and the beginning of the programmer’s code.
```java
public class Zoo {
	public static void main(String[] args) {

	}
}
```
To compile Java code, the fi le must have the extension .java. The name of the file must match the name of the class. The result is a fi le of bytecode by the same name, but with a .class filename extension.  
**Bytecode** consists of instructions that the JVM knows how to execute.

Rules:   
- Each file can contain only one class.
- The filename must match the class name, including case, and have a .java extension.

The keyword public is what’s called an **access modifier**.  
The keyword **static** binds a method to its class so it can be called by just the class name, as in, for example, Zoo.main().  
Java doesn’t need to create an object to call the main().
The keyword **void** represents the return type. In general, it’s good practice to use void for methods that change an object’s state.  
  
Finally we arrive at the main() method’s parameter list, represented as an array of java.lang.String objects. In practice, you can write **String[] args**, **String args[]** or **String... args**; the compiler accepts any of these.

The characters **...** are called **varargs** (variable argument lists).

```java
public class Zoo {
	public static void main(String[] args) {
		System.out.println(args[0]);
		System.out.println(args[1]);
	} 
}
```
```sh
$ javac Zoo.java
$ java Zoo Bronx Zoo

Bronx
Zoo

$ javac Zoo.java
$ java Zoo "San Diego" Zoo

San Diego
Zoo

$ javac Zoo.java
$ java Zoo Zoo

ZooException in thread "main"
java.lang.ArrayIndexOutOfBoundsException: 1
at mainmethod.Zoo.main(Zoo.java:7)
```
Reading args[0] goes fi ne and Zoo is printed out. Then Java panics. There’s no second argument! What to do? Java prints out an exception telling you it has no idea what to do with this argument at position 1.

#### 1.3. Understanding Package Declarations and Imports

Java puts classes in **packages**. These are logical groupings for classes.
It needs you to tell it which packages to look in to fi nd code.

Suppose you try to compile this code:

```java
public class ImportExample {
	public static void main(String[] args) {
		Random r = new Random(); // DOES NOT COMPILE
		System.out.println(r.nextInt(10));
	}
}
```
Random cannot be resolved to a type

This error could mean you made a typo in the name of the class. You double-check and discover that you didn’t. The other cause of this error is omitting a needed import statement.

```java 
import java.util.Random; // import tells us where to find Random

public class ImportExample {
	public static void main(String[] args) {
		Random r = new Random();
		System.out.println(r.nextInt(10)); // print a number between 0 and 9
	}
}
```

The import statement tells the compiler which package to look in to fi nd a class. This is similar to how mailing a letter works.

Package names are hierarchical like the mail as well. The postal service starts with the top level, looking at your country fi rst. You start reading a package name at the beginning too. If it begins with java or javax, this means it came with the JDK.


##### 1.3.1. Wildcards
---

##### 1.3.2. Redundant Imp#orts 
##### 1.3.3. Naming Conflicts 
##### 1.3.4. Creating a New Package 
##### 1.3.5. Code Formatting on the Exam 

#### 1.4. Creating Objects 
##### 1.4.1. Constructors
---
##### 1.4.2. Reading and Writing Object Fields 
---
##### 1.4.3. Instance Initializer Blocks 
---
##### 1.4.4. Order of Initialization 
---
#### 1.5. Distinguishing Between Object References and Primitives 
##### 1.5.1. Primitive Types 
---
##### 1.5.2. Reference Types 
---
##### 1.5.3. Key Differences 
---
#### 1.6. Declaring and Initializing Variables 
##### 1.6.1. Declaring Multiple Variables 
---
##### 1.6.2. Identifiers 
---
#### 1.7. Understanding Default Initialization of Variables 
##### 1.7.1. Local Variables 
---
##### 1.7.2. Instance and Class Variables 
---
#### 1.8. Understanding Variable Scope 

#### 1.9. Ordering Elements in a Class 

#### 1.10. Destroying Objects 
##### 1.10.1. Garbage Collection 
---
##### 1.10.2. finalize() 
---
#### 1.11. Benefits of Java

#### 1.12. Summary 

#### 1.13. Exam Essentials 

#### Review Questions 