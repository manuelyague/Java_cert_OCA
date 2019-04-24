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

Each Java class is defi ned in its own \* .java file.  
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

Since the code begins with line 1, you don’t get to assume that valid imports were provided earlier. `The exam will let you know what package classes are in unless they’re covered in the objectives. You’ll be expected to know that ArrayList is in java.util—at least you will once you get to Chapter 3 of this book!`

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
> Al contar los inicializadores de instancia, tenga en cuenta que sí importa si las llaves están dentro de un método. Sólo hay un par de llaves fuera de un método. La línea 6 es un inicializador de instancia.

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

| Keyword | Type                        | Example |
| ------- | --------------------------- | ------- |
| boolean | true or false               | true    |
| byte    | 8-bit integral value        | 123     |
| short   | 16-bit integral value       | 123     |
| int     | 32-bit integral value       | 123     |
| long    | 64-bit integral value       | 123     |
| float   | 32-bit floating-point value | 123.45f |
| double  | 64-bit floating-point value | 123.456 |
| char    | 16-bit Unicode value        | 'a'     |

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
>
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

A **reference type** refers to an object (an instance of a class). Unlike primitive types that hold their values in the memory where the variable is allocated, references do not hold the value of the object they refer to. Instead, a reference “points” to an object by storing the memory address where the object is located, a concept referred to as a **pointer**. Unlike other languages, Java does not allow you to learn what the physical memory address is. You can only use the reference to refer to the object.

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
- Now that we’ve declared a variable, we can give it a value. This is called **initializing a variable**.

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

- The name must begin with a letter or the symbol $ or \_.
- Subsequent characters may also be numbers.
- You cannot use the same name as a Java reserved word. As you might imagine, a reserved word is a keyword that Java has reserved so that you are not allowed to use it.
- Remember that Java is case sensitive, so you can use versions of the keywords that only differ in case. Please don’t, though.  


**Reserved words :**

|           |            |           |              |            |
| --------- | ---------- | --------- | ------------ | ---------- |
| abstract  | assert     | boolean   | break        | byte       |
| case      | catch      | char      | class        | const\*    |
| continue  | default    | do        | double       | else       |
| enum      | extends    | false     | final        | finally    |
| float     | for        | goto\*    | if           | implements |
| import    | instanceof | int       | interface    | long       |
| native    | new        | null      | package      | private    |
| protected | public     | return    | short        | static     |
| strictfp  | super      | switch    | synchronized | this       |
| throw     | throws     | transient | true         | try        |
| void      | volatile   | while     |              |            |

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

| Variable type                           | Default initialization value   |
| --------------------------------------- | ------------------------------ |
| boolean                                 | false                          |
| byte, short, int, long                  | 0 (in the type’s bit-length)   |
| float, double                           | 0.0 (in the type’s bit-length) |
| char                                    | '\u0000' (NUL)                 |
| All object references (everything else) | null                           |

### 1.8. Understanding Variable Scope

You’ve learned that local variables are declared within a method.

```java
public void eat(int piecesOfCheese) {
	int bitesOfCheese = 1;
}
```

**`The exam may attempt to trick you with questions on scope.`**

```java
1: public class Mouse {
2: 		static int MAX_LENGTH = 5; //class variable
3: 		int length;	// instance variable
4: 		public void grow(int inches) { //local variables
5: 			if (length < MAX_LENGTH) {
6: 				int newSize = length + inches; //local variables
7: 				length = newSize;
8: 			}
9: 		}
10:}
```

- Local variables—in scope from declaration to end of block
- Instance variables—in scope from declaration until object garbage collected
- Class variables—in scope from declaration until program ends
- There are two local variables in this method.
- bitesOfCheese is declared inside the method.
- piecesOfCheese is called a method parameter.

### 1.9. Ordering Elements in a Class

| Element             | Example              | Required? | Where does it go?             |
| ------------------- | -------------------- | --------- | ----------------------------- |
| Package declaration | package abc;         | No        | First line in the file        |
| Import statements   | import java.util.\*; | No        | Immediately after the package |
| Class declaration   | public class C       | Yes       | Immediately after the import  |
| Field declarations  | int value;           | No        | Anywhere inside a class       |
| Method declarations | void method()        | No        | Anywhere inside a class       |

You need to know one more thing about class structure for the OCA exam:

- multiple classes can be defi ned in the same file, but only one of them is allowed to be public.
- The public class matches the name of the file.

