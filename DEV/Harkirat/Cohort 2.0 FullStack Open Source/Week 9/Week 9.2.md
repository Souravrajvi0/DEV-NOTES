---
view-count: 2
---
# Introduction to Typescript
![Week 9.2-20241026170127052.webp](../../../Images/Week%209.2-20241026170127052.webp)

  

## 1] Loosely Typed Languages

1. **Runtime Type Association:** Data types are associated with values at runtime. Unlike strongly typed languages, type information is not strictly bound during compilation but rather at the time of execution.
2. **Dynamic Type Changes:** Variables can change types during execution, offering more adaptability. This flexibility allows for a dynamic approach to variable assignments and operations.
3. **Runtime Error Discovery:** Type errors may be discovered during runtime, potentially leading to unexpected behaviors. This characteristic provides more freedom but requires careful handling.
4. **Examples of Loosely Typed Languages: J**avaScript, Python, Ruby

  

## C++ Code (Doesn't Work ❌)

```C++
\#include <iostream>

int main() {
  int number = 10;
  number = "text";  // Error: Cannot assign a string to an integer variable
  return 0;
}
```

**Explanation:**

- C++ is a statically-typed language, meaning variable types must be declared and are enforced at compile-time.
- In the given code, `number` is declared as an integer (`int`), and attempting to assign a string ("text") to it results in a compile-time error.
- The type mismatch between the declared type and the assigned value leads to a compilation failure.

## 2] Strongly Typed Languages

1. **Compile-Time Enforcement:** The data type of a variable is strictly enforced during compilation. This means that the compiler checks and ensures that variables are used in a way that is consistent with their types at compile time.
2. **Type Safety:** The compiler or interpreter guarantees that operations are performed only on compatible types. This ensures that type-related errors are caught early in the development process.
3. **Early Error Detection:** Type errors are identified and addressed at compile-time, providing early feedback to developers. This leads to increased reliability and reduces the likelihood of runtime errors.
4. **Examples of Strongly Typed Languages:** Java, C#, TypeScript

  

## JavaScript Code (Does Work ✅)

```JavaScript
function main() {
  let number = 10;
  number = "text";  // Valid: JavaScript allows dynamic typing
  return number;
}
```

**Explanation:**

- JavaScript is a dynamically-typed language, allowing variables to change types during runtime.
- In the provided JavaScript code, `number` is initially assigned the value `10` (a number), and later, it is assigned the value `"text"` (a string).
- JavaScript allows this flexibility, and the code executes without type-related errors.

**Considerations:**

- Statically-typed languages like C++ provide early error detection during compilation, ensuring type consistency.
- Dynamically-typed languages like JavaScript offer flexibility but may require careful handling to avoid unexpected runtime errors.

  

> The choice between strongly typed and loosely typed languages depends on project requirements, developer preferences, and the balance between early error detection and flexibility during development. Each type has its advantages and considerations, influencing their suitability for specific use cases.
![Week 9.2-20241026170252089.webp](../../../Images/Week%209.2-20241026170252089.webp)
  

# Typescript

## Why Typescript

JavaScript is a powerful and widely used programming language, but it has a dynamic typing system, which means variable types are determined at runtime. While dynamic typing provides flexibility, it can lead to runtime errors that are challenging to catch during development.

## What Typescript

In response to these challenges, Microsoft introduced TypeScript, a superset of JavaScript that adds static typing to the language. TypeScript is designed to address some of the limitations of JavaScript by providing developers with a more robust type system.

  PROVIDING TYPES TO JAVASCRIPT!

![Untitled 14.png](../../../Images/Untitled%2014.png)
-> Iska mtlb ki if I just change the extension of js files to ts it will still work but the opposite is not true!
## How Typescript

1. **Static Typing:**
    - TypeScript introduces static typing, allowing developers to **declare the types of variables, parameters, and return values at compile-time.**
    - Static typing helps catch potential errors during development, offering a level of code safety that may not be achievable in pure JavaScript.
2. **Compatibility with JavaScript:**
    - **TypeScript is a superset of JavaScript, meaning that any valid JavaScript code is also valid TypeScript code.**
    - Developers can gradually adopt TypeScript in existing JavaScript projects without the need for a full rewrite.
3. **Tooling Support:**
    - TypeScript comes with a rich set of tools and features for development, including code editors (like Visual Studio Code) with built-in TypeScript support.
    - T**he TypeScript compiler (tsc) translates TypeScript code into plain JavaScript, allowing it to run in any JavaScript environment.**
4. **Enhanced IDE Experience:**
    - IDEs (Integrated Development Environments) that support TypeScript offer improved code navigation, autocompletion, and better refactoring capabilities.
    - TypeScript's type information enhances the overall development experience.
5. **Interfaces and Type Declarations:**
    - **TypeScript introduces concepts like interfaces and type declarations, enabling developers to define clear contracts for their code.**
    - **Interfaces help document the shape of objects, making it easier to understand and maintain the code.**
6. **Compilation:**
    - **TypeScript code is transpiled (GETS CONVERTED) to JavaScript during the compilation process, ensuring that the resulting code is compatible with various JavaScript environments and browsers.**

  

