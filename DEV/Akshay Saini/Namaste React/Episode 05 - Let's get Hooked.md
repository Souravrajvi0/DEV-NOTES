---
view-count: 5
---
-> Anything That is done by React Can also be done using JS
-> Beauty of framework/Library Makes our Developer Experience Easy
**→We need to make separate files for separate components!**

→We keep all our code in SRC FOLDER

![Untitled 66.png](../../Images/Untitled%2066.png)

**-> SEPERATE COMPONENTS SHOULD HAVE SEPERATE FILES**
**->Component Name and their file name should be kept same! Normal Convention**

->Industry Standard ye hai ki app ek component folder bnao usmein respective components ka code likho!

![Untitled 1 56.png](../../Images/Untitled%201%2056.png)

----

->Even File Extension .jsx can be used
-> .js bhi chl jata hai
→both will work!

![Untitled 2 43.png](../../Images/Untitled%202%2043.png)

---

->**PEHLE EXPORT KA SOCHO FIR IMPORT KA**

In React, there are two primary ways to export components: default export and named export

**Default Export**:
YE THODA SIMPLE HOTA HAI!
- With default export, you export a single component or value from a file. When importing a default export, you can use any name for the imported component.
- A module can’t have multiple default exports!

![Untitled 3 39.png](../../Images/Untitled%203%2039.png)

```JavaScript
import React from 'react';
const MyComponent = () => {
return <div>Hello, I am a default export component.</div>;
};
export default MyComponent;
// export default (Name of the component)
//Yes, you can use an alias while importing MyComponent in App.js. This can be 
//particularly useful if you want to avoid potential naming conflicts or if you
// prefer a different name for the component in the current module
//import React from 'react';
//import MyComponentAlias from './MyComponent';. 
```

  

```JavaScript
// App.js
import React from 'react';
import MyComponent from './MyComponent';
// import using the path of the file! // Yahan par ./MyComponent.js likhne mein koi prob nahi hai
const App = () => {
return <MyComponent />;
}
export default App;
```

**Named Export**:

- With named export, you can export multiple components or values from a file. When importing named exports, you use the exact name specified in the export statement.
- In a single file when we have to export multiple things we use this

```JavaScript
// FirstComponent.js
import React from 'react';

export const FirstComponent = () => {
  return <div>Hello, I am the first named export component.</div>;
};

export const SecondComponent = () => {
  return <div>Hello, I am the second named export component.</div>;
};
```

![Untitled 4 36.png](../../Images/Untitled%204%2036.png)

->While importing There will be slight difference
![Untitled 5 31.png](../../Images/Untitled%205%2031.png)
-> BASICALLY YE DESTRUCTURING HI HAI BHAI
->Named Export is imported like this!
![Untitled 6 29.png](../../Images/Untitled%206%2029.png)

  

---

**→Always Export First and then Import!**

→We can Import and export anywhere

→Never put the hardcoded data in the App files

→Hardcoded Data ko utils (Source folder k andar naya folder) usmein constant name ki file banano! and usmein dal do!

→We cannot use a default export with a named import directly in a single import statement. The default export and named export are separate concepts in JavaScript modules and have different import syntaxes.

---

Click Handlers in JS→

![Untitled 7 25.png](../../Images/Untitled%207%2025.png)

→OnClick attribute hai na wo ek Callback function lega!
-> And Since wo callback hai meaning JS CODE toh vo toh {} K andar aega!


```javascript
const Body=()=>{
    let resturantList=resList;
    return (
        <div className="body">
            <div className="filter">
                <button className="filter-btn" onClick={()=>{
                    resturantList=resturantList.filter(
                     (res)=>res.info.avgRating >4.5 
                    )
                    console.log(resturantList);
                    }}>Top Rated Resturants</button>
            </div>
            <div className="res-container">    
            {
              resturantList.map((resturant,index)=><RestaurantCard key={index} resdata={resturant}/>)
            }

            </div>
        </div>
    )
}

```