```java
1: public class Meerkat { }
2: class Paw { }
```

### 1.10. Destroying Objects

- Java provides a garbage collector to automatically look for objects that aren’t needed anymore.
- All Java objects are stored in your program memory’s heap.

#### 1.10.1. Garbage Collection

---

- Process of automatically freeing memory on the heap by deleting objects that are no longer reachable in your program.
- You do need to know that System.gc() is not guaranteed to run, and you should be able to recognize when objects become eligible for garbage collection.
- System.gc()., Java is free to ignore the request.
- Java waits patiently until the code no longer needs that memory.
  An object will remain on the heap until it is no longer reachable. An object is no longer reachable when one of two situations occurs: - he object no longer has any references pointing to it. - All references to the object have gone out of scope.

> - El objeto ya no tiene ninguna referencia que lo señale.
> - Todas las referencias al objeto han quedado fuera de alcance.

- The **reference** is a variable that has a name and can be used to access the contents of an object. A **reference** can be assigned to another reference, passed to a method, or returned from a method. All references are the same size, no matter what their type is.
  An **object** sits on the heap and does not have a name. Therefore, you have no way to access an object except through a reference. Objects come in all different shapes and sizes and consume varying amounts of memory. An object cannot be assigned to another object, nor can an object be passed to a method or returned from a method. It is the object that gets garbage collected, not its reference.

- **figure 1**

```java
1: public class Scope {
2: public static void main(String[] args) {
3: String one, two;
4: one = new String("a");
5: two = new String("b");
6: one = two;
7: String three = one;
8: one = null;
9: } }
```

When you get asked a question about garbage collection on the exam, we recommend you draw what’s going on. There’s a lot to keep track of in your head and it’s easy to make a silly mistake trying to keep it all in your memory. Let’s try it together now. Really. Get a pencil and paper. We’ll wait.

Got that paper? Okay, let’s get started. On line 3, we write one and two. Just the words. No need for boxes or arrows yet since no objects have gone on the heap yet. On line 4, we have our fi rst object. Draw a box with the string "a" in it and draw an arrow from the word one to that box. Line 5 is similar. Draw another box with the string "b" in it this time and an arrow from the word two. At this point, your work should look like Figure 1.2.

- **figure 2**

On line 6, the variable one changes to point to "b". Either erase or cross out the arrow from one and draw a new arrow from one to "b". On line 7, we have a new variable, so write the word three and draw an arrow from three to "b". Notice that three points to what one is pointing to right now and not what it was pointing to at the beginning. This is why we are drawing pictures. It’s easy to forget something like that. At this point, your work should look like Figure 1.3.

- **figure 3**

Finally, cross out the line between one and "b" since line 8 sets this variable to null. Now, we were trying to fi nd out when the objects were fi rst eligible for garbage collection. On line 6, we got rid of the only arrow pointing to "a", making that object eligible for garbage collection. "b" has arrows pointing to it until it goes out of scope. This means "b" doesn’t go out of scope until the end of the method on line 9.

#### 1.10.2. finalize()

---

- This method gets called if the garbage collector tries to collect the object.
- Remember, finalize() is only run when the object is eligible for garbage collection.
- The
  problem here is that by the end of the method, the object is no longer eligible for garbage collection because a static variable is referring to it and static variables stay in scope until the program ends. Java is smart enough to realize this and aborts the attempt to throw out the object. Now suppose later in the program objects is set to null. Oh, good, we can finally remove the object from memory. Java remembers already running finalize() on this object and will not do so again. The lesson is that the finalize() call could run zero or one time. This is the exact same lesson as the simple example—that’s why it’s so easy to

### 1.11. Benefits of Java

- **Object Oriented**, which means all code is defined in classes and most of those classes can be instantiated into objects.
- **Encapsulation** access modifiers to protect data from unintended access and modification.
- **Platform Independent** Java is an interpreted language because it gets compiled to bytecode.
- **Robust** One of the major advantages of Java over C++ is that it prevents memory leaks. Java manages memory on its own and does garbage collection automatically. Bad memory management in C++ is a big source of errors in programs.
- **Simple** Java was intended to be simpler than C++. - **In addition to eliminating pointers**, it got rid of operator overloading. In C++, you could write a + b and have it mean almost anything.
- **Secure Java code runs inside the JVM**. This creates a sandbox that makes it hard for Java code to do evil things to the computer it is running on.

### 1.12. Summary

### 1.13. Exam Essentials

