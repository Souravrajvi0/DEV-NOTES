---
view-count: 4
---
**CSS (Cascading Style Sheets)** is a stylesheet language used to control the presentation of HTML content on web pages. CSS allows developers to apply styles like colors, fonts, layouts, spacing, and much more to HTML elements, enabling the separation of content (HTML) from design (CSS). This makes websites more flexible, consistent, and easier to manage.

### Why CSS is Used:

- **Visual Styling**: CSS adds visual styles to HTML elements, such as colors, fonts, and layouts, to make websites look polished and professional.
- **Consistent Design**: CSS lets you create a consistent look and feel across all pages by centralizing styles in one place.
- **Responsive Design**: CSS helps build responsive layouts that adjust to different screen sizes and devices, creating a better user experience.
- **Maintainability**: With CSS, styling rules are separate from HTML, making it easier to maintain and update.

### How CSS is Applied

CSS can be added to HTML in three primary ways:

1. **Inline CSS**: Directly in the HTML element's `style` attribute.
2. **Internal CSS**: Inside the `<style>` tag within the HTML `<head>`.
3. **External CSS**: Using an external `.css` file linked to the HTML file.


#### 1. Inline CSS

Inline CSS applies styles directly to individual HTML elements. This is not recommended for large projects since it makes maintenance more difficult.

**Example:**
<p style="color: blue; font-size: 20px;">This is styled text.</p>

#### 2. Internal CSS

Internal CSS is defined within a `<style>` tag in the `<head>` section of the HTML document. It applies styles to the whole page but only for that page.

**Example:**


```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      color: blue;
      font-size: 20px;
    }
  </style>
</head>
<body>
  <p>This is styled text.</p>
</body>
</html>

```

#### 3. External CSS

External CSS is stored in a separate `.css` file and linked to HTML files. This is the best practice for larger websites because it enables you to style multiple pages with a single stylesheet.

LINKING IS DONE JUST BELOW THE TITLE TAG!!!
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>HELLO</h1>
</body>
</html>

```


### Basic CSS Syntax

CSS is made up of **selectors** and **declarations**.

- **Selector**: Specifies which HTML element(s) the styles should apply to.
- **Declaration**: Contains a **property** (the feature to style, like `color`) and a **value** (the style to apply, like `blue`).

```css

selector {
  property: value;
}
```


**Example:**


```css
p {
  color: red;
  font-size: 18px;
}
```


### CSS Selectors

CSS selectors specify which HTML elements to style. Here are some common selectors:

- **Type Selector**: Selects all elements of a type (e.g., `p`, `h1`, `div`).

```css
h1 {
  color: green;
}

```

- **Class Selector**: Targets elements with a specific class (prefixed with `.`).


```css
.highlight {
  color: orange;
}

```

- **ID Selector**: Targets an element with a specific id (prefixed with `#`).

```css
#main-title {
  font-size: 24px;
}

```

- **Attribute Selector**: Targets elements with a specific attribute.


```css
input[type="text"] {
  border: 1px solid #000;
}

```



### CSS Properties

CSS has hundreds of properties. Here are some commonly used ones:

### `width` Property

- **Purpose**: Defines the width of an element.
- **Values**:
    - **`auto`**: Default value. The browser calculates the width.
    - **`<length>`**: Specifies width in units (e.g., `px`, `em`, `rem`, `cm`).
    - **`%`**: Specifies width as a percentage of its containing element.
    - **`min-content`**: Sets the width to the smallest possible size without overflowing.
    - **`max-content`**: Sets the width to the largest possible size without wrapping.
    - **`fit-content`**: Fits the width of the content, but respects container constraints.

### `height` Property

- **Purpose**: Defines the height of an element.
- **Values**:
    - **`auto`**: Default value. Height is based on the content inside the element.
    - **`<length>`**: Sets a specific height (e.g., `px`, `em`, `vh`).
    - **`%`**: Sets height as a percentage of the container's height.
    - **`min-content`**: Sets the height to the smallest size that still contains the content.
    - **`max-content`**: Sets the height to the largest size based on the content.
    - **`fit-content`**: Similar to `width: fit-content`, adjusts based on constraints.

### Additional Properties

1. **`min-width` and `min-height`**: Set minimum size limits for an element.
2. **`max-width` and `max-height`**: Set maximum size limits for an element


