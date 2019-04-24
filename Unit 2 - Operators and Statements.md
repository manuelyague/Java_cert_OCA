# Chapter 2 Operators and Statements

## 2. Operators and Statements
### 2.1. Understanding Java Operators 
- A Java operator is a special symbol that can be applied to a set of variables, values, or 
- literals—referred to as operands—and that returns a result.
- Three flavors of operators are available in Java: 
	- unary, 
	- binary, and 
	- ternary. 
- not necessarily evaluated from left-to-right order.

```java
//evaluated from right-to-left given the specifi c operators
involved:
int y = 4;
double x = 3 + 2 * --y;
```
In this example, you would first decrement y to 3, and then multiply the resulting value by 2, and fi nally add 3. The value would then be automatically upcast from 9 to 9.0 and assigned to x. The fi nal values of x and y would be 9.0 and 3, respectively. If you didn’t follow that evaluation, don’t worry. By the end of this chapter, solving problems like this should be second nature.P

> En este ejemplo, primero reduciría y a 3, y luego multiplicaría el valor resultante por 2, y añadiría finalmente 3. El valor se subirá automáticamente de 9 a 9.0 y se asignará a x. Los valores finales de x e y serían 9.0 y 3, respectivamente. Si no siguió esa evaluación, no se preocupe. Al final de este capítulo, resolver problemas como este debería ser una segunda naturaleza.
 
Unless overridden with parentheses, Java operators follow **order of operation**, listed in Table 2.1, by decreasing order of **operator precedence**. If two operators have the same level of precedence, then Java guarantees left-to-right evaluation. You need to know only those operators in bold for the OCA exam.
 
| Operator                        | Symbols and examples                              |
| ------------------------------- | ------------------------------------------------- |
| Post-unary operators            | expression++, expression--                        |
| Pre-unary operators             | ++expression, --expression                        |
| Other unary operators           | +, -, !                                           |
| Multiplication/Division/Modulus | *, /, %                                           |
| Addition/Subtraction            | +, -                                              |
| Shift operators                 | <<, >>, >>>                                       |
| Relational operators            | <, >, <=, >=, instanceof                          |
| Equal to/not equal to           | ==, !=                                            |
| Logical operators               | &, ^,                                             |
| Short-circuit logical operators | &&, pai-pai                                       |
| Ternary operators               | boolean expression ? expression1 : expression2    |
| Assignment operators            | =, +=, -=, *=, /=, %=, &=, ^=, !=, <<=, >>=, >>>= |

### 2.2. Working with Binary Arithmetic Operators 
#### 2.2.1. Arithmetic Operators 
---
- Arithmetic operators are often encountered in early mathematics and include addition (+), subtraction (-), multiplication ( * ), division (/), and modulus (%). 
- They also include the unary operators, ++ and --
- the multiplicative operators ( * , /, %) have a higher order of precedence than the additive operators (+, -).
```java
	int x = 2 * 5 + 3 * 4 - 8; //
```
you first evaluate the 2 * 5 and 3 * 4, which reduces the expression to the following:
```java
	int x = 10 + 12 - 8; // left-to-right order

	int x = 2 * ((5 + 3) * 4 – 8); // change the order of operation explicitly by wrapping parentheses around the sections you want evaluated first.
```
- division results in the fl oor value of the nearest integer that fulfills the operation,
- whereas modulus is the remainder value
```java
System.out.print(9 / 3); // Outputs 3
System.out.print(9 % 3); // Outputs 0

System.out.print(10 / 3); // Outputs 3
System.out.print(10 % 3); // Outputs 1

System.out.print(11 / 3); // Outputs 3
System.out.print(11 % 3); // Outputs 2

System.out.print(12 / 3); // Outputs 4
System.out.print(12 % 3); // Outputs 0
```
Note that the division results only increase when the value on the left-hand side goes from 9 to 12, whereas the modulus remainder value increases by 1 each time the left-hand side is increased until it wraps around to zero. For a given divisor y, which is 3 in these examples, the modulus operation results in a value between 0 and (y - 1) for positive dividends. This means that the result of a modulus operation is always 0, 1, or 2.

