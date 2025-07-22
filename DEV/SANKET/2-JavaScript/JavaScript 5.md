---
view-count: 2
---
**Promises**

![Untitled 75.png](../../Images/Untitled%2075.png)

![Untitled 1 65.png](../../Images/Untitled%201%2065.png)

![Untitled 2 50.png](../../Images/Untitled%202%2050.png)

→This x can be used later on with some other functionality while it can’t be done the same with the Callbacks!

![Untitled 3 47.png](../../Images/Untitled%203%2047.png)

→ Promise objects are native to JS,even iske bare Mein bat bhi hui hai ecma script k Andar

![Untitled 4 44.png](../../Images/Untitled%204%2044.png)

![Untitled 5 39.png](../../Images/Untitled%205%2039.png)

→Creation of Promise object is synchronous in nature .When We create a Promise its creation is synchronous in nature and if in the callback We have a synchronous piece of code then it'll execute as a synchronous piece of code only

→State k alawa value property bhi hoti hai promise ki depending upon the situation The value property will be changed

![Untitled 6 37.png](../../Images/Untitled%206%2037.png)

![Untitled 7 32.png](../../Images/Untitled%207%2032.png)

→So Whatever argument we pass into the resolve(x) Will be assigned to the value property of the promise object

→Same for the reject Function as well

![Untitled 8 29.png](../../Images/Untitled%208%2029.png)

→Here we waited for some time before printing x-> because jo wo for loop hai na wo blocking piece of code hai

![Untitled 9 24.png](../../Images/Untitled%209%2024.png)

→But yahan par set time out ek asyn piece of code hai isliye promise immediately return hogya and print bhi hogya and uski jo state hai vo bhi pending aa rahi hai as we can see but y place holder ka use kar sakte hain kaise bhi karke  
JS created our object at that time only and now our code can move forward  

→

![Untitled 10 23.png](../../Images/Untitled%2010%2023.png)

→Doesn't matter how many values we pass here only the first value will take the promise value // doesn't value if we pass multiple values we can passs array to do that if you want to

→SO NOW YOU KNOW RIGHT WHAT IT MEANS BY PROMISE IS RETURNED IMMEDIATELY IF THE EXCETUOR FUNCTION CODE IS NON BLOCKING(asyn)

→agar immediately mil gya toh state of promise pending rahegi  
JS MEIN syn code blocking hota hai  

![Untitled 11 21.png](../../Images/Untitled%2011%2021.png)

![Untitled 12 19.png](../../Images/Untitled%2012%2019.png)

→The state of of the promise will be pending always unless we don't call the reject and resolve functions these can be named a or b farak nahi padta

![Untitled 13 13.png](../../Images/Untitled%2013%2013.png)

![Untitled 14 11.png](../../Images/Untitled%2014%2011.png)

→Now bat ye hai ki reject and resolve agar uske bad hi maine kuch code likha hai toh in that case wo bhhi exeecute hoga bass hota ye hai ki when resolve ya reject aya toh vo activate hua and state of the promise and the value wil be changed that's it not like return lol jo code k flow ko hi rokh deta hai

→

![Untitled 15 10.png](../../Images/Untitled%2015%2010.png)

![Untitled 16 9.png](../../Images/Untitled%2016%209.png)

→Agar ek bas resolve hogya then vapis se karenge toh promise ki state and value par koi farak nahi padega  
It can be updated just once  

→WHEN USING NEW AND PROMISE CONSTRUCTOR, the constructor expects a callback funnction whose defaut arguement are reslove and reject(ye dono function go as argemnets)  
And inside this executor we can write asyn or syn code doesn't matter  

![Untitled 17 9.png](../../Images/Untitled%2017%209.png)

![Untitled 18 9.png](../../Images/Untitled%2018%209.png)

The executor is called synchronisly jaise hi new promise constructor call hua jo ye executor callback funtion hai ye call hoga usii time and execute hoga synchronusly and ismein agar blokcing peiece of code hua(native js code which take time) toh promise tab tak return nahi hoga jabtak wo code nahi hota and agar kuch asyn code hai ismein toh vo runtime ki responsibilty hai vo aese hi return hojaega.

![Untitled 19 9.png](../../Images/Untitled%2019%209.png)

    **CONSUMING A PROMISE**

![Untitled 20 9.png](../../Images/Untitled%2020%209.png)

![Untitled 21 9.png](../../Images/Untitled%2021%209.png)

![Untitled 22 9.png](../../Images/Untitled%2022%209.png)

