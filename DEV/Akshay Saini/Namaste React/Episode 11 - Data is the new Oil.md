---
view-count: 2
Date: 2024-10-29T16:55:00
---
# HIGHER ORDER COMPONENTS 

Higher-Order Components (HOCs) in React are a powerful design pattern used to enhance the functionality of existing components. An HOC is a function that takes a component as an argument and returns a new component, typically with additional props or functionality. This pattern allows for code reuse, separation of concerns, and easier testing.

### Key Characteristics of HOCs:

1. **Function Signature**: An HOC is a function that accepts a component and returns a new component. For example: 

```javascript
const withExtraProp = (WrappedComponent) => {
    return (props) => {
        // Add additional props or functionality here
        return <WrappedComponent {...props} extraProp="someValue" />;
    };
};

```

2. **Reusability**: HOCs can be used to encapsulate common behavior that can be shared across multiple components, such as fetching data, handling authentication, or managing state.
    
3. **Composition**: HOCs can be composed together. You can apply multiple HOCs to a single component to layer additional functionality.
    
4. **Props Manipulation**: HOCs can add, modify, or filter props before passing them down to the wrapped component.
    
5. **Non-mutating**: HOCs do not modify the original component. They create a new component instead, preserving the original component's identity.


EX:
![Episode 11 - Data is the new Oil-20241029170709558.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241029170709558.webp)
The Difference Between these two Components is The Promoted label on The top!

->Now if The Restaurant id is even Then we can add Promoted label to it!!!!



![Episode 11 - Data is the new Oil-20241029173638443.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241029173638443.webp)


![Episode 11 - Data is the new Oil-20241029174938685.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241029174938685.webp)

-> TOH HIGHER ORDER FUNCTION KYA HAI EK NORMAL JS FUNCTION HAI AUR KYA HAI BASS!!!!!
-> NORMAL COMPONENT -> ENHANCED COMPONENT

## **difference between using `<RestaurantCard />` and calling `RestaurantCard()`**

### Example of a Functional Component

First, let’s define a simple functional component:

```javascript

const RestaurantCard = ({ name }) => {
    return (
        <div>
            <h2>{name}</h2>
        </div>
    );
};

```


### Using the Component in JSX

1. **Using `<RestaurantCard />`**:

When you use `<RestaurantCard name="Pizza Place" />`, you are creating an instance of the `RestaurantCard` component:



```javascript
const App = () => {
    return (
        <div>
            <h1>Restaurants</h1>
            <RestaurantCard name="Pizza Place" />  {/* This is how you use the component */}
        </div>
    );
};

```
- **What Happens**: React recognizes `<RestaurantCard />` as a component and calls the `RestaurantCard` function behind the scenes, passing the props (`{ name: "Pizza Place" }`) to it. React manages the lifecycle of this component, including rendering, updating, and unmounting.

### Calling the Function Directly

2. **Calling `RestaurantCard()` Directly**:

If you were to call it like this:


```javascript
const App = () => {
    return (
        <div>
            <h1>Restaurants</h1>
            {RestaurantCard({ name: "Pizza Place" })}  {/* This is NOT how you use the component */}
        </div>
    );
};
```


The difference between creating an instance of a component using JSX (e.g., `<RestaurantCard name="Pizza Place" />`) and calling the function directly (e.g., `RestaurantCard({ name: "Pizza Place" })`) lies in how React handles the component, its lifecycle, and rendering. Here’s a breakdown of the key differences:

### 1. **Lifecycle Management**

- **Creating an Instance with JSX**:
    - When you use `<RestaurantCard name="Pizza Place" />`, React manages the lifecycle of that component. This includes:
        - **Mounting**: React adds the component to the DOM.
        - **Updating**: React re-renders the component when props or state change.
        - **Unmounting**: React removes the component from the DOM when it is no longer needed.
- **Calling the Function Directly**:
    - When you call `RestaurantCard({ name: "Pizza Place" })`, you're bypassing React's lifecycle management. This means:
        - The component is not mounted in the React component tree.
        - React does not track updates or unmounting for that call.

### 2. **Rendering and Output**

- **Creating an Instance with JSX**:
    
    - React processes the JSX and creates a virtual DOM representation of the component. It then reconciles this with the actual DOM.
    - The component's return value (JSX) is rendered as part of the component tree.
- **Calling the Function Directly**:
    
    - The function returns JSX, but it is treated as a standalone value, not part of the React component tree. Thus, the output is not automatically rendered to the DOM.




```javascript 
// THIS FUNCTION WILL RETURN A NEW COMPONENT WITH THE PROMOTED LABEL
// THIS FUNCTION INPUT IS A COMPENT TOO
// COMPONENT IS A FUNCTION THAT RETURN JSX
export const withPromotedLabel=(RestaurantCard)=>{

    return(props)=>{
        return(
            <div>
                <label className="absolute bg-black text-white m-2 p-2 rounded-lg ">Promoted</label>
                <RestaurantCard {...props}/>
            </div>

        )
    }

}
```

TOH YE COMPONENT LE RAHA HAI AUR FIR EK RETURN KAR RAHA HAI!!!

    const RestaurantCardPromoted=withPromotedLabel(RestaurantCard);

->YAHAN HUMNE YE KIYA KI EK COMPONENT PASS KIYA AND USNE HUMEIN EK NAYA COMPONENT DE DIYA!!!
-> AB IS NAYE COMPONENT KO HUM USE KAR SKTE HAIN!!



