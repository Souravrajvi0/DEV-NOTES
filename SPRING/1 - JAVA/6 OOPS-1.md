
# ⭐ 1. Why Do We Even Need to Learn Stack & Heap?

Because understanding **how Java stores variables, objects, arrays, and methods** solves 80% of confusion in:

- Arrays
- String vs StringBuilder
- Method calls
- Passing objects
- Reference behavior
- Garbage collection

---

# ⭐ 2. Stack Memory — The Basics

The **stack** is the memory used for:

### ✔ Local variables

### ✔ Method calls

### ✔ References (the variable holding the memory address)

### ✔ Function parameters

### ✔ Return addresses

Stack follows **LIFO (Last In, First Out)**.

Example:

```
void fun() {
    int x = 10; // local variable → stored in stack
}
```

Stack frame created when method starts → destroyed when method ends.

---

# ⭐ 3. Heap Memory — The Basics

The **heap** is used for storing:

### ✔ All Java objects

### ✔ Arrays

### ✔ Strings (SCP also inside heap)

### ✔ Objects created with new

### ✔ Objects referenced by variables in stack

Example:

```
Student s = new Student();
```
- `s` → stack
- Student object → heap

Heap memory is managed by the **Garbage Collector (GC)**.

---

# ⭐ 4. Combining Both: How Variables Are Actually Stored

Take this example:

```
int a = 10;
String s = "Hello";
int[] arr = new int[5];
StringBuilder sb = new StringBuilder("Hi");
```

Breakdown:

| Code | Stored in Stack | Stored in Heap |
| --- | --- | --- |
| `int a` | ✔ value 10 | ❌ |
| `String s` | ✔ reference | ✔ String object (in SCP) |
| `int[] arr` | ✔ reference | ✔ array object |
| `StringBuilder sb` | ✔ reference | ✔ SB object + internal char\[\] |

---

# ⭐ 5. Stack = Reference, Heap = Actual Object

This is THE most important line:

### **Stack stores the reference. Heap stores the object.**

Example:

```
String s = "Java";
```

Memory:

- Stack → `s`
- Heap → "Java"
- SCP → (literal stored here)

---

# ⭐ 6. String Literal vs new String() — Memory Difference

```
String s1 = "Hello";           // SCP
String s2 = new String("Hello"); // Heap
```
- s1 → stack reference to SCP object
- s2 → stack reference to heap object
- Two **different memory locations**

---

# ⭐ 7. Arrays → Always in Heap

Even if it stores primitives:

```
int[] arr = {10, 20, 30};
```
- arr → stack
- array object → heap
- elements → inside the heap object (not stack!)

---

# ⭐ 8. What Goes in Stack?

- local primitives (`int`, `double`, `char`)
- references (addresses of objects)
- method call information
- temporary variables

---

# ⭐ 9. What Goes in Heap?

- Objects created using `new`
- Arrays
- Strings
- StringBuilder/StringBuffer
- Collections (ArrayList, HashMap, etc.)

---

# ⭐ 10. What Happens When You Pass Objects to Methods?

Example:

```
void update(int[] a){
    a[0] = 99;
}

int[] arr = {1,2,3};
update(arr);
```
- arr (stack) → reference
- array (heap) → actual values
- reference is copied → both refer to same heap array
- so changes reflect outside method

This is why arrays/objects behave like **pass-by-reference** (but technically Java is pass-by-value-of-reference).

---

# ⭐ 11. Garbage Collection

GC removes heap objects that have **no references pointing to them**.

Example:

```
String s = new String("Hi");
s = null;
```

Now heap object "Hi" is eligible for GC.

But:

```
String a = "Hi";
String b = a;
a = null;
```

Still not GC, because `b` is pointing to "Hi".

---

# ⭐ 12. Stack vs Heap — Full Comparison

| Feature | Stack | Heap |
| --- | --- | --- |
| Size | Small | Large |
| Speed | Very fast | Slower |
| Stores | Local vars, references | Objects, arrays |
| Lifetime | Method-level | Until GC |
| Manages | JVM creates/destroys | Garbage Collector |
| Thread Safety | Each thread has its own stack | Heap shared across all threads |

---

