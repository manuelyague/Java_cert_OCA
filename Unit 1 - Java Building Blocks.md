# Unit 1 - Java Building Blocks

## 1. Java Building Blocks

### 1.1. Understanding the Java Class Structure

An object is a runtime instance of a class in memory. All the various 
objects of all the different classes represent the state of your program.

#### 1.1.1. Fields and Methods
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

#### 1.1.2 Comments
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


#### 1.1.3. Classes vs. Files
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

### 1.2. Writing a main() Method

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

### 1.3. Understanding Package Declarations and Imports

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


#### 1.3.1. Wildcards
---
Can use a shortcut to import all the classes in a package:
```java
import java.util.*; // imports java.util.Random among other things
public class ImportExample {
	public static void main(String[] args) {
		Random r = new Random();
		System.out.println(r.nextInt(10));
	}
}
```
It doesn’t import child packages, fields, or methods; it imports only classes.
You might think that including so many classes slows down your program, but it doesn’t. The compiler fi gures out what’s actually needed. Which approach you choose is personal preference.

Using the wildcard can shorten the import list.

#### 1.3.2. Redundant Imports 
---
There’s one special package in the Java world called java.lang. This package is
special in that it is automatically imported. You can still type this package in an import statement, but you don’t have to.

```java
import java.lang.System;
import java.lang.*; // Lines 1 and 2 are redundant
import java.util.Random;
import java.util.*; // Also redundant in this example because Random is already imported from java.util.Random.

public class ImportExample {
 	public static void main(String[] args) {
		Random r = new Random();
		System.out.println(r.nextInt(10));
	}
}
```

What imports do you think would work to get this code to compile?

```java
public class InputImports {
	public void read(Files files) {
		Paths.get("name");
	}
}
```
There are two possible answers. The shorter one is to use a wildcard to import both at the same time:

```java
import java.nio.file.*; 

//The other answer is to import both classes explicitly:
import java.nio.file.Files;
import java.nio.file.Paths;

//Now let’s consider some imports that don’t work:
import java.nio.*; // NO GOOD – a wildcard only matches class names, not "file.*Files"
import java.nio.*.*; // NO GOOD – you can only have one wildcard and it must be at the end
import java.nio.files.Paths.*; // NO GOOD – you cannot import methods only class names
```

#### 1.3.3. Naming Conflicts 
---
One of the reasons for using packages is so that class names don’t have to be unique across all of Java.

```java
import java.util.*;
import java.sql.*; // DOES NOT COMPILE

//this code is no good.
import java.util.Date;
import java.sql.Date;

//One to use in the import and use the other’s fully qualifi ed class name
public class Conflicts {
	Date date;
	java.sql.Date sqlDate;
}
// Use the fully qualifi ed class name:

public class Conflicts {
	java.util.Date date;
	java.sql.Date sqlDate;
}

```

#### 1.3.4. Creating a New Package 
---

```sh
# Windows Setup
# Create the two fi les:
C:\temp\packagea\ClassA.java
C:\temp\packageb\ClassB.java
# Then type this command:
cd C:\temp

# Mac/Linux Setup
# Create the two fi les:
/tmp/packagea/ClassA.java
/tmp/packageb/ClassB.java

# Then type this command:
cd /tmp

# To Compile
# Type this command:
javac packagea/ClassA.java packageb/ClassB.java

# To Run
# Type this command:
java packageb.ClassB

# Class Paths and JARs
# A JAR file is like a zip fi le of mainly Java class files

# On Windows, you type the following:
java -cp ".;C:\temp\someOtherLocation;c:\temp\myJar.jar" myPackage.MyClass

# And on Mac OS/Linux, you type this:
java -cp ".:/tmp/someOtherLocation:/tmp/myJar.jar" myPackage.MyClass

# Use a wildcard (*) to match all the JARs in a directory. Here’s an example:
java -cp "C:\temp\directoryWithJars\*" myPackage.MyClass

# This command will add all the JARs to the class path that are in directoryWithJars. It won’t include any JARs in the class path that are in a subdirectory of directoryWithJars.
```

#### 1.3.5. Code Formatting on the Exam 
---

Not all questions will include the imports. If the exam isn’t asking about imports in the question, it will often omit the imports to save space. You’ll see examples with line numbers that don’t begin with 1 in this case. The question is telling you, “Don’t worry—imagine the code we omitted is correct; just focus on what I’m giving you.” This means when you do see the line number 1 or no line numbers at all, you have to make sure imports aren’t missing. Another thing the exam does to save space is to merge code on the same line. You should expect to see code like the following and to be asked whether it compiles. (You’ll learn about ArrayList in Chapter 3—assume that part is good for now.)

