---
view-count: 4
---
INTERVIEW MEIN  KABHI KABHI PUCHLETE HAIN!

# **CLASS BASED COMPONENTS→**

**What is a class based Component?? It's a normal JavaScript Class**

  Class-based components are an older way to define components in React, before the introduction of functional components with hooks in React 16.8. Though modern React primarily uses functional components, class-based components are still used in legacy codebases, and understanding them can be useful for working with older projects.

  ### Basic Structure of a Class Component

Class components are ES6 classes that extend `React.Component`. They have access to lifecycle methods, state management, and `this` context, which gives them a different feel from functional components.
-> When We class UserClass(name of The component) extends React.Component , Then React Starts Tracking this  component!
-> render method will return piece of JSX with the help of return  keyword!
-> Jabh import karte vaqt bhi destructure kar skte haiin
```
 import{Component} from "react";
```

  

![Untitled 68.png](../../Images/Untitled%2068.png)



**Class-based Components:**

1. **Syntax**: Class-based components are defined using ES6 classes that extend `**React.Component**`.
2. Here we have a **render()** method that returns a piece of JSX
3. `React.Component` is a class given to us by react! and our Userclass extends some of it’s properties!
4. We need to import this REACT to use this!

![Untitled 1 58.png](../../Images/Untitled%201%2058.png)
-> Export and Import of this class is same as Functional Based Components!

---

# **Props**

