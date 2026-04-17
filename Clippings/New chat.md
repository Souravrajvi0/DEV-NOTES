

# ⭐ 1. Why Do We Need StringBuilder?

Because **String is immutable**.

Example:

```
String s = "A";
s = s + "B";
s = s + "C";
```

This creates **3 different string objects**:

- "A"
- "AB"
- "ABC"

Very slow for loops, concatenations, and frequently-changing text.

So we need something **mutable**, which can change without creating new objects.

That's **StringBuilder**.

---

# ⭐ 2. What Is String?

### ✔ Immutable object

Once created, cannot be changed.

### ✔ Memory Allocation

Stored in:

- String Constant Pool (SCP)
- or normal heap (when using `new`)

### ✔ Concatenation using `+`

Behind the scenes, Java internally uses **StringBuilder** for optimization.

Example:

```
String s = "Hello" + "World";
```

Compiler rewrites it as:

```
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append("World");
s = sb.toString();
```

---

# ⭐ 3. What Is StringBuilder?

### ✔ Mutable (contents can change)

You can append, delete, modify text **without creating new objects**.

### ✔ Faster for String manipulation

Especially for loops, heavy concatenation, dynamic text creation.

### ✔ Not thread-safe

(Meaning: not synchronized → but faster than StringBuffer)

---

# ⭐ 4. Main Difference Table (Very Important)

| Feature | String | StringBuilder |
| --- | --- | --- |
| Mutability | ❌ Immutable | ✔ Mutable |
| Speed (modifying) | Slow | Very Fast |
| Memory usage | High (creates new objects) | Low (modifies same buffer) |
| Thread safety | Yes (immutable) | No |
| Use cases | Fixed text | Changing text (loops, concat, buffers) |
| Storage | SCP or Heap | Heap only |

---

# ⭐ 5. Examples (Very Clear)

## ✔ A. Using String

```
String s = "Hello";
s = s + " World";
```

Creates new objects → slower.

---

## ✔ B. Using StringBuilder

```
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
```

No new objects created → much faster.

---

# ⭐ 6. Performance Difference Example

### Using String in a loop (❌ very slow):

```
String s = "";
for(int i=0; i<10000; i++){
    s = s + i;
}
```

This creates **10,000 new String objects**.

---

### Using StringBuilder (✔ extremely fast):

```
StringBuilder sb = new StringBuilder();
for(int i=0; i<10000; i++){
    sb.append(i);
}
```

Only **1 object** for the whole loop.

---

# ⭐ 7. Important Methods of StringBuilder

```
append()      // add text
insert()      // insert at position
delete()      // remove characters
deleteCharAt()
reverse()     // reverse the string
toString()    // convert back to String
setLength()   // resize
replace()
```

Example:

```
StringBuilder sb = new StringBuilder("Hello");
sb.append("World");
System.out.println(sb);  // HelloWorld
```

---

# ⭐ 8. When to Use String vs StringBuilder

## ✔ Use **String** when:

- Text is **constant or rarely changes**
- Creating string literals
- Using it as a key in a HashMap
- For read-only operations

## ✔ Use **StringBuilder** when:

- You are building strings inside loops
- Heavy concatenation
- Dynamic strings (logging, JSON building, SQL building)
- Modifying strings frequently

---

# ⭐ 9. What About StringBuffer?

- Same as StringBuilder
- BUT thread-safe (synchronized)
- Slower than StringBuilder
- Rarely used today unless in multi-threaded code


# ⭐ 1. What Is an ArrayList?

`ArrayList` is a **resizable array** from the Java Collections Framework.

Java’s normal array has limitations:

- Fixed size
- Hard to insert/delete
- No built-in functions

So Java created **ArrayList** to solve this.

### ArrayList:

- Dynamic size (grows automatically)
- Stores elements **in order**
- Allows duplicates
- Indexed like arrays (`get(index)`)
- Uses a **dynamic array internally**

---

# ⭐ 2. How to Import ArrayList

ArrayList is in `java.util`.

```
import java.util.ArrayList;
```

---

# ⭐ 3. How to Declare an ArrayList

Syntax:

```
ArrayList<Integer> list = new ArrayList<>();
ArrayList<String> names = new ArrayList<>();
ArrayList<Double> nums = new ArrayList<>();
```

⚠ **You must use wrapper classes**, not primitives.

❌ Not allowed:

```
ArrayList<int>
```

✔ Allowed:

```
ArrayList<Integer>
```

This is due to **generics**.

---

# ⭐ 4. Adding Elements

```
list.add(10);
list.add(20);
list.add(30);
```

Add at specific index:

```
list.add(1, 99);  // Insert 99 at index 1
```

---

# ⭐ 5. Accessing Elements

```
list.get(0);  // returns element at index 0
```

If you use an invalid index → `IndexOutOfBoundsException`.

---

# ⭐ 6. Updating Elements

```
list.set(1, 500);  // changes index 1 to 500
```

---

# ⭐ 7. Removing Elements

By index:

```
list.remove(2);
```

By value (Object):

```
list.remove(Integer.valueOf(10));
```

---

# ⭐ 8. ArrayList Size vs Capacity

This is extremely important.

### ✔ Size → number of elements

`list.size()`

### ✔ Capacity → internal array length

Not directly visible.

### How it works internally:

- Default capacity = **10**
- When full, ArrayList grows by **1.5x** (i.e., 10 → 15 → 22 → 33…)

This resizing is expensive (creates new array + copies elements).

---

# ⭐ 9. Internal Working of ArrayList (Deep)

Internally, ArrayList uses:

```
Object[] elementData;
```

When you do `add()`, it checks:

- If space available -> add directly
- If full -> create new array with 1.5x capacity → copy old data → then add new element

---

# ⭐ 10. Autoboxing/Unboxing (Important)

ArrayList cannot store primitives.  
But JVM automatically converts:

```
list.add(10); // int → Integer (autoboxing)
int x = list.get(0); // Integer → int (unboxing)
```

---

# ⭐ 11. Looping Over ArrayList

## ✔ Normal for loop (when you need index)

```
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}
```

## ✔ Enhanced for loop (best for reading)

```
for (int num : list) {
    System.out.println(num);
}
```

⚠ Cannot modify structure using enhanced loop  
(remove while iterating → gives error).

---

# ⭐ 12. Iterator (Safe for remove)

```
Iterator<Integer> it = list.iterator();

while (it.hasNext()) {
    int x = it.next();
    if (x == 10) it.remove();
}
```

---

# ⭐ 13. Common Methods of ArrayList

### ✔ size()

```
list.size();
```

### ✔ contains()

```
list.contains(20);
```

### ✔ indexOf()

```
list.indexOf(30);
```

### ✔ clear()

```
list.clear();
```

### ✔ isEmpty()

```
list.isEmpty();
```

### ✔ addAll()

```
list.addAll(otherList);
```

### ✔ subList()

```
List<Integer> part = list.subList(1, 3);
```

---

# ⭐ 14. Passing ArrayList to Methods

Same as arrays → passes **reference**, not copy.

```
void fun(ArrayList<Integer> a){
    a.add(100);
}

ArrayList<Integer> list = new ArrayList<>();
fun(list);
System.out.println(list); // contains 100
```

Because the internal array is referenced.

---

# ⭐ 15. Array vs ArrayList — FULL Comparison

| Feature | Array | ArrayList |
| --- | --- | --- |
| Size | Fixed | Dynamic |
| Type | Can store primitives | Cannot store primitives (uses wrappers) |
| Syntax | `int[] arr` | `ArrayList<Integer> list` |
| Performance | Fast for fixed-size operations | Slightly slower due to resizing |
| Length | `arr.length` | `list.size()` |
| Adding/removing | Hard (manual shifting) | Easy (built-in methods) |
| Memory | Direct contiguous array | Dynamic array inside (Object\[\]) |
| Best for | Low-level, performance-critical | High-level resizable lists |

---

# ⭐ 16. When to Use ArrayList?

Use ArrayList when:

- You need **dynamic size**
- You frequently **add/remove elements**
- You want built-in methods
- You need to pass lists around easily
- You want readable & clean code

Use **Array** when:

- Size is fixed
- Performance-critical situations
- Working with primitives (to avoid boxing)


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