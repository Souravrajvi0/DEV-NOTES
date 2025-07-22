---
view-count: 4
---
- In Node.js and npm (Node Package Manager) projects, dependencies are categorized into two main types: regular dependencies and development dependencies.

1. **Regular Dependencies**:
    - Regular dependencies, sometimes referred to as production dependencies, are the packages that your project needs to run in a production environment.
    - These dependencies are essential for the functioning of your application and are typically packages that your application relies on to provide its core features and functionality.
    - Examples of regular dependencies include libraries, frameworks, and utilities that your application directly uses to fulfill its intended purpose.
2. **Development Dependencies**:
    
    - Development dependencies are packages that are only needed during the development process and are not required for the application to run in a production environment.
    - These dependencies are used for tasks such as testing, building, linting, formatting, and other development-related activities.
    - Examples of development dependencies include testing frameworks, build tools, code linters, and other utilities that facilitate the development workflow but are not part of the final deployed application.

→Scripts are there to make things easy for us!

![Untitled 64.png](../../Images/Untitled%2064.png)

→By Doing this in package.json we no longer have to use this

![Untitled 1 54.png](../../Images/Untitled%201%2054.png)

→Now we can do this instead of doing the above code

![Untitled 2 41.png](../../Images/Untitled%202%2041.png)

![Untitled 3 37.png](../../Images/Untitled%203%2037.png)
-> HOW TO RUN THESE SCRIPTS-> NPM RUN (NAME OF THE SCRIPT)
→We can even do **npm start because start is a keyword reserved by the NPM**
→Won’t work for npm run build
-> BHAI YAHAN PAR NPX MAT LIKHNA NPM LIKHNA WHILE RUNNING A SCRIPT
→In the  `**scripts**` field of the `**package.json**` file, you can define custom scripts that you can run using npm or yarn commands. These scripts can perform various tasks related to your project, such as starting a development server, running tests, building your project for production, and more.  
  

```JavaScript
"scripts": {
"start": "command_to_start_your_development_server",
"build": "command_to_build_your_project_for_production",
"test": "command_to_run_tests"
// Add more scripts as needed
}
```

---






`**react**` and `**react-dom**` are two separate packages that serve different purposes, but they are closely related and are both part of the React ecosystem.

1. **React (**`**react**`**)**:
    - The `**react**` package is the core library for building user interfaces with React.
    - It provides the functionality for creating and managing React components, handling component lifecycles, managing state and props, and rendering components to the DOM.
    - When you write React code, you import components and APIs from the `**react**` package to define your UI and its behavior.
2. **React DOM (**`**react-dom**`**)**:
    - The `**react-dom**` package provides DOM-specific methods that are not available in the core React library.
    - It includes methods for rendering React components to the DOM, hydrating server-rendered markup, and interacting with the browser's DOM.
    - `**react-dom**` is typically used in web applications where you want to render React components into the browser's DOM.
    - When building web applications with React, you typically import methods like `**ReactDOM.render()**` from the `**react-dom**` package to mount your React components into the DOM.

![Untitled 4 34.png](../../Images/Untitled%204%2034.png)
-> Here heading is a JavaScript object or react element not a html element but when we render this object into the DOM this Becomes the part of the html!
→This is not a very developer friendly way to create react elements. How To solve this? Well
->Facebook developers made JSX
**JSX IS NOT PART OF REACT**
**WE CAN WRITE REACT WITHOUT JSX!**
**JSX IS NOT HTML WRITTEN INSIDE JS FILE**
**JSX Has like HTML SYNTAX**
**JSX IS JUST A SYNTAX**
![Untitled 5 29.png](../../Images/Untitled%205%2029.png)

----
→Creation of React element using JSX

```JavaScript
const element = <h1 className="greeting">Hello, world!</h1>;

```

`**element**` is a variable that holds a React element. The React element itself is the JavaScript object that this JSX syntax compiles down to.

![Untitled 7 23.png](../../Images/Untitled%207%2023.png)
→The creation of both results in the same type of React element like literally the same object!
→So It’s better not to use React.createElement()

![Untitled 8 20.png](../../Images/Untitled%208%2020.png)
->JavaScript engine won’t understand this code! Because this is not valid pure JavaScript!

**HERE COME PARCEL IN THE PLAY**

->so every time we write JSX code, Then it is transpiled to javascript before it goes to The browser/js engine!

→Even Root.render() Won’t understand Jsxheading! So before that it’s transpiled by Parcel which acts as a manager that gives this task to the package called “Babel” which in turns transpiles our code that react can understand

1. **Writing JSX**: In your React code, you write JSX syntax, which is a syntax extension for JavaScript that allows you to write HTML-like code within your JavaScript files. JSX makes it easier to write and reason about React components.
2. **Bundling with Parcel**: When you run your project through Parcel, it analyzes your code and determines all the dependencies, including JSX files. Parcel is a bundler that automatically handles the configuration needed for your project, including transpiling JSX to JavaScript.
3. **Transpilation with Babel**: Parcel, by default, uses Babel as its JavaScript compiler. Babel is a popular tool for transforming modern JavaScript syntax, including JSX, into code that is compatible with older browsers or environments that don't yet support these features.
4. **JSX to JavaScript**: Babel transforms JSX syntax into regular JavaScript function calls. For example, a JSX element like `**<Heading />**` might be transformed into a `**React.createElement**` call like `**React.createElement(Heading, null)**`.
5. **React's Understanding**: After Babel transpiles JSX into regular JavaScript, React can then understand and work with the resulting JavaScript code. This includes rendering components using `**ReactDOM.render()**`

