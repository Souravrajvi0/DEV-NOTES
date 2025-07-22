---
view-count: 3
---
![Untitled 62.png](../../Images/Untitled%2062.png)

HOW TO USE JS IN MY HTML FILE??
![Episode 01 - Inception-20241026090443093.webp](../../Images/Episode%2001%20-%20Inception-20241026090443093.webp)
->BROWSERS DOESN'T UNDERSTAND REACT CODE!!!!!

How to add react in my html file?

**1st WAY TO INCLUDE REACT IN OUR PROJECT IS USING CDN LINKS**

[https://legacy.reactjs.org/docs/cdn-links.html](https://legacy.reactjs.org/docs/cdn-links.html)

``` javascript
<script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
Core react file
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
This is for react file needed for DOM
```

Put em just above the closing body tag!

What is CDN?

### Content Delivery Network (CDN).

A CDN is a network of servers distributed across various locations, each containing copies of data (in this case, JavaScript libraries like React). When you import React via a CDN, you're essentially fetching React from one of these servers.

This is a security measure to prevent certain types of attacks, such as cross-site request forgery (CSRF). By fetching the resource with the `**crossorigin="anonymous"**` attribute, the browser ensures that any sensitive user credentials or cookies are not sent along with the request, which helps protect the user's privacy and security.  
  
**→Jabh hum react ko import karte hain toh humein ek react object bhi milta hai console mein**  

![Untitled 1 52.png](../../Images/Untitled%201%2052.png)

**→ReactDom object bhi milta hai**

![Untitled 2 39.png](../../Images/Untitled%202%2039.png)

![Untitled 3 35.png](../../Images/Untitled%203%2035.png)

React Code inside the HTML file

To write React code inside HTML file we use the script tag!

→This same code can be written inside a JS file and then that JS file can be just injected using a script tag inside The html code

⇒React.createElement(type, [props], [...children])

- `**type**` (string or React component): The type of the element to create. This can be a string representing an HTML tag (e.g., 'div', 'h1', 'p') or a reference to a custom React component.
- `**props**` (object, optional): The properties (or props) to be passed to the element. These are typically attributes like `**className**`, `**id**`, `**style**`, etc.
- `**children**` (React elements, optional): The children of the element. These can be strings, numbers, other React elements created with `**React.createElement()**`, or arrays of React element

⇒**ReactDOM.createRoot()**

`**ReactDOM.createRoot()**` is a method provided by React for creating a root React render tree. It is typically used in React applications that are built using the Concurrent Mode feature, which enables React to perform rendering work in a more incremental and interruptible manner, allowing for smoother user interactions and better responsiveness.  
  
We first create a root React render tree using  
`**ReactDOM.createRoot()**`. This method takes a DOM element as its argument, specifying where the root of the React component tree should be mounted in the HTML document.

→In React, a "root" ReactDOM render tree refers to the entry point of a React application where the entire component tree is mounted onto the DOM. It's essentially the top-level container where React starts rendering and managing the user interface.

When we say `**ReactDOM.createRoot()**` is used to create a new "root" ReactDOM render tree, it means that this method is used to instantiate a new root container where your React application will be mounted.

In more technical terms:

- **Root**: In the context of React, a root is a container element in the HTML DOM where React attaches and renders the component tree. You can think of it as the starting point of your React application.
- **ReactDOM render tree**: This refers to the hierarchical structure of React components that are rendered into the DOM by ReactDOM. It represents the entire component tree rooted at the top-level ReactDOM container

The `**root.render()**` method is used to render a React component or element into the specified root render tree.  
  -> HAR CHIZ KI EK FEEL HOTI HAI! NOW THE THING HERE IS THAT TUJHE REACT KI FEEL SAMAJHNI PADEGI 
  -> THE MOST COSTLY OPERATION IN A WEBPAGE IS DOM MANIPULATION

![Untitled 4 32.png](../../Images/Untitled%204%2032.png)

→`**heading**` is a JavaScript object that represents a React element. This object will be used by React to create and update the corresponding DOM element when rendering

→And render method jo hai na vo ye object lega and it will make that this react element/Js object will get mounted on the DOM
![Episode 01 - Inception-20241026095224453.webp](../../Images/Episode%2001%20-%20Inception-20241026095224453.webp)

HOW TO GET 
  
  
  

![Untitled 5 27.png](../../Images/Untitled%205%2027.png)

-Now If we have a Nested structure in HTML how to create it using React?

![Untitled 6 25.png](../../Images/Untitled%206%2025.png)

→Nested HTML structure inside the react now when we pass the children we create a new react element.

→Since Children text bhi ho skta hai,Toh h1 k andar koi attribute toh nahi hai but children text hai

![Untitled 7 21.png](../../Images/Untitled%207%2021.png)

⇒So when we want to have siblings? what can we do?

**Passing multiple children in the form of an array**

![Untitled 8 18.png](../../Images/Untitled%208%2018.png)

**Array of children**

![Untitled 9 13.png](../../Images/Untitled%209%2013.png)

Warning

![Untitled 10 12.png](../../Images/Untitled%2010%2012.png)

This will throw an error // ki react is not defined

![Untitled 11 10.png](../../Images/Untitled%2011%2010.png)

Correct Order

So when we already have a h1 in div root tag like this

![Untitled 12 8.png](../../Images/Untitled%2012%208.png)

And then we render root,So in this case This will be replaced in Will the react element

⇒Whatever code we have in this Div with root id will be replaced(everything)

![Untitled 13 4.png](../../Images/Untitled%2013%204.png)

→The upper h1 and the below one won’t be affected by this
SO THIS MEANS KI REACT CAN ONLY BE APPLIED TO A SMALL PART OF OUR PAGE ALSO!

Yes, when importing React from a CDN (Content Delivery Network), there are typically both development and production versions available. These versions serve different purposes:

1. **Development Version**: This version includes extra debugging information, warnings, and error messages aimed at helping developers identify issues during development. It's larger in file size because of these additional features. The development version is usually used during the development phase of a project to aid in debugging and testing.
    
    Example:
    
    ```HTML
    htmlCopy code
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    
    ```
    
2. **Production Version**: This version is optimized for performance and is stripped of any debugging information or development-specific features. It's smaller in file size compared to the development version, making it more suitable for production environments where file size and performance are critical.
    
    Example:
    
    ```HTML
    htmlCopy code
    <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
    
    ```
    

When deploying a React application to production, it's recommended to use the production version of React to minimize file size and improve performance. However, during development, it's common to use the development version for its helpful debugging features.