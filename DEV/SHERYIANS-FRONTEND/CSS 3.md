---
view-count: 3
---
## FLEXBOX

Now if we want ki mere elements agal bagal ayein like this

![CSS 3-20241112175137253.webp](../Images/CSS%203-20241112175137253.webp)

Well we can use **inline** or **inline block**



JABH BHI ELEMENTS KO MAIN AGAL BAGAL CHAHTA HUON IN THAT CASE!!! FLEX BOX LAGEGA!!!
JADA CONTROL MILTA HAI YAHAN!!!

![873](../Images/CSS%203-20241112175435101.webp)

So flexbox kinpar lagta hai well jinko agal bagal lana hota hai unpar nahi balki!! PARENT PAR LAGTA HAI!!!
CHILDREN PAR LAGTA HAI!!!

PARENT YAHAN PICHE WALA BOARD HAI!!! ISPAR FLEX-BOX LAGEGA

PHONE'S AND REMOTE NA CHILDREN HAI BHAI!!

JAISE HI HUM KISI KO FLEXBOX BANATE HAIN NA TOH WAHAN PAR 2 AXIS ACTIVATE HOTI HAI!! YAHAN HOGI BLACK BOARD pAR

![546](../Images/CSS%203-20241112175908527.webp)

Elements ki direction bataegi main axis!!! iska by default left to right hota hai!!!
Cross by default top to bottom jata hain!!

MAIN AXIS PAR WORK KRNE K LIYE USE HOTA HAI **justify-content** (default case)
CROSS AXIS PAR WORK KRNE K LIYE USE HOTA HAI **align-items** (default case)




![CSS 3-20241112180339150.webp](../Images/CSS%203-20241112180339150.webp)

 ![381](../Images/CSS%203-20241112180409965.webp)

![216](../Images/CSS%203-20241112180429498.webp)

![CSS 3-20241112180452917.webp](../Images/CSS%203-20241112180452917.webp)

![CSS 3-20241112180503302.webp](../Images/CSS%203-20241112180503302.webp)



NOW WE HAVE TO WORK ON THE MAIN AXIS RIGHT!!

**FOR THAT WE use justify-content**

![427](../Images/CSS%203-20241112180726980.webp)

![CSS 3-20241112180751321.webp](../Images/CSS%203-20241112180751321.webp)

![CSS 3-20241112180806498.webp](../Images/CSS%203-20241112180806498.webp)

now we do align items works on the y axis

![CSS 3-20241112180851222.webp](../Images/CSS%203-20241112180851222.webp)

![CSS 3-20241112180906159.webp](../Images/CSS%203-20241112180906159.webp)


Justify-content: space-between 

![CSS 3-20241112181006997.webp](../Images/CSS%203-20241112181006997.webp)

Justify-content: space-around

![CSS 3-20241112181041135.webp](../Images/CSS%203-20241112181041135.webp)


Justify-content: space-evenly

![CSS 3-20241112181144800.webp](../Images/CSS%203-20241112181144800.webp)


![CSS 3-20241112181221277.webp](../Images/CSS%203-20241112181221277.webp)

![CSS 3-20241112181252322.webp](../Images/CSS%203-20241112181252322.webp)

Justify-content: end

![CSS 3-20241112181358963.webp](../Images/CSS%203-20241112181358963.webp)



## PSEUDIO-ELEMENTS


![CSS 3-20241112181610112.webp](../Images/CSS%203-20241112181610112.webp)

![CSS 3-20241112182648336.webp](../Images/CSS%203-20241112182648336.webp)
![CSS 3-20241112182701899.webp](../Images/CSS%203-20241112182701899.webp)

for every tag this is the case but they are by default inactive!




![CSS 3-20241112182933051.webp](../Images/CSS%203-20241112182933051.webp)



![CSS 3-20241112183000730.webp](../Images/CSS%203-20241112183000730.webp)

![CSS 3-20241112183038670.webp](../Images/CSS%203-20241112183038670.webp)

Button jab tab hum dabak rakhenge!

![CSS 3-20241112183117956.webp](../Images/CSS%203-20241112183117956.webp)

![CSS 3-20241112183152923.webp](../Images/CSS%203-20241112183152923.webp)

![CSS 3-20241112183204260.webp](../Images/CSS%203-20241112183204260.webp)


![CSS 3-20241112183234997.webp](../Images/CSS%203-20241112183234997.webp)

![CSS 3-20241112183534956.webp](../Images/CSS%203-20241112183534956.webp)

![CSS 3-20241112184035400.webp](../Images/CSS%203-20241112184035400.webp)

![CSS 3-20241112184732252.webp](../Images/CSS%203-20241112184732252.webp)

![CSS 3-20241112184748588.webp](../Images/CSS%203-20241112184748588.webp)

![CSS 3-20241112184819278.webp](../Images/CSS%203-20241112184819278.webp)

EK GRID TYPE STRUCTURE BNEGA!!!


GRID  Helps us in making the perfect structure!!!

![CSS 3-20241112185207934.webp](../Images/CSS%203-20241112185207934.webp)

same as 
![CSS 3-20241112185220639.webp](../Images/CSS%203-20241112185220639.webp)


PROBLEMS WITH DISPLAY FLEX!!
KI DISPLAY FLEX EK SINGLE DIMENSIONAL PROPERTY HAI!!

![679](../Images/CSS%203-20241112191708590.webp)

**BUT DISPPLAY GRID IS A 2 DIMENSIONAL PROPERTY!!**

when you change `flex-direction` to `column` in a flex container, the axes do indeed change. By default, a flex container's primary axis (main axis) is horizontal, and the cross axis is vertical. But when you set `flex-direction: column;`, the primary axis switches to vertical, and the cross axis becomes horizontal.

Here’s how it works in detail:

### 1. **Default Horizontal Axis (Row)**

- When you have `flex-direction: row;` (the default setting):
    - The **main axis** is **horizontal** (left to right).
    - The **cross axis** is **vertical** (top to bottom).
- Justify content and align items work on these axes:
    - `justify-content` controls alignment along the **horizontal (main) axis**.
    - `align-items` controls alignment along the **vertical (cross) axis**.

### 2. **Changing to Vertical Axis (Column)**

- When you set `flex-direction: column;`:
    - The **main axis** becomes **vertical** (top to bottom).
    - The **cross axis** becomes **horizontal** (left to right).
- With `flex-direction: column`, the functions of `justify-content` and `align-items` switch axes:
    - `justify-content` now aligns items along the **vertical (main) axis** (top to bottom).
    - `align-items` aligns items along the **horizontal (cross) axis** (left to right)


**DISPLAY GRID HELPS IN BUILDING THE LAYOUTS OF THE WEBSITE!!!**

DISPLAY GRID ELEMENTS KO ROWS AND COLUMNS MEIN DIVIDE KAR DETA HAI!!!
AND YAHAN HUM ROWS AND COLUMNS DONO KO EKBAR MEIN TARGET KAR SKTE HO!!!

![CSS 3-20241112192558231.webp](../Images/CSS%203-20241112192558231.webp)


![476](../Images/CSS%203-20241112192611722.webp)

if you only apply `display: grid` without defining `grid-template-columns` or `grid-template-rows`, the grid container will still become a grid, but no explicit rows or columns are created. Instead, it will act as an **implicit grid**, which means:

1. **Single Column Layout by Default**:
    
    - Without `grid-template-columns`, the grid items will stack in a single column (essentially behaving like a block layout).
    - Each grid item will take up the full width of the container, one below the other.
2. **Implicit Row Creation**:
    
    - As you add grid items, the grid will automatically create new rows to accommodate each item, sizing each row based on the content (effectively `grid-auto-rows: auto` by default).
3. **No Control Over Item Positioning**:
    
    - Since no columns or rows are explicitly defined, you can’t use properties like `grid-column` or `grid-row` to place items across multiple columns or rows. All items will simply fall into this default layout.



`display: grid` property is a powerful layout tool used to create complex, responsive web layouts easily. It works by turning an HTML element into a grid container, where you can define rows, columns, and gaps for positioning items in a structured grid.

### Key Concepts of Grid

1. **Grid Container and Grid Items**:
    
    - When you set `display: grid` on an element, it becomes a _grid container_, and its direct children become _grid items_.
2. **Defining Rows and Columns**:
    
    - You can define the number and size of rows and columns within the grid container using properties like `grid-template-columns` and `grid-template-rows`.
// basically Yahan par hum column and rows define kar skte hain!!!!


```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr; /* Creates 3 equal-width columns */
  grid-template-rows: auto 100px;     /* Creates 2 rows: 1 auto-sized and 1 fixed 100px row */
}


```



```css
.box{
    width: 100%;
    height: 100%;
    background-color: lightblue;
    display: grid;
    gap: 10px;
}
```


![569](../Images/CSS%203-20241112210956466.webp)




![CSS 3-20241112213857636.webp](../Images/CSS%203-20241112213857636.webp)



```css

.box{
    width: 100%;
    height: 100%;
    background-color: lightblue;
    display: grid;
    grid-template-columns: 20% 20% 20% 20% 20% 20%;
    grid-template-rows: 20% 20% 20% 20% 20%;
    gap: 10px;
    
}

#elem1{
    height: 100px;
    width: 100px;
   background-color: pink;
   border: 3px solid black;
}

#elem2{
    height: 100px;
    width: 100px;
    background-color: pink;
    border: 3px solid black;
 }

 #elem3{
    height: 100px;
    width: 100px;
    background-color: pink;
    border: 3px solid black;
 }

```



```css
grid-template-columns: 20% 20% 20% 20% 20% 20%;
    grid-template-rows: 20% 20% 20% 20% 20%;
    gap: 10px;
```

IS SEEE EK GRID TYPE STRUCTURE BUILD UP HUA AND USKE ANDAR BHI HUM ELEMENTS KI PLACING ACHE SE KAR SAKTE HAIN!!

  
```css
   .box{
    width: 100%;
    height: 100%;
    background-color: lightblue;
    display: grid;
    grid-template-columns: 20% 20% 20% 20% 20% 20%;
    grid-template-rows: 20% 20% 20% 20% 20%;
    gap: 10px;
    align-items: center;
    justify-items: center;
}
```


![651](../Images/CSS%203-20241112214510744.webp)



```css
.box{
    width: 100%;
    height: 100%;
    background-color: lightblue;
    display: grid;
    grid-template-columns: 200px 200px;
    grid-template-rows: 200px 200px;
   }

#elem1{
    height: 200px;
    width: 200px;
   background-color: pink;
   border: 3px solid black;
 }
```

![873](../Images/CSS%203-20241112215136647.webp)






```css
.box{
    width: 100%;
    height: 100%;
    background-color: lightblue;
    display: grid;
    grid-template-columns: 200px 200px;
    grid-template-rows: 200px 200px;
    align-content: space-between;
    justify-content: space-between;
    
}
```


![553](../Images/CSS%203-20241112215518325.webp)






![CSS 3-20241112220447175.webp](../Images/CSS%203-20241112220447175.webp)



```css
#nav{
    display: grid;
    background-color: red;
    grid-template-columns: 40% 10% 10% 10% 10% 10% 10%;
    grid-template-rows: 100px;
    align-items: center;
    justify-items: center;
}

#nav h1{
    justify-self: start;
}


```



![CSS 3-20241112220847444.webp](../Images/CSS%203-20241112220847444.webp)