---

## How babel Works?

Babel is a JavaScript compiler that is widely used for transforming modern JavaScript syntax into older versions of JavaScript that can be executed in environments that do not support newer syntax features. Here's how Babel transforms JSX into JavaScript:

1. **Parsing**: Babel starts by parsing the input code (which may include JSX syntax) into an abstract syntax tree (AST). This step involves breaking down the code into its individual elements and representing them as a structured tree.
2. **Transforming JSX**: Once the code is parsed, Babel identifies JSX syntax within the AST. JSX elements are represented as function calls to `**React.createElement()**`. For example, a JSX element `**<Heading />**` might be transformed into a `**React.createElement()**` call like `**React.createElement(Heading, null**`

3. **Applying Plugins and Presets**: Babel uses plugins and presets to customize the transformation process. Plugins like `**@babel/plugin-transform-react-jsx**` handle JSX transformation, while presets like `**@babel/preset-react**` bundle commonly use plugins for React development.  
4. **Generating Output**: Babel generates JavaScript code based on the modified AST, ensuring compatibility with older JavaScript versions. This output code can be executed in various environments.  
5. **Optimizations**: Babel may apply additional optimizations to the generated code, such as minimizing size and improving performance, based on configuration and plugins used.

![Untitled 9 15.png](../../Images/Untitled%209%2015.png)

![Untitled 10 14.png](../../Images/Untitled%2010%2014.png)

---

## **JSX VS HTML**

![Untitled 11 12.png](../../Images/Untitled%2011%2012.png)

In HTML we write class=”head” while In JSX we write ClassName_**(CAMEL CASE)**_=”Head”

So if we give attributes In JSX WE NEED TO WRITE EM IN CAMEL CASE

`**className**` **vs** `**class**`

- In HTML, the attribute to specify CSS classes is `**class**`.
- In JSX, to avoid conflict with the JavaScript `**class**` keyword, you use `**className**` instead of `**class**`
-> Yahan N capital hota hai!
`**htmlFor**` **vs** `**for**`

- In HTML, the attribute to associate a label with a form control is `**for**`.
- In JSX, to avoid conflict with the JavaScript `**for**` loop keyword, you use `**htmlFor**` instead of `**for**`.

---
## **Single line and Multiple Line:**

![Untitled 12 10.png](../../Images/Untitled%2012%2010.png)
Single line mein koi dikkat nahi hoti hai
But if we want to code in multiple line then we have to use () brackets, Since babel needs to understand Where JSX code is starting and ending
![Untitled 13 6.png](../../Images/Untitled%2013%206.png)

---

# **REACT COMPONENTS**

![Untitled 14 4.png](../../Images/Untitled%2014%204.png)

→React Functional Component is just a normal JS function that returns some piece of JSX
-> Ek bat ye Dhyan rakhni hai ki kuch alag se treat mat kar isko in the end Basic JS hi hai just usmein kya kehte hain ki kuch JSX return Ho raha hai, Return Se pehle toh full JS hi hota hai!
**→So Anytime we’re creating a new Functional Component or React Component Name it starting with a capital Letter!**

![Untitled 15 3.png](../../Images/Untitled%2015%203.png)

![Untitled 16 3.png](../../Images/Untitled%2016%203.png)

Both these functions are same

![Untitled 17 3.png](../../Images/Untitled%2017%203.png)

→Since we know arrow function mein agar ek hi statement hota hai toh return statement nahi lagana padta hai

→The same can be done With the functional Statement also

![Untitled 18 3.png](../../Images/Untitled%2018%203.png)

Both are same // we can skip on the curly braces! and then we don’t even have to use return

In React functional components, you typically use parentheses `**()**` when returning JSX code if the JSX spans multiple lines. If the JSX fits on a single line, you can use curly braces `**{}**`.
![Episode 03 - Laying the foundation-20241027160004646.webp](../../Images/Episode%2003%20-%20Laying%20the%20foundation-20241027160004646.webp)
  -> DHYAN DENA WHEN USING {} WE have to use the return statement to return it 
Here's when to use each:

1. **Parentheses** `**()**`:
    - Use parentheses when the JSX spans multiple lines for better readability and maintainability.
    - This is particularly useful when you have multiple nested elements or when you're returning JSX with conditional logic.
    - No need to write return statement
    ```JavaScript

    const MyComponent = () => (
      <div>
        <h1>Hello</h1>
        <p>World</p>
      </div>
    );
    ```
2. **Curly Braces** `**{}**`:
    - Use curly braces when the JSX fits on a single line, especially for concise JSX expressions.
    - This is common when returning a single element or when the JSX is short and simple.
    ```JavaScript

    const MyComponent = () => {
    return <div>Hello World</div>
    };
    or 
    const MyComponent = () => <div>Hello World</div>;
    ```

