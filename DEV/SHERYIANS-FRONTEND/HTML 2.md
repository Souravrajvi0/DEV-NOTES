---
view-count: 4
---
## FORM TAG

![HTML 2-20241112102930530.webp](../Images/HTML%202-20241112102930530.webp)


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact Form</title>
</head>
<body>
  <h1>Contact Us</h1>
  <form action="submit_form.php" method="POST">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required><br><br>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required><br><br>

    <label for="message">Message:</label><br>
    <textarea id="message" name="message" rows="4" cols="50" required></textarea><br><br>

    <button type="submit">Submit</button>
  </form>
</body>
</html>


### Key Attributes of the `<form>` Tag

1. **`action`**: The URL where the form data will be sent when the form is submitted. This could be a server script or an API endpoint.
    
    - Example: `<form action="/submitForm" method="POST">`
2. **`method`**: Defines how the form data will be sent:
    
    - **`GET`**: Appends data to the URL (e.g., `?name=value&email=value`). It's used for simple, non-sensitive requests like searches. Data can be visible in the browser’s address bar.
    - **`POST`**: Sends data in the request body, which is more secure and suitable for larger or sensitive data (e.g., user credentials).
3. **`target`**: Specifies where to open the result of the form submission.
    
    - **`_blank`**: Opens in a new window or tab.
    - **`_self`** (default): Opens in the same frame as the form.
    - **`_parent`**: Opens in the parent frame.
    - **`_top`**: Opens in the full window.
4. **`enctype`**: Defines how the form data should be encoded when sent to the server (used with the `POST` method). This is especially important when sending files.
    
    - **`application/x-www-form-urlencoded`**: Default encoding for text-based data.
    - **`multipart/form-data`**: Used for file uploads.
    - **`text/plain`**: Sends data as plain text.
5. **`name`**: Provides a name for the form, which is useful for referencing the form in JavaScript.
    
    - Example: `<form name="contactForm">`
6. **`autocomplete`**: Specifies whether the browser should automatically complete the form based on previous entries.
    
    - **`on`**: The browser can autocomplete form fields.
    - **`off`**: Autocomplete is disabled.

### Form Elements Inside `<form>`

Inside the `<form>` tag, various input elements are used to collect data. These include text fields, radio buttons, checkboxes, select boxes, textareas, and buttons.


#### Common Form Elements

**Text Input** (`<input type="text">`): Used for single-line text input.

<input type="text" name="username" placeholder="Enter your username">

**Password Input** (`<input type="password">`): Used for password input fields (the entered text is obscured).

<input type="password" name="password" placeholder="Enter your password">

**Radio Buttons** (`<input type="radio">`): Used when the user needs to select one option from a set of choices.

<input type="radio" name="gender" value="male"> Male
<input type="radio" name="gender" value="female"> Female

**Checkboxes** (`<input type="checkbox">`): Used for multiple selections where the user can check or uncheck options.

<input type="checkbox" name="subscribe" value="yes"> Subscribe to newsletter


**Select Dropdown** (`<select>`): A dropdown menu for choosing an option.

<select name="country">
  <option value="usa">United States</option>
  <option value="canada">Canada</option>
</select>

**Submit Button** (`<button type="submit">`): A button that submits the form data.

<button type="submit">Submit</button>


### Example: Contact Form

<form action="process_form.php" method="POST">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" required><br><br>

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required><br><br>

  <label for="message">Message:</label><br>
  <textarea id="message" name="message" rows="4" cols="50" required></textarea><br>

  <button type="submit">Send Message</button>
</form>


### When is the `<form>` Tag Used?

- **User Authentication**: Forms are used for login and registration forms.
- **Feedback and Contact**: Users can submit queries or feedback.
- **Search**: Forms are used for search boxes.
- **Data Collection**: For surveys, polls, or any kind of data input.
- **File Uploads**: Forms are used to upload files from the user to the server