> Overall, TypeScript provides developers with the benefits of static typing while preserving the flexibility and features of JavaScript. It has gained popularity in large-scale applications and projects where maintaining code quality and catching errors early are crucial.

-> Static Typing is a feature in languages Where Variable types are known and checked at the compile Time, meaning before the code is run. This can help catch type related errors early, making the code safer and often easier to debug!
  

  

# **Execution of TypeScript Code**

->TypeScript code doesn't run natively in browsers or JavaScript environments. Instead, it undergoes a compilation process to generate equivalent JavaScript code. Here's an overview of how TypeScript code is executed:
![Week 9.2-20241026171019955.webp](../../../Images/Week%209.2-20241026171019955.webp)

  

1. **Writing TypeScript Code:**
    - Developers write TypeScript code using `.ts` or `.tsx` files, employing TypeScript's syntax with features like static typing, interfaces, and type annotations.

  

1. **TypeScript Compiler (tsc):**
    - The TypeScript Compiler (`tsc`) is a command-line tool that processes TypeScript code.
    - Developers run `tsc` to initiate the compilation process.

  

1. **Compilation Process:**
    - The TypeScript Compiler parses and analyzes the TypeScript code, checking for syntax errors and type-related issues.
    - It generates equivalent JavaScript code, typically in one or more `.js` or `.jsx` files.

  

1. **Generated JavaScript Code:**
    - The output JavaScript code closely resembles the original TypeScript code but lacks TypeScript-specific constructs like type annotations.
    - TypeScript features that aren't present in JavaScript (e.g., interfaces) are often transpiled or emitted in a way that doesn't affect runtime behavior.

  

1. **JavaScript Execution:**
    - **The generated JavaScript code can now be executed by any JavaScript runtime or browser.**
    - **Developers can include the resulting JavaScript files in HTML documents or use them in Node.js environments.**

  

1. **Runtime Environment:**
    - In the chosen runtime environment, the JavaScript code is interpreted or compiled by the JavaScript engine (e.g., V8 in Chrome, SpiderMonkey in Firefox).
    - Just-in-time (JIT) compilation or interpretation occurs to convert the code into machine code that the computer's processor can execute.

  

1. **Interacting with the DOM (Browser Environments):**
    - In browser environments, the JavaScript code, generated from TypeScript, may interact with the Document Object Model (DOM) to manipulate web page structure and behavior.

  

![Untitled 1 9.png](../../../Images/Untitled%201%209.png)

# **TypeScript Compiler (**`**tsc**`**)**

- **The TypeScript Compiler (`tsc`) is responsible for transpiling TypeScript code into JavaScript.**
- It is a part of the official TypeScript distribution and can be installed using tools like npm.
- **Developers run `tsc` from the command line, specifying the TypeScript file(s) they want to compile.**
- **Configuration for the compilation process can be provided via a `tsconfig.json` file.**
- The compiler performs type checking, emits JavaScript files, and allows customization of compilation options.

  

> In summary, **TypeScript code is transformed into JavaScript through the TypeScript Compiler (`tsc`). This compilation process ensures that TypeScript's features are compatible with existing JavaScript environments, enabling developers to benefit from static typing during development while still producing standard JavaScript for execution.**

  

In addition to the TypeScript Compiler (`**tsc**`), several alternative tools have gained popularity for their efficiency, speed, and additional features when transpiling TypeScript to JavaScript. Here are a couple of noteworthy ones:

1. esbuild: a highly performant JavaScript bundler and minifier, but it also supports TypeScript.
2. **swc (Speedy Web Compiler): a fast and low-level JavaScript/TypeScript compiler.**

The `tsconfig.json` file is essential for configuring how TypeScript compiles your project. It allows you to set various options for the TypeScript compiler, making it easier to manage complex configurations, specify which files should be included or excluded, and enforce consistent type-checking across your codebase.
**BASICALLY WE STATE IN THIS FILE HOW WE WANT TO CONVERT OUR TS FILE TO TS**
Here's what `tsconfig.json` can help you control:
  - **Targeting JavaScript Versions**
    
    - Use the `"target"` option to specify the version of JavaScript (e.g., ES5, ES6) the TypeScript compiler should produce. This is useful for ensuring compatibility with different JavaScript environments.
- **Module System Specification**
    
    - Set the `"module"` option to control how modules are handled (e.g., CommonJS, ES6, UMD), which is critical for compatibility with different JavaScript environments and tools.
- **Type-Checking Options**
    
    - The `"strict"` option enables all strict type-checking options, such as `noImplicitAny` and `strictNullChecks`. These help enforce type safety and prevent potential runtime errors.
    - Additional options (like `"noImplicitReturns"` and `"noUnusedLocals"`) further help catch common errors.
- **Include and Exclude Files**
    
    - **"include"** and **"exclude"** options allow you to specify files or directories to include or exclude from the compilation process. This helps keep your compilation targets focused and efficient.

  

# Setting up a Typescript Nodejs Application

Let's walk through the process of setting up a simple TypeScript Node.js application locally on your machine.

  

**Step 1 - Install TypeScript Globally:**

```Shell
npm install -g typescript
```

**This command installs TypeScript globally on your machine, allowing you to use the `tsc` command anywhere.**

  

**Step 2 - Initialize a Node.js Project with TypeScript:**

