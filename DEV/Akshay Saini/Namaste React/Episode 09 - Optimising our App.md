---
view-count: 4
Date: 2024-10-29T10:34:00
---
->The Single Responsibility Principle (SRP) is one of the five SOLID principles of object-oriented programming and design, focusing on the importance of structuring software in a way that promotes maintainability and scalability. The SRP states that a class or module should have only one reason to change, meaning it should have only one responsibility or job

LAYMEN BHASHA MEIN BOLUN TOH HAR FUNCTION/CLASS KI EK HI RESPONSIBILTY HONI CHAHIYE!!!
### Key Aspects of SRP

1. **Definition**:
    
    - A class should encapsulate only one responsibility, ensuring that it focuses on a single aspect of functionality. This reduces the likelihood of bugs and makes the class easier to understand and maintain.
2. **Benefits**:
    
    - **Maintainability**: Changes to one responsibility will not affect others, making it easier to update or modify the code.
    - **Reusability**: Classes with a single responsibility can be reused across different parts of an application or in other projects.
    - **Testability**: Classes with focused responsibilities are easier to test since each class can be tested independently of others.
    - **Readability**: Clear separation of concerns leads to code that is easier to read and understand.
3. **Example**:
    
    - Consider a class `Report` that generates reports, sends emails, and logs activities. This violates SRP because it has multiple responsibilities. Instead, you could break it down into:
        - `ReportGenerator`: Responsible for creating the report.
        - `EmailSender`: Responsible for sending the report via email.
        - `ActivityLogger`: Responsible for logging activities related to report generation.
    
    By separating these responsibilities, each class can evolve independently, making the overall system more robust

-> HAR COMPONENT KI EK SINGLE RESPONSIBILTY HONI CHAHIYE!!!!
-> WE SHOULD NOT DO MULTIPLE THINGS IN A SINGLE COMPONENT!!!
-> YAHAN MODULARITY ATI HAI ISSE CODE RESUABLE ,MAINTANIBLE AND TESTABLE BNTA HAI SINCE TEST EK HI COMPONENT KARNA ASAN HOGA VS KOI KHICDI SI PADI HO

---
## **HOOKS** 
->Hooks are Just Basic Utility Functions!!!
-> So What We could Do Extract some Functionality from the A component and give it to the Custom Hook!


YE HAI RESTURANT MENU COMPONENT
-> 1ST TASK ISKA YE HAI KI YE DATA FETCH KAR RAHA HAI
-> SECOND TASK ISKA YE HAI KI YE DATA SHOW KAR RAHA HAI AS THE MENU CARD
```javascript
import { useEffect,useState } from "react"
import Shimmer from "./Shimmer";
import{useParams} from "react-router-dom";
import { MENU_API } from "../utils/constants";
const RestaurantMenu = () => {
    const[resInfo,setResInfo]=useState(null);
    const [resMenu,setResMenu]=useState(null);
    const{resId}=useParams();
    useEffect(()=>{
        fetchMenu();
    },[])

    const fetchMenu= async()=>{
        const data=await fetch(MENU_API+resId);
        const json=await data.json();
        setResInfo(json.data.cards[2].card.card.info);
        setResMenu(json.data.cards[4].groupedCard.cardGroupMap.REGULAR.cards[2].card.card);
    }
    if(resInfo==null){
      return <Shimmer/>
    }
    const{name,costForTwoMessage,cuisines,totalRatingsString}=resInfo;
    const{itemCards}=resMenu;
  return (
    <div className="menu">
        <h1>{name}</h1>
        <h2>{costForTwoMessage}</h2>
        <h2>{totalRatingsString}</h2>
        <h2>{cuisines.join(", ")}</h2>
        <ul>
        {itemCards.map(item=><li key={item.card.info.id}>{item.card.info.name+"-Rs."}{item.card.info.price/100||item.card.info.defaultPrice/100 }</li>)}   
        </ul>

    </div>
  )
}

export default RestaurantMenu
```

->NOW WE'LL MAKE THE CUSTOM HOOK FOR THIS

->SO REMEBER THS WHENEVER YOU MAKE A CUSTOM HOOK, ALWAYS START THE NAME with "use" and FIR JO LIKHNA HAI LIKH DO
-> Utils mein likhte hain Hooks ko!!!!
-> So if the function name is starting from use Then React understand That It's a Hook!!

## CUSTOM HOOKS
Custom hooks in React are JavaScript functions that allow you to reuse stateful logic across multiple components. They start with the prefix `use`, which tells React that this function will use hooks (like `useState`, `useEffect`, etc.) inside.


### Purpose of Custom Hooks

React's built-in hooks, like `useState` and `useEffect`, work great for managing state and side effects within a single component. But when you want to **share stateful logic** (such as fetching data or handling forms) across multiple components, custom hooks are helpful. They let you **encapsulate this logic** in one place, making the code reusable and more organized.


### Why Use Custom Hooks?

1. **Code Reusability**: You can move logic that would otherwise need to be repeated across multiple components into a single custom hook.
2. **Separation of Concerns**: Custom hooks help separate the “what” (data fetching, event handling, etc.) from the “where” (specific UI components).
3. **Cleaner Code**: With complex logic encapsulated in custom hooks, component code becomes simpler and easier to read.


