---
view-count: 2
Date: 2024-10-31T10:21:00
---
**var**
- Variables declared with `var` have **function scope or global scope, but not block scope.** They can be **redeclared and reassigned within their scope.**
**let**
- Variables declared with `let` have **block scope**, meaning they are only accessible within the block they are declared in (like loops or conditionals).
- They **can be reassigned but not redeclared within their scope.**
- `let` was introduced in ES6 and is now the **preferred way to declare variables when you need to reassign them.**
**const**
- Variables declared with `const` also have **block scope.**
- They **must be initialized with a value and cannot be reassigned.**
- They **cannot be redeclared within their scope.**
- `const` is **used for values that should not change during the program's execution.**

In JavaScript, when you use the `const` keyword, it declares a constant variable. The value of a `const` variable cannot be reassigned once it's been initialized. However, it's important to note that if the value assigned to a `const` variable is an object or array, the properties or elements of that object/array can still be modified. The immutability only applies to the variable binding itself, not to its contents in the case of complex data types like objects and arrays.

```javascript 
// Declaring a constant variable with a number
const number = 5;
// Trying to reassign the constant variable
number = 10; // ❌ Error: Assignment to constant variable
```

This error happens because `number` is a primitive constant, and JavaScript doesn't allow reassigning `const` variables.

Now, let's see what happens when we use `const` with an object or array:


```javascript
// Declaring a constant object
const car = { brand: 'Toyota', color: 'red' };

// Modifying properties of the object
car.color = 'blue'; // ✅ This is allowed
console.log(car); // Output: { brand: 'Toyota', color: 'blue' }

// Adding a new property
car.model = 'Corolla'; // ✅ This is allowed
console.log(car); // Output: { brand: 'Toyota', color: 'blue', model: 'Corolla' }

// Trying to reassign the entire object
car = { brand: 'Honda' }; // ❌ Error: Assignment to constant variable

```

Here, even though `car` is declared with `const`, we can change its properties and add new ones. However, reassigning `car` to a different object causes an error because the reference binding of `car` itself is constant.

### Example with an Array

```javascript
// Declaring a constant array
const numbers = [1, 2, 3];

// Modifying elements of the array
numbers[0] = 10; // ✅ This is allowed
console.log(numbers); // Output: [10, 2, 3]

// Adding elements to the array
numbers.push(4); // ✅ This is allowed
console.log(numbers); // Output: [10, 2, 3, 4]

// Trying to reassign the entire array
numbers = [5, 6, 7]; // ❌ Error: Assignment to constant variable
```


![Untitled 72.png|1083x516](../../Images/Untitled%2072.png)

![Untitled 1 62.png](../../Images/Untitled%201%2062.png)

-> JS,Agar purely interpreted hoti toh hello toh print hota na

![Untitled 2 47.png](../../Images/Untitled%202%2047.png)
Every JS code is executed in two phases:
**1.Parsing→ Scope resolution: JS Reads the whole code in the first go and every variable and function it sees tries to allocate a particular scope**
**2.Execution**
![Untitled 3 44.png](../../Images/Untitled%203%2044.png)
Global Scope:→
![Untitled 4 41.png](../../Images/Untitled%204%2041.png)
->Global scope hai kyonki kisi bhi block and function k bahar hai ye name variable declaration hua h toh iska scope global hoga
![Untitled 5 36.png](../../Images/Untitled%205%2036.png)
->YAHAN ERROR AEGA FOR SURE
![Untitled 6 34.png](../../Images/Untitled%206%2034.png)
The error occurs on **line 1** because of the **Temporal Dead Zone**:

- Variables declared with `let` and `const` are hoisted but not initialized
    
- They cannot be accessed before their declaration line
    
- From the start of the scope until the declaration, the variable exists in a "dead zone"
    

If you were to **fix the code** by removing or commenting out line 1:
![Untitled 7 29.png](../../Images/Untitled%207%2029.png)
INTRESTING
![Untitled 8 26.png](../../Images/Untitled%208%2026.png)

![Untitled 9 21.png](../../Images/Untitled%209%2021.png)
->MEANING KI AGAR INITIALIZATION NAHI KIYA TOH IN THAT CASE KI DECLARATION SE PEHLE USE KAR SAKTE HAIN KYONKI GLOBAL SCOPE HAI!!

![Untitled 10 20.png](../../Images/Untitled%2010%2020.png)

->Var only declares function and global scoped Variables no block scope variables are created, Block mein koi var variable declare kiya toh uss case mein hum bahar use kar skte hain block k

![Untitled 11 18.png](../../Images/Untitled%2011%2018.png)

