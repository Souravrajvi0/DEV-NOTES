
# ✅ 1. Why do we need input in Java?

When your program runs, it often needs some data **from the user** — for example:

- name
    
- age
    
- numbers for calculations
    
- menu options
    

Java does **not** have a built-in direct input function like Python’s `input()`.  
So Java uses **classes** from libraries to read input.

That’s where **Scanner** comes in.

---

# ✅ 2. What is the Scanner class?

Scanner is a **utility class in `java.util` package**.

It reads input from sources like:

- keyboard (System.in)
    
- files
    
- strings
    

This is why, before using it, we must **import** it
# ✅ 3. Correct Order of Using Scanner (Super Important)

### Step 1: Import

```
import java.util.Scanner;
```

### Step 2: Create Scanner object

```
Scanner sc = new Scanner(System.in);
```

### Step 3: Take inputs using scanner methods

Examples:

```
int age = sc.nextInt();          // read integer
double price = sc.nextDouble();  // read decimal
String name = sc.nextLine();     // read full line
String word = sc.next();         // read single word
```

### Step 4: Close scanner (optional for now)

```
sc.close();
```

---

# ✅ 4. Full Example (Minimal & Correct)

```
import java.util.Scanner;

public class InputExample {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = sc.nextLine();

        System.out.print("Enter your age: ");
        int age = sc.nextInt();

        System.out.print("Enter your height: ");
        double height = sc.nextDouble();

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Height: " + height);

        sc.close();
    }
}
```

---

# ✅ 5. Scanner Input Methods (All You Need)

### 🔹 For numbers

| Data Type | Method |
| --- | --- |
| int | `nextInt()` |
| long | `nextLong()` |
| float | `nextFloat()` |
| double | `nextDouble()` |

### 🔹 For Strings

| What you want | Method | Meaning |
| --- | --- | --- |
| One word | `next()` | Stops at space |
| Full sentence | `nextLine()` | Reads till newline |
# ❗ Very Important Concept: nextLine() Issue

If you mix `nextInt()` and `nextLine()`, you may see this problem:

```
int age = sc.nextInt();
String name = sc.nextLine();   // this SKIPS input, why?
```

**Reason:**  
`nextInt()` leaves a `\n` (newline) in the input buffer.  
`nextLine()` immediately reads that leftover `\n`.

### Fix:

After any numeric input, add:

```
sc.nextLine();
```

---

# 🔥 Example with fix

```
System.out.print("Enter age: ");
int age = sc.nextInt();
sc.nextLine();    // clear leftover newline

System.out.print("Enter full name: ");
String name = sc.nextLine();
```

---

# ✅ 6. Most Common Errors Beginners Get

### ❌ `InputMismatchException`

You typed text when Java expected a number.

### ❌ `nextLine()` getting skipped

Because you used `nextInt()` or `nextDouble()` just before it.

### ❌ Forgot to import Scanner

Always import:

```
import java.util.Scanner;
```

---

# 🔥 7. Final Summary (You should memorize this order)

```
1. import java.util.Scanner;
2. Scanner sc = new Scanner(System.in);
3. Use sc.nextInt(), sc.nextLine(), etc.
4. If mixing nextInt and nextLine → do sc.nextLine() to clear buffer
5. sc.close();
```



---
# **OPERATORS** 
# ✅ 1. What is an operator?

An operator is a **symbol** that performs an operation on one or more values.

Example:

```
int a = 10 + 20;
```

`+` is the operator, `10` and `20` are operands.

---

# ✅ 2. Types of Operators in Java

Java operators are:

1. **Arithmetic Operators**
2. **Unary Operators**
3. **Assignment Operators**
4. **Relational (Comparison) Operators**
5. **Logical Operators**
6. **Bitwise Operators**
7. **Ternary Operator**
8. **Increment / Decrement Operators** (part of unary, but important)
9. **Instanceof Operator**

Let’s go one-by-one.

---

# 🔵 3. Arithmetic Operators

Used for mathematical operations.

| Operator | Meaning |
| --- | --- |
| + | Addition |
| \- | Subtraction |
| \* | Multiplication |
| / | Division |
| % | Modulo (remainder) |

Example:

```
int a = 10;
int b = 3;
System.out.println(a + b); // 13
System.out.println(a - b); // 7
System.out.println(a * b); // 30
System.out.println(a / b); // 3
System.out.println(a % b); // 1
```