# ⭐ 13. Visual Mental Model

Even without an image, imagine it like:

```
Stack                Heap
-----------------------------------------------
a -> 10            [Object 1: Student]
b -> ref123  --->  [Object 2: Array]
c -> ref891  --->  [Object 3: StringBuilder]
```

Stack holds **pointers**, heap holds the **real objects**.

---

# ⭐ 14. Final Summary (Everything in Correct Order)

### ✔ 1. Stack = local vars + references

### ✔ 2. Heap = objects + arrays + strings

### ✔ 3. String literal → SCP

### ✔ 4. `new String()` → always heap

### ✔ 5. Arrays are always heap

### ✔ 6. Passing objects → passes reference copy

### ✔ 7. Garbage Collector cleans unused heap objects

### ✔ 8. Stack is fast & temporary; heap is slow & persistent



---
# OOPS 


OOPS is a programming style where **everything is modelled as objects**, just like real-world things.

# **1. Functional Programming (FP): What is it?**

Functional Programming is a style of programming where:

### **❶ Functions are treated like first-class citizens**

You can:
- pass functions as arguments,
    
- return functions from other functions,
    
- store functions in variables.
    

### **❷ Focus is on _what to do_, not _how to do_ it**

It avoids detailed step-by-step logic and uses expressions.

### **❸ No changing state**

FP avoids variables that change.  
Instead of updating values, you create new ones.

This makes FP:

- predictable
    
- easy to reason about
    
- highly testable
    
- less buggy
    

### **Example mindset:**

In FP, you don't modify a list; you create a new list with changes.  
You don’t tell “how to loop”; you tell “what you want done”.

---

# **2. What is OOPS (Object-Oriented Programming System)?**

OOPS is a programming style where **everything is modelled as objects**, just like real-world things.

### Think of objects like:


- A **Car**
- A **Laptop**
- A **User**
- A **Bank Account**

Each has:

- **State** (data)
- **Behaviour** (actions/functions)

OOP focuses on:

- organizing code like real-world models
- combining data + functions together
- making large codebases easier to maintain

---

# **3\. Why OOPS was created? (The purpose)**

Before OOP, code was procedural (step-by-step), which caused issues in large systems:

### **Problem 1: Data was scattered**

Functions were separate…  
Data was separate…  
Anything could modify anything → chaos.

### **Problem 2: Reusability was low**

Same logic repeated everywhere.

### **Problem 3: Large programs became unmanageable**

More features → more confusion → more bugs.

### **Solution: OOPS**

OOPS groups data + behaviour into a single unit → an **object**.

This gives:  
✔ Encapsulation (data is protected)  
✔ Reusability (via classes, inheritance)  
✔ Structure (blueprints & objects)  
✔ Scalability (big apps easier to manage)

---

# **4\. OOPS in Java**

Java is **100% object-oriented** except for primitive types.

Java applies OOP rules strictly:

- Everything lives inside a **class**.
- You cannot write a function outside a class.
- Objects are created from classes using `new`.

OOP is the core philosophy of Java.

---

# **5\. OOP languages vs Non-OOP languages**

### **OOP Languages**

Support classes, objects, inheritance, polymorphism.

Examples:

- Java
- Python
- C++
- C#
- JavaScript (prototype-based)
- Ruby
- Swift
- Kotlin

### **Non-OOP languages**

Do NOT support objects or do so in a very limited way.

Examples:

- C (pure procedural)
- Assembly
- Early versions of PHP
- Go (has structs but no classes — partially OOP)
- SQL (not a programming language; declarative)

Some languages support **both styles** (multi-paradigm):

- Python
- JavaScript
- Kotlin
- Scala
- Rust

---

# **6\. What is a Class?**

A **class** is a *blueprint* or *template* for creating objects.

### Think of a class as:

A recipe → NOT the cake.  
A design → NOT the building.  
A blueprint → NOT the car.

It defines:

- What data the object will have (state)
- What actions the object can perform (behaviour)

### Example:

`Car` is a class  
but  
`myCar` and `yourCar` are objects (instances of Car).

---

# **7\. What is an Object?**

An object is a **real thing created from a class**.

If `class` is a blueprint,  
then `object` is the **actual product** built from it.