```Shell
mkdir node-app
cd node-app
npm init -y
npx tsc --init
```

These commands create a new directory (`node-app`), initialize a Node.js project with default settings (`npm init -y`), and then generate a `tsconfig.json` file using `npx tsc --init`.
The `-y` flag in `npm init -y` automatically accepts all default settings in the initialization process, bypassing the interactive prompts.
The command `npx tsc --init` initializes a new TypeScript project by generating a `tsconfig.json` file, which configures the TypeScript compiler options for your project.

Here's a breakdown of each part:

- **`npx`**: Executes a package (in this case, `tsc`, the TypeScript compiler) without needing to install it globally.
- **`tsc`**: The TypeScript compiler, used to compile TypeScript files into JavaScript.
- **`--init`**: Tells `tsc` to generate a `tsconfig.json` file with default settings.

After running this command, you’ll get a `tsconfig.json` file in your project directory,

**Step 3 - Create a TypeScript File (a.ts):**

```TypeScript
// a.ts
const x: number = 1;
console.log(x);
```
->THIS IS SIMILAR TO KI JAISE MAINE LIKHA 
->const x=1 in js but ab x ka type specify kar raha huon!
  

**Step 4 - Compile the TypeScript File to JavaScript:**

```Shell
tsc -b
```

The `-b` flag tells TypeScript to build the project based on the configuration in `tsconfig.json`. This generates a JavaScript file (`index.js`) from the TypeScript source (`a.ts`).
`tsc -b` is used to **build** TypeScript projects in **"project references"** mode, which is especially useful for **monorepos** or **large codebases** with multiple TypeScript projects that depend on each other. Here’s a breakdown of what each part does:

- **`tsc`**: This is the TypeScript compiler command, used to compile `.ts` files to JavaScript.
- **`-b`** (short for `--build`): This option triggers the build mode, enabling TypeScript to build multiple projects efficiently, especially when dependencies are involved.
  

**Step 5 - Explore the Generated JavaScript File (**`**index.js**`**):**

```JavaScript
// index.js
const x = 1;
console.log(x);
```

Note that the generated JavaScript file doesn't include TypeScript-specific code. It's standard JavaScript without types.
-> The final file we always run is the javascript file!
  
![Week 9.2-20241026190248984.webp](../../../Images/Week%209.2-20241026190248984.webp)
**Step 6 - Attempt to Assign a String to a Number:**

```TypeScript
// a.ts
let x: number = 1;
x = "harkirat";
console.log(x);
```

  

**Step 7 - Try Compiling the Code Again:**

```Shell
tsc -b
```

Upon compiling, TypeScript detects the type error (`x` being assigned a string) and reports it in the console. Additionally, no `index.js` file is generated due to the type error.

  

> This example illustrates one of TypeScript's key benefits: **catching type errors at compile time. By providing static typing, TypeScript enhances code reliability and helps identify potential issues before runtime. This is particularly valuable in large codebases where early error detection can save time and prevent bugs because developers can make stupid mistakes!**

  

  

# Basic Types in Typescript

In TypeScript, basic types serve as the building blocks for defining the data types of variables. Here's an overview of some fundamental types provided by TypeScript:

  

1. **Number:**
    - Represents numeric values.
    - Example:
        
        ```TypeScript
        let age: number = 25;
        ```
        
2. **String:**
    - Represents textual data (sequences of characters).
    - Example:
        
        ```TypeScript
        let name: string = "John";
        ```
        
3. **Boolean:**
    - Represents true or false values.
    - Example:
        
        ```TypeScript
        let isStudent: boolean = true;
        ```
        
4. **Null:**
    - Represents the absence of a value.
    - Example:
        
        ```TypeScript
        let myVar: null = null;
        ```
        
5. **Undefined:**
    - Represents a variable that has been declared but not assigned a value.
    - Example:
        
        ```TypeScript
        let myVar: undefined = undefined;
        ```
        

  

  

# Problems and Code Implementation

  

## 1] **Hello World Greeting**

  

**Objective:**

Learn **how to give types to function arguments in TypeScript.**

  

**Task:**  
Write a TypeScript function named  
`greet` that takes a user's first name as an argument and logs a greeting message to the console.

  ->THE ARGUEMENT NEEDS TO HAVE A TYPE 

**Function Signature:**

```TypeScript
function greet(firstName: string): void {
    // Implementation goes here
}
```

  

**Solution:**

```TypeScript
function greet(firstName: string): void {
    console.log("Hello " + firstName);
}

// Example Usage
greet("harkirat");
```

  

**Explanation:**

1. **Function Definition (**`**function greet(firstName: string): void**`**):**
    - The `greet` function is declared with a parameter named `firstName`.
    - `: string` indicates that the `firstName` parameter must be of type string.
    - `: void` specifies that the function does not return any value.
2. **Function Body (**`**console.log("Hello " + firstName);**`**):**
    - Inside the function body, a `console.log` statement prints a greeting message to the console.
    - The message includes the provided `firstName` parameter.
3. **Function Invocation (**`**greet("harkirat");**`**):**
    - The function is called with the argument `"harkirat"`.
    - The provided argument must be a string, aligning with the specified type in the function definition.

  

