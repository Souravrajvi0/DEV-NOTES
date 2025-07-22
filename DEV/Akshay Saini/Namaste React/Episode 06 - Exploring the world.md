---
view-count: 4
---
![Untitled 67.png](../../Images/Untitled%2067.png)

![Untitled 1 57.png](../../Images/Untitled%201%2057.png)

Microservices and monolithic architectures are two different approaches to designing and structuring software applications, each with its own set of characteristics and trade-offs.

1. **Monolithic Architecture**:
    - In a monolithic architecture, the entire application is developed, deployed, and maintained as a single, self-contained unit.
    - All the components of the application, such as the user interface, business logic, and data access layer, are tightly integrated and run within the same process or application container.
    - Monolithic architectures are characterized by their simplicity, as they involve a single codebase, development environment, and deployment process.
    - However, monolithic architectures can become complex and difficult to manage as the application grows in size and complexity. They can also suffer from scalability and flexibility limitations, as all components are tightly coupled.
2. **Microservices Architecture**:
    
    - In a microservices architecture, an application is decomposed into smaller, loosely-coupled services, each responsible for a specific business function or domain.
    - Each microservice is developed, deployed, and scaled independently, often using different programming languages, frameworks, and databases.
    - Microservices communicate with each other over the network, typically using lightweight protocols such as HTTP or messaging queues.
    - Microservices architectures offer several benefits, including improved scalability, flexibility, and maintainability. They enable teams to develop and deploy services independently, allowing for faster development cycles and better isolation of failures.
    - However, microservices architectures also introduce complexity, as they require additional infrastructure for service discovery, communication, and management. They can also introduce challenges related to data consistency, distributed transactions, and deployment orchestration.
    
    → In Microservices Architecture one service can be written in VUE while other can be written in REACT…..
    
    ---
    
    ![Untitled 2 44.png](../../Images/Untitled%202%2044.png)
    -> In the 1st method for the initial 500ms the page would be blank! and then Suddenly The page will come and BOOM! BUT THIS IS POOR UI!
    →React render cycles are very fast! So two renders mein kya hi farak padega i guess
    →The 2nd approach is better
    -> Pehle humne Shimmer UI Ko render kar liya and then after 500ms maine ekbar aur render karke PURA PAGE LEKAR AGYA

   First Render k bad api call lagegi mtlb useEffect mein dalo api call and also Re render bhi chahiye toh mtlb vahan par state variable bhi change karo useEffect mein hi ya koi fucntion jise call lagi ho in useEffect mein uski body mein taki re render toh wo by this incoming data jisko api call lagai thi in the first place 
    ---
    
    ## **USE EFFECT** HOOK
    
    ![Untitled 3 40.png](../../Images/Untitled%203%2040.png)
    The `useEffect` hook handles **side effects** in functional components. A side effect could be anything that affects something outside the component, like data fetching, subscriptions, or changing the document title.
   ##### How to Use `useEffect`

    **Import** it as a named import from React:
    `import { useEffect } from 'react';
    2.**Declare the effect** by passing a function to `useEffect`:
       `useEffect(() => {`
    `conso`le.log(`Count changed to ${count}`);
               `}, [count]);`

    →So when will be this callback function will be called after our component is rendered!

  Yes, the callback function inside `useEffect` in React is executed **in two main scenarios**:
  The `useEffect` callback function will re-run **whenever a state or prop in the component changes**, but only if that state or prop is specified in the dependency array apart from the first render!
1. **On Initial Render**: When the component is mounted (i.e., displayed for the first time), the callback function inside `useEffect` is called after the component is rendered to the screen.
    
2. **On State or Prop Changes**: Whenever a **state variable** or **prop** specified in the `useEffect` dependency array changes, the callback function will run again. If a variable in the dependency array changes, the effect will re-run with the updated state or prop values.

### When Will the Effect Run?

In the above example:

- On **initial render** of `ExampleComponent`, the effect runs, and `"Effect is running!"` is logged.
- Every time the **`count`** state changes (when you click the "Increment" button), the effect re-runs, logging `"Effect is running!"` again.

### The Dependency Array

- If you pass an **empty array** (`[]`) as the dependency array, the effect will only run **once on initial render**.
- If you **omit the dependency array** entirely, the effect will run **on every render**, which can lead to performance issues if the component re-renders often.// so if any of the state variable changes then it is re rendered 

 
    In React's `**useEffect**` hook, the parameters passed are:
    
    1. **Effect Function**: This is the first parameter and it's a function that contains the code for the effect you want to perform. This function will run after every render unless specified otherwise.
    2. **Dependency Array (Optional)**: This is the second parameter and it's an array containing values (usually props or state variables) that the effect depends on. If any of the values in this array change between renders, the effect function will run again. If this array is empty, the effect will only run after the initial render. If you omit this parameter, the effect will run after every render



```javascript
useEffect(() => {
    // Your code here, e.g., fetch data or subscribe to a service.
    console.log('Component mounted or updated');
     // CALLBACK FUNCTION
    // Optional cleanup function
    return () => console.log('Component unmounted or cleanup');
}, [/* Dependency array here */]);
```


**Using `useEffect` in a Component**:

- The function passed to `useEffect` will run **after every render** by default. if I don't add the dependency array!
- You can specify when it should re-run by adding dependencies in an **array** (called the "dependency array").


```javascript
useEffect(() => {
    console.log(`Count changed to ${count}`);
}, [count]);  // Only runs when `count` changes