![Untitled 23 8.png](../../Images/Untitled%2023%208.png)

Depending upon the environment setimeout returns different values in browser it might return a number while in node it might return an object so when we do x%2 we arwe doin that on an objec

![Untitled 24 8.png](../../Images/Untitled%2024%208.png)

Yahan humne timeout jo return kar rahai hai uska wait nahi kiya ,kyonki x k andar timerid hai and uske hisab se promise resolve ya reject ho jaega  
ismein ye hua ki promise fulfilled with the execution of execute function and fulfilled the promise  

![Untitled 25 8.png](../../Images/Untitled%2025%208.png)

→ .then karke hum bas inn functions ko register karte hain into their respctive array , Inka execution nahi hota yahan  
Vo toh jabh promise ki state change hogi tabhhi jitne bhi handlers hai depending upon wether the promise it rejected or fulfilled us array k sare handlers execute ho jayenge  

→Mtlb if the state changes of the promise then depending upon the state change jo handlers hai na vo micro queue mein add ho jaeyege. But execute tabhi honge jabh Event handler dekhega ki areee ab call stack mein kuch nahi hai and main piece of code bhi khatam ho chuka hai.

→ agar event queue mein kuch hai in that case kya hoga ki micro task wale functions ko priority di jayengi

→.then se HUM WE ARE ONLY REGISTRING THE FUNCTIONS IN THE ARRAY OF THE PROMISE OBJECT THEY ARE NOT GETTING EXECUTED AT THAT TIME

→Aur registration k bad bhi code likha hai toh vo execute hota rahega  
Multiple .then likh kar hum multiple handlers add kar sakte hain promise object k andar jo array hota hai usmein  

![Untitled 26 6.png](../../Images/Untitled%2026%206.png)

![Untitled 27 6.png](../../Images/Untitled%2027%206.png)

![Untitled 28 6.png](../../Images/Untitled%2028%206.png)

So jitne bhi callback the hmare pass in the rejectecion or fulfilmment callback array in the promise vo sab jayenge  microtask queue after the promise state is resolved or rejected.

And depeding upon the global code and call stack if there is none left event handler will give prority to the microtask queue functions and fir wo execute honge and then finally jo callback queue k funtions hain vo execute honge

mIcrotask queue k andar jitne bhi handlers hai vo sab bhi gloabal piece of code khatam hone k bad execute honge

Eventloop end mein lega callback queue se funtions ko execute krne k liye

jabh promise fulfil/reject hoga tabhi wo array k funtions microtask queue mein aenge

  

![Untitled 29 6.png](../../Images/Untitled%2029%206.png)

![Untitled 30 6.png](../../Images/Untitled%2030%206.png)

→Agar ek hi handler ho then k andar then it means ki usko lenge resolving handler ki trah  
promise fulffil hot hai and tabbh uske array wale functio jate hai miscro task qeueu k andar  

→Agar call stack khali and global code khali then we go for for the funtions in the micro queue

![Untitled 31 6.png](../../Images/Untitled%2031%206.png)

![Untitled 32 6.png](../../Images/Untitled%2032%206.png)

Gives you an already resolved promise !

same as→

![Untitled 33 6.png](../../Images/Untitled%2033%206.png)

---

  

![Untitled 34 6.png](../../Images/Untitled%2034%206.png)

![Untitled 35 6.png](../../Images/Untitled%2035%206.png)

→Saves you from Inversion of control since even if someone tried to resolve the promise twice it won't change anything and if someone doesn't resolve your promise then the state will tell you that

→To register a handler we use .then function which in turn also returns a promise

→.then takes two argument which is fulfilment handler and rejectiion handler(if ek hi function pass kiya hai toh wo fulfillment handler hota hai)

→

![Untitled 36 6.png](../../Images/Untitled%2036%206.png)

→We can use this new promise to make a chain of .then

![Untitled 37 4.png](../../Images/Untitled%2037%204.png)

![Untitled 38 4.png](../../Images/Untitled%2038%204.png)

→And agar value define nahi ki return k sath toh in that case undefined rahegi value resolved returnable promise ki.

  

![Untitled 39 4.png](../../Images/Untitled%2039%204.png)

![Untitled 40 2.png](../../Images/Untitled%2040%202.png)

→Resolve ya reject mujhe Hamesha promise constructor mein milenenge and to resolve promise using a constructore it is necessary to use resolve keyword but .then se chain kiye gaye promises ko hum resolve return karke ya direct promise return karke bhi kar sakte hain

  

  

NOW IMPLEMENTATION EXAMPLE