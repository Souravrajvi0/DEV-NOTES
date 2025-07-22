---
view-count: 4
---
->**Planning is something we ought to do!**
->Since we need to make our code modular! Which means if the code is repetitive Then you can just make one part and repeat it over time!
->So whenever we need a component which can be reused overtime always make a component for it!
![Episode 04 - Talk is cheap, show me the code!-20241027170026184.webp](../../Images/Episode%2004%20-%20Talk%20is%20cheap,%20show%20me%20the%20code!-20241027170026184.webp)
![Episode 04 - Talk is cheap, show me the code!-20241027170216145.webp](../../Images/Episode%2004%20-%20Talk%20is%20cheap,%20show%20me%20the%20code!-20241027170216145.webp)

---

**How to give inline Style in JSX?**

![Untitled 65.png](../../Images/Untitled%2065.png)

→Since Inline style jo hota usmein style humein ek JS object pass krna hota hai so isliye maine{} inka use kiya hai styleCard k sath!
→But inline Styling is not preferred! What we can do is make a css file and using class names we can apply style on the files!
→Directly object bhi likh skte hain curly braces k andar!
![Episode 04 - Talk is cheap, show me the code!-20241027172055424.webp](../../Images/Episode%2004%20-%20Talk%20is%20cheap,%20show%20me%20the%20code!-20241027172055424.webp)
  

---
![1108](../../Images/Episode%2004%20-%20Talk%20is%20cheap,%20show%20me%20the%20code!-20241027173129773.webp)


**HOW TO MAKE THE CARDS DYNAMIC????** Since Until Now I've just hardcoded Data!
## **PROPS**
**-> WHAT IS FUNCTIONAL COMPONENT IN THE END OF THE DAY??? IT'S JUST A NORMAL JAVASCRIPT FUNCTION**
**->Passing A prop to a component is just as same as passing an argument to a function**
->**When You have to dynamically pass in some data to a component you pass it as a prop!**
-> SO IN THE END OF THE DAY PROPS ARE JUST NORMAL ARGUEMENTS TO A FUNCTION
![Untitled 1 55.png](../../Images/Untitled%201%2055.png)
->THIS IS CALLED PASSIN PROPS TO AN FUNCTION
->**What react will do is wrap all these properties inside an object! and pass it as props!**

![Untitled 2 42.png](../../Images/Untitled%202%2042.png)

**Yahan par props ek object hai!**

![Untitled 3 38.png](../../Images/Untitled%203%2038.png)

![Untitled 4 35.png](../../Images/Untitled%204%2035.png)

  

In React, you can pass data to a component using props (short for "properties"). Props are a way of passing data from parent components to child components. Here's how you can pass props to a component:

### 1. **Define Props in the Parent Component**

- In React, **props** (short for properties) allow you to pass data from a **parent component** down to a **child component**.
- In the parent component, you define the data you want to send. For example, if you want to pass a `name` and an `age` to the child, you can define them as variables in the parent component.

```javascript
function ParentComponent() {
    const name = "John";
    const age = 30;
    // Define variables in the parent component
    return (
        <div>
            {/* Pass data as props to the child component & also name and age is variable here toh humne {]use karliyea hai yahan*/}
            <ChildComponent name={name} age={age} />
        </div>
    );
}
```

### . **Pass Data as Props**

- When you include the child component in the parent’s JSX, you pass data as attributes in the **child component’s tag**.
- **Curly braces `{}`** are used to embed JavaScript expressions in JSX. For example, `{name}` and `{age}` pass the `name` and `age` values as props.
- You also showed that you can pass data directly by writing the values in quotes (like `"John"` for `name` and `30` for `age`). This approach is fine for fixed values, but curly braces allow you to pass variables, expressions, and other JavaScript code.


```javascript
<ChildComponent name={name} age={age} />

```

```javascript
<ChildComponent name="John" age="30" />
```
### 3. **Access Props in the Child Component**