### Objects have:

- **State** → stores data inside variables
- **Behaviour** → performs actions using methods

---

# **8\. What does “state” and “behaviour” mean?**

### **State = the data stored inside the object**

Example:  
For a Car object:

- color = "Red"
- speed = 0
- fuelLevel = 80

These values make up the **current condition of the object**. 
just variables man

### **Behaviour = actions the object can do**

Example behaviors for Car:

- start()
- accelerate()
- brake()
- refuel()

the methods man

State = nouns  
Behaviour = verbs

```java
class car {
 private string name = audi ;
 // name is a field with state as audi 
 
 
 //method is breaking
 public void breaking(){
 }
 
}

```

---

# **9\. How to create a class in Java**

### Step 1: Define the class

```
class Car {
    // state (variables)
    String color;
    int speed;

    // behaviour (methods)
    void start() {
        System.out.println("Car started");
    }

    void stop() {
        System.out.println("Car stopped");
    }
}
```

### Step 2: Create an object of the class

```
Car myCar = new Car();
classname objectname = new classname();
```

### Step 3: Access or modify state and behaviour

```
myCar.color = "Blue";
myCar.speed = 60;

myCar.start();
```

---

# **Putting It All Together — One Clean Summary**

| Concept | Meaning |
| --- | --- |
| Functional Programming | No changing state; functions > objects |
| OOPS | Organizing code as objects with state + behaviour |
| Why OOPS | Makes large apps manageable, reusable, structured |
| Class | Blueprint / template |
| Object | Real instance created from class |
| State | Data inside object |
| Behaviour | Actions object can perform |
| Java and OOP | Java is fully OOP; everything lives inside classes |


---
# CLASS AND PACKAGE

In Java, if two classes are in the **same package**, they can directly access each other **without importing**.

### ✔ Same package → No need to write `import`

Java will automatically know where the class is.

But…  
What you *can access* depends on the **access modifier**.

Let's build this step-by-step.

---

# 🔹 **1\. Two classes inside the same package**

Example folder structure:

```
src/
 └── mypackage/
       ├── Car.java
       └── Main.java
```

So both `Car.java` and `Main.java` are in **mypackage**.

---

# 🔹 **2\. Class 1 – Car**

```
package mypackage;

public class Car {
    String color = "Red";   // default access
    public int speed = 100; // public access

    public void drive() {
        System.out.println("Car is driving");
    }
}
```

---

# 🔹 **3\. Class 2 – Main**

```
package mypackage;

public class Main {
    public static void main(String[] args) {

        Car c = new Car();  // using class from SAME package

        System.out.println(c.color);
        System.out.println(c.speed);
        c.drive();
    }
}
```

---

# 🚀 **This works without importing because:**

- Both files have `package mypackage;`
- Both are compiled together
- Java searches inside same package by default

---

# 🔥 **4\. What if you want to use a class from another file in the same package?**

Just **create an object**.  
That's it.

### Example:

```
Car c = new Car();
```

No import required.

---

# 🔑 **5\. Access Modifiers Matter**

If classes are in the same package:

| Modifier | Accessible in SAME package? |
| --- | --- |
| public | ✔ Yes |
| protected | ✔ Yes |
| default (no modifier) | ✔ Yes |
| private | ❌ No |

So if you write:

```
String color; // default access
```

Other classes in the same package can access it.

But:

```
private String engineNumber;
```

This is only accessible **inside Car itself**.

---

# 🧠 **6\. What if I have multiple classes inside the SAME file?**

This is also allowed BUT:

- Only *one class* can be `public`
- Filename must match the public class

Example:

```
class Helper {      
    void help() {
        System.out.println("Helping...");
    }
}

public class Main {
    public static void main(String[] args) {
        Helper h = new Helper();   // works
        h.help();
    }
}
```

Everything works because both classes are in the same file.

---

# 📝 **7\. Summary (Super Simple)**

### ✔ Same package → No import needed

### ✔ Just create an object

### ✔ Access depends on modifier

### ✔ Can access public, protected, default


# CLASS AND **MAIN**

- Every file **usually contains one class**, but it’s *not required* to have the `main()` method.
- **Only one class needs `main()`** — the entry point where the program starts.
- All other classes are **helper classes** → they exist to support logic, not to run the program.

