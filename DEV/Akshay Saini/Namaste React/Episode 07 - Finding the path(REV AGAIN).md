---
view-count: 4
Date: 2024-10-28T16:26:00
---
## **USE EFFECT HOOK**

---



![Untitled 69.png](../../Images/Untitled%2069.png)

→So when is this useEffect called After every render of this component!
->It’s not Mandatory to Use a dependency array! Only the callback function is mandatory inside the useeffect Function!


![Untitled 1 59.png](../../Images/Untitled%201%2059.png)

![Untitled 2 45.png](../../Images/Untitled%202%2045.png)

![Untitled 3 41.png](../../Images/Untitled%203%2041.png)

![Untitled 4 38.png](../../Images/Untitled%204%2038.png)

-> If you try to make/ use useState Hook Outside the functional component then ERROR WILL COME
-> BAT SAHI BHI HAI KISKI STATE REACT TRACK KAREGA BHAI?? WHEN THEY ARE CREATED OUTSIDE
-> USESTATE KA EK SPECFIC USE HOTA HAI!!! IT IS USED TO CREATE STATE VARIABLES INSIDE YOUR FUCNTIONAL COMPONENT THEN BHAI BAHAR KYON HI BANAEGA TU
### Why UseState Must Be Inside Functional Components

1. **React's Rules of Hooks**:
    
    - React has a set of rules called **"Rules of Hooks"**, which state that hooks can only be called at the top level of a React function component or from within custom hooks. This ensures that hooks are called in the same order every time a component renders.
2. **Tracking State**:
    
    - When you call `useState`, React creates and tracks the state for that specific component instance.
    - If you try to call `useState` outside of a functional component, React does not have a component instance to attach that state to. It wouldn’t know which component’s state to track, leading to confusion.

![Untitled 5 33.png](../../Images/Untitled%205%2033.png)

→It’s a good practice to make all the state variables at the start of the Component!

![Untitled 6 31.png](../../Images/Untitled%206%2031.png)

![Untitled 7 26.png](../../Images/Untitled%207%2026.png)

![Untitled 8 23.png](../../Images/Untitled%208%2023.png)

→Never Make state variables inside the if or else block! or for loop or inside a function

# **ROUTING**

**React Router DOM** is a package that contains bindings for using React Router in web applications
→So whenever we have to develop Routes, We need to create routing configuration!

![Untitled 10 17.png](../../Images/Untitled%2010%2017.png)

**React Router DOM** is a library that enables navigation and routing in React applications. It allows you to create a single-page application (SPA) with dynamic routing capabilities, making it easy to manage multiple views without reloading the entire page


### How SPAs Work

1. **Single HTML Page**:
    
    - An SPA loads a single HTML page initially. This page contains the core structure of the application.
2. **Dynamic Content Loading**:
    
    - Instead of loading new HTML pages from the server when you navigate to different sections (like in traditional multi-page applications), SPAs use JavaScript to dynamically update the content on the same page.
    - When you click a link or perform an action, the SPA fetches the necessary data (often via AJAX or Fetch API) and updates only the relevant parts of the page.
3. **Client-Side Routing**:
    
    - SPAs use client-side routing (e.g., with libraries like React Router) to manage navigation. This means that the URL can change based on the user's actions, but the browser does not perform a full page reload.
    - The application keeps track of the user's location (e.g., `/about`, `/profile`) and updates the view accordingly.


### Why React Router DOM is Used

1. **Single-Page Applications (SPA)**:
    
    - In SPAs, content is dynamically updated as users interact with the app without full page reloads. React Router allows for smooth transitions between different views of the application.
2. **Navigation**:
    
    - It enables developers to create navigation links and manage different routes efficiently, providing a better user experience.
3. **Dynamic Routing**:
    
    - React Router allows for dynamic routing, meaning the routes can be defined based on user actions or data fetched from an API.
4. **URL Management**:
    
    - It manages browser history and URLs, allowing users to navigate through the application using the back and forward buttons, as well as bookmarking specific views.




### When React Router DOM is Used

