# Chapter 2 Operators and Statements

## 2. Operators and Statements
### 2.1. Understanding Java Operators 
- A Java operator is a special symbol that can be applied to a set of variables, values, or 
- literals—referred to as operands—and that returns a result.
- Three fl avors of operators are available in Java: 
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
In this example, you would fi rst decrement y to 3, and then multiply the resulting value by 2, and fi nally add 3. The value would then be automatically upcast from 9 to 9.0 and assigned to x. The fi nal values of x and y would be 9.0 and 3, respectively. If you didn’t follow that evaluation, don’t worry. By the end of this chapter, solving problems like this should be second nature.

> En este ejemplo, primero reduciría y a 3, y luego multiplicaría el valor resultante por 2, y añadiría finalmente 3. El valor se subirá automáticamente de 9 a 9.0 y se asignará a x. Los valores finales de x e y serían 9.0 y 3, respectivamente. Si no siguió esa evaluación, no se preocupe. Al final de este capítulo, resolver problemas como este debería ser una segunda naturaleza.

Unless overridden with parentheses, Java operators follow **order of operation**, listed in Table 2.1, by decreasing order of **operator precedence**. If two operators have the same level of precedence, then Java guarantees left-to-right evaluation. You need to know only those operators in bold for the OCA exam.

| Operator | Symbols and examples | 
 | -  | -  | 
| Post-unary operators  | expression++, expression-- | 
| Pre-unary operators  | ++expression, --expression | 
| Other unary operators  | +, -, ! | 
| Multiplication/Division/Modulus |  *, /, % | 
| Addition/Subtraction |  +, - | 
| Shift operators |  <<, >>, >>> | 
| Relational operators  | <, >, <=, >=, instanceof | 
| Equal to/not equal to |  ==, != | 
| Logical operators  | &, ^, | | 
| Short-circuit logical operators |  &&, pai-pai | 
| Ternary operators  | boolean expression ? expression1 : expression2 | 
| Assignment operators  | =, +=, -=, *=, /=, %=, &=, ^=, !=, <<=, >>=, >>>= | 

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
### 2.3. Working with Unary Operators
#### 2.3.1. Logical Complement and Negation Operators
---
#### 2.3.2. Increment and Decrement Operators
### 2.4. Using Additional Binary Operators
---
#### 2.4.1. Assignment Operators
#### 2.4.2. Compound Assignment Operators
---
#### 2.4.3. Relational Operators
---
#### 2.4.5. Logical Operators
---
#### 2.4.6. Equality Operators
---
### 2.5. Understanding Java Statements 
#### 2.5.1. The if-then Statement
---
#### 2.5.2. The if-then-else Statement
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