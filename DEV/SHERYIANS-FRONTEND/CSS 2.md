---
view-count: 5
---
## DISPLAY PROPERTY!!!


The `display` property in CSS is one of the most fundamental properties for controlling the layout and behavior of elements on a webpage. It determines how an element is displayed in relation to its surrounding content and other elements.

Here’s an overview of the different values the `display` property can take, and how each one affects the layout.

### 1. **`display: block;`**

- **Definition**: The element will be displayed as a **block-level element**.
- **Behavior**: Block elements take up the entire width available (by default) and start on a new line, pushing subsequent elements below them.
- **Examples**: `<div>`, `<p>`, `<h1>`, `<section>`, `<header>`, etc.

WE CAN CHANGE THE WIDTH,HEIGHT OF BLOCK ELEMENTS!!
```css
div {
    display: block;
}
```

- **Effect**: The element will behave like a block, taking full width and stacking vertically.


SO KOI ELEMENT AGAR BLOCK HOTA HAI TOH WO ALLOW NAHI KARTA KI KOI ELEMENT USKE BAGAL MEIN AEE!!!

TOH CHAHE  SPACE HO!!! TOBHI BLOCK ELEMENT NICHE HI AEGA !!!!

BLOCK ELEMENT KEHTA HAI PURI SPACE MERI HAI!! MERE SPACE MEIN SIRF MEIN AUNGA!!!

![CSS 2-20241112153403522.webp](../Images/CSS%202-20241112153403522.webp)




### 2. **`display: inline;`**

- **Definition**: The element will be displayed as an **inline element**.
- **Behavior**: Inline elements do not start on a new line. They only take up as much width as necessary for their content and do not affect the layout of other elements.
- **Examples**: `<span>`, `<a>`, `<strong>`, `<em>`, etc.
- **Usage**:


```css
span {
    display: inline;
}
```
**Effect**: The element will stay in line with the text or other inline elements, without breaking the flow.


INLINE ELEMENT KEHTA HAI KI BACHI HUI SPACE MEIN AGAR KOI AUR AA SKTA HAI TOH AAJAO!!

![CSS 2-20241112153515738.webp](../Images/CSS%202-20241112153515738.webp)

But wo dono hi inline elements hone chahiye!!

In case ek inline hua and ek block toh sath mein nahi aenge!

Even in the case agar dono inline hain but problem ye hai ki space available nahi first wale k bad jada toh fir 2nd inline sath mein nahi aega!!!


inline element don't let you play/change the width of the element!



### 3.**`display: inline-block;`**

- **Definition**: The element behaves like an inline element, but it can also have set width and height values like a block element.
- **Behavior**: The element remains inline with other elements, but unlike `inline`, it allows setting dimensions (like width, height), padding, and margins.
- **Examples**: This is often used for elements like buttons, images, or navigation items.

```css
button {
    display: inline-block;
    width: 100px;
    height: 50px;
}
```
- **Effect**: The element stays in the flow of inline elements but allows for block-like styling.

INLINE Elements doesn't allow you to increase height and width!!
AND IF WE STILL WANT TO INCREASE WIDTH/HEIGHT THEN WE NEED INLINE BLOCK ELEMENTS!!

SO IN INLINE BLOCK ELEMENTS WE CAN INCREASE THE WIDTH/HEIGHT AND ALSO WE CAN USE THE INLINE PROPERTY IN THE SAME LINE!!! THEY CAN COME TOGETHER!!!


![CSS 2-20241112154421993.webp](../Images/CSS%202-20241112154421993.webp)







![CSS 2-20241112154302922.webp](../Images/CSS%202-20241112154302922.webp)




## POSITION

The `position` property in CSS is used to control the positioning of elements within a webpage. It determines how an element is placed relative to its parent or other elements. The `position` property works in conjunction with other properties such as `top`, `right`, `bottom`, and `left`, which specify the exact positioning of the element once its `position` is defined.

There are **5 main values** for the `position` property:

ABSOLUTE KI BAT KARTE HAIN PEHLE!!!


### Position:absolute

So when we make an element absolute wo apne ek dusre plain mein upar aa jata hai! toh jahan se upar aya vahaan toh space khali hui na!!!! toh piche wala element aage badh jaega and hum upar se hi dekhte hain!
NORMAL FLOW SE UPAR UTH JATA HAI ELEMENT

![546](../Images/CSS%202-20241112170415188.webp)



![565](../Images/CSS%202-20241112170530558.webp)

HUM WEBISTE KO HAMESHA TOP SE DEKHTE HAIN YE BAT DHYAN RAKHNA BHAI!!!

SO YAHaAN JO OBJECT 3 wo chup gaya na dekh!!! KYONKI JAISE HI ELEMNT 2 WO UPAR UTHA ELMENT 3 AGE AGYA USKI JAGAH 
Jabh bhi hum kisi element ko absolute bnate hai na toh wo upar uth jata hai! And hum kahan se dekhte hain upar seee!!