- **When Building SPAs**: React Router is commonly used when building single-page applications that require navigation between different components or pages.
- **When You Need Dynamic Routing**: If your application has views that need to change based on user input or data (e.g., user profiles, product details), React Router is essential.
- **When You Want to Manage URL State**: If you need to reflect application state in the URL (like displaying specific content or user data), you should use React Router.




When you use `createBrowserRouter` in React Router DOM, you're setting up a more modern and flexible way to define routes for your React application. This function creates a router object that handles your app’s routing using the browser's history API, which means it will behave like a traditional multi-page application with a clean URL structure, but without actual page reloads.


### Why We Use `createBrowserRouter`

- **Declarative Routing**: `createBrowserRouter` allows you to define routes and their structure more declaratively in a single place. This simplifies your routing setup and makes it easier to manage.
- **Data Fetching & Error Handling**: With `createBrowserRouter`, you can more easily integrate data fetching and error handling for specific routes, making it especially useful for complex or data-driven applications.
- **Route-Based Code Splitting**: You can define which components should load for each route, helping with lazy loading (code splitting) to improve performance

### What `createBrowserRouter` Does

The `createBrowserRouter` function takes an array of route objects, where each object specifies:

1. The **path** for the route.
2. The **element** (or component) to render when the path matches the URL.
3. Optionally, data fetching, error handling, or even nested routes

Here’s how it works:

1. **Create a Router Object**: When you call `createBrowserRouter`, it creates an object that React Router DOM uses to handle the routing for your application.
2. **Handle URL Changes**: This router object listens to changes in the URL. When the user navigates to a different path, it updates the view to match the route configuration.
3. **Renders Components for Each Route**: Based on the defined paths, it renders the specific component(s) associated with the current URL.

### Example of `createBrowserRouter` Usage


```javascript
import { createBrowserRouter, RouterProvider } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import ErrorPage from './components/ErrorPage';
import UserProfile from './components/UserProfile';

const appRouter = createBrowserRouter([
    {
        path: "/",
        element: <Home />,     // Renders Home component at "/"
        errorElement: <ErrorPage />, // Shows if there's an error loading the route
    },
    {
        path: "/about",
        element: <About />,    // Renders About component at "/about"
    },
    {
        path: "/user/:userId",
        element: <UserProfile />, // Renders UserProfile component for dynamic user paths like "/user/1"
    },
]);

const App = () => {
    return (
        <RouterProvider router={appRouter} />
    );
};

export default App;
```

### How This Code Works

1. **Define Routes**: `createBrowserRouter` is given an array of route objects, each with a path and component (element) to render.
    - When the path in the URL matches a route's path, React Router renders the specified component.
2. **Dynamic Parameters**: With paths like `/user/:userId`, it allows for dynamic URLs by defining URL parameters. Here, `userId` can be accessed within the `UserProfile` component to show user-specific data.
3. **Error Handling**: You can define an `errorElement` for any route to render in case of issues (e.g., if data fetching fails or the component can’t load).
4. **Rendering with RouterProvider**: The `RouterProvider` component takes the router (created by `createBrowserRouter`) and enables routing in the app. This setup allows React Router DOM to manage navigation, rendering, and history management.

### Explanation of below Part

1. **`const App = () => { ... }`**:
    - This defines a functional component called `App`.
    - In React, functional components are used to return UI elements, often in the form of JSX, and they render whenever they are called or their internal state/props change.


2.**`<RouterProvider router={appRouter} />`**:

- `RouterProvider` is a special component from React Router DOM that enables routing within this `App` component.
- It takes in a `router` prop, which is an instance of the `appRouter` object (defined separately), that specifies how routing should work throughout the app.
- This `RouterProvider` component makes the defined routes available to the entire application, allowing React Router to handle URL changes and render the appropriate components.

3.**`router={appRouter}`**:

- The `appRouter` object, defined elsewhere using `createBrowserRouter`, contains all the route configurations for the app.
- By passing `appRouter` to `RouterProvider`, React Router DOM will use these route definitions to control which components are displayed based on the current URL.
- For example, if `appRouter` contains a route for `/about` that points to an `About` component, then when the URL matches `/about`, React Router DOM will render that component.
### How This Code Works Together

