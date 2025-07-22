---
view-count: 3
---
The most Important Dependency is Bundler. Ex-Vite, parcel
![Untitled 63.png](../../Images/Untitled%2063.png)
→So we’re using -D flag to show that we’re installing it as Dev dependency!
- **Dev Dependency**: These packages are only necessary for development and are not required in the production environment. Examples include tools like `nodemon`, `parcel`, and testing libraries, which help during development but don’t need to be present in the final, deployed application.
    
- **Regular Dependency**: These packages are necessary for your application to run in production. Examples might include frameworks (e.g., Express for Node.js) or libraries essential for the app's core functionality. Like React, React-Dom
# BUNDLER
A bundler like Parcel is a tool used in web development to bundle multiple files (such as JavaScript, CSS, images, etc.) into a single file or a few files for easier deployment and faster loading times. It’s ideal for frontend development workflows where you want a seamless development experience without manually refreshing the browser after each change.
### What Does a Bundler Do?

1. **Combines Files**:
    
    - A bundler takes multiple source files and combines them into a smaller number of output files (often just one) to reduce the number of requests a browser needs to make to load a web page.
2. **Transpilation**:
    
    - Bundlers can also transpile modern JavaScript (ES6+) and other languages (like TypeScript) into a version compatible with older browsers. For example, Parcel uses Babel for transpiling JavaScript.
3. **Minification**:
    
    - Bundlers can minify your code by removing whitespace, comments, and shortening variable names, reducing the file size and improving load times.
4. **Asset Management**:
    
    - Bundlers can manage various asset types like images, fonts, and stylesheets, optimizing them and ensuring they are included in the final bundle.
5. **Hot Module Replacement (HMR)**:
    
    - During development, bundlers like Parcel support hot module replacement, which allows changes to be reflected in the browser without a full page reload.
6. **Dependency Resolution**:
    
    - Bundlers automatically resolve module dependencies, meaning if one file imports another, the bundler figures out the correct order and includes everything needed in the output bundle.


### Why Use a Bundler?

1. **Performance**:
    
    - Fewer files mean faster load times since the browser can make fewer requests. Bundling helps optimize the performance of web applications.
2. **Simplifies Development**:
    
    - Developers can write modular code using ES6 modules or CommonJS, making it easier to manage dependencies without worrying about how they will be bundled for production.
3. **Cross-Browser Compatibility**:
    
    - By transpiling code, a bundler ensures that the application runs smoothly across different browsers and environments.
4. **Organized Codebase**:
    
    - Bundlers encourage a modular approach to development, allowing developers to break their code into reusable components.
5. **Automation**:
    
    - Many bundlers provide automation features, such as running tasks like minification, linting, or testing as part of the build process.


->If i don’t put anything then It always keep the exact version written by me! in the package.json file!
->**package-lock.json**:
- **Generated Automatically**: It's generated automatically by npm whenever you run `**npm install**` or `**npm update**`.
- **Machine Generated**: Unlike `**package.json**`, you generally don't manually edit `**package-lock.json**`. It's meant to be machine-generated and managed by npm

->Transitive dependencies are dependencies that your project relies on indirectly through its direct dependencies. In other words, if your project depends on Package A, and Package A itself depends on Package B, then Package B is a transitive dependency of your project.

Here's an example to illustrate this concept:

Let's say your project (`**Project X**`) depends on two packages: `**Package A**` and `**Package C**`.

- `**Package A**` is a direct dependency of `**Project X**`.
- `**Package A**`, in turn, depends on `**Package B**`.


->**Am I supposed to put this package.json and package-lock.json on git?**
ABSOLUTELY YES