```

-> The Callback function will be called after the component Renders!
### **SO IF WE HAVE TO DO SOMETHING AFTER THE COMPNENT IS RENDERED WE NEED TO WRITE IT INSIDE THE USE EFFECT**

If we make an API Call outside in our project the there might be error due to CORS policy!

![[Episode 06 - Exploring the world-20241028103733520.webp]]
-> Our Browser Blocks us from Calling Api from one origin to another origin!
-> This is CORS POLICY! WE USE CORS EXTENSION

```javascript
useEffect(()=>{
        console.log("BODY RENDERED");
        fetchData();

    },[]);


    const fetchData=async()=>{
        const data =await fetch("https://www.swiggy.com/dapi/restaurants/list/v5?lat=12.9599618&lng=77.6131577&is-seo-homepage-enabled=true&page_type=DESKTOP_WEB_LISTING");
       const json=await data.json();
        setResturantList(json?.data?.cards[4]?.card?.card?.gridElements?.infoWithStyle?.restaurants);
    }



```
See We've done The fetchData Call in the useffect so that kinda makes sense!
-> But yahan ek problem hai ye infinite loop ban raha hai yahan!!!  if we omit the dependency array
-> Can you see because RENDER -> USEFFECT-> NEW DATA: SET RESTURANT LIST -> RENDER -> USE EFFECT-> NEW DATA: SET RESTURANT LIST-> RENDER .......
-> solved this by passing an empty array so ekbar ki call hoga useEffect

-> Within a React component, you can return different JSX based on conditions. This allows you to render different UI elements depending on the state of your component or props passed to it.


```javascript
const MyComponent = ({ isLoggedIn }) => {
    return (
        <div>
            {isLoggedIn ? (
                <h1>Welcome back!</h1>
            ) : (
                <h1>Please log in.</h1>
            )}
        </div>
    );
};

```



```javascript
 if(restaurantList.length===0){
        return(
            <h1>LOADING</h1>
        )
    }

    return (
        <div className="body">
            <div className="filter">
                <button className="filter-btn" onClick={()=>{
                     let filteredrestaurantList=restaurantList.filter(
                     (res)=>res.info.avgRating >4.5 
                    )
                    setResturantList(filteredrestaurantList);
                    console.log(filteredrestaurantList);
                    }}>Top Rated Resturants</button>
            </div>
            <div className="res-container">    
            {
              restaurantList.map((resturant,index)=><RestaurantCard key={index} resdata={resturant}/>)
            }

            </div>
        </div>
    )

```


NOW THIS IS THE INSPIRATION FOR SHIMMER UI!
ALWAYS WHEN YOU'RE BUILDING YOU UI APPLICATION AND THE API IS TAKING SOME TIME LOAD A SHIMMER UI QUICKLY!
# **SHIMMER UI**


Shimmer UI is a visual effect used in user interfaces, particularly in mobile applications and web development, to indicate that content is loading. It typically involves displaying a subtle animation, often resembling a shimmering light, over an area where content will appear once it's loaded.

The shimmer effect gives users visual feedback that something is happening in the background and that content is on its way. It's particularly useful in situations where loading times may be longer or when the content is fetched asynchronously. Instead of displaying a blank or static loading screen, the shimmer effect provides a more engaging and visually appealing experience for users.

Conditional rendering is a concept in web development, particularly in frameworks like React, Vue.js, and Angular, where you conditionally display components or content based on certain conditions or states.

 CONDITION TO RENDER THE SHIMMER UI COMPONENT!
```javascript
  if(restaurantList.length===0){
        return <Shimmer />
    }

```

SHIMMER COMPONENT
```javascript
const Shimmer=()=>{
    return(
      <div className="shimmer-container">
       <div className="shimmer-card"></div>
       <div className="shimmer-card"></div>
       <div className="shimmer-card"></div>
       <div className="shimmer-card"></div>
       <div className="shimmer-card"></div>
       <div className="shimmer-card"></div>
      </div>
    )
}
export default Shimmer;