Let’s break it down properly.



# 🔹 **1\. A Java project = many classes, but only 1 class needs `main()`**

Example:

```
mypackage/
    Main.java
    Car.java
    User.java
    Calculator.java
```

Here:

- `Main.java` → contains `public static void main(String[] args)`
- `Car.java` → does NOT need main
- `User.java` → does NOT need main
- `Calculator.java` → does NOT need main

The main class runs the project.  
Other classes contain logic.

---

# 🔹 **2\. Why does only one class need `main()`?**

Because the JVM asks:

> “Where should I start running your program?”

It looks for **exactly one** entry point — the `main()` method.

But the rest of the classes are like:

- tools
- models
- components
- utilities

They are *used inside the main class*, but don’t run by themselves.

---

# 🔹 **3\. What is the structure of a typical Java application?**

### ✔ One file = One class

(but can have more than one class inside same file — rare and not recommended)

### ✔ Only one class = Entry point (main)

Usually named:

- `Main.java`, or
- `App.java`, or
- `Application.java`

### ✔ Other classes = Normal classes (no main)

---

# 🔹 **4\. What’s inside these “normal classes”?**

Normal classes (non-main classes) contain:

### **➤ State (variables)**

Example:

```
String color;
int speed;
```

### **➤ Behaviour (methods)**

Example:

```
void drive() { }
void stop() { }
```

They don’t need a main method because:

- They don’t start the program
- They provide only functionality

---

# 🔹 **5\. Deep clarity with Example**

### 📌 File 1 — `Main.java`

```
package mypackage;

public class Main {
    public static void main(String[] args) {
        Car c = new Car("Red", 120);
        c.drive();
    }
}
```

### 📌 File 2 — `Car.java`

```
package mypackage;

public class Car {
    String color;
    int speed;

    Car(String color, int speed) {
        this.color = color;
        this.speed = speed;
    }

    void drive() {
        System.out.println(color + " car driving at " + speed + " km/h");
    }
}
```

Notice:

- `Main.java` has main
- `Car.java` does NOT have main
- Both are in same package → can use each other without import

---

# 🔹 **6\. Why don’t other classes need main()?**

Because the purpose of main() is:

👉 "Start the program."

Normal classes:

- are “blueprints”
- are used by main class
- should NOT start the program

If every class had main, it would be like giving 100 drivers the steering wheel at the same time.

---

# 🔹 **7\. Can you run a class without main()?**

Yes — but not directly.

You can:

- **instantiate it**
- **call its methods**

But JVM won’t execute that class directly because `main` doesn’t exist.

---

# 🔹 **8\. Summary (Super Clear)**

### **❌ Not every file needs main()**

### **✔ Only one entry point (one main) per application**

### **✔ Other files contain normal classes**

### **✔ Same package = easy access without import**

### **✔ Each file usually contains 1 class, but not mandatory**

### **✔ Main class controls the whole program**


---

# HOW IMPORT WORKS

1️⃣ How `import` actually works  
2️⃣ How Java packages + folder structure work  
3️⃣ Access modifiers deeply  
4️⃣ How JVM finds and loads classes (class loader)

Let’s go step by step.

# ⭐ **1\. How `import` Actually Works**

### ❗ Myth:

`import` copies code from another file.

### ✔ Truth:

`import` just tells Java **where to find the class**.

Nothing more.

---

## 🔍 Example

Folder structure:

```
src/
  com/example/
      Car.java
  main/
      App.java
```

### Car.java

```
package com.example;

public class Car {
    public void drive() {
        System.out.println("Car driving");
    }
}
```

### App.java

```
package main;

import com.example.Car;   // <-- THIS is import

public class App {
    public static void main(String[] args) {
        Car c = new Car();
        c.drive();
    }
}
```

### What the import does:

It simply says:

> "JVM, if you need class Car, look inside **com.example** package."

That’s it.

### ✔ It does NOT:

- copy Car code
- include Car in App
- make Car part of App

---

## 🧠 Important — When do we need import?

### ✔ When class is **in a different package**

### ❌ When class is in the **same package** (no import needed)