- In the child component, you access these props using a `props` object.
- You can either access each prop by `props.name` and `props.age` or destructure `props` right in the function parameters for cleaner code.


```javascript
function ChildComponent(props) {
    return (
        <div>
            <h2>Name: {props.name}</h2>
            <p>Age: {props.age}</p>
        </div>
    );
}
```

Alternatively, destructure `props`:

```javascript
function ChildComponent({ name, age }) {
    return (
        <div>
            <h2>Name: {name}</h2>
            <p>Age: {age}</p>
        </div>
    );
}

```

->In React, when you pass props to a component using JSX, React creates an object with those props. This object is referred to as the props object, and it contains key-value pairs where the keys are the names of the props and the values are the data passed to those props.

![Untitled 5 30.png](../../Images/Untitled%205%2030.png)
→We can do destructuring on the fly also

![Untitled 6 28.png](../../Images/Untitled%206%2028.png)

  

---

## Config Driven UI

→When The website is driven by the data! Or The UI is driven by the data This is called Config driven UI. For example- when in Delhi The Ui is different and in Sardarshahar The Ui is different.

→"**Config-driven UI**" refers to a user interface (UI) design approach where the layout, behavior, and features of the UI are determined by a configuration file or set of parameters rather than being hard-coded into the application's source code. This approach offers flexibility and allows for easier customization and modification of the UI without the need for extensive coding.

**Dynamic Rendering**: The UI components are rendered dynamically based on the configuration provided. This means that the UI adapts and changes according to the configuration settings without requiring changes to the underlying codebase

  -> Ek tarika se skeleton hai hmare pass but usmein ab Meat/mans will make Look everyone Different but the basic Skeleton is same and Skeleton mein meat bharke sabke asthetics change kar skte hain!
  
  

![Untitled 7 24.png](../../Images/Untitled%207%2024.png)

The reason we use `props.resdata.name` instead of `props.resObj.name` is because of the **prop name** used in the parent component.

In the parent component, you named the prop `resdata`, not `resObj`:
`<RestaurantCard resdata={resObj} />`

Here:
- `resdata` is the name of the prop you’re using to pass `resObj`.
- `resObj` is the actual object being passed, but it’s now assigned to the `resdata` prop in the child component.

In the child component, we refer to `resdata`, which contains the data of `resObj`. So, to access the properties of `resObj`, we use `props.resdata.name`, `props.resdata.location`

    const {resdata}=props;


---

->Exactly. The `**.join()**` method takes an array and concatenates its elements into a single string, using the specified separator between each pair of elements.  
RETURNS A STRING

```javascript
const fruits = ['Apple', 'Banana', 'Orange'];  
const joinedString = fruits.join(', '); // Joins elements with comma and space  
console.log(joinedString); // Output: "Apple, Banana, Orange"  

//array.join(separator)

```


---

### **We always need to write reusable components!**

---

->Optional chaining is a feature introduced in JavaScript to simplify accessing properties of nested objects when there's a possibility of encountering `**null**` or `**undefined**` along the way. It allows you to safely access deeply nested properties without causing an error if one of the intermediate properties is `**null**` or `**undefined**`


```javascript
const user = {  
name: 'John',  
address: {  
city: 'New York',  
postalCode: '10001'  
}  
};  

const postalCode = user.address.postalCode; // "10001"

Another example of optional chaining!

The variable names should match the property names in the `**resData?.data**`

const {  
cloudinaryImageId,  
name,  
cuisines,  
avgRating,  
costForTwo,  
deliveryTime,  
} = resData?.data;  
```





---

->Jabh bhi .map() lagao in that case we ought to specify a key!

![Untitled 8 21.png](../../Images/Untitled%208%2021.png)

**→ The callback function inside the map() method is indeed returning JSX elements. The arrow function (restaurant) => (...) is returning the JSX element <Resturantcard resData={restaurant} /> for each iteration over the reslist array.**  
**→The map() function in JavaScript expects a callback function that returns a value for each element in the array. In this case, the callback function is returning a JSX element, specifically a <Resturantcard/> component with the resData prop set to the current restaurant object.**  
→When JSX elements are returned directly within parentheses in an arrow function, they are automatically treated as the return value of the function. This allows for concise and readable code when rendering lists of components in React without the need for an explicit return statement.