- **Be able to write code using a main() method**. A main() method is usually written as public static void main(String[] args). Arguments are referenced starting with args[0]. Accessing an argument that wasn’t passed in will cause the code to throw an exception.
- **Understand the effect of using packages and imports** . Packages contain Java classes. Classes can be imported by class name or wildcard. Wildcards do not look at subdirectories. In the event of a confl ict, class name imports take precedence.
- **Be able to recognize a constructor**. A constructor has the same name as the class. It looks like a method without a return type.
  **Be able to identify legal and illegal declarations and initialization**. Multiple variables can be declared and initialized in the same statement when they share a type. Local variables require an explicit initialization; others use the default value for that type. Identifi ers may contain letters, numbers, $, or \_. Identifi ers may not begin with numbers. Numeric literals may contain underscores between two digits and begin with 1–9, 0, 0x, 0X, 0b, and 0B.
- **Be able to determine where variables go into and out of scope**. All variables go into scope when they are declared. Local variables go out of scope when the block they are declared in ends. Instance variables go out of scope when the object is garbage collected. Class variables remain in scope as long as the program is running.
- **Be able to recognize misplaced statements in a class**. Package and import statements are optional. If present, both go before the class declaration in that order. Fields and methods are also optional and are allowed in any order within the class declaration.
- **Know how to identify when an object is eligible for garbage collection**. Draw a diagram to keep track of references and objects as you trace the code. When no arrows point to a box (object), it is eligible for garbage collection.

### Review Questions

1. Which of the following are valid Java identifiers? (Choose all that apply)

- A. A$B :heavy_check_mark: :heavy_check_mark:
- B. \_helloWorld :heavy_check_mark:
- C. true
- D. java.lang
- E. Public :heavy_check_mark: :heavy_check_mark:
- F. 1980_s

2. What is the output of the following program?

```java
1: public class WaterBottle {
2: private String brand;
3: private boolean empty;
4: public static void main(String[] args) {
5: WaterBottle wb = new WaterBottle();
6: System.out.print("Empty = " + wb.empty);
7: System.out.print(", Brand = " + wb.brand);
8: } }
```

- A. Line 6 generates a compiler error.
- B. Line 7 generates a compiler error.
- C. There is no output.
- D. Empty = false, Brand = null :heavy_check_mark:
- E. Empty = false, Brand =
- F. Empty = null, Brand = null

3. Which of the following are true? (Choose all that apply)

```java
4: short numPets = 5;
5: int numGrains = 5.6;
6: String name = "Scruffy";
7: numPets.length();
8: numGrains.length();
9: name.length();
```

- A. Line 4 generates a compiler error.
- B. Line 5 generates a compiler error. :heavy_check_mark:
- C. Line 6 generates a compiler error.
- D. Line 7 generates a compiler error. :heavy_check_mark:
- E. Line 8 generates a compiler error. :heavy_check_mark:
- F. Line 9 generates a compiler error.
- G. The code compiles as is.

4. Given the following class, which of the following is true? (Choose all that apply)

```java
1: public class Snake {
2:
3: public void shed(boolean time) {
4:
5: if (time) {
6:
7: }
8: System.out.println(result);
9:
10: }
11: }
```

- A. If String result = "done"; is inserted on line 2, the code will compile. :heavy_check_mark:
- B. If String result = "done"; is inserted on line 4, the code will compile. :heavy_check_mark:
- C. If String result = "done"; is inserted on line 6, the code will compile.
- D. If String result = "done"; is inserted on line 9, the code will compile.
- E. None of the above changes will make the code compile.

5. Given the following classes, which of the following can independently replace INSERT IMPORTS HERE to make the code compile? (Choose all that apply)

```java
package aquarium;
public class Tank { }

package aquarium.jellies;
public class Jelly { }

package visitor;
INSERT IMPORTS HERE
public class AquariumVisitor {
	public void admire(Jelly jelly) { } }
```

- A. import aquarium.\*;
- B. import aquarium.\*.Jelly;
- C. import aquarium.jellies.Jelly; :heavy_check_mark:
- D. import aquarium.jellies.\*; :heavy_check_mark:
- E. import aquarium.jellies.Jelly.\*;
- F. None of these can make the code compile.

6. Given the following classes, what is the maximum number of imports that can be removed and have the code still compile?

```java
package aquarium; public class Water { }

package aquarium;
import java.lang.*;
import java.lang.System;
import aquarium.Water;
import aquarium.*;
public class Tank {
	public void print(Water water) {
		System.out.println(water); } }
```