The **`name`** attribute in HTML is used to identify an element and assign it a unique name within the document. This is crucial for form elements, as it defines the **key** that will be used to associate the input value with the data sent to the server when the form is submitted. It's used by both form processing scripts and in JavaScript to reference form elements

The **`name`** attribute is used to **identify** form elements, and its value helps pair the **name** with the **value** of the form element when the form is submitted. However, just having the same `name` attribute doesn't mean all elements with that name will automatically send their data together. Here's a breakdown of how the `name` attribute works:

### 1. **The `name` Attribute for Form Submission**

- When a form is submitted, **each form element** (like an `<input>`, `<textarea>`, `<select>`, etc.) that has a **`name`** attribute will send its **value** to the server.
- The **name-value pair** that is sent consists of:
    - **Name**: The value of the `name` attribute.
    - **Value**: The current value of the form element.

### 2. **What Happens If Multiple Elements Share the Same `name` Attribute?**

- **Radio Buttons**: If you have multiple radio buttons with the same `name` attribute, only the **selected** radio button's value will be sent when the form is submitted.

<input type="radio" name="gender" value="male"> Male
<input type="radio" name="gender" value="female"> Female

If the user selects "Female," only the `value="female"` will be sent for the name `gender`.

 **Checkboxes**: If you have checkboxes with the same `name` attribute, **all selected** checkboxes will have their values sent, and they will be sent as an **array** of values. The server will receive multiple values under the same name.

<input type="checkbox" name="hobbies" value="reading"> Reading
<input type="checkbox" name="hobbies" value="traveling"> Traveling
<input type="checkbox" name="hobbies" value="sports"> Sports


If the user selects "Reading" and "Sports," the form will send:

- `hobbies=reading&hobbies=sports`


**Multiple Inputs with Same `name`**: If you have multiple form elements (e.g., `<input>`, `<select>`, etc.) with the same `name` attribute but of different types, only the **value of the selected element** (or filled element) will be sent when the form is submitted.

**Example:**
<input type="text" name="username" value="john_doe">
<input type="text" name="username" value="jane_doe">

If the user fills the first input with "john_doe" and leaves the second one empty, only `username=john_doe` will be sent.

### 3. **How Data is Sent to the Server**

When the form is submitted, the data is sent to the server as a series of **name-value pairs**. If multiple form elements share the same `name` attribute (like radio buttons, checkboxes, etc.), the server will receive all values for that name (for checkboxes) or just the selected value (for radio buttons).

For example:
<form action="/submit" method="POST">
  <input type="checkbox" name="hobbies" value="reading"> Reading
  <input type="checkbox" name="hobbies" value="traveling"> Traveling
  <input type="checkbox" name="hobbies" value="sports"> Sports
  <input type="submit" value="Submit">
</form>
If the user selects "Reading" and "Sports," the data sent to the server will look like this:

`hobbies=reading&hobbies=sports`

If the user selects only "Traveling," the data sent will be:

`hobbies=traveling`

![HTML 2-20241112104404372.webp](../Images/HTML%202-20241112104404372.webp)


![HTML 2-20241112104435925.webp](../Images/HTML%202-20241112104435925.webp)

![HTML 2-20241112104453157.webp](../Images/HTML%202-20241112104453157.webp)




## DIV

Jabh Khali Div tag (MTLB NO TAG INSIDE IT) Will have this configurations look at this
![HTML 2-20241112105001714.webp](../Images/HTML%202-20241112105001714.webp)
Width toh hai but height 0 Hai!!!
DIV KI WIDTH FULL WINDOW JITNI HOTI HAI

![HTML 2-20241112105041738.webp](../Images/HTML%202-20241112105041738.webp)
Ye Charo Elements ek hi Div mein hai bhai!


The `<div>` tag in HTML stands for "division" and is one of the most commonly used elements in web development. It is a **block-level container element** that is used to group together other HTML elements and apply styling or JavaScript functionality to them.

### Purpose of `<div>` Tag:

The `<div>` tag is a **structural** element that does not provide any visual content by itself but is useful for **grouping** content, creating layouts, and styling sections of a webpage using CSS. It is often used to define sections or divisions within a page.

### Key Points:

- **Block-level element**: By default, a `<div>` takes up the full width available, and elements inside it will appear on a new line.
- **No visual impact on its own**: It doesn't add any specific style or visual change by itself. However, you can apply CSS to style the content inside a `<div>`.
- **Used for layout and grouping**: It is primarily used to group other HTML elements for styling purposes, to create complex layouts, or to add interactivity using JavaScript.

![HTML 2-20241112105222566.webp](../Images/HTML%202-20241112105222566.webp)


<div>
  <h1>Welcome to My Website</h1>
  <p>This is a section of my website.</p>
  <img src="image.jpg" alt="Sample Image">
</div>


### Attributes:

While the `<div>` tag does not have many attributes, the most common ones are:

1. **`id`**: Used to uniquely identify the `<div>`, useful for CSS styling or JavaScript manipulation.
    - Example: `<div id="header">`
2. **`class`**: Used to assign a class to the `<div>` that can be targeted in CSS or JavaScript. A class can be used by multiple elements.
    - Example: `<div class="container">`
3. **`style`**: Inline CSS for directly applying styles to the `<div>`.
    - Example: `<div style="background-color: yellow;">`
4. **`data-*`**: Custom attributes for storing extra data (useful for JavaScript).
    - Example: `<div data-user-id="123">`



THESE ARE TWO DIV!!
<div class="section">
  <h2>About Us</h2>
  <p>We are a company that...</p>
</div>

<div class="section">
  <h2>Contact</h2>
  <p>Reach us at...</p>
</div>


### Common Use Cases:

1. **Layouts and Structure**:
    
- A `<div>` is commonly used to define sections of a webpage, like the header, footer, sidebar, or main content area.

EXAMPLE: YE EK DIV MEIN HAI SAARE!

   <div id="header">Header Content</div>
<div id="sidebar">Sidebar Content</div>
<div id="main-content">Main Content</div>
<div id="footer">Footer Content</div>


**CSS Styling**: You can style a `<div>` element using CSS to control its size, layout, borders, background color, and more. Example:

<div class="box" style="width: 300px; height: 200px; background-color: blue;">
  This is a styled div.
</div>


**JavaScript Interaction**: You can use the `<div>` element to trigger actions in JavaScript. For example, you can hide or show content, change styles, or manipulate content inside a `<div>`.
<div id="message" style="display: none;">Hello, World!</div>
<button onclick="document.getElementById('message').style.display='block'">Show Message</button>






### Example of Grouping Content:



`<div class="section">   <h2>About Us</h2>   <p>We are a company that...</p> </div>  <div class="section">   <h2>Contact</h2>   <p>Reach us at...</p> </div>`


### Why Use `<div>`?

- **Flexibility**: It’s a general-purpose container that can be used for a variety of tasks like structuring content and applying styles.
- **Layout Control**: Combined with CSS, `<div>` is extremely powerful for designing complex web layouts. You can use them with modern CSS techniques like Flexbox or Grid.
- **JavaScript Targeting**: It can be targeted easily for dynamic content changes with JavaScript.

## ID AND CLASS

The **`id`** and **`class`** attributes in HTML are used to assign identifiers to elements, which allows you to target and manipulate them using CSS or JavaScript. Both attributes help define the identity of an element, but they serve different purposes and have different rules for usage.

### **`id` Attribute**

The **`id`** attribute is used to assign a unique identifier to an element. This identifier must be unique within the page, meaning that no two elements can have the same `id` value. The `id` is often used to reference the element in JavaScript or to apply specific styling with CSS.

#### Key Characteristics:

- **Unique**: Each `id` value must be unique within the document (no two elements can have the same `id`).
- **One-to-One Relationship**: An `id` should reference only **one element** in the document.
- **Used for specific targeting**: Since `id` is unique, it’s ideal for targeting a single element using JavaScript or applying a specific CSS style.
<div id="header">
  <h1>Welcome to My Website</h1>