> Dados dos números positivos, a (el dividendo) y n (el divisor), a módulo n (abreviado como a mod n) es el resto de la división euclídea de a por n. Por ejemplo, la expresión "5 mod 2" se evaluaría a 1 porque 5 dividido por 2 da un cociente de 2 y un resto de 1, mientras que "9 mod 3" se evaluaría a 0 porque la división de 9 entre 3 tiene un cociente de 3 y da un resto de 0. 

#### 2.2.2.  Numeric Promotion 
---
**Rules**:  
1. If two values have different data types, `Java will automatically promote one of the values to the larger of the two data types`.
2. If one of the values is __integral__ and the other is __floating-point__, `Java will automatically promote the integral value to the floating-point` value’s data type.
3. Smaller data types, namely __byte__, __short__, and __char__, are `first promoted to int any time they’re used with a Java binary arithmetic operator`, even if neither of the operands is int.
4. After all `promotion has occurred` and the `operands have the same data type`, the resulting value will have the `same` data type as its promoted operands.

**Example**
```java
//x * y
int x = 1;
long y = 33;
// If we follow the fi rst rule, since one of the values is long and the other 
//is int, and longis larger than int, then the int value is promoted to a 
//long, and the resulting value is long.

// X + y
double x = 39.21;
float y = 2.1; // No compile 2.1f

// x / y?
short x = 10;
short y = 3;
// the third rule, namely that x and y will both be promotedto int before the 
// operation, resulting in an output of type int. Pay close attention to the 
// fact that the resulting output is not a short,

// x * y / z
short x = 14;
float y = 13;
double z = 30;
// apply all of the rules. First, x will automatically be promoted to int
// solely because it is a short and it is being used in an arithmetic binary operation.
// The promoted x value will then be automatically promoted to a float so 
// that it can be multiplied with y. The result of x * y will then be 
// automatically promoted to a double, so that it can be multiplied with z, 
// resulting in a double value.
```

### 2.3. Working with Unary Operators

By definition, a **unary** operator is one that requires exactly one operand, or variable, to function.  

| Unary operator | Description                                                                                                                          |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| +              | Indicates a number is positive, although numbers are assumed  to be positive in Java unless accompanied by a negative unary operator |
| -              | Indicates a literal number is negative or negates an expression                                                                      |
| ++             | Increments a value by 1                                                                                                              |
| --             | Decrements a value by 1                                                                                                              |
| !              | Inverts a Boolean’s logical value                                                                                                   |

#### 2.3.1. Logical Complement and Negation Operators
---
The **logical complement** operator, **!**, fl ips the value of a boolean expression. For example, if the value is true, it will be converted to false, and vice versa. To illustrate this, compare the outputs of the following statements:

```java
boolean x = false;
System.out.println(x); // false
x = !x;
System.out.println(x); // true
```

Likewise, the **negation operator**, **-**, reverses the sign of a numeric expression, as shown in these statements:

```java
double x = 1.21;
System.out.println(x); // 1.21
x = -x;
System.out.println(x); // -1.21
x = -x;
System.out.println(x); // 1.21
```
Cannot apply a negation operator, -, to a boolean expression, nor can you apply a logical complement operator, !, to a numeric expression.

```java
int x = !5; // DOES NOT COMPILE
boolean y = -true; // DOES NOT COMPILE
boolean z = !0; // DOES NOT COMPILE
```

#### 2.3.2. Increment and Decrement Operators

`Increment` and `decrement` operators, ++ and --, respectively, can be applied to `numeric operands` and `have the higher order` or `precedence`, as `compared to binary operators`. In other words, they often get `applied first to an expression`.

`Increment` and `decrement` operators require special care because `the order they are applied to their associated operand can make a difference in how an expression is processed`. 

- `If the operator is placed before the operand`, `referred to as the pre-increment operator and the pre-decrement operator`, `then the operator is applied first and the value return is the new value of the expression`. 

- Alternatively, `if the operator is placed after the operand, referred to as the post-increment operator and the post-decrement operator, then the original value of the expression is returned, with operator applied after the value is returned`.   

**Example**
```java
int counter = 0;
System.out.println(counter); // Outputs 0
System.out.println(++counter); // Outputs 1
System.out.println(counter); // Outputs 1
System.out.println(counter--); // Outputs 1
System.out.println(counter); // Outputs 0
```