---

# ⭐ **2\. How Java Packages + Folder Structure Works**

Packages = folders.

Think of a package like an **address** for a class.

### Example

Package:

```
package com.example.car;
```

Corresponding folders:

```
src/com/example/car/
```

Inside this folder → your `.java` file must be present.

### ✔ Rule: Folder structure **must match** package name.

That’s why Java is strict.

---

## Why packages exist?

### 1\. To group related classes

Just like arranging files in folders.

### 2\. To avoid name conflicts

Two classes can have the same name **if** they're in different packages.

```
com.company.ui.Button
com.company.engine.Button
```

No conflict.

### 3\. To control access

Protected and default access depend on packages.

---

# ⭐ **3\. Access Modifiers (Deep Explanation)**

Access modifiers decide **where** a variable/method/class can be accessed.

---

# ✔ 3.1 `public`

Accessible **everywhere**.

Across:

- same class
- same package
- different package
- different project (if imported)

Example:

```
public void drive() { }
```

---

# ✔ 3.2 `private`

Accessible **ONLY inside the same class**.

Not even same package can access.

Example:

```
private int engineNumber;
```

Only Car class can touch this.

---

# ✔ 3.3 `protected`

Accessible in:

- same package ✔
- subclasses in different packages ✔
- unrelated classes in other packages ❌

---

# ✔ 3.4 Default (no keyword)

Accessible:

- inside same package ✔
- outside package ❌

Example:

```
String color;  // default access
```

---

## Quick comparison:

| Modifier | Same Class | Same Package | Subclass (other pkg) | Different pkg |
| --- | --- | --- | --- | --- |
| public | ✔ | ✔ | ✔ | ✔ |
| protected | ✔ | ✔ | ✔ | ❌ |
| default | ✔ | ✔ | ❌ | ❌ |
| private | ✔ | ❌ | ❌ | ❌ |

This table will save your life.

---

# ⭐ **4\. How JVM finds and loads classes (Class Loader)**

This part is where programmers get confused, but I’ll explain it simply.

## JVM uses **3 class loaders**:

### ✔ 1. Bootstrap (loads core Java)

Loads fundamental classes like:

- `java.lang.*`
- `java.util.*`
- `java.io.*`

### ✔ 2. Extension Class Loader

Loads classes from Java extensions (rare now).

### ✔ 3. Application Class Loader

Loads:

- your classes
- your project packages
- anything in classpath

This is where your code lives.

---

# 🔥 How JVM loads your classes step-by-step

Let’s say your code uses:

```
Car c = new Car();
```

### Step 1: JVM checks current package

Is Car in same folder / same package?

If yes → load it.

### Step 2: If not found, check imported packages

Example:

```
import com.example.Car;
```

JVM goes to that folder and loads Car.class.

### Step 3: If still not found

Check other libraries in classpath.

### Step 4: If still not found

Throw error:

```
ClassNotFoundException
```

---

# ✔ What is Classpath?

Classpath = a list of places JVM should search for classes.

Like:

```
src/
bin/
lib/somejar.jar
```

JVM uses this path list to find `.class` files.

---

# ⭐ FINAL SUMMARY (Memory Booster)

### ✔ import

Tells Java **from which package to load the class**.

### ✔ Package

A folder that groups classes and prevents name conflicts.

### ✔ Access modifiers

Control who can access what.

### ✔ JVM class loading

JVM searches:

1. same package
2. imported packages
3. classpath
4. otherwise error



---
# **Constructors** 

A **constructor** is a **special method** inside a class whose ONLY job is:

> **To create (construct) an object and set its initial state.**

Think of it like:

- When a baby is born → doctor sets initial things (weight, name, etc.)
- When an object is born → constructor sets initial values.

It runs **automatically** when you write:

```
Car c = new Car();
```

You don’t call constructors manually.  
JVM calls it for you.

---

# ⭐ 2. Why do constructors exist?

Before constructors, programmers had to:

- first create an object
- then manually initialize all values

Example without constructor (if Java didn’t have them):

```
Car c = new Car();
c.color = "Blue";
c.speed = 0;
c.model = "Honda";
```

This is 🔥 **error-prone**, repetitive, and messy.