->Now Here we're Trying to change the restaurant list based on some specific filter and We will change it , atleast the value of the Variable but the changes won't be shown in the UI?? BUT WHY
![815](../../Images/Episode%2005%20-%20Let's%20get%20Hooked-20241028074752594.webp)


-> When you update `resturantList` by filtering it, you're just changing a local variable, not the state variable that React tracks for rendering.
-> In your code, updating `resturantList` won’t trigger a re-render because React re-renders components only when state or props change.
-> When you use a normal variable (let or const) within a functional component, changing its value won't automatically trigger a re-render of the component. React doesn't detect changes to normal variables because it doesn't track them for re-rendering purposes. Therefore, updating a normal variable won't cause React to update the UI.
### Key Concept: React State vs. Variables

In React, when we want the UI to re-render based on a change, we need to use **state** instead of regular variables. When you modify a variable like `resturantList`, React doesn’t "see" that change as it’s not tracking that variable directly.
Here’s why the UI doesn’t update:

1. **State Management**: React components re-render when their state changes. In your code, `resturantList` is just a local variable. React doesn't know that it has changed, so it doesn't trigger a re-render.
    
2. **Using State**: To manage the list of restaurants and allow React to track changes, you should use the `useState` hook. This will allow you to update the state and trigger re-renders when it changes.

-> WHEN WE SAY REACT IS FAST, THAT MEANS IN TERMS OF DOM MANIPULATION!
->     `let resturantList=resList;`
Here resturantList is a Normal React Variable!! BORINGGGGG
-> We need something better than this!
-> LIKE A SUPER VARIABLE !!!! BUT HOW??
THIS SUPER VARIABLE IS CALLED **STATE VARIABLE** 
→So every Library is trying to do That our data layer and the UI work in SYNC with each other effectively

→agar data mein change ae toh in that case ui bhi change hone chahiye
→To make sure the data layer stays in sync with the ui layer meaning if we change data in data layer the change should be reflected in the UI layer!
→ if a change occurs in the normal variable it won’t be shown in UI so that’s shy we need state variables!

# **HOOK**
→A hook is just a normal JS function given to us by REACT but this function comes with some superpowers!
→Who wrote these functions? Facebook developers! 
→So when we’re talking about REACT HOOKS We’re talking about the utility functions!
-> There are Multiple JavaScript Hooks!
-> We need to import these hooks as named imports! KYONKI JAHAN SE EXPORT HORAHE HONGE UNHONE NAMED EXPORT KIYE HONGE 
### What Are React Hooks?

Hooks are simply JavaScript functions that allow you to "hook into" React's features. By using hooks, you can manage state, handle side effects, and interact with the React lifecycle in functional components.

### Why Use Hooks?

Before hooks, state and lifecycle methods were only accessible in class components. Hooks give functional components these "superpowers," making code more concise, easier to read, and removing the need for complex class-based structures.

### The Two Most Important Hooks

There are many hooks, but two are fundamental: `useState` and `useEffect`.
#### 1. `useState` Hook

**The `useState` hook lets you add state to your functional components. State is data or variables that may change over time (e.g., user input, component toggles, etc.).
-> DO YOU KNOW WHY ??
->BECAUSE AGAR STATE VARIABLE KISI BHI FUNCTIONAL COMPONENT MEIN BNAYA THEN USS FUCNTIONAL COMPONENT MEIN BANA KOI BHI STATE VARIABLE JABH CHANGE HOGA THEN COMPONENT RE RENDER HOGA, MTLB KI UI WITH THE UPDATED VALUE OF THE VARIABLE DIKHEGI SIMPLE
-> `useState` gives you superpower state variables 
->  `useState` is used to make State Variables! Why is it called State Variables? Because it maintains the state of your component!
##### How to Use `useState`

 1. **Import** it as a named import from React:
   `import { useState } from 'react';`
   WHY NAMED IMPORT??? BECAUSE JISNE EXPORT KIYA HAI USNE NAMED EXPORT KIYA HAI NAKI DEFAULT
  1. **Declare the state variable** using `useState`, which returns two things: the state variable and a function to update it.

`const [count, setCount] = useState(0);`

- **`count`** is the state variable.
- **`setCount`** is a function that lets you update `count`.
- **`0`** is the initial value of `count`.

**DECLARATION** 

```JavaScript
const [state, setState] = useState(initialState);
const [listOfRes,setListOfRes]=useState([]);// yahan empty array initial state hai!
```

- `**state**`: This represents the current state value. You can read this value to access the current state.
- `**setState**`: This is a function that allows you to update the state. When called, it schedules a re-render of the component with the new state value.
- `**initialState**`: This is the initial value of the state variable.

3.**Using `useState` in a Component**:


```javascript
function Counter() {
    const [count, setCount] = useState(0);
    console.log("FUNCTIONAL COMPONENT RENDERING ")
    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
    );
}
```
-> When you click the button, `setCount` updates `count` by 1, and the component re-renders with the new value.
-> BUT YAHAN PURA FUNCTION FIR SE CHL RAHA HAI
![Episode 05 - Let's get Hooked-20241029073934622.webp](../../Images/Episode%2005%20-%20Let's%20get%20Hooked-20241029073934622.webp)


-> JABH BHI CLICK KIYA console.log("Function component Rendering bhi chal raha hai)
-> MEANING PURA FUNCTION CHLTA HAI
-> when you click the button, the `Counter` component does indeed re-render, which means the function `Counter()` is called again. But this doesn't reset `count` to `0` every time.

Here's why:

1. **React State Retention**: The `useState` hook is designed to "remember" the state between re-renders. So even though the `Counter` function runs again, `useState(0)` doesn't reset to `0` on each re-render. Instead, it provides the current state value (`count`) that React has stored internally.
    
2. **React Re-rendering Mechanism**: When you call `setCount(count + 1)`, React triggers a re-render. During this re-render, React re-executes the `Counter` function but "knows" the current value of `count` due to how `useState` works. So, it passes this current value (`count` after incrementing) back to the component function.
    
3. **Effectively,** `useState(0)` only initializes `count` to `0` on the first render. On subsequent renders, it simply retrieves the updated `count` value from React's internal state storage.
    

So, each time you click the button, `setCount(count + 1)` updates the state, React re-renders the component, but `count` always reflects the latest updated value.


### What Does `useState` Return?

When you call `useState`, it **returns an array with two elements**:

1. **State Variable**: The current value of the state (e.g., `count`).
2. **State Update Function**: A function that lets you update the state variable (e.g., `setCount`).

### What Do We Pass Inside `useState`?

You pass **the initial value** of the state variable as an argument to `useState`. This initial value can be:

- **A Primitive Value**: like a number, string, or boolean. For example, `useState(0)` or `useState('Hello')`.
- **An Object or Array**: You can also use objects or arrays as initial values. For example, `useState([])` or `useState({ name: 'John' })`.

### Is `useState`'s Return Really an Array?

Yes! `useState` **returns an array** with two elements. This is why we often use **array destructuring** to capture both the state variable and its updater function in a single line:
`const [stateVariable, setStateVariable] = useState(initialValue);`

Alternatively, if you didn’t use destructuring, you could access them like this:

```javascript
const state = useState(0); // returns [currentValue, updateFunction]
console.log(state[0]); // current state value
console.log(state[1]); // function to update state


```

->But destructuring makes it much cleaner and more readable, which is why it’s the preferred syntax in React.
->This is just basic Array destructuring
![Untitled 11 14.png](../../Images/Untitled%2011%2014.png)


![Untitled 9 17.png](../../Images/Untitled%209%2017.png)
THESE BOTH ARE EQUIVALENT IN ONE WAY
In JavaScript, **`const`** does indeed create a constant reference, meaning the variable itself can’t be reassigned. However, when using `useState`, we’re not actually reassigning the variable directly; instead, we’re updating the state through the **state updater function** (`setCount` in this case), which React manages internally.

Here’s how it works:

1. **`const` Declaration**: The `const` keyword ensures that the variable reference itself can’t be reassigned, but it doesn’t freeze the value inside the variable. React handles state updates by **re-rendering** the component with a new value for the state variable when we call `setCount`.
    
2. **State Update Process**:
    
    - When you call `setCount(newCount)`, React updates the internal state and triggers a re-render of the component.
    - During this re-render, React recalculates the value of `count` and provides it with the latest value.
    - Because of this, even though `count` is defined with `const`, it can hold a new value each time the component re-renders.

→When you use the `**useState**` hook to create a state variable, React provides a special setter function (`**setState**`) to update the state variable. When you call this setter function to update the state, React knows that the state has changed, and it schedules a re-render of the component. During this re-render, React compares the new state with the previous state and updates only the parts of the UI that depend on the changed state, efficiently updating the UI without re-rendering the entire component tree.

-> SO WHEN A STATE VARIABLE OF A COMPONENT CHANGES REACT RE RENDERS THE WHOLE COMPONENT 

![Untitled 12 12.png](../../Images/Untitled%2012%2012.png)

Virtual DOM (Document Object Model) is a programming concept used by libraries/frameworks like React.js to efficiently update the user interface (UI) of web applications.

**Real DOM vs. Virtual DOM**: The Real DOM is the actual DOM tree created by the browser when a web page is loaded. It's a tree-like structure representing all the elements (nodes) of the HTML document. Manipulating the Real DOM directly can be slow and inefficient, especially for complex web applications.

The Virtual DOM, on the other hand, is an in-memory representation of the Real DOM created by React.js. It's a lightweight copy of the Real DOM that React maintains and manipulates internally. It's designed to be fast and efficient to update.

Yes, the Virtual DOM is indeed represented as a JavaScript object. It's essentially a tree-like data structure that mirrors the structure of the real DOM but is kept in memory by React or other similar libraries/frameworks.

Each node in the Virtual DOM corresponds to an element in the real DOM. These nodes are JavaScript objects containing information about the corresponding HTML element, such as its type (e.g., div, span), attributes, children, and other properties.

**The reconciliation algorithm** is a key aspect of how React efficiently updates the user interface (UI) by determining which parts of the Virtual DOM need to be updated when changes occur in a React component.

Here's an overview of how the reconciliation algorithm works in React:

1. **Virtual DOM Diffing**: When a component's state or props change, React re-renders the component and generates a new Virtual DOM tree representing the updated UI.
2. **Old vs. New Virtual DOM**: React compares the new Virtual DOM tree with the previous Virtual DOM tree to identify the differences between them. This process is often referred to as "diffing".
3. **Tree Reconciliation**: React performs a process known as "tree reconciliation" to efficiently update the real DOM based on the differences identified during the diffing process. React traverses both the old and new Virtual DOM trees simultaneously, comparing each node to its counterpart in the other tree.
4. **Keyed Nodes**: React uses "keys" to identify nodes uniquely within a list of elements. When rendering lists of elements (e.g., in a `**<ul>**` or `**<ol>**`), providing a unique key for each element helps React optimize the reconciliation process. Keys allow React to determine which elements have changed, been added, or been removed from the list, improving performance and reducing unnecessary re-renders.
5. **Minimal Updates**: React aims to make the minimum necessary updates to the real DOM to reflect the changes in the Virtual DOM. Instead of re-rendering the entire UI, React selectively updates only the parts of the UI that have changed, minimizing the amount of work needed and improving performance.
6. **Batched Updates**: React batches multiple updates together and applies them in a single operation to avoid unnecessary re-renders and DOM manipulations. This helps prevent "layout thrashing" and improves the overall performance of the application.




```javascript
import React, { useState, useEffect } from "react";

const MyComponent = () => {
    // JavaScript Logic Area (above `return`)
    
    // 1. Declare state variables
    const [count, setCount] = useState(0);
    const [text, setText] = useState("Hello");

    // 2. Define functions to handle events or logic
    const incrementCount = () => {
        setCount(count + 1);
    };

    const handleChangeText = () => {
        setText("You clicked the button!");
    };

    // 3. Set up side effects using `useEffect`
    useEffect(() => {
        console.log("Component mounted or count changed!");

        // Optional cleanup function
        return () => {
            console.log("Cleanup on component unmount or before re-running the effect");
        };
    }, [count]); // Effect will run on initial render and when `count` changes

    // JSX Section (returned by the component)
    return (
        <div>
            <h1>{text}</h1>
            <p>Count: {count}</p>
            <button onClick={incrementCount}>Increment Count</button>
            <button onClick={handleChangeText}>Change Text</button>
        </div>
    );
};

export default MyComponent;

```


### Explanation of Each Section

1. **JavaScript Logic Area**:
    
    - **State Initialization**: Here, `useState` initializes `count` and `text` with default values.
    - **Event Handlers**: The functions `incrementCount` and `handleChangeText` define actions that update the state variables when a user interacts with the component (e.g., by clicking buttons).
    - **Side Effects with `useEffect`**: The `useEffect` hook sets up a side effect that runs whenever the component mounts and whenever `count` changes. You can also use it for cleanup operations, like removing event listeners or stopping timers when the component unmounts.
2. **JSX (UI Layout)**:
    
    - **Rendering State Values**: The JSX structure renders the `text` and `count` variables within `{}` to display their values dynamically on the screen.
    - **Event Binding**: Event handlers, like `onClick={incrementCount}`, bind functions from the logic area to specific UI elements, letting the component update state in response to user actions.

When a functional component is rendered, **the entire code inside it runs from top to bottom**, and then it returns the JSX that makes up its visual structure. Here's a simplified breakdown:

### Step-by-Step of What Happens During a Render:

1. **Execution Begins**:
    
    - When the component renders, the code inside it starts executing line by line, including variable declarations, `useState` hooks, `useEffect` hooks, and any other logic.
2. **Running the `useEffect` Hooks**:
    
    - As the component renders, if there are `useEffect` hooks, they don’t immediately execute their inner code during this first pass. Instead:
        - React notes each `useEffect` and will run them _after_ the initial render.
        - So, the setup logic in `useEffect` (like data fetching or starting a timer) happens after the JSX is rendered for the first time.
        - If `useEffect` has dependencies, React watches them to decide if the `useEffect` should re-run in future renders.
3. **Returning the JSX**:
    
    - Finally, the component returns the JSX, which tells React what the component should look like on the screen.
4. **Post-Render (Running Effects)**:
    
    - After React has used the JSX to update the UI, it will then run any `useEffect` callbacks.
    - If there’s a cleanup function returned in a `useEffect`, React will store it for later use when needed (like before re-running that effect or when the component unmounts).

### Breakdown of Render Steps Here:

- **First Render**:
    
    - `useState(0)` sets `count` to `0`.
    - Logs `"Component rendering..."`.
    - JSX (`<div>...</div>`) is returned, rendering `Count: 0` and a button.
    - _Then_, `useEffect` runs, logging `"Effect runs after initial render"`.
- **When the Button is Clicked**:
    
    - `setCount` updates `count` to `1`, which triggers a re-render.
    - The component code runs again from top to bottom, logging `"Component rendering..."`.
    - JSX is returned, showing the updated count.
    - `useEffect` runs again due to `[count]`, logging the cleanup message, `"Cleanup before the next effect or when unmounting"`, before re-running the effect.

`setCount(1)` and `setCount(count + 1)` do seem similar, but they serve different purposes in terms of state updates:

1. **Direct Update** (e.g., `setCount(1)`):
    
    - This will set `count` directly to `1` every time it's called, **overwriting** the previous value.
    - This approach is useful when you want to set a **specific value** for the state, regardless of its current value.
2. **Incremental Update** (e.g., `setCount(count + 1)` or using a function):
    
    - This approach updates `count` **based on its current value**. So, if you want to increase `count` by `1` each time, `setCount(count + 1)` is a dynamic way to achieve that.
    - This is particularly helpful when the new state depends on the **previous state value**.

### Example

Imagine if you have a button that users can click multiple times to increase the count:

`const incrementCount = () => {     setCount(count + 1); };`

Using `setCount(count + 1)` will increment `count` by `1` each time the function is called, so the count increases each time the button is clicked.


Wrapping `setCount(count + 1)` and `setText("You clicked the button!")` in functions like `incrementCount` and `handleChangeText` is a common React pattern for a few key reasons:

1. **Encapsulation of Logic**:
    
    - Functions like `incrementCount` and `handleChangeText` encapsulate the logic of what should happen when the state changes.
    - This makes the code cleaner and easier to manage, especially if the update logic becomes more complex (e.g., if you need to check a condition before updating `count`).
2. **Event Handling**:
    
    - These functions are **event handlers**. They respond to user actions (like a button click) and are only called when the user interacts with the component.
    - By defining a specific function for each event, you can directly assign them to elements in JSX, such as `onClick={incrementCount}`, making it clear what action each UI element is responsible for.
3. **Reusability**:
    
    - If you want to reuse the logic in other parts of the component (or pass it as a prop to child components), having it in a standalone function makes it easy to call wherever needed.
4. **State Dependency**:
    
    - When updating a state based on its current value (e.g., `setCount(count + 1)`), it's often more readable and reliable to wrap this logic in a function, especially in cases where multiple updates may occur. Using functions for state updates helps ensure that React consistently updates the state based on the latest value.

### Example: Without Functions

If you were to call `setCount(count + 1)` directly in JSX, it could become confusing:


```javascript
// Without functions:
<button onClick={() => setCount(count + 1)}>Increment Count</button>
<button onClick={() => setText("You clicked the button!")}>Change Text</button>

```


->The `return` inside a `useEffect` is a bit different from the `return` in the main body of the functional component where JSX is returned.
### Two Different Returns in Functional Components

1. **The Main Return (for JSX)**:
    
    - This is the primary `return` statement in the functional component. It’s what actually renders the component’s UI to the screen in the form of JSX.
2. **The `return` inside `useEffect` (for Cleanup)**:
    
    - In `useEffect`, the `return` statement is used specifically for **cleanup purposes**.
    - This cleanup function doesn’t affect the rendered UI but rather handles cleanup of side effects whenever the component is **unmounted** or **before re-running the effect** (in cases where dependencies change).

### Why Use a Cleanup Function in `useEffect`?

The cleanup function inside `useEffect` is helpful in these cases:

1. **Component Unmounting**:
    
    - When a component is removed from the DOM, you might want to stop certain processes (like clearing intervals, stopping timers, removing event listeners, or cancelling API requests).
    - The cleanup function allows you to handle these tasks to prevent memory leaks.
2. **Dependency Changes**:
    
    - When a dependency (like `count` in your example) changes, React first calls the cleanup function from the previous render cycle before executing the `useEffect` callback again.
    - This ensures that each time the effect runs, you have a fresh setup without leftover data or event listeners from previous runs.

### The Role of the Cleanup Function

1. **Setting Up the Task**:
    
    - When we write code in `useEffect`, we’re setting up a task. Let’s say it’s like turning on a timer that adds to a counter every second.
2. **Returning the Cleanup**:
    
    - The `return` inside `useEffect` is where we write a **cleanup function**. This is code that tells React, “Hey, if you’re going to remove this component or restart this task, please turn off that timer first!”
    - In other words, **cleanup is like a reset button**, making sure the task we set up won’t keep running in the background when it’s no longer needed.
3. **Why Use Cleanup?**
    
    - It’s like cleaning up after yourself! Without the cleanup, if we left a timer running and then made new ones, it could get messy, with extra timers or background tasks stacking up and slowing things down.

When we return a function from `useEffect`, that function doesn’t go anywhere else in our code. Instead, React treats this returned function in a special way.

Here’s what happens:

1. **React Stores the Cleanup Function**:
    
    - React knows that if `useEffect` returns a function, it’s meant to be a **cleanup function**. So React takes note of it and holds onto it.
2. **When React Calls the Cleanup Function**:
    
    - React will automatically call this cleanup function in two cases:
        - **When the component unmounts** (i.e., it’s removed from the screen).
        - **When `useEffect` is about to re-run** due to a change in dependencies (e.g., if the component needs a different setup).
3. **You Don’t Directly Use the Cleanup Function**:
    
    - As a developer, you don’t have to worry about where it’s returned to or manually calling it. React handles all of this behind the scenes.