```

**Conditional rendering** in React (and programming in general) refers to the technique of displaying different UI elements or components based on certain conditions. It allows you to render specific parts of your component's output only when certain criteria are met. This is essential for creating dynamic user interfaces that respond to user input, application state, or any other condition.

### Key Concepts of Conditional Rendering

1. **React Components**: In React, components can render different content based on props or state. You can determine what to show by evaluating certain conditions.
    
2. **Logic for Rendering**: The logic can involve simple boolean checks, comparisons, or even more complex expressions. Depending on the condition's outcome (true or false), different elements or components can be rendered.
    
3. **User Experience**: Conditional rendering enhances the user experience by allowing for a more interactive and responsive interface. For example, you might want to show a loading spinner while fetching data, display error messages when a request fails, or show different content based on user authentication status.


## MAKING OF LOGIN?LOGOUT BUTTON!

### Regular JavaScript Variables

- **Not Tracked by React**: Regular JavaScript variables (declared using `let`, `const`, or `var`) are not tracked by React. If you update a regular variable, React has no way of knowing that a change has occurred.
    
- **No Re-renders**: Changing a regular variable does not trigger a re-render of the component. This means that if you use a regular variable to store data and then update it, the UI will not reflect this change unless you manually trigger a re-render (which is generally not the recommended approach in React).

### State Variables

- **Tracked by React**: State variables (declared using `useState` in functional components or `this.state` in class components) are tracked by React. When you declare a state variable, React monitors it for changes.
    
- **Trigger Re-renders**: When you update a state variable using its setter function (e.g., `setCount` from `const [count, setCount] = useState(0)`), React automatically triggers a re-render of the component. This ensures that the UI reflects the latest state.

**Best Practices**: For any dynamic data that needs to affect the rendered output of a component, always use state variables instead of regular variables. This allows React to manage updates efficiently and keeps your components predictable and responsive to user interactions.

**In React, it essentially RE RENDERS means that the functional component is invoked again. Here’s a more detailed breakdown of how this process works:**

### What Happens During a Re-render?

- **State Update**: When you call a state setter function (like `setCount` from `useState`), React updates the state value internally.
    
- **Re-invocation of the Functional Component**: After the state update, React will re-invoke the functional component. This means that the entire function runs again from the top, including all the JavaScript logic and JSX rendering.
    
- **New State Value**: Since the state variable (e.g., `count`) now holds a new value, any expressions or logic that depend on that state variable will reflect the updated value.
    
- **Reconciliation**: React then compares the new output (the new virtual DOM) with the previous output (the previous virtual DOM). It determines what has changed and updates the actual DOM efficiently, only modifying what is necessary. This is known as the reconciliation process.
    
- **UI Update**: The changes are reflected in the user interface based on the updated state
**So yes, re-renders mean that the functional component is called again, and the updated state values allow the component to reflect any changes in the UI. This efficient update process is one of the key features of React that makes it powerful for building dynamic applications**

### Re-rendering Process in React

1. **State Change**: When you change a state variable using a state setter (like `setCount`), React detects that the state has changed.
    
2. **Re-invocation of the Functional Component**:
    
    - React re-invokes the entire functional component. This means all the code in the component runs again, and the state variable reflects its new value.
3. **Creation of a New Virtual DOM**:
    
    - During this re-invocation, React generates a new virtual DOM based on the latest state and props. This new virtual DOM represents what the UI should look like after the state change.
4. **Comparison of Virtual DOMs**:
    
    - React then compares the newly created virtual DOM with the previous virtual DOM (the one from the last render).
    - This process is known as **reconciliation**. React uses a diffing algorithm to efficiently determine what has changed.
5. **Updating the Actual DOM**:
    
    - After identifying the differences between the old and new virtual DOM, React updates only the parts of the actual DOM that have changed.
    - This minimizes direct manipulation of the DOM, which is generally slower, making React applications more performant.
6. **Rendering the Updated UI**:
    
    - Finally, the user interface reflects the updated state, showing the latest data to the user.


```javascript
const Header =()=>{
    const [btn,setBtn]=useState("login");
    const btnchnager=()=>{
        if(btn=="login"){
            setBtn("logout");
        }else{
            setBtn("login");
        }
    }
    return(
        <div className="header">
            <div className="logo-container">
             <img className="logo" src={LOGO_URL}/>
            </div>
            <div className="nav-items">
                <ul>
                    <li>Home</li>
                    <li>About Us</li>
                    <li>Contact Us</li>
                    <li>Cart</li>
                    <button className="login-button" onClick={
                      btnchnager
                    }>{btn}</button>
                </ul>
            </div>
        </div>
    )
}
```

    HERE WHENEVER THE STATE VARIABLE CHANGES! REACT WILL RE-RENDER THIS HEAD COMPONENT!
---
    **MAKING OF SEARCH BAR AND SEACH BUTTON**
Yes, in React, it's common practice to use state to manage the value of an input field, including a search bar. By doing so, you ensure that the input field's value reflects the current state of your application and can be updated dynamically.
    
```JavaScript
    
    const [restaurantList,setResturantList]=useState([]);
    
    const[searchText,setSearchText]=useState("");
    console.log("BODY RENDERING");
    useEffect(()=>{
        console.log("BODY RENDERED");
        fetchData();

    },[]);
    if(restaurantList.length===0){
        return <Shimmer />
    }

    return (
        <div className="body">
            <div className="filter">
                <div className="search" >
                 <input type="text" className="search-box" value={searchText} onChange={(e)=>{
                    setSearchText(e.target.value)
                 }} />
    
    
    ```

![[Episode 06 - Exploring the world-20241028125708635.webp]]

-> YAHAN PAR EK BAT NOTICE KARNA HI useEffect ka dep array empty khali rakhne se kitna fyada hua otherwise tu kya 97 calls lagata api par?
→So whenever we’re changing the state of a state variable react re renders the whole component! and HERE THE BODY IS GETTING RENDERED AGAIN!
-> But Virtual dom mein change toh buhut chota sa hai toh isliye buhut jada hogya hai sab kuch!
![[Images/Untitled 6 30.png|Untitled 6 30.png]]
    
In React, when a component's state changes, the component will re-render. This means that React will run the component's render function again to generate a new virtual DOM representation based on the updated state.
    
 In the case of your search bar component, even though it seems like only the text inside the search bar is changing, the entire component is being re-rendered each time the user types in a new character. This is because the `**value**` attribute of the input element is bound to the `**searchTerm**` state variable. So, whenever `**searchTerm**` changes, React re-renders the entire `**SearchBar**` component to reflect the updated state.
    
However, React is optimized to efficiently update the DOM, and it performs a process called reconciliation to determine the minimum number of changes needed to update the actual DOM. So, even though the entire component is being re-rendered, React will only update the parts of the DOM that have changed, in this case, the text inside the input field.
    
This behavior might seem like overkill for such a simple change, but it's a fundamental aspect of React's declarative programming model. By re-rendering the entire component, React ensures that the UI always reflects the current state of the application, making it easier to reason about and maintain the code. Additionally, modern JavaScript engines are highly optimized for updating the virtual DOM efficiently, so performance issues typically aren't a concern unless the component tree is very large or there are complex computations involved.

SEARCH BAR IS DONE NOW I'VE JUST TO SEARCH THE RESTURANT IN OUR LIST!


```javascript
const Body=()=>{
    const [restaurantList,setResturantList]=useState([]);
    const [filteredResturant,setFilteredResturant]=useState([]);
    const[searchText,setSearchText]=useState("");
    console.log("BODY RENDERING");
    useEffect(()=>{
        console.log("BODY RENDERED");
        fetchData();

    },[]);


    const fetchData=async()=>{
       const data =await fetch("https://www.swiggy.com/dapi/restaurants/list/v5?lat=12.9599618&lng=77.6131577&is-seo-homepage-enabled=true&page_type=DESKTOP_WEB_LISTING");
       const json=await data.json();
     setResturantList(json?.data?.cards[4]?.card?.card?.gridElements?.infoWithStyle?.restaurants);
     setFilteredResturant(json?.data?.cards[4]?.card?.card?.gridElements?.infoWithStyle?.restaurants);
    }
    if(restaurantList.length===0){
        return <Shimmer />
    }

    return (
        <div className="body">
            <div className="filter">
                <div className="search" >
                 <input type="text" className="search-box" value={searchText} onChange={(e)=>{
                    setSearchText(e.target.value)
                 }} />
                 <button className="search-btn" onClick={()=>{
                    // I need to search the resturatant and update the UI and Also get the text from the input 
                    const filteredResturant=restaurantList.filter(
                        (res)=>res.info.name.toLowerCase().includes(searchText.toLowerCase())

                    );
                    setFilteredResturant(filteredResturant);
                 }}  >Search</button>

                </div>
                <button className="filter-btn" onClick={()=>{
                     let filteredrestaurantList=restaurantList.filter(
                     (res)=>res.info.avgRating >4.5 
                    )
                    setResturantList(filteredrestaurantList);
                    console.log(filteredrestaurantList);
                    }}>Top Rated Resturants</button>
            </div>
            <div className="res-container">    
            {
              filteredResturant.map((resturant,index)=><RestaurantCard key={index} resdata={resturant}/>)
            }

            </div>
        </div>
    )
}
export default Body;
```