> This example demonstrates the basic usage of TypeScript types in function parameters, ensuring that the expected data type is enforced and catching errors related to type mismatches during development.

  

  

## 2] **Sum Function**

  

**Objective:**

Learn **how to assign a return type to a function in TypeScript.**

  

**Task:**

Write a TypeScript function named `sum` that takes two numbers as arguments and returns their sum. Additionally, invoke the function with an example.

  

**Function Signature:**

```TypeScript
function sum(a: number, b: number): number {
    // Implementation goes here
}
```

  -> IN THIS CASE WE'RE EXPLICITLY TELLING THAT THE RETURN TYPE IS A NUMBER 

**Solution:**

```TypeScript
function sum(a: number, b: number): number {
    return a + b;
}

// Example Usage
console.log(sum(2, 3));
```

  -> Sometimes if we don't explicitly don't Tell the return type in that case we Don't like this
  ![Week 9.2-20241026193119329.webp](../../../Images/Week%209.2-20241026193119329.webp)
-> To bhi pata laga gaya TS ko ki return type toh number hai isee bolte hain type inference!
**Explanation:**

1. **Function Definition (**`**function sum(a: number, b: number): number**`**):**
    - The `sum` function is declared with two parameters, `a` and `b`, both of type number.
    - `: number` indicates that the function returns a value of type number.
2. **Function Body (**`**return a + b;**`**):**
    - Inside the function body, the sum of `a` and `b` is calculated using the `+` operator.
    - The result is then returned.
3. **Function Invocation (**`**console.log(sum(2, 3));**`**):**
    - The function is called with the arguments `2` and `3`.
    - The result is logged to the console using `console.log`.

  

> This example showcases how to specify the return type of a function in TypeScript, ensuring that the function returns the expected data type. In this case, the `sum` function returns a number.

  

## 3] **Age Verification Function**

  

**Objective:**

Understand **Type Inference in TypeScript.**

 Type inference in TypeScript is the compiler’s ability to automatically deduce types based on the code without requiring explicit type annotations. It helps streamline code by reducing the need for redundant type declarations, making code cleaner while still enforcing type safety.
  

**Task:**  
Write a TypeScript function named  
`isLegal` that takes an `age` as a parameter and returns `true` if the user is 18 or older, and `false` otherwise. Also, invoke the function with an example.

  

**Function Signature:**

```TypeScript
function isLegal(age: number): boolean {
    // Implementation goes here
}
```

  

**Solution:**

```TypeScript
function isLegal(age: number){ // Even we're not explicilty defining the returning type also!
    if (age > 18) {
        return true;
    } else {
        return false;
    }
}
let x=isLegal(23);
// HERE WE ARE NOT SPECIFYING THE TYPE OF X THAT KINDA MEANS KI AUTOMATICALLY INFERS THAT THE TYPE IS BOOLEAN
// Example Usage
console.log(x); // Output: true
```
![Week 9.2-20241026194852285.webp](../../../Images/Week%209.2-20241026194852285.webp)
  

**Explanation:**

1. **Function Definition (**`**function isLegal(age: number): boolean**`**):**
    - The `isLegal` function is declared with a parameter `age` of type number.
    - `: boolean` indicates that the function returns a boolean value.
2. **Function Body (**`**if (age > 18) {...}**`**):**
    - Inside the function body, an `if` statement checks if the provided `age` is greater than 18.
    - If true, the function returns `true`; otherwise, it returns `false`.
3. **Function Invocation (**`**console.log(isLegal(22));**`**):**
    - The function is called with the argument `22`.
    - The result (`true`) is logged to the console using `console.log`.

  

> This example demonstrates how TypeScript's type inference can be leveraged. The return type (`boolean`) is implicitly inferred based on the conditions within the function. The `isLegal` function is designed to return a boolean value indicating whether the provided age is 18 or older.

  ### **->Reduced Boilerplate Code**

- **Eliminates Redundant Annotations**: You don’t have to explicitly specify types everywhere, which reduces the amount of code you write. TypeScript automatically infers types based on the assigned values, making the code cleaner and easier to read.
    `let count = 10; // inferred as number`

## 4] **Delayed Function Execution**

  

**Objective:**

Learn to work with functions as parameters in TypeScript.

  

**Task:**  
Write a TypeScript function named  
`delayedCall` that takes another function (`fn`) as input and executes it after a delay of 1 second. Also, invoke the `delayedCall` function with an example.

  

**Function Signature:**

```TypeScript
function delayedCall(fn: () => void): void {
    // Implementation goes here
}
```

  

**Solution:**

```TypeScript
function delayedCall(fn: () => void): void {
    setTimeout(fn, 1000);
}

// Example Usage
delayedCall(function() {
    console.log("hi there");
});
```

  

**Explanation:**

1. **Function Definition (**`**function delayedCall(fn: () => void): void**`**):**
    - The `delayedCall` function is declared with a parameter `fn` of type function that takes no arguments and returns `void`.
    - `: void` indicates that the function doesn't return any value.
2. **Function Body (**`**setTimeout(fn, 1000);**`**):**
    - Inside the function body, `setTimeout` is used to delay the execution of the provided function (`fn`) by 1000 milliseconds (1 second).