```css
/* Set a div to 50% width of its container and 300px height */
div {
    width: 50%;
    height: 300px;
}

/* Constrain width and height with min and max */
.container {
    width: 80%;
    min-width: 200px;
    max-width: 600px;
    height: auto;
    min-height: 100px;
}
```
The `min-width`, `max-width`, `min-height`, and `max-height` properties set **boundaries** for the element they're applied to, effectively constraining its size:

- **`min-width: 200px`**: Ensures the element’s width is at least 200px, even if the content or container tries to shrink it further.
- **`max-width: 600px`**: Limits the element’s width to a maximum of 600px, preventing it from expanding beyond this point.
- **`min-height: 100px`**: Ensures the element’s height is at least 100px, stopping it from shrinking below this size.

These boundaries work together to keep the element's dimensions within a flexible but defined range, adapting to screen size and content while respecting the limits set by these properties.



**Color and Text Styling**:

- `color`: Text color.
- `font-size`: Size of the font.
- `font-family`: Font type (e.g., Arial, sans-serif).
-  `text-align`: Text alignment (left, right, center).


```css
p {
  color: blue;
  font-size: 18px;
  font-family: Arial, sans-serif;
  text-align: center;
}
```

**Background**:

- `background-color`: Background color.
- `background-image`: Background image.
- `background-repeat`: Controls whether a background image repeats.


```css
body {
  background-color: lightgrey;
  background-image: url('image.jpg');
  background-repeat: no-repeat;
}



```



Question: Ek Box kaise bnta hai????
DIV KA WIDTH TOH HOTA HAI BUT KOI HEIGHT NAHI HOTA!!! IN CASE WHEN WE DON'T ADD ANYTHING IN THE DIV THEN IT WILL TAKE THE FULL PAGE WIDTH AND 0 HEIGHT . If we even add 1px height!! TUJHE SMAJH AA JAEGA!!! WIDTH FULL LI HAI

TOH EVEN IN CASE WE ADD SOME TEXT TO THIS DIV WE INCREASE THE HEIGHT OF THE DIV!!!!