> No todas las preguntas incluirán las importaciones. Si el examen no pregunta sobre las importaciones en la pregunta, a menudo omitirá las importaciones para ahorrar espacio. Verá ejemplos con números de línea que no comienzan con 1 en este caso. La pregunta le dice: "No se preocupe, imagine que el código que omitimos es correcto; solo concéntrate en lo que te estoy dando ”. Esto significa que cuando ves la línea número 1 o no tienes números de línea, debes asegurarte de que no falten las importaciones. Otra cosa que el examen hace para ahorrar espacio es fusionar el código en la misma línea. Debería esperar ver un código como el siguiente y que se le pregunte si se compila. (Aprenderá sobre ArrayList en el Capítulo 3, asumiendo que una parte es buena por ahora).

```java

6: public void method(ArrayList list) {
7: 		if (list.isEmpty()) { System.out.println("e");
8: 		} else { System.out.println("n");
9: } }
```

```java
1: public class LineNumbers {
2: 		public void method(ArrayList list) {
3: 			if (list.isEmpty()) { System.out.println("e");
4: 			} else { System.out.println("n");
5: } } }
```
Since the code begins with line 1, you don’t get to assume that valid imports were provided earlier. `The exam will let you know what package classes are in unless they’re covered in the objectives. You’ll be expected to know that ArrayList is in java.util—at least you will once you get to Chapter 3 of this book!

You’ll also see code that doesn’t have a main() method. When this happens, assume the main() method, class defi nition, and all necessary imports are present. You’re just being asked if the part of the code you’re shown compiles when dropped into valid surrounding code.

> Como el código comienza con la línea 1, no puede asumir que las importaciones válidas se proporcionaron anteriormente. El examen le permitirá saber en qué paquetes se encuentran, a menos que estén cubiertos en los objetivos. Se espera que sepas que ArrayList está en java.util, ¡al menos lo harás una vez que llegues al Capítulo 3 de este libro!

> También verás el código que no tiene un método main (). Cuando esto suceda, suponga que el método main (), la definición de clase y todas las importaciones necesarias están presentes. Solo se le pregunta si la parte del código que se muestra se compila cuando se coloca en un código circundante válido.

### 1.4. Creating Objects 
#### 1.4.1. Constructors
---
To create an instance of a class
```java
Random r = new Random();
```
- First you declare the type that you’ll be creating (Random) 
- and give the variable a name (r). This gives Java a place to store a reference to the object. 
- Then you write new Random() to actually create the object.
- Random() looks like a method since it is followed by parentheses. `It’s called a constructor`, which is a special type of method that creates a new object.

```java
public class Chick {
	public Chick() {
		System.out.println("in constructor");
	}
}
```
- the name of the constructor matches the name of the class
- there’s no return type.

```java
public void Chick() { } // NOT A CONSTRUCTOR
```

#### 1.4.2. Reading and Writing Object Fields 
---
It’s possible to read and write instance variables directly from the caller. In this example, a mother swan lays eggs:

```java
public class Swan {
	int numberEggs;// instance variable
	public static void main(String[] args) {
		Swan mother = new Swan();
		mother.numberEggs = 1; // set variable
		System.out.println(mother.numberEggs); // read variable
	}
}
```

#### 1.4.3. Instance Initializer Blocks 
---
When you learned about methods, you saw braces ({}). The code between the braces is called a `code block`.

- Sometimes code blocks are inside a method. These are run when the method is called.
- Other times, code blocks appear outside a method. These are called instance initializers.
```java
3: public static void main(String[] args) {
4: 	{ System.out.println("Feathers"); }
5: }
6: { System.out.println("Snowy"); }