</div>
In this case, the `id="header"` uniquely identifies the `<div>` element, which you can then reference in CSS or JavaScript.

#### CSS Example (Using `id`):


```css
#header {
  background-color: blue;
  color: white;
}
```


#### JavaScript Example (Using `id`):

`document.getElementById('header').style.backgroundColor = 'green';`


### **`class` Attribute**

The **`class`** attribute is used to assign one or more class names to an element. Unlike `id`, the `class` attribute does not have to be unique, and an element can have multiple classes. The `class` attribute is often used to apply common styling to multiple elements or for targeting multiple elements in JavaScript.

#### Key Characteristics:

- **Reusable**: Multiple elements can share the same `class` name. It is ideal when you want to apply the same style to many elements.
- **One-to-Many Relationship**: A single class can be applied to many elements, and each element can have multiple class names.
- **Used for styling multiple elements**: `class` is great for targeting groups of elements that share similar styling or behavior.
<div class="card">
  <h2>Card Title</h2>
  <p>Some text inside a card.</p>
</div>

<div class="card">
  <h2>Another Card Title</h2>
  <p>Some other text inside a card.</p>
</div>


In this example, both `<div>` elements have the `class="card"`, so they will share the same style or behavior defined by that class.

#### CSS Example (Using `class`):

```css

.card {
  background-color: black;
  padding: 20px;
  margin: 10px;
}
```

USING JAVASCRIPT
```javascript
let cards = document.querySelectorAll('.card');
cards.forEach(function(card) {
  card.style.border = '2px solid black';
});
```




![HTML 2-20241112110030161.webp](../Images/HTML%202-20241112110030161.webp)


### **Multiple Classes in `class` Attribute**

An element can have more than one class, which is especially useful when you want to apply multiple styles or behaviors to the same element.

#### Example:
<div class="card large blue">
  <h2>Card Title</h2>
  <p>Content goes here.</p>
</div>
Here, the `<div>` has three classes: `card`, `large`, and `blue`. You can apply styles for each class separately or combine them.


```css
.card {
  background-color: lightgray;
  padding: 20px;
}

.large {
  font-size: 2em;
}

.blue {
  color: blue;
}
```

### **Best Practices**

- **Use `id` for unique elements**: When you have a specific, unique element that needs individual targeting (like a header, a footer, or a single section), use the `id` attribute.
- **Use `class` for grouping elements**: When you have multiple elements that should share the same style or behavior, use the `class` attribute. This is great for applying common styles to sections, buttons, lists, etc.


## HTML SEMANTICS
![HTML 2-20241112111950854.webp](../Images/HTML%202-20241112111950854.webp)


![HTML 2-20241112112155319.webp](../Images/HTML%202-20241112112155319.webp)

![HTML 2-20241112112224682.webp](../Images/HTML%202-20241112112224682.webp)


**HTML semantics** refers to the practice of using HTML tags that convey meaning about the content inside them. Rather than using generic tags like `<div>` and `<span>` for everything, semantic HTML tags provide more context and describe the purpose of the content they enclose. This makes web pages more accessible, easier to understand, and better structured for both developers and machines (such as search engines and screen readers).

### Why Use Semantic HTML?

- **Improved Accessibility**: Semantic tags make it easier for screen readers to interpret the page structure and convey information to users with disabilities.
- **Better SEO**: Search engines can better understand the structure and content of a webpage, leading to improved rankings.
- **Easier Maintenance**: Semantic tags make the code more readable and maintainable for developers.
- **Consistency**: Using proper tags helps standardize the layout and structure of web pages.


Here’s a breakdown of some of the most commonly used **semantic HTML elements**:

#### 1. **`<header>`**

- Represents the header of a section or the entire page. It typically contains introductory content or navigation links.
    
    **Example:**
    <header>
  <h1>Welcome to My Website</h1>
  <nav>
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#about">About</a></li>
    </ul>
  </nav>
