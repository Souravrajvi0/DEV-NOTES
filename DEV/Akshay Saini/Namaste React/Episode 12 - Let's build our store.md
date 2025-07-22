---
view-count: 1
---
# REDUX(REVISE)

Redux Works In the Data layer!
![Episode 12 - Let's build our store-20241030104859307.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030104859307.webp)

Anything That can Be built without using REDUX also!!!

Use It Only When it's required!!

**React** Is library Used for managing State!!.But there are another libraries also present that can be used to manage states like **ZUSTAND**

When we use redux it gets easier to debug!!

REDUX OFFERS STATE MANAGEMENT DOESN'T HAVE TO BE NECCESARILY WITH REACT ONLY CAN ALSO BE USED WITH OTHER LIBRARIES AS WELL!!!



![Episode 12 - Let's build our store-20241030105642837.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030105642837.webp)
![Episode 12 - Let's build our store-20241030105719244.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030105719244.webp)
Pehle We used to write in vanilla redux but now we write using **REDUX TOOLKIT**

![Episode 12 - Let's build our store-20241030110005869.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030110005869.webp)
REDUX TOOL KIT-> RTK


->HERE WE ARE GOING TO BUILD THE CART FEATURE OF THE FOOD APP!!!!

BASIC IDEA OF THE TASK IS 

![Episode 12 - Let's build our store-20241030110723287.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030110723287.webp)


WHAT IS A REDUX STORE????

It's like a really big JavaScript object that is kept at a global place!!!
So any component inside our application can access this store. It can read and write data from this store and we keep all our data (mostly) in this store!

Is it a good practice to keep all the data in a single JS object?? Yeah Well there's nothing wrong with it but still if our store doesn't bloat with too much data!! We have slices in our store.

We can assume Slices as small portion of the REDUX STORE 
![Episode 12 - Let's build our store-20241030111800509.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030111800509.webp)

 So if we have to add Cart data to our redux store we'll create a separate slice!!!, Same Can be done for LoggedIn User data also! We can create a separate Slice for it in the Redux Store!
Theme Related data also Be Stored!
![Episode 12 - Let's build our store-20241030111830924.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030111830924.webp)
## HOW TO WRITE DATA IN THE STORE 
We Can't directly modify the cart Slice!!

![Episode 12 - Let's build our store-20241030112108155.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030112108155.webp)

1. When we click on the button it **DISPATCHES AN ACTION**
2. This **Action calls a function(REDUCER)**
3. This **function will internally modify the store/update the slice of the redux store**
4. Then our slice will be updated
 
**This function is known as REDUCER**


## HOW TO READ DATA FROM THE STORE 


![Episode 12 - Let's build our store-20241030112757002.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030112757002.webp)

For this we use **SELECTOR**

![Episode 12 - Let's build our store-20241030112940459.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030112940459.webp)

So here we'll say that our header component is **SUBSCRIBED** to our store 
**When I say header component is subscribed to our store it means that it is sync with our store** 

If the data in out store changes my header component will change automatically!

## HOW DO WE SUBSCRIBE???

##### USING SELECTOR


## **BASIC DIAGRAM OF HOW THINGS WORK!!**

![Episode 12 - Let's build our store-20241030113727008.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030113727008.webp)


---



![Episode 12 - Let's build our store-20241030114326851.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030114326851.webp)

**INTALLATION COMMANDS!**

`npm i @reduxjs/toolkit`

`npm i react-redux`

**CREATION OF STORE**

```javascript
import { configureStore } from "@reduxjs/toolkit";

const appStore=configureStore({});
// Configure store creates the store 

export default appStore;
```
Configuring The store is the job of the RTK so configure comes there 
**PROVIDING STORE TO THE APPLICATION**

`import { Provider } from "react-redux";`
**Provider comes from react-redux library not from rtk!!!**

Providing the store to the react application is the job of react-redux library!


```javascript

const AppLayout= ()=>{
    return(
        <Provider store={appStore}>
         <div className="app">
         <Header/>
         <Outlet/>
         </div>
        </Provider>
    )
}
```
Depending upon the Circumstances we can provide the redux to specific part of the App also!


**CREATING THE SLICES NOW** 

```javascript
import { createSlice } from "@reduxjs/toolkit";

const cartSlice=createSlice({
    name:"cart",
    initialState:{
        items:[]
    },
    reducers:{
        addItem:()=>{

        },
        removeItem:()=>{

        },
        clearCart:()=>{
            
        }
    }
});

export const{addItem,removeItem,clearCart}=cartSlice.actions
export default cartSlice.reducer

```


### 1. **Importing `createSlice`**

`import { createSlice } from "@reduxjs/toolkit";`

`createSlice` is a function from Redux Toolkit that lets you easily create a Redux slice. A slice represents a portion of the Redux state, along with the reducers and actions associated with it.

## 2.Defining Slice 


```javascript
const cartSlice = createSlice({
    name: "cart",
    initialState: {
        items: [],
    },
    reducers: {
        // Reducer functions here
    },
});

```

- **`name`**: The name of this slice of the state, which is "cart".
- **`initialState`**: Defines the initial state of the slice. Here, `items` is initialized as an empty array, representing an empty shopping cart.

### 3. **Reducers**

The `reducers` object contains functions that define how the state should change in response to different actions. Here, we have three reducers:

**`addItem`**:
```javascript
addItem: (state, action) => {
    state.items.push(action.payload);
},

```

This function takes the current `state` and an `action` object as arguments. It pushes the `payload` (data from the action) into the `items` array. This simulates adding an item to the cart.

**`removeItem`**:
`removeItem: (state) => { state.items.pop(); },`

This function removes the last item in the `items` array by calling `pop`. This simulates removing the most recently added item from the cart.


**`clearCart`**:
`clearCart: (state) => {     state.items.length = 0; },`

This function clears the cart by setting `items.length` to `0`, effectively emptying the array.
->I didn't do state.items=[] won't work

### 1. Exporting the Actions

`export const { addItem, removeItem, clearCart } = cartSlice.actions;`

- **Purpose**: This line extracts and exports the action creators `addItem`, `removeItem`, and `clearCart` from `cartSlice`.
- **Why?**: In Redux Toolkit, `createSlice` automatically generates action creators for each reducer function you define. By exporting these actions, you can import and use them in your components to dispatch actions that modify the cart's state.
- **Usage**: In a component, you might use these actions like so:

```javascript

import { addItem, removeItem, clearCart } from './pathToSlice';
dispatch(addItem(item)); // Adds an item to the cart
dispatch(removeItem());  // Removes the last item from the cart
dispatch(clearCart());   // Clears all items in the cart

```

### 2. Exporting the Reducer


`export default cartSlice.reducer;`

- **Purpose**: This line exports the reducer function from `cartSlice` as the default export.
- **Why?**: The reducer is needed to update the Redux store’s state when actions are dispatched. By exporting it, you allow this reducer to be added to the Redux store in the root reducer.
- **Usage**: Typically, you’ll import this default export in your store configuration and combine it with other reducers if needed:


```javascript
import cartReducer from './pathToSlice';

const store = configureStore({
  reducer: {
    cart: cartReducer,
    // other reducers can go here
  },
});

```
 

- **Actions (`addItem`, `removeItem`, `clearCart`)**: Exported as named exports so you can easily import and dispatch them in components.
- **Reducer**: Exported as the default export so you can integrate it into your Redux store, allowing it to handle dispatched actions and update the cart state accordingly.

cartSlice object aesa dikhega isliye aese kiya hai maine ki! DESTRUCTURING BHI KAR DI EXPORT KARTE VAQT ACTIONS K SATH
![Episode 12 - Let's build our store-20241030124153208.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030124153208.webp)

### 3.AFTER BUILDING THE SLICE TO THE STORE

THE MAIN STORE ALSO HAS IT'S REDUCERSS!!
![Episode 12 - Let's build our store-20241030125757972.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030125757972.webp)
->Ek bada reducer hai and that contains the other reducers!!

![Episode 12 - Let's build our store-20241030131951804.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030131951804.webp)
->if you are exporting `cartSlice.reducer`, you correctly import it as `cartReducer` in your store configuration. There’s no inconsistency; it’s just a naming choice.


### Explanation:

1. **`const appStore`**:
    
    - This line declares a constant variable named `appStore` that will hold the configured Redux store.
2. **`configureStore({...})`**:
    
    - This function is provided by Redux Toolkit. It simplifies the store configuration process by setting up a store with good default settings.
    - Inside the parentheses, you pass an object that contains various configurations for the store.
3. **`reducer: {...}`**:
    
    - The `reducer` key in the configuration object specifies how the state of the application will be managed.
    - It takes an object where each key represents a slice of the state, and the corresponding value is the reducer function that manages that slice.
4. **`cart: cartSliceReducer`**:
    
    - Here, you are defining a slice of the state called `cart`.
    - The value `cartSliceReducer` is the reducer function imported from your `cartSlice.js`. This function will handle actions related to the `cart` state.
    - Essentially, this means that any actions dispatched that pertain to the `cart` will be handled by the logic defined in `cartSliceReducer`.



## HOW TO READ THE DATA FROM THE CART




We'll Use a selector To subscribe to the store!!

WHAT IS SELECTOR??? 
A selector is nothing but a HOOK in react!

SELECTOR HELPS US SUBSCRIBE TO SOME PORTION!!!
IN HEADER

    const cartItems=useSelector((store)=>store.cart.items)

       <li className="px-4 ">  {"🛒"+" "+cartItems.length}  </li>



NOW LET'S SEE THE WHOLE CYCLE AGAIN

![Episode 12 - Let's build our store-20241030141854106.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030141854106.webp)

WHEN YOU DISPATCH ONE ACTION THIS IS WHAT REDUX DO


![Episode 12 - Let's build our store-20241030142009926.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030142009926.webp)

And give it to the reducer function this object specified above!!




NOW PASSING THE BUTTON DATA IN THE CART!

1. **`onClick={handleAddItem}`**
    
    - This syntax simply passes the `handleAddItem` function as a reference to the `onClick` handler. When the button is clicked, `handleAddItem` will be called without any arguments.
    - This is commonly used when the function doesn’t need any parameters.
    - In your example, `handleAddItem` would execute and log `"clicked"` to the console and dispatch an action with `"ITEM"`.
2. **`onClick={() => handleAddItem(item)}`**
    
    - This syntax uses an **arrow function** to call `handleAddItem` with `item` as an argument when the button is clicked.
    - Here, the arrow function wrapper ensures that `handleAddItem(item)` is only called on a click event, passing `item` as a parameter.
    - This is useful if `handleAddItem` needs additional data (`item` in this case) at the time it’s called.

### Why Use an Arrow Function in the Second Example?

If `handleAddItem` requires a parameter, you can’t directly pass `handleAddItem(item)` to `onClick` because that would immediately call `handleAddItem` during rendering. Wrapping it in an arrow function `() => handleAddItem(item)` delays the call until the `onClick` event is triggered.



HOW TO READ DATA FROM STORE??




![Episode 12 - Let's build our store-20241030160939137.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030160939137.webp)
Never Do this !!
->This is not very efficient Because we're subscribed to the whole store and decreases the efficiency 
-> Always Subscribe to a small portion of the store!!


![Episode 12 - Let's build our store-20241030161628653.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030161628653.webp) 
Upar Reducers and niche reducer hai bhai!!!

![Episode 12 - Let's build our store-20241030161728906.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030161728906.webp)



VANILLA REDUX
![Episode 12 - Let's build our store-20241030162244012.webp](../../Images/Episode%2012%20-%20Let's%20build%20our%20store-20241030162244012.webp)