```
If there aren’t the same number of open ({) and close (}) braces, the code doesn’t compile. It doesn’t matter that one set of braces is inside the main() method—it still counts.
When counting instance initializers, keep in mind that it does matter whether the braces are inside a method. There’s only one pair of braces outside a method. Line 6 is an instance initializer.

> Si no hay el mismo número de llaves abiertas ({) y cerradas (}), el código no se compila. No importa que un juego de llaves esté dentro del método main (), todavía cuenta.
Al contar los inicializadores de instancia, tenga en cuenta que sí importa si las llaves están dentro de un método. Sólo hay un par de llaves fuera de un método. La línea 6 es un inicializador de instancia.

#### 1.4.4. Order of Initialization 
---

Remember:

- Fields and instance initializer blocks are run in the order in which they appear in the file.
- The constructor runs after all fields and instance initializer blocks have run.

```java
1: public class Chick {
2: 	private String name = "Fluffy";
3: 	{ System.out.println("setting field"); }
4: 	public Chick() {
5: 		name = "Tiny";
6: 		System.out.println("setting constructor");
7: 	}
8:	public static void main(String[] args) { 
9: 		Chick chick = new Chick();
10: 	System.out.println(chick.name); } } 
```
1. `Line 8:` main().
2. `Line 9:` Call the constructor of Chick.
3. `Line 2:` Initializes name to "Fluffy".
4. `Line 3:` Executes the print statement.
5. `line 4:` Once all the fields and instance initializers have run, Java returns to the constructor.
6. `Line 5:` Changes the value of name to "Tiny".
7. `Line 6:` Prints another statement.
8. `Line 10:` The constructor is done executing and goes back to the print.

Order matters for the fi elds and blocks of code. You can’t refer to a variable before it has been initialized:

```java
{ System.out.println(name); } // DOES NOT COMPILE
private String name = "Fluffy";
```

What do you think this code prints out?

```java
public class Egg {
	public Egg() {
		number = 5;
	}

	public static void main(String[] args) {
		Egg egg = new Egg();
		System.out.println(egg.number);
	}
	private int number = 3;
	{ number = 4; } }