What if a programmer forgot to set something?  
Object stays **incomplete** → leads to bugs.

### ✔ Constructor solves this EXACT problem:

A constructor guarantees that **every object starts in a valid state**.

---

# ⭐ 3. When is a constructor invoked?

A constructor is invoked **when an object is created using `new`**.

Example:

```
Car c = new Car();  // constructor called HERE
```

JVM flow:

1. Memory is allocated
2. Default values assigned (0, null, false…)
3. **Constructor runs** and overwrites them
4. Object becomes fully ready

You can think of constructor as the “object setup function.”

---

# ⭐ 4. Rules of Constructors

1. **Same name as the class**
	```
	class Car {
	    Car() { }
	}
	```
2. **No return type**  
	Not even `void`.
3. **Automatically called** during object creation.
4. If you do NOT create a constructor → Java creates a **Default Constructor** for you.

---

# ⭐ 5. Types of Constructors in Java

There are **3 main types**:

---

## **1\. Default Constructor (created by Java)**

If YOU don’t write any constructor, Java writes a hidden one:

```
Car() { }
```

This constructor:

- sets default values
- does nothing else

### Example:

```
class Car {
    String color;  // null
    int speed;     // 0
}
```

Java creates a default constructor automatically.

---

## **2\. No-Argument Constructor (you define it)**

This is when you write:

```
class Car {
    Car() {
        this.color = "Black";
        this.speed = 0;
    }
}
```

Here:

- You define initial values
- It overrides Java’s default constructor

---

## **3\. Parameterized Constructor**

This is the **most common** type.

It allows you to give values while creating the object:

```
class Car {
    String color;
    int speed;

    Car(String color, int speed) {
        this.color = color;
        this.speed = speed;
    }
}
```

Now object creation:

```
Car c = new Car("Red", 120);
```

This way:

- no manual setting
- no missing values
- cleaner code
- safer object creation

---

# ⭐ 6. How a Constructor Helps During Object Creation

### ➤ It ensures **mandatory fields** are initialized

Instead of:

```
User u = new User();
u.name = "Sourav";
u.age = 25;
```

Constructor forces required values:

```
User u = new User("Sourav", 25);
```

### ➤ Prevents incomplete objects

With constructor, it’s impossible to forget data.

### ➤ Keeps code consistent

Every object is created with the same flow.

### ➤ Encapsulation

You can keep variables private and only allow initialization through constructor.

### ➤ Readability

One clean line creates a fully valid object.

---

# ⭐ 7. Deep JVM Understanding: How exactly constructor works?

When you write:

```
Car c = new Car();
```

JVM does this internally:

1. **Allocate memory** for Car object
2. **Set default values** (null, 0, false…)
3. **Call constructor**
4. Constructor sets real values
5. Return reference stored in `c`

This is why you never write:

```
new Car.constructor();
```

Because JVM automatically calls it.

---

# ⭐ 8. Constructor Overloading

You can create **multiple constructors** with different parameters.

Example:

```
class Car {
    String color;
    int speed;

    Car() {
        color = "Black";
        speed = 0;
    }

    Car(String color) {
        this.color = color;
        speed = 0;
    }

    Car(String color, int speed) {
        this.color = color;
        this.speed = speed;
    }
}
```

Java will choose the constructor based on your arguments.

---

# ⭐ 9. Can constructors call other constructors?

Yes → using `this()` keyword.

Example:

```
Car() {
    this("Black", 0); // calling another constructor
}

Car(String color, int speed) {
    this.color = color;
    this.speed = speed;
}
```

---

# ⭐ FINAL MEMORY SUMMARY

| Concept | Meaning |
| --- | --- |
| Constructor | special method that sets initial state |
| Why exists | ensures every object starts correctly |
| When called | during `new` object creation |
| Types | default, no-arg, parameterized |
| Helps because | prevents incomplete objects, improves structure |
| JVM role | allocates memory → calls constructor → object ready |



---

# Access **Modifier**

Access modifiers control **who can access**:
- a class
- a variable
- a method
- a constructor

Think of them like **privacy settings** on Instagram:

- Public → everyone can see
- Private → only you
- Protected → your followers
- Default → your close circle