→To uniquely identify the Elements we need keys!

**→In React, when you render a list of elements using a loop (such as with `**map()**`), it's important to specify a `**key**` attribute for each element in the list. The `**key**` attribute helps React identify which items have changed, are added, or are removed. It's used by React for efficient re-rendering of lists.**  
  ![Episode 04 - Talk is cheap, show me the code!-20241027201154820.webp](../../Images/Episode%2004%20-%20Talk%20is%20cheap,%20show%20me%20the%20code!-20241027201154820.webp)


```javascript
const Body=()=>{
    return (
        <div className="body">
            <div className="search">SEARCH BAR</div>
            <div className="res-container">    
            {
              resList.map((resturant)=><RestaurantCard key={resturant.info.id} resdata={resturant}/>)  // alwyas add the key here!
            }

            </div>
        </div>
    )
}
```
->`ResList.map()` will return a new array of elements that are created inside the `.map()` function. In this case, it’s returning an array of `<RestaurantCard />` components.

### Detailed Explanation

`resList.map((restaurant, index) => <RestaurantCard key={index} resdata={restaurant} />)`

1. **Each element in `resList`** (which could be an array of restaurant objects) is transformed into a `<RestaurantCard />` component.
2. So, for each `restaurant` object, it creates:
    `<RestaurantCard key={index} resdata={restaurant} />`
3. After mapping over the entire `resList`, `.map()` collects all of these `<RestaurantCard />` components into a single array.

### Example of What It Returns

If `resList` has three items, it will produce something like this:
`[     <RestaurantCard key={0} resdata={resList[0]} />,     <RestaurantCard key={1} resdata={resList[1]} />,     <RestaurantCard key={2} resdata={resList[2]} /> ]`
SO IT RETURNS THE ARRAY OF JSX ELEMENTS
### Usage in JSX
Since React can render arrays of components directly, this array of `<RestaurantCard />` components will be rendered within the `res-container` div.

----

→It takes a big performance hit when We don’t define keys!

→ if there is no unique id then we might use the index!

![Untitled 10 15.png](../../Images/Untitled%2010%2015.png)

Don’t use indexes for keys!

![Untitled 11 13.png](../../Images/Untitled%2011%2013.png)

![Untitled 12 11.png](../../Images/Untitled%2012%2011.png)


Adding a unique `key` to each element when using `.map()` is crucial because **it helps React efficiently update and manage the list** when there are changes.

Here’s why it’s needed:

1. **Tracking Element Identity**:
    
    - Each child in a list should have a unique `key` prop so React can identify which items have changed, been added, or removed.
    - Without a unique key, React can’t track these changes accurately, which may lead to unexpected behavior.
2. **Performance Optimization**:
    
    - When React renders a list, it compares the current list with the previous one to decide what needs updating. The `key` allows React to re-use or re-order elements efficiently.
    - This optimization improves the app’s performance, especially for large lists, as React can skip re-rendering elements that haven’t changed.
3. **Avoiding Unwanted Side Effects**:
    
    - If there’s no key (or if keys are not unique), React may reuse DOM elements incorrectly. For example, input fields might lose focus, or the wrong item’s data might be displayed after a list update.



**In a functional component in React, you typically have two main sections:**

1. **JavaScript Logic Area (Above `return`)**: This section is where you handle the **logic** for your component, such as:
    
    - Declaring state variables using `useState`
    - Setting up side effects with `useEffect`
    - Defining functions for event handling or other internal logic
2. **JSX (Returned by the Component)**: This section is the **UI layout** that gets rendered on the screen. Here, you use JSX to describe how you want the component to look, and you can also embed JavaScript expressions within `{}` to dynamically display values from the logic area.