**In general, the choice between parentheses and curly braces depends on the complexity and length of the JSX you're returning. It's more of a stylistic preference, but using parentheses for multiline JSX and curly braces for single-line JSX is a common convention in the React community for better readability**

→In React, when you define a functional component using an arrow function with parentheses `**()**`, and you directly return JSX within those parentheses, you don't need to use the `**return**` keyword explicitly. This is called an implicit return.
->In React, when you wrap JSX in parentheses, JavaScript treats the entire JSX block as a single expression. Since an arrow function with an implicit return automatically returns that expression, the JSX is returned without needing `return`.
So, in your example:

```JavaScript
jsxCopy code
const MyComponent = () => (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div> <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);
```

In React functional components, you typically use the `**return**` statement explicitly in two main scenarios:

1. **Returning a Single Expression**:
    
    - If your component's JSX expression spans multiple lines and you're not using parentheses `**()**` to wrap it, you need to use the `**return**` statement to return the JSX explicitly.
    
    Example:
    
    ```JavaScript
    jsxCopy code
    const MyComponent = () => {
      return (
        <div>
          <h1>Hello</h1>
          <p>World</p>
        </div>
      );
    };
    
    ```
    
2. **Returning a Value Conditionally**:
    
    - If your component needs to conditionally return different JSX based on certain conditions, you use the `**return**` statement along with conditional logic.
    
    Example:
    
    ```JavaScript
    jsxCopy code
    const MyComponent = ({ isLoggedIn }) => {
      if (isLoggedIn) {
        return <p>Welcome back!</p>;
      } else {
        return <p>Please log in.</p>;
      }
    };
    
    ```
    

In both of these scenarios, the `**return**` statement explicitly specifies the value that the component should return. It's used to define what JSX should be rendered by the component.

However, if your component consists of a single expression that fits on a single line, you can use implicit return without the `**return**` keyword. In such cases, you can omit the curly braces `**{}**` and the `**return**` statement, and simply return the JSX expression directly from the arrow function.

→Yes, when you use a **normal function** declaration instead of an arrow function in React functional components, you need to use the `**return**` statement explicitly to return the JSX expression.
In React, functional components can also be defined using regular function declarations instead of arrow functions. In this case, the `**return**` statement is necessary to specify what value the component should return, just like in regular JavaScript functions

---

**Difference Between React element and React functional component**

![Untitled 19 3.png](../../Images/Untitled%2019%203.png)

1. A React **functional component** is a JavaScript function that returns a React element.

2. A **React element**t is a lightweight representation of a DOM element or a user-defined component in the React virtual DOM.
- React elements are typically **created using JSX syntax or** `**React.createElement()**` function.

**→Now There is a difference When We render the react elements and React Functional Components**

![Untitled 20 3.png](../../Images/Untitled%2020%203.png)

The correct way to render React functional components!

---
## Component Composition

![Untitled 21 3.png](../../Images/Untitled%2021%203.png)

→This will just replace the JSX Code of title in Heading component where <Title/> is written. This is called **Component Composition** putting Component into a component

---

**But why do I need to write Arrow Functions here? Well I can write normal functions also**

![Untitled 22 3.png](../../Images/Untitled%2022%203.png)
-> So while using normal function we need to explicitly add return keyword while returning a piece of JSX and Keep it in Mind that if the JSX is single line we don't need () and if it's multiline we need ()
→But arrow functions is Industry Standard

---

## JSX AND JAVASCRIPT

→In JSX, you can embed JavaScript expressions and statements directly within curly braces{}
→This allows you to dynamically generate content, compute values, or execute functions within your JSX code.
→Basically ek trike se humne HTML ko dynamic bna diya hai!

```JavaScript
const name = "John";
const element = <h1>Hello, {name}!</h1>;
---
const isLoggedIn = true;
const element = (
  <div>
    {isLoggedIn ? <p>User is logged in.</p> : <p>User is not logged in.</p>}
  </div>
);
----
function greet(name) {
  return `Hello, ${name}!`;
}

const element = <p>{greet("John")}</p>;
```

  

---

**How to pass a React element in a functional component?**

->Since we know react component is just a variable we can use it with the help of {}

![Untitled 23 3.png](../../Images/Untitled%2023%203.png)

→Since Title is normal JS variable So it can be written in {} while writing some other piece of code!
So we can Compose Anything Inside anything! That’s what is the beauty of react!
-> WE CAN ALSO RENDER A FUNCTIONAL COMPONENT LIKE THIS
![Untitled 24 3.png](../../Images/Untitled%2024%203.png)
-> ANOTHER WAY TO RENDER FUNCTIONAL COMPONENT 
![Untitled 25 3.png](../../Images/Untitled%2025%203.png)

-> What if It's a bad api!
![Episode 03 - Laying the foundation-20241027164404436.webp](../../Images/Episode%2003%20-%20Laying%20the%20foundation-20241027164404436.webp)
Yes, JSX (not JS) and the React library provide some built-in protections against cross-site scripting (XSS) attacks when we write {}!