- A. 0
- B. 1
- C. 2
- D. 3 :heavy_check_mark: :heavy_check_mark:
- E. 4
- F. Does not compile.

7. Given the following classes, which of the following snippets can be inserted in place of INSERT IMPORTS HERE and have the code compile? (Choose all that apply)

```java
package aquarium;
public class Water {
	boolean salty = false;
}

package aquarium.jellies;
public class Water {
	boolean salty = true;
}

package employee;
INSERT IMPORTS HERE
public class WaterFiller {
	Water water;
}
```

- A. import aquarium.\*; :heavy_check_mark:
- B. import aquarium.Water; :heavy_check_mark: :heavy_check_mark: - import aquarium.jellies.\*;
- C. import aquarium.\*; :heavy_check_mark: :heavy_check_mark: - import aquarium.jellies.Water;
- D. import aquarium._; - import aquarium.jellies._;
- E. import aquarium.Water; - import aquarium.jellies.Water;
- F. None of these imports can make the code compile.

8. Given the following class, which of the following calls print out Blue Jay? (Choose all that apply)

```java
public class BirdDisplay {
public static void main(String[] name) {
	System.out.println(name[1]);
} }
```

- A. java BirdDisplay Sparrow Blue Jay
- B. java BirdDisplay Sparrow "Blue Jay" :heavy_check_mark:
- C. java BirdDisplay Blue Jay Sparrow
- D. java BirdDisplay "Blue Jay" Sparrow
- E. java BirdDisplay.class Sparrow "Blue Jay"
- F. java BirdDisplay.class "Blue Jay" Sparrow
- G. Does not compile.

9. Which of the following legally fill in the blank so you can run the main() method from the command line? (Choose all that apply)

```java
public static void main( )
```

- A. String[] \_names :heavy_check_mark:
- B. String[] 123
- C. String abc[] :heavy_check_mark:
- D. String \_Names[] :heavy_check_mark:
- E. String... $n :heavy_check_mark:
- F. String names
- G. None of the above.

10. Which of the following are legal entry point methods that can be run from the command line? (Choose all that apply)

- A. private static void main(String[] args)
- B. public static final main(String[] args)
- C. public void main(String[] args)
- D. public static void test(String[] args)
- E. public static void main(String[] args) :heavy_check_mark:
- F. public static main(String[] args)
- G. None of the above.

11. Which of the following are true? (Choose all that apply)

- A. An instance variable of type double defaults to null.
- B. An instance variable of type int defaults to null.
- C. An instance variable of type String defaults to null. :heavy_check_mark:
- D. An instance variable of type double defaults to 0.0. :heavy_check_mark: :heavy_check_mark:
- E. An instance variable of type int defaults to 0.0.
- F. An instance variable of type String defaults to 0.0.
- G. None of the above.

12. Which of the following are true? (Choose all that apply)

- A. A local variable of type boolean defaults to null.
- B. A local variable of type float defaults to 0.
- C. A local variable of type Object defaults to null.
- D. A local variable of type boolean defaults to false.
- E. A local variable of type boolean defaults to true.
- F. A local variable of type float defaults to 0.0.
- G. None of the above. :heavy_check_mark: :heavy_check_mark:

> local variables do not get assigned default values.

13. Which of the following are true? (Choose all that apply)

- A. An instance variable of type boolean defaults to false. :heavy_check_mark:
- B. An instance variable of type boolean defaults to true.
- C. An instance variable of type boolean defaults to null.
- D. An instance variable of type int defaults to 0. :heavy_check_mark:
- E. An instance variable of type int defaults to 0.0.
- F. An instance variable of type int defaults to null.
- G. None of the above.

14. Given the following class in the file /my/directory/named/A/Bird.java:
    INSERT CODE HERE public class Bird { }

Which of the following replaces INSERT CODE HERE if we compile from /my/directory? (Choose all that apply)

- A. package my.directory.named.a;
- B. package my.directory.named.A;
- C. package named.a;
- D. package named.A; :heavy_check_mark:
- E. package a;
- F. package A;
- G. Does not compile.

15. Which of the following lines of code compile? (Choose all that apply)

- A. int i1 = 1_234; :heavy_check_mark:
- B. double d1 = 1*234*.0;
- C. double d2 = 1_234.\_0;
- D. double d3 = 1*234.0*;
- E. double d4 = 1_234.0; :heavy_check_mark:
- F. None of the above.