->Even if we delete this node_modules we can still get them back because their meta data is stored in the Package.json and [package-lock.json](http://package-lock.json.So) So we just need to npm install again. And we’ll get all the node modules.

->**Whatever you can regenerate Don’t put it on git**

![Untitled 4 33.png](../../Images/Untitled%204%2033.png)

**->To ignite our app→ yahan par we use the starting file of our project and since my starting file for the project is index.html**

`**npx parcel index.html**` is used to bundle and serve a web application using Parcel, a web application bundler. Let's break down what each part of the command does:

- `**npx**`: This is a package runner tool that comes with npm 5.2.0 and higher. It allows you to run commands from npm packages without installing them globally. If you have Parcel installed locally in your project, you can use `**npx**` to run it without having to install it globally.
- `**parcel**`: This is the command to run the Parcel bundler. When you run `**parcel**`, it bundles your project's assets (such as JavaScript, CSS, images, etc.) for deployment. Parcel automatically detects the entry file of your project and creates a dependency graph to bundle all necessary files.
- `**index.html**`: This is the entry point of your web application. Parcel uses this file as the starting point to build your project. It will analyze `**index.html**` and its dependencies (like JavaScript or CSS files referenced within it) and bundle them accordingly.

![Untitled 5 28.png](../../Images/Untitled%205%2028.png)

![Untitled 6 26.png](../../Images/Untitled%206%2026.png)

Parcel created a server for us

---

1. **npm**:
    - npm is primarily used for managing Node.js packages and dependencies.
    - It is used to install, uninstall, update, and manage packages for your Node.js projects.
    - npm commands include `**npm install**`, `**npm uninstall**`, `**npm update**`, `**npm init**`, etc.
    - npm installs packages locally within your project's `**node_modules**` directory by default.
2. **npx**:
    
    - npx is a tool that comes with npm 5.2.0 and higher (bundled with npm) and is used to execute Node.js packages.
    - It allows you to run binaries of packages without having to install them globally or locally.
    - npx executes commands from Node.js packages as if they were installed globally, but without the need to actually install them
    
    ---
    
    Se we injected react in out Html file using the CDN links Which is not the preferable way!! Since we don’t have to make network calls again and again since when the version changes or the url changes do we need to make change those CDN links again
    
    →Another way to do it is to use NPM
    
    ![Untitled 7 22.png](../../Images/Untitled%207%2022.png)
    
    →We’re installing it as a normal dependency not a dev
    
    ![Untitled 8 19.png](../../Images/Untitled%208%2019.png)
    
    i=install
    
    ---
    
    Since we installed react in the node modules but how do we use it? in our code?
    
    ![Untitled 9 14.png](../../Images/Untitled%209%2014.png)
    
    in our JS file and run it??
    
    ![Untitled 10 13.png](../../Images/Untitled%2010%2013.png)
    
    Since in the HTML code we did this
    
    ![Untitled 11 11.png](../../Images/Untitled%2011%2011.png)
    
    So browser will treat this as a Normal JS code file which it is not
    
    ![Untitled 12 9.png](../../Images/Untitled%2012%209.png)
    
    How to fix this?
    
    ![Untitled 13 5.png](../../Images/Untitled%2013%205.png)
    
    Now this will be considered as a module not a script.
    
    ---
    
    ![Untitled 14 3.png](../../Images/Untitled%2014%203.png)
    
    →HMR karta hai parcel meaning if there is any change in the source code automatically hi Parel browser page refresh kar dega
    
    →kaise kart hai parcel ye sab?
    
    ![Untitled 15 2.png](../../Images/Untitled%2015%202.png)
    
    ![Untitled 16 2.png](../../Images/Untitled%2016%202.png)
    
    ![Untitled 17 2.png](../../Images/Untitled%2017%202.png)
    
    ![Untitled 18 2.png](../../Images/Untitled%2018%202.png)
    
    ![Untitled 19 2.png](../../Images/Untitled%2019%202.png)
    
    ![Untitled 20 2.png](../../Images/Untitled%2020%202.png)
    
    How is parcel so fast? Because it has parcel cache with it!
    
    ---
    
    Inside the Package.json file we have,Meaning the entry point is app.js
    
    ![Untitled 21 2.png](../../Images/Untitled%2021%202.png)
    
    Ye jabh maine build add kiya toh error aega!
    
      
    
      
    
    ![Untitled 22 2.png](../../Images/Untitled%2022%202.png)
    
    and when writing code for production with parcel we
    
    So here we’re specifying index.html as the starting point which will create an error so in this case we need to remove main:app.js
    
    ---
    
    ![Untitled 23 2.png](../../Images/Untitled%2023%202.png)
    
    We don’t have to put dist and parcel cache on github or git
    
      
    
    ---
    
    The `**browserslist**` field is not placed in the `**dependencies**` section of the `**package.json**` file because it's not a dependency of your project in the same sense as libraries or tools you use directly in your code. Instead, it's a configuration setting used by build tools like Babel, Autoprefixer, and PostCSS to determine which browser versions to target when compiling and optimizing your code.
    
    ![Untitled 24 2.png](../../Images/Untitled%2024%202.png)
    
      
    
    ![Untitled 25 2.png](../../Images/Untitled%2025%202.png)
    
    When you use Parcel as a bundler for your web application, the `**dist**` folder (short for "distribution") is where Parcel puts the bundled and optimized version of your application for deployment. Let's break down what happens with the `**dist**` folder when using Parcel:
    
    1. **Bundling**: Parcel analyzes your project's dependencies, including JavaScript, CSS, HTML, and other assets, and creates a dependency graph. It then bundles these assets together into a format optimized for web deployment.
    2. **Optimization**: Parcel performs optimizations on your code to improve performance and reduce file sizes. This can include minification (removing unnecessary characters and spaces), tree shaking (removing unused code), and code splitting (splitting code into smaller files for efficient loading).
    3. **Output to Dist**: Once the bundling and optimization processes are complete, Parcel outputs the bundled files to the `**dist**` folder by default. Inside the `**dist**` folder, you'll find the optimized versions of your HTML, CSS, JavaScript, and any other assets that your application depends on.
    4. **Self-Contained**: The contents of the `**dist**` folder are typically self-contained and ready for deployment to a web server or hosting platform. You can simply upload the contents of the `**dist**` folder to your web server, and your web application should be ready to go.
    5. **Automatic Updates**: Whenever you make changes to your source code and run Parcel again, it will regenerate the `**dist**` folder with the updated bundled and optimized files. This means you don't need to manage the contents of the `**dist**` folder manually—Parcel takes care of it for you.
    
    In summary, the `**dist**` folder serves as the output directory for Parcel, containing the bundled and optimized version of your web application that is ready for deployment to a web server or hosting platform.
    
    Yes, there can be a difference in the contents of the `**dist**` folder depending on whether you use `**npx parcel index.html**` or `**npx parcel build index.html**`. Let's explore each scenario:
    
    1. `**npx parcel index.html**`:
        - When you run `**npx parcel index.html**`, Parcel starts a development server and serves your application from memory without writing the bundled files to disk.
        - This mode is typically used during development because it allows for fast iteration. Parcel watches your files for changes and automatically rebuilds and updates your application in memory as you make changes.
        - Since the files are served from memory, the `**dist**` folder might not be created at all, or it might contain temporary files used by Parcel during development. These files are not optimized for production and may include additional development-related features like source maps.
    2. `**npx parcel build index.html**`:
        - When you run `**npx parcel build index.html**`, Parcel builds your application for production and outputs the bundled and optimized files to the `**dist**` folder.
        - This mode is used when you're ready to deploy your application to a production environment. Parcel performs various optimizations, such as minification, tree shaking, and code splitting, to produce optimized and efficient production-ready code.
        - The `**dist**` folder created in this mode contains the finalized and optimized version of your application, ready to be deployed to a web server or hosting platform. It typically includes minified and concatenated JavaScript and CSS files, along with any other assets needed for your application to run.
    
    In summary, when using `**npx parcel index.html**`, the `**dist**` folder may not be created, or it may contain temporary development-related files. On the other hand, when using `**npx parcel build index.html**`, the `**dist**` folder will contain the optimized and production-ready version of your application.
    
      
    
    important links-
    
    [https://en.parceljs.org/](https://en.parceljs.org/)
    
    [https://browserslist.dev/?q=bGFzdCAxNSBjaHJvbWUgdmVyc2lvbnMg](https://browserslist.dev/?q=bGFzdCAxNSBjaHJvbWUgdmVyc2lvbnMg)

- **Nodemon**: Primarily for Node.js backend development, it watches for file changes in your server code and restarts the server automatically. This is particularly useful when building backend applications, as you don’t need to manually restart the server after each update.
    
- **Parcel**: Mostly for frontend development, Parcel is a bundler that watches for changes in your frontend files (HTML, CSS, JS, etc.) and automatically reloads the page. It’s ideal for frontend development workflows where you want a seamless development experience without manually refreshing the browser after each change.