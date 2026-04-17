# ⭐ 1. What Is an Array & Why Do We Use It?
When you need to store **lots of values of the same type** (int, float, String, objects), instead of creating many variables:

```
int a1, a2, a3, a4;
```

…you create an **array**, which stores them **together in contiguous memory**.

---

# ⭐ 2. How Arrays Work (Very Important)

- Array size is **fixed** once created.
- Elements are stored **next to each other** in memory.
- Every element has an **index** starting from **0**.

Example:

```
Index:  0   1   2   3
Value: 10  20  30  40
```

`arr[0]` → 10  
`arr[3]` → 40

---

# ⭐ 3. Declaring an Array (Just Declaration, No Memory Yet)

Two ways:

```
int[] arr;   // Recommended
int arr2[];  // Also valid
```

Right now, **no memory is allocated**, just a reference variable.

---

# ⭐ 4. Allocating Memory for an Array (Using new)

```
arr = new int[5];
```

This creates an array of 5 integers.

So full declaration + allocation:

```
int[] arr = new int[5];
```

---

# ⭐ 5. Default Values Inside an Array

Java always initializes array elements:

| Type | Default |
| --- | --- |
| int, byte, short, long | 0 |
| float, double | 0.0 |
| char | '\\u0000' (looks blank) |
| boolean | false |
| object references | null |

Example:

```
int[] arr = new int[3];
System.out.println(arr[0]); // prints 0
```

---

# ⭐ 6. Initializing an Array (Putting Values)

### Method 1: Manually

```
arr[0] = 10;
arr[1] = 20;
arr[2] = 30;
```

### Method 2: Using Array Literal (Shortcut)

```
int[] arr = {10, 20, 30, 40};
```

Here memory is automatically created based on values.

---

# ⭐ 7. Accessing Values in Array

```
System.out.println(arr[2]); // prints 30
```

Indexes must be **0 to size-1**.  
Using an invalid index → `ArrayIndexOutOfBoundsException`.

---

# ⭐ 8. Printing the Whole Array — Why “Weird Values”?

This:

```
System.out.println(arr);
```

prints something like:

```
[I@3f99bd52
```

Because:

- Arrays are objects
- `toString()` prints **memory address hash-like value**

### Correct way to print full array:

```
System.out.println(Arrays.toString(arr));
```

But you must import:

```
import java.util.Arrays;
```

---

# ⭐ 9. Loops for Accessing Arrays

## ✔ Normal for loop (best for indexing)

Use when:

- you need **index**
- you want to **modify** array values
- you want to iterate in reverse
```
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

## ✔ Enhanced for loop (for-each loop, best for reading)

Use when:

- you only want to **read** elements
- you don’t care about index
```
for (int value : arr) {
    System.out.println(value);
}
```

### ⚠ Limitation of Enhanced Loop

You **cannot modify index-specific values**:

This **won’t change** the array:

```
for (int x : arr) {
    x = x + 1; // Invalid for modification
}
```

---

# ⭐ 10. Passing Arrays to Methods — Reference Is Passed

### Key point:

Java **passes the reference** (not the whole array).

```
void printArray(int[] a){
    System.out.println(Arrays.toString(a));
}

int[] arr = {1, 2, 3};
printArray(arr);
```

### Example showing reference behavior:

```
void change(int[] a){
    a[0] = 99;
}