16. Given the following class, which of the following lines of code can replace INSERT CODE HERE to make the code compile? (Choose all that apply)

```java
public class Price {
public void admission() {
INSERT CODE HERE
System.out.println(amount);
} }
```

- A. int amount = 9L;
- B. int amount = 0b101; :heavy_check_mark:
- C. int amount = 0xE; :heavy_check_mark:
- D. double amount = 0xE; :heavy_check_mark: :heavy_check_mark:
- E. double amount = 1*2*.0_0;
- F. int amount = 1*2*;
- G. None of the above.

17. Which of the following are true? (Choose all that apply)

```java
public class Bunny {
public static void main(String[] args) {
	Bunny bun = new Bunny();
} }
```

- A. Bunny is a class. :heavy_check_mark:
- B. bun is a class.
- C. main is a class.
- D. Bunny is a reference to an object.
- E. bun is a reference to an object. :heavy_check_mark:
- F. main is a reference to an object.
- G. None of the above.

18. Which represent the order in which the following statements can be assembled into a program that will compile successfully? (Choose all that apply)

```java
A: class Rabbit {}
B: import java.util.*;
C: package animals;
```

- A. A, B, C
- B. B, C, A
- C. C, B, A :heavy_check_mark:
- D. B, A :heavy_check_mark: :heavy_check_mark:
- E. C, A :heavy_check_mark: :heavy_check_mark:
- F. A, C
- G. A, B

19. Suppose we have a class named Rabbit. Which of the following statements are true? (Choose all that apply)

```java
1: public class Rabbit {
2: public static void main(String[] args) {
3: 		Rabbit one = new Rabbit();
4: 		Rabbit two = new Rabbit();
5: 		Rabbit three = one;
6: 		one = null;
7: 		Rabbit four = one;
8: 		three = null;
9: 		two = null;
10: 	two = new Rabbit();
11: 	System.gc();
12: } }
```

- A. The Rabbit object from line 3 is first eligible for garbage collection immediately following line 6.
- B. The Rabbit object from line 3 is first eligible for garbage collection immediately following line 8. :heavy_check_mark:
- C. The Rabbit object from line 3 is first eligible for garbage collection immediately following line 12.
- D. The Rabbit object from line 4 is first eligible for garbage collection immediately following line 9. :heavy_check_mark: :heavy_check_mark:
- E. The Rabbit object from line 4 is first eligible for garbage collection immediately following line 11.
- F. The Rabbit object from line 4 is first eligible for garbage collection immediately following line 12.

20. What is true about the following code? (Choose all that apply)

```java
public class Bear {
	protected void finalize() {
		System.out.println("Roar!");
	}

	public static void main(String[] args) {
		Bear bear = new Bear();
		bear = null;
		System.gc();
		} }
```

- A. finalize() is guaranteed to be called.
- B. finalize() might or might not be called :heavy_check_mark: :heavy_check_mark:s
- C. finalize() is guaranteed not to be called.
- D. Garbage collection is guaranteed to run.
- E. Garbage collection might or might not run. :heavy_check_mark:
- F. Garbage collection is guaranteed not to run.
- G. The code does not compile.

21. What does the following code output?

```java
1: public class Salmon {
2: 		int count;
3: 		public void Salmon() {
4: 			count = 4;
5: 		}
6: 		public static void main(String[] args) {
7: 			Salmon s = new Salmon();
8: 			System.out.println(s.count);
9: 			} }
```

- A. 0 :heavy_check_mark:
- B. 4
- C. Compilation fails on line 3.
- D. Compilation fails on line 4.
- E. Compilation fails on line 7.
- F. Compilation fails on line 8.

22. Which of the following are true statements? (Choose all that apply)

- A. Java allows operator overloading. :heavy_check_mark:
- B. Java code compiled on Windows can run on Linux. :heavy_check_mark:
- C. Java has pointers to specific locations in memory.
- D. Java is a procedural language.
- E. Java is an object-oriented language. :heavy_check_mark:
- F. Java is a functional programming language.

23. Which of the following are true? (Choose all that apply)

- A. javac compiles a .class file into a .java file.
- B. javac compiles a .java file into a .bytecode file.
- C. javac compiles a .java file into a .class file. :heavy_check_mark:
- D. Java takes the name of the class as a parameter. :heavy_check_mark: :heavy_check_mark:
- E. Java takes the name of the .bytecode file as a parameter.
- F. Java takes the name of the .class file as a parameter.