---

# 🔵 4. Unary Operators

Operators that work on **only one operand**.

| Operator | Meaning |
| --- | --- |
| + | Unary plus |
| \- | Unary minus |
| ! | Logical NOT |
| ~ | Bitwise NOT |

Example:

```
int a = 5;
System.out.println(-a); // -5
System.out.println(+a); // 5
System.out.println(!true); // false
```

---

# 🔵 5. Increment / Decrement Operators (++ and --)

| Operator | Meaning |
| --- | --- |
| ++a | pre-increment |
| a++ | post-increment |
| \--a | pre-decrement |
| a-- | post-decrement |

Example:

```
int x = 5;

System.out.println(++x); // 6   (increment then print)
System.out.println(x++); // 6   (print then increment)
System.out.println(x);   // 7
```

---

# 🔵 6. Assignment Operators

Used to assign values.
Also can you like see values +,- all these symbols come first not after

| Operator | Meaning |
| --- | --- |
| \= | assign |
| += | a += b → a = a + b |
| \-= | a = a - b |
| \*= | a = a \* b |
| /= | a = a / b |
| %= | a = a % b |

Example:

```
int a = 10;
a += 5; // 15
a *= 2; // 30
```

---

# 🔵 7. Relational (Comparison) Operators

Always return **true/false**.
Hamesha true/false hi return karenge remember bhai

| Operator | Meaning |
| --- | --- |
| \== | equal |
| != | not equal |
| \> | greater than |
| < | less than |
| \>= | greater or equal |
| <= | less or equal |

Example:

```
int a = 10;
int b = 20;
System.out.println(a == b); // false
System.out.println(a < b);  // true
```

---

# 🔵 8. Logical Operators

Work on boolean values.
Used in expression or decision making 

| Operator | Meaning |
| --- | --- |
| && | logical AND |
| \|\| | logical OR |
| ! | logical NOT |

Example:

```
boolean x = true;
boolean y = false;

System.out.println(x && y); // false
System.out.println(x || y); // true
System.out.println(!x);     // false
```

---

# 🔵 9. Bitwise Operators (Used less in beginner stage)

Operate on bits (0/1).

| Operator | Meaning |
| --- | --- |
| & | bitwise AND |
| \| | bitwise OR |
| ^ | bitwise XOR |
| ~ | bitwise NOT |
| << | left shift |
| \>> | right shift |
| \>>> | unsigned right shift |

Example:

```
int a = 5;   // 0101
int b = 3;   // 0011
System.out.println(a & b); // 1  (0001)
```

---

# 🔵 10. Ternary Operator

Short form of if-else.

```
condition ? value_if_true : value_if_false
```

Example:

```
int age = 20;
String result = (age >= 18) ? "Adult" : "Minor";
```

---

# 🔵 11. Instanceof Operator

Used to check if an object belongs to a class.

```
String s = "Hello";
System.out.println(s instanceof String); // true
```

---

# 🔥 12. Operator Precedence (which runs first?)

Higher precedence runs first:

```
1. ++  --  (increment/decrement)
2. *  /  %
3. +  -
4. <  >  <=  >=
5. ==  !=
6. &&
7. ||
8. =  +=  -=  ...
```

---

# ❗ Common Mistakes Beginners Make

1. `==` vs `=`
	- `==` → comparison
	- `=` → assignment
2. Using `++` inside print statements without understanding pre/post.
3. Forgetting operator precedence:
```
int result = 10 + 20 * 3; // 70, not 90
```
4. Thinking `/` gives float always:
```
int a = 5/2; // result = 2 not 2.5
```

You need:

```
double a = 5.0/2;
```



---
# SOME POINTS 
## 1️⃣ Core Rule (Memorize This)

> **In Java, the operation happens after type promotion.  
> The result type depends on the highest-precision operand.**

Type priority (low → high):

```
byte → short → int → long → float → double
```

---

## 2️⃣ Division Operator `/`

### 🔹 Case 1: int / int → int (fraction LOST)

```
System.out.println(3 / 2);   // 1
```

**Why?**  
Both operands are `int` → integer division → decimal part is **discarded**, not rounded.

---

### 🔹 Case 2: int / double → double

