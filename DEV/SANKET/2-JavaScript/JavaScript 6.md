---
view-count: 2
---
Functions are first-class citizens in JS, as we can call a function inside a function and Return a function from a function.

![Untitled 77.png](../../Images/Untitled%2077.png)

→My mental model till now When The function is executed it gets removed from the stack

→

![Untitled 1 67.png](../../Images/Untitled%201%2067.png)

→

![Untitled 2 52.png](../../Images/Untitled%202%2052.png)

![Untitled 3 49.png](../../Images/Untitled%203%2049.png)

![Untitled 4 46.png](../../Images/Untitled%204%2046.png)

![Untitled 5 41.png](../../Images/Untitled%205%2041.png)

![Untitled 6 39.png](../../Images/Untitled%206%2039.png)

→So the mental model we get from the other languages is that once function is over it gets removed from the STACK

→

![Untitled 7 34.png](../../Images/Untitled%207%2034.png)

→So this closure property Which is attached to the function remember all those variables That are getting accessed inside your function whose scope might be in your function might be outside your function. It remembers the memory location of all those variables.

→ So the inner function will remember these variables which are getting accessed in the inner function while whose scope might be inside your inner function or outside your inner function

→So The inner storage will remember these variables and make them a persistent storage

→So we’re remembering the original I variable

→USE CASE OF CLOSURES→ SET TIMEOUT IS THE BIGGEST EXAMPLE OF THAT

![Untitled 8 31.png](../../Images/Untitled%208%2031.png)

→ Even here When DO() is called, There’s a set time out function that gets in the Runtime Then end is printed// Since we can say DO() is executed it will removed from the stack and the funtion exec will be executed after 2 seconds then how come it will have the access to the task variable/??Through Closures lol

→Closures are powerful because they allow functions to retain access to variables from their containing (enclosing) scope even after the parent function has finished executing. This makes them useful for maintaining state in functional programming and for creating private variables in JavaScript.

![Untitled 9 26.png](../../Images/Untitled%209%2026.png)

Imperative languages mein batana padta hai ki Kya kaise karna hai Ex→ C++,JAVA

Declarative languages mein sirf Batana hai kya krna hai steps nahi btane.Ex→ SQl

Example of imperative→

  

![Untitled 10 25.png](../../Images/Untitled%2010%2025.png)

_**ITERATORS**_

→It’s a style of programming

→ Humein batana nahi padta hai kis data kaise leke ana basss lekar aajao directly

→

![Untitled 11 23.png](../../Images/Untitled%2011%2023.png)

![Untitled 12 21.png](../../Images/Untitled%2012%2021.png)

→Inbuilt iterators Syntax is given by this

  

**_GENERATORS_**

![Untitled 13 15.png](../../Images/Untitled%2013%2015.png)

![Untitled 14 13.png](../../Images/Untitled%2014%2013.png)

![Untitled 15 12.png](../../Images/Untitled%2015%2012.png)

![Untitled 16 11.png](../../Images/Untitled%2016%2011.png)

→Iter is a whole object all together

→Now this iter will act like an iterator

→

![Untitled 17 11.png](../../Images/Untitled%2017%2011.png)

→jaise Hi generator funtion k execution mein yield aega uska execution stop ho jyaega and whattever value we’re yielding it returns that value as the return value of the iterator

![Untitled 18 11.png](../../Images/Untitled%2018%2011.png)

→ not a single line of code is executed of the Generator function

→So everytime we call next it starts just after the next yield and continues execution until it encounter another yield

![Untitled 19 11.png](../../Images/Untitled%2019%2011.png)

→Return keyword k bad no yield will matter

→

  

# _**ASYNC AWAIT**_

  

  

![Untitled 20 11.png](../../Images/Untitled%2020%2011.png)

![Untitled 21 11.png](../../Images/Untitled%2021%2011.png)

→jaise hi usee yield mila control vahin se exectuion khatam hogya since we know toh even in an expression flow totega and agli bar hum jabh likenege iter.next() then in that case agar koi value pass nahi ki hai iter.next(x) k andar toh yield ki jagah undefined jayega otherwise jo value pass ki hai iter.next(6) jaise 6 yahan toh wo chli jayegi

→