### How to Create a Custom Hook

A custom hook is just a function that can use other hooks like `useState`, `useEffect`, etc. Here’s a simple example of a custom hook that fetches data:


### Key Points to Remember

- Custom hooks can use other React hooks, and they must start with `use` to follow React’s naming convention.
- They do not directly render any UI; they only encapsulate logic.
- Custom hooks make it easy to reuse and share stateful logic across multiple components, improving modularity and maintainability.

### How Custom Hooks Affect UI Rendering

1. **State Sharing with Components**:
    
    - When you create state within a custom hook (e.g., using `useState` or `useReducer`), that state is directly tied to the component using the custom hook.
    - So, when the state in the hook changes, React treats it as if the component itself has state changes, triggering a re-render of that component.
2. **Encapsulated Logic Without UI**:
    
    - Custom hooks encapsulate logic (like data fetching, validation, or complex calculations) without directly involving UI elements.
    - They simply return state and functions to the component that can then decide how to use this data to render specific UI elements.
3. **Re-rendering Mechanism**:
    
    - Since custom hooks are just functions, when a component re-renders, it re-invokes the hook, receiving updated state and effects.
    - The component is responsible for rendering the UI based on these returned values. When the custom hook’s state changes, React knows that the component using this hook has an update, and thus, it re-renders the component with the latest state.




CONTRACTS KI TERMS MEIN DEKHO!!!

```javascript
const useRestaurantMenu=(resId)=>{


    return resInfo;
}
```

->Ache Se Dekhoge! Toh samajh aega ki kI HUM CHAHTE KYA HAI YAHAN!!!
-> HUM KARWANA KYA CHAHTE HAIN
-> AESE SAWAL PUCH KAR WE CAN DECIDE THE CONTRACT HERE

-> RES ID LEGA AND THEN USS RESTURANT KI INFORMATION BHEJ DEGA VAPIS!!!!



-> YE HAI HMARA CUSTOM HOOK!!!!
```javascript
import { useEffect, useState } from "react";
import { MENU_API } from "./constants";
const useRestaurantMenu=(resId)=>{
    const[resInfo,setResInfo]=useState(null);
    const [resMenu,setResMenu]=useState(null);

    useEffect(()=>{
        fetchMenu();
    },[])

    const fetchMenu= async()=>{
        const data=await fetch(MENU_API+resId);
        const json=await data.json();
        setResInfo(json.data.cards[2].card.card.info);
        setResMenu(json.data.cards[4].groupedCard.cardGroupMap.REGULAR.cards[2].card.card);

    }
    return [resInfo,resMenu];
}
export default useRestaurantMenu;  
```


The re-render happens in `RestaurantMenu` even though the state variables (`resInfo` and `resMenu`) are in the custom hook because **React re-renders a component whenever any of its hook states or props change**. Here’s why this applies even when the state is managed within a custom hook.

### Why `RestaurantMenu` Re-renders with State in a Custom Hook

1. **State in a Hook is Tied to the Component Using It**:
    
    - When `RestaurantMenu` calls `useRestaurantMenu`, it’s as if `resInfo` and `resMenu` are part of `RestaurantMenu`'s state.
    - Custom hooks are essentially a way to share logic across components, but they don’t isolate state; instead, the hook’s state is tied directly to the component that calls it.
2. **State Update in Hook Triggers a Component Re-render**:
    
    - When `fetchMenu` updates `resInfo` and `resMenu` in the hook, React’s state management system detects that `RestaurantMenu` has a dependency on these state variables.
    - React re-renders `RestaurantMenu` so it can access the updated values of `resInfo` and `resMenu`.
3. **Custom Hook Acts Like a Function**:
    
    - Think of the custom hook as a function that organizes state and effects but doesn’t isolate them from the component. It’s simply a way to encapsulate logic.
    - So, when `useRestaurantMenu` updates `resInfo` and `resMenu`, React treats this as if `RestaurantMenu` had local state updates, triggering a re-render.


## CUSTOM HOOK TO TELL IF We're online or offline 

![Episode 09 - Optimising our App-20241029121513308.webp](../../Images/Episode%2009%20-%20Optimising%20our%20App-20241029121513308.webp)



```javascript
import { useState,useEffect } from "react"
const useOnlineStatus=()=>{
const[onlineStatus,setOnlineStatus]=useState(true);

useEffect(()=>{
    const handleOffline = () => {
        setOnlineStatus(false);
    };

    const handleOnline = () => {
        setOnlineStatus(true);
    };

    setOnlineStatus(navigator.onLine);

    window.addEventListener("offline", handleOffline);
    window.addEventListener("online", handleOnline);

    return () => {
        window.removeEventListener("offline", handleOffline);
        window.removeEventListener("online", handleOnline);
    };

},[]);
return onlineStatus;
}
export default useOnlineStatus;
```

CUSTOM HOOK K NAMES MEIN USE DALNA HI SAHI TARIKA HAI


---
->LAST 30 Minutes mujhe lage bakchod revison mein cover karna 
-> 


![Episode 09 - Optimising our App-20241029131933137.webp](../../Images/Episode%2009%20-%20Optimising%20our%20App-20241029131933137.webp)


CHUNKING/CODE SPLITTING

->To break down our app in smaller chunks! We Do this!!
LAZY LOADING 