- **Block-Level Element**: A `<div>` is a block-level element by default. Block-level elements naturally take up the full available width of their container (in this case, the entire screen or the parent element's width) unless you specify a different width.
    
- **Height Determination**: The height of a `<div>` (or any block element) is determined by its content if no specific height is set. So, it will only be as tall as needed to accommodate the text or other content inside it.



```css
#box{
    background-color: aqua;
    height: 100px;
    border: 1px solid black;
    position: absolute;
}



```


When you add `position: absolute` to the `<div>`, it changes how the browser calculates its width. Here’s why:

1. **Default Width of Absolute Positioning**: When an element is positioned absolutely, it no longer behaves like a standard block element within the flow of the document. Instead, it’s removed from the normal document flow, meaning it only takes up as much width as needed for its content by default (similar to how inline or inline-block elements behave).
2. **Full-Width Behavior**: By default, block-level elements take up the full width of their container when they are in the regular document flow. However, with `position: absolute`, the element is only as wide as its content unless you specify a width.
## UNITS

In CSS, there are several units for defining distances such as font sizes, margins, paddings, and dimensions (widths and heights). They fall into two main categories: **absolute** and **relative** units.

### Absolute Units

Absolute units are fixed and do not change based on other elements or the viewport.

1. **`px` (pixels)**:
    
    - One pixel on the screen.
    - Commonly used as a default unit for dimensions (e.g., `width`, `height`).
    - Provides consistent sizing but lacks flexibility for responsiveness.
2. **`cm` (centimeters)**, **`mm` (millimeters)**, **`in` (inches)**:
    
    - Units based on physical measurements.
    - Rarely used in web design since screens can vary greatly, and actual measurement may depend on the device’s DPI (dots per inch).
3. **`pt` (points)** and **`pc` (picas)**:
    
    - Used primarily in print media.
    - **`pt`**: 1 point = 1/72 of an inch.
    - **`pc`**: 1 pica = 12 points.
    - Rarely used for screens, but sometimes useful for print layouts.

 - Now using px is a bad practice since it's absolute size is fixed  so even if we change the size of the window it'll still take X amount of pixels defined in the first place now this will create a Scroll bar!
 ![455](../Images/CSS%201-20241112131528536.webp)

![463](../Images/CSS%201-20241112131547601.webp)

We can see the size of the box is absolute and it's not changing on both the cases!!!

And if we do something like width:800px now the content will get hidden and we'll have to see it using Scroll bar!!!
**SO USE px unit LESS!!!!**
PIP AND DIP BHI MATTER KRTA HAI YHAN SCREEN KA!!!Since 500 px is constant but the size is going to differ for different screens with different  per unit surface area pixels!!
### Relative Units

Relative units adapt to other factors, making them more flexible and often more suitable for responsive designs.

1. **`%` (percentage)**:
    
    - Relative to the size of the parent element.
    - Useful for responsive layouts (e.g., making elements take a percentage of their container’s width).
    - SCREEN KA SIZE CHANGE HOGA YAHAN BHI CHANGE HONGE!!!
![617](../Images/CSS%201-20241112132149707.webp)

![605](../Images/CSS%201-20241112132126942.webp)

In a scenario where there’s only a `<div>` inside the `<body>`, and you set the `<div>`'s width to `50%`, the `50%` width will be **relative to the `<body>` element**. By default, the `<body>` element's width will match the width of the viewport (the entire visible area of the browser).


```css
width:50%;
height:50%;
```

2. **`em` (relative to the parent font size)**:
    
    - `1em` equals the font size of the element’s nearest parent.
    - For example, if the parent has `font-size: 20px`, then `1em` within that context is equal to `20px`.
    - Used for text sizes, paddings, and margins relative to text size.
![CSS 1-20241112133424736.webp](../Images/CSS%201-20241112133424736.webp)

BUT YAHAN PAR BHI VALUES PIXEL KI TRAH FIX RAHEGI!!!


3. **`rem` (relative to the root font size)**:
    
    - `1rem` is relative to the `font-size` set on the `<html>` (root) element.
    - Great for avoiding compounding size effects with nested elements.
    - If `<html>` is `16px`, then `1rem` is `16px` throughout the document, regardless of the nesting level.

4. **`vw` (viewport width)** and **`vh` (viewport height)**:
    
    - `1vw` is 1% of the viewport’s width.
    - `1vh` is 1% of the viewport’s height.
    - Useful for creating fully **responsive layouts** that adjust based on screen size.
    - Example: `width: 50vw;` makes an element 50% of the viewport’s width.

     % hamesha Parent se value leta hai!! But vw and vh hamesha screen se value lete hain
![CSS 1-20241112133119203.webp](../Images/CSS%201-20241112133119203.webp)

THIS WILL COVER THE WHOLE SCREEN!!!!

5. **`vmin` and `vmax`**:
    
    - `vmin`: 1% of the viewport’s **smaller** dimension (width or height).
    - `vmax`: 1% of the viewport’s **larger** dimension.
    - Ensures elements maintain consistent scaling, regardless of orientation (landscape or portrait).
6. **`ch` (relative to the width of the "0" character)**:
    
    - `1ch` is approximately the width of the character “0” in the element’s font.
    - Useful for sizing elements that need to align to character widths, like inputs.
7. **`ex` (relative to the height of the lowercase “x” character)**:
    
    - `1ex` is the height of the lowercase “x” in the font used.
    - Primarily used for accessibility or typography-based design adjustments.


max-width:x ek tarike ki boundary hai mtlb usee kam hui toh width value y hi rahegi but if y>x in that case width:x hojaegi!

Same for min-width



## font-family

![CSS 1-20241112134233337.webp](../Images/CSS%201-20241112134233337.webp)

Even In google fonts: filter values are!!!
 ![CSS 1-20241112134326743.webp](../Images/CSS%201-20241112134326743.webp)



### 1. **`font-family`**

- Defines the typeface for an element.
- You can list multiple fonts as fallbacks in case a font is unavailable.
- Syntax:
  `font-family: "Arial", "Helvetica", sans-serif;`

### 2. **`font-size`**

- Sets the size of the font.
- Accepts various units: `px`, `em`, `rem`, `%`, etc.
- Example:
  `font-size: 16px;`
  `font-size: 1.5em;`
  TO KEEP THE WEBSITE RESPONSIVE BETTER KEEP IT IN VW
  `font-size:2vw`

### 3. **`font-weight`**

- Adjusts the thickness or boldness of the font.
- Common values:
    - **`normal`** (default weight)
    - **`bold`** (bold text)
    - Numeric values: 100, 200, …, 900 (usually `400` is normal, `700` is bold).

### 4. **`font-style`**

- Sets the style of the font.
- Options include:
    - **`normal`**: Regular, upright text.
    - **`italic`**: Italicized text.
    - **`oblique`**: Similar to italic but slightly different, often slanted text.

### 5. **`text-transform`**

- Alters the case of text.
- Common values:
    - **`uppercase`**: Transforms text to all uppercase letters.
    - **`lowercase`**: Transforms text to all lowercase letters.
    - **`capitalize`**: Capitalizes the first letter of each word.

### 6. **`text-decoration`**

- Adds decoration to text, such as underline, overline, or strikethrough.
- Common values:
    - **`none`**: No decoration.
    - **`underline`**: Underlines the text.
    - **`line-through`**: Adds a strikethrough.
    - **`overline`**: Adds a line above the text.


### 7. **`line-height`**

- Sets the space above and below inline elements, controlling vertical spacing within lines.
- Accepts unitless values (e.g., `1.5`) or unit values (e.g., `20px`).
- BASICALLY SPACE BETWEEN THE TWO LINES , 1 ya 1 se choti value par overlap karega!!


### 8. **`text-align`**

- Sets the horizontal alignment of text.
- Common values:
    - **`left`**, **`right`**, **`center`**, **`justify`**
- Default value toh left hi hoti hai!!
- Justify kahin space nahi chorega dono side!



## PADDING & MARGIN



### PADDING
CONSIDER ONE PARENT AND  A CHILD INSIDE IT!!

Black Wala Part Parent hai and phone child hai!!! Now the thing here is ki child ekdam left upper corner mein chippak k aega!!!!


![600](../Images/CSS%201-20241112140633965.webp)


Now if we want ye child thoda andar aajaye toh kaise karnege???
Well Uske liye HUM **PADDING DENGE PARENT KO NAKI CHILD KO**
PARENT KO BOLA PADDING 20px 

![598](../Images/CSS%201-20241112140937738.webp)
Now ab ek imaginary border ban jaega 20px ka charo taraf!!!

So Agar children/kisi element ko andar karna ho toh uske parent ko padding denge hum toh usse kya hoga ki ek imaginary boundary/gap/border aa jaega of the value all the sides 


![CSS 1-20241112143209341.webp](../Images/CSS%201-20241112143209341.webp)


```html

  <div id="parent">
        <h1> PARENT UP</h1>

        <div id="child">
           INSIDE CHILD

        </div>

        <h1>PARENT DOWN</h1>
    </div>
```




```css
#parent{
    background-color: orange;
    margin: 50px;
    padding: 20px;
    width: 400px;
    height: 300px;
}
```
**Parent Element (`#parent`):**

- The parent element has a width of 400px and a height of 300px.
- The padding of 20px is applied to the parent element.
- This means the content (the two `<h1>` elements and the `<div id="child">`) will be positioned 20px away from the edges of the parent.
- The overall size of the parent element, including the padding, is 440px wide (400px + 2 * 20px) and 340px tall (300px + 2 * 20px)

You're absolutely right. The reason why the right and bottom padding of the parent element only increase its overall size, without directly impacting the child element's positioning or visibility, is because the default alignment for HTML elements is to the top and left.

![CSS 1-20241112143734701.webp](../Images/CSS%201-20241112143734701.webp)
Here we can see padding is applied on three sides !!!



NOW HOW ARE VALUES APPLIED AND WRITTEN

### MARGIN

MARGIN HUM 2 ELEMENTS K BICKH MEIN HUM APPLY KARTE HAIN!!!

![CSS 1-20241112144028232.webp](../Images/CSS%201-20241112144028232.webp)

Jaise yahan hum inke bich mein margin apply kar sakte hain!!!

- KISI ELEMENT K ANDAR SPACE DENA HO TOH USEE PADDING KEHTE HAIN
- YAHAN DEKH ANDAR SPACE KIYA HAI!
![467](../Images/CSS%201-20241112144141921.webp)

![CSS 1-20241112144248108.webp](../Images/CSS%201-20241112144248108.webp)

Now element k bahar space dena ho toh use hum kehte hain margin!!!
YAHAN FIRST PAR HUMNE MARGIN BOTTOM LAGAYA HAI!!! YA NICHE WALE KO BOL DO MARGIN TOP!!


```css
property: value1 value2 value3 value4;
```


- `property` can be either `margin` or `padding`.
- `value1`, `value2`, `value3`, and `value4` represent the values for the top, right, bottom, and left sides, respectively.

The number of values provided in the shorthand determines how the values are applied:

1. **One value**:
    
    - If only one value is provided, it is applied to all four sides (top, right, bottom, left).
2. **Two values**:
    
    - If two values are provided, the first value is applied to the top and bottom, and the second value is applied to the right and left.
3. **Three values**:
    
    - If three values are provided, the first value is applied to the top, the second value is applied to the right and left, and the third value is applied to the bottom.
4. **Four values**:
    
    - If four values are provided, they are applied to the top, right, bottom, and left sides, respectively, in that order.(CLOCKWISE)


## BORDER

The `border` property in CSS is used to set the style, width, and color of an element's border. It's a shorthand property that allows you to set all the border-related properties in a single declaration


```css
border: [border-width] [border-style] [border-color];
```

1. **Border Width**:
    
    - Specifies the width of the border.
    - Can be a length value (e.g., `1px`, `2em`, `0.5rem`) or one of the keyword values: `thin`, `medium`, or `thick`.
2. **Border Style**:
    
    - Specifies the style of the border.
    - Possible values include: `none`, `hidden`, `dotted`, `dashed`, `solid`, `double`, `groove`, `ridge`, `inset`, and `outset`.
3. **Border Color**:
    
    - Specifies the color of the border.
    - Can be a color value (e.g., `#000000`, `rgb(0,0,0)`, `blue`, `transparent`).



```css

/* Single value */
border: 2px;
/* Specifies a 2-pixel wide solid black border */

/* Two values */
border: solid red;
/* Specifies a solid red border with the default width (medium) */

/* Three values */
border: 3px dotted #00ff00;
/* Specifies a 3-pixel wide dotted green border */

```


You can also set the border properties individually using the following properties:

- `border-width`: Sets the width of the border.
- `border-style`: Sets the style of the border.
- `border-color`: Sets the color of the border.

Additionally, you can set the border properties for each side of the element using the following properties:

- `border-top`, `border-right`, `border-bottom`, `border-left`
- `border-top-width`, `border-right-width`, `border-bottom-width`, `border-left-width`
- `border-top-style`, `border-right-style`, `border-bottom-style`, `border-left-style`
- `border-top-color`, `border-right-color`, `border-bottom-color`, `border-left-color`

The `border` property is a versatile way to add borders to elements in CSS, and it's commonly used to enhance the visual appearance and layout of web page

- When you add a border to the parent element, the border is added to the outside of the element's content box.
- This means the overall size of the parent element increases by the width of the border on all four sides.
- The child element is still positioned within the parent element's boundaries, but now those boundaries include the added border width



#### BORDER RADIUS COMES INTO PLAY AFTER APPLYING BORDER 
the `border-radius` property in CSS is used to add rounded corners to an element. It's a very useful property for creating visually appealing and modern-looking user interfaces.

The CSS `border-radius` property is used to create rounded corners for elements. It defines the radius of the element's corners, allowing you to go from slightly rounded to fully circular corners.

![CSS 1-20241112150226369.webp](../Images/CSS%201-20241112150226369.webp)

![CSS 1-20241112150322361.webp](../Images/CSS%201-20241112150322361.webp)


![CSS 1-20241112150500187.webp](../Images/CSS%201-20241112150500187.webp)


![CSS 1-20241112150437408.webp](../Images/CSS%201-20241112150437408.webp)



![CSS 1-20241112150557433.webp](../Images/CSS%201-20241112150557433.webp)
![CSS 1-20241112150544442.webp](../Images/CSS%201-20241112150544442.webp)




![CSS 1-20241112150631356.webp](../Images/CSS%201-20241112150631356.webp)

![CSS 1-20241112150618036.webp](../Images/CSS%201-20241112150618036.webp)


Assuming I'm giving border-radius in pixels it will get in circle shape as we keep on increasing the border radius after a while when the circle has been reached then it won't increase!! And stay the circle even if we keep on increasing the border radius!!!

We can get the shape of the capsule if the half the width in pixels  is equal to the border radius!!!