---

# ⭐ PART 2 — Why Do Access Modifiers Exist?

Because **not all data should be open to everyone**.

Example:

- A `BankAccount` should NOT allow anyone to directly change the balance.
- A `Car` should NOT let another class directly change the engine number.

Without access modifiers:  
❌ Any class can modify anything  
❌ No data safety  
❌ High chances of bugs  
❌ No control over object state

Access modifiers give **security + structure**.

---

# ⭐ PART 3 — The 4 Access Modifiers (Explained Like a Baby)

Here is the table first:

| Modifier | Same Class | Same Package | Subclass in other pkg | Other Packages |
| --- | --- | --- | --- | --- |
| public | ✔ | ✔ | ✔ | ✔ |
| protected | ✔ | ✔ | ✔ | ❌ |
| default (no keyword) | ✔ | ✔ | ❌ | ❌ |
| private | ✔ | ❌ | ❌ | ❌ |

Now let’s break them one by one.

---

## ⭐ 1. public

**Everyone can use it. Anywhere.**

Example:

```
public void start() {}
```

Why useful?

- Methods that must be called from outside (e.g., `main()`, API methods)

---

## ⭐ 2. private

**Only the same class can use it.**  
Not even same package can access.

Example:

```
private int balance;
```

Why useful?

- To protect sensitive data
- No random changes allowed

---

## ⭐ 3. default (package-private)

If you do **NOT** write any modifier:

```
String color;
```

This means:

- Accessible only within same package
- Not accessible outside package

---

## ⭐ 4. protected

Accessible in:

- same class
- same package
- subclasses in other packages

Not accessible to non-subclass in other packages.

Useful for inheritance.

---

# ⭐ PART 4 — The Real Problem With `public` Variables

Suppose we write:

```
public int balance;
```

Then anywhere in the code, someone can do:

```
account.balance = -1000;
```

This is DANGEROUS.

- wrong values
- inconsistent object state
- security risk
- business rules broken

So Java gives a concept called:

# ⭐ Encapsulation

Where you:

1. Make variables **private**
2. Provide **controlled access** through getters & setters

---

# ⭐ PART 5 — What Are Getters and Setters?

## 🔹 Getter

A method that **returns** (gets) a private variable’s value.

```
public int getBalance() {
    return this.balance;
}
```

## 🔹 Setter

A method that **sets/updates** a private variable’s value.

```
public void setBalance(int balance) {
    this.balance = balance;
}
```

---

# ⭐ PART 6 — Why Do We Use Getters & Setters?

This is **VERY important**.

### ✔ Reason 1: To protect data (Encapsulation)

Instead of:

```
public int balance;
```

We use:

```
private int balance;
```

No one can modify it directly.

### ✔ Reason 2: We can apply validation

Example:

```
public void setBalance(int balance) {
    if(balance >= 0) {
        this.balance = balance;
    } else {
        System.out.println("Invalid balance!");
    }
}
```

Now no one can set negative balance.

### ✔ Reason 3: We can add logic later without breaking code

If another class accesses:

```
int x = obj.getBalance();
```

We can later modify how balance is calculated.

### ✔ Reason 4: Read-only or write-only variables

Getter only → read-only  
Setter only → write-only

Example:

```
public int getAge() { return age; } // read-only
```

---

# ⭐ PART 7 — How They Look in Real Java Classes

```
class Car {
    private String color;
    private int speed;

    // Getter
    public String getColor() {
        return color;
    }

    // Setter
    public void setColor(String color) {
        this.color = color;
    }

    // Getter
    public int getSpeed() {
        return speed;
    }

    // Setter with validation
    public void setSpeed(int speed) {
        if(speed >= 0) this.speed = speed;
    }
}
```

And usage:

```
Car c = new Car();
c.setColor("Red");
c.setSpeed(100);

System.out.println(c.getColor());
System.out.println(c.getSpeed());
```

---

# ⭐ FINAL MEMORY SUMMARY (Keep This Forever)

### ⭐ Access modifiers = control who can access what

### ⭐ Why? → security + structure + safety

### ⭐ 4 types:

- public → everyone
- private → only same class
- protected → package + subclass
- default → only package