3. **Function Invocation (**`**delayedCall(function() {...});**`**):**
    - The `delayedCall` function is invoked with an anonymous function as an argument.
    - The provided function logs "hi there" to the console after a 1-second delay.

  

> This example illustrates how TypeScript handles functions as first-class citizens, allowing them to be passed as arguments to other functions. The `delayedCall` function provides a way to execute a given function after a specified delay.

  

# **The** `**tsconfig.json**` **File in TypeScript**

**The `**tsconfig.json**` file in TypeScript is a configuration file that provides settings for the TypeScript compiler (`**tsc**`). It allows you to customize various aspects of the compilation process and define how your TypeScript code should be transpiled into JavaScript.**

  

Below are a bunch of options that you can change to change the compilation process in the `**tsconfig.json**` file:

  

## 1] **Target Option in** `**tsconfig.json**`**:**

The `target` option in a `tsconfig.json` file specifies the ECMAScript target version to which the TypeScript compiler (`tsc`) will compile the TypeScript code. It **allows you to define the lowest version of ECMAScript that your code should be compatible with.** Here's an explanation and example usage:

  

- **ES5 (ECMAScript 5):**
    - When `target` is set to `"es5"`, the TypeScript compiler generates code compatible with ECMAScript 5, which is widely supported across browsers.
    - Example:
        
        ```JSON
        {
          "compilerOptions": {
            "target": "es5",
            // Other options...
          }
        }
        ```
        
    - TypeScript Code:
        
        ```TypeScript
        const greet = (name: string) => `Hello, ${name}!`;
        ```
        
    - Output:
        
        ```JavaScript
        "use strict";
        var greet = function (name) { return "Hello, ".concat(name, "!"); };
        ```
        

  

- **ES2020 (ECMAScript 2020):**
    - When `target` is set to `"es2020"`, the TypeScript compiler generates code compatible with ECMAScript 2020, incorporating the latest features.
    - Example:
        
        ```JSON
        {
          "compilerOptions": {
            "target": "es2020",
            // Other options...
          }
        }
        ```
        
    - TypeScript Code:
        
        ```TypeScript
        const greet = (name: string) => `Hello, ${name}!`;
        ```
        
    - Output:
        
        ```JavaScript
        "use strict";
        const greet = (name) => `Hello, ${name}!`;
        ```
        

  

> By setting the `target` option, you ensure that the generated JavaScript code adheres to the specified ECMAScript version, allowing you to control the level of compatibility and take advantage of the features available in newer ECMAScript versions.

  

## **2]** `**rootDir:**`

- The `rootDir` option in a `tsconfig.json` file specifies the root directory where the TypeScript compiler (`tsc`) should look for `.ts` files.
- It is considered a good practice to set `rootDir` to the source folder (`src`), indicating the starting point for TypeScript file discovery.

  

- Example:
    
    ```JSON
    {
      "compilerOptions": {
        "rootDir": "src",
        // Other options...
      }
    }
    ```
    

  

## 3**]** `**outDir**`

- The `outDir` option defines the output directory where the TypeScript compiler will place the generated `.js` files.
- It determines the structure of the output directory relative to the `rootDir`.
-  It is considered a good practice to set `outDir` to the dist/build folder (`dist`), indicating the point where all the javascript files are stored!
-> WE ALWAYS IGNORE THE DIST FOLDER LIKE THE NODE MODULES
-> We never push these js files to github!

  

- Example:
    
    ```JSON
    {
      "compilerOptions": {
        "outDir": "dist",
        // Other options...
      }
    }
    ```
    

  

> If `rootDir` is set to `"src"` and `outDir` is set to `"dist"`, the compiled files will be placed in the `dist` folder, mirroring the structure of the `src` folder.



## 4] `**noImplicitAny**`

- The `noImplicitAny` option in a `tsconfig.json` file determines whether TypeScript should issue an error when it encounters a variable with an implicit `any` type.
- **Enabled (**`**"noImplicitAny": true**`**):**
    
    ```JSON
    {
      "compilerOptions": {
        "noImplicitAny": true,
        // Other options...
      }
    }
    ```
    
    Example:
    
    ```TypeScript
    // Compilation Error: Implicit any type
    const greet = (name) => `Hello, ${name}!`;
    ```
    

  

- **Disabled (**`**"noImplicitAny": false**`**):**
    
    ```JSON
    {
      "compilerOptions": {
        "noImplicitAny": false,
        // Other options...
      }
    }
    ```
    
    No error will be issued for implicit `any` types.
    

  

## 5] `**removeComments**`

- The `removeComments` option in a `tsconfig.json` file determines whether comments should be included in the final JavaScript output.
- **Enabled (**`**"removeComments": true**`**):**
    
    ```JSON
    {
      "compilerOptions": {
        "removeComments": true,
        // Other options...
      }
    }
    ```
    
    Comments will be stripped from the generated JavaScript files.
    

  

- **Disabled (**`**"removeComments": false**`**):**
    
    ```JSON
    {
      "compilerOptions": {
        "removeComments": false,
        // Other options...
      }
    }
    ```
    
    Comments will be retained in the generated JavaScript files.
    

  

> These options provide flexibility and control over the compilation process, allowing you to structure your project and handle type-related scenarios according to your preferences.

  

  

# Interfaces