```
If you answered 5, you got it right. Fields and blocks are run fi rst in order, setting number to 3 and then 4. Then the constructor runs, setting number to 5.

### 1.5. Distinguishing Between Object References and Primitives 
Two types of data: 
- primitive types
- reference types.

#### 1.5.1. Primitive Types 
---
8 data types, represent the building blocks for Java objects: 

| Keyword|Type | Example|
|-| -|-|
| boolean | true or false|  true|
| byte | 8-bit integral value | 123|
| short | 16-bit integral value | 123|
| int | 32-bit integral value | 123|
| long | 64-bit integral value | 123|
| float | 32-bit floating-point value | 123.45f|
| double | 64-bit floating-point value | 123.456|
| char | 16-bit Unicode value | 'a'|

- 1 byte is 8 bits, 2^8.   

There’s a lot of information in Table 1.1. Let’s look at some key points:
   
- float and double are used for floating-point (decimal) values.
- A float requires the letter f following the number so Java knows it is a float.
- byte, short, int, and long are used for numbers without decimal points.
- Each numeric type uses twice as many bits as the smaller similar type. For example, short uses twice as many bits as byte does.

You do not have to know this for the exam, but the maximum number an int can hold is
2,147,483,647. How do we know this? One way is to have Java tell us:

```java
System.out.println(Integer.MAX_VALUE);
```

Java complains the number is out of range. And it is—for an int. However, we don’t have an int. The solution is to add the character L to the number:

```java
long max = 3123456789L; // now Java knows it is a long
```

There are a few more things you should know about numeric primitives. When a number is present in the code, it is called a literal. By default, Java assumes you are defi ning an int value with a literal. In this example, the number listed is bigger than what fi ts in an int.   
Remember, you aren’t expected to memorize the maximum value for an int. The exam will include it in the question if it comes up.

> Hay algunas cosas más que debe saber sobre los primitivos numéricos. Cuando un número está presente en el código, se llama un literal. Por defecto, Java asume que está definiendo un valor int con un literal. En este ejemplo, el número listado es más grande de lo que cabe en un int.  
>  
> Recuerde, no se espera que memorice el valor máximo para un int. El examen lo incluirá en la pregunta si surge.

```java 
long max = 3123456789; // DOES NOT COMPILE
```

Alternatively, you could add a lowercase l to the number. But please use the uppercase L.   
The lowercase l looks like the number 1.   
Another way to specify numbers is to change the “base.” When you learned how to count, you studied the digits 0–9. This numbering system is called base 10 since there are 10 numbers. It is also known as the decimal number system. Java allows you to specify digits in several other formats:

- octal (digits 0–7), which uses the number 0 as a prefix—for example, 017
- hexadecimal (digits 0–9 and letters A–F), which uses the number 0 followed by x or X as a prefix—for example, 0xFF
- binary (digits 0–1), which uses the number 0 followed by b or B as a prefix—for example, 0b10

> Alternativamente, podría agregar una l minúscula al número. Pero por favor use la mayúscula L.  
> La letra minúscula l parece el número 1.  
> Otra forma de especificar números es cambiar la "base". Cuando aprendió a contar, estudió los dígitos 0–9. Este sistema de numeración se llama base 10 ya que hay 10 números. También se conoce como el sistema numérico decimal. Java te permite especificar dígitos en varios otros formatos:   
> 
> - octal (dígitos 0–7), que usa el número 0 como prefijo, por ejemplo, 017
> - hexadecimal (dígitos 0–9 y letras A – F), que usa el número 0 seguido de x o X como un prefijo, por ejemplo, 0xFF
> - binario (dígitos 0–1), que usa el número 0 seguido de b o B como prefijo, por ejemplo, 
   
Although you don’t need to convert between number systems on the exam, we’ll look at one example in case you’re curious:

- System.out.println(56); // 56
- System.out.println(0b11); // 3
- System.out.println(017); // 15
- System.out.println(0x1F); // 31

First we have our normal base 10 value. We know you already know how to read that, but bear with us. The rightmost digit is 6, so it’s “worth” 6. The second-to-rightmost digit is 5, so it’s “worth” 50 (5 times 10.) Adding these together, we get 56.

Next we have binary, or base 2. The rightmost digit is 1 and is “worth” 1. The second-torightmost digit is also 1. In this case, it’s “worth” 2 (1 times 2) because the base is 2. Adding these gets us 3.

Then comes octal, or base 8. The rightmost digit is 7 and is “worth” 7. The second-torightmost digit is 1. In this case, it’s “worth” 8 (1 times 8) because the base is 8. Adding these gets us 15.

Finally, we have hexadecimal, or base 16, which is also known as hex. The rightmost “digit” is F and it’s “worth” 15 (9 is “worth” 9, A is “worth” 10, B is “worth” 11, and so forth). The second-to-rightmost digit is 1. In this case, it’s “worth” 16 (1 times 16) because the base is 16. Adding these gets us 31.

> Aunque no necesita convertir entre sistemas numéricos en el examen, veremos un ejemplo en caso de que tenga curiosidad:
> - System.out.println (56); // 56
> - System.out.println (0b11); // 3
> - System.out.println (017); // 15
> - System.out.println (0x1F); // 31.  
>  
> Primero tenemos nuestro valor normal de base 10. Sabemos que ya sabes cómo leer eso, pero ten paciencia con nosotros. El dígito más a la derecha es 6, por lo que vale “6”. El dígito del segundo a la derecha es 5, por lo que “vale” 50 (5 por 10). Sumando estos, obtenemos 56.   
> Luego tenemos el binario, o base 2. El dígito más a la derecha es 1 y "vale" 1. El dígito del segundo más alto es también 1. En este caso, vale "2" (1 por 2) porque la base es 2. Añadiendo estos nos pone 3.   
> Luego viene octal, o base 8. El dígito más a la derecha es 7 y “vale” 7. El dígito del segundo más alto es 1. En este caso, vale “8” (1 por 8) porque la base es 8. Sumando estos nos lleva 15.  
> Finalmente, tenemos hexadecimal, o base 16, que también se conoce como hex. El "dígito" más a la derecha es F y su "valor" es 15 (9 es "vale" 9, A es "vale" 10, B es "vale" 11 y así sucesivamente). El segundo dígito más a la derecha es 1. En este caso, vale 16 (1 por 16) porque la base es 16. Si sumamos estos, obtendremos 31.

The last thing you need to know about numeric literals is a feature added in Java 7. You can have underscores in numbers to make them easier to read:
```java
int million1 = 1000000;
int million2 = 1_000_000;

// You can add underscores anywhere except at the beginning of a literal, 
// the end of a literal, right before a decimal point, or right after a 
// decimal point.
double notAtStart = _1000.00; // DOES NOT COMPILE
double notAtEnd = 1000.00_; // DOES NOT COMPILE
double notByDecimal = 1000_.00; // DOES NOT COMPILE
double annoyingButLegal = 1_00_0.0_0; // this one compiles