int[] arr = {1, 2, 3};
change(arr);
System.out.println(arr[0]); // prints 99
```

Because the method got **same array reference**, not a copy.

---

# ⭐ 11. Array Functions (Methods) from java.util.Arrays

Java provides many useful methods:

### ✔ Sort an array

```
Arrays.sort(arr);
```

### ✔ Convert array to string

```
Arrays.toString(arr);
```

### ✔ Fill array with a value

```
Arrays.fill(arr, 5);
```

### ✔ Copy an array

```
int[] b = Arrays.copyOf(arr, arr.length);
```

### ✔ Compare arrays

```
Arrays.equals(arr, b);
```

---
# STRING
# ⭐ 1. Is String an Object in Java?

**YES.**  
`String` is a **class in java.lang** package.

So every String you create is an **object**, even if you write it like this:

```
String s = "Hello";
```

This looks like a primitive, but it's actually an **object created by the String class**.

---

# ⭐ 2. Two Ways to Create Strings

## ✔ (A) Using String Literal

This is the most common and efficient way.

```
String s1 = "Java";
```

Where is it stored?

👉 In **String Constant Pool (SCP)** — a special memory area inside the heap.

### Behavior:

- If `"Java"` already exists in SCP, Java **reuses** it.
- If not, it creates it once.

Example:

```
String s1 = "Hello";
String s2 = "Hello";
```

Here **one object** is created, and both variables point to it.

---

## ✔ (B) Using new String()

```
String s1 = new String("Java");
```

This ALWAYS creates a **new object in the heap**, even if `"Java"` already exists in SCP.

So:

```
String s1 = "Java";            // in SCP
String s2 = new String("Java"); // new object in heap
```

🚨 These are **not the same objects**, even though their content is same.

---

# ⭐ 3. Where Exactly Is String Stored?

Java stores Strings in two areas:

## ✔ 1. **String Constant Pool** (inside Heap)

Created when:

```
String s = "ABC";
```

Why SCP exists?

- To save memory
- To reuse same literals
- To be efficient

## ✔ 2. **Normal Heap Memory**

Created when using:

```
new String("ABC");
```

So:

| Syntax | Where stored? | Why |
| --- | --- | --- |
| `"Java"` | SCP | Shared, reusable |
| `new String("Java")` | Heap | Always new object |

---

# ⭐ 4. String Immutability — What Does It Mean?

**A String cannot be changed once created.**

Example:

```
String s = "Hello";
s = s + "World";
```

What actually happens?

- `"HelloWorld"` is a **new object**
- `"Hello"` stays unchanged
- `s` now points to the new object

### Why immutable?

- Security (used in passwords, file paths)
- Thread-safety
- Hashing optimization
- SCP would break if Strings could change

---

# ⭐ 5. String Comparison: `==` vs `.equals()`

This is CRITICAL.

## ✔ `==` → compares **references**

- Do both variables point to the **same object**?

Example:

```
String a = "Hello";
String b = "Hello";
System.out.println(a == b); // true (same SCP object)
```

But:

```
String a = "Hello";
String b = new String("Hello");
System.out.println(a == b); // false (different objects)
```

## ✔ `.equals()` → compares **content**

```
System.out.println(a.equals(b)); // true (content same)
```

---

# ⭐ 6. Important Methods of the String Class

Here are the main methods you actually use:

### ✔ Length

```
str.length();
```

### ✔ charAt()

```
str.charAt(2);
```

### ✔ substring()

```
str.substring(1, 4);
```

### ✔ equals() / equalsIgnoreCase()

```
str.equals("abc");
str.equalsIgnoreCase("ABC");
```

### ✔ toUpperCase(), toLowerCase()

```
str.toUpperCase();
```

### ✔ startsWith / endsWith

```
str.startsWith("He");
str.endsWith("lo");
```

### ✔ split()

```
str.split(" ");
```

### ✔ trim()

```
str.trim();
```

### ✔ replace()

```
str.replace("a", "b");
```

### ✔ indexOf()

```
str.indexOf('a');
```

---

# ⭐ 7. Why String Is Used So Much?

- Represents text
- Used in 90% of APIs
- Immutable → safe
- Hashing → fast
- Common in keys (HashMap, etc.)

---

# ⭐ 8. Example: Literal vs new String Comparison

```
String s1 = "Java";
String s2 = "Java";
String s3 = new String("Java");

System.out.println(s1 == s2); // true (same SCP object)
System.out.println(s1 == s3); // false (heap object)
System.out.println(s1.equals(s3)); // true (content)
```

---

# ⭐ 9. Interning Strings — Bringing Strings to SCP

```
String s1 = new String("Hello");
String s2 = s1.intern();
String s3 = "Hello";

System.out.println(s2 == s3); // true
```

`intern()` → ensures object is in SCP



# StringBuilder
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


# ArrayList
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