---
view-count: 2
---
Higher Order Functions→

![Untitled 73.png](../../Images/Untitled%2073.png)

![Untitled 1 63.png](../../Images/Untitled%201%2063.png)

![Untitled 2 48.png](../../Images/Untitled%202%2048.png)

→The function which we’re passing in the higher order function is called Callback function. like→ exec()

→higher order functions consume functions

  

![Untitled 3 45.png](../../Images/Untitled%203%2045.png)

Ye settimeout ko call lagaya aur humne pass kiya function exec ko now jahan settimeout ki defition likhi hui hai wo apne app dekhega ki kaise call karna 4 seconds and uske bad vo execute hojayega

  

Disadvantages of callbacks

![Untitled 4 42.png](../../Images/Untitled%204%2042.png)

![Untitled 5 37.png](../../Images/Untitled%205%2037.png)

→Readability problem hoti hai callback hell se but agar 2-3 hee callbacks nested hain toh in that case callback hell itna panga nahi karega

![Untitled 6 35.png](../../Images/Untitled%206%2035.png)

Now When we pass the callback inside doTask we don’t know in the defintion of dotask vo callback ko kiss tarike se implement karega,kya krega mere passed funtion k sath mein.

![Untitled 7 30.png](../../Images/Untitled%207%2030.png)

![Untitled 8 27.png](../../Images/Untitled%208%2027.png)

![Untitled 9 22.png](../../Images/Untitled%209%2022.png)

But there is a mechanism by which JS is able to handle Asynchronous piece of code as well

![Untitled 10 21.png](../../Images/Untitled%2010%2021.png)

→is jagah JS ne wait kiya tha depending upon how much time the loop takes to get comepleted

![Untitled 11 19.png](../../Images/Untitled%2011%2019.png)

→But yahan kya hoga ki hi and by pehle print ho jayega and 5 sec bad time done print hoga
→In order to run a valid piece of javascript code then there are a lot of functionalities and libraries are required,all of these of functionalities are given to JS by the run time
→JS+Runtime(node,Browser)→ MAKES IT SO GOOD
→Even though the browser is a runtime for JS,Browser provides a lot of features that are not native to javascript.
→Using JS code we can modify the html but these functions are not native to JS.
→JS is synchronouss in nature for the piece of code that is native to JS. Uske alawa Js synchronus nahi hai
→Settimeout nahi hai ecma script mein
![Untitled 12 17.png](../../Images/Untitled%2012%2017.png)

![Untitled 13 11.png](../../Images/Untitled%2013%2011.png)

→Any runtime feature of JS will not block the execution of the code,since the latency is like 0 and Jaise hi runtime ko btaya ki bhai ye code mila hai mujhe yahan control vapis aajata hai next line of code par. aaage ko code execute hojaata hai

→ callback ko event queue mein bhejte hai jabh timer done sa hojata hai

→ But event loop check karta rehta hai ki kya koi main piece of code bacha hai ya nahi ya kuch call stack mein toh nahi hai. agar Dono mein kuch nahi hai toh in that case event queue wale funtions call stack mein aate hain and unke sath ye hota hai ki jiska timer pehle khatam hua tha wo pehle aajayega queue mein.

→

```JavaScript
console.log("hello");
for (let i = 0; i < 100000000; i++) {
    }
```

The `**console.log("hello")**` statement will indeed execute before the `**for**` loop because JavaScript is single-threaded and synchronous by default. That means statements are executed in the order they appear in the code, unless there's an asynchronous operation involved.

So, `**console.log("hello")**` gets executed first because it's encountered first in the code, and then the `**for**` loop follows.

1. **Single-threaded**: In JavaScript, there's only one execution thread. This means that JavaScript code is executed line by line, one after the other, in a single sequence. Unlike some other programming languages, JavaScript doesn't have multiple threads of execution running simultaneously.
2. **Synchronous**: Synchronous means that code is executed one line at a time, in order. Each line of code waits for the previous one to finish executing before it starts. So, if there's a function call or operation, the next line won't execute until that operation completes.

Yes, `**console.log()**` is synchronous in nature. When you call `**console.log()**` in your JavaScript code, it executes immediately and logs the provided message to the console synchronously. This means that the message is printed to the console at the point in the code where the `**console.log()**` function is called.  
Yes,  
`**setTimeout**` is asynchronous in nature. When you call `**setTimeout**`, it schedules a task to be executed asynchronously after a specified delay. This means that the callback function provided to `**setTimeout**` will not execute immediately, but instead, it will be queued to run after the specified delay, allowing the rest of the code to continue executing without waiting for the timeout to complete.  
→In JavaScript, console.log() is a run time feature which is synchronus in nature so some runtime features can be synchronous or asynchronous  

Here's a more comprehensive list:

**Synchronous:**

1. Variable assignment
2. Arithmetic operations
3. Conditional statements (if, else if, else)
4. Loops (for, while, do-while)
5. Function calls
6. DOM manipulation
7. Reading from synchronous APIs (e.g., FileReaderSync)

**Asynchronous:**

1. setTimeout
2. setInterval
3. AJAX requests (e.g., XMLHttpRequest, fetch API)
4. Promises
5. Event listeners (e.g., onClick, addEventListener)
6. Reading from asynchronous APIs (e.g., FileReader)
7. Web Workers
8. IndexedDB
9. Writing to files (e.g., using FileWriter)
10. setTimeout and setInterval callbacks
11. Geolocation API
12. WebSockets
13. Asynchronous iteration (e.g., for-await-of loop with async generators)
14. Callback functions in asynchronous APIs

In JavaScript, synchronous code blocks the execution thread until it completes. This means that while the synchronous code is running, nothing else can happen in the program. If you have a long-running synchronous operation, it can make your entire application unresponsive.

On the other hand, asynchronous code allows other operations to run while waiting for a particular task to complete. Asynchronous operations are non-blocking, meaning they don't halt the execution of the program. Instead, they execute in the background, and when they're finished, they trigger a callback or a promise resolution.

This non-blocking behavior is especially useful for tasks like fetching data from a server, reading from a file, or waiting for user input. Instead of freezing the entire application while waiting for these tasks to complete, asynchronous code allows the application to remain responsive and continue executing other tasks concurrently.

By leveraging asynchronous programming techniques, JavaScript can efficiently handle I/O-bound operations without sacrificing responsiveness or performance.

![Untitled 14 9.png](../../Images/Untitled%2014%209.png)

→Any asynchronous piece of code can’t hamper my synchronous piece of code

→ But we can’t be sure that console.log is synchronous all the time So in that case we ought to be a little hesitant

→SET INTERVAL

→What does set interval does is that it executes the callback again and again at the duration specified in the set interval function

→And in different environments it gives different output though the working can be same but the output of the function can be different like in browser it gives a numerical id while in Node js it returns an object,

→We can use clear intreval to stop the setinterval function

---

- Google Chrome: Uses V8 JavaScript engine.
- Mozilla Firefox: Uses SpiderMonkey JavaScript engine.
- Apple Safari: Uses JavaScriptCore (Nitro) engine.
- Microsoft Edge: Initially Chakra, now V8 (Chromium-based).
- Opera: Uses V8 (Chromium-based).
- Brave: Also uses V8 (Chromium-based).

Like node js the browser uses these runtime environments to run java script code on it,So every browser had mostly different run times so we can’t expect them to have the same feature all the time.

---

![Untitled 15 8.png](../../Images/Untitled%2015%208.png)