```
System.out.println(3 / 2.0);   // 1.5
System.out.println(3 / 1.0);   // 3.0
```

**Why?**

- `3` (int) → promoted to `double`
- calculation happens in `double`

Equivalent to:

```
3.0 / 2.0
```

---

### 🔹 Case 3: double / int → double

```
System.out.println(3.0 / 2);   // 1.5
```

Same reason: higher type wins.

---

### 🔹 Case 4: int / float → float

```
System.out.println(3 / 2f);    // 1.5
```

---

### 🔹 Case 5: casting AFTER division (common mistake)

```
System.out.println((double)(3 / 2)); // 1.0 ❌
```

**Why wrong?**

- `3 / 2` happens first → `1`
- then cast to double → `1.0`

✅ Correct:

```
System.out.println((double)3 / 2); // 1.5
```

---

## 3️⃣ Modulus Operator `%`

### 🔹 What `%` really means

```
a % b  → remainder after division
```

But the **rule stays the same**: type promotion applies.

---

### 🔹 Case 1: int % int → int

```
System.out.println(3 % 2);  // 1
```

---

### 🔹 Case 2: int % double → double

```
System.out.println(3 % 2.0); // 1.0
```

**Why?**

- `3` → promoted to `double`
- result is `double`

---

### 🔹 Case 3: double % int → double

```
System.out.println(3.5 % 2); // 1.5
```

Calculation:

```
3.5 = 2 * 1 + 1.5
```

---

### 🔹 Case 4: double % double

```
System.out.println(5.5 % 2.0); // 1.5
```

---

## 4️⃣ Very Important Edge Cases

### ⚠️ Division by zero

```
System.out.println(5 / 0);   // ArithmeticException ❌
```

But:

```
System.out.println(5.0 / 0); // Infinity
System.out.println(-5.0 / 0); // -Infinity
System.out.println(0.0 / 0); // NaN
```

**Why?**

- Floating-point follows **IEEE 754**
- Integer division does NOT allow zero

---

### ⚠️ Modulus with zero

```
System.out.println(5 % 0);   // ArithmeticException ❌
System.out.println(5.0 % 0); // NaN
```

---

## 5️⃣ Sign Rule for Modulus (VERY IMPORTANT)

> **Result sign = sign of the dividend (left operand)**

```
System.out.println(5 % 3);    // 2
System.out.println(-5 % 3);   // -2
System.out.println(5 % -3);   // 2
System.out.println(-5 % -3);  // -2
```

This is **language-defined**, not math convention.

---

## 6️⃣ Mental Model (Use This Always)

### Division

```
type of result = max(type(left), type(right))
```

### Modulus

```
a % b = a - (a / b) * b
```

(where `/` follows Java rules)

---

## 7️⃣ Interview-Grade Tricky Examples

```
System.out.println(10 / 3 * 3);      // 9
System.out.println(10 / (3 * 3));    // 1
System.out.println(10.0 / 3 * 3);    // 10.0
System.out.println(1 / 2 * 10);      // 0
```

Why last one?

```
1 / 2 → 0
0 * 10 → 0
```

---

## 8️⃣ One-Line Rules You Should Remember

- **Integer division truncates**
- **One floating operand → floating result**
- **Casting must happen BEFORE division**
- **`%` works with floating types**
- **Sign of `%` follows left operand**
- **`/ 0` crashes only for integers**



---

# ✅ 1. What is a conditional?

A conditional lets your program **decide** what to do based on a condition (true/false).

Example idea:  
If age ≥ 18 → allow voting else → deny.

Java conditionals rely on **boolean expressions**.

---

# 🔵 2. The `if` Statement

This is the simplest conditional.

```
if (condition) {
    // runs only when condition is true
}
```

Example:

```
int age = 20;

if (age >= 18) {
    System.out.println("Adult");
}
```

If `condition = true`, the block runs.  
If `condition = false`, the block is skipped.

---

# 🔵 3. The `if-else` Statement

Use when you need either **A** or **B**.

```
if (condition) {
    // true block
} else {
    // false block
}
```

Example:

```
int age = 16;

if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Minor");
}
```

---

# 🔵 4. The `else if` Chain

Use when you have **multiple conditions**.

```
if (condition1) {
    ...
} else if (condition2) {
    ...
} else if (condition3) {
    ...
} else {
    // final option
}
```