->In functional Components we send Props Like this!
![Episode 08 - Let's get Classy-20241028200629438.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241028200629438.webp)
->And Receive Like this 
![Episode 08 - Let's get Classy-20241028200711639.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241028200711639.webp)

-> Props wo object mein stuff karke bhejta hai toh destructure on the fly kar diya

**NOW IN CLASS BASED COMPONENTS WE DO THIS** 
![Episode 08 - Let's get Classy-20241028200826281.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241028200826281.webp)
->Bhejne ka tarika toh same sa hi hai!
-> Constructor mein receive karte hain props!
![Episode 08 - Let's get Classy-20241028201333672.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241028201333672.webp)
In React class components, `super(props)` is required in the constructor when you’re extending from `React.Component`. This is because `super` calls the constructor of the parent class (`React.Component`) so that your component can inherit its properties and behavior. By passing `props` to `super`, you allow the base `React.Component` class to initialize `this.props` in your component.

### Why `super(props)` Is Needed

1. **Initialize `this.props`**: When you pass `props` to `super`, React can initialize `this.props` within the component. Without this, `this.props` won’t be accessible inside the constructor, which could lead to errors if you try to use it before calling `super(props)`.
    
2. **Required for Class Inheritance in JavaScript**: In JavaScript, when you extend a class and create a constructor, you need to call `super()` before you can use `this` in the constructor. Not calling `super` will result in an error, as `this` must be initialized by the parent class before use.
-> YAHAN PAR this.props object jo hai na wo contain karega jo chizen maine pass ki thi!


```javascript 
import React from "react";
class UserClass extends React.Component{
    constructor(props){
        super(props);
    }

    render(){
        const{name,location}=this.props;
        return <div className="user-card">
        <h2>Name from CP:{name}</h2>
        <h3>Location from CP:{location}</h3>
        <h3>EMAILID:Souravrajvi@gmail.com</h3>
    </div>

    }
}
export default UserClass;
```



----
**STATE VARIABLES IN CLASS COMPONENTS!!**

In functional Components We used Hook UseState to Create State Variables!
Now in class Based Components!

**So whenever I say I’m loading a class-based component on our webpage that means I’m creating a new instance of this class!**

->THE BEST PLACE TO CREATE STATE VARIABLES IS INSIDE THE Constructor

->`const [count]=useState(0)`
This is How we did in Functional Components!

-> This Is How we do in Class based Components!
 
```javascript
   class UserClass extends React.Components {
   constructor(props){
        super(props);
        this.state={
            count:0,
        }
    }
    render(){
        const{name,location}=this.props;
        const{count}=this.state;
        return <div className="user-card">
        <h1>Count:{count}</h1>  
        <h2>Name from CP:{name}</h2>
        <h3>Location from CP:{location}</h3>
        <h3>EMAILID:Souravrajvi@gmail.com</h3>
    </div>

    }


```

-> `this.state.count` Dhyan rakha


Now if We want to use Multiple State Variables 
-> In functional components we do this
![Episode 08 - Let's get Classy-20241028204540462.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241028204540462.webp)
-> In class based components we could do this!
![Episode 08 - Let's get Classy-20241028204730297.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241028204730297.webp)


## NOW CAN WE UPDATE THESE STATE VARIABLES 

In class Components I Thought I could do this!
![Episode 08 - Let's get Classy-20241028205722407.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241028205722407.webp)
->BUT THIS WON'T WORK KOI ERROR NAHI AEGA BUT JUST HOGA YE KI Count Ki value nahi badhegi!

-> We Can't Update Our State variables Directly!
-> WE CAN DO THIS
```javascript
<button onClick={()=>{
        this.setState({
            count:this.state.count+1,
        })
        }}>Increase Count</button>
```
-> this.set.State puure component Mein har jagah available Hota hai!
-> this.set.State Mein Ek Object Pass Hota hai!
-> Aur vahi baat yahan bhi lagu hoti hai ki in case Agar State Variable Ki value Change Hoti hai toh fir Component Re render hota hai!


-> We can even Batch Two state variables in the same setState and Then Use it!
-> It is possible and can be done separately too!
-> React won't touch The other State Variables which are not stated in the setState function
-> YAHAN PAR BHI STATE VARIABLE K CHANGE SE RE-RENDER HOTA HAI

---
## **LIFECYCLE OF CLASS BASED COMPONENTS** 

-> **So whenever I say I’m loading a class-based component on our webpage that means I’m creating a new instance of this class!**
->THE FIRST THING WHEN A CLASS IS CALLED THE CONSTRUCTOR IS CALLED!
-> First Constructor then render is called 
-> ![Episode 08 - Let's get Classy-20241029085845984.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029085845984.webp)

![Episode 08 - Let's get Classy-20241029085919299.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029085919299.webp)

-> SO FIRST THE CONSTRUCTOR IS CALLED THEN THE RENDER IS CALLED 
**What if We Class Component K andar Class Component Call horaha hai!**
->  PARENT CHILD RELATIONSHIP HERE!!!

PARENT-> 

![Episode 08 - Let's get Classy-20241029090406766.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029090406766.webp)


CHILD-> 


![Episode 08 - Let's get Classy-20241029090445119.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029090445119.webp)



![Episode 08 - Let's get Classy-20241029090554063.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029090554063.webp)

-> Apart from The constructor and the render method Class based components also have another very important method component did mount!!!!

-> YE LIFE CYCLE METHODS BOLTE HAIN INKO!!!
## **COMPONENT DID MOUNT**

`componentDidMount()` is a lifecycle method in React class components that runs after a component has been rendered to the DOM for the first time. It’s commonly used to perform side effects, such as fetching data, setting up subscriptions, or manually interacting with the DOM.

Here's how `componentDidMount()` works:

1. **Runs Once**: It runs only once in the component’s lifecycle, immediately after the component is mounted.
2. **Ideal for Side Effects**: It’s commonly used for operations that need the component to be present in the DOM, such as fetching data from an API or setting up event listeners.

-> In the initial Render Sabse pehle Constructor is called then render then CDM(component did mount)

-> What if the parent as well as the child Both have CDM IN THEM
ORDER=P C=> P R=> C C => C R => C CDM => P CDM 


->CDM SE useEffect ki Feel nahi aarahi kya?? Mujhe toh aarhai hai!! Which Means We're going to use it make API CALLS!!! Kyonki ekbar component render hogya fir hum Api call laga sakte hain na!
![Episode 08 - Let's get Classy-20241029093032838.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029093032838.webp)


-> WHat if The parent Has Two Child Like This
![Episode 08 - Let's get Classy-20241029093610584.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029093610584.webp)

-> ![Episode 08 - Let's get Classy-20241029093710609.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029093710609.webp)

WHYYY



![1034](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029094046162.webp)

->REACT IS SMART SO WHAT IT WILL DO IT THAT KI REACT WILL BATCH THE RENDER PHASE OF BOTH THE CHILD AND ATFER THAT CDM WILL BE CALLED FOR BOTH
-> This is an optimization done By react!

-> After That The Commit Phase will be batched Together!

![Episode 08 - Let's get Classy-20241029095034300.webp](../../Images/Episode%2008%20-%20Let's%20get%20Classy-20241029095034300.webp)

-> NOW HOW CAN WE MAKE API CALLS IN OUR CLASS BASED COMPONENTS!!!
```javascript
import React from "react";
class UserClass extends React.Component{
    constructor(props){
        super(props);
        this.state={
            userInfo:{
                login:"",
                followers:"",
                bio:"",
                avatar_url:"",
            }
        }
    }
  async componentDidMount(){
    const data =await fetch(" https://api.github.com/users/Souravrajvi0");
    const json=await data.json();
    console.log(json);
    this.setState({
        userInfo:json,
    })
  }
  componentDidUpdate(){
    console.log("Component Did Update");
  }
   componentWillUnmount(){
    console.log("Component Will Unmount");
  }

    render(){
        const{login,followers,bio,avatar_url}=this.state.userInfo;
        return <div className="user-card">
        <img src={avatar_url} alt="user-avatar" />
        <h2>Name:{login}</h2>
        <h3>Followers:{followers}</h3>
        <h3>Bio:{bio}</h3>
    </div>

    }
}
export default UserClass;
```

WHEN STATE CHANGES -> COMPONENET DID UPDATE CHLEGA !!
WHEN COMPONENT IS UNMOUNTED THEN = COMPONENT WILL UNMOUNT CHLEGA!!!