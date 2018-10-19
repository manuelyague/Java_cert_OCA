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


#### Understanding Package Declarations and Imports
##### Wildcards
##### Redundant Imp#orts 
##### Naming Conflicts 
##### Creating a New Package 
##### Code Formatting on the Exam 
&nbsp;
#### Creating Objects 
##### Constructors
##### Reading and Writing Object Fields 
##### Instance Initializer Blocks 
##### Order of Initialization 
&nbsp;
#### Distinguishing Between Object References and Primitives 
##### Primitive Types 
##### Reference Types 
##### Key Differences 
&nbsp;
#### Declaring and Initializing Variables 
##### Declaring Multiple Variables 
##### Identifiers 
&nbsp;
#### Understanding Default Initialization of Variables 
##### Local Variables 
##### Instance and Class Variables 
&nbsp;
#### Understanding Variable Scope 
&nbsp;
#### Ordering Elements in a Class 
&nbsp;
#### Destroying Objects 
##### Garbage Collection 
##### finalize() 
&nbsp;
#### Benefits of Java
&nbsp;
#### Summary 
&nbsp;
#### Exam Essentials 
&nbsp;
#### Review Questions 