![625](../Images/CSS%202-20241112170747307.webp)

Aur ye jo element hai jo utha apne plan mein kahin bhi ja skta hai!!!!, so isko apne plan mein move karke jiss elemnet k upar laenge wo element wo hide kar dega!!!

Aese toh agar sabko absolute bana diyo toh sab upar aagaye then fir upar ko aega???

![728](../Images/CSS%202-20241112171005870.webp)

Sab element apne plan mein toh aenge but absolute karne k bad plain mein k level different honge ,sabse last wale ka plain sabse upar hoga!!

1st level 1 par uthega
2nd level 2 par uthega
3rd level 3 par uthega

by defualt saare level 0 par hote hain!!!




![CSS 2-20241112171311017.webp](../Images/CSS%202-20241112171311017.webp)

![CSS 2-20241112171410944.webp](../Images/CSS%202-20241112171410944.webp)


![CSS 2-20241112171429911.webp](../Images/CSS%202-20241112171429911.webp)



now if we do this

![CSS 2-20241112171503302.webp](../Images/CSS%202-20241112171503302.webp)
GREEN KO UPAR WALE PLAIN MEIN UTHAYA NA!!!

![CSS 2-20241112171519753.webp](../Images/CSS%202-20241112171519753.webp)



![CSS 2-20241112171612598.webp](../Images/CSS%202-20241112171612598.webp)

![556](../Images/CSS%202-20241112171624762.webp)

We can even move this green car anywhere in it's plain!



![CSS 2-20241112171708641.webp](../Images/CSS%202-20241112171708641.webp)

![CSS 2-20241112171727722.webp](../Images/CSS%202-20241112171727722.webp)
since last wali ka level 3 tha toh wo upar  aagayi!!





### position:relative 

![606](../Images/CSS%202-20241112171901030.webp)

Yahan Ye apne plain mein move nahi kar skta hai!
Now if we make the cube absolute!!

![606](../Images/CSS%202-20241112171941259.webp)

Ab ye apne plain mein move kar sakta hai!!!!!

![629](../Images/CSS%202-20241112172104111.webp)


Now agar main drawer ko relative bana duon and cube toh absolute hai hi hai!

Toh now cube apne plain mein bhi drawer k surface area ki shadow k bahar nahi jaega!!!


![589](../Images/CSS%202-20241112172356118.webp)

![CSS 2-20241112172410044.webp](../Images/CSS%202-20241112172410044.webp)

left se 40% le ra ha  box k andar agar relative nahi krte toh wo 40% screen k respect mein leta!!!







### postion:fixed 

![CSS 2-20241112172619585.webp](../Images/CSS%202-20241112172619585.webp)
Now even if we scroll the bar the down the element will stay at it's position only!

![CSS 2-20241112172705358.webp](../Images/CSS%202-20241112172705358.webp)




## BACKGROUND




```css
#box{
    width: 300px;
    height: 300px;
    background: url(https://media.gettyimages.com/id/544181648/photo/1912-oil-opaque-color-on-wood-32-4-x-40-2-cm-located-in-the-leopold-museum-vienna-austria.jpg? 
         s=612x612&w=0&k=20&c=iAApVSVENnMGOZvqeVLa0qIpCaBCphiLDkwK_R3kIhI=);
     
}
```

![288](../Images/CSS%202-20241112173232711.webp)

Not showing the complete image 

SO WHAT WE CAN DO IS!!!

  `background-size: cover;`  cover / contain

![166](../Images/CSS%202-20241112173408605.webp)
cover kya karta hai ki pure div/container mein cover karo image ko!!!
 contain kya karega ki image mein div mein laega aese->
 ![204](../Images/CSS%202-20241112173947242.webp)

for no repeat `background-repeat:no-repeat`

Jitni show ho skti hai utni dikhegi mtlb humne image ko chota karke uss container mein daalkar show karne ki koshish ki hai yahan!!!
     `background-position: center;` top/center/bottom kuch bhi de skte hain depending upon the need!
AB AUR BETTER DIKHEGI!!!
![217](../Images/CSS%202-20241112173553091.webp)

BETTER COMBO IN THE END :
![CSS 2-20241112174102450.webp](../Images/CSS%202-20241112174102450.webp)


We can also use background to set color!

![CSS 2-20241112174201355.webp](../Images/CSS%202-20241112174201355.webp)

By default top to bottom hota hai but maine yahan specify kar diya from right to left!!

![CSS 2-20241112174347342.webp](../Images/CSS%202-20241112174347342.webp)


ye bhi likh skate hain

![CSS 2-20241112174417541.webp](../Images/CSS%202-20241112174417541.webp)

and ye bhi kar skate hain

![CSS 2-20241112174436705.webp](../Images/CSS%202-20241112174436705.webp)

![CSS 2-20241112174452509.webp](../Images/CSS%202-20241112174452509.webp)