**Example**
```java
int x = 3;
int y = ++x * 5 / x-- + --x;
System.out.println("x is " + x);
System.out.println("y is " + y);

int y = 4 * 5 / x-- + --x; // the x is incremented, x assigned value of 4
int y = 4 * 5 / 4 + --x; // x assigned value of 3
int y = 4 * 5 / 4 + 2; // x assigned value of 2

// finaly
x is 2
y is 7
``` 

### 2.4. Using Additional Binary Operators
#### 2.4.1. Assignment Operators
---
Is a binary operator that modifi es, or assigns, the variable on the left-hand side of the operator, with the result of the value on the right-hand side of the equation.

```java
int x = 1;
```

#### 2.4.2. Casting Primitive Values
---
Casting primitives is required any time you are going from a larger numerical data type to a smaller numerical data type, or converting from a fl oating-point number to an integral value.

```java
int x = (int)1.0;
short y = (short)1921222; // Stored as 20678
int z = (int)9l;
long t = 192301398193810323L;
```
> **Overflow and Underflow**
> The expressions in the previous example now compile, although there’s a cost. The second value, 1,921,222, is too large to be stored as a short, so numeric overfl ow occurs and it becomes 20,678. Overfl ow is when a number is so large that it will no longer fit within the data type, so the system “wraps around” to the next lowest value and counts up from there. There’s also an analogous underfl ow, when the number is too low to fi t in the data type.  
> This is beyond the scope of the exam, but something to be careful of in your own code.
> For example, the following statement outputs a negative number:  
> System.out.print(2147483647+1); // -2147483648  
> Since 2147483647 is the maximum int value, adding any strictly positive value to it will cause it to wrap to the next negative number.

```java
short x = 10;
short y = 3;
short z = x * y; // DOES NOT COMPILE
```
Short values are automatically promoted to int when applying any arithmetic operator, with the resulting value being of type int. Trying to set a short variable to an int results in a compiler error, as Java thinks you are trying to implicitly convert from a larger data type to a smaller one.
```java
short x = 10;
short y = 3;
short z = (short)(x * y);
```

#### 2.4.3. Compound Assignment Operators

Los operadores complejos son simplemente formas glorificadas del operador de asignación simple, con una operación aritmética o lógica integrada que aplica los lados izquierdo y derecho de la declaración y almacena el valor resultante en una variable en el lado izquierdo de la declaración.

```java
int x = 2, z = 3;
x = x * z; // Simple assignment operator
x *= z; // Compound assignment operator
```
Esta última línea podría fijarse con una conversión explícita a (int), pero hay una mejor manera de usar el operador de asignación compuesto:

```java
long x = 10;
int y = 5;
y *= x;
```
The compound operator will fi rst cast x to a long, apply the multiplication of two long values, and then cast the result to an int. Unlike the previous example, in which the compiler threw an exception, in this example we see that the compiler will automatically cast the resulting value to the data type of the value on the left-hand side of the compound operator.  

One fi nal thing to know about the assignment operator is that the result of the assignment is an expression in and of itself, equal to the value of the assignment. For example, the following snippet of code is perfectly valid, if not a little odd looking:
```java
long x = 5;
long y = (x=3);
System.out.println(x); // Outputs 3
System.out.println(y); // Also, outputs 3
```

La clave aquí es que (x = 3) hace dos cosas. Primero, establece que el valor de la variable x sea 3. En segundo lugar, devuelve un valor de la asignación, que también es 3. A los creadores de exámenes les gusta insertar el operador de asignación = en la mitad de una expresión y usar el valor de la asignación como parte de una expresión más compleja.

#### 2.4.4. Relational Operators
---
- Compare two expressions and return a boolean value.
- applied to numeric primitive data types only:
  - **<** Strictly less than
  - **<=** Less than or equal to
  - **>** Strictly greater than
  - **>=** Greater than or equal to

```java
int x = 10, y = 20, z = 10;
System.out.println(x < y); // Outputs true
System.out.println(x <= y); // Outputs true
System.out.println(x >= z); // Outputs true
System.out.println(x > z); // Outputs false
```

