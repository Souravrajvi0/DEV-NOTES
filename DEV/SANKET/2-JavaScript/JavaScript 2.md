---
view-count: 5
---
![Untitled 71.png](../../Images/Untitled%2071.png)

![Untitled 1 61.png](../../Images/Untitled%201%2061.png)

![Untitled 2 46.png](../../Images/Untitled%202%2046.png)

### 1. **Multiplication (`*`)**

- Used for multiplying two numbers. If one operand is not a number, JavaScript attempts to convert it to a number.
- **Example**:
    `5 * 2       // Result: 10=5 * "2"     // Result: 10 (string "2" is converted to number 2) "5" * "3"   // Result: 15 (both strings are converted to numbers)`


### 2. **Division (`/`)**

- Divides the first operand by the second. JavaScript converts strings to numbers if possible.
- **Example**:
    
    
    
    `10 / 2       // Result: 5= 10 / "2"     // Result: 5 "10" / "2"   // Result: 5`
    

### 3. **Modulus (`%`)**

- Returns the remainder after division.
- **Example**:
    
    
    
    `10 % 3       // Result: 1 =10 % "3"     // Result: 1 (string "3" is converted to number 3)`
    

### 4. **Exponentiation (`**`)**

- Raises the first operand to the power of the second.
- **Example**:
    
    
    
    `2 ** 3       // Result: 8 (2 to the power of 3) "2" ** 3     // Result: 8 (string "2" is converted to number 2)`
    

### 5. **Unary Plus (`+`) and Unary Minus (`-`)**

- The unary `+` operator converts its operand to a number.
- The unary `-` operator converts its operand to a number and negates it.
- **Example**:
    
    
    
    `+"5"         // Result: 5 (string "5" is converted to number 5) -"5"         // Result: -5 (string "5" is converted to number -5)`
    



### 6. **== **  ===
    == (loose equality) allows type coercion, meaning it converts operands to the same type before comparison.
    === (strict equality) does not allow type coercion, so operands must be of the same type and value.

`5 == "5"     // Result: true (type conversion happens)`
`5 === "5"    // Result: false (no type conversion, different types)`



### 7. **Inequality (`!=` and `!==`)**

- `!=` checks if two values are not equal with type conversion.
- `!==` checks if two values are not equal without type conversion.
- **Example**:

    `5 != "5"     // Result: false (type conversion happens) 5 !== "5"    // Result: true (no type conversion, different types)`
    

### 8. **Logical Operators (`&&`, `||`, `!`)**

- Used for logical operations.
- `&&` (AND) returns the first falsy operand or the last operand if all are truthy.
- `||` (OR) returns the first truthy operand or the last operand if all are falsy.
- `!` (NOT) inverts the truthiness of a value.
- **Example**:

    `true && false    // Result: false false || "hello" // Result: "hello" !true            // Result: false`
    

### 9. **Nullish Coalescing (`??`)**

- Returns the right operand if the left operand is `null` or `undefined`.
- **Example**:
    
    `null ?? "default"      // Result: "default" undefined ?? "default" // Result: "default" 0 ?? "default"         // Result: 0 (0 is not null or undefined)`
    

### 10. **Ternary Operator (`condition ? exprIfTrue : exprIfFalse`)**

- A compact form of an if-else statement.
- **Example**:
    
    `const age = 18; const isAdult = age >= 18 ? "Yes" : "No"; // Result: "Yes"`

### 11. **Optional Chaining (`?.`)**

- Allows you to safely access nested properties without causing errors if an intermediate property is `null` or `undefined`.
- **Example**:

    `const person = { name: "Alice", address: { city: "Seattle" } }; console.log(person.address?.city);   // Result: "Seattle" console.log(person.contact?.phone);  // Result: undefined (no error)`


### Summary
![Untitled 3 43.png](../../Images/Untitled%203%2043.png)

![Untitled 4 40.png](../../Images/Untitled%204%2040.png)

![Untitled 5 35.png](../../Images/Untitled%205%2035.png)

![Untitled 6 33.png](../../Images/Untitled%206%2033.png)

![Untitled 7 28.png](../../Images/Untitled%207%2028.png)

![Untitled 8 25.png](../../Images/Untitled%208%2025.png)

![Untitled 9 20.png](../../Images/Untitled%209%2020.png)

![Untitled 10 19.png](../../Images/Untitled%2010%2019.png)

![Untitled 11 17.png](../../Images/Untitled%2011%2017.png)