Example:

```
int marks = 85;

if (marks >= 90) {
    System.out.println("A Grade");
} else if (marks >= 80) {
    System.out.println("B Grade");
} else if (marks >= 70) {
    System.out.println("C Grade");
} else {
    System.out.println("Fail");
}
```

**Order matters** — first true condition wins.

---

# 🔵 5. Important Rules for `if` / `else`

### Rule 1: `else` always pairs with the nearest unmatched `if`.

No matter the indentation.

```
if (a > 0)
    if (b > 0)
        System.out.println("Inner");
    else 
        System.out.println("Pairs with b>0 if");
```

---

### Rule 2: Condition must be boolean (Java is strict)

❌ Not allowed:

```
if (5) { } 
if (x)  { }
```

✔ Must be:

```
if (true) { }
if (x > 5) { }
```

---

# 🔵 6. The `switch` Statement

Use when you have a variable that can take a few fixed values (int, String, char, enum).

```
switch (value) {
    case option1:
        // code
        break;

    case option2:
        // code
        break;

    default:
        // runs if no case matches
}
```

Example:

```
int day = 3;

switch (day) {
    case 1: System.out.println("Mon"); break;
    case 2: System.out.println("Tue"); break;
    case 3: System.out.println("Wed"); break;
    default: System.out.println("Unknown");
}
```

---

# 🔵 7. The `break` Keyword in Switch

If you don't use `break`, Java **falls through** to the next case.

```
int n = 1;

switch (n) {
    case 1:
        System.out.println("One");
    case 2:
        System.out.println("Two");
}
```

if we don't add  break agee wale har case ka code execute ho jaega
Output:

```
One
Two
```

---

# 🔵 8. `switch` with Strings (Important)

Java supports:

```
String command = "start";

switch (command) {
    case "start": System.out.println("Started"); break;
    case "stop": System.out.println("Stopped"); break;
}
```

---

# 🔵 9. Enhanced `switch` (Java 14+)

Clean syntax:

```
String day = switch (3) {
    case 1 -> "Mon";
    case 2 -> "Tue";
    case 3 -> "Wed";
    default -> "Unknown";
};
```

Or without return:

```
switch (day) {
    case "Mon" -> System.out.println("Start");
    case "Fri" -> System.out.println("End");
}
```

---

# 🔵 10. Boolean Logic Inside Conditionals

Common patterns:

```
if (age >= 18 && age <= 60) { }   // AND
if (marks > 80 || grade.equals("A")) { }   // OR
if (!isOpen) { }                 // NOT
```

---

# 🔥 11. Common Mistakes Beginners Make

### ❌ Using assignment instead of comparison

```
if (x = 5)  // wrong, this assigns
if (x == 5) // correct, compares
```

### ❌ Conditions that are always true

```
if (x = 0) { }     // invalid
if (x == 0) { }    // correct
```

### ❌ Writing unreachable code

```
if (false) {
    // unreachable
}
```

---

# 🔥 12. Good Practices

✔ Use braces `{}` always  
✔ Use `else if` instead of multiple `if`s  
✔ Use `switch` when you have fixed known options  
✔ Keep conditions readable

# ✅ What changed in the new `switch`?
Before Java 14, `switch` was old-style:

- Required `break` to avoid fall-through
- Verbose
- Could NOT directly return a value
- Harder to read

Now, Java 14+ gives you a **new, cleaner, safer** `switch`.

---

# ✅ 1. Switch can **produce a value**

This is the biggest new feature.

### Example:

```
String day = switch (3) {
    case 1 -> "Mon";
    case 2 -> "Tue";
    case 3 -> "Wed";
    default -> "Unknown";
};
```

### What this means:

- `switch` is now an **expression** (not just a statement).
- It **returns** a value.
- Whatever value the matching case produces is **assigned to `day`**.

### Flow:

- Input: `3`
- Matches: `case 3`
- Produces → `"Wed"`
- So `day` becomes `"Wed"`.

No breaks, no fall-through, no curly braces needed.

---

# 🔥 Why `->` ?

The arrow means:

> “If this case matches, produce this value.”

It removes the old need for:

```
case 3:
    return "Wed";
    break;
```

---

# ✅ 2. Switch without returning (just running code)

You can still use switch just for executing statements:

```
switch (day) {
    case "Mon" -> System.out.println("Start");
    case "Fri" -> System.out.println("End");
}
```

### What this means:

- No `break` needed
- Cleaner and safer
- Each case is like “do this action”
- No accidental fall-through

Only the matching case runs.

---

# 🧠 Core difference to remember

| Old Switch | New Switch |
| --- | --- |
| Needs `break` | No break needed |
| Can’t return a value | Can directly return a value |
| Verbose | Clean and short |
| Fall-through bugs | No fall-through by default |

---

# TL;DR

### When you want a value:

Use `switch (...) { case X -> value; }`

### When you want to run code:

Use `switch (...) { case X -> statement; }`

---

# ✅ 1. What is a loop?

A loop repeats a block of code **multiple times** until a certain condition becomes false.

Example idea:  
Print numbers from 1 to 10 → loop is perfect for this.

Java has **3 main loops**:

1. `for`
2. `while`
3. `do-while`

And also:

4. **enhanced for loop** (for arrays & collections)
5. **break & continue**

Let's go step-by-step.

---

# 🔵 2. The `for` loop (Most commonly used)

### Syntax:

```
for (initialization; condition; update) {
    // body
}
```

### Example 1: Print 1 to 5

```
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

Breakdown:

- `int i = 1` → start
- `i <= 5` → continue until this is false
- `i++` → increment after each iteration

---

### Example 2: Print even numbers

```
for (int i = 2; i <= 10; i += 2) {
    System.out.println(i);
}
```

---

### Notes:

- Initialization runs **once**
- Condition checked **every iteration**
- Update runs **after body**

---

# 🔵 3. The `while` loop (Use when you don’t know how many times it will run)

### Syntax:

```
while (condition) {
    // body
}
```

### Example:

```
int i = 1;

while (i <= 5) {
    System.out.println(i);
    i++;
}
```

Best when:

- you wait for user input
- you wait for some event
- you don’t know loop count in advance

---

# 🔵 4. The `do-while` loop (Runs **at least once**)

### Syntax:

```
do {
    // body
} while (condition);
```

### Example:

```
int i = 1;

do {
    System.out.println(i);
    i++;
} while (i <= 5);
```

Key difference:

- `do-while` runs the body **first**, checks condition later.

Used for:

- menus
- user input
- run-first-then-check scenarios
# 🔵 5. Enhanced For Loop (for-each loop)
Used **only for arrays and collections**.  
You cannot manually control the index in this loop.

### Syntax:

```
for (dataType element : arrayOrCollection) {
    // use element
}
```

### Example:

```
int[] arr = {10, 20, 30};

for (int num : arr) {
    System.out.println(num);
}
```

Cleanest way to loop over arrays.

---

# 🔵 6. Nested Loops

A loop inside another loop.

### Example:

```
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        System.out.println(i + " " + j);
    }
}
```

Used for:

- patterns
- matrices
- 2D data
- complex loops

---

# 🔵 7. `break` and `continue`

### `break` → exit the loop immediately

```
for (int i = 1; i <= 10; i++) {
    if (i == 5) break;
    System.out.println(i);
}
```

Stops at 4.

---

### `continue` → skip the current iteration

```
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    System.out.println(i);
}
```

Skips printing 3.

---

# 🔥 8. Infinite Loops

### with for:

```
for(;;) {
    // infinite
}
```

### with while:

```
while (true) {
    // infinite
}
```

Be careful—your program will never stop unless you break manually.

---

# 🔥 9. Most Common Beginner Mistakes

### ❌ Forgetting to update your loop variable

```
while (i <= 5) {
    System.out.println(i);  // infinite loop if i++ missing
}
```

### ❌ Condition that never becomes false

```
while (i >= 0) {
    i++; // i is increasing, condition always true
}
```

### ❌ Misusing semicolon

```
while (i < 5);  // wrong ❌
{
    System.out.println(i);
}
```

That semicolon creates an **empty loop**.

### ❌ Off-by-one errors

Classic bug: running loop 1 extra time or 1 less.

---

# 🔥 10. When to use which loop?

| Loop | Best Use |
| --- | --- |
| **for** | known number of iterations |
| **while** | unknown number, condition-based |
| **do-while** | run at least once |
| **for-each** | arrays, lists (no index control) |

