# How to start PORT on an env variable

### Install dotenv package

Install the `**dotenv**` package using npm. This package allows you to load environment variables from a file.

```Bash
npm install dotenv
```

  

### **Create a** `**.env**` **File:**

Create a file named `**.env**` in the root of your project. This file will contain your environment variables. Add a variable for the port, for example:

```Bash
PORT=3000
```

### **Load Environment Variables in Your Express App:**

In your main Express application file (e.g., `**app.js**` or `**index.js**`), load the environment variables using `**dotenv**`. Add the following lines at the top of your file:

```JavaScript
require('dotenv').config();
```

### **Use the PORT Environment Variable:**

```JavaScript
const express = require('express');
const app = express();
const port = process.env.PORT || 3000;

// Rest of your Express app code...

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

### **Run Your Express App:**

```Bash
node app.js
```