![Untitled 12 16.png](../../Images/Untitled%2012%2016.png)

![Untitled 13 10.png](../../Images/Untitled%2013%2010.png)
-> Pehle Parsing toh hogayi hai na that mean scope decide ho chuka hai 
->Yahan Bat horahi hai visibilty ki naki value ki
-> DECLARAT
```javascript
if (false) {
    var x = 10;
}
console.log(x); // Output: 10
```


![Untitled 14 8.png](../../Images/Untitled%2014%208.png)

![Untitled 15 7.png](../../Images/Untitled%2015%207.png)

- Both snippets will throw a `ReferenceError` when trying to log `x` and `y` respectively, as they are not defined in the scope of the `console.log` statements.



![Untitled 16 7.png](../../Images/Untitled%2016%207.png)

-> Hoisting Hogayi na yahan toh y ki!!

```javascript
function gun() {
    var y;        // Declaration is hoisted
    console.log(y); // y is currently undefined
    y = 10;      // Initialization happens here
}

```





![Untitled 17 7.png](../../Images/Untitled%2017%207.png)

->On the other hand When we use let, Hum use uss variable k declaration k bad hi use kar sakte hain pehle karenge toh error dega

-> Basically We can use var anywhere in the scope uski value undefined aa skti hai agar humne use kiya before initialization but agar let use kiya toh hum usko sirf uske niche hu  use kar sakte hain jahan maine use declare kiya hai!

-> Ye decisions liye jate hain parsing k time kon kisko kahan accesible hoga

————————————————————————————————————————————------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


So what happens during the parsing cycle→

->JS pura code padhega and then start allocating their corresponding scopes to the variables
-> Every Time we see a formal Declaration We think of thee scope in the Parsing phase!
  

![Untitled 18 7.png](../../Images/Untitled%2018%207.png)

AUTOGLOBALS

->Since parsing mein formal declarations walo ko scope define hojaega

When we’re trying to assign a value to a variable or fetch value from it And we didn’t find it in the all the enclosing scopes then this variable will automatically get a global scope (during execution phase)

Jabh hum value mein kuch asssign kar rahe hote hain tabhi autoglobals ka concept kam krta hai and access karenge value tabh refrence error aega

![Untitled 19 7.png](../../Images/Untitled%2019%207.png)

But yahan error aega since execution phase mein content ka scope global hua tha so is bar error aega

![Untitled 20 7.png](../../Images/Untitled%2020%207.png)

**Kkabhi bhi dikkat ho koi toh bas two parts mein divide kar lo process ko parsing and execution mein**

![Untitled 21 7.png](../../Images/Untitled%2021%207.png)

->This Fun will get the outside enclosing scope, Hence global scope

![Untitled 22 7.png](../../Images/Untitled%2022%207.png)

->While in strict mode you can only use in it inside the block bahar error aega




![Untitled 23 6.png](../../Images/Untitled%2023%206.png)




![Untitled 24 6.png](../../Images/Untitled%2024%206.png)




![Untitled 25 6.png](../../Images/Untitled%2025%206.png)



Use case of var and let

![Untitled 26 4.png](../../Images/Untitled%2026%204.png)




![Untitled 27 4.png](../../Images/Untitled%2027%204.png)



![Untitled 28 4.png](../../Images/Untitled%2028%204.png)



![Untitled 29 4.png](../../Images/Untitled%2029%204.png)



![Untitled 30 4.png](../../Images/Untitled%2030%204.png)

![Untitled 31 4.png](../../Images/Untitled%2031%204.png)

Unitnitialised const is not allowed

---

  

![Untitled 32 4.png](../../Images/Untitled%2032%204.png)

![Untitled 33 4.png](../../Images/Untitled%2033%204.png)

![Untitled 34 4.png](../../Images/Untitled%2034%204.png)

![Untitled 35 4.png](../../Images/Untitled%2035%204.png)

→Fun() will give error!

→ Now Fun() will only be accesible through the variable f,In one way we can say fun() ka scope f [hai.So](http://hai.So) to use funtion fun we need to use contant f. TOh jo scope f ka hoga vahi scope fun ka bhi hoga

→Tight boundation to f

→If we do console.log(f()) it will give undefined ,since it’s not returning anything

Why anonymous funtions are a bad choice

![Untitled 36 4.png](../../Images/Untitled%2036%204.png)

![Untitled 37 2.png](../../Images/Untitled%2037%202.png)

![Untitled 38 2.png](../../Images/Untitled%2038%202.png)

Use Case Of iffy

![Untitled 39 2.png](../../Images/Untitled%2039%202.png)

Js mein funtion mein function pass kr skte hain