![Untitled 12 15.png](../../Images/Untitled%2012%2015.png)

![Untitled 13 9.png](../../Images/Untitled%2013%209.png)

In JavaScript, the `+` operator is used for both arithmetic addition and string concatenation. When used with strings, it concatenates them together.  
console.log("My name is sourav" + "rajvi");  

In JavaScript, when you use the `+` operator with a string and a number, the number is automatically converted to a string, and then the strings are concatenated together.  
console.log("My roll number is " + 32);  

console.log(32 + "Is my roll number");

console.log(32 - "Is my roll number");→ Nan Dega // Since - only works on number and string will get converted NAN

---

![Untitled 14 7.png](../../Images/Untitled%2014%207.png)

![Untitled 15 6.png](../../Images/Untitled%2015%206.png)

→SAME OUTPUT

A "templated string" typically refers to a string that contains placeholders or variables that can be replaced with actual values at runtime. These placeholders are often denoted by special symbols or syntax.

For example, in JavaScript or many other programming languages, you might see templated strings using backticks (`) to enclose the string and placeholders represented by `**${}**` inside like →

const name = "John";  
const greeting =  
`Hello, ${name}!`;  
console.log(greeting); // Output: Hello, John!  

![[Images/Untitled 16 6.png|Untitled 16 6.png]]

![[Images/Untitled 17 6.png|Untitled 17 6.png]]

An object is going to get converted into a string the default Tostring implementation will give you an object object

![[Images/Untitled 18 6.png|Untitled 18 6.png]]

Here In when we use an addition operator, We are trying to concatenate an object with a string so in this case the abstract operations will come into play and.

→ but when we try to use string interpolation here also abstract operations come into play which in turn leads to the same result since whatever variable injection we did will also be converted into a string.

![[Images/Untitled 19 6.png|Untitled 19 6.png]]

Explicit Conversion→

![[Images/Untitled 20 6.png|Untitled 20 6.png]]

![[Images/Untitled 21 6.png|Untitled 21 6.png]]

→Two NAN Are never equal to each other

![[Images/Untitled 22 6.png|Untitled 22 6.png]]
FALSE AEGA
![[Images/Untitled 23 5.png|Untitled 23 5.png]]
TRUE
![[Images/Untitled 24 5.png|Untitled 24 5.png]]

TRUE

![[Images/Untitled 25 5.png|Untitled 25 5.png]]

![[Images/Untitled 26 3.png|Untitled 26 3.png]]

![[Images/Untitled 27 3.png|Untitled 27 3.png]]

How to work with -0?

![[Images/Untitled 28 3.png|Untitled 28 3.png]]

x.toString() will give 0 not -0

![[Images/Untitled 29 3.png|Untitled 29 3.png]]

![[Images/Untitled 30 3.png|Untitled 30 3.png]]

![[Images/Untitled 31 3.png|Untitled 31 3.png]]

Internal workings of a Math sign according to ecma script

PRIMITIES AND NON PRIMITIVES

![[Images/Untitled 32 3.png|Untitled 32 3.png]]

BOXING/AUTOBOXING

Primitive types tries to get converted into non primitive types Which is called boxing

![[Images/Untitled 33 3.png|Untitled 33 3.png]]

![[Images/Untitled 34 3.png|Untitled 34 3.png]]

→So in case of 1 which is a literal we can’t use those properties but when we used a number variable we were able to use it

→ Tries to box the values as an object and then apply the properties to it

So in javascript everything can be forced to be looked upon as an object

Though in reality it’s type is not changed into object it’s just treated as an object

![[Images/Untitled 35 3.png|Untitled 35 3.png]]

![[Images/Untitled 36 3.png|Untitled 36 3.png]]

In JavaScript, primitive types are the most basic data types that represent single values. They are immutable (cannot be changed) and are not objects. JavaScript has six primitive types:

1. **Boolean**: Represents a logical value, either `**true**` or `**false**`.
2. **Null**: Represents the intentional absence of any object value.
3. **Undefined**: Represents a variable that has been declared but not assigned a value, or a function that does not return any value.
4. **Number**: Represents numeric data, including integers and floating-point numbers. It can also represent special numeric values such as `**NaN**` (Not-a-Number) and `**Infinity**`.
5. **String**: Represents textual data enclosed in single quotes (`**''**`) or double quotes (`**""**`).
6. **Symbol**: Represents a unique and immutable value that may be used as the key of an object property.