### ⭐ Use private variables → hide data

### ⭐ Use getters/setters → control access

### ⭐ They prevent invalid changes + give clean API

---

# ⭐ 1. What does "passing an object" mean?

When you call a method and give it an object as a parameter:

```
Car c = new Car();
driveCar(c);
```

You are **passing the object** to another method.

But *what exactly is passed*?

---

# ⭐ 2. IMPORTANT TRUTH: Java is ALWAYS “Pass-by-Value”

Many people say “Java is pass-by-reference.”

❌ That is incorrect.  
✔ Java passes everything **by value**, but…  
✔ When an object is passed, the value being passed = **the reference to the object**, not the object itself.

So the method receives a **copy of the reference** to the object.

Let’s break this down.

---

# ⭐ 3. Memory Model: Stack + Heap (Simple Visual)

### ✔ Heap

Where objects actually live.

### ✔ Stack

Where references (variables pointing to objects) live.

Example:

```
Car c = new Car();
```
- `c` is a reference variable → lives in **stack**
- actual `Car` object → lives in **heap**

When you pass an object:

```
driveCar(c);
```

You are passing **the reference value** (the memory address) to the method.

---

# ⭐ 4. Example — Passing an Object

```
void driveCar(Car car) {
    car.speed = 100;
}
```

Call:

```
Car c = new Car();
driveCar(c);
System.out.println(c.speed);  // 100
```

Why does `speed` change?

Because:

- inside `driveCar()`, you have a reference pointing to the **same object**
- modifying it changes the actual heap object

---

# ⭐ 5. Diagram (Simple)

```
Car c ---> [Car Object in Heap]
             speed = 0
```

When passed to function:

```
driveCar(c);

Inside method:
car ---> [same Car Object in Heap]
```

Both `c` and `car` point to **same object**.

So modifying through `car` affects `c`.

---

# ⭐ 6. Example where object does NOT change

Many beginners get confused here:

```
void change(Car car) {
    car = new Car();   // new object created
    car.speed = 200;
}
```

Call:

```
Car c = new Car();
change(c);
System.out.println(c.speed);   // still 0, NOT 200
```

Why?

Because you changed **the reference inside method**, not the original.

Think of it like copying a key:

```
You have houseKey1 (points to your house)
You make houseKey2 (copy of key)

Inside method:
houseKey2 starts pointing to another house
But houseKey1 still points to original house
```

---

# ⭐ 7. IMPORTANT RULES

### ✔ Rule 1: If you change object’s fields → changes reflect outside

Because both references point to same heap object.

### ✔ Rule 2: If you assign new object inside method → does NOT affect original reference

Because assignment changes only the local copy of reference.

---

# ⭐ 8. Another Example — Modifying object values

```
class NumberWrapper {
    int x;
}

void modify(NumberWrapper n) {
    n.x = 50;           // modifies actual object
}

NumberWrapper nw = new NumberWrapper();
nw.x = 10;
modify(nw);
System.out.println(nw.x); // 50
```

Works because object is shared.

---

# ⭐ 9. Another Example — Reassigning Reference

```
void modify(NumberWrapper n) {
    n = new NumberWrapper();  
    n.x = 100;
}

NumberWrapper nw = new NumberWrapper();
nw.x = 10;

modify(nw);

System.out.println(nw.x); // 10 (unchanged)
```

Because inside the method, you only changed the local reference.

---

# ⭐ 10. Why this matters in real life?

Because:

- Functions modify objects all the time
- Lists, Maps, custom objects are passed around
- Understanding reference behavior prevents bugs
- You’ll understand why some changes stick and some don’t
- Core concept for frameworks like Spring, Hibernate
- Helps understand immutability (String, Integer)

---

# ⭐ 11. Interaction with Constructors

When you do:

```
Car c = new Car();
```

Constructor returns a **reference** to new heap object.

Passing that reference is what allows other methods to modify the object.

---

# ⭐ FINAL SUMMARY (Keep This Forever)

### ✔ Java is ALWAYS pass-by-value

BUT

### ✔ When passing objects → the "value" is the reference

Therefore:

### ✔ Changing object’s fields → affects original

### ✔ Reassigning reference inside method → does NOT affect original