</header>
#### 2. **`<footer>`**

- Represents the footer section of a page or a section. It often contains information such as copyright, contact information, or links to privacy policies.

<footer>
  <p>&copy; 2024 My Website</p>
  <p><a href="#privacy">Privacy Policy</a></p>
</footer>


#### 3.**`<article>`**

- Represents independent, self-contained content that could stand alone, such as blog posts, news articles, or product descriptions.

<article>
  <h2>Breaking News: Web Development Trends</h2>
  <p>Web development is evolving rapidly. Here's what's new in 2024...</p>
</article>


#### 4. **`<section>`**

- Represents a thematic grouping of content, often with a heading. Sections are typically used for grouping related content, such as different sections of an article or a page.
<section>
  <h2>About Us</h2>
  <p>We are a company that values...</p>
</section>
#### 5. **`<nav>`**

- Represents navigation links. This element is used to wrap the links to help both search engines and assistive technologies understand that this content is for navigation.
    
    **Example:**
    
    <nav>
  <ul>
    <li><a href="#home">Home</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>
#### 6. **`<aside>`**

- Represents content that is tangentially related to the content around it. Often used for sidebars, advertisements, or related links.
    
    **Example:**
    <aside>
  <h3>Related Articles</h3>
  <ul>
    <li><a href="#">Learn HTML5</a></li>
    <li><a href="#">Understanding CSS</a></li>
  </ul>
</aside>
#### 7. **`<main>`**

- Represents the dominant content of the `<body>` element, excluding things like navigation, footers, sidebars, etc. It’s meant to contain the primary content of the page.

<main>
  <h1>Main Content</h1>
  <p>This is the primary content of the page.</p>
</main>
### Benefits of Using Semantic HTML

1. **Accessibility**: Semantic tags help screen readers and assistive technologies better understand the structure of the page, providing a more meaningful and navigable experience for users with disabilities.
    
2. **SEO (Search Engine Optimization)**: Search engines use semantic HTML to better understand the content of your page. Proper use of semantic elements helps search engines rank your content more accurately, improving the page's visibility in search results.
    
3. **Code Readability and Maintainability**: Using semantic tags makes the HTML code more readable and meaningful, both for developers and for tools that might analyze the code (such as linters or compilers).
    
4. **Consistency**: Using semantic tags aligns with best practices in web development, leading to cleaner, more consistent, and standards-compliant code.
    
5. **Future-proofing**: As web technologies evolve, semantic HTML helps ensure your content remains structured in a way that’s compatible with new features and frameworks.


### Non-Semantic Tags (For Comparison)

Before semantic HTML, developers used generic containers like `<div>` and `<span>` for almost everything. While these elements are useful in certain situations (for example, for grouping content or applying styles), they don't provide any meaning about the content they contain. Overusing them can lead to code that is difficult to understand, especially for users with accessibility needs or for search engines.

#### Example of non-semantic code:

<div>
  <h1>My Blog</h1>
  <div>Welcome to my blog. Here's an article on web development.</div>
  <div>Contact us</div>
</div>


This code is valid, but using semantic tags (`<header>`, `<article>`, `<footer>`, etc.) would provide more meaning.



![HTML 2-20241112113443896.webp](../Images/HTML%202-20241112113443896.webp)


Applying CSS To these tags!

![HTML 2-20241112113635998.webp](../Images/HTML%202-20241112113635998.webp)


![HTML 2-20241112113653626.webp](../Images/HTML%202-20241112113653626.webp)


AUDIO AND VIDEO TAG

![HTML 2-20241113074919075.webp](../Images/HTML%202-20241113074919075.webp)

This is for!! Adding audio in the file!!

![HTML 2-20241113075017126.webp](../Images/HTML%202-20241113075017126.webp)



TO ADD VIDEO:


```html
   <video src="Limitless.mp4" autoplay muted loop></video>
```

   ![376](../Images/HTML%202-20241113075610438.webp)