```javascript
                {
                (resturant.info.id%2==0)?<RestaurantCardPromoted resdata={resturant}/>:<RestaurantCard resdata={resturant}/>
                }

```
YAHAN HUMNE NEW COMPONENT KO USE KIYA!!!


---

**->A REACT APPLICATION OF TWO LAYERS** 
1. **DATA LAYER**
2. **UI LAYER**

**->UI LAYER HOGAYI JSX WALA PART**
**-> DATA LAYER HOGAYI STATE,PROPS,AND OTHER JS PART**


HOW DO WE MANAGE OUR DATA PROPERLY!!!



## CONTROL AND UNCONTROLLED COMPONENTS

WHERE A PARENT COMPONENT IS CONTROLLING THE CHILD COMPONENT VIA PROPS THAT ARE BEING FROM THE PARENT COMPONENT TO THE CHILD!!!

RESTURANT MENU
![Episode 11 - Data is the new Oil-20241030084339941.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030084339941.webp)

![Episode 11 - Data is the new Oil-20241030084417175.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030084417175.webp)

->See We're Controlling the showItems from the Parent component! SO THIS IS A CONTROLLED COMPONENT

![Episode 11 - Data is the new Oil-20241030084703005.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030084703005.webp)

-> Here Restaurant Category is controlling Itself!!!! Toh uncontrolled hogya ye!

-> CAN A CHILD MAKE CHANGES IN A PARENT COMPONENT YES IT CAN BUT THE THING WE NEED TO PASS SOME FUCNTION FROM THE PARENT TO THE CHILD AND THEN THE FUNCTION CAN HELP US IN CHANGING THAT PARENT COMPONENT!

-> LIFTING THE STATE UPP


## **CONTEXT IN REACT**(REVISE)

PROPS DRILLING!!

->**REACT HAS ONE WAY DATA FLOW WHICH MEANS THE DATA FLOW FROM THE PARENT TO THE CHILD!!!!**
-> TOH COMPONENT1-> COMPONENT2-> COMPONENT3-> COMPONENT4 SABMEIN PROPS PASS KAR RAHA HUON!! TOH END MEIN JAHAN CHAHIYE WAHAN MUJHE MIL JAYEGA!

![Episode 11 - Data is the new Oil-20241030091334476.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030091334476.webp)

![Episode 11 - Data is the new Oil-20241030091352620.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030091352620.webp)
-> 2 -3 Levels ki drilling toh fir bhi sahi hai but usee jada deep drilling is not worth it!!!


**->So To Avoid the problem of passing props to the WE USE CONTEXT WHICH IS KIND OF A GLOBAL SPACE WHERE OUR DATA IS KEPT AND ANYBODY CAN ACCESS THAT**

-> LIKE WE NEED SOME DATA TO BE ACCESSED FROM ANYWHERE FROM OUR APP!!!
-> SO THERE IS A NEED OF SOMETHING THAT CAN PROVIDE THAT DATA FROM ANY COMPONENT LEVEL WHETHER IT IS A PARENT COMPONENT OR SOME GRANDCHILD COMPONENT!!!
->  FOR EXAMPLE: LOGIN INFORMATION CAN BE NEEDED ANYWHERE RIGHT!!!
-> It's like a global Object 
-> Bnate Kaise hain Isko???
-> React Gives us an important METHOD OR FUCNTION TO MAKE CONTEXT


-> WE CAN CREATE AS MANY CONTEXTS AS WE WANT!!!
![Episode 11 - Data is the new Oil-20241030094442498.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030094442498.webp)

HOW TO CREATE????




```javascript
import {createContext} from "react"

const UserContext= createContext({
    LoggedInUser:"Default User"
})

export default UserContext;

```

![Episode 11 - Data is the new Oil-20241030094557283.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030094557283.webp)
useContext ek Hook hai given by react to us!!

DATA THAT YOU FEEL CAN BE USED IN MULTIPLE PLACES SHOULD BE ADDED INTO CONTEXT

-> CLASS BASED COMPONENT MEIN HOOKS NAHI HOTE TOH IN THAT CASE WE CAN'T USE CONTEXT WITH IT!!!
![Episode 11 - Data is the new Oil-20241030095703490.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030095703490.webp)
AESE KARNA HOTA HAI


![Episode 11 - Data is the new Oil-20241030095743829.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030095743829.webp)


->CAN WE MODIFY THIS CONTEXT DEPENDING UPON SOME SITUATION

![Episode 11 - Data is the new Oil-20241030101054465.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030101054465.webp)

->Here I'm overriding The value of the default Context!!!

-> We Can Also Do this!!
![Episode 11 - Data is the new Oil-20241030101343815.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030101343815.webp)
-> YAHAN SIRF HEADER MEIN JAHAN DEFAULT VALUE HAI WOHI CHANGE HOGI!!!!


-> SO FOR EVEN SPECIFIC PORTION WE CAN JUST PROVIDE THE CONTEXT TOO!
-> NESTING OF CONTEXT

![Episode 11 - Data is the new Oil-20241030101710523.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030101710523.webp)

->
![Episode 11 - Data is the new Oil-20241030101901388.webp](../../Images/Episode%2011%20-%20Data%20is%20the%20new%20Oil-20241030101901388.webp)

ANOTHER WAY TO MODIFY THE CONTEXT!!!!