```

#### 1.5.2. Reference Types 
---

A **reference type** refers to an object (an instance of a class). Unlike primitive types that hold their values in the memory where the variable is allocated, references do not hold the value of the object they refer to. Instead, a reference “points” to an object by storing the memory address where the object is located, a concept referred to as a __pointer__. Unlike other languages, Java does not allow you to learn what the physical memory address is. You can only use the reference to refer to the object.

```java
java.util.Date today;
String greeting;
```
The today variable is a reference of type Date and can only point to a Date object. The greeting variable is a reference that can only point to a String object. A value is assigned to a reference in one of two ways:

- A reference can be assigned to another object of the same type.
- A reference can be assigned to a new object using the new keyword.
```java
// Reference object:
today = new java.util.Date();
greeting = "How are you?";
```

#### 1.5.3. Key Differences 
---
- Reference types can be assigned null, which means they do not currently refer to an object. 
- Primitive types will give you a compiler error if you attempt to assign them null. 
```java
int value = null; // DOES NOT COMPILE
String s = null;
```
- Reference types can be used to call methods when they do not point to null.
- Primitives do not have methods declared on them. 
```java
String reference = "hello";
int len = reference.length();
int bad = len.length(); // DOES NOT COMPILE
```
- notice that all the primitive types have lowercase type names. 
- All classes that come with Java begin with uppercase.

### 1.6. Declaring and Initializing Variables 
- A variable is a name for a piece of memory that stores data. 
- When you declare a variable, you need to state the variable type along with giving it a name.
- Now that we’ve declared a variable, we can give it a value. This is called __initializing a variable__.

#### 1.6.1. Declaring Multiple Variables 
---
```java
String s1, s2;
String s3 = "yes", s4 = "no";
int i1, i2, i3 = 0;

int num, String value; // DOES NOT COMPILE, different types.

// Exam 
boolean b1, b2;
String s1 = "1", s2;
double d1, double d2; // DOES NOT COMPILE, If you want to declare multiple variables in the same 
			//statement, they must. share the same type declaration and not repeat it. 
int i1; int i2;
int i3; i4; // DOES NOT COMPILE i4;

```

#### 1.6.2. Identifiers 
---
- The name must begin with a letter or the symbol $ or _.
- Subsequent characters may also be numbers.
- You cannot use the same name as a Java reserved word. As you might imagine, a reserved word is a keyword that Java has reserved so that you are not allowed to use it.
- Remember that Java is case sensitive, so you can use versions of the keywords that only differ in case. Please don’t, though.  
   
**Reserved words :**

||||||
|-|-|-|-|-|
|abstract | assert  |boolean  |break | byte |
|case  |catch  |char  |class | const* |
|continue | default  |do  |double  |else |
|enum  |extends  |false  |final  |finally |
|float  |for  |goto*  |if  |implements |
|import | instanceof | int | interface  |long |
|native | new  |null | package  |private |
|protected | public | return | short  |static |
|strictfp | super  |switch |synchronized  |this |
|throw | throws |transient  |true  |try |
|void | volatile | while | | |

```java
// this OK!

okidentifier
$OK2Identifier
_alsoOK1d3ntifi3r
__SStillOkbutKnotsonice$


//This bad

3DPointClass // identifiers cannot begin with a number
hollywood@vine // @ is not a letter, digit, $ or _
*$coffee // * is not a letter, digit, $ or _
public // public is a reserved word

```

- **Method** and **variables** names begin with a lowercase letter followed by CamelCase.
- **Class** names begin with an uppercase letter followed by CamelCase. Don’t start any identifi ers with $. The compiler uses this symbol for some files.


### 1.7. Understanding Default Initialization of Variables 
#### 1.7.1. Local Variables 
---
- is a variable defi ed within a method.
- Local variables must be initialized before use



```java
4: public int notValid() {
5: int y = 10;
6: int x;
7: int reply = x + y; // DOES NOT COMPILE, x might not have been initialized.
8: return reply;
9: }
```
The compiler knows there is the possibility for check to be false, resulting in uninitialized code, and gives a compiler error.

```java
int answer;
int onlyOneBranch;
if (check) {
	onlyOneBranch = 1;
	answer = 1;
} else {
	answer = 2;
}
System.out.println(answer);
System.out.println(onlyOneBranch); // DOES NOT COMPILE
}
```

#### 1.7.2. Instance and Class Variables 
---
- Variables that are not local variables are known as instance variables or class variables.
- Instance variables are also called fi elds. Class variables are shared across multiple objects.
- You can tell a variable is a class variable because it has the keyword static before it.
- Instance and class variables do not require you to initialize them. As soon as you declare these variables, they are given a default value.
- To make this easier, remember that the compiler doesn’t know what value to use and so wants the simplest type it can give the value: null for an object and 0/false for a primitive.

| Variable type | Default initialization value| 
| -| -| 
| boolean | false| 
| byte, short, int, long | 0 (in the type’s bit-length)| 
| float, double | 0.0 (in the type’s bit-length)| 
| char | '\u0000' (NUL)| 
| All object references (everything else) | null| 

### 1.8. Understanding Variable Scope 

### 1.9. Ordering Elements in a Class 

### 1.10. Destroying Objects 
#### 1.10.1. Garbage Collection 
---
#### 1.10.2. finalize() 
---
### 1.11. Benefits of Java

### 1.12. Summary 

### 1.13. Exam Essentials 

### Review Questions