#### 2.4.5. Logical Operators
---
| x & y (AND) | -      | -       |
| ----------- | ------ | ------- |
| -           | y=true | y=false |
| x=true      | true   | false   |
| x=false     | false  | false   |

| x & y (inclusive OR) | -      | -       |
| -------------------- | ------ | ------- |
| -                    | y=true | y=false |
| x=true               | true   | true    |
| x=false              | true   | false   |

| x ^ y (Exclusive OR) | -      | -       |
| -------------------- | ------ | ------- |
| -                    | y=true | y=false |
| x=true               | false  | true    |
| x=false              | true   | false   |

Here are some tips to help remember this table:
- AND is only true if both operands are true.
- Inclusive OR is only false if both operands are false.
- Exclusive OR is only true if the operands are different.

conditional operators, && and ||, which are often referred to as `short-circuit operators`. The `short-circuit operators` are nearly identical to the logical operators, & and |, respectively, except that the right-hand side of the expression may never be evaluated if the fi nal result can be determined by the left-hand side of the expression.
```java
boolean x = true || (y < 4);

if(x != null && x.getValue() < 5) { //short-circuit prevents a NullPointerException
// Do something
}

int x = 6;
boolean y = (x >= 6) || (++x <= 7);
System.out.println(x); //Because x >= 6 is true, the increment operator on the right-hand side of the expression is never evaluated, so the output is 6.
```

#### 2.4.7. Equality Operators
---
== Equals
!= not equals   
   
The equality operators are used in one of three scenarios:
1. Comparing two numeric primitive types. If the numeric values are of different data types, the values are automatically promoted as previously described. For example, 5 == 5.00 returns true since the left side is promoted to a double.
2. Comparing two boolean values.
3. Comparing two objects, including null and String values.

 ```java
boolean x = true == 3; // DOES NOT COMPILE
boolean y = false != "Giraffe"; // DOES NOT COMPILE
boolean z = 3 == "Kangaroo"; // DOES NOT COMPILE
 ```
 example: 
 ```java
File x = new File("myFile.txt");
File y = new File("myFile.txt");
File z = x;
System.out.println(x == y); // Outputs false
System.out.println(x == z); // Outputs true
```
In particular, you should be able to answer questions that indicate x and y are two separate and distinct objects, even if you do not know the data types of these objects.

### 2.5. Understanding Java Statements
- Java statement is a complete unit of execution in Java, terminated with a semicolon (;).

#### 2.5.1. The if-then Statement
---
```java
if(booleanExpression){
	//Branch if true
}
```
#### 2.5.2. The if-then-else Statement
---
```java
if(booleanExpression){
	//Branch if true
}else{
	//Branch if false
}

/////

int x = 1;
if(x) { // DOES NOT COMPILE
...
}

int x = 1;
if(x = 5) { // DOES NOT COMPILE
...
}
```
#### Ternary Operator
---
The conditional operator, ? :, otherwise known as the `ternary operator`, is the only operator that takes three operands and is of the form:
- **booleanExpression ? expression1 : expression2**
the following two snippets of code are equivalent:
```java
int y = 10;
final int x;
if(y > 5) {
	x = 2 * y;
} else {
	x = 3 * y;
}

int y = 10;
int x = (y > 5) ? (2 * y) : (3 * y);
```
Compare the following two statements:
```java
System.out.println((y > 5) ? 21 : "Zebra");
int animal = (y < 91) ? 9 : "Horse"; // DOES NOT COMPILE
```
Both expressions evaluate similar boolean values and return an int and a String, although only the fi rst line will compile. The System.out.println() does not care that the statements are completely different types, because it can convert both to String. On the other hand, the compiler does know that "Horse" is of the wrong data type and cannot be assigned to an int; therefore, it will not allow the code to be compiled.
	
#### 2.5.3. The switch Statement
---
#### 2.5.4. The while Statement 
---
#### 2.5.5. The do-while Statement
---
#### 2.5.6. The for Statement
---
### 2.6. Understanding Advanced Flow Control
#### 2.6.1. Nested Loops
---
#### 2.6.2. Adding Optional Labels
---
#### 2.6.3. The break Statement
---
#### 2.6.4. The continue Statement
---
### 2.7. Summary
### 2.8. Exam Essentials
### 2.9. Review Questions