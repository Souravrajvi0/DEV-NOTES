Java has **8 primitive types**:

|Type|Size|Range|
|---|---|---|
|`byte`|1 byte|-128 to 127|
|`short`|2 bytes|approx ±32k|
|`int`|4 bytes|approx ±2B|
|`long`|8 bytes|huge|
|`float`|4 bytes|decimal|
|`double`|8 bytes|larger decimal|
|`char`|2 bytes|Unicode (0–65535)|
|`boolean`|1 bit|true/false|
# **1️⃣ Widening (Implicit) Typecasting**
Also called **automatic type conversion**.

### ✔ When it happens?

- When you convert a **smaller datatype → bigger datatype**
- Java does it **automatically**
- **No data loss**

### Order of widening

`byte → short → int → long → float → double`

### Example:

```
int a = 10;
double b = a;   // automatic conversion from int → double
```

You don’t need to write any cast manually.

### Why does it work automatically?

- Because larger data types can store all values of smaller types safely.

---

# **2️⃣ Narrowing (Explicit) Typecasting**

Also called **manual conversion**.

### ✔ When it happens?

- When converting a **bigger datatype → smaller datatype**
- Java **requires explicit cast**
- ⚠ May cause data loss

### Example:

```
double x = 10.75;
int y = (int) x;  // explicit cast (double → int)
System.out.println(y); // Output: 10 (decimal lost)
```

You must write `(type)` manually

---

# **Visual Difference**

- **Widening casting** goes from small → big (safe, automatic)
- **Narrowing casting** goes from big → small (unsafe, manual)

---

# **3️⃣ Typecasting with Non-Primitive Types**

Java also allows casting **objects**, but with rules.

### ✔ Upcasting (Implicit)

Child → Parent

```
class Animal {}
class Dog extends Animal {}

Dog d = new Dog();
Animal a = d;  // upcasting - automatic
```

### ✔ Downcasting (Explicit)

Parent → Child

```
Animal a = new Dog();
Dog d = (Dog) a; // downcasting - manual
```

If the object is NOT actually a Dog, this will throw `ClassCastException`.

---

# **4️⃣ Typecasting in Expressions**

Java will automatically promote values in expressions.
### Type Promotion (Happens ONLY in expressions)

This happens when you do **math**:

```
+  -  *  /  %
```

When Java sees math, it upgrades (promotes) small integer types:

### RULE:

```
byte
short       →   all become int before doing math
char
```

### Example:

```
byte x = 5;
byte y = 10;
int z = x + y; // x and y become int, so result = int
```

This is **NOT the same as implicit typecasting**.  
This happens **only because of an operator (like +)**


Example:

```
byte a = 5;
byte b = 10;

byte c = (byte)(a + b);  // a+b becomes int automatically
```

This confuses many beginners, but remember:

> Any arithmetic on `byte`, `short`, or `char` → becomes `int`.

---

# **5️⃣ Real-World Use Examples**

### ✔ Converting user input

```
String s = "123";
int number = Integer.parseInt(s);
```

### ✔ Precise division

```
int a = 5, b = 2;
double result = (double) a / b;  // 2.5 instead of 2
```

### ✔ Memory optimization in large loops

Sometimes you cast large values to smaller ones to save RAM.

---

# **Summary Table**

| Type | Direction | Automatic? | Risk |
| --- | --- | --- | --- |
| Widening | small → big | Yes | No data loss |
| Narrowing | big → small | No | Data loss possible |
| Upcasting | Child → Parent | Yes | Safe |
| Downcasting | Parent → Child | No | Can throw error |
When both values are integers, Java defaults to integer division. It’s a design choice for efficiency and clarity—no hidden decimals. If you want decimals, you need to explicitly cast at least one value to a float or double.


When you perform an operation between two values of the same type, Java expects the result to remain that same type. Since both `3` and `2` are literal integers (`int`), Java performs the math and then "chops off" everything after the decimal point to return an integer.

### The Logic Behind It

In many programming languages, including Java, division doesn't automatically "upgrade" to a decimal just because there's a remainder.

- **Standard Math:** $3 \div 2 = 1.5$
    
