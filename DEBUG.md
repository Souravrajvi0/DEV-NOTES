```javascript
# 🧠 Node.js Debugging Cheat Sheet

## 1. 🐞 Read the Error Message
- **Start with the first few lines**: They usually contain the exact line of failure.
- Look for:
  - **Error Type**: `TypeError`, `ReferenceError`, `SyntaxError`, `RangeError`, etc.
  - **What failed**: e.g., `"Cannot read properties of undefined (reading 'createAirport')"`
  - **Where**: File path and line number.

## 2. 🔍 Identify the Line of Failure
- Go to the **file and line number** mentioned.
- **Check the variable/object** being accessed.
- Add `console.log()` **right before the line** to check if the variable is:
  - `undefined`
  - `null`
  - Unexpected data type (e.g., expecting an object but got a string)

## 3. 💥 Common Crash Reasons & Fixes
### 🔸 TypeError: Cannot read properties of undefined
- You're accessing `.something` on an undefined value.
- Fix:
  - Log the variable before access.
  - Ensure the object exists.

### 🔸 ReferenceError: xyz is not defined
- You’re using a variable/function before declaring or importing it.
- Fix:
  - Check your `require` or `import`.
  - Verify the spelling and scope.

### 🔸 RangeError [ERR_HTTP_INVALID_STATUS_CODE]
- You’re returning a response with an undefined or invalid status code.
- Fix:
  - Check if `statusCode` is being passed or returned correctly.
  - Add a fallback default: `res.status(err.statusCode || 500)`

### 🔸 SyntaxError
- Usually a typo or missing `}` / `)` / `;`
- Fix:
  - Read the error line and nearby lines carefully.

## 4. ✅ Checklist Before Blaming Others
- [ ] Have you restarted the server after changes?
- [ ] Have you saved all files?
- [ ] Did you `console.log` variables to understand their values?
- [ ] Have you checked module exports/imports?

## 5. 📦 Module/Import Errors
- Check that the file **exports** the function or object correctly.
- Check that your **path is correct** in the `require` or `import`.
  ```js
  module.exports = new AirportService(); // not just AirportService
  ```

## 6. 📌 Steps to Debug Effectively

### 🔁 Step-by-step:
1. Read full stack trace top-down.
2. Identify exact error and line.
3. Console log any involved variables before the error line.
4. Trace back: Who is calling this? What are they passing?
5. Check your imports/exports.
6. Check if it works in other modules/services. If yes, **diff** them.
7. Log full flow:
   ```js
   console.log("Inside createAirportController");
   console.log(req.body);
   ```

## 7. 🛠 Tools You Can Use
- `console.log()` everywhere.
- `debugger;` keyword + run with `node inspect filename.js`.
- Use VS Code's Debug panel (set breakpoints).
- Use `try/catch` blocks to narrow errors.

## 8. 📚 Log Style You Can Use
```js
console.log("[AirportController] req.body: ", req.body);
console.log("[AirportService] response: ", response);
```

## 9. 📁 Logging AppError
- Always log when creating an AppError:
  ```js
  console.error("AppError: ", new AppError("message", 400));
  ```

## 10. 🚀 How to Learn from Errors
- Always read the **first 5 lines** of the error.
- Google the error **exactly** as it appears.
- Build a `mistake-log.md` file in Obsidian for recurring issues.

## 11. 🧹 Final Tips
- Clean up your `console.log`s once fixed.
- Write a helper method for standard error handling.
- Add fallback values to prevent crashes:
  ```js
  const code = err.statusCode || 500;
  const message = err.explanation || "Something went wrong";
  ```

---
> ✍️ Pro Tip: After solving the issue, write **"What was wrong and why"** in your daily dev diary or `mistakes.md` file in Obsidian.
```