In TypeScript, an interface is a way to define a contract for the shape of an object. It allows you to specify the expected properties, their types, and whether they are optional or required. Interfaces are powerful tools for enforcing a specific structure in your code.
TypeScript, interfaces are not limited to just objects. While they’re commonly used to define the structure of object types, they can be applied more broadly to define shapes for various types,
 
### 1. **Object Types**

- Interfaces can define the shape of objects, specifying what properties they should have and their types.

```typescript
interface Person {
    name: string;
    age: number;
}
const user: Person = { name: "Alice", age: 25 };

```



### 2. **Function Types**

- Interfaces can define the type of a function, specifying parameters and return types.


```typescript
interface Greet {
    (name: string): string;
}
const sayHello: Greet = (name) => `Hello, ${name}!`;
```


### 3. **Array Types**

- Interfaces can describe the structure of an array, including the types of elements it contains.


```typescript
interface StringArray {
    [index: number]: string;
}
const colors: StringArray = ["red", "green", "blue"];
```



### 4. **Class Types**

- Interfaces can be used to define types for classes, describing methods and properties that the class must implement.

```typescript
interface Animal {
    name: string;
    speak(): void;
}
class Dog implements Animal {
    name = "Dog";
    speak() {
        console.log("Woof!");
    }
}
```



### 5. **Hybrid Types**

- Interfaces can define "hybrid" types that combine function and object properties, often used in complex APIs.


```typescript
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}
const getCounter = (): Counter => {
    const counter = ((start: number) => `Starting at ${start}`) as Counter;
    counter.interval = 1000;
    counter.reset = () => console.log("Reset!");
    return counter;
};
const counter = getCounter();
counter(10);
counter.reset();
counter.interval = 500;

```


-> BASICALLY WE'RE DEFINING THE TYPE OF OBJECT HERE 
-> INTERFACES ARE NOT EVEN PRESENT IN THE FINAL JS FILE WE ONLY USE THEM TO GET THE COMPILE TIME ERRORS!
## Understanding Interfaces

Suppose you have an object representing a user:

```TypeScript
const user = {
  firstName: "harkirat",
  lastName: "singh",
  email: "email@gmail.com",
  age: 21,
};
```

To assign a type to the `user` object using an interface, you can create an interface named `User`:

```TypeScript
interface User {
  firstName: string;
  lastName: string;
  email: string;
  age: number;
}
```

Now, you can explicitly specify that the `user` object adheres to the `User` interface:

```TypeScript
const user: User = {
  firstName: "harkirat",
  lastName: "singh",
  email: "email@gmail.com",
  age: 21,
};
```

  

**Explanation:**

1. **Interface Declaration (**`**interface User**`**):**
    - The `interface` keyword is used to declare an interface named `User`.
    - Inside the interface, you define the expected properties (`firstName`, `lastName`, `email`, `age`) along with their types.
2. **Assigning Type to Object (**`**const user: User = { /* ... */ };**`**):**
    - By stating `const user: User`, you are explicitly indicating that the `user` object must adhere to the structure defined by the `User` interface.
    - If the `user` object deviates from the defined structure or misses any required property, TypeScript will raise a compilation error.

  

  

### Assignment 1

  

Problem: Create a function `isLegal` that returns true or false if a user is above 18. It takes a user as an input.

  

Solution:

```TypeScript
// Define an interface to specify the structure of a user object
interface User {
  firstName: string;
  lastName: string;
  email: string;
  age: number;
}

// Create a function 'isLegal' that checks if a user is above 18
function isLegal(user: User): boolean {
    // Check if the user's age is greater than 18
    if (user.age > 18) {
        return true; // Return true if the user is legal
    } else {
        return false; // Return false if the user is not legal
    }
}
```

  

**Code Explanation:**

- An interface "User" is defined to enforce the structure of a user object with properties: firstName, lastName, email, and age.
- The function "isLegal" takes a user object as input and checks if the user's age is greater than 18.
- It returns true if the user is legal (age > 18) and false otherwise.

  

### Assignment 2

  

Problem: Create a React component that takes todos as an input and renders them.

  

Solution:

```TypeScript
// Define an interface to specify the structure of a todo object
interface TodoType {
  title: string;
  description: string;
  done: boolean;
}

// Define the input prop for the Todo component
interface TodoInput {
  todo: TodoType;
}

// Create a React component 'Todo' that takes a 'todo' prop and renders it
function Todo({ todo }: TodoInput): JSX.Element {
  return (
    <div>
      <h1>{todo.title}</h1>
      <h2>{todo.description}</h2>
      {/* Additional rendering logic can be added for other properties */}
    </div>
  );
}
```

  

**Code Explanation:**

- An interface "TodoType" is defined to specify the structure of a todo with properties: title, description, and done.
- An interface "TodoInput" is defined to specify the input prop for the Todo component.
- The React component "Todo" takes a prop "todo" of type "TodoType" and renders its properties (title and description).

  

  

## Implementing Interfaces

In TypeScript, you can implement interfaces using classes. This provides a way to define a blueprint for the structure and behavior of a class. Let's take an example:
ONLY IF THERE IS COMMANLITY BETWEEN TWO ITEMS THEN ISKA USE KARENGE 
Assume you have a `Person` interface:

```TypeScript
interface Person {
    name: string;
    age: number;
    greet(phrase: string): void;
}
```

Now, you can create a class that adheres to this interface:

```TypeScript
class Employee implements Person {
    name: string;
    age: number;

    constructor(n: string, a: number) {
        this.name = n;
        this.age = a;
    }

    greet(phrase: string) {
        console.log(`${phrase} ${this.name}`);
    }// Now whoever is writing the Employee class will be forced to write the greet function because the class is implementing Person interface
}
```

Here's what's happening:

- The `Employee` class implements the `Person` interface.
- It has properties (`name` and `age`) matching the structure defined in the interface.
- The `greet` method is implemented as required by the interface.

  

> This approach is handy when creating various types of persons (like Manager, CEO), ensuring they all adhere to the same interface contract. It maintains consistency in the structure and behavior across different classes.

  

  

# Types

In TypeScript, **types** allow you to aggregate data together in a manner very similar to interfaces. They provide a way to define the structure of an object, similar to how interfaces do. Here's an example:

-> YAHAN = KA USE HOTA HAI YE BAT DHYAN RAKHNA
  

```TypeScript
type User = {
    firstName: string;
    lastName: string;
    age: number;
};
```

### Features

1. **Unions:**  
    Unions allow you to define a type that can be one of several types. This is useful when dealing with values that could have different types. For instance, imagine you want to print the ID of a user, which can be either a number or a string:  
    
    ```TypeScript
    type StringOrNumber = string | number;
    
    function printId(id: StringOrNumber) {
      console.log(`ID: ${id}`);
    }
    
    printId(101);     // ID: 101
    printId("202");   // ID: 202
    ```
    
    Unions provide flexibility in handling different types within a single type definition.
    
![Week 9.2-20241027095412927.webp](../../../Images/Week%209.2-20241027095412927.webp)

  

1. **Intersection:**  
    Intersections allow you to create a type that has every property of multiple types or interfaces. If you have types like  
    `Employee` and `Manager`, and you want to create a `TeamLead` type that combines properties of both:
    In TypeScript, you can take the intersection between a type and an interface
    ```TypeScript
    type Employee = {
      name: string;
      startDate: Date;
    };
    
    type Manager = {
      name: string;
      department: string;
    };
    
    type TeamLead = Employee & Manager;
    
    const teamLead: TeamLead = {
      name: "harkirat",
      startDate: new Date(),
      department: "Software Developer"
    };
    ```
    
    Intersections provide a way to create a new type that inherits properties from multiple existing types.
    

  

> In summary, while types and interfaces are similar in defining object structures, types in TypeScript offer additional features like unions and intersections, making them more versatile in certain scenarios.

  

# Interfaces vs Types

  

## Major Differences

### 1. **Declaration Syntax:**

- **Type:**
    - Uses the `type` keyword.
    - More flexible syntax, can represent primitive types, unions, intersections, and more.
- **Interface:**
    - Uses the `interface` keyword.
    - Typically used for defining the structure of objects.

### **2. Extension and Merging:**

- **Type:**
    - Supports extending types.
    - Can't be merged; if you define another type with the same name, it will override the previous one.
- **Interface:**
    - Supports extending interfaces using the `extends` keyword.
    - Automatically merges with the same-name interfaces, combining their declarations.

### 3. **Declaration vs. Implementation:**

- **Type:**
    - Can represent any type, including primitives, unions, intersections, etc.
    - Suitable for describing the shape of data.
- **Interface:**
    - Mainly used for describing the shape of objects.
    - Can also be used to define contracts for classes.

  

## Other Differences

- **Type Overriding:**
    - Types cannot be overridden or merged. Redefining a type with the same name replaces the previous one.
    - Interfaces automatically merge if declared with the same name.
- **Object Literal Strictness:**
    - Types are more lenient when dealing with object literal assignments.
    - Interfaces enforce strict object literal shapes.
- **Implementation for Classes:**
    - Interfaces can be used to define contracts for class implementations.
    - Types are more versatile for creating complex types and reusable utility types.

  

## When to Use Which

- **Use Types:**
    - For advanced scenarios requiring union types, intersections, or mapped types.
    - When dealing with primitive types, tuples, or non-object-related types.
    - Creating utility types using advanced features like conditional types.
- **Use Interfaces:**
    - When defining the structure of objects or contracts for class implementations.
    - Extending or implementing other interfaces.
    - When consistency in object shape is a priority.

  

## Examples

  

**Type Example:**

```TypeScript
type StringOrNumber = string | number;

function printId(id: StringOrNumber) {
  console.log(`ID: ${id}`);
}

printId(101);       // ID: 101
printId("202");     // ID: 202
```

  

**Interface Example:**

```TypeScript
interface Employee {
  name: string;
  startDate: Date;
}

interface Manager {
  name: string;
  department: string;
}

type TeamLead = Employee & Manager;

const teamLead: TeamLead = {
  name: "Harkirat",
  startDate: new Date(),
  department: "Software Developer",
};
```

  

> In summary, choose types for flexibility and advanced type features, and use interfaces for object shapes, contracts, and class implementations, ensuring a consistent and readable codebase.