- **Java Integer Math:** $3 \div 2 = 1$ (The $.5$ is truncated, not rounded).

There are two main reasons why Java (and many other languages like C++ and C#) behaves this way: **predictability** and **performance**.

### 1. Type Safety and Memory

In Java, every variable has a fixed "bucket" size in memory.

- An `int` (integer) is 32 bits and cannot store a decimal point.
    
- A `double` (decimal) is 64 bits and uses a completely different internal format (IEEE 754) to store numbers.
    

If Java automatically turned an `int` into a `double` during division, it would be making a massive assumption. It would have to allocate more memory and change the data format without you explicitly asking it to. To keep things **predictable**, Java sticks to the rule: _If you start with integers, you stay with integers._

### 2. Efficiency (Performance)

At the hardware level, your CPU handles integer math and floating-point (decimal) math using different units:

- **ALU (Arithmetic Logic Unit):** Handles integers. It is incredibly fast and simple.
    
- **FPU (Floating Point Unit):** Handles decimals. It is more complex and historically slower than integer math.
    

By defaulting to integer division, Java ensures the operation is as fast as possible. If it converted everything to decimals "just in case," it would add unnecessary overhead to programs that don't need that level of precision.

### 3. Truncation vs. Rounding

Java **truncates** (chops off) rather than rounds because it’s computationally cheaper. To round a number, the computer would have to:

1. Calculate the remainder.
    
2. Check if that remainder is $\ge 0.5$.
    
3. Increment the result if necessary.
    

Truncation requires zero extra steps—it simply discards the bits that don't fit into the integer format.

---

# **Type promotion**


**Type promotion** means Java automatically **converts smaller data types into larger data types** when performing expressions or operations, so that the operation is safe and consistent.

It is part of Java’s **Numeric Promotion Rules**.

# 🔥 Two Types of Type Promotion

# 1️⃣ **Unary Numeric Promotion**

Happens when a single operand is used with unary operators (`+`, `-`, `~`).

Example:

```
byte a = 5;
int b = +a;   // promoted to int
```

Even one `byte` becomes `int`.

---

# 2️⃣ **Binary Numeric Promotion**

Happens when **two operands** are used in arithmetic:

Operators: `+`, `-`, `*`, `/`, `%`

When Java sees an arithmetic expression between different types, it follows strict rules:

---

# ✔️ Official Type Promotion Order

From smallest → biggest:

```
byte → short → char → int → long → float → double
```

Java promotes values step-by-step until both sides match.

---

# ⭐ RULE 1:

## **Any operand smaller than int (byte, short, char) → promoted to int**

Example:

```
byte a = 10;
byte b = 20;
var c = a + b; // c becomes int
```

Even though both are `byte`, Java promotes them to `int`.

---

# ⭐ RULE 2:

## **If either operand is long → result becomes long**

```
int a = 5;
long b = 10L;

var c = a + b;  // c is long
```

---

# ⭐ RULE 3:

## **If either operand is float → result becomes float**

```
float x = 1.2f;
int y = 3;

var z = x + y;  // z is float
```

---

# ⭐ RULE 4:

## **If either operand is double → result becomes double**

```
double d = 3.14;
float f = 2.5f;

var r = d + f;  // r is double
```

---

# 🎯 WHY Does Java Promote Types?

## 1) CPU Efficiency

Most CPUs work faster with 32-bit integers, so Java promotes smaller types to `int`.

## 2) Prevent Silent Overflow

If Java kept everything as `byte`, values would wrap silently.

## 3) Consistent, Simple Rule

Instead of dozens of confusing possibilities, Java uses **one promotion path**.

---

# 📌 IMPORTANT CONSEQUENCE

Because byte/short/char → int, this fails:

```
byte a = 5;
byte b = 10;

byte c = a + b; // ERROR
```

Fix:

```
byte c = (byte)(a + b);
```

---

# ✔️ EASY SUMMARY TABLE

| Expression Contains | Promoted To |
| --- | --- |
| byte/short/char | int |
| int + long | long |
| int/long + float | float |
| anything + double | double |

---

# ✔️ A Real-World Example

```
byte a = 50;
byte b = 60;

float c = a * b + 2.5;
```

Steps:

1. a → int
2. b → int
3. a \* b → int (3000)
4. 3000 → float (because adding 2.5)
5. result → float


# String concatenation
## ❗ String concatenation is a **different rule**

It does NOT follow the integer promotion rules.

String concatenation happens when Java sees:

```
something + "string"
```

When you join anything with a **String**, Java converts the other value into a string.

### Example:

```
String s = "Hello";
int a = 10;

String result = s + a;  
// result = "Hello10"
```

Here:

- No type promotion
- No typecasting
- No numeric math
- It simply converts `a` to a **string** and joins

### ⚡ Even this:

```
System.out.println("" + 1 + 2);
```

Result:

```
12
```

Not `3`  
Because the first `""` starts string mode.


---

`char` ALWAYS gets type-promoted to `int` in arithmetic

Let’s break down **`9 + ' '`** in the cleanest possible way.


Whenever Java sees **any arithmetic operator** (`+`, `-`, `*`, `/`, `%`):

```
byte
short        →  ALL become int
char
```

So in your example:

```
9 + ' '
```
- `9` is an **int**
- `' '` space is a **char**

### Java promotes `' '` to its **ASCII value** (integer).

ASCII value of `' '` (space) = **32**

So the expression becomes:

```
9 + 32 = 41

```


# ✅ **2. Why does Java promote char → int?**

Because **chars are stored as numbers internally** (Unicode values).  
So Java *must* convert them to integers before doing math.

That’s part of **type promotion**, not typecasting.

---

# ☑️ Final Answer in Simple Words:

### ✔️ **Yes**, `9 + ' '` gets type promoted

### ✔️ `' '` becomes its ASCII code (32)

### ✔️ Result = `41`

---

# 🔥 Quick Similar Examples

### Example 1:

```
'a' + 1
```

ASCII of `'a'` = 97  
So:

```
97 + 1 = 98
```

### Example 2:

```
'0' + 5
```

ASCII of `'0'` = 48  
So:

```
48 + 5 = 53
```

### Example 3:

```
char c = 'A';
int x = c; // promotion
```

ASCII of `'A'` = 65  
So:

```
x = 65
```

---

# ⭐ FINAL CHEAT SENTENCE (MEMORIZE THIS)

```
Whenever you do math with char, Java converts it to int using its ASCII/Unicode value.
```


byte a = 40; byte b = 50; // byte c = a + b; // Will the line above compile? If not, why?

### Why does it fail?

Even though 40 + 50 = 90 (which fits perfectly inside a `byte`), Java follows a strict rule called **Binary Numeric Promotion**.

Whenever you use an arithmetic operator like `+`, Java automatically promotes any `byte`, `short`, or `char` to an `int` **before** doing the math.

1. Java sees `a + b`.
    
2. It converts `a` (40) to an `int`.
    
3. It converts `b` (50) to an `int`.
    
4. It adds them together to get an `int` result of `90`.
    

Now, look at your assignment:

`byte c = (int) 90;`

Java refuses to put a **32-bit `int`** into an **8-bit `byte`** bucket automatically, because it views this as a "narrowing conversion" that _could_ lead to data loss.

---

### How to fix it

You have to tell Java, "I know what I'm doing, please force this back into a byte" by using an **explicit cast**:

Java

```
byte c = (byte) (a + b); // This works!
```

### Why does Java do this? (The Practical Reason)

Imagine if Java _didn't_ do this. What if `a` was 100 and `b` was 50?

- $100 + 50 = 150$
    
- A `byte` can only hold up to **127**.
    
- The result would "wrap around" to **-106** due to overflow.
    

By forcing everything to `int` during math, Java prevents these "silent errors" from happening in the middle of your calculations. It forces **you** to acknowledge that the result might not fit by making you type `(byte)`.

---

### The One Exception: Literals

Interestingly, if you use direct numbers (literals), the compiler is smart enough to check if they fit:

Java

```
byte c = 40 + 50; // This WORKS!
```

Because `40` and `50` are constants, the compiler does the math itself, sees that `90` fits in a byte, and allows it. But with variables (`a + b`), the compiler plays it safe because the values of `a` and `b` could change at runtime

---