- **Enable Routing**: Wrapping the entire app in `RouterProvider` connects the application to React Router, enabling all defined routes to work as expected.
- **Render Dynamic Components**: Based on the current URL, `RouterProvider` consults `appRouter` to find the right component(s) to render.
- **Centralize Routing Logic**: The routing setup is centralized in one place, making it easy to manage navigation across the application. All route-related logic and configurations are handled by `appRouter`, so this `App` component doesn’t need to manage individual routes directly.


→HERE BASICALLY WE'RE CREATING THE CONFIGURATION
![Untitled 11 15.png](../../Images/Untitled%2011%2015.png)

->First ,we need to create the routing configuration so here createBrowserRouter() Takes in a list of paths !
→RouterProvider Provides/gives our configuration to our app!
→After Creating this We need to provide this for renedering!

![Untitled 12 13.png](../../Images/Untitled%2012%2013.png)

→RouterProvider ek component hi hai!

![Untitled 13 7.png](../../Images/Untitled%2013%207.png)

->aur uske andar hum apna appRouter pass kar denge!

→we can even add error element to it
-> RAFCE IS A VS CODE SHORT CUT TO GET THE COMPONENT
![Untitled 14 5.png](../../Images/Untitled%2014%205.png)
->When I entered Some Ajeeb sa URL!// THIS COMES REACT ROUTER DOM SE AARA HAI YE
![Episode 07 - Finding the path-20241028151634975.webp](../../Images/Episode%2007%20-%20Finding%20the%20path-20241028151634975.webp)
→TO ADD AN ERROR ELEMENT AND WE CAN JUST MAKE A NEW ERROR COMPONENT
![422](../../Images/Episode%2007%20-%20Finding%20the%20path-20241028152135225.webp)


-> ANOTHER FUNCTIONALITY IN TERMS OF ERROR!

![Untitled 15 4.png](../../Images/Untitled%2015%204.png)

-> React mein mostly saare hook use se chalu hote hain!
-> But Ise Pehle ise react-router-dom se import karna padta hai!
→UseRouteError hook can be used to get extra information about the error!
The `useRouteError` hook is a utility in React Router (v6.4 and newer) that allows you to handle errors in your routes. It’s particularly useful for displaying custom error messages or components when a route fails to load, such as when there’s an error fetching data, or an invalid route is accessed.

- **How It Works**:
    
    - When a route throws an error (for example, if data loading fails or a `throw` statement is triggered), React Router catches it.
    - You can use `useRouteError` to retrieve this error within your error-handling component and display an appropriate message.
- **Where to Use It**:
    
    - Use `useRouteError` within components dedicated to error handling in your route definitions.
    - These components are typically set in your router configuration as _error elements_ for specific routes, so they’re displayed only when an error occurs.

---
->PROBLEM IS -> EVERY TIME I GO TO MY A DIFFERENT ROUTE I LOOSE MY HEADER AND FOOTER!??? THIS SHOULDN'T BE HAPPENING
-> WHAT I NEED IS HEADER TO STAY BUT THE BODY WILL CHANGE DEPENDING UPON THE ROUTE
-> To get this functionality we need to create Children Routes!
# **CHILDREN ROUTE**

→What if we want the header to stay and The content down should change! Mtlb ki if i want to go to the contact us page my header should remain there! But uske niche wala content change hojana chahiye!

```javascript
const AppLayout= ()=>{
    return(
        <div className="app">
        <Header/>
        <Outlet/>
        </div>
    )
}
const appRouter=createBrowserRouter([
    {
        path:"/",
        element:<AppLayout/>,
        children:[
            {
                path:"/",
                element:<Body/>

            },
            {
                path:"/about",
                element:<About/>
            },
            {
                path:"/contact",
                element:<Contact/>
            }

        ],
        errorElement:<Error/>
    },
  
]);
```

→ We need to import outlet too
![Untitled 18 4.png](../../Images/Untitled%2018%204.png)
-> So Whenever The case arises This outlet is replaced by the component!
-> So in HTML WE WON'T EVEN KNOW THAT THE OUTLET EXISTED IN THE FIRST PLACE!

---

# Linking different pages!