![Week 9.2-20241027075038825.webp](../../../Images/Week%209.2-20241027075038825.webp)
![Week 9.2-20241027075056525.webp](../../../Images/Week%209.2-20241027075056525.webp)
![Week 9.2-20241027075136301.webp](../../../Images/Week%209.2-20241027075136301.webp)

-> ![Week 9.2-20241027090944366.webp](../../../Images/Week%209.2-20241027090944366.webp)
Well Typescript Should never go to your production code!
![Week 9.2-20241027091108309.webp](../../../Images/Week%209.2-20241027091108309.webp)
It's better to use any here since We won't know the type of the error!
![Week 9.2-20241027091245221.webp](../../../Images/Week%209.2-20241027091245221.webp)
![Week 9.2-20241027091314153.webp](../../../Images/Week%209.2-20241027091314153.webp)


# ENUMS 
![Week 9.2-20241027095007496.webp](../../../Images/Week%209.2-20241027095007496.webp)
![Week 9.2-20241027095105209.webp](../../../Images/Week%209.2-20241027095105209.webp)
![Week 9.2-20241027095522640.webp](../../../Images/Week%209.2-20241027095522640.webp)
BETTER WAY TO DO THIS IN A MORE HUMAN READABLE FORM IS USING ENUM 
![Week 9.2-20241027095737110.webp](../../../Images/Week%209.2-20241027095737110.webp)
In TypeScript, an **enum** (short for "enumeration") is a feature that allows you to define a set of named constants, making your code more readable and maintainable. Enums are used when you have a set of related values that represent specific, limited options. They help by giving these values human-readable names, making code more descriptive and reducing the likelihood of errors.



```typescript
enum Direction{
    left,  //0
    right, //1
    up,    //2
    down   //3
}


function doSomething(keypressed:Direction){
    if(keypressed==Direction.left){

    }else if (keypressed==Direction.right){

    }
}

doSomething(Direction.left);
doSomething(Direction.right);
```
![Week 9.2-20241027101802109.webp](../../../Images/Week%209.2-20241027101802109.webp)


JS FILE CODE 

```typescript
"use strict";
var Direction;
(function (Direction) {
    Direction[Direction["left"] = 0] = "left";
    Direction[Direction["right"] = 1] = "right";
    Direction[Direction["up"] = 2] = "up";
    Direction[Direction["down"] = 3] = "down";
})(Direction || (Direction = {}));
function doSomething(keypressed) {
    if (keypressed == Direction.left) {
    }
    else if (keypressed == Direction.right) {
    }
}
doSomething(Direction.left);
doSomething(Direction.right);
```
ENUM AS AN KEYWORD DOESN'T GO INTO THE JAVASCRIPT FILE
![Week 9.2-20241027102219063.webp](../../../Images/Week%209.2-20241027102219063.webp)


```typescript
enum Direction{
    left="left",//10 agar ek number hi diya toh in that case by default sabmein counting aage badh jaegi and then right mein 11 , up mein 12, down mein 13 aa jayega
    right="right",
    up="up",
    down="down"
}

```
![Week 9.2-20241027102436383.webp](../../../Images/Week%209.2-20241027102436383.webp)
![Week 9.2-20241027102534752.webp](../../../Images/Week%209.2-20241027102534752.webp)

# GENERICS(REVISE)

![Week 9.2-20241027102826862.webp](../../../Images/Week%209.2-20241027102826862.webp)
Generics in TypeScript provide a way to create reusable, flexible, and type-safe components by allowing you to specify types as parameters. Generics let you write functions, interfaces, classes, and other structures that work with any type, while still enforcing type constraints. They’re especially useful when you want to apply the same functionality to different types without sacrificing type safety.

### Why Use Generics?

Generics help to avoid `any` types and give your code more flexibility. For example, without generics, you might have to write separate functions to handle different types, or use `any`, which sacrifices type safety.


```typescript
type input=string|number;

function firstEl(arr:input[]){
    return arr[0];
}

const val=firstEl(["as","asd","asdf"]);
//val.toUpperCase()->THIS WON'T WORK BECAUSE VAL KA TYPE INPUT HAI NAKI STRING


```
![Week 9.2-20241027105038598.webp](../../../Images/Week%209.2-20241027105038598.webp)
Now Here the type of val should be string right but it's not doing inference and just showing the type as input!

![Week 9.2-20241027105212756.webp](../../../Images/Week%209.2-20241027105212756.webp)

We also don't want someone to do this right!
![Week 9.2-20241027105250549.webp](../../../Images/Week%209.2-20241027105250549.webp)
Toh we can do this 

THIS MEAN THE IDENTITY CAN BE CALLED WITH ANYTHING T REPRESENTS A GENERIC VALUE HERE
![Week 9.2-20241027105521735.webp](../../../Images/Week%209.2-20241027105521735.webp)
 THIS IS SAME AS DOING THIS 
 ![Week 9.2-20241027105804277.webp](../../../Images/Week%209.2-20241027105804277.webp)
 ![Week 9.2-20241027110024528.webp](../../../Images/Week%209.2-20241027110024528.webp)

![Week 9.2-20241027110319105.webp](../../../Images/Week%209.2-20241027110319105.webp)



![Week 9.2-20241027110618530.webp](../../../Images/Week%209.2-20241027110618530.webp)