![Untitled 19 4.png](../../Images/Untitled%2019%204.png)
-> We Can't do This!
**-> While working with react and we want to route some other page NEVER USE ANCHOR TAG!**
-> Because the whole page will get refreshed!
->IN REACT WE CAN NAVIGATE TO A DIFFERENT TO A PAGE WHILE RELOADING THE WHOLE PAGE!
-> React Lets us navigate between different pages without loading the whole page!

![Untitled 20 4.png](../../Images/Untitled%2020%204.png)

```javascript
  <div className="header">
            <div className="logo-container">
             <img className="logo" src={LOGO_URL}/>
            </div>
            <div className="nav-items">
                <ul>
                    <li><Link to="/">Home</Link></li>
                    <li><Link to="/about">About Us</Link></li>
                    <li><Link to="/contact">Contact Us</Link></li>
                    <li>Cart</li>
                    <button className="login-button" onClick={()=>{
                      btnchnager();
                    }}>{btn}</button>
                </ul>
            </div>
        </div>

```

→Link will work same as anchor tag but the real deal here is the page won’t refresh while we navigate to other pages!

---

->**THIS IS WHY EVERYTHING REACT APPLICATIONS ARE KNOWN AS SINGLE PAGE APPLICATIONS!**
->SO BASICALLY YAHAN PAR PAGE EK HI HAI AND COMPONENTS INTERCHANGE HO RAHE HAI SAME PAGE K ANDAR
-> SO HUA NA YE EK SINGLE PAGE APPLICATION

---

Server-side routing and client-side routing are two approaches used in web development to manage how URLs (Uniform Resource Locators) are handled within a web application.

1. **Server-side routing**:
    - In server-side routing, the routing logic is handled by the web server. When a user makes a request to a particular URL, the server determines which resources to serve based on the URL.
    - The server generates HTML pages dynamically based on the requested URL and sends the complete page back to the client.
    - Each time a new page is requested, the server reloads the entire page, resulting in a full page refresh.
    - This approach is common in traditional web applications built with server-side technologies like PHP, Ruby on Rails, Django, and Express.js (with server-side rendering).
2. **Client-side routing**:
    
    - In client-side routing, the routing logic is handled by JavaScript running in the user's browser rather than on the server.
    - When the user navigates to a new URL within the application, the JavaScript code intercepts the request, prevents the default browser behavior (full-page refresh), and instead updates the content of the page dynamically.
    - This approach is commonly used in single-page applications (SPAs) where the initial HTML is loaded once, and subsequent navigation and content updates are handled by JavaScript.
    - Client-side routing frameworks like React Router for React.js, Vue Router for Vue.js, and Angular Router for Angular provide tools to implement client-side routing effectively.
    
    ---

# MENU

```javascript
const RestaurantMenu = () => {
  return (
    <div className="menu">
        <h1>NAME OF THE RESTURANT</h1>
        <h2>MENU</h2>
        <ul>
          <li>ITEM1</li>
          <li>ITEM2</li>
          <li>ITEM3</li>
        </ul>

    </div>
  )
}
export default RestaurantMenu
```


->NOW THIS IS LIKE A TEMPLATE COMPONENT WE WILL CREATE!
-> Jaise glass mein daru bhi dal skte hain,MILK BHI,WATER BHI,HONEY BHI ETC!!! WAISE HI YAHAN TEMPLATE MEIN HAR RESTURANT KA DATA AEGA! USKO DALO AND DONE!!!
-> We will load this component on some specific route! Which in turns! like some route -> resturant/id

NOW FOR PATH WE CAN DO THIS


```javascript
path:"/",
        element:<AppLayout/>,
        children:[
            {
                path:"/",
                element:<Body/>

            },
            {
                path:"/about",
                element:<About/>
            },
            {
                path:"/contact",
                element:<Contact/>
            },
            {
                path:"/restaurant/:resId",
                element:<RestaurantMenu/>

            }

        ],


```


-> UseEffect and useState Component Specific bat karte hain hamesha! Mtlb Hamesha context Hona Hi chahiye apke pass!


-> Key Hamesha Parent JSX ELEMENT MEIN DALNI HOTI HAI
-> LINK COMPONENT BEHIND THE SCENES ANCHOR TAG HI USE KARTA HAI, LINK IS A WRAPER OVER ANCHOR TAG
